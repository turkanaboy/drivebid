# DriveBid — Product Overview

**Version:** 0.1 (prototype)  
**Last updated:** May 2026  
**Status:** Pre-development — all flows prototyped, backend not yet built

---

## What is DriveBid?

DriveBid is a reverse car marketplace. In a traditional dealership model, buyers visit lots, face pressure tactics, and negotiate from a position of information disadvantage. DriveBid inverts this entirely:

1. A customer posts a structured request describing what they want (vehicle type, budget, features, timeline)
2. An AI advisor helps refine the request into a clear, actionable brief
3. Verified dealers see the request and compete by submitting matched offers
4. The customer reviews offers with fair market value data visible, negotiates via messaging, and accepts on their own terms

The platform serves two distinct user types — customers and dealers — each with their own portal, dashboard, and notification system.

---

## Core product decisions

### Fair market value is always free

Fair market value data is shown on every offer, for every user, at no cost. This was a deliberate decision: hiding FMV behind a paywall would undercut the core promise of the platform ("we're on your side") and leave uninformed buyers vulnerable to lowball offers. Free FMV also self-regulates dealer behavior — dealers know customers can see market comparisons, so submitting above-market offers is immediately visible and counterproductive.

### Pricing: free tier + $20 one-time unlock

There is no subscription. Car buying happens once every few years — a monthly recurring fee makes no sense for the average customer. Instead:

- **Free tier:** 1 active request, dealers within 50 miles, full AI advisor, fair market value, messaging, offer comparison, 24-hr claim protection, responsiveness score
- **Unlocked ($20, one-time per deal):** Up to 3 simultaneous requests, nationwide dealer radius, priority placement, dealer performance reports, price history and trend data, multi-vehicle comparison, saved search profiles

The unlock expires when the deal closes (or after 90 days of inactivity). Customers pay $20 again next time they buy. No auto-renewals, no subscriptions.

### The 24-hour exclusive claim window

When a dealer claims a customer's request, the customer gets an exclusive 24-hour window to respond — accept, negotiate, or pass. During this window, no other dealer can claim the same request.

This mechanic exists to protect dealers from investing time building offers that get ignored, which would erode marketplace participation over time.

**Rules:**
- Accepting opens the full messaging thread
- Negotiating (sending a counter) pauses the countdown until the dealer replies
- Passing releases the window with no score penalty — the next dealer can claim immediately
- The clock pauses if the dealer goes quiet mid-negotiation (customer not penalized for dealer's silence)
- One 24-hour extension is available per claim window, usable once
- Letting the clock expire without any response is the only action that negatively affects the customer's responsiveness score

### Responsiveness score

Every customer has a visible responsiveness score (0–100) that dealers can see before deciding whether to claim a request. The score reflects how reliably the customer responds to claim windows.

**What counts in the customer's favor:** Any response within the window — accept, counter, or pass — is a positive signal. Engagement matters, not selectivity.

**What hurts the score:** Only unanswered (expired) windows count negatively. Denying or passing on offers does not count against the score.

**Score bands visible to dealers:**
- 80–100: Highly responsive — dealers are significantly more likely to invest in a strong offer
- 50–79: Fair — dealers may deprioritize in favor of higher-scoring buyers
- Below 50: Low — dealers are notified; some lead slots may be restricted until score recovers

**Score recovery:** Expired windows have diminishing impact over time as the customer builds a longer positive history. New users start with a neutral score.

### Document preparation is a Phase 2 feature

Paperwork (credit applications, DMV forms, trade-in documentation) will not be part of the initial product. This decision was made for three reasons:

1. Credit application and DMV filing require legal compliance review (CFPB, state DMV rules, GLBA) before building — rushing this into v1 would likely require rebuilding it
2. The core value proposition — the marketplace itself — should be validated first
3. A pre-filled document packet is a natural upgrade feature that strengthens the Phase 2 pitch to investors

When built, the model will be: the platform pre-fills standardized templates from customer profile data, and the dealer retains responsibility for final submission and legal compliance. The goal is to compress the signing process, not replace dealer back-office operations.

### Backend is deliberately deferred

All current prototypes are static HTML with simulated data. The backend has not been built. This is intentional — the prototype stage exists to validate the product concept before committing to a tech stack or infrastructure investment.

When the backend is built, it will need at minimum:
- A database (users, requests, offers, messages, documents)
- Authentication (customer and dealer accounts, dealer verification status)
- An API layer connecting frontend to database
- Email and push notification delivery
- Secure file storage (dealer credential documents)
- DMS integrations for real-time dealer inventory sync (CDK, Reynolds & Reynolds, Dealertrack, DealerSocket, vAuto)

---

## The two-sided marketplace

### Customer side

**Home / onboarding:** Value proposition, how-it-works flow, key stats (avg. savings, dealer count, time to first offer)

**Request form:** Vehicle type, condition (new / CPO / used), transaction type (purchase / lease / either), timeline, preferred makes, dealer radius, max monthly budget (slider), must-have features (tag selection), free-text notes, ZIP code

**AI advisor:** Conversational advisor that helps customers who don't know car jargon articulate their needs into a clear dealer brief. No commission, no pressure. Scripted for prototype; designed to be replaced with real API calls when ready.

**Bids board:** Incoming dealer offers ranked by match score. Each offer shows: vehicle details, monthly payment, term, due at signing, features matched vs. missing, fair market value comparison, dealer rating and distance. Customer can express interest, message dealer, accept, or counter.

**Messaging:** Full conversation threads with dealers. Each thread shows the offer terms at the top, a deal info panel on the right, and quick-reply shortcuts. Counter offers trigger a modal. Accepting updates the UI to "deal in progress."

**Notifications:** Filterable inbox with urgency levels. Time-sensitive alerts (claim windows, expiring counters) include live countdown bars. Email notifications include one-click accept/counter/pass links.

**Deal status pipeline:** Six-stage visual pipeline per active deal (Request posted → Offer received → Negotiating → Offer accepted → Appointment scheduled → Deal closed). Both sides see the same pipeline. Each stage shows timestamps, a current-action prompt, activity timeline, and a deal snapshot.

### Dealer side

**Onboarding & verification:** Five-step application flow: business information, license & credentials (dealer license, insurance, surety bond, identity verification), inventory connection (DMS integration or CSV upload), plan selection, review & submit. Includes a real-time verification checklist in the sidebar and a post-submission timeline showing review status. Verified badge appears on dealer profile cards visible to customers.

**Dashboard:** Live stats (new leads, active offers, acceptance rate, monthly revenue), high-intent lead alerts, recent activity feed.

**Lead management:** Incoming customer requests ranked by match score. Each lead shows match percentage, customer's responsiveness score and response history, request details, and a claim button. Leads with low responsiveness scores are visually de-emphasized; very low scores lock the claim button.

**Inventory manager:** Vehicle cards showing stock, MSRP, and number of active customer matches. Quick-send-offer button routes to the offer builder.

**Offer builder:** Form for constructing a deal (vehicle, transaction type, monthly payment, term, APR/money factor, at-signing amount, trade-in offer, dealer notes). Live preview panel updates in real time showing what the customer will see, plus a fair market value comparison and match score summary.

**Messaging:** Same thread view as customer side but from dealer's perspective. Quick-reply shortcuts are dealer-specific (share revised offer, confirm availability, schedule test drive, trade-in appraisal).

---

## Dealer pricing tiers

Dealers pay to participate. Customer use is free (with optional $20 one-time unlock).

| Tier | Price | Leads | Radius | Key features |
|------|-------|-------|--------|--------------|
| Starter | $149/mo | 5/mo | 25 mi | Basic match scoring, offer builder |
| Pro | $349/mo | Unlimited | 50 mi | FMV data, priority placement, dealer analytics |
| Elite | $749/mo | Unlimited | Nationwide | Full analytics, dedicated account rep, top placement |

All plans include a 30-day free trial. Billing begins only after dealer verification is approved.

---

## Revenue model

1. **Dealer subscriptions** — primary revenue. Dealers pay monthly for lead access. High-intent, qualified leads justify the fee.
2. **Customer unlock** — $20 one-time per deal cycle. Secondary revenue. Volume-dependent.
3. **Ad revenue** — non-intrusive placements from auto insurance, warranty providers, and lenders. High-CPM inventory due to purchase intent. Ads kept out of the dealer bid flow to preserve trust.

---

## What DriveBid is not

- Not a financing platform (dealers handle their own financing, DriveBid surfaces the terms)
- Not a document filing service (Phase 2 consideration)
- Not a lead generation service in the traditional sense — the customer controls the relationship, not the dealer
- Not a subscription product for customers (one-time unlock only)
