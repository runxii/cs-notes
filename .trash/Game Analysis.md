---
lastSync: Mon Sep 30 2024 09:51:38 GMT+0100 (爱尔兰标准时间)
---
## Perspectives
+ first-person
	+ adds to the believability of the world
	+ immersion factors
+ third-person 
	+ "over-the-shoulder"
	+ more environment can be seen
+ top-down
	+ like hovering cameras
	+ tactical and micro-management
+ isometric
	+ 2.5D
+ flat
+ side-view
+ text-based

## A Game's Internal Economy
### Resources
>anything that can be measured numerically
+ ammunition: bullets, warheads, bombs, missiles, grenades etc.
+ time (normally disappears by itself), speed
+ player's units (in strategy games)

**tangible <-> intangible**
+ medical kits <-> health points
+ trees <-> lumber (after being harvested)
### Sources
>create new resources out of nothing
+ found clips, medical kits, spawn points
### Drains
>take resources out of the game, **reducing** the amount stored in an entity and permanently deleting them
+ (in shooter games, ammunition is drained by) firing weapon 
+ being hit by an enemy, death

### Traders
>move one resource from one entity to another, and move the other resource in an opposite direction
+ use money to buy (exchanged, no creation or destroy)
## Representational - Abstract

## The flow

``` mermaid
graph TD
    A[Player Airplane] -->|Shoots| B[Enemy Planes]
    B -->|Destroyed| C[Points]
    B -->|Destroyed| D[Power-ups]
    B -->|Collides| E[Lose Life]
    A -->|Collects| D
    D -->|Enhances| A
    E -->|Reduce| F[Lives]
    F -->|When 0| G[Game Over]
    A -->|Avoids| B
    A --> H[Survive Waves]
    H --> I[Progress to Next Level]

```