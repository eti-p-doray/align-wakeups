# How to try Timers coalescing

Timers coalescing is available behind a flag in Chrome 100.0.4876.0
and above. To enable it, navigate to chrome://flags and enable the
"#align-wakeups" feature.

After enabling the feature, run this code in Chrome:

```javascript
let last = performance.now();
function onTimer() {
    setTimeout(onTimer, 5);
    let now = performance.now();
    console.log(`Elapsed: ${Math.round(now - last)} ms`);
    last = now;
}
onTimer();
```

Notice that there is approximately 8ms between each invocation of
the `onTimer()` function.
