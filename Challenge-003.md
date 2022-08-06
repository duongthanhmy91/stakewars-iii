# Stake Wars: Episode III. Challenge 003

Deploy a staking pool contract with wallet mduong.shardnet.near :

* <account_id>: mduong.shardnet.near

* <pool_name>: mduong

* <pool_id>: mduong.factory.shardnet.near

* <public_key>: ed25519:Cjf3mKtwoNEcPaamUtt4KV9u9dY8ELwxzhGskKPeaj19

**Deploy a Staking Pool**

Calls the staking pool factory, creates a new staking pool with the specified name, and deploys it to the indicated accountId.

```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool_name>", "owner_id": "<accountId>", "stake_public_key": "<public_key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```
Be sure to have at least 30 NEAR available, it is the minimum required for storage.

Example 
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "mduong", "owner_id": "mduong.shardnet.near", "stake_public_key": "ed25519:Cjf3mKtwoNEcPaamUtt4KV9u9dY8ELwxzhGskKPeaj19", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="mduong.shardnet.near" --amount=30 --gas=300000000000000
```

Let’s change reward commission to 1%

```
near call mduong.factory.shardnet.near update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId mduong.shardnet.near --gas=300000000000000
```
![image](https://user-images.githubusercontent.com/6175292/183257704-ce124a35-3166-402c-a386-c5a36b4fcfc2.png)

**Transactions Guide**


1. Deposit and Stake NEAR

In order to become validator we need NEAR on in our pool balance about [seat price](https://explorer.shardnet.near.org/nodes/validators), let’s send 1000 NEAR.

Command
```
near call mduong.factory.shardnet.near deposit_and_stake --amount 1000 --accountId mduong.shardnet.near --gas=300000000000000
```
 ![image](https://user-images.githubusercontent.com/6175292/183257742-cf1b6f14-2bf8-4abd-8592-7a2c137a6aeb.png)
  
 2. Unstake NEAR
   
Amount in yoctoNEAR.
 
  Run the following command to unstake:
 ```
 near call mduong.factory.shardnet.near unstake '{"amount": "<amount yoctoNEAR>"}' --accountId mduong.shardnet.near --gas=300000000000000
  ```
To unstake all you can run this one:
  ```
 near call mduong.factory.shardnet.near unstake_all --accountId mduong.shardnet.near --gas=300000000000000
```
3. Withdraw
  
 Unstaking takes 2-3 epochs to complete, after that period you can withdraw in YoctoNEAR from pool.
 
 Command:
 ```
 near call mduong.factory.shardnet.near withdraw '{"amount": "<amount yoctoNEAR>"}' --accountId mduong.shardnet.near --gas=300000000000000
  ```
 Command to withdraw all:
  
 ```
near call mduong.factory.shardnet.near withdraw_all --accountId mduong.shardnet.near --gas=300000000000000
```
**Balances** 

1. Total Balance

Command:
```
near view mduong.factory.shardnet.near get_account_total_balance '{"account_id": "mduong.shardnet.near"}'
```
![image](https://user-images.githubusercontent.com/6175292/183257800-f990027a-0315-4c89-8588-f9a22562e099.png)


2. Staked Balance

Command:
```
near view  mduong.factory.shardnet.near get_account_staked_balance '{"account_id": "mduong.shardnet.near"}'
```

3. Unstaked Balance

Command:
```
near view mduong.factory.shardnet.near get_account_unstaked_balance '{"account_id": "mduong.shardnet.near"}'
```

4. Available for Withdrawal

You can only withdraw funds from a contract if they are unlocked.

Command:
```
near view mduong.factory.shardnet.near is_account_unstaked_balance_available '{"account_id": "mduong.shardnet.near"}'
```

**Pause / Resume Staking**
1. Pause
Command:
```
near call <staking_pool_id> pause_staking '{}' --accountId <accountId>
```
2. Resume
Command:
```
near call <staking_pool_id> resume_staking '{}' --accountId <accountId>
```
**Submit the proposal** 

In order to have a validator seat, you must submit a proposal with a ping. A ping issues a new proposal and updates the staking balances for your delegators. A ping should be issued each epoch to keep reported rewards current
```
near call mduong.factory.shardnet.near ping '{}' --accountId mduong.shardnet.near --gas=300000000000000
```
Upon completion, you can check your node should be in proposals stage on Near ShardNet by this command:
```
near proposals | grep 'mduong'
```
![image](https://user-images.githubusercontent.com/6175292/183257876-c5b1b94c-ca32-4fa9-bfc4-2c000fe3ee95.png)


## Let's go to challenge 4 🚀

[Check your Node](https://github.com/duongthanhmy91/stakewars-iii/blob/main/Challenge-004.md).
  
