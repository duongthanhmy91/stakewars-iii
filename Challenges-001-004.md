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

*# Install Node.js and npm*
```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
sudo apt install build-essential nodejs -y
PATH="$PATH"
```
#Check version
```
node -v
v18.6.0

npm -v
8.13.2
```
*# Install NEAR-CLI, you can use sudo that help wihtout logged in as root* 
```
sudo npm install -g near-cli
```
*# Select the network shardnet ( this is the network we will use for Stake Wars )*
```
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc && source ~/.bashrc
```
#### Server Requirements

Please see the hardware requirement below:

First, we will start with installing Node.js and npm:

curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
sudo apt install build-essential nodejs
PATH="$PATH"
Check Node.js and npm version:

