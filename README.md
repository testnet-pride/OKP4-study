<img width="1291" alt="image" src="https://user-images.githubusercontent.com/83868103/231887751-ad822f8b-9aef-454a-be83-d338ced45046.png">



**The task is to conduct a study on gas consumption in relation to elements such as memory and CPU usage, with the goal of providing feedback and suggestions to ensure a fair cost for smart contracts implementing the protocol using the logic module.** 

**The study should be based on curated data from a running Node, and the results should be communicated to the team. Only Druid's delegator addresses can instantiate the okp4-objectarium and okp4-law-stone smart contracts, through the code id 2 for cw-storage and 3 for cw-law-stone.** 

**The team advises waiting for the second part of the phase before publishing, as new smart contracts will be tested during this phase and documentation will be provided for interacting with them.**
#
**For the task, the following equipment was selected: AX101 Dedicated Server Hetzner, CX11 Virtual Server Hetzner, and Apple MacBook Pro 16" 2021 M1 Max 10-Core located at home.**



| |AX101 Dedicated Server Hetzner | CX11 Virtual Server Hetzner | Apple MacBook Pro 16" 2021 M1 Max 10-Core |
| ---| --- | --- | --- |
| Processor | 32 CPU | 1 VCPU | 10 CPU |
| RAM | 128 GB  | 2 GB | 64 GB |
| Memory | 6.8 TB NVMe  | 20 GB NVMe | 2 TB NVMe |
| Bandwidth | 1 Gbit/s-Port | 400 Mbit/s-Port | 1 Gbit/s-Port |
#
**The research is presented in the form of tables that contain the study results.**
### [**`Objectarium`**](https://github.com/testnet-pride/OKP4-study#objectarium)
| Equipment | Action | Hash | Gas |
| ----- | ----------- | ---------------------------------------------------------------- | ------- |
| AX101 | Instantiate | 8C5C657FB723A5BFCEFD5C9DE519DC94A24271027256BD7C8E13B7124DEEEA8B | 194 972 |
| CX11  | Instantiate | C1B4F73EA23A88B2AD2FB501AD3E38AA5C74743276BE0F174404E43F29FA5EDD | 194 732 |
|MacBook| Instantiate | 4D53DBDEE2843BAF2E53A0D0AA0BF2E23BCD4AC0643996EBABEF3CDC5BB99F8A | 195 453 |
|       |             |                                                                  |         |
| AX101 | Execute     | B59FFEDD0CEFE1FD0FA02BE99E492A9A15CC6E91A1135A8404A7517A238CD109 | 207 651 |
| CX11  | Execute     | 6EC867A12D5C401A9663B971C3119D9B0DF9EF6E940F80FB6D1AED74F15FD420 | 209 918 |
|MacBook| Execute     | 3D3E17EFC6A872F3C904F4AC62B2977100338B34EE84B373E2EEAD87D77FB8A8 | 211 840 |
|       |             |                                                                  |         |
| AX101 | Pin         | 9104D33750BE14AC2D4A04D8AE3CBFCE2673799E53FDA92908EF39A79230FC0E | 149 058 |
| CX11  | Pin         | 383B947184532D546D34E994B1D14F3161F6D834B56A29ADC1222259E4591F37 | 149 046 |
|MacBook| Pin         | A01BC3E78D997E1D6C9D892BB246D93D17EB3106E513E95046451D444D9B5CE5 | 149 070 |
|       |             |                                                                  |         |
| AX101 | Unpin       | 38EF763C3A3E9BE0DECF9FBBDBB40668C1E49CB9A609538968BBBAD3548BBECD | 164 550 |
| CX11  | Unpin       | B3C469B551C4FE6F46DAD456729CFF6635411ED1DAE889573BC4DF9F994E665E | 167 399 |
|MacBook| Unpin       | 01592651A249E4F53918717288E9A276411CDB6376ABF27B34140EC25EF263D6 | 167 423 |
|       |             |                                                                  |         |
| AX101 | Forget      | 774D3A919A952C66E1455BF214E490C09D2817FE1D5BA3588D9E9D7C38A269DF | 170 355 |
| CX11  | Forget      | CD4C729DBE193AC70F69F1D7F39A46B54E20342FD29585FBB88091D2D63260AC | 167 482 |
|MacBook| Forget      | C96ED7775252F1BAC1FDDD0A6A0025E307C5D17035791E0931032C788241D83F | 170 530 |

**Based on the provided data, it appears that the gas consumption for instantiating and executing the smart contracts is consistent across different equipment (AX101, CX11, and MacBook) with values ranging from `194,732` to `211,840`.**

**Additionally, the gas consumption for pinning, unpinning, and forgetting varies slightly across the different equipment, with values ranging from `149,046` to `170,530`.**

**Based on these findings, it appears that the gas consumption is independent of the equipment used and is mostly consistent across different actions. However, it is important to continue monitoring and analyzing the gas consumption as new smart contracts.**

### [**`Single source`**](https://github.com/testnet-pride/OKP4-study#single-source)
| Equipment | Action | Hash | Gas |
| ----- | ----------- | ---------------------------------------------------------------- | ------- |
| AX101 | Instantiate | 1A1FDCE9849074D5B1512C71B69982A1679A45559DE89D8C5C3F9F9ADB78FC72 | 376 146 |
| CX11  | Instantiate | 667048F2A480C3ABED07B3C9675868D79B007353FA57E70D27CAD84D7B9F2CF7 | 375 747 |
|MacBook| Instantiate | 172B0046B083CDE704D5DB33FE1F66052C0CC9D6B4859BE2F296F1352C132024 | 287 796 |
|       |             |                                                                  |         |
| AX101 | Break | 1A1FDCE9849074D5B1512C71B69982A1679A45559DE89D8C5C3F9F9ADB78FC72 | 149 287 |
| CX11  | Break | 667048F2A480C3ABED07B3C9675868D79B007353FA57E70D27CAD84D7B9F2CF7 | 287 796 |
|MacBook| Break | 172B0046B083CDE704D5DB33FE1F66052C0CC9D6B4859BE2F296F1352C132024 | 146 441 |

**The presented table allows to conclude that each equipment (AX101 Dedicated Server Hetzner, CX11 Virtual Server Hetzner, Apple MacBook Pro 16" 2021 M1 Max 10-Core) was used to perform two operations - contract instantiation and deinstantiation, as well as contract destruction operation. Each operation consumed a certain amount of gas. However, there is no clear connection between the equipment and the amount of consumed gas.**
___

### `Navigation:`
- [**`Preparation`**](https://github.com/testnet-pride/OKP4-study#preparation)
- [**`Objectarium`**](https://github.com/testnet-pride/OKP4-study#objectarium)
  - [`Instantiate`](https://github.com/testnet-pride/OKP4-study#instantiate)
  - [`Execute`](https://github.com/testnet-pride/OKP4-study#execute)
  - [`Pin`](https://github.com/testnet-pride/OKP4-study#pin)
  - [`Unpin`](https://github.com/testnet-pride/OKP4-study#unpin)
  - [`Forget`](https://github.com/testnet-pride/OKP4-study#forget)
- [**`Single source`**](https://github.com/testnet-pride/OKP4-study#single-source)
  - [`Instantiate`](https://github.com/testnet-pride/OKP4-study#instantiate-1) 
  - [`Query`](https://github.com/testnet-pride/OKP4-study#query-1)
  - [`Break`](https://github.com/testnet-pride/OKP4-study#break)

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

### For the same experiment conditions, I will use 1 PRC in all tests
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
___

## Usage

### Instantiate

```python
Declaring Variables
```
```
LABEL=TP-test1
ADDRESS=okp418hhw0nx2wqctk22t52nm8qypxpzkstcxd689qh
```

**The `okp4-objectarium` can be instantiated as follows, refer to the schema for more information on configuration, limits and pagination configuration:**
```bash
okp4d tx wasm instantiate 2 \
    --label "$LABEL" \
    --from $ADDRESS \
    --admin $ADDRESS \
    --gas 1000000 \
    "{\"bucket\":"\"$LABEL\"",\"limits\":{}, \"pagination\": {}}" \
    --fees 200uknow \
    -y
```

**The resulting transaction hash is assigned to a variable:**
```bash
txhash=4D53DBDEE2843BAF2E53A0D0AA0BF2E23BCD4AC0643996EBABEF3CDC5BB99F8A
```
```bash
CONTRACT_ADDR=$(okp4d q tx $txhash -o json | jq -r '.logs[].events[0].attributes[0].value')
```

<p align="center">
<img src='https://user-images.githubusercontent.com/83868103/231831622-b7247f91-efbe-4664-97a5-f4382b5d8006.png' alt='PRE-RELISE'  width=80% > 
</p>

___
### Execute

**We can store an object by providing its data in base64 encoded, we can pin the stored object to prevent it from being removed:**

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"store_object\":{\"data\": \"$(echo "$HOME/$LABEL.txt" | base64)\",\"pin\":true}}" \
    -y
```
**The resulting transaction hash is assigned to a variable:**
```bash
txhash=B9E2B23A0A57B53C86A4E31A7156407CFDF1B2640941C798F1F60B119304AC84
```
```bash
OBJECT_ID=$(okp4d q tx $txhash -o json | jq -r '.logs[].events[2].attributes[2].value')
```

<p align="center">
<img src='https://user-images.githubusercontent.com/83868103/231835702-912bbe54-6234-457b-9d04-58db5407269d.png' alt='PRE-RELISE'  width=80% > 
</p>

**The object id is stable as it is a hash, we can't store an object twice.**

____
### Pin
**With the following commands we can pin and unpin existing objects:**
```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"pin_object\":{\"id\": \"$OBJECT_ID\"}}" \
    -y
```

```python
Check Pinning
```
```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object\": {\"id\": \"$OBJECT_ID\"}}"
```

<p align="center">
<img src='https://user-images.githubusercontent.com/83868103/231836995-be436974-f3df-4d7d-8106-555f5519154d.png' alt='PRE-RELISE'  width=80% > 
</p>

___
### Unpin
```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"unpin_object\":{\"id\": \"$OBJECT_ID\"}}" \
    -y
```

```python
Check Unpinning
```
```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object\": {\"id\": \"$OBJECT_ID\"}}"
```

<p align="center">
<img src='https://user-images.githubusercontent.com/83868103/231838649-e2248d62-b40e-4089-83c8-6909a4d97e39.png' alt='PRE-RELISE'  width=80% > 
</p>

___
### Forget

**And if an object is not pinned, or pinned by the sender of transaction, we can remove it:**

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"forget_object\":{\"id\": \"$OBJECT_ID\"}}" \
    -y
```

```python
Query Object By ID
```
```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object\": {\"id\": \"$OBJECT_ID\"}}"
```

<p align="center">
<img src='https://user-images.githubusercontent.com/83868103/231843750-ff2feaff-30bd-4d35-9d40-8b6927c47948.png' alt='PRE-RELISE'  width=100% > 
</p>

```python
Query Object By Data
```
```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object_data\": {\"id\": \"$OBJECT_ID\"}}"
```

<p align="center">
<img src='https://user-images.githubusercontent.com/83868103/231844558-e1d4aaea-b274-4795-bc91-b55c1e8cb374.png' alt='PRE-RELISE'  width=70% > 
</p>

___

### Objectarium HASHS

___
### Query

**Query an object by its id:**

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object\": {\"id\": \"$OBJECT_ID\"}}"
```

**Or its data:**

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object_data\": {\"id\": \"$OBJECT_ID\"}}"
```

**We can also list the objects, eventually filtering on the object owner:**

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"objects\": {\"address\": \"$ADDRESS\"}}"
```

**And navigate in a cursor based pagination:**

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"objects\": {\"first\": 5, \"after\": \"32MUGxHoR66M4HT8ga7haKS6tLkJ1w5P4du6q3X9tZqvdSuSHNoUzwQCPwPyW8u5xLxso1Qx99GexVGfLGep1Wfv\"}}"
```

**We can also query object pins with the same cursor based pagination:**

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"object_pins\": {\"id\": \"$OBJECT_ID\", \"first\": 5, \"after\": \"32MUGxHoR66M4HT8ga7haKS6tLkJ1w5P4du6q3X9tZqvdSuSHNoUzwQCPwPyW8u5xLxso1Qx99GexVGfLGep1Wfv\"}}"
```
___
# Single source

This example aims to illustrate the most simple case of the `okp4-law-stone`: The law is composed of only one Prolog source program.

### The Program

The spirit here is to provide a `okp4-law-stone` smart contract instance providing rules similar in form to Dataspace governance rules.

You'll find in the [gov.pl](gov.pl) Prolog program some predicates defining the rules allowing to perform some typical Dataspaces actions.

The `can(Action, DID)` predicate will allow or not an action for a `did` (i.e. Decentralized Identifier), a `did` being expected to have the form: `did:key:${OKP4_ADDRESS}`. We can describe the action rules as follows:

- `change_governance`: Only the did admin can do it: `did:key:okp41p8u47en82gmzfm259y6z93r9qe63l25dfwwng6`;
- `exec_workflow`: Only a valid DID having a minimum spendable of `1000000uknow`;
- `create_dataset` Only a valid DID having a minimum spendable of `10000uknow`;
- `create_service` Only a valid DID having a minimum spendable of `100000uknow`;

### Instantiate

The instantiate will take as parameters the base64 encoded program and the address of a `okp4-objectarium` contract, on which the program will be stored and pinned to prevent its removal and thus ensure its availability:

```bash
okp4d tx wasm instantiate 3 \
    --label "$LABEL-single-source" \
    --from $ADDRESS \
    --admin $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    "{\"program\":\"$(cat $HOME/contracts/contracts/okp4-law-stone/examples/single-source/gov.pl | base64)\", \"storage_address\": \"$CONTRACT_ADDR\"}"
```


**You can retrieve the new `okp4-law-stone` smart contract address in the `_contract_address` instantiate attribute of the transaction.**

### Query

**By using the `Ask` query we can provide Prolog predicates to be evaluated againsts the underlying program:**

```bash
okp4d query wasm contract-state smart $CONTRACT_ADDR \
    "{\"ask\": {\"query\": \"can('change_governance', 'did:key:okp41p8u47en82gmzfm259y6z93r9qe63l25dfwwng6').\"}}"
```

### Break

**Only the smart contract admin can break the stone, if any.**

**The program stored in the `okp4-objectarium` smart contract will be removed, or at least un-pinned.**

**By breaking the stone, you will not be able to query it anymore.**

```bash
okp4d tx wasm execute $CONTRACT_ADDR \
    --from $ADDRESS \
    --gas 1000000 \
    --fees 2000uknow \
    '"break_stone"'
```
