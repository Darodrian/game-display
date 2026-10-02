# Game Display

A transparent full-screen `model-viewer` overlay for video game display props, with a live UI tuner. Press `F` to open the tuner menu.

## Credits

The GLB models in `models/` were created by the following authors:

| Model | Author |
| --- | --- |
| `cd__jewel_case.glb` | blue man group ([Sketchfab](https://sketchfab.com/bloobloo)), CC BY 4.0 |

## Skins

`cd__jewel_case.glb` has a **Skin** row in the tuner, applied entirely in the
browser: the pristine GLB and the artwork are fetched once, cached, and the
surfaces are rewritten in memory into a `Blob` URL. Nothing is written to disk
and no model file is modified.

Each skin needs four artwork files in its own folder under `media/`:

```
media/<skin-id>/front.jpg
media/<skin-id>/back.jpg
media/<skin-id>/spine.jpg
media/<skin-id>/cd.png
```

To add a skin, drop those four files in and append an entry to `SKINS` in
`index.html`:

```js
{
  id: "your-skin",
  label: "Your Skin",
  surfaces: {
    front: { src: "./media/your-skin/front.jpg", mime: "image/jpeg" },
    back: { src: "./media/your-skin/back.jpg", mime: "image/jpeg" },
    spine: { src: "./media/your-skin/spine.jpg", mime: "image/jpeg" },
    disc: { src: "./media/your-skin/cd.png", mime: "image/png" }
  }
}
```

The `id` is both the `media/` folder name and the select value; `label` is what
the dropdown shows. A skinned entry needs all four roles; `patchCdSkin` throws
if one is missing.

Note that `CD_SURFACES` is shared by all skins, so artwork is expected to use
one layout: front upright, back rotated, spine upright, disc circular and
mirrored. If a new skin needs different orientation, move `transform` and
`rect` into its own entry and thread them through
`patchCdSkin`.

## Artwork

The skin artwork under `media/` consists of scanned box inserts and disc
labels. Use them for personal, non-commercial display only. Do not use them
commercially, and do not imply any endorsement by the respective publishers or
copyright holders. The licenses covering the original game covers do not
generally apply to third-party scans.

| Skin | Publisher / Rights holder |
| --- | --- |
| Vagrant Story | Square / Square Enix |
| Mega Man X6 | Capcom |
| Aconcagua | Unknown — verify before publishing |

## Running

model-viewer cannot load models from `file://`, so serve the folder over HTTP:

```
npx serve .
```