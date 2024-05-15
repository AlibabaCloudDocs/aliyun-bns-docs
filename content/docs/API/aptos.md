---
weight: 2
title: Aptos API
---

# Aptos Node API

> Version 1.2.0

The Aptos Node API is a RESTful API for client applications to interact with the Aptos blockchain.

## Path Table

| Method | Path | Description |
| --- | --- | --- |
| GET | [/accounts/{address}](#getaccountsaddress) | Get account |
| GET | [/accounts/{address}/resources](#getaccountsaddressresources) | Get account resources |
| GET | [/accounts/{address}/modules](#getaccountsaddressmodules) | Get account modules |
| GET | [/spec](#getspec) | Show OpenAPI explorer |
| GET | [/-/healthy](#get-healthy) | Check basic node health |
| GET | [/blocks/by_height/{block_height}](#getblocksby_heightblock_height) | Get blocks by height |
| GET | [/blocks/by_version/{version}](#getblocksby_versionversion) | Get blocks by version |
| GET | [/accounts/{address}/events/{creation_number}](#getaccountsaddresseventscreation_number) | Get events by creation number |
| GET | [/accounts/{address}/events/{event_handle}/{field_name}](#getaccountsaddresseventsevent_handlefield_name) | Get events by event handle |
| GET | [/](#get) | Get ledger info |
| GET | [/accounts/{address}/resource/{resource_type}](#getaccountsaddressresourceresource_type) | Get account resource |
| GET | [/accounts/{address}/module/{module_name}](#getaccountsaddressmodulemodule_name) | Get account module |
| POST | [/tables/{table_handle}/item](#posttablestable_handleitem) | Get table item |
| POST | [/tables/{table_handle}/raw_item](#posttablestable_handleraw_item) | Get raw table item |
| GET | [/transactions](#gettransactions) | Get transactions |
| POST | [/transactions](#posttransactions) | Submit transaction |
| GET | [/transactions/by_hash/{txn_hash}](#gettransactionsby_hashtxn_hash) | Get transaction by hash |
| GET | [/transactions/wait_by_hash/{txn_hash}](#gettransactionswait_by_hashtxn_hash) | Wait for transaction by hash |
| GET | [/transactions/by_version/{txn_version}](#gettransactionsby_versiontxn_version) | Get transaction by version |
| GET | [/accounts/{address}/transactions](#getaccountsaddresstransactions) | Get account transactions |
| POST | [/transactions/batch](#posttransactionsbatch) | Submit batch transactions |
| POST | [/transactions/simulate](#posttransactionssimulate) | Simulate transaction |
| POST | [/transactions/encode_submission](#posttransactionsencode_submission) | Encode submission |
| GET | [/estimate_gas_price](#getestimate_gas_price) | Estimate gas price |
| POST | [/view](#postview) | Execute view function of a module |

## Reference Table

| Name | Path | Description |
| --- | --- | --- |
| AccountData | [#/components/schemas/AccountData](#componentsschemasaccountdata) | Account data

A simplified version of the onchain Account resource |
| AccountSignature | [#/components/schemas/AccountSignature](#componentsschemasaccountsignature) | Account signature scheme

The account signature scheme allows you to have two types of accounts:

1. A single Ed25519 key account, one private key
2. A k-of-n multi-Ed25519 key account, multiple private keys, such that k-of-n must sign a transaction.
3. A single Secp256k1Ecdsa key account, one private key |
| AccountSignature_Ed25519Signature | [#/components/schemas/AccountSignature_Ed25519Signature](#componentsschemasaccountsignature_ed25519signature) |  |
| AccountSignature_MultiEd25519Signature | [#/components/schemas/AccountSignature_MultiEd25519Signature](#componentsschemasaccountsignature_multied25519signature) |  |
| AccountSignature_MultiKeySignature | [#/components/schemas/AccountSignature_MultiKeySignature](#componentsschemasaccountsignature_multikeysignature) |  |
| AccountSignature_SingleKeySignature | [#/components/schemas/AccountSignature_SingleKeySignature](#componentsschemasaccountsignature_singlekeysignature) |  |
| Address | [#/components/schemas/Address](#componentsschemasaddress) | A hex encoded 32 byte Aptos account address.

This is represented in a string as a 64 character hex string, sometimes
shortened by stripping leading 0s, and adding a 0x.

For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
 |
| AptosError | [#/components/schemas/AptosError](#componentsschemasaptoserror) | This is the generic struct we use for all API errors, it contains a string
message and an Aptos API specific error code. |
| AptosErrorCode | [#/components/schemas/AptosErrorCode](#componentsschemasaptoserrorcode) | These codes provide more granular error information beyond just the HTTP
status code of the response. |
| Block | [#/components/schemas/Block](#componentsschemasblock) | A Block with or without transactions

This contains the information about a transactions along with
associated transactions if requested |
| BlockMetadataTransaction | [#/components/schemas/BlockMetadataTransaction](#componentsschemasblockmetadatatransaction) | A block metadata transaction

This signifies the beginning of a block, and contains information
about the specific block |
| DecodedTableData | [#/components/schemas/DecodedTableData](#componentsschemasdecodedtabledata) | Decoded table data |
| DeleteModule | [#/components/schemas/DeleteModule](#componentsschemasdeletemodule) | Delete a module |
| DeleteResource | [#/components/schemas/DeleteResource](#componentsschemasdeleteresource) | Delete a resource |
| DeleteTableItem | [#/components/schemas/DeleteTableItem](#componentsschemasdeletetableitem) | Delete a table item |
| DeletedTableData | [#/components/schemas/DeletedTableData](#componentsschemasdeletedtabledata) | Deleted table data |
| DeprecatedModuleBundlePayload | [#/components/schemas/DeprecatedModuleBundlePayload](#componentsschemasdeprecatedmodulebundlepayload) |  |
| DirectWriteSet | [#/components/schemas/DirectWriteSet](#componentsschemasdirectwriteset) |  |
| Ed25519Signature | [#/components/schemas/Ed25519Signature](#componentsschemased25519signature) | A single Ed25519 signature |
| EncodeSubmissionRequest | [#/components/schemas/EncodeSubmissionRequest](#componentsschemasencodesubmissionrequest) | Request to encode a submission |
| EntryFunctionId | [#/components/schemas/EntryFunctionId](#componentsschemasentryfunctionid) | Entry function id is string representation of a entry function defined on-chain.

Format: `{address}::{module name}::{function name}`

Both `module name` and `function name` are case-sensitive.
 |
| EntryFunctionPayload | [#/components/schemas/EntryFunctionPayload](#componentsschemasentryfunctionpayload) | Payload which runs a single entry function |
| Event | [#/components/schemas/Event](#componentsschemasevent) | An event from a transaction |
| EventGuid | [#/components/schemas/EventGuid](#componentsschemaseventguid) |  |
| FeePayerSignature | [#/components/schemas/FeePayerSignature](#componentsschemasfeepayersignature) | Fee payer signature for fee payer transactions

This allows you to have transactions across multiple accounts and with a fee payer |
| GasEstimation | [#/components/schemas/GasEstimation](#componentsschemasgasestimation) | Struct holding the outputs of the estimate gas API |
| GenesisPayload | [#/components/schemas/GenesisPayload](#componentsschemasgenesispayload) | The writeset payload of the Genesis transaction |
| GenesisPayload_WriteSetPayload | [#/components/schemas/GenesisPayload_WriteSetPayload](#componentsschemasgenesispayload_writesetpayload) |  |
| GenesisTransaction | [#/components/schemas/GenesisTransaction](#componentsschemasgenesistransaction) | The genesis transaction

This only occurs at the genesis transaction (version 0) |
| HashValue | [#/components/schemas/HashValue](#componentsschemashashvalue) |  |
| HealthCheckSuccess | [#/components/schemas/HealthCheckSuccess](#componentsschemashealthchecksuccess) | Representation of a successful healthcheck |
| HexEncodedBytes | [#/components/schemas/HexEncodedBytes](#componentsschemashexencodedbytes) | All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
two hex digits per byte.

Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
 |
| IdentifierWrapper | [#/components/schemas/IdentifierWrapper](#componentsschemasidentifierwrapper) |  |
| IndexResponse | [#/components/schemas/IndexResponse](#componentsschemasindexresponse) | The struct holding all data returned to the client by the
index endpoint (i.e., GET "/").  Only for responding in JSON |
| IndexedSignature | [#/components/schemas/IndexedSignature](#componentsschemasindexedsignature) |  |
| MoveAbility | [#/components/schemas/MoveAbility](#componentsschemasmoveability) |  |
| MoveFunction | [#/components/schemas/MoveFunction](#componentsschemasmovefunction) | Move function |
| MoveFunctionGenericTypeParam | [#/components/schemas/MoveFunctionGenericTypeParam](#componentsschemasmovefunctiongenerictypeparam) | Move function generic type param |
| MoveFunctionVisibility | [#/components/schemas/MoveFunctionVisibility](#componentsschemasmovefunctionvisibility) | Move function visibility |
| MoveModule | [#/components/schemas/MoveModule](#componentsschemasmovemodule) | A Move module |
| MoveModuleBytecode | [#/components/schemas/MoveModuleBytecode](#componentsschemasmovemodulebytecode) | Move module bytecode along with it's ABI |
| MoveModuleId | [#/components/schemas/MoveModuleId](#componentsschemasmovemoduleid) | Move module id is a string representation of Move module.

Format: `{address}::{module name}`

`address` should be hex-encoded 32 byte account address that is prefixed with `0x`.

Module name is case-sensitive.
 |
| MoveResource | [#/components/schemas/MoveResource](#componentsschemasmoveresource) | A parsed Move resource |
| MoveScriptBytecode | [#/components/schemas/MoveScriptBytecode](#componentsschemasmovescriptbytecode) | Move script bytecode |
| MoveStruct | [#/components/schemas/MoveStruct](#componentsschemasmovestruct) | A move struct |
| MoveStructField | [#/components/schemas/MoveStructField](#componentsschemasmovestructfield) | Move struct field |
| MoveStructGenericTypeParam | [#/components/schemas/MoveStructGenericTypeParam](#componentsschemasmovestructgenerictypeparam) | Move generic type param |
| MoveStructTag | [#/components/schemas/MoveStructTag](#componentsschemasmovestructtag) | String representation of a MoveStructTag (on-chain Move struct type). This exists so you
can specify MoveStructTags as path / query parameters, e.g. for get_events_by_event_handle.

It is a combination of:
  1. `move_module_address`, `module_name` and `struct_name`, all joined by `::`
  2. `struct generic type parameters` joined by `, `

Examples:
  * `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>`
  * `0x1::account::Account`

Note:
  1. Empty chars should be ignored when comparing 2 struct tag ids.
  2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).

See [doc](https://aptos.dev/concepts/accounts) for more details.
 |
| MoveStructValue | [#/components/schemas/MoveStructValue](#componentsschemasmovestructvalue) | This is a JSON representation of some data within an account resource. More specifically,
it is a map of strings to arbitrary JSON values / objects, where the keys are top level
fields within the given resource.

To clarify, you might query for 0x1::account::Account and see the example data.

Move `bool` type value is serialized into `boolean`.

Move `u8`, `u16` and `u32` type value is serialized into `integer`.

Move `u64`, `u128` and `u256` type value is serialized into `string`.

Move `address` type value (32 byte Aptos account address) is serialized into a HexEncodedBytes string.
For example:
  - `0x1`
  - `0x1668f6be25668c1a17cd8caf6b8d2f25`

Move `vector` type value is serialized into `array`, except `vector<u8>` which is serialized into a
HexEncodedBytes string with `0x` prefix.
For example:
  - `vector<u64>{255, 255}` => `["255", "255"]`
  - `vector<u8>{255, 255}` => `0xffff`

Move `struct` type value is serialized into `object` that looks like this (except some Move stdlib types, see the following section):
  ```json
  {
    field1_name: field1_value,
    field2_name: field2_value,
    ......
  }
  ```

For example:
  `{ "created": "0xa550c18", "role_id": "0" }`

**Special serialization for Move stdlib types**:
  - [0x1::string::String](https://github.com/aptos-labs/aptos-core/blob/main/language/move-stdlib/docs/ascii.md)
    is serialized into `string`. For example, struct value `0x1::string::String{bytes: b"Hello World!"}`
    is serialized as `"Hello World!"` in JSON.
 |
| MoveType | [#/components/schemas/MoveType](#componentsschemasmovetype) | String representation of an on-chain Move type tag that is exposed in transaction payload.
    Values:
      - bool
      - u8
      - u16
      - u32
      - u64
      - u128
      - u256
      - address
      - signer
      - vector: `vector<{non-reference MoveTypeId}>`
      - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`

    Vector type value examples:
      - `vector<u8>`
      - `vector<vector<u64>>`
      - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`

    Struct type value examples:
      - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
      - `0x1::account::Account`

    Note:
      1. Empty chars should be ignored when comparing 2 struct tag ids.
      2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
 |
| MoveValue | [#/components/schemas/MoveValue](#componentsschemasmovevalue) | An enum of the possible Move value types |
| MultiAgentSignature | [#/components/schemas/MultiAgentSignature](#componentsschemasmultiagentsignature) | Multi agent signature for multi agent transactions

This allows you to have transactions across multiple accounts |
| MultiEd25519Signature | [#/components/schemas/MultiEd25519Signature](#componentsschemasmultied25519signature) | A Ed25519 multi-sig signature

This allows k-of-n signing for a transaction |
| MultiKeySignature | [#/components/schemas/MultiKeySignature](#componentsschemasmultikeysignature) | A multi key signature |
| MultisigPayload | [#/components/schemas/MultisigPayload](#componentsschemasmultisigpayload) | A multisig transaction that allows an owner of a multisig account to execute a pre-approved
transaction as the multisig account. |
| MultisigTransactionPayload | [#/components/schemas/MultisigTransactionPayload](#componentsschemasmultisigtransactionpayload) |  |
| MultisigTransactionPayload_EntryFunctionPayload | [#/components/schemas/MultisigTransactionPayload_EntryFunctionPayload](#componentsschemasmultisigtransactionpayload_entryfunctionpayload) |  |
| PendingTransaction | [#/components/schemas/PendingTransaction](#componentsschemaspendingtransaction) | A transaction waiting in mempool |
| PublicKey | [#/components/schemas/PublicKey](#componentsschemaspublickey) |  |
| PublicKey_string(HexEncodedBytes) | [#/components/schemas/PublicKey_string(HexEncodedBytes)](#componentsschemaspublickey_stringhexencodedbytes) |  |
| RawTableItemRequest | [#/components/schemas/RawTableItemRequest](#componentsschemasrawtableitemrequest) | Table Item request for the GetTableItemRaw API |
| RoleType | [#/components/schemas/RoleType](#componentsschemasroletype) |  |
| ScriptPayload | [#/components/schemas/ScriptPayload](#componentsschemasscriptpayload) | Payload which runs a script that can run multiple functions |
| ScriptWriteSet | [#/components/schemas/ScriptWriteSet](#componentsschemasscriptwriteset) |  |
| Signature | [#/components/schemas/Signature](#componentsschemassignature) |  |
| Signature_string(HexEncodedBytes) | [#/components/schemas/Signature_string(HexEncodedBytes)](#componentsschemassignature_stringhexencodedbytes) |  |
| SingleKeySignature | [#/components/schemas/SingleKeySignature](#componentsschemassinglekeysignature) | A single key signature |
| StateCheckpointTransaction | [#/components/schemas/StateCheckpointTransaction](#componentsschemasstatecheckpointtransaction) | A state checkpoint transaction |
| StateKeyWrapper | [#/components/schemas/StateKeyWrapper](#componentsschemasstatekeywrapper) | Representation of a StateKey as a hex string. This is used for cursor based pagination.
 |
| SubmitTransactionRequest | [#/components/schemas/SubmitTransactionRequest](#componentsschemassubmittransactionrequest) | A request to submit a transaction

This requires a transaction and a signature of it |
| TableItemRequest | [#/components/schemas/TableItemRequest](#componentsschemastableitemrequest) | Table Item request for the GetTableItem API |
| Transaction | [#/components/schemas/Transaction](#componentsschemastransaction) | Enum of the different types of transactions in Aptos |
| TransactionPayload | [#/components/schemas/TransactionPayload](#componentsschemastransactionpayload) | An enum of the possible transaction payloads |
| TransactionPayload_DeprecatedModuleBundlePayload | [#/components/schemas/TransactionPayload_DeprecatedModuleBundlePayload](#componentsschemastransactionpayload_deprecatedmodulebundlepayload) |  |
| TransactionPayload_EntryFunctionPayload | [#/components/schemas/TransactionPayload_EntryFunctionPayload](#componentsschemastransactionpayload_entryfunctionpayload) |  |
| TransactionPayload_MultisigPayload | [#/components/schemas/TransactionPayload_MultisigPayload](#componentsschemastransactionpayload_multisigpayload) |  |
| TransactionPayload_ScriptPayload | [#/components/schemas/TransactionPayload_ScriptPayload](#componentsschemastransactionpayload_scriptpayload) |  |
| TransactionSignature | [#/components/schemas/TransactionSignature](#componentsschemastransactionsignature) | An enum representing the different transaction signatures available |
| TransactionSignature_AccountSignature | [#/components/schemas/TransactionSignature_AccountSignature](#componentsschemastransactionsignature_accountsignature) |  |
| TransactionSignature_Ed25519Signature | [#/components/schemas/TransactionSignature_Ed25519Signature](#componentsschemastransactionsignature_ed25519signature) |  |
| TransactionSignature_FeePayerSignature | [#/components/schemas/TransactionSignature_FeePayerSignature](#componentsschemastransactionsignature_feepayersignature) |  |
| TransactionSignature_MultiAgentSignature | [#/components/schemas/TransactionSignature_MultiAgentSignature](#componentsschemastransactionsignature_multiagentsignature) |  |
| TransactionSignature_MultiEd25519Signature | [#/components/schemas/TransactionSignature_MultiEd25519Signature](#componentsschemastransactionsignature_multied25519signature) |  |
| Transaction_BlockMetadataTransaction | [#/components/schemas/Transaction_BlockMetadataTransaction](#componentsschemastransaction_blockmetadatatransaction) |  |
| Transaction_GenesisTransaction | [#/components/schemas/Transaction_GenesisTransaction](#componentsschemastransaction_genesistransaction) |  |
| Transaction_PendingTransaction | [#/components/schemas/Transaction_PendingTransaction](#componentsschemastransaction_pendingtransaction) |  |
| Transaction_StateCheckpointTransaction | [#/components/schemas/Transaction_StateCheckpointTransaction](#componentsschemastransaction_statecheckpointtransaction) |  |
| Transaction_UserTransaction | [#/components/schemas/Transaction_UserTransaction](#componentsschemastransaction_usertransaction) |  |
| Transaction_ValidatorTransaction | [#/components/schemas/Transaction_ValidatorTransaction](#componentsschemastransaction_validatortransaction) |  |
| TransactionsBatchSingleSubmissionFailure | [#/components/schemas/TransactionsBatchSingleSubmissionFailure](#componentsschemastransactionsbatchsinglesubmissionfailure) | Information telling which batch submission transactions failed |
| TransactionsBatchSubmissionResult | [#/components/schemas/TransactionsBatchSubmissionResult](#componentsschemastransactionsbatchsubmissionresult) | Batch transaction submission result

Tells which transactions failed |
| U128 | [#/components/schemas/U128](#componentsschemasu128) | A string containing a 128-bit unsigned integer.

We represent u128 values as a string to ensure compatibility with languages such
as JavaScript that do not parse u128s in JSON natively.
 |
| U256 | [#/components/schemas/U256](#componentsschemasu256) | A string containing a 256-bit unsigned integer.

We represent u256 values as a string to ensure compatibility with languages such
as JavaScript that do not parse u256s in JSON natively.
 |
| U64 | [#/components/schemas/U64](#componentsschemasu64) | A string containing a 64-bit unsigned integer.

We represent u64 values as a string to ensure compatibility with languages such
as JavaScript that do not parse u64s in JSON natively.
 |
| UserTransaction | [#/components/schemas/UserTransaction](#componentsschemasusertransaction) | A transaction submitted by a user to change the state of the blockchain |
| ValidatorTransaction | [#/components/schemas/ValidatorTransaction](#componentsschemasvalidatortransaction) |  |
| VersionedEvent | [#/components/schemas/VersionedEvent](#componentsschemasversionedevent) | An event from a transaction with a version |
| ViewRequest | [#/components/schemas/ViewRequest](#componentsschemasviewrequest) | View request for the Move View Function API |
| WriteModule | [#/components/schemas/WriteModule](#componentsschemaswritemodule) | Write a new module or update an existing one |
| WriteResource | [#/components/schemas/WriteResource](#componentsschemaswriteresource) | Write a resource or update an existing one |
| WriteSet | [#/components/schemas/WriteSet](#componentsschemaswriteset) | The associated writeset with a payload |
| WriteSetChange | [#/components/schemas/WriteSetChange](#componentsschemaswritesetchange) | A final state change of a transaction on a resource or module |
| WriteSetChange_DeleteModule | [#/components/schemas/WriteSetChange_DeleteModule](#componentsschemaswritesetchange_deletemodule) |  |
| WriteSetChange_DeleteResource | [#/components/schemas/WriteSetChange_DeleteResource](#componentsschemaswritesetchange_deleteresource) |  |
| WriteSetChange_DeleteTableItem | [#/components/schemas/WriteSetChange_DeleteTableItem](#componentsschemaswritesetchange_deletetableitem) |  |
| WriteSetChange_WriteModule | [#/components/schemas/WriteSetChange_WriteModule](#componentsschemaswritesetchange_writemodule) |  |
| WriteSetChange_WriteResource | [#/components/schemas/WriteSetChange_WriteResource](#componentsschemaswritesetchange_writeresource) |  |
| WriteSetChange_WriteTableItem | [#/components/schemas/WriteSetChange_WriteTableItem](#componentsschemaswritesetchange_writetableitem) |  |
| WriteSetPayload | [#/components/schemas/WriteSetPayload](#componentsschemaswritesetpayload) | A writeset payload, used only for genesis |
| WriteSet_DirectWriteSet | [#/components/schemas/WriteSet_DirectWriteSet](#componentsschemaswriteset_directwriteset) |  |
| WriteSet_ScriptWriteSet | [#/components/schemas/WriteSet_ScriptWriteSet](#componentsschemaswriteset_scriptwriteset) |  |
| WriteTableItem | [#/components/schemas/WriteTableItem](#componentsschemaswritetableitem) | Change set to write a table item |

## Path Details

***

### [GET]/accounts/{address}

- Summary  
Get account

- Description  
Return the authentication key and the sequence number for an account  
address. Optionally, a ledger version can be specified. If the ledger  
version is not specified in the request, the latest ledger version is used.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

#### Responses

- 200 

`application/json`

```ts
// Account data
// 
// A simplified version of the onchain Account resource
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  authentication_key: string
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/accounts/{address}/resources

- Summary  
Get account resources

- Description  
Retrieves all account resources for a given account and a specific ledger version.  If the  
ledger version is not specified in the request, the latest ledger version is used.  
  
The Aptos nodes prune account state history, via a configurable time window.  
If the requested ledger version has been pruned, the server responds with a 410.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

```ts
// Representation of a StateKey as a hex string. This is used for cursor based pagination.
// 
start?: string
```

```ts
limit?: integer
```

#### Responses

- 200 

`application/json`

```ts
// A parsed Move resource
{
  // String representation of a MoveStructTag (on-chain Move struct type). This exists so you
  // can specify MoveStructTags as path / query parameters, e.g. for get_events_by_event_handle.
  // 
  // It is a combination of:
  //   1. `move_module_address`, `module_name` and `struct_name`, all joined by `::`
  //   2. `struct generic type parameters` joined by `, `
  // 
  // Examples:
  //   * `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>`
  //   * `0x1::account::Account`
  // 
  // Note:
  //   1. Empty chars should be ignored when comparing 2 struct tag ids.
  //   2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  // See [doc](https://aptos.dev/concepts/accounts) for more details.
  // 
  type: string
  // This is a JSON representation of some data within an account resource. More specifically,
  // it is a map of strings to arbitrary JSON values / objects, where the keys are top level
  // fields within the given resource.
  // 
  // To clarify, you might query for 0x1::account::Account and see the example data.
  // 
  // Move `bool` type value is serialized into `boolean`.
  // 
  // Move `u8`, `u16` and `u32` type value is serialized into `integer`.
  // 
  // Move `u64`, `u128` and `u256` type value is serialized into `string`.
  // 
  // Move `address` type value (32 byte Aptos account address) is serialized into a HexEncodedBytes string.
  // For example:
  //   - `0x1`
  //   - `0x1668f6be25668c1a17cd8caf6b8d2f25`
  // 
  // Move `vector` type value is serialized into `array`, except `vector<u8>` which is serialized into a
  // HexEncodedBytes string with `0x` prefix.
  // For example:
  //   - `vector<u64>{255, 255}` => `["255", "255"]`
  //   - `vector<u8>{255, 255}` => `0xffff`
  // 
  // Move `struct` type value is serialized into `object` that looks like this (except some Move stdlib types, see the following section):
  //   ```json
  //   {
  //     field1_name: field1_value,
  //     field2_name: field2_value,
  //     ......
  //   }
  //   ```
  // 
  // For example:
  //   `{ "created": "0xa550c18", "role_id": "0" }`
  // 
  // **Special serialization for Move stdlib types**:
  //   - [0x1::string::String](https://github.com/aptos-labs/aptos-core/blob/main/language/move-stdlib/docs/ascii.md)
  //     is serialized into `string`. For example, struct value `0x1::string::String{bytes: b"Hello World!"}`
  //     is serialized as `"Hello World!"` in JSON.
  // 
  data: {
  }
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/accounts/{address}/modules

- Summary  
Get account modules

- Description  
Retrieves all account modules' bytecode for a given account at a specific ledger version.  
If the ledger version is not specified in the request, the latest ledger version is used.  
  
The Aptos nodes prune account state history, via a configurable time window.  
If the requested ledger version has been pruned, the server responds with a 410.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

```ts
// Representation of a StateKey as a hex string. This is used for cursor based pagination.
// 
start?: string
```

```ts
limit?: integer
```

#### Responses

- 200 

`application/json`

```ts
// Move module bytecode along with it's ABI
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  bytecode: string
  // A Move module
  abi: {
    // A hex encoded 32 byte Aptos account address.
    // 
    // This is represented in a string as a 64 character hex string, sometimes
    // shortened by stripping leading 0s, and adding a 0x.
    // 
    // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
    // 
    address: string
    name: string
    // Move module id is a string representation of Move module.
    // 
    // Format: `{address}::{module name}`
    // 
    // `address` should be hex-encoded 32 byte account address that is prefixed with `0x`.
    // 
    // Module name is case-sensitive.
    // 
    friends?: string[]
    // Move function
    exposed_functions: {
      name:#/components/schemas/IdentifierWrapper
      // Move function visibility
      visibility: enum[private, public, friend]
      // Whether the function can be called as an entry function directly in a transaction
      is_entry: boolean
      // Whether the function is a view function or not
      is_view: boolean
      // Move function generic type param
      generic_type_params: {
        constraints?: string[]
      }[]
      // String representation of an on-chain Move type tag that is exposed in transaction payload.
      //     Values:
      //       - bool
      //       - u8
      //       - u16
      //       - u32
      //       - u64
      //       - u128
      //       - u256
      //       - address
      //       - signer
      //       - vector: `vector<{non-reference MoveTypeId}>`
      //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
      // 
      //     Vector type value examples:
      //       - `vector<u8>`
      //       - `vector<vector<u64>>`
      //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
      // 
      //     Struct type value examples:
      //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
      //       - `0x1::account::Account`
      // 
      //     Note:
      //       1. Empty chars should be ignored when comparing 2 struct tag ids.
      //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
      // 
      params?: string[]
      return:#/components/schemas/MoveType[]
    }[]
    // A move struct
    structs: {
      name:#/components/schemas/IdentifierWrapper
      // Whether the struct is a native struct of Move
      is_native: boolean
      abilities:#/components/schemas/MoveAbility[]
      // Move generic type param
      generic_type_params: {
        constraints:#/components/schemas/MoveAbility[]
      }[]
      // Move struct field
      fields: {
        name:#/components/schemas/IdentifierWrapper
        type:#/components/schemas/MoveType
      }[]
    }[]
  }
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/spec

- Summary  
Show OpenAPI explorer

- Description  
Provides a UI that you can use to explore the API. You can also  
retrieve the API directly at `/spec.yaml` and `/spec.json`.

#### Responses

- 200 

`text/html`

```ts
{
  "type": "string"
}
```

***

### [GET]/-/healthy

- Summary  
Check basic node health

- Description  
By default this endpoint just checks that it can get the latest ledger  
info and then returns 200.  
  
If the duration_secs param is provided, this endpoint will return a  
200 if the following condition is true:  
  
`server_latest_ledger_info_timestamp >= server_current_time_timestamp - duration_secs`

#### Parameters(Query)

```ts
duration_secs?: integer
```

#### Responses

- 200 

`application/json`

```ts
// Representation of a successful healthcheck
{
  message: string
}
```

`application/x-bcs`

```ts
integer[]
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/blocks/by_height/{block_height}

- Summary  
Get blocks by height

- Description  
This endpoint allows you to get the transactions in a block  
and the corresponding block information.  
  
Transactions are limited by max default transactions size.  If not all transactions  
are present, the user will need to query for the rest of the transactions via the  
get transactions API.  
  
If the block is pruned, it will return a 410

#### Parameters(Query)

```ts
with_transactions?: boolean
```

#### Responses

- 200 

`application/json`

```ts
// A Block with or without transactions
// 
// This contains the information about a transactions along with
// associated transactions if requested
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  block_height: string
  block_hash: string
  block_timestamp:#/components/schemas/U64
  first_version:#/components/schemas/U64
  last_version:#/components/schemas/U64
  // Enum of the different types of transactions in Aptos
  transactions: {
  }[]
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/blocks/by_version/{version}

- Summary  
Get blocks by version

- Description  
This endpoint allows you to get the transactions in a block  
and the corresponding block information given a version in the block.  
  
Transactions are limited by max default transactions size.  If not all transactions  
are present, the user will need to query for the rest of the transactions via the  
get transactions API.  
  
If the block has been pruned, it will return a 410

#### Parameters(Query)

```ts
with_transactions?: boolean
```

#### Responses

- 200 

`application/json`

```ts
// A Block with or without transactions
// 
// This contains the information about a transactions along with
// associated transactions if requested
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  block_height: string
  block_hash: string
  block_timestamp:#/components/schemas/U64
  first_version:#/components/schemas/U64
  last_version:#/components/schemas/U64
  // Enum of the different types of transactions in Aptos
  transactions: {
  }[]
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/accounts/{address}/events/{creation_number}

- Summary  
Get events by creation number

- Description  
Event types are globally identifiable by an account `address` and  
monotonically increasing `creation_number`, one per event type emitted  
to the given account. This API returns events corresponding to that  
that event type.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
start?: string
```

```ts
limit?: integer
```

#### Responses

- 200 

`application/json`

```ts
// An event from a transaction with a version
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  guid: {
    creation_number:#/components/schemas/U64
    // A hex encoded 32 byte Aptos account address.
    // 
    // This is represented in a string as a 64 character hex string, sometimes
    // shortened by stripping leading 0s, and adding a 0x.
    // 
    // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
    // 
    account_address: string
  }
  sequence_number:#/components/schemas/U64
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type: string
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/accounts/{address}/events/{event_handle}/{field_name}

- Summary  
Get events by event handle

- Description  
This API uses the given account `address`, `eventHandle`, and `fieldName`  
to build a key that can globally identify an event types. It then uses this  
key to return events emitted to the given account matching that event type.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
start?: string
```

```ts
limit?: integer
```

#### Responses

- 200 

`application/json`

```ts
// An event from a transaction with a version
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  guid: {
    creation_number:#/components/schemas/U64
    // A hex encoded 32 byte Aptos account address.
    // 
    // This is represented in a string as a 64 character hex string, sometimes
    // shortened by stripping leading 0s, and adding a 0x.
    // 
    // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
    // 
    account_address: string
  }
  sequence_number:#/components/schemas/U64
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type: string
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/

- Summary  
Get ledger info

- Description  
Get the latest ledger information, including data such as chain ID,  
role type, ledger versions, epoch, etc.

#### Responses

- 200 

`application/json`

```ts
// The struct holding all data returned to the client by the
// index endpoint (i.e., GET "/").  Only for responding in JSON
{
  // Chain ID of the current chain
  chain_id: integer
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  epoch: string
  ledger_version:#/components/schemas/U64
  oldest_ledger_version:#/components/schemas/U64
  ledger_timestamp:#/components/schemas/U64
  node_role: enum[validator, full_node]
  oldest_block_height:#/components/schemas/U64
  block_height:#/components/schemas/U64
  // Git hash of the build of the API endpoint.  Can be used to determine the exact
  // software version used by the API endpoint.
  git_hash?: string
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/accounts/{address}/resource/{resource_type}

- Summary  
Get account resource

- Description  
Retrieves an individual resource from a given account and at a specific ledger version. If the  
ledger version is not specified in the request, the latest ledger version is used.  
  
The Aptos nodes prune account state history, via a configurable time window.  
If the requested ledger version has been pruned, the server responds with a 410.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

#### Responses

- 200 

`application/json`

```ts
// A parsed Move resource
{
  // String representation of a MoveStructTag (on-chain Move struct type). This exists so you
  // can specify MoveStructTags as path / query parameters, e.g. for get_events_by_event_handle.
  // 
  // It is a combination of:
  //   1. `move_module_address`, `module_name` and `struct_name`, all joined by `::`
  //   2. `struct generic type parameters` joined by `, `
  // 
  // Examples:
  //   * `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>`
  //   * `0x1::account::Account`
  // 
  // Note:
  //   1. Empty chars should be ignored when comparing 2 struct tag ids.
  //   2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  // See [doc](https://aptos.dev/concepts/accounts) for more details.
  // 
  type: string
  // This is a JSON representation of some data within an account resource. More specifically,
  // it is a map of strings to arbitrary JSON values / objects, where the keys are top level
  // fields within the given resource.
  // 
  // To clarify, you might query for 0x1::account::Account and see the example data.
  // 
  // Move `bool` type value is serialized into `boolean`.
  // 
  // Move `u8`, `u16` and `u32` type value is serialized into `integer`.
  // 
  // Move `u64`, `u128` and `u256` type value is serialized into `string`.
  // 
  // Move `address` type value (32 byte Aptos account address) is serialized into a HexEncodedBytes string.
  // For example:
  //   - `0x1`
  //   - `0x1668f6be25668c1a17cd8caf6b8d2f25`
  // 
  // Move `vector` type value is serialized into `array`, except `vector<u8>` which is serialized into a
  // HexEncodedBytes string with `0x` prefix.
  // For example:
  //   - `vector<u64>{255, 255}` => `["255", "255"]`
  //   - `vector<u8>{255, 255}` => `0xffff`
  // 
  // Move `struct` type value is serialized into `object` that looks like this (except some Move stdlib types, see the following section):
  //   ```json
  //   {
  //     field1_name: field1_value,
  //     field2_name: field2_value,
  //     ......
  //   }
  //   ```
  // 
  // For example:
  //   `{ "created": "0xa550c18", "role_id": "0" }`
  // 
  // **Special serialization for Move stdlib types**:
  //   - [0x1::string::String](https://github.com/aptos-labs/aptos-core/blob/main/language/move-stdlib/docs/ascii.md)
  //     is serialized into `string`. For example, struct value `0x1::string::String{bytes: b"Hello World!"}`
  //     is serialized as `"Hello World!"` in JSON.
  // 
  data: {
  }
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/accounts/{address}/module/{module_name}

- Summary  
Get account module

- Description  
Retrieves an individual module from a given account and at a specific ledger version. If the  
ledger version is not specified in the request, the latest ledger version is used.  
  
The Aptos nodes prune account state history, via a configurable time window.  
If the requested ledger version has been pruned, the server responds with a 410.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

#### Responses

- 200 

`application/json`

```ts
// Move module bytecode along with it's ABI
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  bytecode: string
  // A Move module
  abi: {
    // A hex encoded 32 byte Aptos account address.
    // 
    // This is represented in a string as a 64 character hex string, sometimes
    // shortened by stripping leading 0s, and adding a 0x.
    // 
    // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
    // 
    address: string
    name: string
    // Move module id is a string representation of Move module.
    // 
    // Format: `{address}::{module name}`
    // 
    // `address` should be hex-encoded 32 byte account address that is prefixed with `0x`.
    // 
    // Module name is case-sensitive.
    // 
    friends?: string[]
    // Move function
    exposed_functions: {
      name:#/components/schemas/IdentifierWrapper
      // Move function visibility
      visibility: enum[private, public, friend]
      // Whether the function can be called as an entry function directly in a transaction
      is_entry: boolean
      // Whether the function is a view function or not
      is_view: boolean
      // Move function generic type param
      generic_type_params: {
        constraints?: string[]
      }[]
      // String representation of an on-chain Move type tag that is exposed in transaction payload.
      //     Values:
      //       - bool
      //       - u8
      //       - u16
      //       - u32
      //       - u64
      //       - u128
      //       - u256
      //       - address
      //       - signer
      //       - vector: `vector<{non-reference MoveTypeId}>`
      //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
      // 
      //     Vector type value examples:
      //       - `vector<u8>`
      //       - `vector<vector<u64>>`
      //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
      // 
      //     Struct type value examples:
      //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
      //       - `0x1::account::Account`
      // 
      //     Note:
      //       1. Empty chars should be ignored when comparing 2 struct tag ids.
      //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
      // 
      params?: string[]
      return:#/components/schemas/MoveType[]
    }[]
    // A move struct
    structs: {
      name:#/components/schemas/IdentifierWrapper
      // Whether the struct is a native struct of Move
      is_native: boolean
      abilities:#/components/schemas/MoveAbility[]
      // Move generic type param
      generic_type_params: {
        constraints:#/components/schemas/MoveAbility[]
      }[]
      // Move struct field
      fields: {
        name:#/components/schemas/IdentifierWrapper
        type:#/components/schemas/MoveType
      }[]
    }[]
  }
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [POST]/tables/{table_handle}/item

- Summary  
Get table item

- Description  
Get a table item at a specific ledger version from the table identified by {table_handle}  
in the path and the "key" (TableItemRequest) provided in the request body.  
  
This is a POST endpoint because the "key" for requesting a specific  
table item (TableItemRequest) could be quite complex, as each of its  
fields could themselves be composed of other structs. This makes it  
impractical to express using query params, meaning GET isn't an option.  
  
The Aptos nodes prune account state history, via a configurable time window.  
If the requested ledger version has been pruned, the server responds with a 410.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

#### RequestBody

- application/json

```ts
// Table Item request for the GetTableItem API
{
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  key_type: string
  value_type:#/components/schemas/MoveType
}
```

#### Responses

- 200 

`application/json`

```ts
// An enum of the possible Move value types
{
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [POST]/tables/{table_handle}/raw_item

- Summary  
Get raw table item

- Description  
Get a table item at a specific ledger version from the table identified by {table_handle}  
in the path and the "key" (RawTableItemRequest) provided in the request body.  
  
The `get_raw_table_item` requires only a serialized key comparing to the full move type information  
comparing to the `get_table_item` api, and can only return the query in the bcs format.  
  
The Aptos nodes prune account state history, via a configurable time window.  
If the requested ledger version has been pruned, the server responds with a 410.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

#### RequestBody

- application/json

```ts
// Table Item request for the GetTableItemRaw API
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  key: string
}
```

#### Responses

- 200 

`application/json`

```ts
// An enum of the possible Move value types
{
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/transactions

- Summary  
Get transactions

- Description  
Retrieve on-chain committed transactions. The page size and start ledger version  
can be provided to get a specific sequence of transactions.  
  
If the version has been pruned, then a 410 will be returned.  
  
To retrieve a pending transaction, use /transactions/by_hash.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
start?: string
```

```ts
limit?: integer
```

#### Responses

- 200 

`application/json`

```ts
// Enum of the different types of transactions in Aptos
{
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [POST]/transactions

- Summary  
Submit transaction

- Description  
This endpoint accepts transaction submissions in two formats.  
  
To submit a transaction as JSON, you must submit a SubmitTransactionRequest.  
To build this request, do the following:  
  
1. Encode the transaction as BCS. If you are using a language that has  
native BCS support, make sure of that library. If not, you may take  
advantage of /transactions/encode_submission. When using this  
endpoint, make sure you trust the node you're talking to, as it is  
possible they could manipulate your request.  
2. Sign the encoded transaction and use it to create a TransactionSignature.  
3. Submit the request. Make sure to use the "application/json" Content-Type.  
  
To submit a transaction as BCS, you must submit a SignedTransaction  
encoded as BCS. See SignedTransaction in types/src/transaction/mod.rs.  
Make sure to use the `application/x.aptos.signed_transaction+bcs` Content-Type.

#### RequestBody

- application/json

```ts
// A request to submit a transaction
// 
// This requires a transaction and a signature of it
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
}
```

- application/x.aptos.signed_transaction+bcs

```ts
integer[]
```

#### Responses

- 202 

`application/json`

```ts
// A transaction waiting in mempool
{
  hash: string
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 413 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 507 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/transactions/by_hash/{txn_hash}

- Summary  
Get transaction by hash

- Description  
Look up a transaction by its hash. This is the same hash that is returned  
by the API when submitting a transaction (see PendingTransaction).  
  
When given a transaction hash, the server first looks for the transaction  
in storage (on-chain, committed). If no on-chain transaction is found, it  
looks the transaction up by hash in the mempool (pending, not yet committed).  
  
To create a transaction hash by yourself, do the following:  
1. Hash message bytes: "RawTransaction" bytes + BCS bytes of [Transaction](https://aptos-labs.github.io/aptos-core/aptos_types/transaction/enum.Transaction.html).  
2. Apply hash algorithm `SHA3-256` to the hash message bytes.  
3. Hex-encode the hash bytes with `0x` prefix.

#### Responses

- 200 

`application/json`

```ts
// Enum of the different types of transactions in Aptos
{
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/transactions/wait_by_hash/{txn_hash}

- Summary  
Wait for transaction by hash

- Description  
Same as /transactions/by_hash, but will wait for a pending transaction to be committed. To be used as a long  
poll optimization by clients, to reduce latency caused by polling. The "long" poll is generally a second or  
less but dictated by the server; the client must deal with the result as if the request was a normal  
/transactions/by_hash request, e.g., by retrying if the transaction is pending.

#### Responses

- 200 

`application/json`

```ts
// Enum of the different types of transactions in Aptos
{
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/transactions/by_version/{txn_version}

- Summary  
Get transaction by version

- Description  
Retrieves a transaction by a given version. If the version has been  
pruned, a 410 will be returned.

#### Responses

- 200 

`application/json`

```ts
// Enum of the different types of transactions in Aptos
{
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/accounts/{address}/transactions

- Summary  
Get account transactions

- Description  
Retrieves on-chain committed transactions from an account. If the start  
version is too far in the past, a 410 will be returned.  
  
If no start version is given, it will start at version 0.  
  
To retrieve a pending transaction, use /transactions/by_hash.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
start?: string
```

```ts
limit?: integer
```

#### Responses

- 200 

`application/json`

```ts
// Enum of the different types of transactions in Aptos
{
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [POST]/transactions/batch

- Summary  
Submit batch transactions

- Description  
This allows you to submit multiple transactions.  The response has three outcomes:  
  
1. All transactions succeed, and it will return a 202  
2. Some transactions succeed, and it will return the failed transactions and a 206  
3. No transactions succeed, and it will also return the failed transactions and a 206  
  
To submit a transaction as JSON, you must submit a SubmitTransactionRequest.  
To build this request, do the following:  
  
1. Encode the transaction as BCS. If you are using a language that has  
native BCS support, make sure to use that library. If not, you may take  
advantage of /transactions/encode_submission. When using this  
endpoint, make sure you trust the node you're talking to, as it is  
possible they could manipulate your request.  
2. Sign the encoded transaction and use it to create a TransactionSignature.  
3. Submit the request. Make sure to use the "application/json" Content-Type.  
  
To submit a transaction as BCS, you must submit a SignedTransaction  
encoded as BCS. See SignedTransaction in types/src/transaction/mod.rs.  
Make sure to use the `application/x.aptos.signed_transaction+bcs` Content-Type.

#### RequestBody

- application/json

```ts
// A request to submit a transaction
// 
// This requires a transaction and a signature of it
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
}[]
```

- application/x.aptos.signed_transaction+bcs

```ts
integer[]
```

#### Responses

- 202 

`application/json`

```ts
// Batch transaction submission result
// 
// Tells which transactions failed
{
  // Information telling which batch submission transactions failed
  transaction_failures: {
    // This is the generic struct we use for all API errors, it contains a string
    // message and an Aptos API specific error code.
    error: {
      // A message describing the error
      message: string
      // These codes provide more granular error information beyond just the HTTP
      // status code of the response.
      error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
      // A code providing VM error details when submitting transactions to the VM
      vm_error_code?: integer
    }
    // The index of which transaction failed, same as submission order
    transaction_index: integer
  }[]
}
```

`application/x-bcs`

```ts
integer[]
```

- 206 

`application/json`

```ts
// Batch transaction submission result
// 
// Tells which transactions failed
{
  // Information telling which batch submission transactions failed
  transaction_failures: {
    // This is the generic struct we use for all API errors, it contains a string
    // message and an Aptos API specific error code.
    error: {
      // A message describing the error
      message: string
      // These codes provide more granular error information beyond just the HTTP
      // status code of the response.
      error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
      // A code providing VM error details when submitting transactions to the VM
      vm_error_code?: integer
    }
    // The index of which transaction failed, same as submission order
    transaction_index: integer
  }[]
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 413 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 507 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [POST]/transactions/simulate

- Summary  
Simulate transaction

- Description  
The output of the transaction will have the exact transaction outputs and events that running  
an actual signed transaction would have.  However, it will not have the associated state  
hashes, as they are not updated in storage.  This can be used to estimate the maximum gas  
units for a submitted transaction.  
  
To use this, you must:  
- Create a SignedTransaction with a zero-padded signature.  
- Submit a SubmitTransactionRequest containing a UserTransactionRequest containing that signature.  
  
To use this endpoint with BCS, you must submit a SignedTransaction  
encoded as BCS. See SignedTransaction in types/src/transaction/mod.rs.

#### Parameters(Query)

```ts
estimate_max_gas_amount?: boolean
```

```ts
estimate_gas_unit_price?: boolean
```

```ts
estimate_prioritized_gas_unit_price?: boolean
```

#### RequestBody

- application/json

```ts
// A request to submit a transaction
// 
// This requires a transaction and a signature of it
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
}
```

- application/x.aptos.signed_transaction+bcs

```ts
integer[]
```

#### Responses

- 200 

`application/json`

```ts
// A transaction submitted by a user to change the state of the blockchain
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  hash: string
  state_change_hash:#/components/schemas/HashValue
  event_root_hash:#/components/schemas/HashValue
  state_checkpoint_hash:#/components/schemas/HashValue
  gas_used:#/components/schemas/U64
  // Whether the transaction was successful
  success: boolean
  // The VM status of the transaction, can tell useful information in a failure
  vm_status: string
  accumulator_root_hash:#/components/schemas/HashValue
  // A final state change of a transaction on a resource or module
  changes: {
  }[]
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  sequence_number:#/components/schemas/U64
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
  // An event from a transaction
  events: {
    guid: {
      creation_number:#/components/schemas/U64
      account_address:#/components/schemas/Address
    }
    sequence_number:#/components/schemas/U64
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    type: string
  }[]
  timestamp:#/components/schemas/U64
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 413 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 507 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [POST]/transactions/encode_submission

- Summary  
Encode submission

- Description  
This endpoint accepts an EncodeSubmissionRequest, which internally is a  
UserTransactionRequestInner (and optionally secondary signers) encoded  
as JSON, validates the request format, and then returns that request  
encoded in BCS. The client can then use this to create a transaction  
signature to be used in a SubmitTransactionRequest, which it then  
passes to the /transactions POST endpoint.  
  
To be clear, this endpoint makes it possible to submit transaction  
requests to the API from languages that do not have library support for  
BCS. If you are using an SDK that has BCS support, such as the official  
Rust, TypeScript, or Python SDKs, you do not need to use this endpoint.  
  
To sign a message using the response from this endpoint:  
- Decode the hex encoded string in the response to bytes.  
- Sign the bytes to create the signature.  
- Use that as the signature field in something like Ed25519Signature, which you then use to build a TransactionSignature.

#### RequestBody

- application/json

```ts
// Request to encode a submission
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  secondary_signers:#/components/schemas/Address[]
}
```

#### Responses

- 200 

`application/json`

```ts
{
  "type": "string",
  "format": "hex",
  "description": "All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with\ntwo hex digits per byte.\n\nUnlike the `Address` type, HexEncodedBytes will not trim any zeros.\n",
  "example": "0x88fbd33f54e1126269769780feb24480428179f552e2313fbe571b72e62a1ca1 "
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [GET]/estimate_gas_price

- Summary  
Estimate gas price

- Description  
Gives an estimate of the gas unit price required to get a transaction on chain in a  
reasonable amount of time. The gas unit price is the amount that each transaction commits to  
pay for each unit of gas consumed in executing the transaction. The estimate is based on  
recent history: it gives the minimum gas that would have been required to get into recent  
blocks, for blocks that were full. (When blocks are not full, the estimate will match the  
minimum gas unit price.)  
  
The estimation is given in three values: de-prioritized (low), regular, and prioritized  
(aggressive). Using a more aggressive value increases the likelihood that the transaction  
will make it into the next block; more aggressive values are computed with a larger history  
and higher percentile statistics. More details are in AIP-34.

#### Responses

- 200 

`application/json`

```ts
// Struct holding the outputs of the estimate gas API
{
  // The deprioritized estimate for the gas unit price
  deprioritized_gas_estimate?: integer
  // The current estimate for the gas unit price
  gas_estimate: integer
  // The prioritized estimate for the gas unit price
  prioritized_gas_estimate?: integer
}
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

***

### [POST]/view

- Summary  
Execute view function of a module

- Description  
Execute the Move function with the given parameters and return its execution result.  
  
The Aptos nodes prune account state history, via a configurable time window.  
If the requested ledger version has been pruned, the server responds with a 410.

#### Parameters(Query)

```ts
// A string containing a 64-bit unsigned integer.
// 
// We represent u64 values as a string to ensure compatibility with languages such
// as JavaScript that do not parse u64s in JSON natively.
// 
ledger_version?: string
```

#### RequestBody

- application/json

```ts
// View request for the Move View Function API
{
  // Entry function id is string representation of a entry function defined on-chain.
  // 
  // Format: `{address}::{module name}::{function name}`
  // 
  // Both `module name` and `function name` are case-sensitive.
  // 
  function: string
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type_arguments?: string[]
[]
}
```

- application/x.aptos.view_function+bcs

```ts
integer[]
```

#### Responses

- 200 

`application/json`

```ts
// An enum of the possible Move value types
{
}[]
```

`application/x-bcs`

```ts
integer[]
```

- 400 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 403 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 404 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 410 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 500 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

- 503 

`application/json`

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

## References

### #/components/schemas/AccountData

```ts
// Account data
// 
// A simplified version of the onchain Account resource
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  authentication_key: string
}
```

### #/components/schemas/AccountSignature

```ts
// Account signature scheme
// 
// The account signature scheme allows you to have two types of accounts:
// 
// 1. A single Ed25519 key account, one private key
// 2. A k-of-n multi-Ed25519 key account, multiple private keys, such that k-of-n must sign a transaction.
// 3. A single Secp256k1Ecdsa key account, one private key
{
}
```

### #/components/schemas/AccountSignature_Ed25519Signature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "ed25519_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/Ed25519Signature"
    }
  ]
}
```

### #/components/schemas/AccountSignature_MultiEd25519Signature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "multi_ed25519_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/MultiEd25519Signature"
    }
  ]
}
```

### #/components/schemas/AccountSignature_MultiKeySignature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "multi_key_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/MultiKeySignature"
    }
  ]
}
```

### #/components/schemas/AccountSignature_SingleKeySignature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "single_key_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/SingleKeySignature"
    }
  ]
}
```

### #/components/schemas/Address

```ts
{
  "type": "string",
  "format": "hex",
  "description": "A hex encoded 32 byte Aptos account address.\n\nThis is represented in a string as a 64 character hex string, sometimes\nshortened by stripping leading 0s, and adding a 0x.\n\nFor example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.\n",
  "example": "0x88fbd33f54e1126269769780feb24480428179f552e2313fbe571b72e62a1ca1 "
}
```

### #/components/schemas/AptosError

```ts
// This is the generic struct we use for all API errors, it contains a string
// message and an Aptos API specific error code.
{
  // A message describing the error
  message: string
  // These codes provide more granular error information beyond just the HTTP
  // status code of the response.
  error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
  // A code providing VM error details when submitting transactions to the VM
  vm_error_code?: integer
}
```

### #/components/schemas/AptosErrorCode

```ts
{
  "type": "string",
  "description": "These codes provide more granular error information beyond just the HTTP\nstatus code of the response.",
  "enum": [
    "account_not_found",
    "resource_not_found",
    "module_not_found",
    "struct_field_not_found",
    "version_not_found",
    "transaction_not_found",
    "table_item_not_found",
    "block_not_found",
    "state_value_not_found",
    "version_pruned",
    "block_pruned",
    "invalid_input",
    "invalid_transaction_update",
    "sequence_number_too_old",
    "vm_error",
    "health_check_failed",
    "mempool_is_full",
    "internal_error",
    "web_framework_error",
    "bcs_not_supported",
    "api_disabled"
  ]
}
```

### #/components/schemas/Block

```ts
// A Block with or without transactions
// 
// This contains the information about a transactions along with
// associated transactions if requested
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  block_height: string
  block_hash: string
  block_timestamp:#/components/schemas/U64
  first_version:#/components/schemas/U64
  last_version:#/components/schemas/U64
  // Enum of the different types of transactions in Aptos
  transactions: {
  }[]
}
```

### #/components/schemas/BlockMetadataTransaction

```ts
// A block metadata transaction
// 
// This signifies the beginning of a block, and contains information
// about the specific block
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  hash: string
  state_change_hash:#/components/schemas/HashValue
  event_root_hash:#/components/schemas/HashValue
  state_checkpoint_hash:#/components/schemas/HashValue
  gas_used:#/components/schemas/U64
  // Whether the transaction was successful
  success: boolean
  // The VM status of the transaction, can tell useful information in a failure
  vm_status: string
  accumulator_root_hash:#/components/schemas/HashValue
  // A final state change of a transaction on a resource or module
  changes: {
  }[]
  id:#/components/schemas/HashValue
  epoch:#/components/schemas/U64
  round:#/components/schemas/U64
  // An event from a transaction
  events: {
    guid: {
      creation_number:#/components/schemas/U64
      // A hex encoded 32 byte Aptos account address.
      // 
      // This is represented in a string as a 64 character hex string, sometimes
      // shortened by stripping leading 0s, and adding a 0x.
      // 
      // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
      // 
      account_address: string
    }
    sequence_number:#/components/schemas/U64
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    type: string
  }[]
  previous_block_votes_bitvec?: integer[]
  proposer:#/components/schemas/Address
  failed_proposer_indices?: integer[]
  timestamp:#/components/schemas/U64
}
```

### #/components/schemas/DecodedTableData

```ts
// Decoded table data
{
  // Type of key
  key_type: string
  // Type of value
  value_type: string
}
```

### #/components/schemas/DeleteModule

```ts
// Delete a module
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  address: string
  // State key hash
  state_key_hash: string
  // Move module id is a string representation of Move module.
  // 
  // Format: `{address}::{module name}`
  // 
  // `address` should be hex-encoded 32 byte account address that is prefixed with `0x`.
  // 
  // Module name is case-sensitive.
  // 
  module: string
}
```

### #/components/schemas/DeleteResource

```ts
// Delete a resource
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  address: string
  // State key hash
  state_key_hash: string
  // String representation of a MoveStructTag (on-chain Move struct type). This exists so you
  // can specify MoveStructTags as path / query parameters, e.g. for get_events_by_event_handle.
  // 
  // It is a combination of:
  //   1. `move_module_address`, `module_name` and `struct_name`, all joined by `::`
  //   2. `struct generic type parameters` joined by `, `
  // 
  // Examples:
  //   * `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>`
  //   * `0x1::account::Account`
  // 
  // Note:
  //   1. Empty chars should be ignored when comparing 2 struct tag ids.
  //   2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  // See [doc](https://aptos.dev/concepts/accounts) for more details.
  // 
  resource: string
}
```

### #/components/schemas/DeleteTableItem

```ts
// Delete a table item
{
  state_key_hash: string
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  handle: string
  key:#/components/schemas/HexEncodedBytes
  // Deleted table data
  data: {
    // Deleted key type
    key_type: string
  }
}
```

### #/components/schemas/DeletedTableData

```ts
// Deleted table data
{
  // Deleted key type
  key_type: string
}
```

### #/components/schemas/DeprecatedModuleBundlePayload

```ts
{
}
```

### #/components/schemas/DirectWriteSet

```ts
{
  // A final state change of a transaction on a resource or module
  changes: {
  }[]
  // An event from a transaction
  events: {
    guid: {
      // A string containing a 64-bit unsigned integer.
      // 
      // We represent u64 values as a string to ensure compatibility with languages such
      // as JavaScript that do not parse u64s in JSON natively.
      // 
      creation_number: string
      // A hex encoded 32 byte Aptos account address.
      // 
      // This is represented in a string as a 64 character hex string, sometimes
      // shortened by stripping leading 0s, and adding a 0x.
      // 
      // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
      // 
      account_address: string
    }
    sequence_number:#/components/schemas/U64
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    type: string
  }[]
}
```

### #/components/schemas/Ed25519Signature

```ts
// A single Ed25519 signature
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  public_key: string
  signature:#/components/schemas/HexEncodedBytes
}
```

### #/components/schemas/EncodeSubmissionRequest

```ts
// Request to encode a submission
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  secondary_signers:#/components/schemas/Address[]
}
```

### #/components/schemas/EntryFunctionId

```ts
{
  "type": "string",
  "description": "Entry function id is string representation of a entry function defined on-chain.\n\nFormat: `{address}::{module name}::{function name}`\n\nBoth `module name` and `function name` are case-sensitive.\n",
  "example": "0x1::aptos_coin::transfer"
}
```

### #/components/schemas/EntryFunctionPayload

```ts
// Payload which runs a single entry function
{
  // Entry function id is string representation of a entry function defined on-chain.
  // 
  // Format: `{address}::{module name}::{function name}`
  // 
  // Both `module name` and `function name` are case-sensitive.
  // 
  function: string
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type_arguments?: string[]
[]
}
```

### #/components/schemas/Event

```ts
// An event from a transaction
{
  guid: {
    // A string containing a 64-bit unsigned integer.
    // 
    // We represent u64 values as a string to ensure compatibility with languages such
    // as JavaScript that do not parse u64s in JSON natively.
    // 
    creation_number: string
    // A hex encoded 32 byte Aptos account address.
    // 
    // This is represented in a string as a 64 character hex string, sometimes
    // shortened by stripping leading 0s, and adding a 0x.
    // 
    // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
    // 
    account_address: string
  }
  sequence_number:#/components/schemas/U64
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type: string
}
```

### #/components/schemas/EventGuid

```ts
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  creation_number: string
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  account_address: string
}
```

### #/components/schemas/FeePayerSignature

```ts
// Fee payer signature for fee payer transactions
// 
// This allows you to have transactions across multiple accounts and with a fee payer
{
  // Account signature scheme
  // 
  // The account signature scheme allows you to have two types of accounts:
  // 
  // 1. A single Ed25519 key account, one private key
  // 2. A k-of-n multi-Ed25519 key account, multiple private keys, such that k-of-n must sign a transaction.
  // 3. A single Secp256k1Ecdsa key account, one private key
  sender: {
  }
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  secondary_signer_addresses?: string[]
  secondary_signers:#/components/schemas/AccountSignature[]
  fee_payer_address: #/components/schemas/Address & 
  fee_payer_signer: #/components/schemas/AccountSignature & 
}
```

### #/components/schemas/GasEstimation

```ts
// Struct holding the outputs of the estimate gas API
{
  // The deprioritized estimate for the gas unit price
  deprioritized_gas_estimate?: integer
  // The current estimate for the gas unit price
  gas_estimate: integer
  // The prioritized estimate for the gas unit price
  prioritized_gas_estimate?: integer
}
```

### #/components/schemas/GenesisPayload

```ts
// The writeset payload of the Genesis transaction
{
}
```

### #/components/schemas/GenesisPayload_WriteSetPayload

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "write_set_payload"
        }
      }
    },
    {
      "$ref": "#/components/schemas/WriteSetPayload"
    }
  ]
}
```

### #/components/schemas/GenesisTransaction

```ts
// The genesis transaction
// 
// This only occurs at the genesis transaction (version 0)
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  hash: string
  state_change_hash:#/components/schemas/HashValue
  event_root_hash:#/components/schemas/HashValue
  state_checkpoint_hash:#/components/schemas/HashValue
  gas_used:#/components/schemas/U64
  // Whether the transaction was successful
  success: boolean
  // The VM status of the transaction, can tell useful information in a failure
  vm_status: string
  accumulator_root_hash:#/components/schemas/HashValue
  // A final state change of a transaction on a resource or module
  changes: {
  }[]
  // The writeset payload of the Genesis transaction
  payload: {
  }
  // An event from a transaction
  events: {
    guid: {
      creation_number:#/components/schemas/U64
      // A hex encoded 32 byte Aptos account address.
      // 
      // This is represented in a string as a 64 character hex string, sometimes
      // shortened by stripping leading 0s, and adding a 0x.
      // 
      // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
      // 
      account_address: string
    }
    sequence_number:#/components/schemas/U64
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    type: string
  }[]
}
```

### #/components/schemas/HashValue

```ts
{
  "type": "string"
}
```

### #/components/schemas/HealthCheckSuccess

```ts
// Representation of a successful healthcheck
{
  message: string
}
```

### #/components/schemas/HexEncodedBytes

```ts
{
  "type": "string",
  "format": "hex",
  "description": "All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with\ntwo hex digits per byte.\n\nUnlike the `Address` type, HexEncodedBytes will not trim any zeros.\n",
  "example": "0x88fbd33f54e1126269769780feb24480428179f552e2313fbe571b72e62a1ca1 "
}
```

### #/components/schemas/IdentifierWrapper

```ts
{
  "type": "string"
}
```

### #/components/schemas/IndexResponse

```ts
// The struct holding all data returned to the client by the
// index endpoint (i.e., GET "/").  Only for responding in JSON
{
  // Chain ID of the current chain
  chain_id: integer
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  epoch: string
  ledger_version:#/components/schemas/U64
  oldest_ledger_version:#/components/schemas/U64
  ledger_timestamp:#/components/schemas/U64
  node_role: enum[validator, full_node]
  oldest_block_height:#/components/schemas/U64
  block_height:#/components/schemas/U64
  // Git hash of the build of the API endpoint.  Can be used to determine the exact
  // software version used by the API endpoint.
  git_hash?: string
}
```

### #/components/schemas/IndexedSignature

```ts
{
  index: integer
  signature: {
  }
}
```

### #/components/schemas/MoveAbility

```ts
{
  "type": "string"
}
```

### #/components/schemas/MoveFunction

```ts
// Move function
{
  name: string
  // Move function visibility
  visibility: enum[private, public, friend]
  // Whether the function can be called as an entry function directly in a transaction
  is_entry: boolean
  // Whether the function is a view function or not
  is_view: boolean
  // Move function generic type param
  generic_type_params: {
    constraints?: string[]
  }[]
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  params?: string[]
  return:#/components/schemas/MoveType[]
}
```

### #/components/schemas/MoveFunctionGenericTypeParam

```ts
// Move function generic type param
{
  constraints?: string[]
}
```

### #/components/schemas/MoveFunctionVisibility

```ts
{
  "type": "string",
  "description": "Move function visibility",
  "enum": [
    "private",
    "public",
    "friend"
  ]
}
```

### #/components/schemas/MoveModule

```ts
// A Move module
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  address: string
  name: string
  // Move module id is a string representation of Move module.
  // 
  // Format: `{address}::{module name}`
  // 
  // `address` should be hex-encoded 32 byte account address that is prefixed with `0x`.
  // 
  // Module name is case-sensitive.
  // 
  friends?: string[]
  // Move function
  exposed_functions: {
    name:#/components/schemas/IdentifierWrapper
    // Move function visibility
    visibility: enum[private, public, friend]
    // Whether the function can be called as an entry function directly in a transaction
    is_entry: boolean
    // Whether the function is a view function or not
    is_view: boolean
    // Move function generic type param
    generic_type_params: {
      constraints?: string[]
    }[]
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    params?: string[]
    return:#/components/schemas/MoveType[]
  }[]
  // A move struct
  structs: {
    name:#/components/schemas/IdentifierWrapper
    // Whether the struct is a native struct of Move
    is_native: boolean
    abilities:#/components/schemas/MoveAbility[]
    // Move generic type param
    generic_type_params: {
      constraints:#/components/schemas/MoveAbility[]
    }[]
    // Move struct field
    fields: {
      name:#/components/schemas/IdentifierWrapper
      type:#/components/schemas/MoveType
    }[]
  }[]
}
```

### #/components/schemas/MoveModuleBytecode

```ts
// Move module bytecode along with it's ABI
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  bytecode: string
  // A Move module
  abi: {
    // A hex encoded 32 byte Aptos account address.
    // 
    // This is represented in a string as a 64 character hex string, sometimes
    // shortened by stripping leading 0s, and adding a 0x.
    // 
    // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
    // 
    address: string
    name: string
    // Move module id is a string representation of Move module.
    // 
    // Format: `{address}::{module name}`
    // 
    // `address` should be hex-encoded 32 byte account address that is prefixed with `0x`.
    // 
    // Module name is case-sensitive.
    // 
    friends?: string[]
    // Move function
    exposed_functions: {
      name:#/components/schemas/IdentifierWrapper
      // Move function visibility
      visibility: enum[private, public, friend]
      // Whether the function can be called as an entry function directly in a transaction
      is_entry: boolean
      // Whether the function is a view function or not
      is_view: boolean
      // Move function generic type param
      generic_type_params: {
        constraints?: string[]
      }[]
      // String representation of an on-chain Move type tag that is exposed in transaction payload.
      //     Values:
      //       - bool
      //       - u8
      //       - u16
      //       - u32
      //       - u64
      //       - u128
      //       - u256
      //       - address
      //       - signer
      //       - vector: `vector<{non-reference MoveTypeId}>`
      //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
      // 
      //     Vector type value examples:
      //       - `vector<u8>`
      //       - `vector<vector<u64>>`
      //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
      // 
      //     Struct type value examples:
      //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
      //       - `0x1::account::Account`
      // 
      //     Note:
      //       1. Empty chars should be ignored when comparing 2 struct tag ids.
      //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
      // 
      params?: string[]
      return:#/components/schemas/MoveType[]
    }[]
    // A move struct
    structs: {
      name:#/components/schemas/IdentifierWrapper
      // Whether the struct is a native struct of Move
      is_native: boolean
      abilities:#/components/schemas/MoveAbility[]
      // Move generic type param
      generic_type_params: {
        constraints:#/components/schemas/MoveAbility[]
      }[]
      // Move struct field
      fields: {
        name:#/components/schemas/IdentifierWrapper
        type:#/components/schemas/MoveType
      }[]
    }[]
  }
}
```

### #/components/schemas/MoveModuleId

```ts
{
  "type": "string",
  "description": "Move module id is a string representation of Move module.\n\nFormat: `{address}::{module name}`\n\n`address` should be hex-encoded 32 byte account address that is prefixed with `0x`.\n\nModule name is case-sensitive.\n",
  "example": "0x1::aptos_coin"
}
```

### #/components/schemas/MoveResource

```ts
// A parsed Move resource
{
  // String representation of a MoveStructTag (on-chain Move struct type). This exists so you
  // can specify MoveStructTags as path / query parameters, e.g. for get_events_by_event_handle.
  // 
  // It is a combination of:
  //   1. `move_module_address`, `module_name` and `struct_name`, all joined by `::`
  //   2. `struct generic type parameters` joined by `, `
  // 
  // Examples:
  //   * `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>`
  //   * `0x1::account::Account`
  // 
  // Note:
  //   1. Empty chars should be ignored when comparing 2 struct tag ids.
  //   2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  // See [doc](https://aptos.dev/concepts/accounts) for more details.
  // 
  type: string
  // This is a JSON representation of some data within an account resource. More specifically,
  // it is a map of strings to arbitrary JSON values / objects, where the keys are top level
  // fields within the given resource.
  // 
  // To clarify, you might query for 0x1::account::Account and see the example data.
  // 
  // Move `bool` type value is serialized into `boolean`.
  // 
  // Move `u8`, `u16` and `u32` type value is serialized into `integer`.
  // 
  // Move `u64`, `u128` and `u256` type value is serialized into `string`.
  // 
  // Move `address` type value (32 byte Aptos account address) is serialized into a HexEncodedBytes string.
  // For example:
  //   - `0x1`
  //   - `0x1668f6be25668c1a17cd8caf6b8d2f25`
  // 
  // Move `vector` type value is serialized into `array`, except `vector<u8>` which is serialized into a
  // HexEncodedBytes string with `0x` prefix.
  // For example:
  //   - `vector<u64>{255, 255}` => `["255", "255"]`
  //   - `vector<u8>{255, 255}` => `0xffff`
  // 
  // Move `struct` type value is serialized into `object` that looks like this (except some Move stdlib types, see the following section):
  //   ```json
  //   {
  //     field1_name: field1_value,
  //     field2_name: field2_value,
  //     ......
  //   }
  //   ```
  // 
  // For example:
  //   `{ "created": "0xa550c18", "role_id": "0" }`
  // 
  // **Special serialization for Move stdlib types**:
  //   - [0x1::string::String](https://github.com/aptos-labs/aptos-core/blob/main/language/move-stdlib/docs/ascii.md)
  //     is serialized into `string`. For example, struct value `0x1::string::String{bytes: b"Hello World!"}`
  //     is serialized as `"Hello World!"` in JSON.
  // 
  data: {
  }
}
```

### #/components/schemas/MoveScriptBytecode

```ts
// Move script bytecode
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  bytecode: string
  // Move function
  abi: {
    name: string
    // Move function visibility
    visibility: enum[private, public, friend]
    // Whether the function can be called as an entry function directly in a transaction
    is_entry: boolean
    // Whether the function is a view function or not
    is_view: boolean
    // Move function generic type param
    generic_type_params: {
      constraints?: string[]
    }[]
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    params?: string[]
    return:#/components/schemas/MoveType[]
  }
}
```

### #/components/schemas/MoveStruct

```ts
// A move struct
{
  name: string
  // Whether the struct is a native struct of Move
  is_native: boolean
  abilities?: string[]
  // Move generic type param
  generic_type_params: {
    constraints:#/components/schemas/MoveAbility[]
  }[]
  // Move struct field
  fields: {
    name:#/components/schemas/IdentifierWrapper
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    type: string
  }[]
}
```

### #/components/schemas/MoveStructField

```ts
// Move struct field
{
  name: string
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type: string
}
```

### #/components/schemas/MoveStructGenericTypeParam

```ts
// Move generic type param
{
  constraints?: string[]
}
```

### #/components/schemas/MoveStructTag

```ts
{
  "type": "string",
  "description": "String representation of a MoveStructTag (on-chain Move struct type). This exists so you\ncan specify MoveStructTags as path / query parameters, e.g. for get_events_by_event_handle.\n\nIt is a combination of:\n  1. `move_module_address`, `module_name` and `struct_name`, all joined by `::`\n  2. `struct generic type parameters` joined by `, `\n\nExamples:\n  * `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>`\n  * `0x1::account::Account`\n\nNote:\n  1. Empty chars should be ignored when comparing 2 struct tag ids.\n  2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).\n\nSee [doc](https://aptos.dev/concepts/accounts) for more details.\n",
  "example": "0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>",
  "pattern": "^0x[0-9a-zA-Z:_<>]+$"
}
```

### #/components/schemas/MoveStructValue

```ts
// This is a JSON representation of some data within an account resource. More specifically,
// it is a map of strings to arbitrary JSON values / objects, where the keys are top level
// fields within the given resource.
// 
// To clarify, you might query for 0x1::account::Account and see the example data.
// 
// Move `bool` type value is serialized into `boolean`.
// 
// Move `u8`, `u16` and `u32` type value is serialized into `integer`.
// 
// Move `u64`, `u128` and `u256` type value is serialized into `string`.
// 
// Move `address` type value (32 byte Aptos account address) is serialized into a HexEncodedBytes string.
// For example:
//   - `0x1`
//   - `0x1668f6be25668c1a17cd8caf6b8d2f25`
// 
// Move `vector` type value is serialized into `array`, except `vector<u8>` which is serialized into a
// HexEncodedBytes string with `0x` prefix.
// For example:
//   - `vector<u64>{255, 255}` => `["255", "255"]`
//   - `vector<u8>{255, 255}` => `0xffff`
// 
// Move `struct` type value is serialized into `object` that looks like this (except some Move stdlib types, see the following section):
//   ```json
//   {
//     field1_name: field1_value,
//     field2_name: field2_value,
//     ......
//   }
//   ```
// 
// For example:
//   `{ "created": "0xa550c18", "role_id": "0" }`
// 
// **Special serialization for Move stdlib types**:
//   - [0x1::string::String](https://github.com/aptos-labs/aptos-core/blob/main/language/move-stdlib/docs/ascii.md)
//     is serialized into `string`. For example, struct value `0x1::string::String{bytes: b"Hello World!"}`
//     is serialized as `"Hello World!"` in JSON.
// 
{
}
```

### #/components/schemas/MoveType

```ts
{
  "type": "string",
  "description": "String representation of an on-chain Move type tag that is exposed in transaction payload.\n    Values:\n      - bool\n      - u8\n      - u16\n      - u32\n      - u64\n      - u128\n      - u256\n      - address\n      - signer\n      - vector: `vector<{non-reference MoveTypeId}>`\n      - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`\n\n    Vector type value examples:\n      - `vector<u8>`\n      - `vector<vector<u64>>`\n      - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`\n\n    Struct type value examples:\n      - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>\n      - `0x1::account::Account`\n\n    Note:\n      1. Empty chars should be ignored when comparing 2 struct tag ids.\n      2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).\n",
  "pattern": "^(bool|u8|u64|u128|address|signer|vector<.+>|0x[0-9a-zA-Z:_<, >]+)$"
}
```

### #/components/schemas/MoveValue

```ts
// An enum of the possible Move value types
{
}
```

### #/components/schemas/MultiAgentSignature

```ts
// Multi agent signature for multi agent transactions
// 
// This allows you to have transactions across multiple accounts
{
  // Account signature scheme
  // 
  // The account signature scheme allows you to have two types of accounts:
  // 
  // 1. A single Ed25519 key account, one private key
  // 2. A k-of-n multi-Ed25519 key account, multiple private keys, such that k-of-n must sign a transaction.
  // 3. A single Secp256k1Ecdsa key account, one private key
  sender: {
  }
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  secondary_signer_addresses?: string[]
  secondary_signers:#/components/schemas/AccountSignature[]
}
```

### #/components/schemas/MultiEd25519Signature

```ts
// A Ed25519 multi-sig signature
// 
// This allows k-of-n signing for a transaction
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  public_keys?: string[]
  signatures:#/components/schemas/HexEncodedBytes[]
  // The number of signatures required for a successful transaction
  threshold: integer
  bitmap:#/components/schemas/HexEncodedBytes
}
```

### #/components/schemas/MultiKeySignature

```ts
// A multi key signature
{
  public_keys: {
  }[]
  signatures: {
    index: integer
    signature: {
    }
  }[]
  signatures_required: integer
}
```

### #/components/schemas/MultisigPayload

```ts
// A multisig transaction that allows an owner of a multisig account to execute a pre-approved
// transaction as the multisig account.
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  multisig_address: string
  transaction_payload: {
  }
}
```

### #/components/schemas/MultisigTransactionPayload

```ts
{
}
```

### #/components/schemas/MultisigTransactionPayload_EntryFunctionPayload

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "entry_function_payload"
        }
      }
    },
    {
      "$ref": "#/components/schemas/EntryFunctionPayload"
    }
  ]
}
```

### #/components/schemas/PendingTransaction

```ts
// A transaction waiting in mempool
{
  hash: string
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
}
```

### #/components/schemas/PublicKey

```ts
{
}
```

### #/components/schemas/PublicKey_string(HexEncodedBytes)

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "keyless"
        }
      }
    },
    {
      "$ref": "#/components/schemas/HexEncodedBytes"
    }
  ]
}
```

### #/components/schemas/RawTableItemRequest

```ts
// Table Item request for the GetTableItemRaw API
{
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  key: string
}
```

### #/components/schemas/RoleType

```ts
{
  "type": "string",
  "enum": [
    "validator",
    "full_node"
  ]
}
```

### #/components/schemas/ScriptPayload

```ts
// Payload which runs a script that can run multiple functions
{
  // Move script bytecode
  code: {
    // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
    // two hex digits per byte.
    // 
    // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
    // 
    bytecode: string
    // Move function
    abi: {
      name: string
      // Move function visibility
      visibility: enum[private, public, friend]
      // Whether the function can be called as an entry function directly in a transaction
      is_entry: boolean
      // Whether the function is a view function or not
      is_view: boolean
      // Move function generic type param
      generic_type_params: {
        constraints?: string[]
      }[]
      // String representation of an on-chain Move type tag that is exposed in transaction payload.
      //     Values:
      //       - bool
      //       - u8
      //       - u16
      //       - u32
      //       - u64
      //       - u128
      //       - u256
      //       - address
      //       - signer
      //       - vector: `vector<{non-reference MoveTypeId}>`
      //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
      // 
      //     Vector type value examples:
      //       - `vector<u8>`
      //       - `vector<vector<u64>>`
      //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
      // 
      //     Struct type value examples:
      //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
      //       - `0x1::account::Account`
      // 
      //     Note:
      //       1. Empty chars should be ignored when comparing 2 struct tag ids.
      //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
      // 
      params?: string[]
      return:#/components/schemas/MoveType[]
    }
  }
  type_arguments:#/components/schemas/MoveType[]
[]
}
```

### #/components/schemas/ScriptWriteSet

```ts
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  execute_as: string
  // Payload which runs a script that can run multiple functions
  script: {
    // Move script bytecode
    code: {
      // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
      // two hex digits per byte.
      // 
      // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
      // 
      bytecode: string
      // Move function
      abi: {
        name: string
        // Move function visibility
        visibility: enum[private, public, friend]
        // Whether the function can be called as an entry function directly in a transaction
        is_entry: boolean
        // Whether the function is a view function or not
        is_view: boolean
        // Move function generic type param
        generic_type_params: {
          constraints?: string[]
        }[]
        // String representation of an on-chain Move type tag that is exposed in transaction payload.
        //     Values:
        //       - bool
        //       - u8
        //       - u16
        //       - u32
        //       - u64
        //       - u128
        //       - u256
        //       - address
        //       - signer
        //       - vector: `vector<{non-reference MoveTypeId}>`
        //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
        // 
        //     Vector type value examples:
        //       - `vector<u8>`
        //       - `vector<vector<u64>>`
        //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
        // 
        //     Struct type value examples:
        //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
        //       - `0x1::account::Account`
        // 
        //     Note:
        //       1. Empty chars should be ignored when comparing 2 struct tag ids.
        //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
        // 
        params?: string[]
        return:#/components/schemas/MoveType[]
      }
    }
    type_arguments:#/components/schemas/MoveType[]
[]
  }
}
```

### #/components/schemas/Signature

```ts
{
}
```

### #/components/schemas/Signature_string(HexEncodedBytes)

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "keyless"
        }
      }
    },
    {
      "$ref": "#/components/schemas/HexEncodedBytes"
    }
  ]
}
```

### #/components/schemas/SingleKeySignature

```ts
// A single key signature
{
  public_key: {
  }
  signature: {
  }
}
```

### #/components/schemas/StateCheckpointTransaction

```ts
// A state checkpoint transaction
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  hash: string
  state_change_hash:#/components/schemas/HashValue
  event_root_hash:#/components/schemas/HashValue
  state_checkpoint_hash:#/components/schemas/HashValue
  gas_used:#/components/schemas/U64
  // Whether the transaction was successful
  success: boolean
  // The VM status of the transaction, can tell useful information in a failure
  vm_status: string
  accumulator_root_hash:#/components/schemas/HashValue
  // A final state change of a transaction on a resource or module
  changes: {
  }[]
  timestamp:#/components/schemas/U64
}
```

### #/components/schemas/StateKeyWrapper

```ts
{
  "type": "string",
  "description": "Representation of a StateKey as a hex string. This is used for cursor based pagination.\n",
  "example": "0000000000000000000000000000000000000000000000000000000000000000012f0000000000000000000000000000000000000000000000000000000000000000010d7374616b696e675f70726f7879"
}
```

### #/components/schemas/SubmitTransactionRequest

```ts
// A request to submit a transaction
// 
// This requires a transaction and a signature of it
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  sequence_number: string
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
}
```

### #/components/schemas/TableItemRequest

```ts
// Table Item request for the GetTableItem API
{
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  key_type: string
  value_type:#/components/schemas/MoveType
}
```

### #/components/schemas/Transaction

```ts
// Enum of the different types of transactions in Aptos
{
}
```

### #/components/schemas/TransactionPayload

```ts
// An enum of the possible transaction payloads
{
}
```

### #/components/schemas/TransactionPayload_DeprecatedModuleBundlePayload

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "module_bundle_payload"
        }
      }
    },
    {
      "$ref": "#/components/schemas/DeprecatedModuleBundlePayload"
    }
  ]
}
```

### #/components/schemas/TransactionPayload_EntryFunctionPayload

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "entry_function_payload"
        }
      }
    },
    {
      "$ref": "#/components/schemas/EntryFunctionPayload"
    }
  ]
}
```

### #/components/schemas/TransactionPayload_MultisigPayload

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "multisig_payload"
        }
      }
    },
    {
      "$ref": "#/components/schemas/MultisigPayload"
    }
  ]
}
```

### #/components/schemas/TransactionPayload_ScriptPayload

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "script_payload"
        }
      }
    },
    {
      "$ref": "#/components/schemas/ScriptPayload"
    }
  ]
}
```

### #/components/schemas/TransactionSignature

```ts
// An enum representing the different transaction signatures available
{
}
```

### #/components/schemas/TransactionSignature_AccountSignature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "single_sender"
        }
      }
    },
    {
      "$ref": "#/components/schemas/AccountSignature"
    }
  ]
}
```

### #/components/schemas/TransactionSignature_Ed25519Signature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "ed25519_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/Ed25519Signature"
    }
  ]
}
```

### #/components/schemas/TransactionSignature_FeePayerSignature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "fee_payer_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/FeePayerSignature"
    }
  ]
}
```

### #/components/schemas/TransactionSignature_MultiAgentSignature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "multi_agent_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/MultiAgentSignature"
    }
  ]
}
```

### #/components/schemas/TransactionSignature_MultiEd25519Signature

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "multi_ed25519_signature"
        }
      }
    },
    {
      "$ref": "#/components/schemas/MultiEd25519Signature"
    }
  ]
}
```

### #/components/schemas/Transaction_BlockMetadataTransaction

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "block_metadata_transaction"
        }
      }
    },
    {
      "$ref": "#/components/schemas/BlockMetadataTransaction"
    }
  ]
}
```

### #/components/schemas/Transaction_GenesisTransaction

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "genesis_transaction"
        }
      }
    },
    {
      "$ref": "#/components/schemas/GenesisTransaction"
    }
  ]
}
```

### #/components/schemas/Transaction_PendingTransaction

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "pending_transaction"
        }
      }
    },
    {
      "$ref": "#/components/schemas/PendingTransaction"
    }
  ]
}
```

### #/components/schemas/Transaction_StateCheckpointTransaction

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "state_checkpoint_transaction"
        }
      }
    },
    {
      "$ref": "#/components/schemas/StateCheckpointTransaction"
    }
  ]
}
```

### #/components/schemas/Transaction_UserTransaction

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "user_transaction"
        }
      }
    },
    {
      "$ref": "#/components/schemas/UserTransaction"
    }
  ]
}
```

### #/components/schemas/Transaction_ValidatorTransaction

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "validator_transaction"
        }
      }
    },
    {
      "$ref": "#/components/schemas/ValidatorTransaction"
    }
  ]
}
```

### #/components/schemas/TransactionsBatchSingleSubmissionFailure

```ts
// Information telling which batch submission transactions failed
{
  // This is the generic struct we use for all API errors, it contains a string
  // message and an Aptos API specific error code.
  error: {
    // A message describing the error
    message: string
    // These codes provide more granular error information beyond just the HTTP
    // status code of the response.
    error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
    // A code providing VM error details when submitting transactions to the VM
    vm_error_code?: integer
  }
  // The index of which transaction failed, same as submission order
  transaction_index: integer
}
```

### #/components/schemas/TransactionsBatchSubmissionResult

```ts
// Batch transaction submission result
// 
// Tells which transactions failed
{
  // Information telling which batch submission transactions failed
  transaction_failures: {
    // This is the generic struct we use for all API errors, it contains a string
    // message and an Aptos API specific error code.
    error: {
      // A message describing the error
      message: string
      // These codes provide more granular error information beyond just the HTTP
      // status code of the response.
      error_code: enum[account_not_found, resource_not_found, module_not_found, struct_field_not_found, version_not_found, transaction_not_found, table_item_not_found, block_not_found, state_value_not_found, version_pruned, block_pruned, invalid_input, invalid_transaction_update, sequence_number_too_old, vm_error, health_check_failed, mempool_is_full, internal_error, web_framework_error, bcs_not_supported, api_disabled]
      // A code providing VM error details when submitting transactions to the VM
      vm_error_code?: integer
    }
    // The index of which transaction failed, same as submission order
    transaction_index: integer
  }[]
}
```

### #/components/schemas/U128

```ts
{
  "type": "string",
  "format": "uint128",
  "description": "A string containing a 128-bit unsigned integer.\n\nWe represent u128 values as a string to ensure compatibility with languages such\nas JavaScript that do not parse u128s in JSON natively.\n",
  "example": "340282366920938463463374607431768211454"
}
```

### #/components/schemas/U256

```ts
{
  "type": "string",
  "format": "uint256",
  "description": "A string containing a 256-bit unsigned integer.\n\nWe represent u256 values as a string to ensure compatibility with languages such\nas JavaScript that do not parse u256s in JSON natively.\n",
  "example": "340282366920938463463374607431768211454"
}
```

### #/components/schemas/U64

```ts
{
  "type": "string",
  "format": "uint64",
  "description": "A string containing a 64-bit unsigned integer.\n\nWe represent u64 values as a string to ensure compatibility with languages such\nas JavaScript that do not parse u64s in JSON natively.\n",
  "example": "32425224034"
}
```

### #/components/schemas/UserTransaction

```ts
// A transaction submitted by a user to change the state of the blockchain
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  hash: string
  state_change_hash:#/components/schemas/HashValue
  event_root_hash:#/components/schemas/HashValue
  state_checkpoint_hash:#/components/schemas/HashValue
  gas_used:#/components/schemas/U64
  // Whether the transaction was successful
  success: boolean
  // The VM status of the transaction, can tell useful information in a failure
  vm_status: string
  accumulator_root_hash:#/components/schemas/HashValue
  // A final state change of a transaction on a resource or module
  changes: {
  }[]
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  sender: string
  sequence_number:#/components/schemas/U64
  max_gas_amount:#/components/schemas/U64
  gas_unit_price:#/components/schemas/U64
  expiration_timestamp_secs:#/components/schemas/U64
  // An enum of the possible transaction payloads
  payload: {
  }
  // An enum representing the different transaction signatures available
  signature: {
  }
  // An event from a transaction
  events: {
    guid: {
      creation_number:#/components/schemas/U64
      account_address:#/components/schemas/Address
    }
    sequence_number:#/components/schemas/U64
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    type: string
  }[]
  timestamp:#/components/schemas/U64
}
```

### #/components/schemas/ValidatorTransaction

```ts
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  hash: string
  state_change_hash:#/components/schemas/HashValue
  event_root_hash:#/components/schemas/HashValue
  state_checkpoint_hash:#/components/schemas/HashValue
  gas_used:#/components/schemas/U64
  // Whether the transaction was successful
  success: boolean
  // The VM status of the transaction, can tell useful information in a failure
  vm_status: string
  accumulator_root_hash:#/components/schemas/HashValue
  // A final state change of a transaction on a resource or module
  changes: {
  }[]
  // An event from a transaction
  events: {
    guid: {
      creation_number:#/components/schemas/U64
      // A hex encoded 32 byte Aptos account address.
      // 
      // This is represented in a string as a 64 character hex string, sometimes
      // shortened by stripping leading 0s, and adding a 0x.
      // 
      // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
      // 
      account_address: string
    }
    sequence_number:#/components/schemas/U64
    // String representation of an on-chain Move type tag that is exposed in transaction payload.
    //     Values:
    //       - bool
    //       - u8
    //       - u16
    //       - u32
    //       - u64
    //       - u128
    //       - u256
    //       - address
    //       - signer
    //       - vector: `vector<{non-reference MoveTypeId}>`
    //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
    // 
    //     Vector type value examples:
    //       - `vector<u8>`
    //       - `vector<vector<u64>>`
    //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
    // 
    //     Struct type value examples:
    //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
    //       - `0x1::account::Account`
    // 
    //     Note:
    //       1. Empty chars should be ignored when comparing 2 struct tag ids.
    //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    type: string
  }[]
  timestamp:#/components/schemas/U64
}
```

### #/components/schemas/VersionedEvent

```ts
// An event from a transaction with a version
{
  // A string containing a 64-bit unsigned integer.
  // 
  // We represent u64 values as a string to ensure compatibility with languages such
  // as JavaScript that do not parse u64s in JSON natively.
  // 
  version: string
  guid: {
    creation_number:#/components/schemas/U64
    // A hex encoded 32 byte Aptos account address.
    // 
    // This is represented in a string as a 64 character hex string, sometimes
    // shortened by stripping leading 0s, and adding a 0x.
    // 
    // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
    // 
    account_address: string
  }
  sequence_number:#/components/schemas/U64
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type: string
}
```

### #/components/schemas/ViewRequest

```ts
// View request for the Move View Function API
{
  // Entry function id is string representation of a entry function defined on-chain.
  // 
  // Format: `{address}::{module name}::{function name}`
  // 
  // Both `module name` and `function name` are case-sensitive.
  // 
  function: string
  // String representation of an on-chain Move type tag that is exposed in transaction payload.
  //     Values:
  //       - bool
  //       - u8
  //       - u16
  //       - u32
  //       - u64
  //       - u128
  //       - u256
  //       - address
  //       - signer
  //       - vector: `vector<{non-reference MoveTypeId}>`
  //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
  // 
  //     Vector type value examples:
  //       - `vector<u8>`
  //       - `vector<vector<u64>>`
  //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
  // 
  //     Struct type value examples:
  //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
  //       - `0x1::account::Account`
  // 
  //     Note:
  //       1. Empty chars should be ignored when comparing 2 struct tag ids.
  //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
  // 
  type_arguments?: string[]
[]
}
```

### #/components/schemas/WriteModule

```ts
// Write a new module or update an existing one
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  address: string
  // State key hash
  state_key_hash: string
  // Move module bytecode along with it's ABI
  data: {
    // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
    // two hex digits per byte.
    // 
    // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
    // 
    bytecode: string
    // A Move module
    abi: {
      address:#/components/schemas/Address
      name: string
      // Move module id is a string representation of Move module.
      // 
      // Format: `{address}::{module name}`
      // 
      // `address` should be hex-encoded 32 byte account address that is prefixed with `0x`.
      // 
      // Module name is case-sensitive.
      // 
      friends?: string[]
      // Move function
      exposed_functions: {
        name:#/components/schemas/IdentifierWrapper
        // Move function visibility
        visibility: enum[private, public, friend]
        // Whether the function can be called as an entry function directly in a transaction
        is_entry: boolean
        // Whether the function is a view function or not
        is_view: boolean
        // Move function generic type param
        generic_type_params: {
          constraints?: string[]
        }[]
        // String representation of an on-chain Move type tag that is exposed in transaction payload.
        //     Values:
        //       - bool
        //       - u8
        //       - u16
        //       - u32
        //       - u64
        //       - u128
        //       - u256
        //       - address
        //       - signer
        //       - vector: `vector<{non-reference MoveTypeId}>`
        //       - struct: `{address}::{module_name}::{struct_name}::<{generic types}>`
        // 
        //     Vector type value examples:
        //       - `vector<u8>`
        //       - `vector<vector<u64>>`
        //       - `vector<0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>>`
        // 
        //     Struct type value examples:
        //       - `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>
        //       - `0x1::account::Account`
        // 
        //     Note:
        //       1. Empty chars should be ignored when comparing 2 struct tag ids.
        //       2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
        // 
        params?: string[]
        return:#/components/schemas/MoveType[]
      }[]
      // A move struct
      structs: {
        name:#/components/schemas/IdentifierWrapper
        // Whether the struct is a native struct of Move
        is_native: boolean
        abilities:#/components/schemas/MoveAbility[]
        // Move generic type param
        generic_type_params: {
          constraints:#/components/schemas/MoveAbility[]
        }[]
        // Move struct field
        fields: {
          name:#/components/schemas/IdentifierWrapper
          type:#/components/schemas/MoveType
        }[]
      }[]
    }
  }
}
```

### #/components/schemas/WriteResource

```ts
// Write a resource or update an existing one
{
  // A hex encoded 32 byte Aptos account address.
  // 
  // This is represented in a string as a 64 character hex string, sometimes
  // shortened by stripping leading 0s, and adding a 0x.
  // 
  // For example, address 0x0000000000000000000000000000000000000000000000000000000000000001 is represented as 0x1.
  // 
  address: string
  // State key hash
  state_key_hash: string
  // A parsed Move resource
  data: {
    // String representation of a MoveStructTag (on-chain Move struct type). This exists so you
    // can specify MoveStructTags as path / query parameters, e.g. for get_events_by_event_handle.
    // 
    // It is a combination of:
    //   1. `move_module_address`, `module_name` and `struct_name`, all joined by `::`
    //   2. `struct generic type parameters` joined by `, `
    // 
    // Examples:
    //   * `0x1::coin::CoinStore<0x1::aptos_coin::AptosCoin>`
    //   * `0x1::account::Account`
    // 
    // Note:
    //   1. Empty chars should be ignored when comparing 2 struct tag ids.
    //   2. When used in an URL path, should be encoded by url-encoding (AKA percent-encoding).
    // 
    // See [doc](https://aptos.dev/concepts/accounts) for more details.
    // 
    type: string
    // This is a JSON representation of some data within an account resource. More specifically,
    // it is a map of strings to arbitrary JSON values / objects, where the keys are top level
    // fields within the given resource.
    // 
    // To clarify, you might query for 0x1::account::Account and see the example data.
    // 
    // Move `bool` type value is serialized into `boolean`.
    // 
    // Move `u8`, `u16` and `u32` type value is serialized into `integer`.
    // 
    // Move `u64`, `u128` and `u256` type value is serialized into `string`.
    // 
    // Move `address` type value (32 byte Aptos account address) is serialized into a HexEncodedBytes string.
    // For example:
    //   - `0x1`
    //   - `0x1668f6be25668c1a17cd8caf6b8d2f25`
    // 
    // Move `vector` type value is serialized into `array`, except `vector<u8>` which is serialized into a
    // HexEncodedBytes string with `0x` prefix.
    // For example:
    //   - `vector<u64>{255, 255}` => `["255", "255"]`
    //   - `vector<u8>{255, 255}` => `0xffff`
    // 
    // Move `struct` type value is serialized into `object` that looks like this (except some Move stdlib types, see the following section):
    //   ```json
    //   {
    //     field1_name: field1_value,
    //     field2_name: field2_value,
    //     ......
    //   }
    //   ```
    // 
    // For example:
    //   `{ "created": "0xa550c18", "role_id": "0" }`
    // 
    // **Special serialization for Move stdlib types**:
    //   - [0x1::string::String](https://github.com/aptos-labs/aptos-core/blob/main/language/move-stdlib/docs/ascii.md)
    //     is serialized into `string`. For example, struct value `0x1::string::String{bytes: b"Hello World!"}`
    //     is serialized as `"Hello World!"` in JSON.
    // 
    data: {
    }
  }
}
```

### #/components/schemas/WriteSet

```ts
// The associated writeset with a payload
{
}
```

### #/components/schemas/WriteSetChange

```ts
// A final state change of a transaction on a resource or module
{
}
```

### #/components/schemas/WriteSetChange_DeleteModule

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "delete_module"
        }
      }
    },
    {
      "$ref": "#/components/schemas/DeleteModule"
    }
  ]
}
```

### #/components/schemas/WriteSetChange_DeleteResource

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "delete_resource"
        }
      }
    },
    {
      "$ref": "#/components/schemas/DeleteResource"
    }
  ]
}
```

### #/components/schemas/WriteSetChange_DeleteTableItem

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "delete_table_item"
        }
      }
    },
    {
      "$ref": "#/components/schemas/DeleteTableItem"
    }
  ]
}
```

### #/components/schemas/WriteSetChange_WriteModule

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "write_module"
        }
      }
    },
    {
      "$ref": "#/components/schemas/WriteModule"
    }
  ]
}
```

### #/components/schemas/WriteSetChange_WriteResource

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "write_resource"
        }
      }
    },
    {
      "$ref": "#/components/schemas/WriteResource"
    }
  ]
}
```

### #/components/schemas/WriteSetChange_WriteTableItem

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "write_table_item"
        }
      }
    },
    {
      "$ref": "#/components/schemas/WriteTableItem"
    }
  ]
}
```

### #/components/schemas/WriteSetPayload

```ts
// A writeset payload, used only for genesis
{
  // The associated writeset with a payload
  write_set: {
  }
}
```

### #/components/schemas/WriteSet_DirectWriteSet

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "direct_write_set"
        }
      }
    },
    {
      "$ref": "#/components/schemas/DirectWriteSet"
    }
  ]
}
```

### #/components/schemas/WriteSet_ScriptWriteSet

```ts
{
  "allOf": [
    {
      "type": "object",
      "required": [
        "type"
      ],
      "properties": {
        "type": {
          "type": "string",
          "example": "script_write_set"
        }
      }
    },
    {
      "$ref": "#/components/schemas/ScriptWriteSet"
    }
  ]
}
```

### #/components/schemas/WriteTableItem

```ts
// Change set to write a table item
{
  state_key_hash: string
  // All bytes (Vec<u8>) data is represented as hex-encoded string prefixed with `0x` and fulfilled with
  // two hex digits per byte.
  // 
  // Unlike the `Address` type, HexEncodedBytes will not trim any zeros.
  // 
  handle: string
  key:#/components/schemas/HexEncodedBytes
  value:#/components/schemas/HexEncodedBytes
  // Decoded table data
  data: {
    // Type of key
    key_type: string
    // Type of value
    value_type: string
  }
}
```
