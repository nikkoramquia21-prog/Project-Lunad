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

- **Student persona** — the top toggle is now Passenger | Student | Driver. Student opens a ready-verified sample student (Mika Reyes, CatSU) with their own bookings and a student home. Switching back restores the tourist account.
- **Ride-along attached to TODA Express** — when a student books a free backride and an active TODA Express delivery is on the same route, the student booking is attached to that delivery. The rider accepts the student inside the delivery job card (Accept → Picked up student → Dropped off student), and the sender sees "A student is riding along". If the rider declines or doesn't answer in time, the booking detaches and goes to the normal TODA rider queue.
- The demo script beside the phone now includes the TODA Express and student ride-along steps.

- **Welcome screen: "I’m a student"** — a new button between Get started and I’m a driver. It opens the Student view.
- **Phone frame fix** — the welcome screen had square corners that stuck out past the rounded phone frame (a strip on the right). It now follows the frame. The header toggle (Passenger | Student | Driver) and the menu button fit inside the phone at every size, down to 320 px.

- **Ride-along-only rules for free student rides** — TODA riders never make a separate trip for a free student, and no driver ever sees a standalone student request.
  - A student booking joins a delivery when the rider has accepted it or already has the item on board, and the trip is on the student's route (pickups within 2 km; drop-offs within 2 km or in the same direction). One student per tricycle.
  - **No match → pop-up:** "No TODA Express rider is heading to … right now". The options are **Wait for a ride-along (up to 30 min)** (the student is added automatically when a matching delivery is accepted), **Book a paid ride instead** (switches to Moto Taxi), or **Cancel**.
  - If the rider declines, cancels or doesn't answer in 3 minutes, the student goes back on the waiting list and that rider isn't asked again. After 30 minutes without a match, the request ends with an option to book a paid ride.
  - The free-ride count only goes down when the student is matched. Waiting, no match and cancelling don't use a ride.
  - The sponsor pays the rider a flat **₱20 ride-along fee** instead of the full tricycle fare.

- **Free ride-along on 4-wheelers** — besides TODA Express deliveries, a verified student can take an empty seat on a car or van trip already going their way:
  - **Shared** car/van trips that still have a free seat, or **Solo** trips where the paying passenger ticked "Allow a verified student to ride along free on an empty seat".
  - The seat is free: no sponsor fee for 4-wheel drivers, who still earn student reward points. Paying passengers' fares don't change.
  - The driver accepts the student inside the job card, like TODA riders do.
  - **LUNAD Moto Taxi never carries ride-alongs.** Pasabuy trips are never joined either.
  - Not yet for live multi-phone shared rides (QR join). Those still run on their own sync.

- **Student features only in the Student account** — Passenger no longer shows the Home "Free student rides" row, the Ride-tab student promo, the free ride-along option or the Profile verification card. Students use the Student toggle.
- **No-match pop-up explains why** — e.g. "Only a LUNAD Moto Taxi is going that way — Moto Taxi can’t take ride-alongs", "the passenger didn’t allow a student ride-along", "a Pasabuy trip…", "still waiting for a driver — tap Wait", or "the rider already has a student".
- **Shared rides reach drivers in the claude.ai viewer** — when live phone-to-phone sync isn't available, Shared car/van rides switch to demo mode automatically (sample co-passengers) and go straight to drivers, so students can join them.
- **Driver toggle opens the right driver** — the driver holding the student's ride-along, or the newest booking/delivery waiting for action.

- **"On the way" matching for ride-alongs** — fixes CatSU students not being matched to trips from Virac Public Market (2.4 km apart; the old rule needed the student within 2 km of the trip's *start*). A student now joins when:
  - their pickup is along the trip's route (within 1.5 km of the line from its pickup to its drop-off) or within 2 km of its pickup; and
  - their drop-off is further along that route or within 2 km of the trip's drop-off.
  - The no-match pop-up also says when a running trip is close but off-route ("your pickup is 2.3 km off its route") or ends before the student's destination.

### Not changed
- Branding (logo, tagline, splash) is unchanged on purpose.

### Testing
- `tests/regression_v0.27.0.py` — 193 headless-Chrome checks covering passenger rides, shared car/van rides, TODA Express (sender pays, recipient pays + COD, batching, cancel, driver cancel, timeout, offline queue, storm pause), typed place fields, pasabuy (cap, receipt, chat, moto rider, cash on arrival), student persona, ride-along attach / decline / timeout / different-route, student verification, free backride, share lock, daily cap, driver rewards, registration, the business-review prompt, reset and reload, plus welcome-screen student button and phone-frame/header fit at 1280×900, 1280×700 and 360×740. Result: 193/193 pass, no JavaScript errors.
