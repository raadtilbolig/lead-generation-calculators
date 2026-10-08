# Lead generation calculators

Embed [Råd til Bolig](https://raadtilbolig.dk/) calculators in your website to collect leads for adviser follow-up. This guide covers mortgage refinancing and home equity calculators for Danish homeowners.

[index.html](index.html) is a complete HTML embed example with both calculators. Replace `ASSET_ORIGIN`, `YOUR_THEME_CLASS`, `YOUR_COMPANY_NAME`, `YOUR_ADVISER_NAME` and the example privacy URL, then serve it from your registered HTTPS origin. Keep the calculator sections you need.

The calculators render inline as web components. Visitors enter their address, loans and contact details before seeing the result. Submitting the contact step creates a customer and property record with the supplied loans for your company.

| Calculator | Result |
| --- | --- |
| **Loan Check (Lånetjek)** | Calculates a refinancing scenario and saves the proposal with the customer's property. |
| **Home Equity (Friværdi)** | Shows estimated property value, debt and potential equity release. |

The calculator interface uses Danish and amounts in DKK. Results depend on the property and loan inputs and require an adviser's review before a financing decision.

## Setup

Agree these values with Råd til Bolig for staging and production:

- **Website origins:** each exact HTTPS origin hosting a calculator, including preview subdomains.
- **Asset origin:** the supplied host for components, styles, fonts, images and recommendations.
- **Theme class:** the CSS class supplied with your theme.
- **Brand details:** company display name, privacy policy URL and adviser name.

Råd til Bolig configures company routing and cross-origin access for your website origins. Each component bundle uses the API and platform services selected at build time, so use the supplied asset host for the matching environment.

## Load the components

Add these imports once per page. Replace `ASSET_ORIGIN` with your supplied HTTPS asset origin, without a trailing slash, and replace the company and privacy examples. Load the configuration before the module scripts.

```html
<link rel="stylesheet" href="ASSET_ORIGIN/app.css">
<link rel="stylesheet" href="ASSET_ORIGIN/fonts.css">

<script>
  window.RAAD_TIL_BOLIG = window.RAAD_TIL_BOLIG || {};
  window.RAAD_TIL_BOLIG.config = {
    brandName: "YOUR_COMPANY_NAME",
    privacyUrl: "https://www.example.com/privacy"
  };
</script>

<script type="module"
  src="ASSET_ORIGIN/static/components/components.esm.js"></script>
<script type="module"
  src="ASSET_ORIGIN/static/assets/ionicons/ionicons.esm.js"></script>
```

Keep one component version and one Ionicons import per page. Leave `initializeSite` unset for a CMS integration. Your CMS owns the surrounding layout, cookie banner and analytics configuration.

## Embed Loan Check

Place this markup in your page's content area. Replace `YOUR_THEME_CLASS` and `YOUR_ADVISER_NAME` with your installation values.

```html
<div class="YOUR_THEME_CLASS">
  <app-calculator-inline sync-url="false" url-prefix="loan-check">
    <app-calculator-state-address
      state="address" label="Address" pagination>
    </app-calculator-state-address>
    <app-calculator-state-loans
      state="loans" label="Loans" pagination>
    </app-calculator-state-loans>
    <app-calculator-state-contact
      state="contact" label="Contact" pagination>
    </app-calculator-state-contact>
    <app-rebalance-state-result
      state="result" advisorname="YOUR_ADVISER_NAME">
    </app-rebalance-state-result>
  </app-calculator-inline>
</div>
```

## Embed Home Equity

Use the same imports and configuration with this markup:

```html
<div class="YOUR_THEME_CLASS">
  <app-calculator-inline sync-url="false" url-prefix="home-equity">
    <app-calculator-state-address
      state="address" label="Address" pagination>
    </app-calculator-state-address>
    <app-calculator-state-loans
      state="loans" label="Loans" pagination>
    </app-calculator-state-loans>
    <app-calculator-state-contact
      state="contact" label="Contact" pagination>
    </app-calculator-state-contact>
    <app-calculator-state-result
      state="result" advisorname="YOUR_ADVISER_NAME">
    </app-calculator-state-result>
  </app-calculator-inline>
</div>
```

## Configuration

| Setting | Behaviour |
| --- | --- |
| `brandName` | Company name in the contact consent text. Company routing is configured server-side for the website origin. |
| `privacyUrl` | Destination of the privacy link in the contact step. |
| `sync-url="false"` | Preserves the CMS page's URL hash during step changes. |
| `url-prefix` | Identifies saved browser state. Use distinct, stable values for each flow. |
| `advisorname` | Adviser name shown with the result. The image comes from the supplied asset bundle. |
| `recommendationCtaUrl` and `recommendationCtaLabel` | Optional fields in `window.RAAD_TIL_BOLIG.config` that add a contact link to the recommendation card. |

The example step labels customise navigation. Other interface text comes from the Danish component bundle.

Calculator state is stored in local storage and restored when up to 24 hours old. Expired state is removed when the calculator next reads it. A `customer_token` cookie allows subsequent customer updates and expires after one hour. Review the actual storage and consent behaviour with your site's privacy setup.

## CMS requirements

Your CMS must preserve custom elements and `type="module"` scripts. Check the published HTML after saving. The components obtain their calculator token automatically from the platform's `/v2/calculator/token` endpoint using the registered website origin.

If your site uses a Content Security Policy, allow the supplied asset host for scripts, styles, fonts and images; the matching API and platform hosts for connections; and `blob:` images for property photos. Include any Google Fonts origins referenced by your theme.

Apply the CMS-generated nonce to the inline configuration script when required. If generated component styles also require a nonce, add this to the page's `<head>` before the component scripts, using the current response's nonce:

```html
<meta name="csp-nonce" content="CMS_NONCE">
```

## Before launch

Complete both flows on your actual staging pages, then repeat on production:

- Check desktop, mobile and the narrowest CMS content column, including the result layout.
- Check fonts, icons, photos, recommendations, adviser details and privacy and contact links.
- Verify that customer and property records reach the correct company and Loan Check saves the proposal.
- Check surrounding page styles, URL hashes, restored state after reload and consent behaviour.
- Check blocked requests, unavailable recommendation files and API failures. Resolve incorrect results or loading failures with Råd til Bolig before launch.

Keep the previous CMS version so you can restore it if installation fails. For missing content or failed requests, inspect the browser console and network panel and verify the asset origin, registered website origin and security policy. Send your integration contact the affected step, browser, viewport size and failed response status, excluding tokens and customer data.

Contact [Råd til Bolig](https://raadtilbolig.dk/) to arrange an integration.
