# Throttle DOM Timers to 30 Hz on Foreground Pages

## Proposed Change

Run all timers (with a few exceptions) with a non-zero delay on a regular 125 Hz tick, instead of as soon as their delay has passed.

This affect DOM timers; On foreground pages, run DOM timers with a non-zero delay on a regular 125 Hz tick, instead of as soon as their delay has passed.
On background pages, DOM timers already run on a regular 1 Hz tick (or even less frequently after 5 minutes).

## Motivation

DOM Timers running at more than 125 Hz can almost always be replaced with alternative APIs that provide a better user experience and consume less resources, as explained in this [blog post](https://developer.chrome.com/blog/timer-throttling-in-chrome-88/#workarounds).

Throttling DOM Timers to 125 Hz will incentivize some Web developers to switch to these alternative APIs. At the same time, content isn't updated will consume less resources, because timers will run less often.

An experiment on the Beta channel shows that this reduces Chrome's Energy Impact by 10% on Mac.

## Spec

The
[spec](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#run-steps-after-a-timeout)
already allow adding arbitrary delays to DOM Timers ("Optionally, wait a further
implementation-defined length of time.").
