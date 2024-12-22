# Starknet: Counter smart contract

A simple counter smart contract built on Starknet that demonstrates basic storage management, events, and access control. The contract allows users to increment and decrement a counter value, while maintaining ownership controls.

## Features
- Get the current counter value
- Increase the counter by 1
- Decrease the counter by 1 (with checks to prevent negative values)
- Reset the counter to 0 (owner-only function)
- Event emission for tracking changes
- Access control using OpenZeppelin's ownable component

## Contract Address
Deployed on Sepolia testnet: [0x0759108261aab68ebf8a032fd29db4a2e5fb779fd7a1589aeac10cbae0b79248](https://sepolia.starkscan.co/contract/0x0759108261aab68ebf8a032fd29db4a2e5fb779fd7a1589aeac10cbae0b79248#read-write-contract)

### Build the Contract
```bash
scarb build
```

### Account Setup
1. Create a new keystore:
```bash
starkli signer keystore new keystore.json
```

2. Initialize the account:
```bash
starkli account oz init account.json --keystore keystore.json
```

3. Deploy the account:
```bash
starkli account deploy --account account.json --keystore keystore.json
```

### Contract Deployment
1. Declare the contract to get the class hash:
```bash
starkli declare --account account.json --keystore keystore.json <CONTRACT_PATH>
```
> Note: The class hash will be available in `/target/dev/*.contract_class.json`

2. Deploy the contract:
```bash
starkli deploy --account account.json --keystore keystore.json <CLASS_HASH> <INITIAL_COUNT> <OWNER_ADDRESS>
```

The class hash can be found in `/target/dev` and use the `*.contract_class.json` file.

Deploy the contract:
```
starkli deploy --account account.json --keystore keystore.json <CLASS_HASH> <ARGS>
```

In this case `ARGS` is the initial value of the counter and the owner's address.

### Contract Interaction
Query the current counter value:
```bash
starkli call 0x0759108261aab68ebf8a032fd29db4a2e5fb779fd7a1589aeac10cbae0b79248 get_counter
```


Invoke the contract:

```bash
starkli invoke --account account.json --keystore keystore.json 0x0759108261aab68ebf8a032fd29db4a2e5fb779fd7a1589aeac10cbae0b79248 increase_counter 
```