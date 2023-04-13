
Исследование 
Objectarium
1. Instantiate
4D53DBDEE2843BAF2E53A0D0AA0BF2E23BCD4AC0643996EBABEF3CDC5BB99F8A
2. Execute
3D3E17EFC6A872F3C904F4AC62B2977100338B34EE84B373E2EEAD87D77FB8A8
3. Pin

4. Unpin

5. Forget





## Preparation
```python
Installation
```
```bash
git clone https://github.com/okp4/okp4d.git
cd okp4d
make install
   
okp4d version 
# 4.1.0
```

```python
Wllet Recovery
```

```bash
okp4d keys add wallet --recover
```
#

### I'll be doing research from my MAC without sync, so I'll be using open RPC.
```python
List Of Open RPC
```
```http
1: http://195.201.228.51:27657

2: http://195.201.194.249:26657

3: http://154.12.225.88:26657

4: http://65.108.6.45:61357

5: http://185.144.99.16:26657

6: http://65.108.249.79:36657

7: http://167.235.21.165:46657

8: http://144.76.97.251:12657

9: http://144.76.97.251:12657

10: http://88.99.164.158:10097

11: http://54.36.109.62:26657

12: http://65.109.88.162:36657

13: http://194.163.162.56:28657

14: http://65.108.131.190:23457

15: http://95.111.225.137:37657

16: http://54.36.109.62:11157

17: http://135.181.139.153:26657

18: http://95.111.225.137:37657

19: http://65.21.170.3:42657

20: http://65.109.93.152:28657

21: http://65.109.38.208:46657

22: http://136.243.88.91:6041
```
```python
Update client.toml
```
```
okp4d config node http://195.201.228.51:27657
```
```
okp4d config chain-id okp4-nemeton-1
```
___
# Objectarium

## Overview

The `okp4-objectarium` smart contract enables the storage of arbitrary `objects` in any [Cosmos blockchains](https://cosmos.network/) using the [CosmWasm](https://cosmwasm.com/) framework.

This contract allows for storing `objects`, pinning and unpinning `objects` for a given sender address, and it also includes the ability to remove (forget) `objects` if they are no longer pinned.

## Usage

### Instantiate

The `okp4-objectarium` can be instantiated as follows, refer to the schema for more information on configuration, limits and pagination configuration:

```bash
okp4d tx wasm instantiate 2 \
    --label "TestnetPride" \
    --from okp418hhw0nx2wqctk22t52nm8qypxpzkstcxd689qh \
    --admin okp418hhw0nx2wqctk22t52nm8qypxpzkstcxd689qh \
    --gas 1000000 \
    --broadcast-mode sync \
    "{\"bucket\":"\"TestnetPride\"",\"limits\":{}, \"pagination\": {}}" \
    --fees 2000uknow \
    --chain-id okp4-nemeton-1 \
    --node http://167.235.21.165:46657
```
<img width="365" alt="image" src="https://user-images.githubusercontent.com/83868103/231804268-77d67738-7030-45fd-897a-053fed2a33c3.png"> <img width="600" alt="image" src="https://user-images.githubusercontent.com/83868103/231805293-ae1ae765-ac06-47e5-8ff8-3e3dad801105.png">

Получаем адрес контракта и записываем в переменную

```
txhash=4D53DBDEE2843BAF2E53A0D0AA0BF2E23BCD4AC0643996EBABEF3CDC5BB99F8A
```
<img width="684" alt="image" src="https://user-images.githubusercontent.com/83868103/231808055-d22072ea-feea-4052-afdc-8e175a7f9b0d.png">

```
CONTRACT_ADDR=$(okp4d q tx $txhash -o json | jq -r '.logs[].events[0].attributes[0].value')
```



### Execute

cd $HOME/.okp4d

touch data.txt


We can store an object by providing its data in base64 encoded, we can pin the stored object to prevent it from being removed:

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from okp418hhw0nx2wqctk22t52nm8qypxpzkstcxd689qh \
    --gas 1000000 \
    --broadcast-mode sync \
    --fees 2000uknow \
    --chain-id okp4-nemeton-1 \
    --node http://167.235.21.165:46657 \
    "{\"store_object\":{\"data\": \"$(echo "/Users/romanv1812/.okp4d/data.txt" | base64)\",\"pin\":true}}"
```

<img width="525" alt="image" src="https://user-images.githubusercontent.com/83868103/231813532-b1ca9849-1eee-469e-b25d-279fc2309aa4.png"> <img width="465" alt="image" src="https://user-images.githubusercontent.com/83868103/231813704-6623ebb9-98dd-4cfa-8f97-5d87f59a4178.png">



The object id is stable as it is a hash, we can't store an object twice.
```
OBJECT_ID=$(okp4d q tx 3D3E17EFC6A872F3C904F4AC62B2977100338B34EE84B373E2EEAD87D77FB8A8 -o json | jq -r .logs[].events[2].attributes[2].value)
```
With the following commands we can pin and unpin existing objects:

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDR \
    --gas 1000000 \
    --broadcast-mode block \
    "{\"pin_object\":{\"id\": \"$OBJECT_ID\"}}"
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDR \
    --gas 1000000 \
    --broadcast-mode block \
    "{\"unpin_object\":{\"id\": \"$OBJECT_ID\"}}"
```

And if an object is not pinned, or pinned by the sender of transaction, we can remove it:

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDR \
    --gas 1000000 \
    --broadcast-mode block \
    "{\"forget_object\":{\"id\": \"$OBJECT_ID\"}}"
```

### Query

Query an object by its id:

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object\": {\"id\": \"$OBJECT_ID\"}}"
```

Or its data:

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object_data\": {\"id\": \"$OBJECT_ID\"}}"
```

We can also list the objects, eventually filtering on the object owner:

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"objects\": {\"address\": \"okp41p8u47en82gmzfm259y6z93r9qe63l25dfwwng6\"}}"
```

And navigate in a cursor based pagination:

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"objects\": {\"first\": 5, \"after\": \"23Y5t5DBe7DkPwfJo3Sd26Y8Z9epmtpA1FTpdG7DiG6MD8vPRTzzbQ9TccmyoBcePkPK6atUiqcAzJVo3TfYNBGY\"}}"
```

We can also query object pins with the same cursor based pagination:

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object_pins\": {\"id\": \"$OBJECT_ID\", \"first\": 5, \"after\": \"23Y5t5DBe7DkPwfJo3Sd26Y8Z9epmtpA1FTpdG7DiG6MD8vPRTzzbQ9TccmyoBcePkPK6atUiqcAzJVo3TfYNBGY\"}}"
```
