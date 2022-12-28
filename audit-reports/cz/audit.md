# Chess Zombies
**Smart contract audit report**

[***$ENRG*** is an investment governance token for the Chess Zombies project](https://shedever-studio.gitbook.io/chess-zombies-wpeng/information/energy-cells-usdenrg#usdenrg-is-an-investment-governance-token-for-the-chess-zombies-project.)

Prepare for:
[Chess Zombies](https://chesszombies.fun)

By: [Roman Inozemtsev](https://github.com/inozemtsev-roman)
12/29/2022

|Audited Files |SHA256 |
|---|---|
|__jetton-minter.fc__ | 2fc54e873deb47f067973497f6467b5dcf12b59a226ce464bf2f975435b7cec5|
|__jetton-utils.fc__ |3e92b2788eabecf7ad82fa8bca0fc63c66f3d0f2195932f0bf5f2e66ea538b13 |
|__jetton-wallet.fc__ |ee9f2e6a4456a161578aa93498deea821f2715814052a08997d28050be13b909 |
|__msg.fc__ |2a9e449aa1f9dd26570b1b7628361dc8e37a6c864176fb6bc8e325060528a0d1 |
|__op-codes.fc__ |5401cb124e112ebf04e03dc67c98266056331cd6ba1ed91130c5f2e9fe7dfde3 |
|__params.fc__ |74cea061e2af9498477b53cd19180969aa858727152aed772ed6d6633d802d3e |
|__rate-oracle.fc__ |8ebb5abc07a99ed2e3088cd0924362a599fe1aac37072a064b05ffb54d60bc67 |
|__send-modes.fc__ |ef1ad3e0e65bb6f04661fda76d65c3e9c17520f2fb5822339d14cf5bc6ed46bb |
|__stdlib.fc__ |eef66332256805555bceb1d76b4550a454d088c834467fe4f7314365f1f95e06 |

## Audit Timeline
✅ Requested on 12/27/2022

✅ Revisioned on 12/29/2022

## Findings Performance
⌛ No Critical Findings (Logic)

## Contents

[Disclaimer](#1-disclaimer)

[Introduction](#2-introduction)

[Contracts overview](#3-contracts-overview)

[Found issues](#4-found-issues)

[Conclusion](#5-conclusion)

[References](#6-references)

[Appendix. Issues' severity classification](#7-appendix-issues-severity-classification)

[Appendix B. List of examines issue types](#8-appendix-b-list-of-examines-issue-types)

[Results](#results)

# 1. Disclaimer
Note that this audit does not give any warranties on finding all possible security issues of the given smart contract(s), i.e., the evaluation result does not guarantee the nonexistence of any further findings of security issues. As one audit-based assessment cannot be considered comprehensive, we always recommend proceeding with several independent audits and a public bug bounty program to ensure the security of smart contract(s). Last but not least, this security audit should not be used as investment advice.

## Common Weakness Enumeration (CWE) Classifications Used in This Audit

|Category| Summary|
|---|---|
|Configuration |Weaknesses in this category are typically introduced during the configuration of the software |
|Data Processing Issues |Weaknesses in this category are typically found in functionality that processes data. |
|Numeric Errors |Weaknesses in this category are related to improper calculation or conversion of numbers. |
|Security Features  |Weaknesses in this category are concerned with topics like authentication, access control, confidentiality, cryptography, and privilege management. (Software security is not security software.) |
|Time and State |Weaknesses in this category are related to the improper management of time and state in an environment that supports simultaneous or near-simultaneous computation by multiple systems, processes, or threads. |
|Error Conditions, Return Values, Status Codes |Weaknesses in this category include weaknesses that occur if a function does not generate the correct return/status code, or if the application does not handle all possible return/status codes that could be generated by a function. |
|Resource Management |Weaknesses in this category are related to improper management of system resources. |
|Behavioral Issues  |Weaknesses in this category are related to unexpected behaviors from code that an application uses. |
|Business Logic |Weaknesses in this category identify some of the underlying problems that commonly allow attackers to manipulate the business logic of an application. Errors in business logic can be devastating to an entire application. |
|Initialization and Cleanup |Weaknesses in this category occur in behaviors that are used for initialization and breakdown. |
|Arguments and Parameters |Weaknesses in this category are related to improper use of arguments or parameters within function calls. |
|Expression Issues |Weaknesses in this category are related to incorrectly written expressions within code. |
|Coding Practices |Weaknesses in this category are related to coding practices that are deemed unsafe and increase the chances that an exploitable vulnerability will be present in the application. They may not directly introduce a vulnerability, but indicate the product has not been carefully developed or maintained. |

# 2. Introduction
The report has been prepares for [Chess Zombies](https://chesszombies.fun)

| | |
|---|---|
|Network | The Open Network | 
|Contract type | [TEP - 64](https://github.com/ton-blockchain/TEPs/blob/master/text/0064-token-data-standard.md) / [TEP - 74](https://github.com/ton-blockchain/TEPs/blob/master/text/0074-jettons-standard.md) / [TEP - 89](https://github.com/ton-blockchain/TEPs/blob/master/text/0089-jetton-wallet-discovery.md) |

## Tokenomics
[Chess Zombies Whitepaper Tokenomics](https://shedever-studio.gitbook.io/chess-zombies-wpeng/information/energy-cells-usdenrg/tokenomics)

| | |
|-|-|
|Type | A token with a limited issue|
|Ticker |***$ENGR*** | 
|Total supply| 100 000 000|
|Decimals | 9 |
|Seed price |$0.25 USD |
|Private sale price |$0.30 USD |
|Strategic sale price |$0.35 USD |
|Public sale price |$0.5 USD |

A flexible tokenomics has been developed for the token, which has the following key advantages for both investors and players: 
1. Fixed total suplay of 100,000,000 ***$ENRG***;
2. Uniform distribution of allocation between ***$ENRG*** holders;
3. Smooth emission unlocking due to the freeze & reveal mechanisms built into the smart contract;
4. Maintain liquidity by integrating ***$ENRG*** into the in-game economy;
5. Deflationary mechanism by burning ***$ENRG*** in exchange for SFT Energy (in-game SFT token);
6. Reduced ***$ENRG*** circulating supply by integrating the token into the Chess Zombies DAO;
7. Correlation of the price of SFT Energy with the price of ***$ENRG*** (the higher the price of ***$ENRG***, the more profitable players will be able to sell SFT Energy on external marketplaces).

## Token allocation
[Chess Zombies Whitepaper Token allocation](https://shedever-studio.gitbook.io/chess-zombies-wpeng/information/energy-cells-usdenrg/token-allocation)

| | |
|--|--|
|4% Seed |$1 000 000 - $0.25 - freeze 3 month - reveal 6.25% = 16 month |
|5% Private sale |$1 500 000 - $0.30 - freeze 2 month - reveal 6.25% = 16 month |
|4% Strategic sale |$1 400 000 - $0.35 - freeze 1 month - reveal 6.25% = 16 month |
|3% Public sale |$1 500 000 - $0.5 - 20% unlocked immediately - reveal 20% = 4 month |
|15% Team |freeze 19 month - reveal 4% = 25 month |
|6% Advisors |freeze 19 month - reveal 4% = 16 month |
|15% Liquiduty |without freeze |
|27% Strategic Reserve |freeze 16 month - reveal 3.85% = 26 month |
|21% Community / Ecosystem | 5% unlocked - reveal 2.5% = 39 month |

## Use of funds
| | |
|--|--|
|Development / Content | 48% |
|Marketing |32% |
|Operations |10% |
|Other |5% |
|Neworking |5% |

## Tha game as a sourth of liquidity for $ENRG

* 1 player to fully level up in Chess Zombies needs to spend (burn) at least 1 200 000 Energy (in-game token). Those, the more players, the more Energy will be burned inside the game.
* The math model of the game maintains a constant overall deficit of Energy in the game at the level of 15%-30%, encouraging players to look for additional sources of Energy<sup>[1](#1)</sup>.
* 2.5% Energy is burned on everytrade in the in-game market.
* Energy can be obtained in several ways: actively trading within the game (slowly), buying Energy in the form of NFTs from other players on external marketplaces (not enough<sup>[2](#2)</sup>), buying Energy within the game with $ENRG (fast and easy).
* **1 $ENRG = 1000 Energy** (fixed rate in the game).
* When exchanging $ENRG for Energy, $ENRG tokens are burned, reducing the total emission.

<a name="1">1</a>: The mathematical model uses the double inflation algorithm, which flexibly regulates the emission of Energy in the game based on the general economic indicators within the game and the active each individual player.

<a name="2">2</a>: Players who actively withdraw Energy from the game are penalized and receive up to 99% less Energy in the game (speculator protection). Thus, the supply of Energy on the foreign market is limited. Energy on the external market can only be sold in the form of SFTs, which makes instant transactions impossible and eliminates the risk of a collapse in the price of Energy due to gambler speculation.


# 3. Contracts overview

The purpose of this audit was to achieve the following:
* Formally check the logic behind given smart contracts.
* Identify potential security issues with smart contracts

> Information in this report should be used for understanding the risk exposure of smart contracts, and tas a guide to improving the security posture of smart contracts by remediating the issues that were identified.

The Jetton is deployed on testnet TON at address:
 
```EQD_ahhMhsy9gDmTT32K1rOS3oZL1E5dBNnzZ_21_mTar64T``` ([testnet.tonscan.org](https://testnet.tonscan.org/address/EQD_ahhMhsy9gDmTT32K1rOS3oZL1E5dBNnzZ_21_mTar64T))

The Oracle is deployed on testnet TON at address:

```EQBZCXERWPRQAihJOxA9DvnyyXj6veqOQI7WW6o6asMCwH8v``` ([testnet.tonscan.org](https://testnet.tonscan.org/address/EQBZCXERWPRQAihJOxA9DvnyyXj6veqOQI7WW6o6asMCwH8v))


### Summary
| | |
|---|---|
|Project name | Chess Zombies |
| Platform | The Open Network |
| Language | FunC |

### Requirements

[Python](https://www.python.org/downloads/)

[Python SDK for TON](https://pypi.org/project/tonsdk/)

[The next generation HTTP client](https://pypi.org/project/httpx/)

[Python logging made (stupidly) simple](https://pypi.org/project/loguru/)

## Contract deployment and operation process 

1. Deploy Oracle contract
    * Generate oracle seed
    * Deploying oracle contract
    * Setting delivery rate
        * Requested new rate
        * Sending new rate to the contract
    * Edit owner (optional)
2. Deploy Root Jetton
    * Generate minter admin mnemonics
    * Input metadata Jetton
    * Deploy minter contract
3. Manage Jetton
    * Set address oracle
    * Change admin
    * Change URI metadata Jetton
    * Mint Jetton
    * Sell Jetton
    * Withdraw (Jetton/TON)

# 4. Found issues

The owner of ```admin_address``` is allowed to:

* ```op::mint``` any amount of jettons to any wallet
* ```op::change_admin``` to any other one
* lock any wallet (prevent funds transferring)
* transfer funds from any wallet to any other one or burn them
* invalidate all the wallets, invalidate total_supply and other data
* rename Jetton, change description or decimals

```c
send_boc(
                wallet.create_transfer_message(
                    minter.address.to_string(1, 1, 1),
                    5 * 10 ** 7,
                    wallet_seqno,
                    payload=begin_cell() \
                    .store_uint(3, 32).store_uint(0, 64) \
                    .store_address(new_admin) \
                    .end_cell()
                )['message'].to_boc(False)
            )
```

### Minter Recommendation
The risk describes the current project design, in most cases, it can’t be completely Resolved.

We advise to carefully manage the privileged account private key to avoid any potential risks of being hacked.

There are some feasible suggestions that would also mitigate the potential risk:

* Assignment of privileged role to the [multi-signature](https://github.com/mir-one/dao-multisig) wallet to prevent a single point of failure
* Removing or limiting some features controlled by admin_address

> ```op::change_admin``` creates a new mnemonic phrase in minter_admin and this operation creates a new minter contract. After such an operation, the project will not be able to manage Jetton

### Oracle recommendation

```c
var msg_body = begin_cell()
        .store_uint(op::get_rate, 32)
        .store_uint(query_id, 64);
        
```
```c
payload.store_ref(
                begin_cell().store_int(-1, 1)
                    .store_uint(price, 32)
                    .store_coins(remain_jettons)
                    .store_uint(freeze_timer, 64)
                    .store_uint(lock_parts, 16)
                    .store_uint(lock_time, 64)
                    .end_cell()
            )
```

To protect against malicious exploitation of Oracle, use the command ```Remaining jettons``` - address of Orbit Bridge Ton USD Coin
[EQC61IQRl0_la95t27xhIpjxZt32vl1QQVF2UgTNuvD18W-4](https://tonscan.org/jetton/EQC61IQRl0_la95t27xhIpjxZt32vl1QQVF2UgTNuvD18W-4)

Use a jetton ```ico_remain_amount``` - EQC61IQRl0_la95t27xhIpjxZt32vl1QQVF2UgTNuvD18W-4
```c
ico_remaining_amount -= jetton_amount;
        store::sell_params = begin_cell()
            .store_int(true, 1)
            .store_uint(jetton_price, 32)
            .store_coins(ico_remaining_amount)
            .store_uint(freeze_timer, 64)
            .store_uint(lock_parts_count, 16)
            .store_uint(lock_time, 64).end_cell();
```


## Potential insecure manage Oracle&Minter hosting
Applications should ideally be hosted with their own dedicated server. If that is not possible, make sure the hosting services are reputable and can be trusted. To enhance the security of an application, it's recommended to restrict the access of the original source from the public internet.

## Verify contracts in TON
Explorers on the TON network display contracts other than the standard ones as unverifiable. The immutability of a smart contract after being published on the blockchain allows participants in the business process to "believe" in its "honesty" - all possible actions, as well as already completed transactions, are visible to anyone, so there is no room for various kinds of data manipulations or business logic. Unfortunately, this quality also poses a threat: if an error (accidental or specially introduced at the development stage) into the logic of a smart contract, it cannot be corrected after the contract is written to the blockchain, and an attacker can use the vulnerability at any time to benefit.

This would reduce the likelihood of malicious code being compiled in the same byte code, but contains misleading comments and variables that do not affect the resulting byte code.

> To verification Jetton, after Deploy in mainnet - sent 1 TON + 1 000 Donation on address: ```fingerprints.ton```