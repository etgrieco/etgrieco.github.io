---js
const title="Recurse: W2D1-2"
const date="2025-02-25"
const tags="recurse"
---

# Recurse center: W2D1-2

These past two days, I've been working on what I've been calling 'building reps' with building games and animation.

## W2D1 - space invaders clone

On W2D1, started on a space invaders clone to get a feel for [koota](https://github.com/pmndrs/koota) as a state management solution for JavaScript based games in general. I started building it out using p5.js as the drawing layer. Based off my lessons on the last animation, I've done a much better job distinguishing the simulation state and how that model moves over time, from the 'drawing' actions that derive from changes to that state.

Now that it's W2D2, here's [a quick snapshot](https://github.com/etgrieco/space-invaders-p5-koota/commit/f968cc2198eb548095502eb99466d524c1c301ab) for where I've gotten so far. Integrating Koota hasn't quite worked out yet, but here's some reflections on at least distinguishing the simulation from the draw:

I've encapsulated the state + simulation into a lightweight object for now (perhaps, this should just be pure procedures? Not sure.)

```ts
if (gameSceneState.sceneId === "CRAWL_INTRO") {
    gameSceneState.simulation.tick();
    drawIntro(p, gameSceneState.simulation.state);
} else if (gameSceneState.sceneId === "SPACE_INVADERS_GAME") {
    gameSceneState.simulation.tick();
    drawGame(p, gameSceneState.simulation.state);
} else if (gameSceneState.sceneId === "END") {
    // etc.
```

This allows me to break up the different simulations happening into different 'scenes' that run independently of each other.

Right now, I'm controlling the transitions between these scenes in less than optimal ways, by setting up an overly complex machine like so:

```ts
gameSceneState = {
    sceneId: "CRAWL_INTRO",
    simulation: introSimulationFactory(
    p,
    queueNextTick(() => {
        gameSceneState = {
            sceneId: "SPACE_INVADERS_GAME",
            simulation: gameSimulationFactory(
                p,
                queueNextTick(() => {
                    gameSceneState = {
                        sceneId: "END",
                    };
                })
            ),
            };
        })
    ),
};
```

Definitely some cleanup and re-thinking I can do here; I basically came up with my own version of callback hell with what I have here. Trying to create something lightweight, without having to reach for a more robust solution like [xstate](https://xstate.js.org/)

I also ended up publishing the [P5, TypeScript, Vite template](https://github.com/etgrieco/p5-vite-typescript-template). I used this as the starting point for my space invaders game, so it was good to get that out of the way.

## W2D2 - pairing jam

There was a pairing jam set up today for the entirety of the day. I ended up pairing with [rwhaling](https://github.com/rwhaling). The goal there was 1) learn some React, 2) figure out how to get some kind of shared state between our "React world" and our P5.js world and 3) create some fun math-based animations.

I learned a lot, especially on the #3 front. It was also gratifying to be able to [use the template](https://github.com/etgrieco/p5-vite-typescript-template) from the day prior to get some fast environment setup.

We ended up with a finish product meeting our goals. It can be played [with here](https://websiteaboutmy.website/p5-react-test/)

<p id="p5-react-demo-video-desc" class="visually-hidden">
  A demo of the animation using P5.js and React
</p>
<video controls width="640" height="360" aria-describedby="p5-react-demo-video-desc">
    <source src="/blog-assets/recurse-w2d1-2/p5-react-demo-web.mp4" type="video/mp4">
</video>
