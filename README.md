# GitHub Page Previews

This repository is an experiment & demo for implementing GitHub Page previews using only a single repo and GitHub Actions.

Production Site: https://grayside.github.io/gh-page-previews/

## Methodology

GitHub Pages serves content from a designated GitHub branch. Content in an
unreferenced subdirectory of that branch is also served. In this repository,
PRs are built and deployed to `previews/PR-NN`.

Unlike production, the preview site doesn't sit at the root URL.

## Features

* **Production/deploy** with `peaceiris/actions-gh-pages`
  * Deploy does not delete previously published files
* **Preview/deploy** with `peaceiris/actions-gh-pages` to `previews/PR-NN`
  * Triggered by opening a PR, updated on ever commit
* **Cleanup/preview** when the PR is closed, the preview site is deleted
* **Preview status updates** with `actions/github-script` as comments on the PR, linking to the deployed site on each update, and commenting on closed PRs to confirm tear-down.
* Hacky **Build Step** showcasing how to adjust theming and inject source code
links into the deployed site.
