+++
date = 2026-09-15
title = "Navio Mainnet Is Live: Private Proof-of-Stake Is Finally Here"
description = "Navio, the successor to NavCoin, launched its mainnet in the summer of 2026. Here's what shipped, how Proof-of-Private-Stake works, how to move your old NAV over, and how to start staking."
[taxonomies]
tags = ["navio", "navcoin", "staking", "cryptocurrency", "privacy", "blsct", "proof of stake"]
+++

Back in January, I wrote a
[retrospective on my NavCoin staking journey](@/blog/2026-01-26-from-navcoin-to-navio-a-staking-retrospective.md)
and said I was eagerly anticipating the launch of Navio. Well, the wait is over.
**The Navio mainnet is live**, and it has been running since the start of July.

I've been staking NAV since 2018, and over the last few years I've also been
contributing to [navio-core](https://github.com/nav-io/navio-core) itself, with
more than 500 commits to the codebase. So this launch is personal. Let's walk
through what actually shipped.

## The Launch

[Navio Core v0.1.0](https://github.com/nav-io/navio-core/releases/tag/v0.1.0)
was published on June 28, 2026, as the first stable release of Navio Core and
the launch of the Navio mainnet. The genesis block carries a timestamp of **July
1, 2026, 13:00 UTC**.

Under the hood, Navio Core is built on the Bitcoin Core codebase, with BLSCT
(Boneh-Lynn-Shacham Confidential Transactions) added at the base layer. Binaries
were released for Linux (x86_64, ARM, RISC-V and PowerPC), macOS (Intel and
Apple Silicon) and Windows, with signed `SHA256SUMS` so you can verify your
download before running it.

## What Makes Navio Different

In that retrospective I explained that NavCoin only offered private transactions
through its `xNAV` token. Navio flips that around: privacy is the default, not
an add-on.

### Confidential Transactions Everywhere

Every shielded output hides both the amount and the parties involved, using
Pedersen commitments and BLS12-381 range proofs. The chain stays publicly
verifiable (anyone can check that no coins were created out of thin air) without
anyone learning who sent what to whom. Addresses are bech32m stealth addresses
that start with `nav1`.

### Proof-of-Private-Stake (PoPS)

This is the part I've been most excited about. On a normal Proof-of-Stake chain,
everyone can see which address produced a block and how much it had staked. With
PoPS, a staker proves two things with zero-knowledge proofs:

1. A **set-membership proof** showing it controls _one_ of the staked
   commitments, without revealing which one.
2. A **range proof** showing the hidden amount in that commitment is enough to
   win this particular block.

The result is that the validator's identity, the amount staked, and even the
link between two blocks produced by the same staker never appear on-chain. You
help secure the network without putting a target on your wallet.

### Mainnet Parameters

According to the
[Navio consensus documentation](https://docs.nav.io/concepts/consensus/), the
key mainnet numbers are:

| Parameter         | Mainnet value                  |
| ----------------- | ------------------------------ |
| Target block time | 120 seconds                    |
| Block reward      | 8 NAV                          |
| Minimum stake     | 10,000 NAV                     |
| Consensus         | Short PoW bootstrap, then PoPS |
| P2P / RPC ports   | 48470 / 48471                  |
| Address format    | bech32m, `nav1...`             |

## Moving Your Old NAV to Navio

If you're still holding legacy NavCoin, the migration goes through the official
bridge at [bridge.nav.io](https://bridge.nav.io). It's a two-step process:

1. **NAV to wNAV:** Connect a BNB Smart Chain wallet on the bridge, register
   once, and send your legacy NAV to the deposit address the bridge gives you.
   The equivalent amount of wrapped NAV (wNAV) is minted to your BSC wallet,
   usually within a few minutes.
2. **wNAV to native NAV:** On the bridge's Withdraw page, enter a Navio address
   (starting with `nav1`). The bridge burns your wNAV and sends native NAV to
   that address on the new chain.

**Be careful here.** The bridge only accepts mainnet `nav1...` addresses. Old
NavCoin (`N...`) addresses and testnet (`tnv1...`) addresses are rejected, and
the official guide warns that burning with a wrongly formatted address destroys
the wNAV with no refund. **Send a small test amount first**, and follow the
[official coin swap guide](https://docs.nav.io/guides/coin-swap/) step by step
rather than a summary like this one.

## Staking on Navio

Staking works a little differently from the old `navcoind` setup I described
[back in 2018](@/blog/2018-03-27-wanna-start-staking-navcoin.md). Instead of the
wallet staking on its own, you lock coins into a stake and run a separate staker
process.

First, download Navio Core from the
[releases page](https://github.com/nav-io/navio-core/releases), start `naviod`,
and let it sync. Then create a wallet (BLSCT is the default wallet type) and
grab a `nav1` address to receive your coins:

```bash
navio-cli createwallet "staking"
navio-cli -rpcwallet=staking getnewaddress "Staking" "blsct"
```

Once your NAV has arrived, lock at least the 10,000 NAV minimum into a stake:

```bash
navio-cli -rpcwallet=staking stakelock 10000
```

Finally, run the staker against your wallet. It connects to your node over RPC,
builds the Proof-of-Private-Stake proofs, and submits blocks when you win:

```bash
navio-staker -wallet=staking
```

When you want your coins back, `stakeunlock` releases them from the stake into
your regular spendable balance.

### Cold Staking

If you'd rather not keep your spending keys on an always-online server, Navio
Core v0.1.7 added **delegated cold staking**. You hand an operator the ability
to produce blocks with your stake, while only your offline key can spend or
unstake the coins, and you can revoke the delegation at any time with
`stakeunlock`. The details are in the
[cold staking documentation](https://github.com/nav-io/navio-core/blob/master/doc/cold-staking.md).

## Life After Launch

A mainnet launch is the start of the work, not the end. The releases have kept
coming at a fast pace, up to
[v0.2.1](https://github.com/nav-io/navio-core/releases/tag/v0.2.1) at the time
of writing. The biggest one so far is
[v0.2.0](https://github.com/nav-io/navio-core/releases/tag/v0.2.0), which:

- Moved the BLSCT cryptography from the herumi/mcl library to
  supranational/blst, while staying byte-compatible with the existing chain.
- Brought in a hardened "v2" proof transcript that activates at **mainnet height
  42,500**, so every node needs to be on v0.2.0 or later.
- Introduced an encrypted peer-to-peer messaging layer, with aggregated sends
  that hide which outputs belong to the sender, and atomic swaps between tokens
  and NAV.
- Fixed a block production stall that hit mainnet on September 5, 2026.

That last point is worth being honest about: a brand-new chain running brand-new
cryptography will have rough edges, and it did. What matters to me is that it
was diagnosed and fixed in the open within days. If you run a node, **keep it up
to date**.

## Final Thoughts

When I first set up a NavCoin staking box on an Ubuntu 16.04 server in 2018, a
fully private Proof-of-Stake chain felt like a far-off research idea. Now it's
running, and I get to help build it.

If you want to dig deeper, start with the
[Navio documentation](https://docs.nav.io/) and the
[navio-core repository](https://github.com/nav-io/navio-core). And if you're
still sitting on legacy NAV, now is a good time to make the move.
