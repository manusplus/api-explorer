# Manus API Explorer - GitHub Pages build

This folder is ready to upload to a GitHub repository and serve with GitHub Pages.

## Structure

```text
index.html
assets/
  app.js
  styles.css
schemas/
  index.json
  hours.json
  illnesscase.json
```

## Schema loading behavior

For each schema resource in the dropdown, the explorer now tries the live Manus schema endpoint first:

```text
{endpoint}/{client}/{instance}/schema/...
```

If the live schema request fails, for example with HTTP 500, 404, or a network/CORS error, it falls back to the matching local GitHub file from `./schemas/`.

Dropdown labels show the source:

```text
Pure Hours          = live schema was used
**Pure Hours**      = local GitHub schema was used
```

The source result is remembered for the current browser session and updates again when the schema is reloaded.

## Add more schemas

1. Copy additional schema files into `schemas/`.
2. Add each file to `schemas/index.json`:

```json
{
  "path": "/schema/node/example",
  "file": "example.json",
  "title": "Example"
}
```

The `path` is the schema endpoint to try online. The `file` is the fallback file name in `schemas/`.

## GitHub Pages

Use relative paths only. This build already uses `./assets/...` and `./schemas/...`, so it works both at a custom domain and under `https://username.github.io/repository/`.

## Notes

- The explorer still calls the Manus API directly for login, live schema checks, node-tree, helper dropdowns, and sending requests. Those calls require CORS to be allowed by the Manus API.
- The two sample schemas contain JavaScript-style comments. The explorer strips comments before parsing, so they can remain as-is.
