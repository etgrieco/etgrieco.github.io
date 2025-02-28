---js
const title="Recurse: W2D5"
const date="2025-02-28"
const tags="recurse"
---

# W2D5

Today I took on one of the ideas I thought about yesterday -- moving the game to another rending engine.

I decided that the next step in my journey would be seeing how well the game ported over to a 3d engine -- [three.js](https://threejs.org/). Here is a snapshot of [all those changes](https://github.com/etgrieco/space-invaders-p5-koota/commit/c1c14b43a2e9a035a740a9e7369c0aff14655ea8).

The biggest thing I had trouble with the two different drawing models -- p5.js basically had me clearing the canvas and re-drawing every frame. For three.js, I had to perform per-frame updates to underlying object meshes. What I ended up doing was attaching the meshes to the entities directly, and performing a separate "mesh draw" system for these. Ultimately, the most vital thing to do was updates to position over time. Other properties, such as rotation, are not currently tracked in the game engine, but could be added later.

The other thing I had trouble with was that the coordinate systems are completely different -- as a result, I either have to 1) do some kind of transformation during the draw logic to the 'coordinate assumptions' underlying all of my logic or 2) completely re-write the position logic to fit this new system.

For now, I just let the problem exist as-is 🙃 -- [you can play the work-in-progress I ended the day with here](/blog-assets/recurse-w2d5/space-invaders-demo)