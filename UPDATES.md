# Recent engineering updates

Last updated: 25 November 2026. Latest execution evidence: 22 November 2026.

This page describes private implementation work. It contains no executable
automation source, account credentials or customer evidence. Existing screenshots
illustrate the dashboard using synthetic data; they are not screenshots of the
latest live verification.

## Account-specific test runs

QA and developers can supply optional shopping-account credentials alongside the
target URL. This lets the same suite exercise accounts assigned to different A/B
variants. Both fields are required together; leaving both blank uses the server
default when configured.

Overrides are scoped to one run. The service does not persist the custom password
in run history or pass it as a command-line argument. Credential fingerprints
support request identity checks, and authentication diagnostics are sanitized.
Reports and recordings remain access-controlled evidence that needs careful
handling; this portfolio does not publish them.

## Nested address selection

Some regional address branches require another location selection after district
and area. The previous assumption that every branch ended after two selections
caused a scenario to stop before payment.

The runner now follows additional levels until the picker commits a final
location. It waits for actual option changes, tolerates an empty loading state,
records the selected path, and limits traversal depth. A stuck picker fails
instead of looping forever or saving an incomplete address.

## Unexpected cancellation diagnostics

A Book/bKash scenario successfully created an order and opened the gateway, but
the order was subsequently shown as cancelled. The cancelled card had no tracking
link, so the previous link-based assertion produced a misleading timeout.

Order identity is now checked independently of the tracking link. A cancelled
order produces an explicit failure with its status and supporting evidence. The
suite does not mark it as passed, silently create a replacement, or claim to know
who cancelled it. Merchant audit logs are needed to establish the cause.

## Other checkout reliability changes

- Recover supported storefront GET-navigation interruptions without retrying
  purchase submissions.
- Wait for interactive cart handlers and inspect current button state before
  deciding whether an add operation is needed.
- Accept canonical product slugs only when the product type and numeric identity
  match; verify bilingual names against recorded pre-purchase data.
- Compare subtotal, delivery, known discounts and payable amount consistently.
- Preserve native Rocket merchant-response verification across a page refresh.
- Keep report downloads on the dashboard origin instead of stale localhost links.

## Storefront and checkout redesign compatibility

The redesigned homepage offers a button to return to the old storefront. The
runner now selects that visible control when necessary and verifies the legacy
search UI before proceeding. An already selected legacy storefront continues
normally. A bounded second attempt handles a version-preference click that
leaves the new homepage active. Current DOM evidence is saved after reloads.

The redesigned login defaults to mobile-number mode. Email-based runs explicitly
select the Email radio, verify the input mode and continue with the account's
password flow. Both older login forms and the redesigned form remain supported.

My Orders changed its header from `Order ID:` to `Order #` and now uses article
cards with separate product thumbnail and title links. Verification supports
both structures while retaining exact order identity, product quantities,
prices, package composition and invoice checks. Tracking payment controls also
support their current `aria-pressed` selection state.

Buy Now now redirects to `/quick-cart/shipping?bn=...`. The runner accepts the
reviewed legacy and current routes only when the numeric product identity is
preserved. Receipt capture and preview write guards also recognize the new route.

## Verification status

On 22 November, 156 related Docker Chromium checks passed, followed by 22 focused
quick-cart checks. These selections overlap and are not additive unique coverage.
Earlier broader offline verification recorded 263 passed and 56 skipped.

All six live scenario outcomes were verified across attempts: four existing
orders were reconciled without replacement checkout submissions, one fresh
Buy Now purchase completed the remaining flow, and regional delivery comparison
passed. This was not one uninterrupted fresh 6/6 run. The initial failures remain
recorded in private reports rather than being rewritten as successful attempts.
Online payment checks cover gateway or merchant initiation and unpaid state;
financial settlement is outside this verification.

The latest implementation was submitted for internal review. Deployment status
has not been independently confirmed in this public case study. No additional
live tests or purchases were performed for the 25 November portfolio update.

## CI/CD status

Execution currently uses the Dockerized dashboard/API or CLI. A personal GitHub
Actions experiment is planned, but a completed GitHub Actions test run is not
claimed here. This public repository contains showcase documentation and demo
screenshots; the automation implementation remains private.
