# lunascape-config

Small, public configuration files that Lunascape Desktop reads at runtime so
some things can change without a new release.

| File | Read by | Purpose |
| --- | --- | --- |
| `ai-models.json` | AI sidebar (service worker) | Model catalogue for the Claude and OpenAI-compatible pickers: ids, labels, recommended entry, deprecated ids to hide, and the OpenAI-compatible presets' endpoints and known models. |

The app merges three sources for every picker, in this order: the catalogue
built into that version, this file, and the model list the provider's own API
returns. So a model added here appears in every installed copy within a few
hours; a model listed under `hidden` disappears from the built-in list.

## Editing

- Keep `version` at `1` unless the shape changes; the app ignores files whose
  version it does not know.
- Every Claude id must start with `claude-`; the app filters others out.
- Validate before pushing: `npx ajv-cli validate -s ai-models.schema.json -d ai-models.json`
  (CI runs the same check on every push).

Served from `https://raw.githubusercontent.com/lunascape/lunascape-config/main/ai-models.json`.
