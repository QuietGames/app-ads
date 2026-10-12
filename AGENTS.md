# app-ads — how to work in this repository

This repository holds **`app-ads.txt`**, the public file that tells ad networks
which sellers may sell Quiet's app inventory. GitHub Pages serves it at
<https://quietgames.github.io/app-ads/app-ads.txt>, and `quiet.app/app-ads.txt`
is a 301 redirect to that URL (set once in Webflow).

> The repository is public. The file is public anyway, but commit messages are
> too: never put an internal exchange with a partner in one.

## Change the file

Use the `update-app-ads` skill of `ai-quiet-plugin` (`/update-app-ads`). It reads
this file, applies your change, shows the diff, and commits to `main` once you
say go. There is no pull request on purpose: write access is limited to the
people in [`CODEOWNERS`](.github/CODEOWNERS), and git keeps every line's author.

By hand, one line per entry: `domain, publisher-id, DIRECT|RESELLER[, certification-authority-id]`.
A trailing `# comment` is allowed. Do not "fix" an old line unless asked.

## Rules

- Commit messages follow semantic commits: `<type>(app-ads): <subject>`, for
  example `feat(app-ads): add example-ssp.com 12345`. Use `fix` to correct a line
  and `chore` for anything that is not the file.
- Never rename or delete this repository, or move it to another organization:
  the redirect on quiet.app points at its Pages URL, and every network would get
  a 404.
- `.github/workflows/pages.yml` publishes **only** `app-ads.txt`, and refuses a
  file of fewer than 100 lines (a truncated file would drop every seller).

## Roll back

`git revert <commit>` on `main`, then push. Pages republishes within two minutes.
