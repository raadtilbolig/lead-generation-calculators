# Lead generation calculators

Open [index.html](index.html) to embed [Råd til Bolig](https://raadtilbolig.dk/) calculators in your website. The example contains both calculators; keep the sections you need.

| Calculator | Result |
| --- | --- |
| **Loan Check (Lånetjek)** | Calculates a mortgage refinancing scenario and saves the proposal with the customer's property. |
| **Home Equity (Friværdi)** | Shows estimated property value, debt and potential equity release. |

The calculators collect the visitor's address, loans and contact details. Submitting the contact step creates a customer and property record with the supplied loans for your company, ready for adviser follow-up.

The interface uses Danish and amounts in DKK. Results depend on the property and loan inputs. Have an adviser review them before a financing decision.

## 1. Register your website

Send [Råd til Bolig](https://raadtilbolig.dk/) the exact HTTPS origins where you will use the calculators, including staging and preview subdomains. For example: `https://www.example.com`.

We register the origins, configure which company receives the records and provide your asset hosts and theme class. Each bundle is built for specific API and platform services. Use the asset host supplied for the matching staging or production environment.

## 2. Configure the example

Replace these values in `index.html`:

| Example value | Replace with |
| --- | --- |
| `ASSET_ORIGIN` | Your supplied HTTPS asset origin, without a trailing slash. Replace every occurrence. |
| `YOUR_THEME_CLASS` | Your supplied CSS theme class. |
| `YOUR_COMPANY_NAME` | The company name shown in the contact consent text. |
| `YOUR_ADVISER_NAME` | The adviser name shown with the result. The image comes from your asset bundle. |
| `https://www.example.com/privacy` | Your privacy policy URL. |

Each calculator needs one element:

```html
<rtb-loan-check advisorname="YOUR_ADVISER_NAME"></rtb-loan-check>
<rtb-home-equity advisorname="YOUR_ADVISER_NAME"></rtb-home-equity>
```

The wrappers include the address, loans, contact and result steps with Danish navigation labels. They preserve your page's URL hash by default (`sync-url="false"`). Their default `url-prefix` values are `loan-check` and `home-equity`, which keep their saved browser states separate. If you install multiple copies of one calculator, give each a distinct, stable `url-prefix`.

Optional attributes:

| Attribute | Behaviour |
| --- | --- |
| `advisorname` | Adviser name shown with the result. |
| `subtitle` | Text above address search. The Danish bundle supplies the default. |
| `url-prefix` | Key for saved browser state and, when enabled, URL navigation. |
| `sync-url="true"` | Updates the URL hash when moving between steps. |

When replacing an existing integration, keep its `url-prefix` to preserve saved browser state. Shared configuration still supplies the company name, privacy URL, recommendation profile, adviser image and contact link.

To add a contact link to the recommendation card, set `recommendationCtaUrl` and `recommendationCtaLabel` in `window.RAAD_TIL_BOLIG.config`.

### Calculator overview

Use a slotted list with one tile per calculator:

```html
<rtb-calculator-navigation-list>
  <rtb-calculator-navigation-tile
    calculator="loan-check"
    href="/lanetjek/">
  </rtb-calculator-navigation-tile>

  <rtb-calculator-navigation-tile
    calculator="home-equity"
    href="/frivaerdi/">
  </rtb-calculator-navigation-tile>
</rtb-calculator-navigation-list>
```

`calculator` supplies the configured brand's Danish title, description and icon.
Set `href` to the calculator page on your website. The example file links to the
two calculator sections on the same page; replace those fragment URLs when using
separate pages.

Choose which calculators appear by adding, removing or reordering the child tiles.
An explicit title inside a tile, `description`, `iconname` and `image` override its
defaults. Existing tiles with explicit content continue to work. Use the supplied
brand asset host, or set the supplied `recommendationProfile` in the shared
configuration when your integration requires it.

Install this overview after your asset host has published calculator tile presets.

## 3. Add the example to your website

Serve the configured file from your registered HTTPS origin. To embed it in an existing CMS page, copy its stylesheet links, configuration, module scripts and chosen calculator section into the CMS's HTML or code facility.

Keep the configuration before the module scripts. Load one component version and one Ionicons import per page. Leave `initializeSite` unset for a CMS integration.

Your CMS controls the surrounding layout, cookie banner and analytics. Check that it preserves custom elements and `type="module"` scripts when saving. Keep the previous CMS version so you can restore it if installation fails.

The components obtain their calculator token from `/v3/calculator/token` on the matching public host (`public.raadtilbolig.dk` or `public.beta.raadtilbolig.dk`) using your registered website origin. Calculator data requests also use that public host's `/v3/` routes.

### Component versions

The example pins runtime, icons and brand styles to `v1`. Confirm that your supplied asset host has published the wrapper build before installing it. Compatible updates are published within the current major. A future `v2` uses new asset paths while `v1` remains hosted; upgrading requires changing all imports together. Load one component major per page.

Existing `app-*` integrations keep their current markup and unversioned asset URLs. Their compiled files remain hosted. Install the versioned `rtb-*` example when you are ready to migrate.

### Content Security Policy

If your site uses a Content Security Policy, allow:

- Your supplied asset host for scripts, styles, fonts and images.
- Your supplied asset host and the matching public host in `connect-src`. The asset host serves the recommendation JSON files.
- `blob:` images for property photos.
- Any Google Fonts origins referenced by your theme.

Apply your CMS's nonce to the inline configuration script when required. If generated component styles also require a nonce, add this to the page's `<head>` before the component scripts:

```html
<meta name="csp-nonce" content="CMS_NONCE">
```

Replace `CMS_NONCE` with the current response's nonce.

### Browser storage

The calculator saves state in local storage and restores it when up to 24 hours old. It removes expired state when it next reads it.

A `customer_token` cookie allows subsequent customer updates and expires after one hour. Check the storage behaviour and contact consent wording against your site's privacy setup.

## 4. Check the integration on staging

1. Complete each installed calculator on desktop, mobile and your narrowest CMS content column.
2. Check fonts, icons and photos. Check recommendation text, adviser details, privacy links and contact links.
3. Confirm the customer and property records reach your company. For Loan Check, verify that the proposal is saved.
4. Reload a partly completed flow to check restored state. Check the surrounding page styles, navigation and URL hash.
5. Check blocked requests, unavailable recommendation files and API failures. Resolve incorrect results or loading failures with Råd til Bolig before launch.

If a request fails, check its asset origin, your registered website origin and the security policy in the browser's console and network panel. Send your integration contact the affected step, browser, viewport size and response status. Remove tokens and customer data from the report.

After staging passes, repeat these checks on your production pages.
