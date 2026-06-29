# WordPress Post-Update Test Taxonomy

Use this reference when turning an exploratory site audit into a QA report or checklist.

## Discovery Areas

- Global layout: header, footer, logo, menus, breadcrumbs, sticky elements, cookie consent, language/currency switchers, accessibility shortcuts.
- Navigation: desktop menu, mobile menu, dropdowns, mega menus, anchor links, footer links, internal CTAs, broken links, external links.
- Content templates: home, standard page, landing page, archive, category, tag, search results, single post, author page, 404.
- Ecommerce: shop/category, product card, product detail, variations, stock, price, sale badges, related products, wishlist/compare, cart, coupon, shipping, checkout, payment, confirmation, account.
- Forms: contact, newsletter, lead capture, quote request, login, registration, password reset, comments/reviews, file upload, multi-step forms.
- Interactive UI: tabs, accordions, dropdowns, selects, filters, sorters, pagination, autocomplete, popups, modals, sliders, galleries, maps, videos, chat widgets.
- Responsive behavior: mobile menu, horizontal overflow, tap targets, sticky bars, product grids, checkout fields, form labels, long text.
- Integrations: payment, shipping, CRM, email marketing, analytics, maps, social feeds, embedded videos, chat, CAPTCHA, consent manager.
- Technical signals: console errors, failed requests, mixed content, missing assets, redirect loops, cache/minification issues, layout shift, very slow pages.

## Template Grouping Rule

When many pages share a layout, list the group and examples, then choose one representative URL for detailed testing. Good grouping examples:

- Product category pages that share filters, product cards, pagination, and sorting.
- Blog category/archive pages that share cards, pagination, sidebar, and post metadata.
- Standard institutional pages that share hero, content blocks, forms, and CTAs.
- Product detail pages with the same product type, variation logic, and buy box.

Mention exceptions separately when a page in the same group has unique widgets, custom forms, unusual filters, or special campaign content.

## Behavior Observations To Capture

- What the user did.
- What changed on screen.
- Validation, success, error, loading, empty, and disabled states.
- URL changes, redirects, query strings, pagination state, cart count, price/stock updates.
- Console errors or failed network calls tied to the action.
- Whether behavior depends on login, cookies, location, selected variation, or viewport size.

## Checklist Scenario Patterns

- Verify page loads without visual breakage or fatal errors.
- Verify navigation path reaches the expected page.
- Verify interactive element opens, closes, changes state, and remains usable on mobile.
- Verify form required-field validation, invalid data validation, consent checkbox, success message, email/CRM behavior when known, and spam/CAPTCHA behavior.
- Verify ecommerce flow from product discovery to cart and checkout review.
- Verify filters/sort/pagination preserve expected results and do not break layout.
- Verify repeated templates by testing one representative page and spot-checking exceptions.
- Verify login/reset/register/account scenarios when credentials or test users are available.
- Verify console/network health on critical pages and after major interactions.
