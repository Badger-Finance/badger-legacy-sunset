# Etherscan Guide

## Table of Contents
- [Overview](#overview)
- [Ebtc Positions](#ebtc-positions)
    - [Contract Addresses](#contract-addresses)
    - [Steps to Close a CDP Position](#steps-to-close-a-cdp-position)
- [Legacy Vault Positions](#legacy-vault-positions)
    - [Staking Contract Addresses](#staking-contract-addresses)
    - [Steps to Unstake](#steps-to-unstake)
    - [Vault Contract Addresses](#vault-contracts-addresses)
    - [Steps to Withdraw](#steps-to-withdraw)
- [BadgerTree](#badgertree)
    - [BadgerTree Merkle Proofs](#badgertree-merkle-proofs)
    - [Steps to Claim Rewards](#steps-to-claim-rewards)

## Overview
This guide demonstrates how to manually withdraw eBTC and legacy vault positions through Etherscan.

## Ebtc Positions

### Contract Addresses

| Contract             | Address                                    |
| -----------          | ------------------------------------------ |
| sorted_cdps          | 0x591AcB5AE192c147948c12651a0a5f24f0529BE3 |
| cdp_manager          | 0xc4cbaE499bb4Ca41E78f52F07f5d98c375711774 |
| ebtc_token           | 0x661c70333AA1850CcDBAe82776Bb436A0fCfeEfB |
| borrower_operations  | 0xd366e016Ae0677CdCE93472e603b75051E022AD0 |

### Steps to Close a CDP Position

1. To get a list of your CDP IDs, go to [sorted_cdps](https://etherscan.io/address/0x591AcB5AE192c147948c12651a0a5f24f0529BE3#readContract) and scroll down to `getCdpsOff` (#13), paste your address here and hit `Query`. You’ll get all your CDPs listed, copy your ID.
2. To figure out how much you owe, go to [cdp_manager](https://etherscan.io/address/0xc4cbae499bb4ca41e78f52f07f5d98c375711774#readContract) and scroll down to `GetCdpDebt` (#40), paste your **CDP ID** (from step 1) here and hit `Query`, this is how much eBTC you owe.
3. To check if you have enough eBTC to close your position, go to [ebtc_token](https://etherscan.io/address/0x661c70333AA1850CcDBAe82776Bb436A0fCfeEfB#readContract) and scroll down to `balanceOf` (#5), paste your address here and hit `Query`. **Make sure this number is greater than the amount of eBTC you owe (obtained from step 2)!**
4. Buy more eBTC if needed (optional)
5. Go to [borrower_operations](https://etherscan.io/address/0xd366e016Ae0677CdCE93472e603b75051E022AD0#writeContract) and and use the `connect to web3` button to connect your wallet. Scroll down to `closeCDP` (#5) and paste your **CDP ID** here (from step 3). Then, connect your wallet and hit `Write`. This will close your CDP position and withdraw all availble stETH. **If you have multiple positions, make sure you repeat the step for all of your CDP positions!**

## Legacy Vault Positions

### Staking Contract Addresses

| Contract             | Address                                    |
| -------------        | ------------------------------------------ |
| native.badger        | 0xa9429271a28F8543eFFfa136994c0839E7d7bF77 |
| native.renCrv        | 0x2296f174374508278DC12b806A7f27c87D53Ca15 |
| native.sbtcCrv       | 0x10fC82867013fCe1bD624FafC719Bb92Df3172FC |
| native.tbtcCrv       | 0x085A9340ff7692Ab6703F17aB5FfC917B580a6FD |
| native.uniBadgerWbtc | 0xA207D69Ea6Fb967E54baA8639c408c31767Ba62D |
| sushi.slpEthWbtc     | 0x612f681BCd12A0b284518D42D2DBcC73B146eb65 | 
| harvest.renCrv       | 0x612f681BCd12A0b284518D42D2DBcC73B146eb65 |


### Steps to Unstake:

1. Navigate to one of the staking contracts (i.e [native.badger](https://etherscan.io/address/0xa9429271a28F8543eFFfa136994c0839E7d7bF77#code))
2. On the `Read Contract as Proxy` page, you'll find a function called `totalStakedFor` (#15). Type in your address here and hit `Query` to see the total shares you have staked.
3. Go to the `Write Contract as Proxy` page and use the `connect to web3` button to connect your wallet
4. Find the `unstake` (#10) function and type in an amount to unstake (shares, in Wei, obtained from step 2). In the "data" field put "0x", which means empty data. 
5. Click the `Write` button to unstake

**Please check your wallet against all staking contracts just to make sure!**

### Vault Contracts​ Addresses

| Contract         | Address                                    |
| -------------    | ------------------------------------------ |
| BADGER           | 0x19D97D8fA813EE2f51aD4B4e04EA08bAf4DFfC28 |
| WBTC             | 0x4b92d19c11435614CD49Af1b589001b7c08cD4D5 |
| crvRenWBTC       | 0x6dEf55d2e18486B9dDfaA075bc4e4EE0B28c1545 |
| crvRenWSBTC      | 0xd04c48A53c111300aD41190D63681ed3dAd998eC |
| tbtc/sbtcCrv     | 0xb9D076fDe463dbc9f915E5392F807315Bf940334 |
| DIGG             | 0x7e7E112A68d8D2E221E11047a72fFC1065c38e1a |
| wBTC/Digg SLP    | 0x88128580ACdD9c04Ce47AFcE196875747bF2A9f6 |
| wBTC/Badger SLP  | 0x1862A18181346EBd9EdAf800804f89190DeF24a5 |
| wBTC/wETH SLP    | 0x758A43EE2BFf8230eeb784879CdcFF4828F2544D |

### Steps to Withdraw

1. Navigate to one of the vault contracts (i.e [BADGER](https://etherscan.io/address/0x19D97D8fA813EE2f51aD4B4e04EA08bAf4DFfC28#code))
2. Go to the `Write Contract as Proxy` page and use the `connect to web3` to connect your wallet
3. Find the `withdrawAll` (#22) function, and click the `Write` button 
4. Wait for the transaction to get confirmed and the funds will be in your wallet

**Please check your wallet against all underlying vault contracts just to make sure!**

## BadgerTree

### BadgerTree Merkle Proofs

[Ehereum Mainnet](https://raw.githubusercontent.com/Badger-Finance/badger-legacy-sunset/refs/heads/main/merkle/badger-tree-1.json)

### Steps to Claim Rewards

1. Locate your wallet address in the JSON file gather the following information (for address `0x1F80673CBa95A1792dD6D75a6F6CCFD14ee6b4A1`)
```
"index": "0x8e0",
"user": "0x1F80673CBa95A1792dD6D75a6F6CCFD14ee6b4A1",
"cycle": "0x3403",
"tokens": [
    "0x3472A5A71965499acd81997a54BBA8D852C6E53d",
    "0x798D1bE841a82a273720CE31c822C61a67a601C3"
],
"cumulativeAmounts": [
    "5610960483197843874",
    "13104213354006383672107147760000000000000000000000000000000000000000000"
],
"proof": [
    "0x91e08f2efad14911d473c692582f66c51ce4d44c744f2b3f4ab34904f08d45ec",
    "0xe0777e80678db6e3b1b9af58a7462a7815cae98f34106303f3faaadeb232ce73",
    "0x7253f9bdf0d996ba17cc26a38f2ad8ecc6d042f8b8220a9c6b8c9c752f38b18d",
    "0x92e7e668c4d1f6b11c176fbcd3b063c98ee94e6400629de44c236bc288a484be",
    "0xb5f9e13c1382e97332489d96a9104e9f64e08f90136c8a104791c036d28d4a92",
    "0x5457574880958617e4d369eb0222bb67ba1ce080959c67170fb05a35c489e311",
    "0x3d7032f7c2215f8b6fa586e0514c2d8aa8bd990f28e42e39633484ef975d8df4",
    "0xf5f17e3e51bdb7fd13daf2420637d452153041566881ba9e0eaf13787f2b079d",
    "0xd23e10bdd1ce2243e3f35cc19a65963e05866830a7098a7c851e62ff3af65831",
    "0x34210f8a98759f6cd11bb939ee1373e37978b1b2dda649daada66334d16539e7",
    "0xa565167724235378e738fb65c1ea179efc291158f4e5d1cb9f3463bbedb270d1",
    "0x529731f556e574dae2cc2eb1fad265dbd5a95489bf21ce995e6ca0fcece4aa53",
    "0x7e03b05141808fb49e4b8e65f871343b1c5e7b6c64089ef89265e2ea33f2fa35",
    "0xb943edfe8ccba01a2ad9a71d54fcdb9f1a235c439eb187086e482e9cded1f8e5",
    "0xbdb1134d5500d315aacaa835f688c19e64878a591a5442cb695c0b217023f89f"
],
```

2. Navigate to [BadgerTree](https://etherscan.io/address/0x660802fc641b154aba66a62137e71f331b6d787a#code)
3. On the `Read Contract as Proxy` page, you'll find a function called `getClaimableFor` (#9). Use `user`, `tokens` and `cumulativeAmounts` from Step 1 for the parameters respectively. For array parameters such as `tokens` and `cumulativeAmounts`, use `[0x3472A5A71965499acd81997a54BBA8D852C6E53d,0x798D1bE841a82a273720CE31c822C61a67a601C3]` and `[5610960483197843874,13104213354006383672107147760000000000000000000000000000000000000000000]` respectively without quotes (using the example above, your wallet may have different values). Then, hit `Query` and you will get a response that looks something like this
```
[ getClaimableFor(address,address[],uint256[]) method Response ]
    address[] :  
[[0x3472A5A71965499acd81997a54BBA8D852C6E53d]
[0x798D1bE841a82a273720CE31c822C61a67a601C3]]

These are the `amountsToClaim` for Step 5 ---->  uint256[] :  2883998427461650,24612823809009175509330238518021935148251136709439368600216462363612
```
4. Go to the `Write Contract as Proxy` page and use the `connect to web3` to connect your wallet
5. Find the `claim` (#2) function and filling in the information obtained from step 1 and 3
Use a [hex to decimal converter](https://www.rapidtables.com/convert/number/hex-to-decimal.html) to convert `index` and `cycle` to decimal values.

"index": "0x8e0" => 2272
"cycle": "0x3403" => 13315

```
`tokens`: [0x3472A5A71965499acd81997a54BBA8D852C6E53d,0x798D1bE841a82a273720CE31c822C61a67a601C3]
`cumulativeAmounts: [5610960483197843874,13104213354006383672107147760000000000000000000000000000000000000000000]
`index`: 2272
`cycle`: 13315
`merkleProof`: [0x91e08f2efad14911d473c692582f66c51ce4d44c744f2b3f4ab34904f08d45ec,0xe0777e80678db6e3b1b9af58a7462a7815cae98f34106303f3faaadeb232ce73,0x7253f9bdf0d996ba17cc26a38f2ad8ecc6d042f8b8220a9c6b8c9c752f38b18d,0x92e7e668c4d1f6b11c176fbcd3b063c98ee94e6400629de44c236bc288a484be,0xb5f9e13c1382e97332489d96a9104e9f64e08f90136c8a104791c036d28d4a92,0x5457574880958617e4d369eb0222bb67ba1ce080959c67170fb05a35c489e311,0x3d7032f7c2215f8b6fa586e0514c2d8aa8bd990f28e42e39633484ef975d8df4,0xf5f17e3e51bdb7fd13daf2420637d452153041566881ba9e0eaf13787f2b079d,0xd23e10bdd1ce2243e3f35cc19a65963e05866830a7098a7c851e62ff3af65831,0x34210f8a98759f6cd11bb939ee1373e37978b1b2dda649daada66334d16539e7,0xa565167724235378e738fb65c1ea179efc291158f4e5d1cb9f3463bbedb270d1,0x529731f556e574dae2cc2eb1fad265dbd5a95489bf21ce995e6ca0fcece4aa53,0x7e03b05141808fb49e4b8e65f871343b1c5e7b6c64089ef89265e2ea33f2fa35,0xb943edfe8ccba01a2ad9a71d54fcdb9f1a235c439eb187086e482e9cded1f8e5,0xbdb1134d5500d315aacaa835f688c19e64878a591a5442cb695c0b217023f89f]
`amountsToClaim`: [2883998427461650,24612823809009175509330238518021935148251136709439368600216462363612]
```
Again, these are example values, use your actual values obtained from step 1 and 3.

6. Click the `Write` button to claim