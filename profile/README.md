# Mvua Protocol

Parametric climate insurance on Stellar. When on chain weather data says the season failed, the payout is already on its way.

## What Mvua is

Mvua Protocol is parametric, index based climate insurance for smallholder farmers, built on the Stellar network with Soroban smart contracts. A farmer buys a small policy in USDC at the start of a season. The protocol watches an on chain rainfall index for that region. If the season fails by the rule written into the policy, the payout is released automatically, with no claim to file and no adjuster to convince.

"Mvua" means "rain" in Swahili. Traditional crop insurance was never built for a farmer with a two hectare plot: premiums are out of reach, adjusters cannot reach every field and a claim can take months to settle. Parametric insurance removes the assessment and pays on a number anyone can check, so relief arrives in time to matter.

## How it works

1. Buy cover. A farmer or a cooperative pays a premium in USDC into a regional risk pool. The policy records the rainfall index, the payout trigger and the payout amount before the season begins.
2. Watch the season. Independent publishers submit signed rainfall readings to the oracle. The adapter keeps a median across more than one publisher, so no single reading decides anything.
3. Get paid. At the end of the season the trigger engine reads the index. If it crossed the trigger, the payout vault releases funds to every affected policy automatically.

## The on chain core

Five Soroban contracts, each with one job, so a fault in one part cannot quietly corrupt another.

- `risk-pool` holds the capital.
- `policy` records the terms.
- `oracle-adapter` brings in the weather.
- `trigger-engine` decides the season.
- `payout-vault` releases the money.

Every decision the protocol makes is a function of public inputs: the signed rainfall readings, the index definition and the policy terms. The same inputs produce the same outcome for everyone, so the rules can be read rather than trusted.

## Repositories

- [mvua-contract](https://github.com/Mvua-Protocol/mvua-contract): the on chain core, five Soroban contracts in Rust. This is where funds are held and payouts are decided.
- [mvua-app](https://github.com/Mvua-Protocol/mvua-app): the web interface, built with Next.js. It reads state and submits transactions and never holds funds.
- [mvua-publisher](https://github.com/Mvua-Protocol/mvua-publisher): the off chain oracle publisher in Node and TypeScript. It turns public rainfall archives into signed observations the oracle verifies on chain.
- [mvua-site](https://github.com/Mvua-Protocol/mvua-site): the public showcase and documentation site.

## Project status

Pre alpha, live on Stellar testnet. The contract core is written, tested and released; a first full season is running against real wall clock time. Mainnet is gated behind an external security audit and a full beta season operated like production. An insurance product that pays the wrong amount is worse than one that does not exist yet, so the launch is earned one step at a time.

## Documentation

The protocol reference, the index science with a worked example and the trust model are documented at [mvua.site](https://mvua.site).

---

Nothing here is an offer or a solicitation and nothing here is financial advice. Mvua Protocol operates in USDC on Stellar and has no protocol token.
