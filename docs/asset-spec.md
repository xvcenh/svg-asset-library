# SVG Asset Specification

Standard format for scene engine SVG assets.

## File Naming

```
{category}/{id}.svg
```

- `characters/warrior.svg` — humanoid characters
- `creatures/dragon.svg` — non-human creatures/monsters
- `objects/chest.svg` — interactable objects
- `items/sword.svg` — holdable/wearable items
- `effects/fire.svg` — visual effects (particles, auras)
- `backgrounds/forest-day.svg` — full-scene backgrounds

## SVG Root Attributes

Every SVG MUST have these attributes on the `<svg>` element:

```xml
<svg xmlns="http://www.w3.org/2000/svg"
     viewBox="0 0 W H"
     data-asset-id="{id}"
     data-layer="{layer}"
     data-tags="{tag1},{tag2},{tag3}"
     data-origin="center-bottom">
```

### viewBox Sizes

| Layer      | ViewBox     | Notes                          |
|------------|-------------|--------------------------------|
| character  | 0 0 120 160 | Humanoids, standing pose       |
| creature   | 0 0 160 160 | Monsters, beasts (square)      |
| object     | 0 0 80 80   | Props, furniture               |
| item       | 0 0 60 60   | Holdable items (smaller)       |
| effect     | 0 0 200 200 | Visual effects, particles      |
| background | 0 0 800 500 | Full-scene backgrounds         |

### data-layer Values

- `character` — humanoids (warrior, mage, merchant, guard)
- `creature` — non-human (dragon, wolf, spider, horse)
- `object` — static props (chest, table, barrel, torch)
- `item` — holdable (sword, potion, scroll, key)
- `effect` — visual (fire, fog, magic-sparkle)
- `background` — full scenes (forest, cave, tavern)

### data-tags

Comma-separated, lowercase, English + Chinese:
```xml
data-tags="dragon,fire,drake,wyrm,龙,火龙,boss,monster"
```

Include: English name, synonyms, Chinese name, category, mood/element.

### data-origin

- Characters/creatures: `center-bottom` (feet position)
- Objects: `center-bottom`
- Effects: `center-center`
- Backgrounds: omit

## Visual Style Guide

### Color Palette (Dark Fantasy)

```
Backgrounds:  #0a0a1a → #1a1a2e → #2a2a4a
Characters:   skin #d4a843, cloth #4a4a5a, metal #8a8a9a
Creatures:    body tones #3a5a3a, #5a3a2a, #2a3a5a
Objects:      wood #6b4a20, metal #8a8a9a, stone #5a5a5a
Effects:      fire #ff6600, magic #a78bfa, ice #88ccff
Highlights:   gold #ffd700, danger #cc3333, safe #33cc66
```

### Character Anatomy (120×160)

```
Head:    ellipse cx=60 cy=35 rx=20 ry=22
Body:    rect x=40 y=55 w=40 h=50 rx=5
Legs:    rect x=44 y=105 w=14 h=35 + rect x=62 y=105 w=14 h=35
Arms:    rect x=28 y=60 w=12 h=40 + rect x=80 y=60 w=12 h=40
Feet:    rect at bottom of legs, darker color
```

### Creature Anatomy (160×160)

- Centered in viewBox
- Body fills 60-80% of space
- Add detail: scales, fur texture via small shapes
- Eyes as bright highlights

### Object Anatomy (80×80)

- Object centered, touching bottom
- 60-70% of viewBox height
- Simple, recognizable silhouette

## Animation (Optional)

Use SMIL `<animate>` for subtle motion:

```xml
<!-- Gentle idle breathing -->
<animate attributeName="opacity" dur="3s" repeatCount="indefinite"
         values="1;0.9;1"/>

<!-- Fire flicker -->
<animate attributeName="d" dur="0.6s" repeatCount="indefinite"
         values="path1;path2;path1"/>
```

Keep animations subtle — the engine handles transitions.

## Adding New Assets

1. Create SVG following this spec
2. Place in correct category folder
3. Run `node scripts/validate.js` to check compliance
4. Asset auto-appears in catalog on next deploy

## Integration with Scene Engine

The scene engine loads assets by ID:
```javascript
// Direct reference
{ "id": "warrior", "gx": 4, "gy": 5 }

// The engine looks for assets/svg/characters/warrior.svg
// Falls back to emoji composition if SVG not found
```

ID must match filename (without .svg extension).
