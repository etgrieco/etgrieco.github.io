---js
const title="Recurse: W3D1"
const date="2025-03-03"
const tags="recurse"
---

# Recurse - W3D1

Today I iterated on my [space invaders game](https://github.com/etgrieco/space-invaders-p5-koota) to learn some new skills working with Three.js
- l[oad custom assets](https://github.com/etgrieco/space-invaders-p5-koota/blob/a2aba95d68f9db8be7fcabd687e7c0666778bf51/src/main.ts#L16-L26)
- scale those custom assets properly to the game engine
- Refine 3d collision handling
- [make some basic scene lighting](https://github.com/etgrieco/space-invaders-p5-koota/blob/a2aba95d68f9db8be7fcabd687e7c0666778bf51/src/main.ts#L40-L42) (for the custom asset)


A lot of this was about getting to grips with more confort with dealing with numbers and entities in 3D space. At this point, I'm pretty satisfied with space invaders as a learning exercise, both for orchestrating a game engine/logic in general, and also for learning some basics of 3D programming.

A snapshot of the product can be [played here](/blog-assets/recurse-w3d1/space-invaders-demo/index.html) (arrows, move; "v" to shoot)

<p id="space-invaders-demo-video-desc" class="visually-hidden">
  Space invaders demo at end of day W31D1
</p>
<video controls width="640" height="360" aria-describedby="space-invaders-demo-video-desc">
    <source src="/blog-assets/recurse-w3d1/space-invaders-demo-w3d1.mp4" type="video/mp4">
</video>
