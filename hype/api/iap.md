# IAP

## API Reference

## purchase

Requests an in-app purchase for credits.

### Signature

```luau
hype.iap.purchase(price: number, text: string, listener: function): ()
```

### Parameters
- price - cost of the purchase
- text - message shown to the player in the purchase prompt
- listener - callback invoked once the purchase completes with boolean succeeded
