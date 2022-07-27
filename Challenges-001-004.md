# NEAR Stake Wars Challenges 001 → 004 by MyDuong
## Challenge 001 

Create your Shardnet wallet & deploy the NEAR CLI. This is designed to be your very first challenge: use it to understand how staking on NEAR works.

NEAR-CLI is a command-line interface that communicates with the NEAR blockchain via remote procedure calls (RPC):

* Setup and Installation NEAR CLI

* View Validator Stats

### 1. Create a wallet on ShardNet 

Go to https://wallet.shardnet.near.org/ . Created new account and Make sure to backup your seed phrase.

### 2. Setup NEAR-CLI

Access to server via SSH and do the below commands: 
*If you use cloud providers to run your node please refer [Challenge 005](https://github.com/duongthanhmy91/stakewars-iii/edit/main/005.md) first:*

*# Update linux machine*
```
sudo apt update && sudo apt upgrade -y
```
![image](https://user-images.githubusercontent.com/6175292/181298222-08cfd6f9-9e67-4327-a03a-d850c423e4e9.png)

*# Install Node.js and npm*
```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
sudo apt install build-essential nodejs -y
PATH="$PATH"
```
#Check version
```
node -v
```
![image](https://user-images.githubusercontent.com/6175292/181299316-59461d8c-bb40-4e3a-a3bc-478840c72746.png)

```
npm -v
```

![image](https://user-images.githubusercontent.com/6175292/181299248-3f2352a6-1993-455b-9d11-9504b1c3c152.png)


*# Install NEAR-CLI, you can use sudo that help wihtout logged in as root* 
```
sudo npm install -g near-cli
```
![image](https://user-images.githubusercontent.com/6175292/181299576-c1063fb3-1eea-4fe4-bd9e-31993f2e5761.png)

*# Select the shardnet network ( this is the network we will use for Stake Wars )*
```
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc && source ~/.bashrc
```
### NEAR CLI Commands Guide:

*# Proposals*

A proposal by a validator indicates they would like to enter the validator set, in order for a proposal to be accepted it must meet the minimum seat price.

Command: 
```
near proposals
```
![image](https://user-images.githubusercontent.com/6175292/181300569-d32bc881-755e-4112-be96-87b12a1048a6.png)

*# Validators Current*

This shows validators whose proposal was accepted one epoch ago, and that will enter the validator set in the next epoch.

Command:

```
near validators next
```








