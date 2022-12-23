# BulletproofVM
Rust based Virtual Machine on Avalanche that implements Bulletproof ZK Proofs. 


# Zero-Knowledge Virtual Machine
This is a virtual machine (VM) implemented in Rust that allows you to execute transactions with zero-knowledge (ZK) proofs. The VM maintains a state consisting of accounts with balances and assets, and supports several types of transactions, including standard transactions for transferring assets between two accounts, smart contract transactions for executing arbitrary code on a contract account, multi-asset transactions for transferring multiple different assets between two accounts, and decentralized governance transactions for proposing and voting on changes to the system.

# Features
- Maintains a state consisting of accounts with balances and assets
- Executes standard transactions for transferring assets between two accounts
- Executes smart contract transactions for executing arbitrary code on a contract account
- Executes multi-asset transactions for transferring multiple different assets between two accounts
- Executes decentralized governance transactions for proposing and voting on changes to the system
- Uses zero-knowledge (ZK) proofs to ensure the correctness and privacy of transactions

# Dependencies
- Rust 1.51 or higher
- The curve25519-dalek library for implementing elliptic curve cryptography
- The rand library for generating randomness
- The bulletproofs library for implementing Bulletproof ZK proofs

# Usage
- To use the VM, create a new instance of the MyVirtualMachine struct and use its methods to create new accounts and execute transactions: 
'''
use zk_vm::{
    codec::{Codec, Decode, Encode},
    execution::{Execution, Executable},
    MyVirtualMachine,
    MyTransaction,
    SmartContractTransaction,
    MultiAssetTransaction,
    DecentralizedGovernanceTransaction,
    KeyPair,
    PublicKey,
};

// Create a new instance of the VM
let mut vm = MyVirtualMachine::new();

// Generate keypair for the sender and recipient
let sender_keypair = KeyPair::generate();
let recipient_keypair = KeyPair::generate();

// Create accounts for the sender and recipient
vm.create_account(sender_keypair);
vm.create_account(recipient_keypair);

// Construct a MyTransaction to transfer 100 units from the sender to the recipient
let tx = MyTransaction {
    sender: sender_keypair.public,
    recipient: recipient_keypair.public,
    amount: 100,
    proof: Proof::new(BulletproofGroth16),
};

// Serialize the transaction to a byte array
let bytes = tx.encode();

// Deserialize the transaction from the byte array
let tx = MyTransaction::decode(&bytes).unwrap();

// Execute the transaction on the VM
vm.execute(&tx).unwrap();

// Check the balances of the sender and recipient
let sender_account = vm.get_account(sender_keypair.public).unwrap();
assert_eq!(sender_account.balance, 900);
let recipient_account = vm.get_account(recipient_keypair.public).unwrap();
assert_eq!(recipient_account.balance, 100);
'''

You can also execute other types of transactions, such as smart contract transactions, multi-asset transactions, and decentralized governance transactions, using the same process.

# License
This project is licensed under the MIT License.
