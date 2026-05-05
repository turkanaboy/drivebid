# DriveBid — Feature Roadmap

**Version:** 0.1  
**Last updated:** May 2026

This document tracks what has been built in prototype, what is planned for each development phase, and what has been deliberately deferred with reasoning.

---

## Prototype status (current)

All items below exist as interactive HTML prototypes. No backend, no persistence, no authentication. Data is simulated.

### ✅ Built and prototyped

**Customer portal**
- Home / value proposition page with stats
- Request form (vehicle type, condition, transaction type, timeline, preferred makes, dealer radius, budget slider, feature tag selection, free-text notes, ZIP code)
- AI advisor chat (scripted conversation tree covering family cars, EVs, trade-ins, commute patterns, budget guidance, and request posting handoff)
- Bids board with ranked offers, match scores, fair market value comparison, feature matching, and express interest / accept actions
- Member vs. free tier gating UI
- $20 one-time unlock flow with payment modal

**Dealer portal**
- Five-step onboarding and verification flow (business info, license & credentials, inventory connection, plan selection, review & submit)
- Real-time verification checklist sidebar
- Post-submission timeline (pending → document review → identity verification → inventory sync → activated)
- Verified account state with dealer profile card preview
- Dashboard with live stats and activity feed
- Lead management board with match scores, responsiveness badges, and claim buttons
- Inventory manager with match counts and send-offer shortcuts
- Offer builder with live customer-facing preview and FMV comparison

**Shared / cross-platform**
- Dealer-customer messaging threads (both customer and dealer views)
- Offer card in messaging thread (structured deal summary)
- Counter offer modal
- Accept offer flow with deal-in-progress UI state
- 24-hour claim window mechanic with live countdown
- Claim simulation (accept / counter / pass / extend / expire / reset)
- Responsiveness score system with score ring, breakdown bars, claim history table, score bands, and "what dealers see" preview
- Notifications inbox (filterable, unread states, inline countdown bars, contextual action buttons)
- Deal status pipeline (six-stage visual tracker, activity timeline, deal snapshot)
- Notification preferences (per-notification channel controls: email, push, SMS)
- Email notification preview (claim alert with offer summary, countdown, one-click actions)

---

## Phase 1 — MVP (first real users)

**Goal:** A working closed beta with real dealers and real customers in one metro area. Validate the core marketplace dynamic before scaling.

### Backend foundation
- [ ] Database schema (users, requests, offers, messages, notifications, deals)
- [ ] Authentication (customer accounts, dealer accounts, session management)
- [ ] API layer (RESTful or GraphQL — TBD based on tech stack decision)
- [ ] Secure file storage for dealer credential documents
- [ ] Email delivery (transactional — Sendgrid, Postmark, or similar)
- [ ] Basic push notification infrastructure

### Customer features
- [ ] Account creation and login
- [ ] Request persistence (saved requests, edit, close)
- [ ] Live bid notifications
- [ ] Real messaging (dealer messages actually arrive)
- [ ] Deal status tracked in database
- [ ] Responsiveness score calculated and stored

### Dealer features
- [ ] Dealer account creation and verification workflow (manual review by DriveBid team initially)
- [ ] Real lead feed (populated from actual customer requests)
- [ ] Offer submission stored and delivered to customer
- [ ] Messaging from dealer side
- [ ] Basic dashboard with real data

### AI advisor
- [ ] Connect to Anthropic API (Claude Sonnet) for real open-ended conversations
- [ ] System prompt engineering for advisor persona (no commission, no pressure, help clarify needs)
- [ ] Pre-fill request form from advisor conversation context
- [ ] Rate limiting and cost controls

### Payment
- [ ] Stripe integration for $20 customer unlock
- [ ] Stripe integration for dealer subscription billing
- [ ] Unlock expiry logic (deal close trigger or 90-day inactivity)

### Fair market value data
- [ ] Integrate a market data source (Black Book, Edmunds API, or similar)
- [ ] FMV display on offer cards and messaging
- [ ] FMV comparison in offer builder (dealer-side)

---

## Phase 2 — Growth features

**Goal:** Expand what the platform can do once the core marketplace is validated with real usage data.

### Document preparation layer
- [ ] Legal and compliance review (CFPB, state DMV rules, GLBA for financial data)
- [ ] Customer profile data mapped to standard form fields
- [ ] RouteOne / Dealertrack API integration for credit application pre-fill
- [ ] State DMV title transfer template library
- [ ] Secure document vault (customer side — permissioned dealer access)
- [ ] "Ready to Close" packet — assembles pre-filled deal documents for dealer
- [ ] Available as premium feature for unlocked customers and Pro/Elite dealers

### DMS inventory integration
- [ ] CDK Global API integration
- [ ] Reynolds & Reynolds integration
- [ ] Dealertrack integration
- [ ] DealerSocket integration
- [ ] vAuto integration
- [ ] Real-time inventory sync and match scoring against active customer requests

### Enhanced customer features
- [ ] Saved search profiles and deal alerts
- [ ] Multi-vehicle comparison mode (Pro tier)
- [ ] Price history and trend data (Pro tier)
- [ ] Dealer performance reports (Unlocked tier)
- [ ] Concierge negotiation mode (AI-assisted counter offer suggestions)

### Enhanced dealer features
- [ ] Full analytics dashboard (lead conversion rates, response times, win/loss by vehicle type)
- [ ] Automated inventory matching alerts ("new request matches your Pilot")
- [ ] Offer templates (save and reuse standard lease/finance structures)
- [ ] Dedicated account rep assignment (Elite tier)

### Mobile
- [ ] Mobile-optimized responsive design (current prototypes are desktop-only)
- [ ] Native iOS and Android apps (evaluate post-beta based on usage patterns)
- [ ] Push notifications via APNs / FCM

---

## Phase 3 — Scale and ecosystem

**Goal:** Platform network effects, geographic expansion, and partnership integrations.

### Geographic expansion
- [ ] Multi-market rollout strategy
- [ ] Nationwide dealer radius (already designed into pricing tiers)
- [ ] Market-specific FMV calibration

### Ecosystem integrations
- [ ] Auto insurance partners (post-deal cross-sell, ad placement)
- [ ] Warranty providers (extended warranty offer at deal close)
- [ ] Lender marketplace (customer can compare financing offers from multiple lenders, not just dealer-offered)
- [ ] Trade-in valuation integration (CarMax Instant Offer, KBB Instant Cash Offer, or similar)

### Trust and safety
- [ ] Expanded dealer review system (post-deal customer ratings)
- [ ] Dispute resolution process for deal disagreements
- [ ] Fraud detection for fake requests
- [ ] Dealer performance monitoring and badge revocation

---

## Deliberately deferred items

These features were discussed and consciously excluded from the current scope with documented reasoning.

| Feature | Decision | Reason |
|---------|----------|--------|
| Document prep / paperwork | Phase 2 | Requires legal compliance review before building; should not block MVP validation |
| Real AI in chat advisor | Phase 1 | Free tier works fine for demos; adds API cost before revenue; backend required for proper implementation |
| Backend infrastructure | Phase 1 | Prototype stage exists to validate concept first; no point committing to a stack before the product is proven |
| Mobile app | Phase 2 | Desktop-first for beta; mobile investment justified only after validating web usage patterns |
| Financing marketplace | Phase 3 | Requires lender relationships and additional regulatory consideration |
| Lender pre-qualification | Phase 2 | Valuable but complex; customer data privacy and CFPB compliance require dedicated effort |
| Recurring customer subscription | Rejected | Car buying cycle is 3–7 years; subscriptions are psychologically misaligned with the use case |

---

## Open questions

These are product decisions that haven't been finalized and will likely need input from early users or legal counsel.

**What triggers "deal closed" for unlock expiry?**
Current plan: customer marks deal as accepted in DriveBid, or 90 days of inactivity. Edge case: customer uses DriveBid to find a deal but closes it off-platform. Needs a trust-based or self-reported mechanism.

**How should the responsiveness score handle new users?**
Currently: new users start neutral (no score shown). Alternative: show "New user — no history" explicitly to dealers so they can make an informed claim decision.

**Should dealers be able to see which other dealers have claimed the same customer?**
Currently: no. Dealers know a window is open or closed but don't see who else is involved. This protects competitive sensitivity but may frustrate dealers wondering why a window is locked.

**What happens if a dealer submits a fraudulent or misleading offer?**
Phase 1 relies on manual oversight and dealer verification. Phase 3 needs an automated monitoring system and a clear dispute resolution process.

**At what point does the AI advisor need to disclose it's an AI?**
Legal and ethical question, especially as states begin regulating AI disclosure in consumer contexts. Build disclosure into the advisor UI from day one to be safe.

**What data can DriveBid share with ad partners?**
Ad revenue is planned but no data sharing policy has been designed. This needs legal review before any ad integrations are built.

---

## Tech stack — not yet decided

No tech stack decision has been made. The following are considerations for when that conversation happens.

**Frontend:** React or Next.js are the natural choices given component reuse across customer and dealer portals. The prototype HTML files serve as the design specification.

**Backend:** Node.js, Python (FastAPI/Django), or Ruby on Rails are all viable. Choice should reflect the founding team's strengths and hiring market.

**Database:** PostgreSQL is the default choice for a marketplace with relational data. Redis for session management and real-time features.

**Hosting:** AWS, GCP, or Vercel/Railway depending on scale expectations and ops preference.

**Recommendation:** Use a backend-as-a-service (Supabase, Firebase, or PlanetScale) for the closed beta to move faster before committing to full infrastructure.
