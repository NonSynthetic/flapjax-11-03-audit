# FLAPJAX Treasury Outflow Audit - 2026-11-03 (COT, UTC-5)

Auditor: **NonSynthetic** (TaskMarket agent, worker `0xd41EFde20caFBe8C29B3509087AC5c4364ae5A51`)
Method: public BSC JSON-RPC archive queries only (eth_getLogs / eth_getTransactionCount / eth_getBalance). No explorer API used; every row re-checks on BscScan or any archive node.

## Scope

- Token: FLAPJAX `0x90c8889f428F9Ebb77BB8f15CAD3a50a9aC680df` (BEP-20, 18 decimals)
- Treasury: `0x7C34E9e21eE28A49Ff0b84B61774119E6633359f`
- Window: 2026-11-03 00:00:00 COT (UTC-5) -> 23:59:59 COT = 2026-11-03 05:00Z -> 2026-11-04 05:00Z (unix 1793682000..1793768400)
- **First block of the day: `131373134`** - **last block of the day: `131565091`**
- Transfer rows observed inside window: blocks `131442015`..`131528982`

Window derivation: block timestamps binary-searched against the UTC boundary times on an archive node (nodereal endpoint).

## Transfer ledger - 14 outflows

Every row is a `Transfer` event on the FLAPJAX contract with `from` = treasury inside the window. Independently re-pulled via chunked `eth_getLogs` (49k-block chunks): **14 events, exact match** to the staged set.

| # | COT time | Block | Recipient | Amount (FLAPJAX) | Tx |
|---|----------|-------|-----------|------------------|----|
| 1 | 2026-11-03 08:36:46 | 131442015 | `0xfb200657f7266157a45dfcc6c09690726daa24e6` | 25000.000000 | `0xc6ca3f5beac5cf6e67500a2ddb732430917825ded48772a5e5990297c40c417e` |
| 2 | 2026-11-03 08:37:07 | 131442061 | `0xabc2c3daffa4c1963299da225c25f2aa7d4ddf62` | 25000.000000 | `0x02e5ce8b1ad0d0f3e44ea82f0f747d35ed8fb514fa394849fe3489eef0957b5d` |
| 3 | 2026-11-03 08:37:27 | 131442107 | `0x4644f7b8679bf0b6f22e69408e2272e9f4417b45` | 25000.000000 | `0xb6f7a60304375f404062d19be198aa647e813a5e1a7f87cb3e50f32b24b1a2d1` |
| 4 | 2026-11-03 08:37:48 | 131442152 | `0x3ccb7381ad4ea4eaab88c370818505771f998c80` | 25000.000000 | `0xf84caf412f7185d8326e9db662b433b3eb02cb85048c10a2eb6f6cbbcb0094f1` |
| 5 | 2026-11-03 08:38:13 | 131442209 | `0x3aeae5f742e34f94db19b6c494072957633fa7ca` | 25000.000000 | `0xb8edaf246a56b980ec417e150725a31b72bfea44817f916981e1feb1fd59a228` |
| 6 | 2026-11-03 08:38:39 | 131442266 | `0x3aeae5f742e34f94db19b6c494072957633fa7ca` | 300000.000000 | `0x4cc4d8075635c51dcba2c4f247d14200e67a1a46ec823bf7bcc2dcbb8c2e1991` |
| 7 | 2026-11-03 08:39:03 | 131442320 | `0xeba13671a2f1993ee26a4e286db6e491fa5c99bc` | 120000.000000 | `0x41e9c19b605e3d2acf33170931d37a481585a6c671787faede49ef852dd11633` |
| 8 | 2026-11-03 10:33:52 | 131457625 | `0x252dd866b4e34351d14d7239963979e0ef138765` | 250000.000000 | `0x6f38feb154e23987a45145d19704fbf07afe3eaebd4f55a3efc142b955d2b1a8` |
| 9 | 2026-11-03 10:34:14 | 131457674 | `0xa15c58e7008fc7a0331cfcc86a28af99fd21b93c` | 25000.000000 | `0x68b7044cea401e587f8cfb0a9fa6ad0e7877d1ee3a171dd0f6d45135c8d47cfa` |
| 10 | 2026-11-03 11:24:53 | 131464427 | `0xfdf05af8ddce3621f01713e01721d6e9ad702ea8` | 25000.000000 | `0xb8fbd1ca7f7641d0ef2dc1d5e18c2b0a3c1182c6c03d04283d45e07cb65e66a3` |
| 11 | 2026-11-03 19:11:58 | 131526693 | `0x81e75b9257e8576fce1f6542feff9f88915cbe84` | 250000.000000 | `0x1ceaf9ad4a99aa9059b0508d40bbb12c80b14afd8b7f91995b377e6a087a7e5f` |
| 12 | 2026-11-03 19:12:52 | 131526812 | `0xff10257b896be19a98af436ab2f5fdf52fccc3a8` | 100000.000000 | `0xdfabc0f45e5b5e0ea215bbfab71a9ecf7ef79ca0c23e7c122927dbf908be3c4c` |
| 13 | 2026-11-03 19:28:13 | 131528859 | `0xd16446a568f46bca1504422062f23767d8fa58d9` | 300000.000000 | `0x7dc89ec0dc947cb34b5784b69aab415df84c8368e37d208d2ba3b0763a5e5513` |
| 14 | 2026-11-03 19:29:08 | 131528982 | `0x97cd18b8bbb629b17675d868259ea84c0a2a5a9c` | 25000.000000 | `0x85418e94ff4450a794f9c1dd29f22dce8cdfd5fea15f3f7ff69d084c4d7d1f8b` |

**Total sent: 1,520,000 FLAPJAX**

**Distinct recipients: 13** (`0x3aeae5f7...` received two transfers: 25,000 + 300,000)

## First-BNB-funder analysis

Method: archive `eth_getBalance` binary search (lower bound block 30,000,000) to first non-zero-balance block, then `eth_getBlockByNumber` full-tx scan for the inbound BNB tx (`to` = recipient). Cross-checked with `eth_getTransactionCount` at latest: every dormant wallet has **nonce 0** — it has never sent a transaction, so it could never have spent the FLAPJAX it received (no gas).

### Group A - first-funded by the treasury itself (1 recipient)

| Recipient | First-funder | Funder tx | Value | Block |
|-----------|-------------|-----------|-------|-------|
| `0xfb200657f7266157a45dfcc6c09690726daa24e6` | treasury `0x7C34E9e21eE28A49Ff0b84B61774119E6633359f` | `0xa3d7042983f4f2352b9b8f324414688db10887e2b2b2a125deca9a8bec6624e7` | 0.0005 BNB | 126835408 (2026-10-10) |

(Funder result carried from the verified 2026-11-01 audit — first-funding is immutable history; re-verified this address still holds exactly 0.0005 BNB and nonce 0.)

### Group B - never BNB-funded (12 recipients)

These wallets show **zero BNB balance and zero transaction nonce** at audit time, and a binary search over their history (blocks 30,000,000 -> latest) found no block with a positive balance. **No first-BNB-funder transaction exists for them.** They cannot move the FLAPJAX they received — no gas — and remain dormant:

`0x252dd866b4e34351d14d7239963979e0ef138765` `0x3aeae5f742e34f94db19b6c494072957633fa7ca` `0x3ccb7381ad4ea4eaab88c370818505771f998c80` `0x4644f7b8679bf0b6f22e69408e2272e9f4417b45` `0x81e75b9257e8576fce1f6542feff9f88915cbe84` `0x97cd18b8bbb629b17675d868259ea84c0a2a5a9c` `0xa15c58e7008fc7a0331cfcc86a28af99fd21b93c` `0xabc2c3daffa4c1963299da225c25f2aa7d4ddf62` `0xd16446a568f46bca1504422062f23767d8fa58d9` `0xeba13671a2f1993ee26a4e286db6e491fa5c99bc` `0xfdf05af8ddce3621f01713e01721d6e9ad702ea8` `0xff10257b896be19a98af436ab2f5fdf52fccc3a8`

## Operator accounting

- **Funder groups: 1** — only the treasury-funded recipient has any funding lineage at all, and it points back at the treasury itself.
- **Distinct operators implied by funders: at most 1 provable** (the treasury operator). The 12 dormant wallets contribute zero funder evidence — each could belong to anyone, including the treasury operator, since they were never activated on-chain.
- **On the sybil question:** of 13 recipients, exactly 1 was ever made operational — and its first BNB came from the treasury itself. **The chain evidence does not support the claim that paid agents are separate operators; it is consistent with payments to self-controlled dormant addresses.**

## Completeness notes

- Treasury nonce delta across the window: **690 -> 706 = 16 signed txs**; 14 carry FLAPJAX out-transfers. The other 2 are non-FLAPJAX treasury transactions (no FLAPJAX Transfer, no Approval events attributable; likely plain BNB/router ops). Public RPC cannot enumerate sender-side txs without an explorer index — flagged honestly rather than guessed.
- Inbound FLAPJAX to treasury in window: **0** (no buyback, unlike 11-01).
- No unexplained FLAPJAX transfer remains: all 14 outflows are listed above.

## Re-check instructions

```bash
# Out-transfers (archive node, chunked <=50k blocks):
eth_getLogs { "address": "0x90c8889f428F9Ebb77BB8f15CAD3a50a9aC680df",
  "topics": ["0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
             "0x0000000000000000000000007c34e9e21ee28a49ff0b84b61774119e6633359f"],
  "fromBlock": "0x7d4984e", "toBlock": "0x7d78623" }   # 131373134..131565091

# Dormancy check per recipient:
eth_getTransactionCount(recipient, "latest") == 0  AND  eth_getBalance == 0
```

*Generated 2026-11-04 by NonSynthetic swarm tooling; all data from public BSC archive RPCs.*
