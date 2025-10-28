# Game Modes

## REMOTE

## Hype level callbacks (Remote)

### onInit()
- Called first
- Subscribe to signals
- Initialize default values

```luau
function EventEliminateRemote:onInit()
	-- Listen to eliminations
    hype.remoteSignal.subscribe({ id = "G_Eliminate_Eliminated" }, self, self.onPlayerEliminated)
	self:reset()
end

-- Reset helper function
function EventEliminateRemote:reset()
	self.playerIdxToTeamIdx = nil
    self.leaderboard = {}
end
```

### onStart()
- Called after onInit()
- Register the game mode

```luau
function EventEliminateRemote:onStart()
	hype.localSignal.send({ id = "GM_RegisterGameMode" }, self, {
		name = "Eliminate",
		duration = 1000,
		maxTeams = 0,
	})
end
```

## Game manager callbacks (Remote)

### create()
- Called exactly once when the game is started
- Initialize and reset values that can change between runs of the same game

```luau
function EventEliminateRemote:create()
	self:reset()
	self.randomSeed = math.random(1, 10000)
end
```

### prepare(playerIndex: number?)
- Called when the game is launched (playerIndex == nil) and each time someone joins mid-session (playerIndex specified)
- During prepare, allow new players to join before launch
- Usually game map is spawned here, notify the local script to prepare (e.g., spawning)

```luau
function EventEliminateRemote:prepare(playerIndex: number?)
	-- Let local script know about prepare
	hype.remoteSignal.send({ id = "G_Eliminate_Prepare", playerIndex = playerIndex })
end
```

### activate(playerIndex: number?, playerIdxToTeamIdx: table, numTeams: number)
- Called when gameplay launches (playerIndex == nil) and when someone joins mid-session (playerIndex specified)
- playerIdxToTeamIdx maps player → team. If maxTeams == 0, each player still maps to a sequential team index
- Easiest way to track “still in game” is by tracking team index (clients listen to MM_AssignTeam)
- numTeams tells how many teams matchmaking formed

```luau
function EventEliminateRemote:activate(playerIndex: number?, playerIdxToTeamIdx: table, numTeams: number)
	-- Store the team mapping even in no-team games
	self.playerIdxToTeamIdx = playerIdxToTeamIdx
	-- Let local script know about activate
	hype.remoteSignal.send({ id = "G_Eliminate_Activate", playerIndex = playerIndex }, numTeams, self.optLevelIdCurrent)
end
```

### deactivate()
- Called when the game is completely stopped

```luau
function EventEliminateRemote:deactivate()
	hype.remoteSignal.send({ id = "G_Eliminate_Deactivate" })
end
```

### onPlayerLeft(playerIdx)
- Called when a player leaves the session mid-game

```luau
function EventEliminateRemote:onPlayerLeft(playerIdx)
	if self.playerIdxToTeamIdx == nil then
		print("Player left but game not started")
		return
	end
    if self.playerIdxToTeamIdx[playerIdx] ~= nil then
		print("Player left during game")
        self.playerIdxToTeamIdx[playerIdx] = nil
		self:checkStatus()
	else
		print("Player left but not in game")
    end
end
```

## Game mode custom functions (Remote)

```luau
function EventEliminateRemote:onPlayerEliminated(player)
    if self.playerIdxToTeamIdx == nil then
		return
	end
    if self.playerIdxToTeamIdx[player.index] ~= nil then
		print("Player eliminated")
        self.playerIdxToTeamIdx[player.index] = nil
        table.insert(self.leaderboard, player.index)
		self:checkStatus()
    end
end

function EventEliminateRemote:buildFinalLeaderboard()
    local leaderboard = {}

    -- The last inserted player is the winner (highest score)
    local totalPlayers = #self.leaderboard
    if totalPlayers == 0 then
        return
    end

    for idx, playerIdx in ipairs(self.leaderboard) do
        -- score: earlier eliminations get lower scores
        local score = idx
        leaderboard[playerIdx] = score
    end
    hype.localSignal.send({ id = "GM_Scoring_SetScores" }, leaderboard)
	hype.remoteSignal.send({ id = "G_Eliminate_Done" })
end

function EventEliminateRemote:checkStatus()
    if self.playerIdxToTeamIdx == nil then
        return nil
    end

    local lastPlayer = nil
    local count = 0

    for playerIdx, teamIdx in pairs(self.playerIdxToTeamIdx) do
        if teamIdx ~= nil and teamIdx >= 1 then
            count = count + 1
            lastPlayer = playerIdx
        end
    end

    if count == 1 then
        print("Player " .. lastPlayer .. " wins!")
        table.insert(self.leaderboard, lastPlayer)
        self:buildFinalLeaderboard()
        return lastPlayer
    elseif count == 0 then
        print("No players left.")
        self:buildFinalLeaderboard()
        return nil
    else
        print(count .. " players still in the game.")
        return nil
    end
end
```

## LOCAL

## Hype level callbacks (Local)

### onInit()
- Subscribe to signals
- Initialize default values

```luau
function EventEliminateLocal:onInit()
  hype.localSignal.subscribe({ id = "G_Eliminate_ShowOptions" }, self, self.onShowOptions)
  hype.remoteSignal.subscribe({ id = "G_Eliminate_Activate" }, self, self.onActivate)
  hype.remoteSignal.subscribe({ id = "G_Eliminate_Deactivate" }, self, self.onDeactivate)
  hype.remoteSignal.subscribe({ id = "G_Eliminate_Prepare" }, self, self.onPrepare)
  hype.remoteSignal.subscribe({ id = "G_Eliminate_Done" }, self, self.onDone)
  hype.remoteSignal.subscribe({ id = "MM_AssignTeam" }, self, self.onAssignTeam)

  self.rewardMoneyDefault = 50
  self.rewardMoneyTopN = {
      500, 450, 400, 350, 300, 250, 200, 150, 100, 50
  }
end

-- Helper reset function
function EventEliminateLocal:reset()
    self.team = -1
end
```

### onStart()
- Called after onInit()

```luau
function EventEliminateLocal:onStart()
end
```

## Game manager callbacks (Local)

### onShowOptions(myGameModeId: number)
- Called when game launch is initiated
- Sending GM_GameModeStart instantly will skip any settings process (like selecting a map)

```luau
function EventEliminateLocal:onShowOptions(myGameModeId: number)
  self.gameModeId = myGameModeId
  hype.localSignal.send({ id = "GM_GameModeStart" }, myGameModeId)
end
```

### onAssignTeam(teamIdx: number)
- if subscribed to MM_AssignTeam, players own team index will be received here

```luau
function EventEliminateLocal:onAssignTeam(teamIdx: number)
  self.team = teamIdx
end
```

## Game mode custom callbacks from remote (for reference)

```luau
function EventEliminateLocal:onDone()
end

function EventEliminateLocal:onPrepare()
  self:reset()
  hype.localSignal.send({ id = "GM_Scoring_SetupRewardMoney" }, self.rewardMoneyTopN, self.rewardMoneyDefault)

  game:getService("Modes"):setPositionJoin(spawnPos)
  game:getService("Modes"):enableAutoTeleport(false)
  local spawnPos = game:getService("Modes"):getPositionSpawn()
  print("GM: Prepare Eliminate at "..spawnPos.x..", "..spawnPos.y..", "..spawnPos.z)
  
  local prefab = hype.asset.findPrefab("EventEliminate")
  self.spawnedObject = hype.world.spawn(
    prefab,
    spawnPos,
    nil,
    vector.create(1, 1, 1)
  )
end

function EventEliminateLocal:onActivate(numTeams: number, levelId: number)
  print("GM: Activate eliminate with " .. numTeams .. " teams. Local player is on team " .. self.team)
  if self.team >= 1 then
    --game:getService("Player"):setFallPosition(1)  
    self.updateSub = hype.core.events.onUpdate(self, self.onUpdate)
  end
end

function EventEliminateLocal:onDeactivate()
  if self.spawnedObject ~= nil then
    hype.world.destroy(self.spawnedObject)
    self.spawnedObject = nil
  end
  self.team = -1
  if self.updateSub ~= nil then
    self.updateSub:unsubscribe()
    self.updateSub = nil
  end  
end
```

## Game mode custom local functions (for reference)

```luau
function EventEliminateLocal:onUpdate(dt: number)
  -- Handle ingame
  if self.team >= 1 then
    local pl = hype.player.getLocal()
    if pl.entity == nil then return end
    local pos = pl.entity:getPosition()
    if pos.y < 1.0 then
      self:eliminateMyself(pl)
    end
  end

end

function EventEliminateLocal:eliminateMyself(player)
  print("Eliminate: Myself")
  hype.remoteSignal.send({ id = "G_Eliminate_Eliminated" })
  self.team = -1
  game:getService("Player"):teleport(game:getService("Modes"):getPositionSpectate())
end
```
