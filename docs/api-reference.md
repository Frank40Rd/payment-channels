# API Reference for Asynchronous Payment Channel

## Introduction

This API reference provides detailed information on the available functions and their parameters for the asynchronous payment channel. The payment channel allows two parties to make a series of payments instantaneously, free of charge, without the necessity to commit all transactions into the blockchain and with reasonable guarantees.

## Functions

### `top_up_balance`

The `top_up_balance` function allows parties to top up their balances in the payment channel.

**Parameters:**
- `add_A`: Coins to be added to party A's balance.
- `add_B`: Coins to be added to party B's balance.

Example code:
```python
top_up_balance(add_A=<add_A>, add_B=<add_B>)
```

### `init_channel`

The `init_channel` function initializes the payment channel with the provided parameters. It sets the initial balances, keys, and channel ID, and ensures that the contract is properly initialized.

**Parameters:**
- `is_A`: Boolean value indicating whether the caller is party A.
- `signature`: Signature of the caller.
- `tag`: Tag value (0x696e6974).
- `channel_id`: Unique identifier for the payment channel.
- `balance_A`: Initial balance of party A.
- `balance_B`: Initial balance of party B.

Example code:
```python
init_channel(is_A=True, signature=<signature>, tag=0x696e6974, channel_id=<channel_id>, balance_A=<balance_A>, balance_B=<balance_B>)
```

### `cooperative_close`

The `cooperative_close` function closes the payment channel cooperatively. Both parties must sign the close request with the final state, and the function distributes the funds accordingly.

**Parameters:**
- `sig_A`: Signature of party A.
- `sig_B`: Signature of party B.
- `tag`: Tag value (0x436c6f73).
- `channel_id`: Unique identifier for the payment channel.
- `balance_A`: Final balance of party A.
- `balance_B`: Final balance of party B.
- `seqno_A`: Final sequence number of party A.
- `seqno_B`: Final sequence number of party B.

Example code:
```python
cooperative_close(sig_A=<sig_A>, sig_B=<sig_B>, tag=0x436c6f73, channel_id=<channel_id>, balance_A=<final_balance_A>, balance_B=<final_balance_B>, seqno_A=<final_seqno_A>, seqno_B=<final_seqno_B>)
```

### `cooperative_commit`

The `cooperative_commit` function commits the current state of the payment channel cooperatively. Both parties must sign the commit request with the current state, and the function updates the committed state in the contract.

**Parameters:**
- `sig_A`: Signature of party A.
- `sig_B`: Signature of party B.
- `tag`: Tag value (0x43436d74).
- `channel_id`: Unique identifier for the payment channel.
- `seqno_A`: Current sequence number of party A.
- `seqno_B`: Current sequence number of party B.

Example code:
```python
cooperative_commit(sig_A=<sig_A>, sig_B=<sig_B>, tag=0x43436d74, channel_id=<channel_id>, seqno_A=<current_seqno_A>, seqno_B=<current_seqno_B>)
```

### `start_uncooperative_close`

The `start_uncooperative_close` function initiates the uncooperative closure process. It submits the latest known states signed by each party and starts the grace period for challenging the state.

**Parameters:**
- `signed_by_A`: Boolean value indicating whether the closure is initiated by party A.
- `signature`: Signature of the initiator.
- `tag`: Tag value (0x556e436c).
- `channel_id`: Unique identifier for the payment channel.
- `sch_A`: Signed semi-channel state of party A.
- `sch_B`: Signed semi-channel state of party B.

Example code:
```python
start_uncooperative_close(signed_by_A=True, signature=<signature>, tag=0x556e436c, channel_id=<channel_id>, sch_A=<signed_state_A>, sch_B=<signed_state_B>)
```

### `challenge_quarantined_state`

The `challenge_quarantined_state` function allows the counterparty to challenge the final state submitted by the uncooperative closure initiator. It checks the validity of the challenge and updates the state if necessary.

**Parameters:**
- `challenged_by_A`: Boolean value indicating whether the challenge is initiated by party A.
- `signature`: Signature of the challenger.
- `tag`: Tag value (0x43686751).
- `channel_id`: Unique identifier for the payment channel.
- `sch_A`: Signed semi-channel state of party A.
- `sch_B`: Signed semi-channel state of party B.

Example code:
```python
challenge_quarantined_state(challenged_by_A=True, signature=<signature>, tag=0x43686751, channel_id=<channel_id>, sch_A=<signed_state_A>, sch_B=<signed_state_B>)
```

### `settle_conditionals`

The `settle_conditionals` function settles conditional payments after the final state is settled. It processes the conditionals and updates the state accordingly.

**Parameters:**
- `from_A`: Boolean value indicating whether the settlement is initiated by party A.
- `signature`: Signature of the initiator.
- `tag`: Tag value (0x436c436e).
- `channel_id`: Unique identifier for the payment channel.
- `conditionals_to_settle`: Hashmap of conditionals to settle.

Example code:
```python
settle_conditionals(from_A=True, signature=<signature>, tag=0x436c436e, channel_id=<channel_id>, conditionals_to_settle=<conditionals_to_settle>)
```

### `finish_uncooperative_close`

The `finish_uncooperative_close` function finishes the uncooperative closure process and distributes the funds according to the final state.

Example code:
```python
finish_uncooperative_close()
```

## Conclusion

This API reference provides detailed information on the available functions and their parameters for the asynchronous payment channel. By following this reference, you should be able to successfully interact with the payment channel contract. If you encounter any issues or have any questions, please refer to the user guide and developer guide for more detailed information.
