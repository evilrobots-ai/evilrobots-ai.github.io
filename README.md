# evilrobots.ai

This repository contains the Hugo source for [evilrobots.ai](https://evilrobots.ai).

## Theme setup

The active theme, `ananke`, is vendored directly in `themes/ananke`. It is tracked as ordinary repository content, not as a Git submodule and not as a Hugo module dependency.

That means:

- a normal `git clone` is enough to work on the site
- there is no `git submodule update --init --recursive` step
- the root repository does not use `go.mod` or `go.sum`

Site-specific theme fixes and overrides live outside the vendored theme, primarily in:

- `layouts/partials/func/style/GetMainCSS.html`
- `layouts/partials/social-share.html`

## Local development

Requirements:

- Hugo Extended `0.157.0` or later

Start the local development server:

```bash
hugo server
```

Build the production output:

```bash
hugo --gc --minify
```

The generated site is written to `docs`, which is committed because GitHub Pages is serving the built output from this repository.

## CI

GitHub Actions runs a build check on pushes and pull requests using the vendored theme directly. The workflow does two things:

1. builds the site with `hugo --gc --minify`
2. fails if the generated `docs` output is not up to date

If CI fails on the second step, rebuild locally and commit the changed files under `docs/`.

## Updating the vendored theme

When updating `ananke`, replace the contents of `themes/ananke` from the upstream theme, then rebuild and verify that the local overrides listed above are still required and still correct.
