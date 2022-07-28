
# Challenge 001 

Create your Shardnet wallet & deploy the NEAR CLI. This is designed to be your very first challenge: use it to understand how staking on NEAR works.

NEAR-CLI is a command-line interface that communicates with the NEAR blockchain via remote procedure calls (RPC):

* Setup and Installation NEAR CLI

* View Validator Stats

## 1. Create a wallet on ShardNet 

Go to https://wallet.shardnet.near.org/ .create wallet choose your name and save seed phrase. This walled will be used to hold NEAR tokens.


## 2. Setup NEAR-CLI

*If you use cloud providers to run your node please refer [Challenge 005](https://github.com/duongthanhmy91/stakewars-iii/blob/main/Challenges-005.md) first*

Access to server via SSH and do the below commands: 

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
*#Check version*
```
node -v
```
![image](https://user-images.githubusercontent.com/6175292/181299316-59461d8c-bb40-4e3a-a3bc-478840c72746.png)

```
npm -v
```

![image](https://user-images.githubusercontent.com/6175292/181299248-3f2352a6-1993-455b-9d11-9504b1c3c152.png)


*# Install NEAR-CLI, you can use sudo that help without logged in as root* 
```
sudo npm install -g near-cli
```
![image](https://user-images.githubusercontent.com/6175292/181299576-c1063fb3-1eea-4fe4-bd9e-31993f2e5761.png)

*# Select the shardnet network ( this is the network we will use for Stake Wars ). This command will put it to .bashrc and these variables will loading automatically for every new terminal session.*
```
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc && source ~/.bashrc
```
## NEAR CLI Commands Guide:

We ready to execute some commands, let’s see how works.

*# Proposals*

A proposal by a validator indicates they would like to enter the validator set, in order for a proposal to be accepted it must meet the minimum seat price.

Command: 
```
near proposals
```
![image](https://user-images.githubusercontent.com/6175292/181531103-ea2d7b44-10ac-4dec-95dd-bac62aa3468a.png)

*# Validators Current*

This shows a list of active validators in the current epoch, the number of blocks produced, number of blocks expected, and online rate. Used to monitor if a validator is having issues.

Command:

```
near validators current
```
![image](https://user-images.githubusercontent.com/6175292/181532949-af571eda-7d83-4796-8e60-93f6f107192b.png)


*# Validators Next*

This shows validators whose proposal was accepted one epoch ago, and that will enter the validator set in the next epoch.

Command: 
```
near validators next
```
![image](https://user-images.githubusercontent.com/6175292/181538688-e2084204-adde-468a-beed-4362ff0a1ecc.png)


Full list of Near CLI commands: https://github.com/near/near-cli

Now We will go to Challenge 002 [Setup and Run your Node](https://github.com/duongthanhmy91/stakewars-iii/blob/main/Challenge-002.md)












