# Face media images (`assets/`)

Two visuals per topic. Place files **directly in `assets/`**.

## Naming

```text
{prefix}_image01.jpg
{prefix}_image02.jpg
```

PNG is fine too (`{prefix}_image01.png`) — if you use PNG, update the matching `src` in `cube.html`.

| Prefix | Topic | Face | Files to provide |
| --- | --- | --- | --- |
| `ov` | Overview | overview | `ov_image01.jpg`, `ov_image02.jpg` |
| `cf` | Core Facility Applications | front | `cf_image01.jpg`, `cf_image02.jpg` |
| `co` | Controlling | back | `co_image01.jpg`, `co_image02.jpg` |
| `re` | Reporting | right | `re_image01.jpg`, `re_image02.jpg` |
| `bi` | Billing | left | `bi_image01.jpg`, `bi_image02.jpg` |
| `um` | User Management | top | `um_image01.jpg`, `um_image02.jpg` |
| `sm` | Service Management | bottom | `sm_image01.jpg`, `sm_image02.jpg` |

## How to replace

1. Export two photos per topic (suggested ~1600×1000, web-optimized).
2. Save/overwrite the matching filenames in `assets/`.
3. Keep the exact stem (`cf_image01`, …). Extension default in HTML is **`.jpg`**.
4. If you supply `.png` instead, change that image’s `src` in `cube.html` to `.png`.

Placeholder `.jpg` files are tiny stubs so paths resolve until real images are dropped in.
