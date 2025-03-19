---js
const title="Recurse: W5D2"
const date="2025-03-18"
const tags="recurse"
---

# Recurse - W5D2

Another check-in about today, and hopefully some catch up since [the last one](./recurse-w4d1) as well!

My goal last week was to get the multiplayer project to be robust and recoverable across 'lost signals'. It's not 100% , but it definitely recovers and handles HMR elegantly across many cases, including client and server restarts.

Here's a demo:

<p id="multiplayer-game-demo-w5d2-video-desc" class="visually-hidden">
  Demo of multiplayer game project, W5D2
</p>
<video controls width="640" height="360" aria-describedby="multiplayer-game-demo-w5d2-video-desc">
    <source src="/blog-assets/recurse-w5d2/w5d2-demo-lost-signals-demo.mp4" type="video/mp4">
</video>


Here's a snapshot of [where I'm currently at with the project](https://github.com/etgrieco/game-ws-multiplayer-experiment/tree/0e3bbd75f50e7454cd0158a945c6da6b3a86c147)


Here are some new things I learned today while adding features:
- Controls, with [leva](https://github.com/pmndrs/leva/)
- An orbital control camera, and other niceties, with [drei](https://github.com/pmndrs/drei)
- [Followed along with this playlist](https://www.youtube.com/playlist?list=PLtzt35QOXmkKkZL63E3IXDxqvP13MHyTE) as inspiration for setting up cameras, flat terrain plains, etc. It's written in non-React Three.JS, plus taking on the additional challenge of having things work in a multiplayer (server/client) setup.

I also went through with a refactor to potentially allow for >2 players, in case a gameplay idea comes out of that. It also gives me some more flexibility in how I handle sending updates from the server; for example, I may only update some players, not all, per-update message send.

## Looking back --

Since last week, the major improvements were primarily around the organization of the web socket state machine, both on web and server. It's still a quite 'loose' state machine at this point, and potentially prone to unexpected behaviors. I wanted some flexibility still at this point, but basically I organized my states as follows:

The state of the game, according to the client:
```ts
type GameMachineState =
  | {
      name: "INIT";
    }
  | {
      name: "SESSION_CONNECTED_WITH_GAME_PLAYING";
    }
  | {
      name: "SESSION_CONNECTED_WITH_GAME_READY";
    }
  | {
      name: "SESSION_CONNECTED_WITH_GAME_WAITING_PLAYER";
    };
```

"Transitions"/events that can be triggered by the server, and cause changes between these states

```ts
export type MultiplayerGameStatus =
  | "PAUSED_AWAITING_START"
  | "PAUSED_AWAITING_PLAYERS"
  | "PLAYING";
```

which come packaged in updates like:

```ts
{
  type: "GAME_STATUS_UPDATE";
  id: string;
  data: {
    sessionId: string;
    gameStatus: MultiplayerGameStatus;
  };
};
```

I should perhaps think on if there's a mistake here -- is it worth it to unify the state definitions between client and server? That may make things a bit simpler to follow as the application grows.

But that would require another refactor, and may push forward on adding gameplay features instead, and return back to this part as a cleanup later.
