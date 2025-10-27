# Experimental

## API Reference

## tts

Speaks the given text using system text-to-speech.

### Signature

```luau
hype.experimental.tts(text: string, opts: { voice: number?, rate: number?, pitch: number?, volume: number? }?): ()
```

### Parameters
- text - text to speak immediately
- opts.voice - voice id (default 0)
- opts.rate - speech rate in [0,1] (default 0.5)
- opts.pitch - speech pitch in [0,1] (default 0.5)
- opts.volume - local volume in [0,1] (default 0.5)
