
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
This will take some time. Waiting to finish.

![image](https://user-images.githubusercontent.com/6175292/181591151-711c7c1a-5e15-419d-b8a2-feaca1841aa6.png)

**Initialize working directory**

Create the directory structure and generate config.json, node_key.json, and genesis.json.
```
./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
```
![image](https://user-images.githubusercontent.com/6175292/181591559-c8632fd5-9080-493e-abd9-a5fdab02d70c.png)


**Replace the config.json**
```
rm ~/.near/config.json && wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
```
![image](https://user-images.githubusercontent.com/6175292/181591692-028be7c9-7675-4fe0-aec1-d5a2f3fcaeeb.png)

**Install AWS Cli**
```
sudo apt-get install awscli -y
```
**Replace current genesis block**
```
rm ~/.near/genesis.json && wget -O ~/.near/genesis.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/genesis.json
```
![image](https://user-images.githubusercontent.com/6175292/181592001-2f1291e8-673c-4f88-a825-315845250d86.png)


*If the above fails, AWS CLI may be oudated in your distribution repository. Instead, try:*
```
pip3 install awscli --upgrade
```
**Run the node**
```
cd ~/nearcore
./target/release/neard --home ~/.near run
```

![image](https://user-images.githubusercontent.com/6175292/181593737-6c193b7e-2a0b-4a91-9d00-b4c84b27c4f8.png)


![image](https://user-images.githubusercontent.com/6175292/181593300-88ac3631-427b-4f09-89c7-38133bf343cd.png)


We need to wait for Downloading headers 100% and Downloading blocks 100% Then Ctrl + C to exit this command.

**Activating the node as validator**

On next step, we need to setup node as validator. To setup a validator we need to sign transactions and this required access to our wallet keys. 








  











