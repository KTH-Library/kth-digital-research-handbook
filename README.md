This repository redirects traffic
from its Github Pages website at
<https://kth-library.github.io/kth-digital-research-handbook>
to <https://kth-library.github.io/kth-datahub-workspace>.

It also takes care to redirect the Swedish language landing
page at `/sv` (since some users may have bookmarks
or similar that point directly to it).

These redirects were put in place because we changed the repository's
name from `kth-digital-research-handbook` to `kth-datahub-workspace`.


## Notes on setting up a minimal Github Pages website

Create `index.html` in the repo root that contains a meta redirect.
Configure the Github repo to deploy from the main branch.

> GitHub Pages publishes any static files that you push to your repository. You can create 
> your own static files or use a static site generator to build your site for you.

For this repo, I don't think we need to use any static site generator, since all we are
pushing is a ready-to-go HTML file.

+ https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
+ https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
