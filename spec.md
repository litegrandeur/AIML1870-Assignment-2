# Starfield Particle System Specification

## Overview
A canvas-based starfield effect where particles emanate from a central radius and travel outward toward screen edges, leaving fading trails. Includes rare planets that drift through the scene with parallax movement.

## Technical Requirements
- **Single HTML file** containing all HTML, CSS, and JavaScript
- **Full-screen canvas** that resizes with the browser window

## Particle Behavior
- Stars spawn within a configurable **spawn radius** at screen center
- Movement direction: radially outward from center
- Each star maintains a **trail** of previous positions that fade over time
- Stars reset to spawn area when they exit the viewport
- On initialization, stars are spread across the viewport (not all starting at center) to avoid "bursty" spawning
- Trail fading uses cubic easing for smooth visual appearance

## Trail Rendering
- Trails rendered as line segments with round caps for efficiency
- Each segment has decreasing opacity and width using eased interpolation
- Faster stars maintain consistent trail density (no gaps)

## Visual Style
- Stars rendered as small filled circles
- Trails: tapered line segments with progressively fading opacity
- Dark background (black)

## Planets
- Rare gradient-filled circles that simulate distant celestial bodies
- Spawn near center (50-130px from center) and travel outward
- **Size scaling**: Start at 30% of max size and grow as they move outward (simulates approaching from distance)
- **Fade-in effect**: New planets gradually fade in when spawning
- **Parallax movement**: Move slower than stars (15-30% of star speed) to create depth
- **Color palettes**: Mars red, Neptune blue, Saturn gold, green gas giant, purple, orange desert
- **Glow effect**: Subtle white glow around each planet
- Drawn behind stars so stars pass in front

## Controls Panel
**Location:** Top-left corner, collapsible (click to expand/collapse)

### Sliders
| Control | Range | Default | Description |
|---------|-------|---------|-------------|
| Trail Length | 5–50 | 20 | Number of trail segments per star |
| Star Count | 50–250 | 200 | Total particles in system |
| Star Speed | 1–10 | 3 | Pixels per frame base speed |
| Spawn Radius | 10–200 | 50 | Radius from center where stars appear |
| Planet Frequency | 0–8 | 2 | Number of planets visible at once |

## Animation
- Use `requestAnimationFrame` for smooth 60fps rendering
- Clear canvas fully each frame for clean trail rendering
- Update and draw planets first (background), then stars (foreground)

## File Structure
```
index.html
├── <style> - All CSS inline
├── <canvas> - Full viewport
├── <div> - Collapsible control panel
└── <script> - Particle system logic
    ├── Star class - particle behavior and rendering
    └── Planet class - gradient spheres with parallax
```
