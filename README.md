# TrueTally

TrueTally is a proposed campus voting dApp built around Algorand Standard Assets (ASAs). The project will explore whether a blockchain-based workflow can make vote submission and tally updates easier to verify after a poll.

## How it is intended to work

An election administrator registers an election, its candidates, and the eligible voters. Each eligible voter receives one election-specific voting asset. A voter submits a ballot by transferring that asset to the wallet assigned to their chosen candidate.

The vote transaction is intended to be an Algorand atomic group containing both the asset transfer and an application call. The smart contract will validate the election state and voter eligibility, then update the on-chain tally. If any transaction in the group fails validation, the group fails as a whole, so the asset transfer and tally update cannot succeed separately.

The ASA's transfer controls still need careful design. Algorand assets are not inherently non-transferable. The prototype will need to restrict or mediate transfers, for example through the asset's freeze and clawback controls and contract checks, so a voting asset cannot be reused or moved outside the voting flow.

## Planned stack

- Algorand smart contracts written in Python with AlgoKit and the Algorand Python SDK.
- LocalNet for development and automated tests; TestNet for a public test deployment.
- A lightweight web client using the Algorand JavaScript SDK.
- Pera Wallet connection through WalletConnect for wallet authentication and transaction signing.

LocalNet is intended for fee-free development. TestNet transactions use test ALGO and are not mainnet transactions.

## Planned milestones

1. Specify election, candidate, and voter state, including asset transfer restrictions and tally rules.
2. Implement the contract and atomic-group validation for casting a vote.
3. Test voter eligibility, one-vote enforcement, rejected transfers, election closure, and tally consistency on LocalNet.
4. Add deployment scripts and test the flow on TestNet.
5. Build the web client and connect Pera Wallet for transaction signing.

## Current status

This repository currently contains the project definition. The smart contract, deployment scripts, and web client have not been implemented. No election has been created and no votes have been cast.

## Limits and safety

TrueTally is not a system for real elections. A public ledger does not provide ballot secrecy: transaction details and wallet activity may be visible, and linking a wallet to a person can reveal how they voted. The design also depends on correct voter registration, asset controls, contract logic, and election administration. Atomic groups prevent partial execution; they do not by themselves establish voter identity, prevent coercion, or prove an election was administered fairly.

