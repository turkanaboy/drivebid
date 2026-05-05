# DriveBid

> The reverse car marketplace. You post what you want. Dealers compete for your business.

DriveBid inverts the traditional car-buying experience. Instead of customers walking onto dealer lots and negotiating from a weak position, customers post a structured request — budget, vehicle type, must-have features, timeline — and verified dealers compete by submitting matched offers.

---

## What's in this repository

```
drivebid/
├── README.md                          # This file
├── prototypes/                        # HTML prototype files (no dependencies)
│   ├── customer-portal.html           # Customer home, request form, AI advisor, bids board
│   ├── dealer-onboarding.html         # Dealer verification & onboarding flow
│   ├── messaging.html                 # Dealer-customer messaging threads (both views)
│   ├── tiers-claims-score.html        # Pricing tiers, 24-hr claim mechanic, responsiveness score
│   └── notifications.html            # Notifications, deal status pipeline, preferences, email preview
├── docs/
│   ├── product-overview.md            # Full product description, decisions, and rationale
│   └── feature-roadmap.md            # Phased roadmap with priorities and open questions
└── src/                              # Reserved for production code (not yet built)
    ├── frontend/
    ├── backend/
    └── shared/
```

## Viewing the prototypes

All prototype files are standalone HTML — open any of them directly in a browser. No server, no dependencies, no build step required.

## Status

**Phase:** Prototype / pre-development  
**Stage:** All core flows designed and prototyped. Ready for tech stack decision and beta planning.

## Docs

Start with [`docs/product-overview.md`](docs/product-overview.md) for a full picture of what DriveBid is, how it works, and the decisions made during product design.

Then read [`docs/feature-roadmap.md`](docs/feature-roadmap.md) for what's been built, what's planned, and what's deliberately deferred.
