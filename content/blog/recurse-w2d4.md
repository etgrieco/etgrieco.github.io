---js
const title="Recurse: W2D4"
const date="2025-02-27"
const tags="recurse"
---

# Recurse center: W2D4

After getting into the basics of [ECS](https://en.wikipedia.org/wiki/Entity_component_system) and [koota](https://github.com/pmndrs/koota)


Most of my coding time was dedicated towards doing some maintenance and general code pattern making around organizing the parts.

Turns out the simplest way to go about it is to segregate Entity-Component-System by entity, component ("trait"s), and system definitions.

All changes made for the koota migration are captured [in this pull request](https://github.com/etgrieco/space-invaders-p5-koota/pull/1). 

Ultimately, the "main" method for our game simulation is now organized as follows

1. When the game simulation is started, [do some one-off resource creation](https://github.com/etgrieco/space-invaders-p5-koota/blob/25097131c24478922eb1637e865c0bb77af8e12d/src/scenes/gameSimulation.ts#L87-L147). This includes setting up listening for the controller inputs, setting up basic level entities, and setting up the initial state
1. Set up a method for every tick. Every tick, [run through each of the systems](https://github.com/etgrieco/space-invaders-p5-koota/blob/25097131c24478922eb1637e865c0bb77af8e12d/src/scenes/gameSimulation.ts#L170-L212) to perform updates on the underlying components per-entity. Concepts that are beginning to merge are "game logic systems" and "draw" systems. The game logic systems depends upon the game state only, and is about making changes to that game state. The "draw" systems then take this processed game state, and determines what to draw on the screen based on this info.

While improving basic code organization, some logic was improved as well -- I learned about [axis-aligned bounding boxes](https://en.wikipedia.org/wiki/Minimum_bounding_rectangle), and this was a rather quick way to get collision detection working. I'm happy overall that the bounding box and drawing logic are completely independent of one-another, which feels much better than where I was with working on binary sort a week ago.

## Some things I'm unhappy about

Thinking through what I should do with "systems" [like this](https://github.com/etgrieco/space-invaders-p5-koota/blob/25097131c24478922eb1637e865c0bb77af8e12d/src/scenes/gameSimulation/adhocSystems.ts#L17). Here, I am simply calling it an 'adhoc' system, and having it operate on a single entity. As designed, functions that receive an entity alone are kind of weird, and probably an anti-pattern. There are 'hidden' parts of the contract as-is that say "oh, by the way this better be a `Position` and `Velocity`-based entity, or this won't work. These are all code-smells to me.

Perhaps the solution is -- turn everything into a system, even if it feels like a one-off. Think if there's some kind of extractable behavior. For example, perhaps there is something like a 'route' that this entity should follow, and there's a systemic relationship between 'routes', 'positions', and velocities? Perhaps it is really that simple. I'll give it a shot tomorrow.

On the one hand, in these ambiguous one-off cases, I'm happy to leave it alone. Gives me time to find the right abstraction. 

The nice thing here, at least, is that the wrong abstraction does not appear to be as 'expensive' as when the same wrong abstraction is selected for in OOP. 


## Some things to work on tomorrow

- Look into turning swarm behavior into a system
- Fix controls by using an input queue and handle inputs per-tick
- Add some interesting effects, especially lighting
    - since the game logic is completely de-coupled from the view, consider experimenting with other drawing strategies?
- update koota to 0.2.0. I [posted an issue](https://github.com/pmndrs/koota/issues/54) today, which got fixed by this release.
- Perhaps create a github action for building and publishing assets per-merge to main, for long-term tracking of progress

## Some things on the horizon

- Recurse's "impossible" day. Is that when some kind of client-server interaction should be handled
- A game jam -- a game jame is being scheduled for sometime next week, it seems. that would take me off my current project for a bit, but game jams are fun.

Here is the current code [snapshot](https://github.com/etgrieco/space-invaders-p5-koota/commit/930805e2ba6031396e5df1f2e6c66d4ea3b6ebf5) of my implementation for the day

[Here are the built assets that can be played with on the website.](/blog-assets/recurse-w2d4/space-invaders-demo/index.html)