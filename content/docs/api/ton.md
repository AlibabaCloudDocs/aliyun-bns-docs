# Ton

TON is focused on achieving widespread cross-chain interoperability, while operating in a highly scalable secure framework. TON is designed to process millions of transactions per second (TPS), with the goal of eventually reaching hundreds of millions of users moving forward.

TON Blockchain is designed as a distributed supercomputer, or “superserver,” intended to provide a variety of products and services to contribute to the development of the decentralized vision for the new internet.

In order for your Web3 application to interact with Ton — either by reading blockchain data or sending transactions to the network — it must connect to a Ton node. Developers interact with the blockchain using the methods provided by the API.

The API interaction follows the [JSON-RPC](https://www.jsonrpc.org/specification) which is a stateless, light-weight remote procedure call (RPC) protocol. It defines several data structures and the rules around their processing. It is transport agnostic in that the concepts can be used within the same process, over sockets, over HTTP, or in other message-passing environments. It uses JSON (RFC 4627) as data format.

## Methods supported

**Direct API**:

* [`estimateFee`](#estimatefee) — Estimate fees required for query processing. body, init-code andinit-data accepted in serialized format (b64-encoded)
* [`getAccountBalance`](#getaccountbalance) - Get balance of a given address
* [`getAddressInformation`](#getaddressinformation) - Get basic information about the address balance, code, data,last_transaction_id
* [`getAddressState`](#getaddressstate) - Get state of a given address. State can be either unitialized, active orfrozen
* [`getBlockHeader`](#getblockheader) - Get metadata of a given block
* [`getBlockTransactions`](#getblocktransactions) - Get transactions of the given block
* [`getConsensusBlock`](#getconsensusblock) - Get consensus block and its update timestamp
* [`getExtendedAddressInformation`](#getextendedaddressinformation) - Similar to [`getAddressInformation`](#getaddressinformation) but tries to parse additionalinformation for known contract types
* [`getMasterchainBlockSignatures`](#getmasterchainblocksignatures) - Get Masterchain Block Signatures
* [`getTokenData`](#gettokendata) - Get NFT or Jetton information
* [`runGetMethod`](#rungetmethod) - Run get method on smart contract
* [`sendMessage`](#sendmessage) - Send Message

**Indexer API**:

* [`getJettonBurns`](#getjettonburns) — Get Jetton Burns
* [`getJettonMasters`](#getjettonmasters) — Get Jetton Masters
* [`getJettonTransfers`](#getjettontransfers) — Get Jetton Transfers
* [`getJettonWallets`](#getjettonwallets) - Get Jetton Wallets
* [`getMasterchainInfo`](#getmasterchaininfo) - Get Masterchain Info
* [`getMessages`](#getmessages) - Get Messages
* [`getNftCollections`](#getnftcollections) - Get NFT Collections
* [`getNftItems`](#getnftitems) - Get NFT Items
* [`getNftTransfers`](#getnfttransfers) - Get NFT Transfers
* [`getTransactions`](#gettransactions) - Get TON Transactions

---

### `estimateFee`

> Estimate fees required for query processing. body, init-code andinit-data accepted in serialized format (b64-encoded).

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): identifier of target TON account in any form
    * `body` (string): messages for estimate fee
    * `ignore_chksig` (boolean): check if message signature matches address public key
    * `init_code` (string): b64-encoded boc-serialized cell with init-code
    * `init_data` (string): b64-encoded boc-serialized cell with init-data

#### Returns

  * `@extra` (string)
  * `@type` (string)
  * `destination_fees` (array; string)
  * `source_fees` (object):
    * `@type` (string)
    * `fwd_fee` (integer)
    * `gas_fee` (integer)
    * `in_fwd_fee` (integer)
    * `storage_fee` (integer)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "estimateFee",
      "params": {
        "address": "EQChncuh-0UAJcmcX7D4gmanDovwNNQXkKnv6tlpBZQ9nHek",
        "body": "te6ccgECBQEAARUAAkWIAWTtae+KgtbrX26Bep8JSq8lFLfGOoyGR/xwdjfvpvEaHg",
        "ignore_chksig": false,
        "init_code": "te6ccgECBQEAARUAAkWIAWTtae+KgtbrX26Bep8JSq8lFLfGOoyGR/xwdjfvpvEaHg",
        "init_data": "te6ccgECBQEAARUAAkWIAWTtae+KgtbrX26Bep8JSq8lFLfGOoyGR/xwdjfvpvEaHg"
      }
}'
```

### `getAccountBalance`

> Get balance of a given address.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): identifier of target TON account in any form

#### Returns

  * `result` (string)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getAccountBalance",
      "params": {
        "address": "EQChncuh-0UAJcmcX7D4gmanDovwNNQXkKnv6tlpBZQ9nHek"
      }
}'
```

#### Response example

```json
{
  "jsonrpc": "2.0",
  "result": "79941533476"
}
```

### `getAddressInformation`

> Get basic information about the address balance, code, data,last_transaction_id.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): identifier of target TON account in any form

#### Returns

  * `@extra` (string)
  * `@type` (string)
  * `balance` (string)
  * `block_id` (object):
    * `@type` (string)
    * `file_hash` (string)
    * `root_hash` (string)
    * `seqno` (integer)
    * `shard` (string)
    * `workchain` (integer)
  * `code` (string)
  * `data` (string)
  * `fronzen_hash` (string)
  * `last_transaction_id` (object):
    * `@type` (string)
    * `hash` (string)
    * `lt` (string)
  * `state` (string)
  * `sync_time` (integer)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getAddressInformation",
      "params": {
        "address": "EQChncuh-0UAJcmcX7D4gmanDovwNNQXkKnv6tlpBZQ9nHek"
      }
}'
```

#### Response example

```json
{
  "result": {
    "@extra": "1687338513.0129201:2:0.9501899250701279",
    "@type": "raw.fullAccountState",
    "balance": "809401535972",
    "block_id": {
      "@type": "ton.blockIdExt",
      "file_hash": "s6I65ivzwVkCLTCTVH0dIS7321rUFfx+4udx/9RRZB8=",
      "root_hash": "lV9RIaO7dQ01pfJhbzR5POMQ9uHgSqAAgcPpy4/K6qI=",
      "seqno": 30517690,
      "shard": "-9223372036854775808",
      "workchain": -1
    },
    "code": "te6cckEBAQEAcQAA3v8AIN0gggFMl7ohggEznLqxn3Gw7UTQ0x/THzHXC//jBOCk8mCDCNcYINMf0x/TH/gjE7vyY+1E0NMf0x/T/9FRMrryoVFEuvKiBPkBVBBV+RDyo/gAkyDXSpbTB9QC+wDo0QGkyMsfyx/L/8ntVBC9ba0=",
    "data": "te6cckEBAQEAKgAAUAAAAAYpqaMXUl8jsumwVsbvK5FBr1eiVrHpUrHZ8HRDfRo1lFx8lpd765yB",
    "frozen_hash": "",
    "last_transaction_id": {
      "@type": "internal.transactionId",
      "hash": "R7vI2AxqgpQQYxQaxZsQwtZXHxE6rw6mDNtKJ3LtPVM=",
      "lt": "34789408000007"
    },
    "state": "active",
    "sync_utime": 1687338490
  }
}
```

### `getAddressState`

> Get state of a given address. State can be either unitialized, active orfrozen.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): identifier of target TON account in any form

#### Returns

  * `result` (string)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getAddressState",
      "params": {
        "address": "EQChncuh-0UAJcmcX7D4gmanDovwNNQXkKnv6tlpBZQ9nHek"
      }
}'
```

#### Response example

```json
{
  "result": "active"
}
```

### `getBlockHeader`

> Get metadata of a given block.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `file_hash` (string): block file hash. Must not use with root_hash
    * `root_hash` (string): block root hash. Must not use with file_hash
    * `seqno` (integer): block seqno
    * `shard` (string): block shard id
    * `workchain` (integer)

#### Returns

  * `@type` (string)
  * `@extra` (string)
  * `after_merge` (boolean)
  * `after_split` (boolean)
  * `before_split` (boolean)
  * `catchain_seqno` (integer)
  * `end_lt` (string)
  * `flags` (integer)
  * `gen_utime` (integer)
  * `global_id` (integer)
  * `id` (object):
      * `@type` (string)
      * `file_hash` (string)
      * `root_hash` (string)
      * `seqno` (integer)
      * `shard` (string)
      * `workchain` (integer)
  * `is_key_block` (boolean)
  * `min_ref_mc_seqno` (integer)
  * `prev_blocks` (array; object):
      * `@type` (string)
      * `file_hash` (string)
      * `root_hash` (string)
      * `seqno` (integer)
      * `shard` (string)
      * `workchain` (integer)
  * `prev_key_block_seqno` (integer)
  * `start_lt` (string)
  * `validator_list_hash_short` (integer)
  * `version` (integer)
  * `vert_seqno` (integer)
  * `want_merge` (boolean)
  * `want_split` (boolean)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getBlockHeader",
      "params": {
        "file_hash": "iPYYhzx1oKbWLhzf+f6ILnazaLzGSynKvT6wLnS2aBc=",
        "root_hash": "3Cci3wvh2fUTb4vHInneLGEGPaV5huC0PbCN2ddMWAw=",
        "seqno": 38203530,
        "shard": "6000000000000000",
        "workchain": -1
      }
}'
```

#### Response example

```json
{
  "result": {
    "@extra": "1687338546.7723587:2:0.5271371713556018",
    "@type": "blocks.header",
    "after_merge": false,
    "after_split": false,
    "before_split": false,
    "catchain_seqno": 449608,
    "end_lt": "38636875000004",
    "flags": 1,
    "gen_utime": 1687271330,
    "global_id": -239,
    "id": {
      "@type": "ton.blockIdExt",
      "file_hash": "t81TFPL17RLgqteZsYf64yY2EX18p/V5f3Z9itK1DrA=",
      "root_hash": "2a8ZfAc+YN+hWDxtnlj+lsmPxDljA1ur8XVvL52UB2s=",
      "seqno": 30497145,
      "shard": "-9223372036854775808",
      "workchain": -1
    },
    "is_key_block": false,
    "min_ref_mc_seqno": 30497141,
    "prev_blocks": [
      {
        "@type": "ton.blockIdExt",
        "file_hash": "/XCWyXIZVy+Bg3AxI5km0IP6bnsmmbI9bSQDO09m3Lw=",
        "root_hash": "i84CdB9iTlC/rsy3kBG+RF3TTWIyG358LxHgaEbCxkA=",
        "seqno": 30497144,
        "shard": "-9223372036854775808",
        "workchain": -1
      }
    ],
    "prev_key_block_seqno": 30488948,
    "start_lt": "38636875000000",
    "validator_list_hash_short": 579715162,
    "version": 0,
    "vert_seqno": 1,
    "want_merge": true,
    "want_split": false
  }
}
```

### `getBlockTransactions`

> Get transactions of the given block

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `file_hash` (string): block file hash. Must not use with root_hash
    * `root_hash` (string): block root hash. Must not use with file_hash
    * `after_hash` (string): after block hash
    * `after_lt` (integer): after block lt
    * `count` (integer): block count
    * `seqno` (integer): block seqno
    * `shard` (string): block shard id
    * `workchain` (integer)

#### Returns

  * `@type` (string)
  * `@extra` (string)
  * `id` (object):
      * `@type` (string)
      * `file_hash` (string)
      * `root_hash` (string)
      * `seqno` (integer)
      * `shard` (string)
      * `workchain` (integer)
  * `incomplete` (boolean)
  * `req_count` (integer)
  * `transactions` (array; object):
    * `@type` (string)
    * `account` (string)
    * `hash` (string)
    * `lt` (string)
    * `mode` (integer)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getBlockTransactions",
      "params": {
        "after_hash": "k56mGTxZjKO/k70DvgBR8NvuRg1dqPHRWvagm9HJofY=",
        "after_lt": 46896908000000,
        "count": 40,
        "file_hash": "iPYYhzx1oKbWLhzf+f6ILnazaLzGSynKvT6wLnS2aBc=",
        "root_hash": "3Cci3wvh2fUTb4vHInneLGEGPaV5huC0PbCN2ddMWAw=",
        "seqno": 38203530,
        "shard": "6000000000000000",
        "workchain": -1
      }
}'
```

#### Response example

```json
{
  "result": {
    "@extra": "1687338546.391785:11:0.37351974452237247",
    "@type": "blocks.transactions",
    "id": {
      "@type": "ton.blockIdExt",
      "file_hash": "t81TFPL17RLgqteZsYf64yY2EX18p/V5f3Z9itK1DrA=",
      "root_hash": "2a8ZfAc+YN+hWDxtnlj+lsmPxDljA1ur8XVvL52UB2s=",
      "seqno": 30497145,
      "shard": "-9223372036854775808",
      "workchain": -1
    },
    "incomplete": false,
    "req_count": 5,
    "transactions": [
      {
        "@type": "blocks.shortTxId",
        "account": "-1:3333333333333333333333333333333333333333333333333333333333333333",
        "hash": "qBth3wIytHqavKianhcpmnFlwHIF5TXV3nXZPgjJ9Dc=",
        "lt": "38636875000001",
        "mode": 135
      },
      {
        "@type": "blocks.shortTxId",
        "account": "-1:3333333333333333333333333333333333333333333333333333333333333333",
        "hash": "w0de1XEy/dYChgNYy0w099SltwGrVvP4gf372c+RUZo=",
        "lt": "38636875000002",
        "mode": 135
      },
      {
        "@type": "blocks.shortTxId",
        "account": "-1:5555555555555555555555555555555555555555555555555555555555555555",
        "hash": "5I6TUoKfhtpaqFWzEfZ3v1HUd1fVLPORb8gVRSuqsGQ=",
        "lt": "38636875000003",
        "mode": 135
      }
    ]
  }
}
```

### `getConsensusBlock`

> Get consensus block and its update timestamp.

#### Parameters

#### Returns

  * `consensus_block` (integer)
  * `timestamp` (number)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getConsensusBlock",
      "params": ""
}'
```

#### Response example

```json
{
  "result": {
    "consensus_block": 30517698,
    "timestamp": 1687338534.241151
  }
}
```

### `getExtendedAddressInformation`

> Similar to [`getAddressInformation`](#getaddressinformation) but tries to parse additionalinformation for known contract types.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): identifier of target TON account in any form

#### Returns

  * `@extra` (string)
  * `@type` (string)
  * `account_state` (object):
    * `@type` (string)
    * `code` (string)
    * `data` (string)
    * `frozen_hash` (string)
  * `address` (object):
    * `@type` (string)
    * `account_address` (string)
  * `balance` (string)
  * `block_id` (object):
    * `@type` (string)
    * `file_hash` (string)
    * `root_hash` (string)
    * `seqno` (integer)
    * `shard` (string)
    * `workchain` (integer)
  * `code` (string)
  * `data` (string)
  * `fronzen_hash` (string)
  * `last_transaction_id` (object):
    * `@type` (string)
    * `hash` (string)
    * `lt` (string)
  * `revision` (integer)
  * `sync_time` (integer)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getExtendedAddressInformation",
      "params": {
        "address": "EQChncuh-0UAJcmcX7D4gmanDovwNNQXkKnv6tlpBZQ9nHek"
      }
}'
```

#### Response example

```json
{
  "ok": true,
  "result": {
    "@extra": "1687338514.115839:6:0.5886804474003975",
    "@type": "fullAccountState",
    "account_state": {
      "@type": "wallet.v3.accountState",
      "seqno": 6,
      "wallet_id": "698983191"
    },
    "address": {
      "@type": "accountAddress",
      "account_address": "EQAFPsHznqgqPUZQVyUBmWxpNwReAIuepKo_BjLiS-C05XB_"
    },
    "balance": "809401535972",
    "block_id": {
      "@type": "ton.blockIdExt",
      "file_hash": "s6I65ivzwVkCLTCTVH0dIS7321rUFfx+4udx/9RRZB8=",
      "root_hash": "lV9RIaO7dQ01pfJhbzR5POMQ9uHgSqAAgcPpy4/K6qI=",
      "seqno": 30517690,
      "shard": "-9223372036854775808",
      "workchain": -1
    },
    "last_transaction_id": {
      "@type": "internal.transactionId",
      "hash": "R7vI2AxqgpQQYxQaxZsQwtZXHxE6rw6mDNtKJ3LtPVM=",
      "lt": "34789408000007"
    },
    "revision": 2,
    "sync_utime": 1687338490
  }
}
```

### `getMasterchainBlockSignatures`

> Get Masterchain Block Signatures.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `seqno` (integer; required): block seqno

#### Returns

  * `@type` (string)
  * `@extra` (string)
  * `id` (object):
    * `@type` (string)
    * `file_hash` (string)
    * `root_hash` (string)
    * `seqno` (integer)
    * `shard` (string)
    * `workchain` (integer)
  * `signatures` (object):
    * `@type` (string)
    * `node_id_short` (string)
    * `signature` (array; string)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getMasterchainBlockSignatures",
      "params": {
        "seqno": 38203530
      }
}'
```

#### Response example

```json
{
  "ok": true,
  "result": {
    "@extra": "1687338543.6958232:6:0.19692230851537695",
    "@type": "blocks.blockSignatures",
    "id": {
      "@type": "ton.blockIdExt",
      "file_hash": "t81TFPL17RLgqteZsYf64yY2EX18p/V5f3Z9itK1DrA=",
      "root_hash": "2a8ZfAc+YN+hWDxtnlj+lsmPxDljA1ur8XVvL52UB2s=",
      "seqno": 30497145,
      "shard": "-9223372036854775808",
      "workchain": -1
    },
    "signatures": [
      {
        "@type": "blocks.signature",
        "node_id_short": "/sZBm51kgjzTPFF6yRy3Es2U4UTw8Wl1vOSaTaGBQUY=",
        "signature": "vVWT6U7M3nqrRr+zfmtg5TNI2A82Hdu8VMTej3P/bI4pMbRrQ8QHs57BrK6KeYes3vOyShMAPPCQZMSGPLbBDg=="
      },
      {
        "@type": "blocks.signature",
        "node_id_short": "3Gtnxj1TpScX0DLnUs3G6sNqsuZt8AVA/870EyMPAE8=",
        "signature": "LBpEGy21IyiJ84SIPWGEAkp2VIhkyILwe9RR4WVhtiedC5apiZyTK+f2pTGNoylD5NCpo6dCywF+jM+0qDkMCQ=="
      },
      {
        "@type": "blocks.signature",
        "node_id_short": "wTXXj2aLhQvJxpy6KqiBL/xvbIMtQ5loLBVO8Z9q9Ow=",
        "signature": "fGSCMmxb6FbsqXAJ04/E79eKBvvSZ5crvERYnDHr4/HkK4/Y9MVfCGz88GSSxJBXvtkDNJY/sD6ZQU84VMFlBw=="
      }
    ]
  }
}
```

### `getTokenData`

> Get NFT or Jetton information.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): identifier of target TON account in any form

#### Returns

  * `admin_address` (string)
  * `balance` (integer)
  * `collection_address` (string)
  * `collection_content` (object):
    * `type` (string)
    * `data` (string)
  * `content` (object):
    * `data` (string)
    * `domain` (string)
    * `type` (string)
  * `contract_type` (string)
  * `index` (integer)
  * `init` (boolean)
  * `jetton` (string)
  * `jetton_content` (object):
    * `type` (string)
    * `data` (string)
  * `jetton_wallet_code` (string)
  * `mintable` (boolean)
  * `next_item_index` (integer)
  * `owner` (string)
  * `owner_address` (string)
  * `total_supply` (integer)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "getTokenData",
      "params": {
        "address": "EQChncuh-0UAJcmcX7D4gmanDovwNNQXkKnv6tlpBZQ9nHek"
      }
}'
```

#### Response example

```json
{
  "result": {
    "next_item_index": 10000,
    "collection_content": {
      "type": "offchain",
      "data": "https://nft.ton.diamonds/diamonds.json"
    },
    "owner_address": "EQDsP4js-X1VVS7mBZAuoeXvKcvOYlkpsdELBHwJOez07ZTW",
    "contract_type": "nft_collection"
  }
}
```

### `runGetMethod`

> Run get method on smart contract.

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): identifier of target TON account in any form
    * `method` (string): method name or method id
    * `stack` (array; string): parameters from method

#### Returns

  * `@type` (string)
  * `@extra` (string)
  * `exit_code` (integer)
  * `gas_used` (integer)
  * `stack` (array; string)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "runGetMethod",
      "params": {
        "address": "EQChncuh-0UAJcmcX7D4gmanDovwNNQXkKnv6tlpBZQ9nHek",
        "method": "get_jetton_data",
        "stack": [
          "string"
        ]
      }
}'
```

#### Response example

```json
{
  "result": {
    "@extra": "string",
    "@type": "string",
    "exit_code": 0,
    "gas_used": 0,
    "stack": [
      "string"
    ]
  }
}
```

### `sendMessage`

> Send message

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `boc` (string; required): base64 boc

#### Returns

  * `result` (string)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "sendMessage",
      "params": {
        "boc": "te6ccgECBQEAARUAAkWIAWTtae+KgtbrX26Bep8JSq8lFLfGOoyGR/xwdjfvpvEaHg"
      }
}'
```

#### Response example

```json
{
  "result": "string"
}
```

### `getJettonBurns`

> Get Jetton Burns

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): account address. Must be sent in hex, base64 and base64url forms
    * `end_lt` (integer): transaction lt, must be sent with start_lt
    * `end_utime` (integer): query transactions with generation UTC timestamp, must be sent with start_utime
    * `jetton_master` (string): jetton master address. Must be sent in hex, base64 and base64url forms
    * `jetton_wallet` (string): jetton wallet address. Must be sent in hex, base64 and base64url forms
    * `limit` (integer)
    * `offset` (integer): skip first N rows. Use with limit to batch read
    * `sort` (string)
    * `start_lt` (integer)
    * `start_utime` (integer)

#### Returns

  * `custom_payload` (string)
  * `jetton_master` (string)
  * `owner` (string)
  * `query_id` (string)
  * `response_destination` (string)
  * `transaction_hash` (string)
  * `transaction_lt` (string)
  * `transaction_now` (integer)

#### Request example

```shell
curl -X POST https://bns.aliyuncs.com/v1/ton/mainnet/{apikey} \
-H 'Content-Type: application/json' \
-d '{
      "id": 1,
      "jsonrpc": "2.0",
      "method": "sendMessage",
      "params": {
        "address": "EQCtgkjNoQrCtadqxDdJMmGQu8WyeKd17cGFiQKl58vqZCst",
        "end_lt": 46220646000001,
        "end_utime": 1714547740,
        "jetton_master": "EQBHR0GWlW56tAGnFV-ycqN1vp0IOaT4rMO2Sp45inVOWX3p",
        "jetton_wallet": "EQCxE6mUtQJKFnGfaROTKOt1lZbDiiX1kCixRv7Nw2Id_sDs",
        "limit": 256,
        "offset": 0,
        "sort": "ASC",
        "start_lt": 46220646000001,
        "start_utime": 1714547740
      }
}'
```

#### Response example

```json
{
  "result": [
    {
      "amount": "string",
      "custom_payload": "string",
      "jetton_master": "string",
      "jetton_wallet": "string",
      "owner": "string",
      "query_id": "string",
      "response_destination": "string",
      "transaction_hash": "string",
      "transaction_lt": "string",
      "transaction_now": 0
    }
  ]
}
```

### `getJettonMasters`

> Get Jetton Masters

#### Parameters
  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string): account address. Must be sent in hex, base64 and base64url forms
    * `admin_address` (string): account address. Must be sent in hex, base64 and base64url forms
    * `limit` (integer)
    * `offset` (integer)

#### Returns

  * `address` (string)
  * `admin_address` (string)
  * `code_hash` (string)
  * `data_hash` (string)
  * `jetton_content` (object):
    * `decimals` (string)
    * `description` (string)
    * `image` (string)
    * `name` (string)
    * `symbol` (string)
    * `uri` (string)
  * `jetton_wallet_code_hash` (string)
  * `last_transaction_lt` (string)
  * `mintable` (boolean)
  * `total_supply` (string)

### `getJettonTransfers`

> Get Jetton Transfers

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): account address. Must be sent in hex, base64 and base64url forms
    * `direction` (string)
    * `end_lt` (integer): transaction lt, must be sent with start_lt
    * `end_utime` (integer): query transactions with generation UTC timestamp, must be sent with start_utime
    * `jetton_master` (string): jetton master address. Must be sent in hex, base64 and base64url forms
    * `jetton_wallet` (string): jetton wallet address. Must be sent in hex, base64 and base64url forms
    * `limit` (integer)
    * `offset` (integer): skip first N rows. Use with limit to batch read
    * `sort` (string)
    * `start_lt` (integer)
    * `start_utime` (integer)

#### Returns

  * `amount` (string)
  * `custom_payload` (string)
  * `destination` (string)
  * `forward_payload` (string)
  * `forward_ton_amount` (string)
  * `jetton_master` (string)
  * `query_id` (string)
  * `response_destination` (string)
  * `source` (string)
  * `source_wallet` (string)
  * `transaction_hash` (string)
  * `transaction_lt` (string)
  * `transaction_now` (integer)

### `getJettonWallets`

> Get Jetton Wallets

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request
  * `params` (object; required):
    * `address` (string; required): account address. Must be sent in hex, base64 and base64url forms
    * `jetton_address` (string; required): jetton master. Must be sent in hex, base64 and base64url forms
    * `limit` (integer)
    * `offset` (integer): skip first N rows. Use with limit to batch read
    * `owner_address` (string): address of Jetton wallet's owner. Must be sent in hex, base64 and base64url forms

#### Returns

  * `address` (string)
  * `balance` (string)
  * `code_hash` (string)
  * `data_hash` (string)
  * `jetton` (string)
  * `last_transaction_lt` (string)
  * `owner` (string)

### `getMasterchainInfo`

> Get Masterchain Info

#### Parameters

  * `id` (integer; required): a request ID (example: 1)
  * `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0)
  * `method` (string; required): a method used for the request

#### Returns

  * `first` (object):
    * `after_merge` (boolean)
    * `after_split` (boolean)
    * `before_split` (boolean)
    * `created_by` (string)
    * `end_lt` (string)
    * `file_hash` (string)
    * `flags` (integer)
    * `gen_catchain_seqno` (integer)
    * `gen_utime` (string)
    * `global_id` (integer)
    * `key_block` (boolean)
    * `master_ref_seqno` (integer)
    * `masterchain_block_ref` (object):
      * `seqno` (integer)
      * `shard` (string)
      * `workchain` (integer)
    * `min_ref_mc_seqno` (integer)
    * `prev_key_block_seqno` (integer)
    * `rand_seed` (string)
    * `root_hash` (string)
    * `seqno` (integer)
    * `start_lt` (string)
    * `tx_count` (integer)
    * `validator_list_hash_short` (integer)
    * `version` (integer)
    * `vert_seqno` (integer)
    * `vert_seqno_incr` (integer)
    * `want_split` (boolean)
    * `workchain` (integer)
  * `last` (object):
    * `after_merge` (boolean)
    * `after_split` (boolean)
    * `before_split` (boolean)
    * `created_by` (string)
    * `end_lt` (string)
    * `file_hash` (string)
    * `flags` (integer)
    * `gen_catchain_seqno` (integer)
    * `gen_utime` (string)
    * `global_id` (integer)
    * `key_block` (boolean)
    * `master_ref_seqno` (integer)
    * `masterchain_block_ref` (object):
      * `seqno` (integer)
      * `shard` (string)
      * `workchain` (integer)
    * `min_ref_mc_seqno` (integer)
    * `prev_key_block_seqno` (integer)
    * `rand_seed` (string)
    * `root_hash` (string)
    * `seqno` (integer)
    * `start_lt` (string)
    * `tx_count` (integer)
    * `validator_list_hash_short` (integer)
    * `version` (integer)
    * `vert_seqno` (integer)
    * `vert_seqno_incr` (integer)
    * `want_split` (boolean)
    * `workchain` (integer)

### `getMessages`

> Get Messages

### `getNftCollections`

> Get NFT Collections

### `getNftItems`

> Get NFT Items

### `getNftTransfers`

> Get NFT Transfers

### `getTransactions`

> Get TON Transactions
