
Исследование 
Objectarium
1. Instantiate
4D53DBDEE2843BAF2E53A0D0AA0BF2E23BCD4AC0643996EBABEF3CDC5BB99F8A
2. Execute
3D3E17EFC6A872F3C904F4AC62B2977100338B34EE84B373E2EEAD87D77FB8A8
3. Pin
A01BC3E78D997E1D6C9D892BB246D93D17EB3106E513E95046451D444D9B5CE5
4. Unpin
01592651A249E4F53918717288E9A276411CDB6376ABF27B34140EC25EF263D6
5. Forget
C96ED7775252F1BAC1FDDD0A6A0025E307C5D17035791E0931032C788241D83F




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

```python
Declaring Variables
```
```
ADDRESS=okp418hhw0nx2wqctk22t52nm8qypxpzkstcxd689qh
```


The `okp4-objectarium` can be instantiated as follows, refer to the schema for more information on configuration, limits and pagination configuration:

```bash
okp4d tx wasm instantiate 2 \
    --label "TestnetPride" \
    --from $ADDRESS \
    --admin $ADDRESS \
    --gas 1000000 \
    "{\"bucket\":"\"TestnetPride\"",\"limits\":{}, \"pagination\": {}}" \
    --fees 200uknow \
    -y
```
<img width="587" alt="image" src="https://user-images.githubusercontent.com/83868103/231832042-ca7043dd-e5b3-4eee-81be-f22973c060c7.png">

The resulting transaction hash is assigned to a variable:

```bash
txhash=4D53DBDEE2843BAF2E53A0D0AA0BF2E23BCD4AC0643996EBABEF3CDC5BB99F8A
```

```bash
CONTRACT_ADDR=$(okp4d q tx $txhash -o json | jq -r '.logs[].events[0].attributes[0].value')
```
<img width="988" alt="image" src="https://user-images.githubusercontent.com/83868103/231831622-b7247f91-efbe-4664-97a5-f4382b5d8006.png">




### Execute



touch $HOME/data.txt

We can store an object by providing its data in base64 encoded, we can pin the stored object to prevent it from being removed:

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"store_object\":{\"data\": \"$(echo "$HOME/data.txt" | base64)\",\"pin\":true}}" \
    -y
```
The resulting transaction hash is assigned to a variable:
```bash
txhash=B9E2B23A0A57B53C86A4E31A7156407CFDF1B2640941C798F1F60B119304AC84
```
```bash
OBJECT_ID=$(okp4d q tx $txhash -o json | jq -r '.logs[].events[2].attributes[2].value')
```
<img width="951" alt="image" src="https://user-images.githubusercontent.com/83868103/231835702-912bbe54-6234-457b-9d04-58db5407269d.png">

The object id is stable as it is a hash, we can't store an object twice.

With the following commands we can pin and unpin existing objects:

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"pin_object\":{\"id\": \"$OBJECT_ID\"}}" \
    -y
```
A01BC3E78D997E1D6C9D892BB246D93D17EB3106E513E95046451D444D9B5CE5
```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object\": {\"id\": \"$OBJECT_ID\"}}"
```

<img width="687" alt="image" src="https://user-images.githubusercontent.com/83868103/231836995-be436974-f3df-4d7d-8106-555f5519154d.png">

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"unpin_object\":{\"id\": \"$OBJECT_ID\"}}" \
    -y
```
01592651A249E4F53918717288E9A276411CDB6376ABF27B34140EC25EF263D6
```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object\": {\"id\": \"$OBJECT_ID\"}}"
```
<img width="694" alt="image" src="https://user-images.githubusercontent.com/83868103/231838649-e2248d62-b40e-4089-83c8-6909a4d97e39.png">


And if an object is not pinned, or pinned by the sender of transaction, we can remove it:

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"forget_object\":{\"id\": \"$OBJECT_ID\"}}" \
    -y
```

C96ED7775252F1BAC1FDDD0A6A0025E307C5D17035791E0931032C788241D83F

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
    "{\"objects\": {\"address\": \"$ADDRESS\"}}"
```

And navigate in a cursor based pagination:

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"objects\": {\"first\": 5, \"after\": \"32MUGxHoR66M4HT8ga7haKS6tLkJ1w5P4du6q3X9tZqvdSuSHNoUzwQCPwPyW8u5xLxso1Qx99GexVGfLGep1Wfv\"}}"
```

We can also query object pins with the same cursor based pagination:

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object_pins\": {\"id\": \"$OBJECT_ID\", \"first\": 5, \"after\": \"32MUGxHoR66M4HT8ga7haKS6tLkJ1w5P4du6q3X9tZqvdSuSHNoUzwQCPwPyW8u5xLxso1Qx99GexVGfLGep1Wfv\"}}"
```
