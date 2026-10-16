# C4L DataCube Presentation

Interactive 3D cube presentation demo (`c4l_datacube_presentation`).

Single-page app built with **HTML**, **CSS**, and **vanilla JavaScript**.  
No build step or dependencies.

## Files

| File | Purpose |
| --- | --- |
| `cube.html` | Complete app (markup, styles, and script) |
| `README.md` | Setup, usage, and UI structure docs |

## Quick start

### Option A — open directly

```bash
open cube.html
```

### Option B — local static server (recommended)

```bash
cd /Users/thomas.micheler/work/c4l_datacube_presentation
python3 -m http.server 8080
```

Open:

```text
http://localhost:8080/cube.html
```

## Final UI structure

```text
┌──────────────────────────────── layout ────────────────────────────────┐
│                                                                        │
│  LEFT: Content pane (~flexible)     RIGHT: Datacube pane (narrow)      │
│  ┌─────────────────────────────┐    ┌──────────────────────────────┐   │
│  │ Content · <template>        │    │ Datacube                     │   │
│  │                             │    │                              │   │
│  │ TOP (~2/3) points section   │    │  3D cube stage               │   │
│  │  ┌──────────────────┬─────┐ │    │  (drag to orbit)             │   │
│  │  │ title/bullets    │ACTOR│ │    │                              │   │
│  │  │                  │200px│ │    │                              │   │
│  │  └──────────────────┴─────┘ │    ├──────────────────────────────┤   │
│  │                             │    │ Features                     │   │
│  │ BOTTOM (~1/3) media         │    │  [Front ]                    │   │
│  │  ┌──────────┬──────────┐    │    │  [Back  ]  vertical stack    │   │
│  │  │ image 1  │ image 2  │    │    │  [Right ]                    │   │
│  │  └──────────┴──────────┘    │    │  [Left  ]                    │   │
│  └─────────────────────────────┘    │  [Top   ]                    │   │
│                                     │  [Bottom]                    │   │
│                                     └──────────────────────────────┘   │
└────────────────────────────────────────────────────────────────────────┘
```

### Left pane (`pane-content`)

Switches by selected cube face (or overview while auto-spinning / free inspect).

Each template includes:

1. **Points section (top, ~2/3 height)**
   - Face kicker, title, intro text
   - Bullet list
   - **ACTOR** placeholder card (200×200) in the top-right corner
2. **Media section (bottom, ~1/3 height)**
   - Exactly **two** reference images with captions

Templates:

- `overview`
- `front`, `back`, `right`, `left`, `top`, `bottom`

### Right pane (`pane-cube`)

1. **Datacube stage**
   - CSS 3D cube
   - Drag to free-orbit
   - Click a cube face to lock that side
2. **Features panel**
   - Six vertically stacked feature buttons
   - Selecting a button locks orientation and swaps left content

## Interaction model

| Action | Result |
| --- | --- |
| Page load | Auto-spin + overview content |
| Click feature button / cube face | Lock face + load matching template |
| Drag cube | Free inspect mode |
| Click empty background | Resume auto-spin + overview |
| Keyboard orbit (`WASD` / arrows, `Q`/`E`) | Free inspect nudges |
| `Space` | Toggle auto-spin |
| `R` | Reset inspect pose |

## Responsive verification

Structural checks passed for the current `cube.html`.

### Breakpoints

| Viewport | Layout behavior |
| --- | --- |
| **> 1100px** | Two columns: flexible content + datacube `220–280px` |
| **≤ 1100px** | Datacube column tightens to `200–240px` |
| **≤ 960px** | Stacked layout: Datacube first, Content below |
| **≤ 720px** | Actor card stops floating top-right and stacks in flow |
| **≤ 640px** | Smaller cube size and compact feature buttons (still vertical) |
| **≤ 420px** | Further compact feature button type size |
| **Desktop short height** (`≥961px` and `max-height: 820px`) | Reduced stage min-height to avoid overflow |
| **`prefers-reduced-motion`** | Non-essential transitions/animations disabled |
| **`hover: none`** | Cube-face hover lift disabled on touch devices |

### Responsiveness notes

- Left template uses CSS grid rows `2fr / 1fr` so points stay dominant across widths.
- Long bullet lists scroll inside the top section instead of pushing media away.
- Media images fill the lower third rather than using a fixed aspect-only box.
- Feature buttons remain one vertical column at all breakpoints.
- On mobile, datacube appears above content for faster interaction.

### Manual check checklist

Use browser devtools device mode (or resize window) and confirm:

1. **Desktop wide:** content left, narrow datacube right, actor top-right in points card  
2. **~1000px:** right column still narrow, no horizontal page scroll  
3. **Tablet (~800px):** stacked panes, datacube on top  
4. **Phone (~390px):** vertical feature list usable, actor not overlapping text  
5. **Landscape short desktop:** cube/controls remain reachable without clipping critical UI  
6. **Reduce motion OS setting:** transitions settle immediately / minimal motion  

## Accessibility snapshot

- Skip link to features/controls panel  
- Native buttons with `aria-pressed` on feature controls  
- Labeled groups and pane landmarks  
- Image `alt` text for media and actor placeholder  
- Focus-visible outlines on interactive controls  
- Reduced-motion support  

Known limits:

- Drag orbit is pointer-based; keyboard alternatives exist  
- Some styling depends on modern CSS (`color-mix`, `@property`, `dvh`)

## Browser support

Target: current Chrome, Edge, Firefox, Safari (desktop/mobile).  
Internet Explorer is not supported.

## Customization

| Area | Where to edit |
| --- | --- |
| Face copy / bullets / images | Face templates in `cube.html` (`data-face="..."`) |
| Actor image | `.actor-card img` in each points section (or shared asset later) |
| Cube size | `:root --cube-size` |
| Column widths | `.layout { grid-template-columns: ... }` |
| Points/media ratio | `.face-template { grid-template-rows: 2fr 1fr; }` |
| Auto-spin feel | `AUTO_SPIN_SPEED`, `PITCH_SPEED`, `PITCH_MAIN` in script |

## Troubleshooting

- **Remote images missing:** Unsplash URLs need network access, or replace with local files.  
- **Content not switching:** ensure a Features button is selected (highlighted).  
- **Auto-spin resume:** click empty background (outside content/features/cube controls).  
- **Motion reduced unexpectedly:** check OS/browser “Reduce motion”.

## License

Demo project for presentation use. Replace placeholder media and copy before public release.
