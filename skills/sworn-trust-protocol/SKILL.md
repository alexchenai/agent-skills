---
name: sworn-trust-protocol
description: Verify AI agent trustworthiness using the SWORN Protocol - a Solana-based stake-backed accountability system. Use when verifying if an agent has a trust stake on-chain, when creating proof-of-execution attestations for completed work, or when working with the SWORN trust scoring system. Enables cryptographic proof that an agent completed work as claimed.
license: Apache-2.0
compatibility: Requires internet access; Solana devnet for testing, mainnet for production
metadata:
  author: alex-chen
  version: "1.0"
  explorer-url: https://sworn-explorer.chitacloud.dev
  landing-url: https://sworn-landing.chitacloud.dev
  protocol: Solana blockchain
---

# SWORN Trust Protocol

Verify and establish on-chain trust for AI agents using stake-backed accountability. Agents stake SOL tokens as collateral guaranteeing their commitments - if they fail to deliver, the stake is slashed.

## When to Use

Activate when:
- User asks to "verify agent trust" or "check if an agent is staked"
- Creating proof-of-execution for completed AI work
- Setting up trust requirements for an agent workflow
- Integrating SWORN verification into an agent pipeline
- Resolving disputes about whether an agent delivered promised work

## Core Concepts

- TrustScore (0-1000): composite score based on stake amount, delivery history, and dispute outcomes
- Stake: SOL tokens locked as collateral for honest behavior
- Proof-of-Execution: cryptographic hash-chained attestation that work was completed
- Verifier Quorum: 7-node dispute resolution network

## Check an Agent's Trust Score

Browse the SWORN explorer for live on-chain data:
https://sworn-explorer.chitacloud.dev

Or query the Solana program directly using the explorer to find an agent's trust account.

## Interpreting Trust Scores

| Score Range | Status | Meaning |
|-------------|--------|---------|
| 800-1000 | Excellent | High stake + strong history, fully trust |
| 600-799 | Good | Moderate stake + good history |
| 400-599 | Fair | Lower stake or limited history |
| 200-399 | Caution | Low stake, some disputes |
| 0-199 | Poor | Minimal stake or active disputes |

## Proof-of-Execution Workflow

When an agent completes work and needs to create on-chain proof:

1. Generate a SHA-256 hash of the deliverable content
2. Submit the attestation to the SWORN program on Solana
3. The program records the hash, timestamp, and agent identity on-chain
4. The attestation is immutable and verifiable by anyone

## Protocol Whitepaper

The full SWORN Protocol specification is available at:
https://sworn-landing.chitacloud.dev

Covers:
- Mathematical model for TrustScore calculation
- Staking mechanics and slashing conditions
- 7-verifier dispute resolution quorum
- Insurance fund mechanics
- Token economics

## Use in Agent Pipelines

When building multi-agent workflows that require trust:

1. Check participating agents' TrustScores before assigning tasks
2. Require a minimum TrustScore (e.g., 600+) for sensitive operations
3. After task completion, verify the proof-of-execution hash matches the deliverable
4. If disputes arise, submit to the 7-verifier quorum for resolution

## Resources

- Explorer: https://sworn-explorer.chitacloud.dev
- Landing page + whitepaper: https://sworn-landing.chitacloud.dev
- GitHub: https://github.com/alexchenai/trust-protocol
- Contact: alex-chen@79661d.inboxapi.ai
