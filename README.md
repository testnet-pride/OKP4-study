Задача:

Description
During this phase we'll start using the logic module and upload smart contracts implementing the protocol, the related transaction messages will have a certain gas consumption which may at first be irrelevant in comparison with the actual execution cost. Regarding your validation role, you have at your disposal elements allowing you to judge this relevance.

Send us a study highlighting gas consumption relevancy in relation with elements at your disposal (e.g. Memory and CPU usage). Argued with curated data from your running Node, provide us feedback and suggestions to help us ensuring a fair cost.

We advise you to wait for the second part of the phase before publishing - new smart contracts will be tested during this phase, we'll provide documentation to interact with them.

Here are some documentation and usage examples for okp4-objectarium and okp4-law-stone smart contracts. Only Druid's delegator addresses can instantiate those contracts, through the code id 2 for cw-storage and 3 for cw-law-stone.

Rewards
Up to 10 000 pts

Judging Criteria
OKP4 team will judge if any submission deserves points or not based on the following:

Relevance
Arguments backed by data
Usefulness
Non-relevant submissions or low-value ones will earn 0 points.

How to Submit
Publish a 1 page report / dashboards using this form.


Исследование 

Подготовка

Установка бинарника 
```bash
git clone https://github.com/okp4/okp4d.git
cd okp4d
make install
   
okp4d version 
# 4.1.0
```
восстановление кошелька друида
```bash
okp4d keys add wallet --recover
```

I will conduct the study from my MAC, so I will use open RPC

Добавить RPC в client.toml

```
okp4d config node http://195.201.228.51:27657
```


Here is a list of open RPC I received that I will use for research:
```
http://195.201.228.51:27657

http://195.201.194.249:26657

http://154.12.225.88:26657

http://65.108.6.45:61357

http://185.144.99.16:26657

http://65.108.249.79:36657

http://167.235.21.165:46657

http://144.76.97.251:12657

http://144.76.97.251:12657

http://88.99.164.158:10097

http://54.36.109.62:26657

http://65.109.88.162:36657

http://194.163.162.56:28657

http://65.108.131.190:23457

http://95.111.225.137:37657

http://54.36.109.62:11157

http://135.181.139.153:26657

http://95.111.225.137:37657

http://65.21.170.3:42657

http://65.109.93.152:28657

http://65.109.38.208:46657

http://136.243.88.91:6041
```

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

CONTRACT_ADDR=$(okp4d q tx $txhash -o json | jq -r .logs[].events[1].attributes[0].value)
```



### Execute

We can store an object by providing its data in base64 encoded, we can pin the stored object to prevent it from being removed:

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDR \
    --gas 1000000 \
    --broadcast-mode block \
    "{\"store_object\":{\"data\": \"$(cat my-data | base64)\",\"pin\":true}}"
```

The object id is stable as it is a hash, we can't store an object twice.

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
