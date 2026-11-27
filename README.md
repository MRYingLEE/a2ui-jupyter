# a2ui-jupyter

Jupyter renderers and kernel helpers for [A2UI](https://github.com/a2ui-project/a2ui).
This repository was split out of the `jupyter` branch of a fork of `a2ui-project/a2ui`.
It consumes the published A2UI packages from npm and PyPI rather than building the A2UI
monorepo.

## Layout

| Path | Package | Purpose |
| --- | --- | --- |
| `python/a2ui_jupyter` | `a2ui-jupyter` (PyPI) | anywidget-based renderer for A2UI surfaces in notebooks; ships the built widget bundle |
| `python/a2ui_form` | `a2ui-form` (PyPI) | Ask for feedback with an A2UI form over Jupyter stdin |
| `typescript/jupyter` | `@a2ui/jupyter` (not on npm) | Browser widget and JupyterLite adapter that build into `python/a2ui_jupyter` |
| `typescript/form` | `@a2ui/form` (not on npm) | Form renderer used by `a2ui-form` |

Upstream dependencies:

- npm: `@a2ui/web_core`, `@a2ui/react`, `@a2ui/markdown-it`
- PyPI: `a2ui-core`

`@a2ui/web_core` is patched in `.yarn/patches/` so that re-registering an identical
element class for a tag does not throw. Remove the patch once upstream publishes a fix.

## TypeScript

Requires Node.js (verified with 22) and Yarn 4 (managed through `packageManager`).

```bash
yarn install
yarn build:all       # build the widget bundle and copy it into python/a2ui_jupyter
yarn test:all
yarn typecheck:all
yarn lint:all
yarn format:check:all
```

After changing the renderer, rebuild and commit the updated
`python/a2ui_jupyter/src/a2ui_jupyter/static/` files.

## Python

Requires [uv](https://docs.astral.sh/uv/). `a2ui-jupyter` requires Python 3.11 or newer;
`a2ui-form` requires Python 3.10 or newer.

```bash
uv sync --all-packages
uv run pytest
uv build --package a2ui-jupyter
uv build --package a2ui-form
```

## License

Apache License 2.0. See [LICENSE](LICENSE).
