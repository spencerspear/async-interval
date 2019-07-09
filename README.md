# Async-Interval
An enhanced implementation of setInterval for promises and async functions available in Node.js.

## Syntax
```javascript
const interval = new AsyncInterval(fn, timeout[, options[, param1, param2, ...]]);
```

### Parameters
1. `fn` - An async function that should be called repeatedly.
1. `delay` - Number of milliseconds between the resolution/rejection of the last `fn` call and the starting of the next `fn` call.
1. `options` - Options
1. `options.count` - The number of times to repeat. If not set, or `0`, will repeat indefinitely. __(Default: `0`)__
1. `options.timeout` - the amount of time in milliseconds before executing the first call to `fn`. A value of `0` invokes `fn` immediately then starts the interval. __(Default: `delay`)__
1. `options.errorCount` - The number of errors to allow before triggering the `ERROR_COUNT_ACHEIVED` event. This counter resets to 0 if `fn` resolves. __(Default: `0`)__
1. `options.stopOnError` - If `true`, no subsequent calls to `fn` will be made when `options.errorCount` is reached.
1. `param1, ..., paramN` - The params to be passed to `fn`

### Return Value
An instance of AsyncInterval.

### Events

#### AsyncInterval
1. `started` - Triggered when the interval instance is started.
1. `paused` - Triggered when the interval instance is paused.
1. `cancelled` - Triggered when the interval instance is cancelled externally.
1. `done` - Triggered when the interval instance has been executed `options.count` times.
1. `error` -Triggered when the interval instance has failed to execute `options.errorCount` times in a row.
1. `stopped` - Triggered when the interval instance is stopped because the `options.errorCount` is reached and `options.stopOnError` is true.

#### AsyncInterval.func
1. `success` - Triggered each time that `fn` resolves.
1. `error` - Triggered each time that `fn` rejects with an error.

## Examples

```javascript
const interval = new AsyncInterval(fn, timeout[, options[, param1, param2, ...]]);

interval.on('started', () => { ... });
interval.on('paused', () => { ... });
interval.on('cancelled', () => { ... });
interval.on('done', () => { ... });
interval.on('error', (e) => { ... });
interval.on('stopped', (e) => { ... });

```

```javascript
const interval = new AsyncInterval(fn, timeout[, options[, param1, param2, ...]]);

interval.func.on('success', () => { ... });
interval.func.on('error', (e) => { ... });
```
