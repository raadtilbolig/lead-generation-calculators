# Lead generation calculators

Embed Råd til Bolig calculators in your website to collect leads for adviser follow-up. The current integrations cover mortgage refinancing and home equity for Danish homeowners.

**[Read the integration guide](https://raadtilbolig.github.io/lead-generation-calculators/)** (available after GitHub Pages is enabled).

The guide is in English. The calculator interface currently uses Danish and amounts in DKK. An integration requires an agreed asset host, theme and registered website origins from Råd til Bolig.

## Files

- `index.html` — the complete documentation page, including styles and integration examples. Open it directly in a browser.
- `sitemap.xml` — the documentation page's canonical URL for search engines.
- `.nojekyll` — serves the files as static content on GitHub Pages.

Edit `index.html` directly. It has no build step, external fonts, analytics or live calculator requests. Code examples are displayed as text and require the installation values supplied for your website.

## Publish on GitHub Pages

1. Create the empty public repository `raadtilbolig/lead-generation-calculators` on GitHub. Leave GitHub's README, licence and `.gitignore` initialisation options unchecked.
2. Commit your documentation changes on `main` inside this submodule, then run this command from the parent repository's root:

   ```sh
   direnv exec . just docs push_lead_generation
   ```

   The command pushes the submodule's committed `main` branch to its configured `origin` and sets upstream tracking. It requires Git push access to the organisation's repository.
3. In **Settings → Pages**, choose **Deploy from a branch**, then **main** and **/ (root)**, and save.
4. Open the published guide and check the links and code examples.

The expected address is `https://raadtilbolig.github.io/lead-generation-calculators/`. If you change the repository name or use a custom domain, update this README, the canonical and Open Graph URLs in `index.html`, and `sitemap.xml` together.

Use this repository description: “Embed lead generation calculators in your website. Integration documentation from Råd til Bolig, starting with mortgage and home equity calculators.” Set the repository website to the published guide. Suggested topics: `lead-generation`, `calculators`, `web-components`, `mortgage-calculator`, `home-equity`, `denmark`.

The page contains a descriptive title, meta description, canonical URL, semantic headings, Open Graph metadata and a sitemap. Add a relevant link from your main website so visitors and search engines can discover it. Search engines decide whether to index and rank the page.

## Repository layout

This repository lives at `docs/public/lead-generation-calculators` as a Git submodule inside the private application repository. It has its own history and publishes only the files listed here. Commit documentation updates inside this repository, then record the updated submodule commit in the parent repository.

Create the public repository before running the push command. Pushing preserves the local history so the parent repository's submodule reference is available remotely.

## Integration support

Contact [Råd til Bolig](https://raadtilbolig.dk/) to agree on the asset hosts, website origins and company routing for staging and production. Run the acceptance checks in the guide on the actual CMS pages before launch.
