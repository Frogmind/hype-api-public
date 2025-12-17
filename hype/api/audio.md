# Audio

## API Reference

## playAudio

Plays an audio asset (music or one-shot SFX).

### Signature

```luau
hype.audio.playAudio(audio: AudioAsset|integer, extraParams: { looping: boolean?, position: vector?, tune: number?, volume: number?, tuneVariation: number? }?): ()
```

### Parameters
- audio - handle returned by hype.asset.findAudio
- extraParams - optional playback parameters
  - extraParams.looping - loop playback (default: false)
  - extraParams.position - plays as 3D sound from this position when provided
  - extraParams.tune - semitone offset, clamped to [-12, 12] (default: 0)
  - extraParams.volume - linear volume multiplier, clamped to [0, 2] (default: 1)
  - extraParams.tuneVariation - random +/- variation fraction of an octave, clamped to [0, 1] (default: 0)

### Notes
- Streaming (music) assets play once by default; set extraParams.looping to loop
- SFX assets create a transient one-shot unless extraParams.looping is true
- Silently ignores invalid ids

## onMusicStart

Registers a listener that fires when music playback starts.

### Signature

```luau
hype.audio.onMusicStart(listener: function): Subscription
```

### Notes
- Listener receives the started music id as the first argument (empty if unavailable)

## onMusicStop

Registers a listener that fires when music playback stops.

### Signature

```luau
hype.audio.onMusicStop(listener: function): Subscription
```

### Notes
- Listener receives the stopped music id as the first argument (empty if unavailable)
