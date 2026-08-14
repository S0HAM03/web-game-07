# Echo Runner 3D — Game Concept

## The Idea
A top-down 3D endless runner on a massive rotating disc where your past decisions physically haunt you.

## Core Loop
1. The player is a glowing 3D orb running automatically on a giant rotating disc platform.
2. The disc rotates underneath the player, creating forward momentum.
3. The player can steer left and right (strafing across different radial lanes) and jump over obstacles.
4. Pre-placed glowing red 3D crystal spikes are positioned around the disc track.
5. Every **5 seconds**, a translucent ghost of the player is permanently dropped at the player's exact location and lane.
6. Ghosts become children of the rotating disc, meaning they orbit back around every lap — dodge them or die.

## What Makes This Unique
- **True 3D Spatial Traps:** You aren't just jumping; you are weaving between lanes.
- The player gains map knowledge (memorizing static obstacles) but simultaneously loses safety (ghosts fill the lanes).
- Natural difficulty curve: the longer you survive, the more dangerous the disc becomes.
- The "I trapped myself!" death moment is extremely shareable and creates a social hook.

## Player Experience Goals
- **First 10 seconds:** "Oh this is easy, I get the steering."
- **30 seconds:** "Oh no, my ghost is in my favorite lane..."
- **60 seconds:** "I created this nightmare myself."
- **Death:** Instant retry urge.

## Ghost Mechanic — Detailed
- Ghost placement is automatic (5-second interval, no player control).
- Ghost's position (angle and radius on the disc) is locked from the moment of deployment.
- On each subsequent lap, the ghost reappears at the exact same track location and lane.
- Ghost is semi-transparent cyan, pulsing gently — looks eerie next to the solid gold player.
- Jumping over a ghost IS possible, as well as steering around it.
