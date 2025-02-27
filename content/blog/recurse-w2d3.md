---js
const title="Recurse: W2D3"
const date="2025-02-26"
const tags="recurse"
---

# Recurse center: W2D1-2

Today, I attempted to do a deep dive into some of the fundamentals of ECS architectures, and how perhaps this could be useful for layering into the game.

[Here is the diff](https://github.com/etgrieco/space-invaders-p5-koota/compare/f968cc2198eb548095502eb99466d524c1c301ab...187a92e0ec867fe8e2e96cd5681baa00075ca34c) of things I got done migrating from "naive, POJO" logic to [koota](https://github.com/pmndrs/koota)

The promises for using this library/state architecture was:
- composability of behaviors ("components") at a per-entity level
- composability of these behaviors into "systems" that would dictate how components interact with each other

The results we hope to get from this are:
- Fun, flexible ways to put these behaviors together as a game evolves
- Easy ways to refactor things as new 'concepts' for components/systems emerge from the development project.

Overall, the migration was pretty smooth. Spoke with [krispya](https://github.com/krispya) a bit about strategies used, asked questions about whether I was 'doing it right'.

Here is a snapshot build of the game in the current state [at this commit](https://github.com/etgrieco/space-invaders-p5-koota/commit/187a92e0ec867fe8e2e96cd5681baa00075ca34c).

[Play "space invaders" progress at W2d3 here](/recurse-w2d3/space-invaders-demo/index.html)


