---js
const title="Recurse: W4D1"
const date="2025-03-10"
const tags="recurse"
---

# Recurse - W4D1

Haven't checked in most of last week.

The theme of a game jam started within Recurse is "Lost Signals" -- building on some work from "impossible day", I am going to focus on getting a good framework setup for multiplayer connectivity. I want it to be robust as the game reloads (due to HMR development), in addition to having resiliency when a websocket connection breaks.

Here's a snapshot of [where I'm currently at with the project](https://github.com/etgrieco/game-ws-multiplayer-experiment/tree/0971080d106bba81a002d1d4c56d1bd66ba6656c)

Here is a quick demo of what works, as-is:

<p id="multiplayer-game-demo-w4d1-video-desc" class="visually-hidden">
  Space invaders demo at end of day W31D1
</p>
<video controls width="640" height="360" aria-describedby="multiplayer-game-demo-w4d1-video-desc">
    <source src="/blog-assets/recurse-w4d1/w4d1-demo.mp4" type="video/mp4">
</video>

Unfortunately, this one is not online yet, as it requires a websocket server up to work!


Here are some cool 'lost signals connections' that do work:
- when a client disconnects or refreshes, it can reconnect to the active session
- when the server closes, it dumps a JSON snapshot of the currently running games so they can be restore and resumed

