---js
const title="Recurse: W5D5"
const date="2025-03-21"
const tags="recurse"
---

# Recurse W5D5 update

Other than mostly fighting a bad cold the past week, made some progress on adding some features to my game

- Adds some terrain features from the server, for synchronization among all clients
- Add an isometric camera perspective
- Add more natural movement (in the isometric perspective)
- Camera following the player

Here's a demo

<p id="w5d5-demo-video-desc" class="visually-hidden">
    W5D5 multiplayer game demo
</p>
<video controls width="640" height="360" aria-describedby="w5d5-demo-video-desc">
    <source src="/blog-assets/recurse-w5d5/w5d5-demo.mp4" type="video/mp4">
</video>

And here's [the snapshot](https://github.com/etgrieco/game-ws-multiplayer-experiment/tree/648a510dad76629d44018ece412c9b1fb1cbb781) of where I'm at.

Challenges during this part were getting the isometric orientation and orthographic camera right. Using the [leva library](https://github.com/pmndrs/leva) helped a lot for making quick changes and getting some intuition around moving around the 3D space.