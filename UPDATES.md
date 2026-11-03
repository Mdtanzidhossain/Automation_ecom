# Recent engineering updates

Last updated: 3 November 2026.

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

## Verification status

The latest focused Docker Chromium verification passed 116 checks. The broader
offline suite previously passed 263 checks with 56 skipped. These counts describe
different test selections and should not be added together as unique coverage.

An earlier live E2E run passed all six scenarios. A later seeded run passed four
and exposed the two cases described above. The latest fixes are locally verified;
their live E2E rerun is pending deployment. No new live orders were placed for
the latest focused checks or for this portfolio update.
