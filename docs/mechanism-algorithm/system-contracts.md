# System Contracts
The TRON network supports many different types of transactions, such as TRX transfer transactions, TRC10 transfer transactions, creating smart contract transactions, triggering smart contract transactions, staking TRX transactions, and more. To create different types of transactions, you need to call different API. For example, the type of smart contract deployment transaction is `CreateSmartContract`, you need to call `wallet/deploycontractAPI` to create a transaction; the type of stake TRX transactions is `FreezeBalanceV2Contract`, you need to call` wallet/freezebalancev2API` to create transactions, we collectively refer to the implementation of these different transaction types as system contracts, the following are the types of system contracts and their contents:

## 1. AccountCreateContract
```
    message AccountCreateContract {
      bytes owner_address = 1;
      bytes account_address = 2;
      AccountType type = 3;
    }
```

- `owner_address`: The owner of the current account.
- `account_address`: The target address to create.
- `type`: Account type. 0 means normal account; 1 means the Genesis account; 2 means smart contract account.

## 2. TransferContract
```
    message TransferContract {
      bytes owner_address = 1;
      bytes to_address = 2;
      int64 amount = 3;
    }
```

- `owner_address`: The owner of the current account.
- `to_address`: The target address to transfer.
- `amount`: The amount of TRX to transfer.

## 3. TransferAssetContract
```
    message TransferAssetContract {
      bytes asset_name = 1;
      bytes owner_address = 2;
      bytes to_address = 3;
      int64 amount = 4;
    }
```

- `asset_name`: The token id to transfer.
- `owner_address`: The owner of the current account.
- `to_address`: The target address to transfer.
- `amount`: The amount of token to transfer.

## 4. VoteWitnessContract
```
    message VoteWitnessContract {
      message Vote {
        bytes vote_address = 1;
        int64 vote_count = 2;
      }
      bytes owner_address = 1;
      repeated Vote votes = 2;
      bool support = 3;
    }
```

- `owner_address`: The owner of the current account.
- `vote_address`: The SR or candidate's address.
- `vote_count`: The votes number.
- `support`: Constant true, not used.

## 5. WitnessCreateContract
```
    message WitnessCreateContract {
      bytes owner_address = 1;
      bytes url = 2;
    }
```

- `owner_address`: The owner of the current account.
- `url`: The website url of the witness.

## 6. AssetIssueContract
```
    message AssetIssueContract {
      message FrozenSupply {
        int64 frozen_amount = 1;
        int64 frozen_days = 2;
      }
      bytes owner_address = 1;
      bytes name = 2;
      bytes abbr = 3;
      int64 total_supply = 4;
      repeated FrozenSupply frozen_supply = 5;
      int32 trx_num = 6;
      int32 num = 8;
      int64 start_time = 9;
      int64 end_time = 10;
      int64 order = 11; // the order of tokens of the same name
      int32 vote_score = 16;
      bytes description = 20;
      bytes url = 21;
      int64 free_asset_net_limit = 22;
      int64 public_free_asset_net_limit = 23;
      int64 public_free_asset_net_usage = 24;
      int64 public_latest_free_net_time = 25;
    }
```

- `owner_address`: The owner of the current account.
- `name`: The token name to issue.
- `abbr`: The abbreviation of the token name.
- `total_supply`: The amount of token to issue.
- `frozen_supply`: The amount of token and staked days to stake.
- `trx_num`: trx_num/num defines the token price.
- `num`: trx_num/num defines the token price.
- `start_time`: ICO starts time.
- `end_time`: ICO ends time.
- `order`: Deprecated.
- `vote_score`: Deprecated.
- `description`: The description of the token.
- `url`: The website url of the token.
- `free_asset_net_limit`: The free bandwidth limit each account owns when transfers asset.
- `public_free_asset_net_limit`: The free bandwidth limit all the accounts can use.
- `public_free_asset_net_usage`: The free bandwidth usage of all the accounts.
- `public_latest_free_net_time`: The latest bandwidth consumption time of token transfer.

## 7. WitnessUpdateContract
```
    message WitnessUpdateContract {
      bytes owner_address = 1;
      bytes update_url = 12;
    }
```

- `owner_address`: The owner of the current account.
- `update_url`: The website url of the witness.

## 8. ParticipateAssetIssueContract
```
    message ParticipateAssetIssueContract {
      bytes owner_address = 1;
      bytes to_address = 2;
      bytes asset_name = 3;
      int64 amount = 4;
    }
```

- `owner_address`: The owner of the current account.
- `to_address`: The token owner address.
- `account_name`: The token id.
- `amount`: The amount of token to purchase.

## 9. AccountUpdateContract
```
    // Update account name. Account name is unique now.
    message AccountUpdateContract {
      bytes account_name = 1;
      bytes owner_address = 2;
    }
```

- `owner_address`: The owner of the current account.
- `account_name`: Account name.

## 10. FreezeBalanceContract
```
    message FreezeBalanceContract {
      bytes owner_address = 1;
      int64 frozen_balance = 2;
      int64 frozen_duration = 3;
      ResourceCode resource = 10;
      bytes receiver_address = 15;
    }
```

- `owner_address`: The owner of the current account.
- `frozen_balance`: The amount of TRX to stake.
- `frozen_duration`: The stake duration.
- `resource`: The type of resource get by staking TRX.
- `receiver_address`: The account address to receive resource.

## 11. UnfreezeBalanceContract
```
    message UnfreezeBalanceContract {
      bytes owner_address = 1;
      ResourceCode resource = 10;
      bytes receiver_address = 13;
    }
```

- `owner_address`: The owner of the current account.
- `resource`: The type of resource to unfree.
- `receiver_address`: The account address to receive resource.

## 12. WithdrawBalanceContract
```
    message WithdrawBalanceContract {
      bytes owner_address = 1;
    }
```

- `owner_address`: The owner of the current account.

## 13. UnfreezeAssetContract
```
    message UnfreezeAssetContract {
      bytes owner_address = 1;
    }
```

- `owner_address`: The owner of the current account.

## 14. UpdateAssetContract
```
    message UpdateAssetContract {
      bytes owner_address = 1;
      bytes description = 2;
      bytes url = 3;
      int64 new_limit = 4;
      int64 new_public_limit = 5;
    }
```

- `owner_address`: The owner of the current account.
- `description`: The description of the token.
- `url`: The website url of the token.
- `new_limit`: The bandwidth consumption limit of each account when transfers asset.
- `new_public_limit`: The bandwidth consumption limit of the accounts.

## 15. ProposalCreateContract
```
    message ProposalCreateContract {
      bytes owner_address = 1;
      map<int64, int64> parameters = 2;
    }
```

- `owner_address`: The owner of the current account.
- `parameters`: The proposal.

## 16. ProposalApproveContract
```
    message ProposalApproveContract {
      bytes owner_address = 1;
      int64 proposal_id = 2;
      bool is_add_approval = 3; // add or remove approval
    }
```

- `owner_address`: The owner of the current account.
- `proposal_id`: The proposal id.
- `is_add_approval`: Whether to approve.

## 17. ProposalDeleteContract
```
    message ProposalDeleteContract {
      bytes owner_address = 1;
      int64 proposal_id = 2;
    }
```

- `owner_address`: The owner of the current account.
- `proposal_id`: The proposal id.

## 18. SetAccountIdContract
```
    // Set account id if the account has no id. Account id is unique and case insensitive.
    message SetAccountIdContract {
      bytes account_id = 1;
      bytes owner_address = 2;
    }
```

- `owner_address`: The owner of the current account.
- `account_id`: The account id.

## 19. CreateSmartContract
```
    message CreateSmartContract {
      bytes owner_address = 1;
      SmartContract new_contract = 2;
      int64 call_token_value = 5;
      int64 token_id = 6;
    }
```

- `owner_address`: The owner of the current account.
- `new_contract`: the smart contract.
- `call_token_value` : The amount of TRC-10 token to send to the contract when triggers.
- `token_id` : The id of the TRC-10 token to be sent to the contract.

## 20. TriggerSmartContract
```
    message TriggerSmartContract {
      bytes owner_address = 1;
      bytes contract_address = 2;
      int64 call_value = 3;
      bytes data = 4;
      int64 call_token_value = 5;
      int64 token_id = 6;
    }
```

- `owner_address`: The owner of the current account.
- `contract_address`: The contract address.
- `call_value`: The amount of TRX to send to the contract when triggers.
- `data`: The parameters to trigger the contract.
- `call_token_value` : The amount of TRC-10 token to send to the contract when triggers.
- `token_id` : The id of the TRC-10 token to be sent to the contract.

## 21. UpdateSettingContract
```
    message UpdateSettingContract {
      bytes owner_address = 1;
      bytes contract_address = 2;
      int64 consume_user_resource_percent = 3;
    }
```

- `owner_address`: The owner of the current account.
- `contract_address`: The address of the smart contract.
- `consume_user_resource_percent`: The percentage of resource consumption ratio.

## 22. ExchangeCreateContract
```
    message ExchangeCreateContract {
      bytes owner_address = 1;
      bytes first_token_id = 2;
      int64 first_token_balance = 3;
      bytes second_token_id = 4;
      int64 second_token_balance = 5;
    }
```

- `owner_address`: The owner of the current account.
- `first_token_id`: First token id.
- `first_token_balance`: First token balance.
- `second_token_id`: Second token id.
- `second_token_balance`: Second token balance.

## 23. ExchangeInjectContract
```
    message ExchangeInjectContract {
      bytes owner_address = 1;
      int64 exchange_id = 2;
      bytes token_id = 3;
      int64 quant = 4;
    }
```

- `owner_address`: The owner of the current account.
- `exchange_id`: The token pair id.
- `token_id`: The token id to inject.
- `quant`: The token amount to inject.

## 24. ExchangeWithdrawContract
```
    message ExchangeWithdrawContract {
      bytes owner_address = 1;
      int64 exchange_id = 2;
      bytes token_id = 3;
      int64 quant = 4;
    }
```

- `owner_address`: The owner of the current account.
- `exchange_id`: The token pair id.
- `token_id`: The token id to withdraw.
- `quant`: The token amount to withdraw.

## 25. ExchangeTransactionContract
```
    message ExchangeTransactionContract {
      bytes owner_address = 1;
      int64 exchange_id = 2;
      bytes token_id = 3;
      int64 quant = 4;
    }
```

- `owner_address`: The owner of the current account.
- `exchange_id`: The token pair id.
- `token_id`: The token id to sell.
- `quant`: The token amount to sell.

## 26. ShieldedTransferContract
```
    message ShieldedTransferContract {
      bytes transparent_from_address = 1;
      int64 from_amount = 2;
      repeated SpendDescription spend_description = 3;
      repeated ReceiveDescription receive_description = 4;
      bytes binding_signature = 5;
      bytes transparent_to_address = 6;
      int64 to_amount = 7;
    }
```

- `transparent_from_address`: The transparent address of the sender.
- `from_amount`: The amount to send.
- `spend_description`: Shielded spend information.
- `receive_description`: Shielded receive information.
- `binding_signature`: The binding signature.
- `transparent_to_address`: The transparent address of the receiver.
- `to_amount`: The amount to receive.

```
message SpendDescription {
  bytes value_commitment = 1;
  bytes anchor = 2;
  bytes nullifier = 3;
  bytes rk = 4;
  bytes zkproof = 5;
  bytes spend_authority_signature = 6;
}
```

- `value_commitment`: _value commitment_ of spender's transfer amount.
- `anchor`: root of the note commitment Merkle tree at some block.
- `nullifier`: _nullifier_ of spender's note, to prevent double-spent.
- `rk`: public key, to verify spender's _Spend Authorization Signature_.
- `zkproof`: zero-knowledge proof of spender's note, prove that this note exists and could be spent.
- `spend_authority_signature`: the spender's _Spend Authorization Signature_.

```
message ReceiveDescription {
  bytes value_commitment = 1;
  bytes note_commitment = 2;
  bytes epk = 3;
  bytes c_enc = 4;
  bytes c_out = 5;
  bytes zkproof = 6;
}
```

- `value_commitment`: _value commitment_ of receiver's transfer amount.
- `note_commitment`: commitment of the receiver's not.
- `epk`: ephemeral public key, in order to generate note's decryption key.
- `c_enc`: part of note ciphertext, encryption of diversifier, receiver's transfer amount, rcm, and memo.
- `c_out`: part of note ciphertext, encryption of the receiver's public key and ephemeral private key.
- `zkproof`: zero-knowledge proof of the receiver's note.

## 27. Multi Signature

[Multi-Signature](./multi-signatures.md)

## 28. ClearABIContract
```
    message ClearABIContract {
      bytes owner_address = 1;
      bytes contract_address = 2;
    }
```

- `owner_address`: The owner of the current account.
- `account_address`: The target contract address to clear ABI.

## 29. UpdateBrokerageContract
```
    message UpdateBrokerageContract {
      bytes owner_address = 1;
      int32 brokerage = 2;
    }
```

- `owner_address`: The owner of the current account.
- `brokerage`: Commission rate, from 0 to 100,1 mean 1%.

## 30. UpdateEnergyLimitContract
```
    message UpdateEnergyLimitContract {
      bytes owner_address = 1;
      bytes contract_address = 2;
      int64 origin_energy_limit = 3;
    }
```

- `owner_address`: The owner of the current account.
- `contract_address`: The contract address.
- `origin_energy_limit`: The target energy limit to change.

## 31. FreezeBalanceV2Contract

```protobuf
     message FreezeBalanceV2Contract {
      bytes owner_address = 1;
      int64 frozen_balance = 2;
      ResourceCode resource = 3;
      }
```

* `owner_address`：Owner address
* `frozen_balance`：TRX stake amount, the unit is sun
* `resource`： Resource type

## 32. UnfreezeBalanceV2Contract

```protobuf
      message UnfreezeBalanceV2Contract {
       bytes owner_address = 1;
       int64 unfreeze_balance = 2;
       ResourceCode resource = 3;
      }
```

* `owner_address`：Owner address
* `unfreeze_balance`：The amount of TRX to unstake, in sun
* `resource`： Resource type
   

## 33. WithdrawExpireUnfreezeContract

```protobuf
      message WithdrawExpireUnfreezeContract {
        bytes owner_address = 1;
      }
```

* `owner_address`：Owner address
   
## 34. DelegateResourceContract

```protobuf
      message DelegateResourceContract {
      bytes owner_address = 1;
      ResourceCode resource = 2;
      int64 balance = 3;
      bytes receiver_address = 4;
      bool  lock = 5;
      }
```

* `owner_address`：Owner address
* `resource`： Resource type
* `balance`： Amount of TRX staked for resources to be delegated, unit is sun
* `receiver_address`：Resource receiver address
* `lock`：Whether it is locked, if it is set to true, the delegated resources cannot be undelegated within 3 days. When the lock time is not over, if the owner delegates the same type of resources using the lock to the same address, the lock time will be reset to 3 days
   
   
## 35. UnDelegateResourceContract

```protobuf
      message UnDelegateResourceContract {
      bytes owner_address = 1;
      ResourceCode resource = 2;
      int64 balance = 3;
      bytes receiver_address = 4;
      }
```

* `owner_address`：Owner address
* `resource`： Resource type
* `balance`：undelegated TRX, unit is sun
* `receiver_address`：Resource receiver address
   







