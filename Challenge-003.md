# Stake Wars: Episode III. Challenge 003

Deploy a staking pool contract.

* <account_id>: satoshi.shardnet.near

* <pool_name>: satoshi

* <pool_id>: satoshi.factory.shardnet.near

* <public_key>: ed25519:7MmAhpHNbUh4AWnaG7hsmfoX2CLsS57xAYWSEMjyXjuB

**Deploy a Staking Pool**

Calls the staking pool factory, creates a new staking pool with the specified name, and deploys it to the indicated accountId.

```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool id>", "owner_id": "<accountId>", "stake_public_key": "<public_key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```
Be sure to have at least 30 NEAR available, it is the minimum required for storage.

**Staking to the pool**
In order to become validator we need NEAR on in our pool balance about [seat price](https://explorer.shardnet.near.org/nodes/validators), let’s send 1000 NEAR.
```
near call satoshi.factory.shardnet.near deposit_and_stake --amount 1000 --accountId satoshi.shardnet.near --gas=300000000000000```
```
Let’s change reward commission to 1%

```
near call satoshi.factory.shardnet.near update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId satoshi.shardnet.near --gas=300000000000000
```
**Transactions Guide**



