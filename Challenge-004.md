# Challenge 004 
Setup tools for monitoring node status. Install and use RPC on port 3030 to get useful information for keep your node working.
## Common RPC commands
### Check your node version
```
curl -s http://127.0.0.1:3030/status | jq .version
```
![image](https://user-images.githubusercontent.com/6175292/183258057-587bfdc2-c6d6-4ab8-bbef-dd6c79bb5633.png)


### Check delegators and stake 
```
near view mduong.factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId mduong.shardnet.near
```
![image](https://user-images.githubusercontent.com/6175292/183258095-9227c66d-3297-483c-a125-73fd05da08bd.png)

### Check reason for validator kicked
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' https://rpc.shardnet.near.org/ | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("mduong"))' | jq .reason
```
![image](https://user-images.githubusercontent.com/6175292/181880298-20d27f97-d804-4238-b382-004f99b4c324.png)

### Check blocks produced / expected
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' http://localhost:3030/ | jq -c '.result.current_validators[] | select(.account_id | contains ("mduong.factory.shardnet.near"))' | jq
```
Your node must be active to be visualized by this command.

![image](https://user-images.githubusercontent.com/6175292/182010279-3fc199f4-87f4-4b84-a2cf-c963a9e4d224.png)

