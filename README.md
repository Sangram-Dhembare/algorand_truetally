# TrueTally

TrueTally is a course project exploring how Algorand can provide a public
record of election setup and published results. The first version will let an
administrator register an election, lock its configuration, and later publish
a digest of the final tally. Anyone will be able to compare those records
with the data published off-chain.

The ledger will store digests, not ballots or voter information. A recorded
digest can show that data has not changed since it was submitted. It cannot
prove that an election was run correctly or that a tally is accurate.

## Planned milestones

1. Define the election configuration and result formats, including how their
   digests are calculated.
2. Build an Algorand smart contract for registering an election, locking its
   configuration, and recording a final result digest.
3. Test permitted state changes, rejected updates, and administrator access.
4. Add a client and deployment instructions after the contract behavior is
   covered by tests.

## Current status

This repository contains the initial project definition. Contract code,
deployment scripts, and a client have not been added. No election data has
been submitted or deployed.

## Scope and limits

TrueTally is an educational prototype. It will not collect votes or personal
information. The project does not provide voter authentication, eligibility
checks, ballot secrecy, or a way to verify the correctness of a tally.
Recording a digest on Algorand does not make an election secure or suitable
for real-world use.
