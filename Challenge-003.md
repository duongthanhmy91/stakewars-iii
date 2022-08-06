# Stake Wars: Episode III. Challenge 003

Deploy a staking pool contract with wallet satoshi.shardnet.near :

* <account_id>: mduong.shardnet.near

* <pool_name>: mduong

* <pool_id>: mduong.factory.shardnet.near

* <public_key>: ed25519:DRo4ic8Wse9R4XuUEqAburSyS2r6Y1KuLwfw1ngLvMMA

**Deploy a Staking Pool**

Calls the staking pool factory, creates a new staking pool with the specified name, and deploys it to the indicated accountId.

```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool_name>", "owner_id": "<accountId>", "stake_public_key": "<public_key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```
Be sure to have at least 30 NEAR available, it is the minimum required for storage.

Example 
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "satoshi", "owner_id": "satoshi.shardnet.near", "stake_public_key": "ed25519:DRo4ic8Wse9R4XuUEqAburSyS2r6Y1KuLwfw1ngLvMMA", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="satoshi.shardnet.near" --amount=30 --gas=300000000000000
```

![image](https://user-images.githubusercontent.com/6175292/181878400-cdfa5395-a1f2-4336-8e6a-542fc5a58254.png)

Let’s change reward commission to 1%

```
near call satoshi.factory.shardnet.near update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId satoshi.shardnet.near --gas=300000000000000
```
![image](https://user-images.githubusercontent.com/6175292/181878981-278630e1-8d84-49b6-8ed0-54b0192c2a63.png)

**Transactions Guide**


1. Deposit and Stake NEAR

In order to become validator we need NEAR on in our pool balance about [seat price](https://explorer.shardnet.near.org/nodes/validators), let’s send 1000 NEAR.

Command
```
near call satoshi.factory.shardnet.near deposit_and_stake --amount 1000 --accountId satoshi.shardnet.near --gas=300000000000000
```
   
 2. Unstake NEAR
   
Amount in yoctoNEAR.
 
  Run the following command to unstake:
 ```
 near call satoshi.factory.shardnet.near unstake '{"amount": "<amount yoctoNEAR>"}' --accountId satoshi.shardnet.near --gas=300000000000000
  ```
To unstake all you can run this one:
  ```
 near call satoshi.factory.shardnet.near unstake_all --accountId satoshi.shardnet.near --gas=300000000000000
```
3. Withdraw
  
 Unstaking takes 2-3 epochs to complete, after that period you can withdraw in YoctoNEAR from pool.
 
 Command:
 ```
 near call satoshi.factory.shardnet.near withdraw '{"amount": "<amount yoctoNEAR>"}' --accountId satoshi.shardnet.near --gas=300000000000000
  ```
 Command to withdraw all:
  
 ```
near call satoshi.factory.shardnet.near withdraw_all --accountId satoshi.shardnet.near --gas=300000000000000
```
**Balances** 

1. Total Balance

Command:
```
near view <staking_pool_id> get_account_total_balance '{"account_id": "<accountId>"}'
```
![image](https://user-images.githubusercontent.com/6175292/181879848-e21749c6-b558-4bbc-bae4-5eafab888c66.png)

2. Staked Balance

Command:
```
near view <staking_pool_id> get_account_staked_balance '{"account_id": "<accountId>"}'
```
![image](https://user-images.githubusercontent.com/6175292/181879874-5e6effff-394a-440b-8397-42977e170dab.png)

3. Unstaked Balance

Command:
```
near view <staking_pool_id> get_account_unstaked_balance '{"account_id": "<accountId>"}'
```
![image](https://user-images.githubusercontent.com/6175292/181879907-aec48184-d47f-4e7f-b933-6f618367b161.png)

4. Available for Withdrawal

You can only withdraw funds from a contract if they are unlocked.

Command:
```
near view <staking_pool_id> is_account_unstaked_balance_available '{"account_id": "<accountId>"}'
```
![image](https://user-images.githubusercontent.com/6175292/181879927-abb01748-6c83-4db5-8bb9-7521b0a985db.png)

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
near call satoshi.factory.shardnet.near ping '{}' --accountId satoshi.shardnet.near --gas=300000000000000
```
Upon completion, you can check your node should be in proposals stage on Near ShardNet by this command:
```
near proposals | grep 'satoshi'
```
![image](https://user-images.githubusercontent.com/6175292/181879740-0278f001-83db-4bb5-9d7b-e936b8229c9a.png)

## Let's go to challenge 4 🚀

[Check your Node](https://github.com/duongthanhmy91/stakewars-iii/blob/main/Challenge-004.md).
  
