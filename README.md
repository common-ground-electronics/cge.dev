# cge.dev

Common Ground Electronics Website

## Local Development Environment

Install [Hugo](https://gohugo.io/):

```sh
brew install hugo
```

Install [Invoke](https://www.pyinvoke.org/index.html):

```sh
pip install invoke
```

## Local Build & Preview

```sh
inv preview
```

## Build & Deploy

[![Deploy](https://github.com/common-ground-electronics/cgnd.dev/actions/workflows/deploy.yml/badge.svg)](https://github.com/common-ground-electronics/cgnd.dev/actions/workflows/deploy.yml)

The site is served by a Cloudflare Worker (`wrangler.toml`) as static assets,
deployed from GitHub Actions; nothing is built by Cloudflare itself.

- Pushes to `main` run [deploy.yml](.github/workflows/deploy.yml): build with
  Hugo, `wrangler deploy`, live at <https://cge.dev>.
- Pull requests run [preview.yml](.github/workflows/preview.yml): build with
  the preview as the base URL, `wrangler versions upload --preview-alias`, and
  a sticky comment on the PR linking to
  `https://pr-<number>-cge-dev.<account>.workers.dev`. Previews never change
  production.

Both workflows need the repository secrets `CLOUDFLARE_API_TOKEN` (the "Edit
Cloudflare Workers" template, scoped to the account and the cge.dev zone) and
`CLOUDFLARE_ACCOUNT_ID`.

The old domain, cgnd.dev, is not part of this deployment: Cloudflare Redirect
Rules in the cgnd.dev zone send every URL to the same path on cge.dev.

## Licenses

See the [LICENSE](LICENSE.md) file for copyright & license information.
