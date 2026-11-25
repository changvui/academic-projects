# CarGrow — design notes

CarGrow is an Ethereum dApp for **milestone-based logistics escrow**. A shipper locks the
freight payment in a smart contract; the carrier is paid in three releases as the shipment
moves. The point is to take the payment decision away from an intermediary and put it into
code both sides can read.

Coursework project for **BMIS2003 Blockchain Application Development** (TAR UMT, 2026),
four-person team. Solidity `^0.8.24`, Hardhat, MetaMask, Ganache, plain JavaScript front end.
See `README.md` for the setup and demo steps.

## Contract model

**Roles.** Two actors, registered on chain: `Shipper` (pays) and `Carrier` (moves the cargo).
Role checks are enforced with a modifier, so only the right side can call each function.

**Agreement lifecycle.**

```
Open ──accept──▶ Accepted ──fund──▶ Funded ──milestone 3──▶ Completed
  │                  │                 │
  └──cancel──────────┘                 ├── settle (expired) ──▶ Refunded
                                       └── claim refund ─────▶ Refunded
```

**Milestones.** Fixed at creation, expressed in basis points of the contract value:

| # | Milestone | Share |
|---|-----------|-------|
| 0 | Cargo pickup at origin | 30% |
| 1 | In-transit / customs clearance | 30% |
| 2 | Final delivery to destination | 40% |

Each milestone carries an evidence reference and a hash, so the document that justified a
payout can be checked later without putting the document itself on chain.

**Reputation.** A completed agreement awards reputation points to the carrier, emitted as an
event. It is a small signal — not a credit score — but it gives a shipper something to look at
beyond price.

## Safety details worth pointing at

- `nonReentrant` on the functions that move ETH, because the payout path is the obvious attack
  surface.
- `validAgreement` on every agreement-scoped call, so an out-of-range id reverts instead of
  reading empty storage.
- Explicit exits: a carrier can cancel an agreement nobody funded; a shipper can claim a refund
  after expiry. Without those two paths, a stranded agreement has no way out.
- Status is an enum, not a free string, so an invalid state cannot be written.

## What this does not solve

- **Physical verification.** The chain records who claimed a milestone and what evidence they
  submitted. It cannot confirm the cargo was actually on the truck.
- **Disputes.** There is no arbitration role. If the shipper refuses to confirm a milestone, the
  only exit is the expiry path.
- **Fiat.** Everything is in test ETH on a local Ganache chain; no real money moved.

## Team

Four-person coursework team. The repository contains the full submission: contract, deployment
script, front end and the setup guide.
