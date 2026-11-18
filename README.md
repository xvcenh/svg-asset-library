# SVG Scene Asset Library

Browse the fantasy scene collection, filter by layer, search English or Chinese tags, and download individual SVGs. The gallery and the scene engine use the relative file paths in `manifest.json`.

[Open the gallery](https://xvcenh.github.io/svg-asset-library/) · [Open the scene engine](https://xvcenh.github.io/svg-scene-engine/)

## Local preview

Run `python -m http.server 8080` from this directory, then open `http://localhost:8080/`. The catalog and images load from the same checkout. Search and layer selections are stored in the URL for sharing.

## Adding an asset

Place the SVG under the matching layer in `assets/`. Add its unique ID, repository-relative path, layer and comma-separated tags to `manifest.json`. The gallery derives its filters and counts from that manifest.
