# CarGrow — decentralized escrow for cargo logistics

Coursework design project for **BMIS2003 Blockchain Application Development** (TAR UMT, 2026).
Four-person team. The deliverable was a full application design, not a deployed contract:
business case, smart contract rules, data model and a walkthrough of the flows.

## The problem

Cross-border cargo moves through intermediaries — banks, freight forwarders, agents — and each one
adds cost, delay and a paper trail nobody can verify. Three things go wrong repeatedly:

- Settlement is slow and expensive because every party holds its own copy of the truth.
- Compliance documents are manual, so they can be forged or lost.
- The buyer has no proof that funds are used for the shipment they paid for.

## The design

**Escrow in a smart contract.** The buyer pre-funds the contract value in ETH. The money is not
released to the carrier until the contract's own conditions are met, so trust moves from the
intermediary to the code.

**Milestone payouts.** Payment is released in fixed portions as the shipment progresses:

| Milestone | Trigger | Payout |
|-----------|---------|--------|
| 1 | Cargo picked up | 30% |
| 2 | In transit | 30% |
| 3 | Final delivery | 40% |

**Evidence hashing.** Each milestone is backed by a document (pickup note, transit record, delivery
receipt). The document itself is not stored on chain — its hash is, so any party can later prove the
paperwork has not changed.

**Wallet-based identity.** Carriers are identified by wallet address rather than an account in a
central system, so a carrier's delivery history is portable and public.

## Business rules encoded in the contract

- An agreement needs a cargo description, origin and destination, a contract value in ETH, and a
  delivery deadline that must be in the future.
- Only a registered carrier can accept an open agreement, and the agreement must not be expired.
- Acceptance flips the status from `OPEN` to `ACCEPTED` and assigns exactly one carrier — no other
  carrier can take the same shipment.
- Milestone payouts total exactly 100% of the contract value.

## Design decisions worth noting

- **Why milestone escrow and not one payment on delivery?** Carriers will not front fuel and labour
  for a full route with no money released; buyers will not pay everything up front. Splitting at
  pickup / transit / delivery is the smallest number of checkpoints that both sides accept.
- **Why hash the documents instead of storing them?** On-chain storage is expensive and public.
  A hash gives the same tamper-evidence without putting a bill of lading on a public ledger.
- **What the design does not solve:** physical verification. Someone still has to confirm the cargo
  was actually picked up; the chain records who claimed it, not whether it happened.

## Note

This was a design assignment for the course — the contract was specified in detail but not deployed
to a testnet. The written report contains teammates' student IDs, so it is not included here.
