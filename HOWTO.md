# How to try Throttling of Foreground Timers

Throttling of Foreground Timers is available behind a flag in Chrome 99.0.4844.0
and above. To enable it, navigate to chrome://flags and enable the
"#throttle-foreground-timers" feature.

After enabling the feature, run this code in Chrome:

```javascript
let last = performance.now();
function onTimer() {
    setTimeout(onTimer, 2);
    let now = performance.now();
    console.log(`Elapsed: ${Math.round(now - last)} ms`);
    last = now;
}
onTimer();
```

Notice that approximately there is approximately 32ms between each invocation of
the `onTimer()` function.