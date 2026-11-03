# Five-minute project walkthrough

1. **Problem (30 seconds):** Explain the product/payment/region combinations and
   why one long dependent test leaves coverage gaps after a failure.
2. **Dashboard (60 seconds):** Show the overview screenshot, target URL input,
   optional per-run account selection, run history, outcome graph and duration graph. State that the displayed data
   is synthetic and that this public repository does not run the system.
3. **Coverage (60 seconds):** Explain the five independent purchase scenarios
   and the sixth delivery-fee comparison. Distinguish gateway initiation and
   unpaid orders from successful financial settlement.
4. **Failure analysis (60 seconds):** Open the scenario-details screenshot.
   Describe per-action timing, screenshots, videos, test-data capture and traces.
   Explain why later scenarios continue and why uncertain purchases are not retried.
   Use the nested-address and cancelled-order examples in `UPDATES.md` to discuss
   the difference between an automation limitation and a merchant state change.
5. **Architecture (45 seconds):** Walk through FastAPI, queue/metadata, Chromium,
   persistent evidence, reports and optional completion callback.
6. **Tradeoffs (45 seconds):** Discuss dynamic product eligibility, shared-account
   serialization, deployment credentials, regional rules and maintenance after UI changes.

Do not share live credentials, internal hosts or customer evidence in an interview.
This package contains screenshots, not a video or a public live demo. A future
recording should use the same isolated synthetic environment.
