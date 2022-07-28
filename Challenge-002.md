
# Challenge 002

This challenge is focused on deploying a node (nearcore), syncing it to the actual state of the network, then activating the node as a validator.

For chunk-only producers, the hardware requirements are reduced significantly. Recommended specs are as following:
| Hardware | Chunk-Only Producer Specifications |
| --- | --- |
| CPU | 4-Core CPU with AVX support |
| RAM | 8GB DDR4 |
| Storage | 500GB SSD |

Before you start, you may want to confirm that your machine has the right CPU features.

```
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
  && echo "Supported" \
  || echo "Not supported"
  ```
  
  ![image](https://user-images.githubusercontent.com/6175292/181564635-6e5c1917-6106-4dac-b622-4d6c0b629d5f.png)

**Install developer tools:**

```
sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo
```
**Install Python pip**
```
sudo apt install python3-pip -y
```
**Include base bin path**
```
USER_BASE_BIN=$(python3 -m site --user-base)/bin
export PATH="$USER_BASE_BIN:$PATH"
```
**Install build tools**
```
sudo apt install clang build-essential make -y
```
**Install Rust**
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
*If have the notification as below:

![image](https://user-images.githubusercontent.com/6175292/181572992-dfe22989-a9dd-45b0-9f84-067e7eb7b9a6.png)

Press Y and Enter to continue*

You will see the following:

![image](https://user-images.githubusercontent.com/6175292/181572954-053866eb-3fea-4241-9b06-ffedd4049791.png)

Press 1 and press enter.

Rust is installing now. Great!

![image](https://user-images.githubusercontent.com/6175292/181575181-0cdb087e-ef2d-481d-afe8-9cca36d56b62.png)


**Source the environment**
```
source $HOME/.cargo/env
```
**Clone nearcore project from GitHub**

```
git clone https://github.com/near/nearcore
cd nearcore 
git fetch
```
**Update the commit**
```
git checkout 0d7f272afabc00f4a076b1c89a70ffc62466efe9
```
Get the lastest commit at  [github.com/near/stakewars-iii/blob/main/commit](https://github.com/near/stakewars-iii/blob/main/commit.md)

![image](https://user-images.githubusercontent.com/6175292/181575613-c5167c9b-5970-4af1-b4fa-03651d15d5ca.png)

**Build the binary**


```
cargo build -p neard --release --features shardnet
```
This will take some time. Waiting ....

![image](https://user-images.githubusercontent.com/6175292/181578711-e0f06c60-e889-497e-a064-a7ad14648020.png)

**Initialize working directory**

Create the directory structure and generate config.json, node_key.json, and genesis.json.
```
./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
```
**Replace the config.json**
```
rm ~/.near/config.json && wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
```
**Install AWS Cli**
```
sudo apt-get install awscli -y
```
**Replace current genesis block**
```
rm ~/.near/genesis.json && wget -O ~/.near/genesis.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/genesis.json
```
*If the above fails, AWS CLI may be oudated in your distribution repository. Instead, try:*
```
pip3 install awscli --upgrade
```
**Run the node**
```
cd ~/nearcore
./target/release/neard --home ~/.near run
```





  











