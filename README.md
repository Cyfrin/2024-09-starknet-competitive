# Starknet Staking 

### Prize Pool

- Total Pool - $65,000
- H/M -  $60,000
- Low - $5,000

- Starts: September 16, 2024 Noon UTC
- Ends: October 04, 2024 Noon UTC

- nSLOC: 2937

[//]: # (contest-details-open)

## About the Project

This project holds the implementation of Staknet staking mechanism.
Following Starknet [SNIP 18](https://community.starknet.io/t/snip-18-staking-s-first-stage-on-starknet/114334)

[Overview drawing](https://drive.google.com/file/d/1ZoAqRSu5Hlgc7xh10eVnSDWkEu49sQRj/view) 


- [Documentation](https://github.com/starkware-libs/starknet-staking/tree/main/docs)
- [Twitter](https://twitter.com/Starknet?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor)
- [GitHub](https://github.com/starkware-libs/starknet-staking)



## Actors


```
Staker: Staker can stake any amount of STRK greater than 20K. In return, they receive rewards. In addition, the Staker can choose if he wants to participate in pooling.
Stake Delegator (AKA delegation pool member): Delegators choose a Staker to whom they delegate their Stake, sharing rewards with said Staker.
Security Admin: Un-pause the activity of the contracts, whether on false positive alerts or after a bug was fixed. Also, can replace the security agent.
Security Agent: Can pause the staking contract in case of a bug.
Operator: The only role that can call state-changing functions of the staking core contract.

L1 Mint Manager:
AllowanceGovernor: Can allow mint manager to mint STRK for an address
StopGovernor: Can set the allowance of an account to 0

```

[//]: # (contest-details-close)

[//]: # (scope-open)

## Scope (contracts)


Contracts in `workspace/apps/staking/contracts/src` that are in scope:

```js
src/
├── constants.cairo
├── errors.cairo
├── lib.cairo
├── minting_curve.cairo
├── pooling.cairo
├── reward_supplier.cairo 
├── staking.cairo
├── utils.cairo
├── minting_cruve
│   ├── interface.cairo
│   └── minting_curve.cairo
├── pooling
│   ├── interface.cairo
│   └── pooling.cairo
├── reward_supplier
│   ├── interface.cairo
│   └── reward_supplier.cairo
├── staking
│   ├── interface.cairo
│   └── staking.cairo

```


Contracts in `workspace/packages/contracts/src` that are in scope:

```js
src/
├── components.cairo
├── errors.cairo
├── lib.cairo
├── components
│   ├── replaceability.cairo
│   ├── roles.cairo
│   ├── replaceability
     │   ├── interface.cairo
     │   └── replaceability.cairo
│   ├── roles
     │   ├── interface.cairo
     │   └── roles.cairo
```

Contracts in workspace/apps/staking/solidity are in scope

```js
└── workspace
    ├── apps
    │   └── staking
    │       └── solidity
    │           ├── IMintManager.sol
    │           ├── MintManager.sol
    │           ├── MintManagerStorage.sol
    │           ├── RewardSupplier.sol
    │           ├── RewardSupplierExternalInterfaces.sol
    │           └── RewardSupplierStorage.sol
```

## Compatibilities

Compatibilities:

  Blockchains:
      - Ethereum/Starknet
  
  Tokens:
      - STRK

[//]: # (scope-close)

[//]: # (getting-started-open)

## Setup

Clone the repo

```
git clone https://github.com/Cyfrin/2024-09-starknet-staking.git
```

Installation:

From within the project's root folder run:

``` bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
nvm install 20
curl -fsSL https://get.pnpm.io/install.sh | sh -
pnpm install turbo --global
pnpm install
```
	
Build:
```bash
Scarb build
```

Tests:
```bash
scarb test
```
[//]: # (getting-started-close)

[//]: # (known-issues-open)

## Known Issues

1. use of get_tx_info().account_contract_address in staking contract - will be replace with get_caller_address()
2. L1 roles management - out of scope. work in progress
3. change operational address - missing a check that the provided address is not currently in use.
4. ability to frontrun the use of another stakers operational address - out of scope
5. bool array - out of scope
6. remove_governance_admin function should have a safe-guard to avoid a sole governance admin to basically renounce their role
7. we don't consider the rewards rounding diff attack vector as concerning
  
[//]: # (known-issues-close)
