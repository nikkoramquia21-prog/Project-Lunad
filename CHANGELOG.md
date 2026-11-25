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

### Added (later on 25 Nov)
- **Typed pickup and drop-off** — Ride and TODA Express use type-ahead fields (place, barangay or landmark) in place of dropdowns. Suggestions appear as you type; Enter picks the best match; an unlisted place is pinned near the town named in the text. The "use my location" button works for both forms.
- **Pasabuy** (inside TODA Express) — the booker lists items, an estimated cost and where to buy. It goes to the nearest TODA Express or LUNAD Moto Taxi rider and is never batched. The rider pays up to ₱1,000 with their own cash, enters the receipt total and attaches a photo (it appears in chat), then delivers. The booker pays back the goods plus fee (delivery + ₱30 shopping fee) by QR after the receipt, or in cash on arrival.
- **Chat** — direct messaging between the booker and the rider, with no phone numbers shown. It has pasabuy quick replies (e.g. "Out of stock — OK to substitute?") and is available from the booking card, the rider's job card and the arrival screen.

### Not changed
- Branding (logo, tagline, splash) is unchanged on purpose.

### Testing
- `tests/regression_v0.27.0.py` — 123 headless-Chrome checks covering passenger rides, shared car/van rides, TODA Express (sender pays, recipient pays + COD, batching, cancel, driver cancel, timeout, offline queue, storm pause), typed place fields, pasabuy (cap, receipt, chat, moto rider, cash on arrival), student verification, free backride, share lock, daily cap, driver rewards, registration, the business-review prompt, reset and reload. Result: 123/123 pass, no JavaScript errors.
