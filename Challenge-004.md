# Challenge 004 
Setup tools for monitoring node status. Install and use RPC on port 3030 to get useful information for keep your node working.
## Common RPC commands
### Check your node version
```
curl -s http://127.0.0.1:3030/status | jq .version
```
![image](https://user-images.githubusercontent.com/6175292/181880073-c0cb3670-cae6-4a40-a653-024210416a33.png)

### Check delegators and stake 
```
near view satoshi.factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId satoshi.shardnet.near
```
![image](https://user-images.githubusercontent.com/6175292/181880097-bd68268f-0f22-4280-a9d3-af31cea8d5b0.png)
### Check reason for validator kicked
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' https://rpc.shardnet.near.org/ | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("satoshi"))' | jq .reason
```
![image](https://user-images.githubusercontent.com/6175292/181880298-20d27f97-d804-4238-b382-004f99b4c324.png)

### Check blocks produced / expected
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' http://localhost:3030/ | jq -c '.result.current_validators[] | select(.account_id | contains ("andreapn.factory.shardnet.near"))' | jq
```
Your node must be active to be visualized by this command.

![image](https://user-images.githubusercontent.com/6175292/182010279-3fc199f4-87f4-4b84-a2cf-c963a9e4d224.png)

