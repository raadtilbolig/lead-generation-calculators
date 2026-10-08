# Mortgage calculator embed

Embed Råd til Bolig's mortgage and home equity calculators in your website to collect property, loan and contact information for adviser follow-up.

**[Read the integration guide](https://raadtilbolig.github.io/mortgage-calculator-embed/)** (available after GitHub Pages is enabled).

The guide is in English. The calculator interface currently uses Danish and amounts in DKK. An integration requires an agreed asset host, theme and registered website origins from Råd til Bolig.

## Files

- `index.html` — the complete documentation page, including styles and integration examples. Open it directly in a browser.
- `sitemap.xml` — the documentation page's canonical URL for search engines.
- `.nojekyll` — serves the files as static content on GitHub Pages.

Edit `index.html` directly. It has no build step, external fonts, analytics or live calculator requests. Code examples are displayed as text and require the installation values supplied for your website.

## Publish on GitHub Pages

1. Create the public repository `raadtilbolig/mortgage-calculator-embed` and upload these files, including `.nojekyll`, to its `main` branch.
2. In **Settings → Pages**, choose **Deploy from a branch**, then **main** and **/ (root)**, and save.
3. Open the published guide and check the links and code examples.

The expected address is `https://raadtilbolig.github.io/mortgage-calculator-embed/`. If you change the repository name or use a custom domain, update this README, the canonical and Open Graph URLs in `index.html`, and `sitemap.xml` together.

Use this repository description: “Embed mortgage and home equity calculators in your website. Integration documentation for lead generation with Råd til Bolig.” Set the repository website to the published guide. Suggested topics: `mortgage-calculator`, `home-equity`, `lead-generation`, `web-components`, `denmark`.

The page contains a descriptive title, meta description, canonical URL, semantic headings, Open Graph metadata and a sitemap. Add a relevant link from your main website so visitors and search engines can discover it. Search engines decide whether to index and rank the page.

## Repository layout

This repository can live at `docs/public/mortgage-calculator-embed` as a Git submodule inside the private application repository. It has its own history and publishes only the files listed here. Commit documentation updates inside this repository, then record the updated submodule commit in the parent repository.

The configured GitHub remote becomes usable after the public repository has been created and uploaded. Keep the initial local commit when pushing so the parent repository's submodule reference remains available remotely. If you upload through GitHub's web interface, update the parent's submodule reference to the resulting remote commit afterwards.

## Integration support

Contact [Råd til Bolig](https://raadtilbolig.dk/) to agree on the asset hosts, website origins and company routing for staging and production. Run the acceptance checks in the guide on the actual CMS pages before launch.
