# Echo Runner — Game Concept

## The Idea
A circular-track endless runner where your past decisions physically haunt you.

## Core Loop
1. The player is a glowing orb that runs automatically around a circular track
2. Only the bottom 20-30% of the circle is visible in the viewport (looks like running on a planet surface)
3. Pre-placed crystal spike obstacles are positioned around the track
4. Every **5 seconds**, a ghost of the player is permanently placed at the player's exact position
5. Ghosts come back around every lap — dodge them or die

## What Makes This Unique
- **No existing game** combines circular track + partial viewport + self-generated ghost traps on the same loop
- The player gains map knowledge (memorizing static obstacles) but simultaneously loses safety (ghosts fill the track)
- Natural difficulty curve: the longer you survive, the more dangerous the track becomes — no artificial speed is needed
- The "I trapped myself!" death moment is extremely shareable and creates a social hook

## Difficulty Progression
| Time | State |
|------|-------|
| 0-20s | Learn static obstacles, no ghosts yet |
| 20-40s | First 4-6 ghosts deployed, track getting crowded |
| 40-80s | 8-12 ghosts, every lap is a minefield |
| 80s+  | 15+ ghosts, near-impossible, legendary runs |

## Player Experience Goals
- **First 10 seconds:** "Oh this is easy, I get it"
- **30 seconds:** "Oh no, my ghost is right there..."
- **60 seconds:** "I created this nightmare myself"
- **Death:** Instant retry urge

## Ghost Mechanic — Detailed
- Ghost placement is automatic (5-second interval, no player control)
- Ghost's circle position is locked from the moment of deployment
- On each subsequent lap, the ghost reappears at the same track location
- Ghost is semi-transparent cyan, pulsing gently — looks eerie next to the solid player
- Jumping over a ghost IS possible (it requires timing, same as an obstacle)
- Ghost collision hitbox is slightly smaller than a static spike (more forgiving)
