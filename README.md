# Interactive 3D Cube

A single-page interactive demo built with **HTML**, **CSS**, and **vanilla JavaScript**.  
It features a CSS 3D cube, face-linked content templates, auto-rotation, and manual orbit controls.

## Files

| File | Purpose |
| --- | --- |
| `cube.html` | Complete app (markup, styles, and script) |
| `README.md` | Setup and usage documentation |

No build step, bundler, or dependencies are required.

## Quick start

### Option A — open directly

```bash
open cube.html
```

Or double-click `cube.html` in Finder.

### Option B — local static server (recommended)

Serving over `http://` avoids some browser restrictions with local files and remote images.

```bash
# from your home directory
cd /Users/thomas.micheler/work/c4l_datacube_presentation
python3 -m http.server 8080
```

Then open:

```text
http://localhost:8080/cube.html
```

## Features

- **Split layout**
  - Left: content pane (bullets + 2 images per face)
  - Right: 3D cube + controls
- **Auto-rotation** by default (tumble path includes top and bottom faces)
- **Face snap buttons** lock the cube and swap left-pane content
- **Manual inspection**
  - Drag the cube
  - On-screen orbit pad + roll / reset / auto-spin
  - Keyboard shortcuts
- **Responsive controls** for desktop and mobile touch targets
- **Motion transitions** for cube locks and content swaps

## Usage

### Cube interaction

1. Watch the cube auto-rotate.
2. Click a **face button** (or a cube face) to lock that side and load its content.
3. Drag the cube (or use orbit controls) for free inspection.
4. Click **Auto-spin** or empty background space to resume rotation.
5. Click **Reset view** to return to a neutral inspect pose.

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `←` `→` or `A` `D` | Yaw left / right |
| `↑` `↓` or `W` `S` | Pitch up / down |
| `Q` `E` | Roll |
| `R` | Reset view |
| `Space` | Toggle auto-spin |

Keyboard shortcuts are ignored while focus is inside form controls/buttons that handle their own keys.

### Content templates

Left-pane content is defined as templates in `cube.html`:

- `data-face="overview"` — shown during auto-spin / free inspect
- `data-face="front|back|right|left|top|bottom"` — shown when that face is locked

Each face template includes:

- title + description
- bullet list (`.content-list`)
- two images (`.content-gallery`)

Edit those blocks to replace sample copy and image URLs.

## Accessibility notes

Checked and improved in this pass:

- Semantic landmarks and labeled control groups
- Native `<button>` controls with `aria-label` / `aria-pressed` where useful
- Skip link to cube controls
- `aria-live="polite"` status text for mode/content changes
- Visible `:focus-visible` outlines on interactive controls
- Image `alt` text on sample media
- `prefers-reduced-motion` disables non-essential animation
- Touch-friendly minimum control sizes on small screens

Known limitations:

- The 3D stage uses pointer dragging; equivalent button/keyboard controls are provided
- Continuous orientation readout is not announced on every frame (by design, to avoid SR noise)
- Some visual effects rely on modern CSS (`color-mix`, `@property`, `dvh`)

## Browser support

Designed for current evergreen browsers:

- Chrome / Edge (latest)
- Firefox (latest)
- Safari (latest, macOS/iOS)

Expected support details:

| Capability | Notes |
| --- | --- |
| CSS 3D transforms | Required core feature |
| `clamp()`, CSS variables | Broad support |
| `dvh` units | Modern browsers; layout still works with fallbacks via min-height |
| `color-mix()` | Modern browsers; accents may degrade gracefully if unsupported |
| Pointer Events API | Used for drag orbit |
| `backdrop-filter` | Visual enhancement only |

For best results use an up-to-date desktop or mobile browser. Internet Explorer is not supported.

## Project structure (conceptual)

```text
cube.html
├── Left pane
│   └── Face content templates (overview + 6 faces)
└── Right pane
    ├── 3D cube stage (drag to orbit)
    └── Controls
        ├── Orbit pad / roll / auto-spin / reset
        └── Face snap buttons
```

## Customization tips

- **Cube size**: change `--cube-size` in `:root`
- **Motion timing**: adjust `--dur-lock`, `--dur-content`, `--dur-bg`
- **Auto-spin feel**: tune `AUTO_SPIN_SPEED`, `PITCH_MAIN`, `PITCH_SECONDARY` in the script
- **Colors**: face gradients and button tokens are per-face CSS custom properties

## Troubleshooting

- **Images don’t load**  
  Sample images are remote (Unsplash). Check network access, or replace with local image paths.

- **Drag feels ignored on mobile**  
  Use the orbit pad buttons; ensure you’re dragging on the cube stage area.

- **Content doesn’t change**  
  Confirm a face button is active (highlighted). Auto-spin mode shows the overview template.

- **Animations are reduced/disabled**  
  Your OS/browser may have “Reduce motion” enabled.

## License

Demo project for local use. Replace sample images/copy with your own assets before publishing.
