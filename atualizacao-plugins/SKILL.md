---
name: atualizacao-plugins
description: Exploratory audit of WordPress sites after plugin, theme, WooCommerce, Elementor, page builder, form, cache, SEO, security, payment, shipping, or integration updates. Use when the user asks Codex to access a website, map public and login-gated functionality, identify UI behaviors, ecommerce flows, forms, dropdowns, selects, animations, menus, templates, category pages, repeated layouts, risky plugin-dependent features, and produce a report of found functionality with observations and a test plan or checklist for post-update validation.
---

# Atualizacao Plugins

## Goal

Audit a WordPress site as a tester would after plugin updates. Discover what the site does, group repeated templates, identify behaviors that can break after updates, and produce a practical report with test coverage guidance.

## Core Workflow

1. Confirm scope only when missing: site URL, whether login credentials are available, whether purchases/submissions may be completed, and whether the output should include the checklist now or only the functional report.
2. Use browser tooling to inspect the site. Prefer visible behavior over assumptions from markup. Capture enough evidence through URLs, page titles, UI labels, screenshots when useful, console errors, and notable network failures.
3. Build an inventory before deep testing:
   - Main navigation, footer navigation, search, menus, modals, cookie banners, language/currency selectors, account links.
   - Page types and templates: home, institutional/content pages, landing pages, blog/archive/single post, category/listing pages, product listing, product detail, cart, checkout, account, contact, FAQs, downloads, restricted areas.
   - Repeated pages: mention all detected similar categories, archives, products, or listing templates, then select one representative page per template for detailed checks.
   - Interactive behaviors: forms, validation, dropdowns, selects, accordions, tabs, carousels, animations, filters, sorters, pagination, search suggestions, maps, embeds, popups, chat widgets, calculators, uploads.
   - Plugin-sensitive features: WooCommerce, payment gateways, shipping calculators, Elementor/visual builder widgets, contact forms, cache/minification, membership/login, multilingual, SEO schema, consent, analytics, security, sliders, galleries, maps, social feeds.
4. Explore with tester discipline:
   - Visit pages from navigation and important internal links.
   - Exercise controls without submitting irreversible actions unless explicitly allowed.
   - For forms, test required fields, invalid values, selects, masks, success/error messages, spam/consent fields, and redirect behavior. Do not send real customer data unless the user authorizes it.
   - For ecommerce, map product discovery, category/listing template, filters, product detail, variation selection, price/stock display, add to cart, cart updates, coupons, shipping estimate, checkout fields, payment method display, login/guest checkout, order review, and confirmation path if safe or authorized.
   - For login-gated areas, include scenarios when credentials are unavailable: login page loads, validation messages, password reset, account creation, and a checklist item to validate internal account pages with credentials.
   - Check desktop and mobile/responsive behavior when feasible, especially menus, sticky headers, sliders, forms, product cards, cart/checkout, and long labels.
   - Inspect console errors and failed requests after interactions. Mention errors with the page/action where they appeared.
5. Read `references/test-taxonomy.md` when creating the final report or checklist. Use it as a coverage menu, not as a rigid template.

## Output Shape

Write in Portuguese unless the user asks otherwise. Keep the output practical for QA execution.

Use this structure:

```markdown
# Relatorio de auditoria exploratoria - [site]

## Escopo e premissas
- URL auditada:
- Data:
- Areas cobertas:
- Areas nao cobertas / dependencias:

## Funcionalidades encontradas
| Area/template | URLs ou exemplos | Funcionalidades/comportamentos | Observacoes de risco |
| --- | --- | --- | --- |

## Templates e paginas similares
| Grupo | Paginas identificadas | Pagina representativa para teste | Justificativa |
| --- | --- | --- | --- |

## Observacoes de comportamento
- [Area] comportamento observado, risco e evidencia.

## Checklist de testes pos-atualizacao
| Prioridade | Area | Cenario | Passos resumidos | Resultado esperado |
| --- | --- | --- | --- | --- |

## Pendencias para validar com acesso/dados reais
- Item pendente e o que e necessario para testar.
```

If the site is large, produce the functional report first and explain that the checklist can be expanded from the inventory. Do not omit the "Templates e paginas similares" section; the user specifically wants similar category/template pages mentioned even when only one representative page will be tested.

## Prioritization

Prioritize checklist items by likely update risk:

- P0: checkout, payment, forms that generate leads, login/account access, broken critical navigation, fatal errors, unavailable pages.
- P1: product/category behavior, filters, search, cart, checkout field validation, key marketing pages, mobile menu, cookie/consent, tracking-critical buttons.
- P2: animations, sliders, visual alignment, secondary pages, blog templates, embeds, cosmetic regressions, noncritical console warnings.

## Safety Rules

- Do not make real purchases, submit production forms, create public content, change account data, trigger emails at scale, or bypass access controls unless the user explicitly authorizes that action.
- Prefer test data clearly marked as QA when submission is authorized.
- If a site has rate limiting, CAPTCHA, payment, or login barriers, document the blocked scenario and propose the manual validation path.
- Treat the audit as exploratory coverage guidance, not proof that the site has no defects.
