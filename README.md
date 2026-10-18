# Powell — Hugo site

## Publish on GitHub Pages (fresh repo)
1. Keep anything you still want from the old repo first: real posts, `resume.md`, your résumé PDF, images.
2. Clear the repo and add everything in this folder, including the hidden `.github/` folder and `.gitignore`. `preview.html` is only a preview; Hugo ignores it.
3. Download the Powell map (link below) to `static/img/powell-arid-region-1890.jpg`. Without it the hero map is blank.
4. In `hugo.toml`, set your email in the Contact menu item and your GitHub/LinkedIn URLs. `baseURL` is set automatically by the workflow.
5. On GitHub: Settings → Pages → Build and deployment → Source: **GitHub Actions**.
6. Push to `main`. The workflow in `.github/workflows/hugo.yml` builds and deploys. Check the Actions tab for progress.

PaperMod is no longer required. If your old repo had it as a git submodule, you can drop it.


Three homepage layouts from the style board, switchable in `hugo.toml`:

    [params.powell]
    layout = "expedition"   # expedition | atlas | fieldnotes

## Install
1. Copy `layouts/`, `assets/`, `static/` into your site root (merge with existing folders).
2. Remove the old overrides so they don't conflict: `layouts/partials/header.html`, `layouts/partials/extend_head.html`, `layouts/partials/extend_footer.html`, `assets/css/extended/custom.css`, `layouts/index.html`.
3. Merge the `[params.powell]` and `[menus]` blocks from `hugo.toml` into your config.
4. Download the high-res Powell map and save it as `static/img/powell-arid-region-1890.jpg`:
   https://commons.wikimedia.org/wiki/File:Map_of_Water_Sheds_of_Arid_Region_of_United_States_by_John_Wesley_Powell.jpg
   (CC BY-SA 4.0, scan by Torpyl. Keep the credit line in `mapCredit`.)
5. Optional engravings: Thomas Moran's illustrations for Powell's 1875 *Exploration of the Colorado River of the West* are public domain. Set `about.image` and `panorama.image`. Without them the site shows topographic lines.

## Content
- Field Notes (project write-ups) live in `content/field-notes/` with `categories`, `tools`, `summary`, `image` and `featured` front matter.
- Resources (articles, guides) live in `content/resources/`.
- The homepage "Recent Work" river log shows the newest items from both, newest upstream. `riverlogStyle = "rows" | "preview"` sets its layout.
- `preview.html` in this folder is a static preview (needs `static/img/powell-arid-region-1890.jpg` or an internet connection for the map).

## Notes
- These layouts override PaperMod's baseof, home, list and single templates. You can keep PaperMod installed for its other features or remove it.
- The style board's two Powell quotes couldn't be verified, so the config uses his documented 1893 Irrigation Congress remark. Change `[params.powell.quote]` if you prefer.
