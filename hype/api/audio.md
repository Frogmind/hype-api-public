# Audio

## API Reference

## playAudio

Plays an audio asset (music or one-shot SFX).

### Signature

```luau
hype.audio.playAudio(audio: AudioAsset|integer): ()
```

### Parameters
- audio - handle returned by hype.asset.findAudio

### Notes
- Streaming (music) assets play once (non-looping)
- SFX assets create a transient one-shot
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
