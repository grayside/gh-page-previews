# GitHub Page Previews

This repository shows an implementation of GitHub Page PR previews using
a single repository and GitHub Actions.

Production Site: https://grayside.github.io/gh-page-previews/

## Features

* **Production Deploy** a static site to gh-pages on merge to main.
* **PR Preview Deploy** a static site to a sub-directory of the gh-pages site
when a PR is opened or new code commits. (`BASE_URL/previews/PR-NN`)
* **Cleanup a preview site** when the PR is closed by deleting the preview code
from the gh-pages branch
* **Preview status updates** are commented on the PR, linking to the deployed
preview site and notifying when the site is deleted after the PR is closed.
(There may be a lag between updating gh-pages branch and site deployment)
* Hacky **Build Step** showcasing how to adjust theming and inject source code
links into the deployed site.

## Visualizing the Flow

### Preview Content

```mermaid
flowchart LR;
  commit (Commit Content)
  push (Push Branch)
  open (Open Pull Request)
  gha (GitHub Actions)
  comment (Comment on PR)
  deploy (Deploy Preview Site)

  commit-->push
  push-->open
  open-->gha
  gha-->deploy
  gha-->comment
```

### Clean-up Content

```mermaid
flowchart LR;
  close (Close Pull Request)
  gha (GitHub Actions)
  clean (Remove preview site)
  comment (Comment on PR)
  
  close-->gha
  gha-->clean
  gha-->comment
```

## Methodology

GitHub Pages serves content from a designated GitHub branch. Content in an
unreferenced subdirectory of that branch is also served. In this repository,
PRs are built and deployed to `previews/PR-NN`.

Unlike production, the preview site doesn't sit at the root URL.

## Dependencies

* [peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages)
is used to deploy production & preview sites.
* [actions/github-script](https://github.com/actions/github-script) is used to
comment on the PR with preview environment status changes.