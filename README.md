# TrueTally

TrueTally is a concept project for a campus voting app built on Algorand. It explores whether a blockchain-based voting flow can make each ballot and tally update easier to inspect after an election. The goal is not to build a production election system, but to test the mechanics of on-chain voting in a small, educational setting.

## Why this project exists

Campus elections often need a process that is simple to observe, easy to audit, and clear in how results are computed. A blockchain ledger can make each vote submission visible and each tally update traceable, but it also raises real concerns around privacy, voter identity, and asset control. TrueTally is an experiment in balancing those trade-offs.

## How the proposed flow works

- An election administrator defines the election, lists the candidates, and registers the eligible voters.
- Each eligible voter receives a unique election-specific Algorand Standard Asset (ASA).
- When a voter chooses a candidate, they transfer that asset to the wallet associated with that candidate.
- The vote transaction is intended to be an atomic group that contains both the asset transfer and an application call.
- The smart contract checks that the election is open, the voter is eligible, and the voting asset has not already been used.
- If any part of the group fails, the whole group fails, so a voter cannot partially submit a ballot or separate the transfer from the tally update.

This design is meant to provide stronger transaction-level evidence than a traditional off-chain tally. It still needs careful rules for asset handling. Algorand assets are not automatically non-transferable. The design must use controls such as freeze, clawback, or application-level checks so a voting asset cannot be reused or moved outside the voting flow.

## Proposed technology stack

- Algorand smart contracts written in Python using AlgoKit and the Algorand Python SDK
- LocalNet for local development and automated testing, and TestNet for a public test deployment
- A lightweight web client built with the Algorand JavaScript SDK
- Pera Wallet integration through WalletConnect for wallet authentication and transaction signing

LocalNet is intended for fee-free development. TestNet transactions use test ALGO and are not mainnet transactions.

## Planned milestones

1. Define the election, candidate, and voter state, including asset transfer restrictions and tally rules.
2. Implement the contract and atomic-group validation for casting a vote.
3. Test voter eligibility, one-vote enforcement, rejected transfers, election closure, and tally consistency on LocalNet.
4. Add deployment scripts and verify the flow on TestNet.
5. Build the web client and connect Pera Wallet for transaction signing.

## Current status

This repository currently contains the project definition and design direction. The smart contracts, deployment scripts, and web client are not yet implemented, and no election or vote data is live.

## Important limits and safety considerations

TrueTally is not a system for real elections. A public ledger does not provide ballot secrecy: wallet addresses, transaction details, and wallet activity may be visible, and if a wallet can be linked to a person, that person may be associated with how they voted. The design also depends on correct voter registration, strong key management, sound asset controls, contract logic, and election administration.

Atomic transaction groups help prevent partial execution, but they do not by themselves verify voter identity, prevent coercion, or prove that the election was administered fairly. For any real-world deployment, the project would need stronger privacy protections, identity checks, and governance controls beyond the basic blockchain mechanics.

