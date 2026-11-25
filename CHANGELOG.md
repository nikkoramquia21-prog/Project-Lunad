# Changelog

## v0.27.0 — TODA Express, Student Mobility, Driver Rewards

Previous version is preserved on branch `release/v0.26.2`.

### Changed
- **TODA passenger ride booking removed.** Regular passengers now book LUNAD Moto Taxi, private car or van. Shared TODA tricycle rides are removed (shared car/van rides stay).
- **TODA drivers are now TODA Express riders** (sample data renamed: Mang Rudy, Aling Bing, Kuya Ben, Leo). New TODA registrations sign up as TODA Express riders.

### Added
- **TODA Express** — same-day local delivery: pickup, delivery location, item description, item category, recipient name and mobile. Payment is by the sender now (QR) or by the recipient on arrival, with optional COD for sellers. The nearest TODA Express rider is assigned automatically. Rider steps: Accept → Arrived → Picked up → Delivered. Sender gets a delivery confirmation and can review; the recipient gets an SMS.
- **Same-route batching** — a rider can carry up to 3 deliveries at once when pickups are within 2 km and drop-offs are within 2 km or in the same direction (±45°). Batched deliveries get 20% off.
- **Student Mobility Program** — students verify with a school ID (required) and optional registration document. Status goes Pending → Verified Student (demo approve button).
- **Free TODA backride for verified students** — 2 rides per day, ₱0 to the student, with the standard fare paid to the rider by the program (sponsor: LGU / schools / local business CSR, sample). Students are matched first with a TODA rider already delivering on the same route.
- **Share-to-unlock** — after each free ride, a pop-up asks the student to share on Facebook or Instagram (it replaces the driver review). The next free ride stays locked until they share.
- **Driver Rewards** — points for rides, deliveries, student rides, 5-star ratings, positive reviews and 5-day activity; tiers, badges; redeem for priority booking or a matching boost (both move the driver up in dispatch). Fuel and maintenance perks are shown as coming soon.

### Not changed
- Branding (logo, tagline, splash) is unchanged on purpose.

### Testing
- `tests/regression_v0.27.0.py` — 93 headless-Chrome checks covering passenger rides, shared car/van rides, TODA Express (sender pays, recipient pays + COD, batching, cancel, driver cancel, timeout, offline queue, storm pause), student verification, free backride, share lock, daily cap, driver rewards, registration, the business-review prompt, reset and reload. Result: 93/93 pass, no JavaScript errors.
