# User Guide for Asynchronous Payment Channel

## Introduction

This user guide provides step-by-step instructions on how to use the asynchronous payment channel. The payment channel allows two parties to make a series of payments instantaneously, free of charge, without the necessity to commit all transactions into the blockchain and with reasonable guarantees.

## Prerequisites

Before you start using the payment channel, ensure that you have the following:

1. A deployed payment channel contract on the blockchain.
2. The public keys of both parties (party A and party B).
3. The withdrawal addresses of both parties.
4. The initial balances of both parties.

## Step-by-Step Instructions

### Step 1: Initialize the Payment Channel

To initialize the payment channel, follow these steps:

1. Deploy the payment channel contract on the blockchain.
2. Call the `init_channel` function with the following parameters:
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

### Step 2: Make a Payment

To make a payment, follow these steps:

1. Generate a new semi-channel state with an increased `seqno` and `sent` amount.
2. Sign the new semi-channel state.
3. Send the signed semi-channel state to the counterparty.

Example code:
```python
new_state = generate_new_state(seqno=<new_seqno>, sent=<new_sent>)
signature = sign_state(new_state)
send_to_counterparty(new_state, signature)
```

### Step 3: Close the Channel Cooperatively

To close the payment channel cooperatively, follow these steps:

1. Both parties sign the close request with the final state.
2. Call the `cooperative_close` function with the following parameters:
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

### Step 4: Start Uncooperative Closure

To start the uncooperative closure process, follow these steps:

1. Get the latest semi-channel states signed by each party.
2. Call the `start_uncooperative_close` function with the following parameters:
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

### Step 5: Challenge Quarantined State

To challenge the quarantined state, follow these steps:

1. Get the latest semi-channel states signed by each party.
2. Call the `challenge_quarantined_state` function with the following parameters:
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

### Step 6: Settle Conditionals

To settle conditionals, follow these steps:

1. Get the conditionals to settle.
2. Call the `settle_conditionals` function with the following parameters:
   - `from_A`: Boolean value indicating whether the settlement is initiated by party A.
   - `signature`: Signature of the initiator.
   - `tag`: Tag value (0x436c436e).
   - `channel_id`: Unique identifier for the payment channel.
   - `conditionals_to_settle`: Hashmap of conditionals to settle.

Example code:
```python
settle_conditionals(from_A=True, signature=<signature>, tag=0x436c436e, channel_id=<channel_id>, conditionals_to_settle=<conditionals_to_settle>)
```

### Step 7: Finish Uncooperative Closure

To finish the uncooperative closure process, follow these steps:

1. Call the `finish_uncooperative_close` function.

Example code:
```python
finish_uncooperative_close()
```

## Conclusion

By following this user guide, you should be able to successfully use the asynchronous payment channel to make a series of payments between two parties. If you encounter any issues or have any questions, please refer to the developer guide and API reference for more detailed information.
