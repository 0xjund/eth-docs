# Solidity Documentation

## Release 0.8.

## Ethereum

**Aug 13, 2024**



## BASICS


- 1 Getting Started
- 2 Translations
- 3 Contents
   - 3.1 Introduction to Smart Contracts
   - 3.2 Solidity by Example
   - 3.3 Installing the Solidity Compiler
   - 3.4 Layout of a Solidity Source File
   - 3.5 Structure of a Contract
   - 3.6 Types
   - 3.7 Units and Globally Available Variables
   - 3.8 Expressions and Control Structures
   - 3.9 Contracts
   - 3.10 Inline Assembly
   - 3.11 Cheatsheet
   - 3.12 Language Grammar
   - 3.13 Using the Compiler
   - 3.14 Analysing the Compiler Output
   - 3.15 Solidity IR-based Codegen Changes
   - 3.16 Layout of State Variables in Storage and Transient Storage
   - 3.17 Layout in Memory
   - 3.18 Layout of Call Data
   - 3.19 Cleaning Up Variables
   - 3.20 Source Mappings
   - 3.21 The Optimizer
   - 3.22 Contract Metadata
   - 3.23 Contract ABI Specification
   - 3.24 Security Considerations
   - 3.25 List of Known Bugs
   - 3.26 Solidity v0.5.0 Breaking Changes
   - 3.27 Solidity v0.6.0 Breaking Changes
   - 3.28 Solidity v0.7.0 Breaking Changes
   - 3.29 Solidity v0.8.0 Breaking Changes
   - 3.30 NatSpec Format
   - 3.31 SMTChecker and Formal Verification
   - 3.32 Yul
   - 3.33 Import Path Resolution
   - 3.34 Style Guide
   - 3.35 Common Patterns
   - 3.36 Resources
   - 3.37 Contributing
   - 3.38 Language Influences
   - 3.39 Solidity Brand Guide
- Index


Solidity is an object-oriented, high-level language for implementing smart contracts. Smart contracts are programs that
govern the behavior of accounts within the Ethereum state.

Solidity is a curly-bracket language designed to target the Ethereum Virtual Machine (EVM). It is influenced by C++,
Python, and JavaScript. You can find more details about which languages Solidity has been inspired by in the _language
influences_ section.

Solidity is statically typed, supports inheritance, libraries, and complex user-defined types, among other features.

With Solidity, you can create contracts for uses such as voting, crowdfunding, blind auctions, and multi-signature
wallets.

When deploying contracts, you should use the latest released version of Solidity. Apart from exceptional cases, only the
latest version receives security fixes. Furthermore, breaking changes, as well as new features, are introduced regularly.
We currently use a 0.y.z version number to indicate this fast pace of change.

```
Warning: Solidity recently released the 0.8.x version that introduced a lot of breaking changes. Make sure you
read the full list.
```
Ideas for improving Solidity or this documentation are always welcome, read our _contributors guide_ for more details.

**Hint:** You can download this documentation as PDF, HTML or Epub by clicking on the versions flyout menu in the
bottom-left corner and selecting the preferred download format.

#### BASICS 1


#### 2 BASICS


#### CHAPTER

### ONE

## 1 Getting Started

**1. Understand the Smart Contract Basics**

If you are new to the concept of smart contracts, we recommend you to get started by digging into the “Introduction to
Smart Contracts” section, which covers the following:

- _A simple example smart contract_ written in Solidity.
- _Blockchain Basics_.
- _The Ethereum Virtual Machine_.
**2. Get to Know Solidity**

Once you are accustomed to the basics, we recommend you read the _“Solidity by Example”_ and “Language Description”
sections to understand the core concepts of the language.

**3. Install the Solidity Compiler**

There are various ways to install the Solidity compiler, simply choose your preferred option and follow the steps outlined
on the _installation page_.

**Hint:** You can try out code examples directly in your browser with the Remix IDE. Remix is a web browser-based IDE
that allows you to write, deploy and administer Solidity smart contracts, without the need to install Solidity locally.

```
Warning: As humans write software, it can have bugs. Therefore, you should follow established software develop-
ment best practices when writing your smart contracts. This includes code review, testing, audits, and correctness
proofs. Smart contract users are sometimes more confident with code than their authors, and blockchains and smart
contracts have their own unique issues to watch out for, so before working on production code, make sure you read
the Security Considerations section.
```
**4. Learn More**

If you want to learn more about building decentralized applications on Ethereum, the Ethereum Developer Resources
can help you with further general documentation around Ethereum, and a wide selection of tutorials, tools, and devel-
opment frameworks.

If you have any questions, you can try searching for answers or asking on the Ethereum StackExchange, or our Gitter
channel.

#### 3


**4 Chapter 1. Getting Started**


#### CHAPTER

### TWO

### TRANSLATIONS

Community contributors help translate this documentation into several languages. Note that they have varying degrees
of completeness and up-to-dateness. The English version stands as a reference.

You can switch between languages by clicking on the flyout menu in the bottom-left corner and selecting the preferred
language.

- Chinese
- French
- Indonesian
- Japanese
- Korean
- Persian
- Russian
- Spanish
- Turkish

**Note:** We set up a GitHub organization and translation workflow to help streamline the community efforts. Please
refer to the translation guide in the solidity-docs org for information on how to start a new language or contribute to
the community translations.

#### 5


**6 Chapter 2. Translations**


#### CHAPTER

### THREE

### CONTENTS

Keyword Index, Search Page

### 3.1 Introduction to Smart Contracts

**3.1.1 A Simple Smart Contract**

Let us begin with a basic example that sets the value of a variable and exposes it for other contracts to access. It is fine
if you do not understand everything right now, we will go into more details later.

**Storage Example**

// SPDX-License-Identifier: GPL-3.
pragma solidity >=0.4.16 <0.9.0;

contract SimpleStorage{
uintstoredData;

```
functionset(uintx) public{
storedData = x;
}
```
functionget()public viewreturns(uint) {
returnstoredData;
}
}

The first line tells you that the source code is licensed under the GPL version 3.0. Machine-readable license specifiers
are important in a setting where publishing the source code is the default.

The next line specifies that the source code is written for Solidity version 0.4.16, or a newer version of the language up
to, but not including version 0.9.0. This is to ensure that the contract is not compilable with a new (breaking) compiler
version, where it could behave differently. _Pragmas_ are common instructions for compilers about how to treat the
source code (e.g. pragma once).

A contract in the sense of Solidity is a collection of code (its _functions_ ) and data (its _state_ ) that resides at a specific
address on the Ethereum blockchain. The lineuint storedData;declares a state variable calledstoredDataof
typeuint( _u_ nsigned _int_ eger of _256_ bits). You can think of it as a single slot in a database that you can query and alter
by calling functions of the code that manages the database. In this example, the contract defines the functionssetand
getthat can be used to modify or retrieve the value of the variable.

#### 7


To access a member (like a state variable) of the current contract, you do not typically add thethis.prefix, you just
access it directly via its name. Unlike in some other languages, omitting it is not just a matter of style, it results in a
completely different way to access the member, but more on this later.

This contract does not do much yet apart from (due to the infrastructure built by Ethereum) allowing anyone to store
a single number that is accessible by anyone in the world without a (feasible) way to prevent you from publishing this
number. Anyone could callsetagain with a different value and overwrite your number, but the number is still stored
in the history of the blockchain. Later, you will see how you can impose access restrictions so that only you can alter
the number.

```
Warning: Be careful with using Unicode text, as similar looking (or even identical) characters can have different
code points and as such are encoded as a different byte array.
```
**Note:** All identifiers (contract names, function names and variable names) are restricted to the ASCII character set. It
is possible to store UTF-8 encoded data in string variables.

**Subcurrency Example**

The following contract implements the simplest form of a cryptocurrency. The contract allows only its creator to create
new coins (different issuance schemes are possible). Anyone can send coins to each other without a need for registering
with a username and password, all you need is an Ethereum keypair.

// SPDX-License-Identifier: GPL-3.
pragma solidity ^0.8.26;

// This will only compile via IR
contract Coin{
// The keyword "public" makes variables
// accessible from other contracts
address publicminter;
mapping(address=>uint) publicbalances;

```
// Events allow clients to react to specific
// contract changes you declare
eventSent(addressfrom, addressto,uint amount);
```
```
// Constructor code is only run when the contract
// is created
constructor() {
minter =msg.sender;
}
```
```
// Sends an amount of newly created coins to an address
// Can only be called by the contract creator
functionmint(addressreceiver,uintamount)public {
require(msg.sender== minter);
balances[receiver] += amount;
}
```
```
// Errors allow you to provide information about
(continues on next page)
```
**8 Chapter 3. Contents**


```
(continued from previous page)
// why an operation failed. They are returned
// to the caller of the function.
error InsufficientBalance(uintrequested, uintavailable);
```
// Sends an amount of existing coins
// from any caller to an address
functionsend(addressreceiver,uintamount)public {
require(amount <= balances[msg.sender], InsufficientBalance(amount, balances[msg.
˓→sender]));
balances[msg.sender] -= amount;
balances[receiver] += amount;
emit Sent(msg.sender, receiver, amount);
}
}

This contract introduces some new concepts, let us go through them one by one.

The lineaddress public minter;declares a state variable of type _address_. Theaddresstype is a 160-bit value
that does not allow any arithmetic operations. It is suitable for storing addresses of contracts, or a hash of the public
half of a keypair belonging to _external accounts_.

The keywordpublicautomatically generates a function that allows you to access the current value of the state variable
from outside of the contract. Without this keyword, other contracts have no way to access the variable. The code of
the function generated by the compiler is equivalent to the following (ignoreexternalandviewfor now):

functionminter()externalviewreturns(address) {return minter; }

You could add a function like the above yourself, but you would have a function and state variable with the same name.
You do not need to do this, the compiler figures it out for you.

The next line,mapping(address => uint) public balances;also creates a public state variable, but it is a more
complex datatype. The _mapping_ type maps addresses to _unsigned integers_.

Mappings can be seen as hash tables which are virtually initialized such that every possible key exists from the start
and is mapped to a value whose byte-representation is all zeros. However, it is neither possible to obtain a list of all
keys of a mapping, nor a list of all values. Record what you added to the mapping, or use it in a context where this is
not needed. Or even better, keep a list, or use a more suitable data type.

The _getter function_ created by thepublickeyword is more complex in the case of a mapping. It looks like the following:

functionbalances(addressaccount)externalviewreturns(uint) {
return balances[account];
}

You can use this function to query the balance of a single account.

The lineevent Sent(address from, address to, uint amount);declares an _“event”_ , which is emitted in
the last line of the functionsend. Ethereum clients such as web applications can listen for these events emitted on
the blockchain without much cost. As soon as it is emitted, the listener receives the argumentsfrom,toandamount,
which makes it possible to track transactions.

To listen for this event, you could use the following JavaScript code, which uses web3.js to create theCoincontract
object, and any user interface calls the automatically generatedbalancesfunction from above:

Coin.Sent().watch({},'',function(error, result) {
if (!error) {
(continues on next page)

**3.1. Introduction to Smart Contracts 9**


(continued from previous page)
console.log("Coin transfer: " + result.args.amount +
" coins were sent from " + result.args.from+
" to " + result.args.to + ".");
console.log("Balances now:\n" +
"Sender: " + Coin.balances.call(result.args.from) +
"Receiver: " + Coin.balances.call(result.args.to));
}
})

The _constructor_ is a special function that is executed during the creation of the contract and cannot be called afterwards.
In this case, it permanently stores the address of the person creating the contract. Themsgvariable (together withtx
andblock) is a _special global variable_ that contains properties which allow access to the blockchain.msg.senderis
always the address where the current (external) function call came from.

The functions that make up the contract, and that users and contracts can call aremintandsend.

Themintfunction sends an amount of newly created coins to another address. The _require_ function call defines
conditions that reverts all changes if not met. In this example,require(msg.sender == minter);ensures that only
the creator of the contract can callmint. In general, the creator can mint as many tokens as they like, but at some point,
this will lead to a phenomenon called “overflow”. Note that because of the default _Checked arithmetic_ , the transaction
would revert if the expressionbalances[receiver] += amount;overflows, i.e., whenbalances[receiver] +
amountin arbitrary precision arithmetic is larger than the maximum value ofuint(2**256 - 1). This is also true
for the statementbalances[receiver] += amount;in the functionsend.

_Errors_ allow you to provide more information to the caller about why a condition or operation failed. Errors are used
together with the _revert statement_. Therevertstatement unconditionally aborts and reverts all changes, much like
the _require function_. Both approaches allow you to provide the name of an error and additional data which will be
supplied to the caller (and eventually to the front-end application or block explorer) so that a failure can more easily be
debugged or reacted upon.

Thesendfunction can be used by anyone (who already has some of these coins) to send coins to anyone else. If the
sender does not have enough coins to send, theifcondition evaluates to true. As a result, therevertwill cause the
operation to fail while providing the sender with error details using theInsufficientBalanceerror.

**Note:** If you use this contract to send coins to an address, you will not see anything when you look at that address on a
blockchain explorer, because the record that you sent coins and the changed balances are only stored in the data storage
of this particular coin contract. By using events, you can create a “blockchain explorer” that tracks transactions and
balances of your new coin, but you have to inspect the coin contract address and not the addresses of the coin owners.

**10 Chapter 3. Contents**


**3.1.2 Blockchain Basics**

Blockchains as a concept are not too hard to understand for programmers. The reason is that most of the complications
(mining, hashing, elliptic-curve cryptography, peer-to-peer networks, etc.) are just there to provide a certain set of
features and promises for the platform. Once you accept these features as given, you do not have to worry about the
underlying technology - or do you have to know how Amazon’s AWS works internally in order to use it?

**Transactions**

A blockchain is a globally shared, transactional database. This means that everyone can read entries in the database
just by participating in the network. If you want to change something in the database, you have to create a so-called
transaction which has to be accepted by all others. The word transaction implies that the change you want to make
(assume you want to change two values at the same time) is either not done at all or completely applied. Furthermore,
while your transaction is being applied to the database, no other transaction can alter it.

As an example, imagine a table that lists the balances of all accounts in an electronic currency. If a transfer from one
account to another is requested, the transactional nature of the database ensures that if the amount is subtracted from
one account, it is always added to the other account. If due to whatever reason, adding the amount to the target account
is not possible, the source account is also not modified.

Furthermore, a transaction is always cryptographically signed by the sender (creator). This makes it straightforward
to guard access to specific modifications of the database. In the example of the electronic currency, a simple check
ensures that only the person holding the keys to the account can transfer some compensation, e.g. Ether, from it.

**Blocks**

One major obstacle to overcome is what (in Bitcoin terms) is called a “double-spend attack”: What happens if two
transactions exist in the network that both want to empty an account? Only one of the transactions can be valid,
typically the one that is accepted first. The problem is that “first” is not an objective term in a peer-to-peer network.

The abstract answer to this is that you do not have to care. A globally accepted order of the transactions will be selected
for you, solving the conflict. The transactions will be bundled into what is called a “block” and then they will be
executed and distributed among all participating nodes. If two transactions contradict each other, the one that ends up
being second will be rejected and not become part of the block.

These blocks form a linear sequence in time, and that is where the word “blockchain” derives from. Blocks are added
to the chain at regular intervals, although these intervals may be subject to change in the future. For the most up-to-date
information, it is recommended to monitor the network, for example, on Etherscan.

As part of the “order selection mechanism”, which is called attestation, it may happen that blocks are reverted from
time to time, but only at the “tip” of the chain. The more blocks are added on top of a particular block, the less likely
this block will be reverted. So it might be that your transactions are reverted and even removed from the blockchain,
but the longer you wait, the less likely it will be.

**Note:** Transactions are not guaranteed to be included in the next block or any specific future block, since it is not up
to the submitter of a transaction, but up to the miners to determine in which block the transaction is included.

If you want to schedule future calls of your contract, you can use a smart contract automation tool or an oracle service.

**3.1. Introduction to Smart Contracts 11**


**3.1.3 The Ethereum Virtual Machine**

**Overview**

The Ethereum Virtual Machine or EVM is the runtime environment for smart contracts in Ethereum. It is not only
sandboxed but actually completely isolated, which means that code running inside the EVM has no access to network,
filesystem or other processes. Smart contracts even have limited access to other smart contracts.

**Accounts**

There are two kinds of accounts in Ethereum which share the same address space: **External accounts** that are controlled
by public-private key pairs (i.e. humans) and **contract accounts** which are controlled by the code stored together with
the account.

The address of an external account is determined from the public key while the address of a contract is determined at
the time the contract is created (it is derived from the creator address and the number of transactions sent from that
address, the so-called “nonce”).

Regardless of whether or not the account stores code, the two types are treated equally by the EVM.

Every account has a persistent key-value store mapping 256-bit words to 256-bit words called **storage**.

Furthermore, every account has a **balance** in Ether (in “Wei” to be exact,1 etheris10**18 wei) which can be
modified by sending transactions that include Ether.

**Transactions**

A transaction is a message that is sent from one account to another account (which might be the same or empty, see
below). It can include binary data (which is called “payload”) and Ether.

If the target account contains code, that code is executed and the payload is provided as input data.

If the target account is not set (the transaction does not have a recipient or the recipient is set tonull), the transaction
creates a **new contract**. As already mentioned, the address of that contract is not the zero address but an address
derived from the sender and its number of transactions sent (the “nonce”). The payload of such a contract creation
transaction is taken to be EVM bytecode and executed. The output data of this execution is permanently stored as the
code of the contract. This means that in order to create a contract, you do not send the actual code of the contract, but
in fact code that returns that code when executed.

**Note:** While a contract is being created, its code is still empty. Because of that, you should not call back into the
contract under construction until its constructor has finished executing.

**Gas**

Upon creation, each transaction is charged with a certain amount of **gas** that has to be paid for by the originator of the
transaction (tx.origin). While the EVM executes the transaction, the gas is gradually depleted according to specific
rules. If the gas is used up at any point (i.e. it would be negative), an out-of-gas exception is triggered, which ends
execution and reverts all modifications made to the state in the current call frame.

This mechanism incentivizes economical use of EVM execution time and also compensates EVM executors (i.e. miners
/ stakers) for their work. Since each block has a maximum amount of gas, it also limits the amount of work needed to
validate a block.

**12 Chapter 3. Contents**


The **gas price** is a value set by the originator of the transaction, who has to paygas_price * gasup front to the
EVM executor. If some gas is left after execution, it is refunded to the transaction originator. In case of an exception
that reverts changes, already used up gas is not refunded.

Since EVM executors can choose to include a transaction or not, transaction senders cannot abuse the system by setting
a low gas price.

**Storage, Memory and the Stack**

The Ethereum Virtual Machine has three areas where it can store data: storage, memory and the stack.

Each account has a data area called **storage** , which is persistent between function calls and transactions. Storage
is a key-value store that maps 256-bit words to 256-bit words. It is not possible to enumerate storage from within
a contract, it is comparatively costly to read, and even more to initialise and modify storage. Because of this cost,
you should minimize what you store in persistent storage to what the contract needs to run. Store data like derived
calculations, caching, and aggregates outside of the contract. A contract can neither read nor write to any storage apart
from its own.

The second data area is called **memory** , of which a contract obtains a freshly cleared instance for each message call.
Memory is linear and can be addressed at byte level, but reads are limited to a width of 256 bits, while writes can be
either 8 bits or 256 bits wide. Memory is expanded by a word (256-bit), when accessing (either reading or writing) a
previously untouched memory word (i.e. any offset within a word). At the time of expansion, the cost in gas must be
paid. Memory is more costly the larger it grows (it scales quadratically).

The EVM is not a register machine but a stack machine, so all computations are performed on a data area called the
**stack**. It has a maximum size of 1024 elements and contains words of 256 bits. Access to the stack is limited to the
top end in the following way: It is possible to copy one of the topmost 16 elements to the top of the stack or swap the
topmost element with one of the 16 elements below it. All other operations take the topmost two (or one, or more,
depending on the operation) elements from the stack and push the result onto the stack. Of course it is possible to
move stack elements to storage or memory in order to get deeper access to the stack, but it is not possible to just access
arbitrary elements deeper in the stack without first removing the top of the stack.

**Instruction Set**

The instruction set of the EVM is kept minimal in order to avoid incorrect or inconsistent implementations which
could cause consensus problems. All instructions operate on the basic data type, 256-bit words or on slices of memory
(or other byte arrays). The usual arithmetic, bit, logical and comparison operations are present. Conditional and
unconditional jumps are possible. Furthermore, contracts can access relevant properties of the current block like its
number and timestamp.

For a complete list, please see the _list of opcodes_ as part of the inline assembly documentation.

**Message Calls**

Contracts can call other contracts or send Ether to non-contract accounts by the means of message calls. Message calls
are similar to transactions, in that they have a source, a target, data payload, Ether, gas and return data. In fact, every
transaction consists of a top-level message call which in turn can create further message calls.

A contract can decide how much of its remaining **gas** should be sent with the inner message call and how much it wants
to retain. If an out-of-gas exception happens in the inner call (or any other exception), this will be signaled by an error
value put onto the stack. In this case, only the gas sent together with the call is used up. In Solidity, the calling contract
causes a manual exception by default in such situations, so that exceptions “bubble up” the call stack.

As already said, the called contract (which can be the same as the caller) will receive a freshly cleared instance of
memory and has access to the call payload - which will be provided in a separate area called the **calldata**. After it has

**3.1. Introduction to Smart Contracts 13**


finished execution, it can return data which will be stored at a location in the caller’s memory preallocated by the caller.
All such calls are fully synchronous.

Calls are **limited** to a depth of 1024, which means that for more complex operations, loops should be preferred over
recursive calls. Furthermore, only 63/64th of the gas can be forwarded in a message call, which causes a depth limit of
a little less than 1000 in practice.

**Delegatecall and Libraries**

There exists a special variant of a message call, named **delegatecall** which is identical to a message call apart from
the fact that the code at the target address is executed in the context (i.e. at the address) of the calling contract and
msg.senderandmsg.valuedo not change their values.

This means that a contract can dynamically load code from a different address at runtime. Storage, current address and
balance still refer to the calling contract, only the code is taken from the called address.

This makes it possible to implement the “library” feature in Solidity: Reusable library code that can be applied to a
contract’s storage, e.g. in order to implement a complex data structure.

**Logs**

It is possible to store data in a specially indexed data structure that maps all the way up to the block level. This feature
called **logs** is used by Solidity in order to implement _events_. Contracts cannot access log data after it has been created,
but they can be efficiently accessed from outside the blockchain. Since some part of the log data is stored in bloom
filters, it is possible to search for this data in an efficient and cryptographically secure way, so network peers that do
not download the whole blockchain (so-called “light clients”) can still find these logs.

**Create**

Contracts can even create other contracts using a special opcode (i.e. they do not simply call the zero address as a
transaction would). The only difference between these **create calls** and normal message calls is that the payload data
is executed and the result stored as code and the caller / creator receives the address of the new contract on the stack.

**Deactivate and Self-destruct**

The only way to remove code from the blockchain is when a contract at that address performs theselfdestruct
operation. The remaining Ether stored at that address is sent to a designated target and then the storage and code is
removed from the state. Removing the contract in theory sounds like a good idea, but it is potentially dangerous, as if
someone sends Ether to removed contracts, the Ether is forever lost.

```
Warning: FromEVM >= Cancunonwards,selfdestructwill only send all Ether in the account to the given
recipient and not destroy the contract. However, whenselfdestructis called in the same transaction that creates
the contract calling it, the behaviour ofselfdestructbefore Cancun hardfork (i.e.,EVM <= Shanghai) is pre-
served and will destroy the current contract, deleting any data, including storage keys, code and the account itself.
See EIP-6780 for more details.
The new behaviour is the result of a network-wide change that affects all contracts present on the Ethereum mainnet
and testnets. It is important to note that this change is dependent on the EVM version of the chain on which the
contract is deployed. The--evm-versionsetting used when compiling the contract has no bearing on it.
Also, note that theselfdestructopcode has been deprecated in Solidity version 0.8.18, as recommended by
EIP-6049. The deprecation is still in effect and the compiler will still emit warnings on its use. Any use in newly
```
**14 Chapter 3. Contents**


```
deployed contracts is strongly discouraged even if the new behavior is taken into account. Future changes to the
EVM might further reduce the functionality of the opcode.
```
```
Warning: Even if a contract is removed byselfdestruct, it is still part of the history of the blockchain and
probably retained by most Ethereum nodes. So usingselfdestructis not the same as deleting data from a hard
disk.
```
**Note:** Even if a contract’s code does not contain a call toselfdestruct, it can still perform that operation using
delegatecallorcallcode.

If you want to deactivate your contracts, you should instead **disable** them by changing some internal state which causes
all functions to revert. This makes it impossible to use the contract, as it returns Ether immediately.

**Precompiled Contracts**

There is a small set of contract addresses that are special: The address range between 1 and (including)0x0acontains
“precompiled contracts” that can be called as any other contract but their behavior (and their gas consumption) is not
defined by EVM code stored at that address (they do not contain code) but instead is implemented in the EVM execution
environment itself.

Different EVM-compatible chains might use a different set of precompiled contracts. It might also be possible that
new precompiled contracts are added to the Ethereum main chain in the future, but you can reasonably expect them to
always be in the range between 1 and0xffff(inclusive).

### 3.2 Solidity by Example

**3.2.1 Voting**

The following contract is quite complex, but showcases a lot of Solidity’s features. It implements a voting contract. Of
course, the main problems of electronic voting is how to assign voting rights to the correct persons and how to prevent
manipulation. We will not solve all problems here, but at least we will show how delegated voting can be done so that
vote counting is **automatic and completely transparent** at the same time.

The idea is to create one contract per ballot, providing a short name for each option. Then the creator of the contract
who serves as chairperson will give the right to vote to each address individually.

The persons behind the addresses can then choose to either vote themselves or to delegate their vote to a person they
trust.

At the end of the voting time,winningProposal()will return the proposal with the largest number of votes.

// SPDX-License-Identifier: GPL-3.
pragma solidity >=0.7.0 <0.9.0;
/// @title Voting with delegation.
contract Ballot {
// This declares a new complex type which will
// be used for variables later.
// It will represent a single voter.
(continues on next page)

**3.2. Solidity by Example 15**


```
(continued from previous page)
struct Voter {
uintweight;// weight is accumulated by delegation
boolvoted; // if true, that person already voted
addressdelegate;// person delegated to
uintvote; // index of the voted proposal
}
```
```
// This is a type for a single proposal.
struct Proposal {
bytes32name; // short name (up to 32 bytes)
uintvoteCount; // number of accumulated votes
}
```
```
address publicchairperson;
```
```
// This declares a state variable that
// stores a`Voter` struct for each possible address.
mapping(address=> Voter)public voters;
```
```
// A dynamically-sized array of`Proposal` structs.
Proposal[]public proposals;
```
```
/// Create a new ballot to choose one of`proposalNames`.
constructor(bytes32[] memory proposalNames) {
chairperson =msg.sender;
voters[chairperson].weight = 1;
```
```
// For each of the provided proposal names,
// create a new proposal object and add it
// to the end of the array.
for(uinti = 0; i < proposalNames.length; i++) {
//`Proposal({...})` creates a temporary
// Proposal object and`proposals.push(...)`
// appends it to the end of`proposals`.
proposals.push(Proposal({
name: proposalNames[i],
voteCount: 0
}));
}
}
```
```
// Give`voter` the right to vote on this ballot.
// May only be called by`chairperson`.
functiongiveRightToVote(addressvoter)external{
// If the first argument of`require` evaluates
// to`false`, execution terminates and all
// changes to the state and to Ether balances
// are reverted.
// This used to consume all gas in old EVM versions, but
// not anymore.
// It is often a good idea to use`require`to check if
// functions are called correctly.
(continues on next page)
```
**16 Chapter 3. Contents**


```
(continued from previous page)
// As a second argument, you can also provide an
// explanation about what went wrong.
require(
msg.sender== chairperson,
"Only chairperson can give right to vote."
);
require(
!voters[voter].voted,
"The voter already voted."
);
require(voters[voter].weight == 0);
voters[voter].weight = 1;
}
```
```
/// Delegate your vote to the voter`to`.
functiondelegate(addressto)external{
// assigns reference
Voter storage sender = voters[msg.sender];
require(sender.weight != 0, "You have no right to vote");
require(!sender.voted, "You already voted.");
```
```
require(to != msg.sender, "Self-delegation is disallowed.");
```
```
// Forward the delegation as long as
// `to` also delegated.
// In general, such loops are very dangerous,
// because if they run too long, they might
// need more gas than is available in a block.
// In this case, the delegation will not be executed,
// but in other situations, such loops might
// cause a contract to get "stuck" completely.
while(voters[to].delegate != address(0)) {
to = voters[to].delegate;
```
```
// We found a loop in the delegation, not allowed.
require(to != msg.sender, "Found loop in delegation.");
}
```
```
Voter storage delegate_ = voters[to];
```
```
// Voters cannot delegate to accounts that cannot vote.
require(delegate_.weight >= 1);
```
```
// Since`sender`is a reference, this
// modifies`voters[msg.sender]`.
sender.voted =true;
sender.delegate = to;
```
```
if (delegate_.voted) {
// If the delegate already voted,
// directly add to the number of votes
proposals[delegate_.vote].voteCount += sender.weight;
(continues on next page)
```
**3.2. Solidity by Example 17**


```
(continued from previous page)
}else{
// If the delegate did not vote yet,
// add to her weight.
delegate_.weight += sender.weight;
}
}
```
```
/// Give your vote (including votes delegated to you)
/// to proposal `proposals[proposal].name`.
functionvote(uintproposal) external{
Voter storage sender = voters[msg.sender];
require(sender.weight != 0, "Has no right to vote");
require(!sender.voted, "Already voted.");
sender.voted =true;
sender.vote = proposal;
```
```
// If`proposal` is out of the range of the array,
// this will throw automatically and revert all
// changes.
proposals[proposal].voteCount += sender.weight;
}
```
```
/// @dev Computes the winning proposal taking all
/// previous votes into account.
functionwinningProposal()public view
returns(uintwinningProposal_)
{
uintwinningVoteCount = 0;
for(uintp = 0; p < proposals.length; p++) {
if (proposals[p].voteCount > winningVoteCount) {
winningVoteCount = proposals[p].voteCount;
winningProposal_ = p;
}
}
}
```
// Calls winningProposal() function to get the index
// of the winner contained in the proposals array and then
// returns the name of the winner
functionwinnerName()externalview
returns(bytes32winnerName_)
{
winnerName_ = proposals[winningProposal()].name;
}
}

**18 Chapter 3. Contents**


**Possible Improvements**

Currently, many transactions are needed to assign the rights to vote to all participants. Moreover, if two or more
proposals have the same number of votes,winningProposal()is not able to register a tie. Can you think of a way to
fix these issues?

**3.2.2 Blind Auction**

In this section, we will show how easy it is to create a completely blind auction contract on Ethereum. We will start
with an open auction where everyone can see the bids that are made and then extend this contract into a blind auction
where it is not possible to see the actual bid until the bidding period ends.

**Simple Open Auction**

The general idea of the following simple auction contract is that everyone can send their bids during a bidding period.
The bids already include sending some compensation, e.g. Ether, in order to bind the bidders to their bid. If the highest
bid is raised, the previous highest bidder gets their Ether back. After the end of the bidding period, the contract has to
be called manually for the beneficiary to receive their Ether - contracts cannot activate themselves.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;
contract SimpleAuction{
// Parameters of the auction. Times are either
// absolute unix timestamps (seconds since 1970-01-01)
// or time periods in seconds.
addresspayablepublicbeneficiary;
uint publicauctionEndTime;

```
// Current state of the auction.
address publichighestBidder;
uint publichighestBid;
```
```
// Allowed withdrawals of previous bids
mapping(address=>uint) pendingReturns;
```
```
// Set to true at the end, disallows any change.
// By default initialized to `false`.
boolended;
```
```
// Events that will be emitted on changes.
eventHighestBidIncreased(addressbidder,uintamount);
eventAuctionEnded(addresswinner,uintamount);
```
```
// Errors that describe failures.
```
```
// The triple-slash comments are so-called natspec
// comments. They will be shown when the user
// is asked to confirm a transaction or
// when an error is displayed.
```
```
/// The auction has already ended.
error AuctionAlreadyEnded();
(continues on next page)
```
**3.2. Solidity by Example 19**


```
(continued from previous page)
/// There is already a higher or equal bid.
error BidNotHighEnough(uinthighestBid);
/// The auction has not ended yet.
error AuctionNotYetEnded();
/// The function auctionEnd has already been called.
error AuctionEndAlreadyCalled();
```
```
/// Create a simple auction with `biddingTime`
/// seconds bidding time on behalf of the
/// beneficiary address`beneficiaryAddress`.
constructor(
uintbiddingTime,
addresspayable beneficiaryAddress
) {
beneficiary = beneficiaryAddress;
auctionEndTime =block.timestamp+ biddingTime;
}
```
```
/// Bid on the auction with the value sent
/// together with this transaction.
/// The value will only be refunded if the
/// auction is not won.
functionbid()external payable{
// No arguments are necessary, all
// information is already part of
// the transaction. The keyword payable
// is required for the function to
// be able to receive Ether.
```
```
// Revert the call if the bidding
// period is over.
if (block.timestamp > auctionEndTime)
revert AuctionAlreadyEnded();
```
```
// If the bid is not higher, send the
// Ether back (the revert statement
// will revert all changes in this
// function execution including
// it having received the Ether).
if (msg.value<= highestBid)
revert BidNotHighEnough(highestBid);
```
```
if (highestBid != 0) {
// Sending back the Ether by simply using
// highestBidder.send(highestBid) is a security risk
// because it could execute an untrusted contract.
// It is always safer to let the recipients
// withdraw their Ether themselves.
pendingReturns[highestBidder] += highestBid;
}
highestBidder = msg.sender;
highestBid =msg.value;
(continues on next page)
```
**20 Chapter 3. Contents**


```
(continued from previous page)
emit HighestBidIncreased(msg.sender,msg.value);
}
```
```
/// Withdraw a bid that was overbid.
functionwithdraw() external returns(bool) {
uintamount = pendingReturns[msg.sender];
if (amount > 0) {
// It is important to set this to zero because the recipient
// can call this function again as part of the receiving call
// before`send` returns.
pendingReturns[msg.sender] = 0;
```
```
// msg.sender is not of type`address payable` and must be
// explicitly converted using`payable(msg.sender)` in order
// use the member function`send()`.
if (!payable(msg.sender).send(amount)) {
// No need to call throw here, just reset the amount owing
pendingReturns[msg.sender] = amount;
return false;
}
}
return true;
}
```
```
/// End the auction and send the highest bid
/// to the beneficiary.
functionauctionEnd()external{
// It is a good guideline to structure functions that interact
// with other contracts (i.e. they call functions or send Ether)
// into three phases:
// 1. checking conditions
// 2. performing actions (potentially changing conditions)
// 3. interacting with other contracts
// If these phases are mixed up, the other contract could call
// back into the current contract and modify the state or cause
// effects (ether payout) to be performed multiple times.
// If functions called internally include interaction with external
// contracts, they also have to be considered interaction with
// external contracts.
```
```
// 1. Conditions
if (block.timestamp < auctionEndTime)
revert AuctionNotYetEnded();
if (ended)
revert AuctionEndAlreadyCalled();
```
```
// 2. Effects
ended =true;
emit AuctionEnded(highestBidder, highestBid);
```
```
// 3. Interaction
beneficiary.transfer(highestBid);
(continues on next page)
```
**3.2. Solidity by Example 21**


(continued from previous page)
}
}

**Blind Auction**

The previous open auction is extended to a blind auction in the following. The advantage of a blind auction is that
there is no time pressure towards the end of the bidding period. Creating a blind auction on a transparent computing
platform might sound like a contradiction, but cryptography comes to the rescue.

During the **bidding period** , a bidder does not actually send their bid, but only a hashed version of it. Since it is currently
considered practically impossible to find two (sufficiently long) values whose hash values are equal, the bidder commits
to the bid by that. After the end of the bidding period, the bidders have to reveal their bids: They send their values
unencrypted, and the contract checks that the hash value is the same as the one provided during the bidding period.

Another challenge is how to make the auction **binding and blind** at the same time: The only way to prevent the bidder
from just not sending the Ether after they won the auction is to make them send it together with the bid. Since value
transfers cannot be blinded in Ethereum, anyone can see the value.

The following contract solves this problem by accepting any value that is larger than the highest bid. Since this can of
course only be checked during the reveal phase, some bids might be **invalid** , and this is on purpose (it even provides an
explicit flag to place invalid bids with high-value transfers): Bidders can confuse competition by placing several high
or low invalid bids.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;
contract BlindAuction{
struct Bid {
bytes32blindedBid;
uintdeposit;
}

```
addresspayablepublicbeneficiary;
uint publicbiddingEnd;
uint publicrevealEnd;
bool publicended;
```
```
mapping(address=> Bid[])public bids;
```
```
address publichighestBidder;
uint publichighestBid;
```
```
// Allowed withdrawals of previous bids
mapping(address=>uint) pendingReturns;
```
```
eventAuctionEnded(addresswinner,uinthighestBid);
```
```
// Errors that describe failures.
```
```
/// The function has been called too early.
/// Try again at`time`.
error TooEarly(uint time);
/// The function has been called too late.
(continues on next page)
```
**22 Chapter 3. Contents**


```
(continued from previous page)
/// It cannot be called after`time`.
error TooLate(uinttime);
/// The function auctionEnd has already been called.
error AuctionEndAlreadyCalled();
```
```
// Modifiers are a convenient way to validate inputs to
// functions.`onlyBefore`is applied to `bid`below:
// The new function body is the modifier's body where
// `_` is replaced by the old function body.
modifieronlyBefore(uinttime) {
if (block.timestamp >= time) revert TooLate(time);
_;
}
modifieronlyAfter(uinttime) {
if (block.timestamp <= time) revert TooEarly(time);
_;
}
```
```
constructor(
uintbiddingTime,
uintrevealTime,
addresspayable beneficiaryAddress
) {
beneficiary = beneficiaryAddress;
biddingEnd =block.timestamp + biddingTime;
revealEnd = biddingEnd + revealTime;
}
```
```
/// Place a blinded bid with `blindedBid` =
/// keccak256(abi.encodePacked(value, fake, secret)).
/// The sent ether is only refunded if the bid is correctly
/// revealed in the revealing phase. The bid is valid if the
/// ether sent together with the bid is at least "value" and
/// "fake" is not true. Setting "fake" to true and sending
/// not the exact amount are ways to hide the real bid but
/// still make the required deposit. The same address can
/// place multiple bids.
functionbid(bytes32blindedBid)
external
payable
onlyBefore(biddingEnd)
{
bids[msg.sender].push(Bid({
blindedBid: blindedBid,
deposit:msg.value
}));
}
```
```
/// Reveal your blinded bids. You will get a refund for all
/// correctly blinded invalid bids and for all bids except for
/// the totally highest.
functionreveal(
(continues on next page)
```
**3.2. Solidity by Example 23**


```
(continued from previous page)
uint[] calldata values,
bool[] calldata fakes,
bytes32[] calldata secrets
)
external
onlyAfter(biddingEnd)
onlyBefore(revealEnd)
{
uintlength = bids[msg.sender].length;
require(values.length == length);
require(fakes.length == length);
require(secrets.length == length);
```
```
uintrefund;
for(uinti = 0; i < length; i++) {
Bid storage bidToCheck = bids[msg.sender][i];
(uintvalue, boolfake,bytes32secret) =
(values[i], fakes[i], secrets[i]);
if (bidToCheck.blindedBid != keccak256(abi.encodePacked(value, fake,␣
˓→secret))) {
// Bid was not actually revealed.
// Do not refund deposit.
continue;
}
refund += bidToCheck.deposit;
if (!fake && bidToCheck.deposit >= value) {
if (placeBid(msg.sender, value))
refund -= value;
}
// Make it impossible for the sender to re-claim
// the same deposit.
bidToCheck.blindedBid =bytes32(0);
}
payable(msg.sender).transfer(refund);
}
```
```
/// Withdraw a bid that was overbid.
functionwithdraw() external{
uintamount = pendingReturns[msg.sender];
if (amount > 0) {
// It is important to set this to zero because the recipient
// can call this function again as part of the receiving call
// before`transfer` returns (see the remark above about
// conditions -> effects -> interaction).
pendingReturns[msg.sender] = 0;
```
```
payable(msg.sender).transfer(amount);
}
}
```
```
/// End the auction and send the highest bid
/// to the beneficiary.
(continues on next page)
```
**24 Chapter 3. Contents**


```
(continued from previous page)
functionauctionEnd()
external
onlyAfter(revealEnd)
{
if (ended) revert AuctionEndAlreadyCalled();
emit AuctionEnded(highestBidder, highestBid);
ended =true;
beneficiary.transfer(highestBid);
}
```
// This is an "internal" function which means that it
// can only be called from the contract itself (or from
// derived contracts).
functionplaceBid(addressbidder,uintvalue) internal
returns(boolsuccess)
{
if (value <= highestBid) {
return false;
}
if (highestBidder !=address(0)) {
// Refund the previously highest bidder.
pendingReturns[highestBidder] += highestBid;
}
highestBid = value;
highestBidder = bidder;
return true;
}
}

**3.2.3 Safe Remote Purchase**

Purchasing goods remotely currently requires multiple parties that need to trust each other. The simplest configuration
involves a seller and a buyer. The buyer would like to receive an item from the seller and the seller would like to get
some compensation, e.g. Ether, in return. The problematic part is the shipment here: There is no way to determine for
sure that the item arrived at the buyer.

There are multiple ways to solve this problem, but all fall short in one or the other way. In the following example, both
parties have to put twice the value of the item into the contract as escrow. As soon as this happened, the Ether will
stay locked inside the contract until the buyer confirms that they received the item. After that, the buyer is returned the
value (half of their deposit) and the seller gets three times the value (their deposit plus the value). The idea behind this
is that both parties have an incentive to resolve the situation or otherwise their Ether is locked forever.

This contract of course does not solve the problem, but gives an overview of how you can use state machine-like
constructs inside a contract.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;
contract Purchase{
uint publicvalue;
addresspayablepublicseller;
addresspayablepublicbuyer;

```
(continues on next page)
```
**3.2. Solidity by Example 25**


```
(continued from previous page)
enumState { Created, Locked, Release, Inactive }
// The state variable has a default value of the first member,`State.created`
Statepublic state;
```
```
modifiercondition(boolcondition_) {
require(condition_);
_;
}
```
```
/// Only the buyer can call this function.
error OnlyBuyer();
/// Only the seller can call this function.
error OnlySeller();
/// The function cannot be called at the current state.
error InvalidState();
/// The provided value has to be even.
error ValueNotEven();
```
```
modifieronlyBuyer() {
if (msg.sender != buyer)
revert OnlyBuyer();
_;
}
```
```
modifieronlySeller() {
if (msg.sender != seller)
revert OnlySeller();
_;
}
```
```
modifierinState(State state_) {
if (state != state_)
revert InvalidState();
_;
}
```
```
eventAborted();
eventPurchaseConfirmed();
eventItemReceived();
eventSellerRefunded();
```
```
// Ensure that`msg.value`is an even number.
// Division will truncate if it is an odd number.
// Check via multiplication that it wasn't an odd number.
constructor() payable{
seller =payable(msg.sender);
value =msg.value/ 2;
if ((2 * value) != msg.value)
revert ValueNotEven();
}
```
```
/// Abort the purchase and reclaim the ether.
(continues on next page)
```
**26 Chapter 3. Contents**


```
(continued from previous page)
/// Can only be called by the seller before
/// the contract is locked.
functionabort()
external
onlySeller
inState(State.Created)
{
emit Aborted();
state = State.Inactive;
// We use transfer here directly. It is
// reentrancy-safe, because it is the
// last call in this function and we
// already changed the state.
seller.transfer(address(this).balance);
}
```
```
/// Confirm the purchase as buyer.
/// Transaction has to include`2 * value` ether.
/// The ether will be locked until confirmReceived
/// is called.
functionconfirmPurchase()
external
inState(State.Created)
condition(msg.value== (2 * value))
payable
{
emit PurchaseConfirmed();
buyer =payable(msg.sender);
state = State.Locked;
}
```
```
/// Confirm that you (the buyer) received the item.
/// This will release the locked ether.
functionconfirmReceived()
external
onlyBuyer
inState(State.Locked)
{
emit ItemReceived();
// It is important to change the state first because
// otherwise, the contracts called using`send`below
// can call in again here.
state = State.Release;
```
```
buyer.transfer(value);
}
```
```
/// This function refunds the seller, i.e.
/// pays back the locked funds of the seller.
functionrefundSeller()
external
onlySeller
(continues on next page)
```
**3.2. Solidity by Example 27**


```
(continued from previous page)
inState(State.Release)
{
emit SellerRefunded();
// It is important to change the state first because
// otherwise, the contracts called using`send`below
// can call in again here.
state = State.Inactive;
```
seller.transfer(3 * value);
}
}

**3.2.4 Micropayment Channel**

In this section, we will learn how to build an example implementation of a payment channel. It uses cryptographic
signatures to make repeated transfers of Ether between the same parties secure, instantaneous, and without transaction
fees. For the example, we need to understand how to sign and verify signatures, and setup the payment channel.

**Creating and verifying signatures**

Imagine Alice wants to send some Ether to Bob, i.e. Alice is the sender and Bob is the recipient.

Alice only needs to send cryptographically signed messages off-chain (e.g. via email) to Bob and it is similar to writing
checks.

Alice and Bob use signatures to authorize transactions, which is possible with smart contracts on Ethereum. Alice will
build a simple smart contract that lets her transmit Ether, but instead of calling a function herself to initiate a payment,
she will let Bob do that, and therefore pay the transaction fee.

The contract will work as follows:

1. Alice deploys theReceiverPayscontract, attaching enough Ether to cover the payments that will be made.
2. Alice authorizes a payment by signing a message with her private key.
3. Alice sends the cryptographically signed message to Bob. The message does not need to be kept secret (explained
    later), and the mechanism for sending it does not matter.
4. Bob claims his payment by presenting the signed message to the smart contract, it verifies the authenticity of the
    message and then releases the funds.

**Creating the signature**

Alice does not need to interact with the Ethereum network to sign the transaction, the process is completely offline.
In this tutorial, we will sign messages in the browser using web3.js and MetaMask, using the method described in
EIP-712, as it provides a number of other security benefits.

/// Hashing first makes things easier
varhash = web3.utils.sha3("message to sign");
web3.eth.personal.sign(hash, web3.eth.defaultAccount,function () { console.log("Signed
˓→"); });

**28 Chapter 3. Contents**


**Note:** Theweb3.eth.personal.signprepends the length of the message to the signed data. Since we hash first,
the message will always be exactly 32 bytes long, and thus this length prefix is always the same.

**What to Sign**

For a contract that fulfills payments, the signed message must include:

1. The recipient’s address.
2. The amount to be transferred.
3. Protection against replay attacks.

A replay attack is when a signed message is reused to claim authorization for a second action. To avoid replay attacks we
use the same technique as in Ethereum transactions themselves, a so-called nonce, which is the number of transactions
sent by an account. The smart contract checks if a nonce is used multiple times.

Another type of replay attack can occur when the owner deploys aReceiverPayssmart contract, makes some pay-
ments, and then destroys the contract. Later, they decide to deploy theRecipientPayssmart contract again, but the
new contract does not know the nonces used in the previous deployment, so the attacker can use the old messages again.

Alice can protect against this attack by including the contract’s address in the message, and only messages containing the
contract’s address itself will be accepted. You can find an example of this in the first two lines of theclaimPayment()
function of the full contract at the end of this section.

Furthermore, instead of destroying the contract by callingselfdestruct, which is currently deprecated, we will
disable the contract’s functionalities by freezing it, resulting in the reversion of any call after it being frozen.

**Packing arguments**

Now that we have identified what information to include in the signed message, we are ready to put the message
together, hash it, and sign it. For simplicity, we concatenate the data. The ethereumjs-abi library provides a function
calledsoliditySHA3that mimics the behavior of Solidity’skeccak256function applied to arguments encoded using
abi.encodePacked. Here is a JavaScript function that creates the proper signature for theReceiverPaysexample:

// recipient is the address that should be paid.
// amount, in wei, specifies how much ether should be sent.
// nonce can be any unique number to prevent replay attacks
// contractAddress is used to prevent cross-contract replay attacks
functionsignPayment(recipient, amount, nonce, contractAddress, callback) {
varhash = "0x" + abi.soliditySHA3(
["address", "uint256", "uint256", "address"],
[recipient, amount, nonce, contractAddress]
).toString("hex");

web3.eth.personal.sign(hash, web3.eth.defaultAccount, callback);
}

**3.2. Solidity by Example 29**


**Recovering the Message Signer in Solidity**

In general, ECDSA signatures consist of two parameters,rands. Signatures in Ethereum include a third parameter
calledv, that you can use to verify which account’s private key was used to sign the message, and the transaction’s
sender. Solidity provides a built-in function _ecrecover_ that accepts a message along with ther,sandvparameters and
returns the address that was used to sign the message.

**Extracting the Signature Parameters**

Signatures produced by web3.js are the concatenation ofr,sandv, so the first step is to split these parameters apart.
You can do this on the client-side, but doing it inside the smart contract means you only need to send one signature
parameter rather than three. Splitting apart a byte array into its constituent parts is a mess, so we use _inline assembly_
to do the job in thesplitSignaturefunction (the third function in the full contract at the end of this section).

**Computing the Message Hash**

The smart contract needs to know exactly what parameters were signed, and so it must recreate the message from
the parameters and use that for signature verification. The functionsprefixedandrecoverSignerdo this in the
claimPaymentfunction.

**The full contract**

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned{
addresspayable owner;
constructor() {
owner =payable(msg.sender);
}
}

contract Freezable isOwned {
bool private_frozen =false;

```
modifiernotFrozen() {
require(!_frozen, "Inactive Contract.");
_;
}
```
functionfreeze()internal{
if (msg.sender == owner)
_frozen =true;
}
}

contract ReceiverPays isFreezable {
mapping(uint256=>bool) usedNonces;

```
constructor() payable{}
(continues on next page)
```
**30 Chapter 3. Contents**


```
(continued from previous page)
```
```
functionclaimPayment(uint256amount,uint256nonce,bytes memory signature)
external
notFrozen
{
require(!usedNonces[nonce]);
usedNonces[nonce] =true;
```
```
// this recreates the message that was signed on the client
bytes32message = prefixed(keccak256(abi.encodePacked(msg.sender, amount, nonce,␣
˓→this)));
require(recoverSigner(message, signature) == owner);
payable(msg.sender).transfer(amount);
}
```
```
/// freeze the contract and reclaim the leftover funds.
functionshutdown()
external
notFrozen
{
require(msg.sender== owner);
freeze();
payable(msg.sender).transfer(address(this).balance);
}
```
```
/// signature methods.
functionsplitSignature(bytes memory sig)
internal
pure
returns(uint8v, bytes32r, bytes32s)
{
require(sig.length == 65);
```
```
assembly {
// first 32 bytes, after the length prefix.
r := mload(add(sig, 32))
// second 32 bytes.
s := mload(add(sig, 64))
// final byte (first byte of the next 32 bytes).
v := byte(0, mload(add(sig, 96)))
}
```
```
return(v, r, s);
}
```
```
functionrecoverSigner(bytes32message,bytes memory sig)
internal
pure
returns(address)
{
(uint8v, bytes32r, bytes32s) = splitSignature(sig);
returnecrecover(message, v, r, s);
(continues on next page)
```
**3.2. Solidity by Example 31**


```
(continued from previous page)
}
```
/// builds a prefixed hash to mimic the behavior of eth_sign.
functionprefixed(bytes32hash)internalpure returns(bytes32) {
returnkeccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", hash));
}
}

**Writing a Simple Payment Channel**

Alice now builds a simple but complete implementation of a payment channel. Payment channels use cryptographic
signatures to make repeated transfers of Ether securely, instantaneously, and without transaction fees.

**What is a Payment Channel?**

Payment channels allow participants to make repeated transfers of Ether without using transactions. This means that
you can avoid the delays and fees associated with transactions. We are going to explore a simple unidirectional payment
channel between two parties (Alice and Bob). It involves three steps:

1. Alice funds a smart contract with Ether. This “opens” the payment channel.
2. Alice signs messages that specify how much of that Ether is owed to the recipient. This step is repeated for each
    payment.
3. Bob “closes” the payment channel, withdrawing his portion of the Ether and sending the remainder back to the
    sender.

**Note:** Only steps 1 and 3 require Ethereum transactions, step 2 means that the sender transmits a cryptographically
signed message to the recipient via off chain methods (e.g. email). This means only two transactions are required to
support any number of transfers.

Bob is guaranteed to receive his funds because the smart contract escrows the Ether and honours a valid signed message.
The smart contract also enforces a timeout, so Alice is guaranteed to eventually recover her funds even if the recipient
refuses to close the channel. It is up to the participants in a payment channel to decide how long to keep it open. For
a short-lived transaction, such as paying an internet café for each minute of network access, the payment channel may
be kept open for a limited duration. On the other hand, for a recurring payment, such as paying an employee an hourly
wage, the payment channel may be kept open for several months or years.

**Opening the Payment Channel**

To open the payment channel, Alice deploys the smart contract, attaching the Ether to be escrowed and specifying the
intended recipient and a maximum duration for the channel to exist. This is the functionSimplePaymentChannelin
the contract, at the end of this section.

**32 Chapter 3. Contents**


**Making Payments**

Alice makes payments by sending signed messages to Bob. This step is performed entirely outside of the Ethereum
network. Messages are cryptographically signed by the sender and then transmitted directly to the recipient.

Each message includes the following information:

- The smart contract’s address, used to prevent cross-contract replay attacks.
- The total amount of Ether that is owed to the recipient so far.

A payment channel is closed just once, at the end of a series of transfers. Because of this, only one of the messages
sent is redeemed. This is why each message specifies a cumulative total amount of Ether owed, rather than the amount
of the individual micropayment. The recipient will naturally choose to redeem the most recent message because that is
the one with the highest total. The nonce per-message is not needed anymore, because the smart contract only honours
a single message. The address of the smart contract is still used to prevent a message intended for one payment channel
from being used for a different channel.

Here is the modified JavaScript code to cryptographically sign a message from the previous section:

functionconstructPaymentMessage(contractAddress, amount) {
return abi.soliditySHA3(
["address", "uint256"],
[contractAddress, amount]
);
}

functionsignMessage(message, callback) {
web3.eth.personal.sign(
"0x" + message.toString("hex"),
web3.eth.defaultAccount,
callback
);
}

// contractAddress is used to prevent cross-contract replay attacks.
// amount, in wei, specifies how much Ether should be sent.

functionsignPayment(contractAddress, amount, callback) {
varmessage = constructPaymentMessage(contractAddress, amount);
signMessage(message, callback);
}

**Closing the Payment Channel**

When Bob is ready to receive his funds, it is time to close the payment channel by calling aclosefunction on the
smart contract. Closing the channel pays the recipient the Ether they are owed and deactivates the contract by freezing
it, sending any remaining Ether back to Alice. To close the channel, Bob needs to provide a message signed by Alice.

The smart contract must verify that the message contains a valid signature from the sender. The process for do-
ing this verification is the same as the process the recipient uses. The Solidity functionsisValidSignatureand
recoverSignerwork just like their JavaScript counterparts in the previous section, with the latter function borrowed
from theReceiverPayscontract.

Only the payment channel recipient can call theclosefunction, who naturally passes the most recent payment message
because that message carries the highest total owed. If the sender were allowed to call this function, they could provide

**3.2. Solidity by Example 33**


a message with a lower amount and cheat the recipient out of what they are owed.

The function verifies the signed message matches the given parameters. If everything checks out, the recipient is sent
their portion of the Ether, and the sender is sent the remaining funds via atransfer. You can see theclosefunction
in the full contract.

**Channel Expiration**

Bob can close the payment channel at any time, but if they fail to do so, Alice needs a way to recover her escrowed funds.
An _expiration_ time was set at the time of contract deployment. Once that time is reached, Alice can callclaimTimeout
to recover her funds. You can see theclaimTimeoutfunction in the full contract.

After this function is called, Bob can no longer receive any Ether, so it is important that Bob closes the channel before
the expiration is reached.

**The full contract**

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Frozeable{
bool private_frozen =false;

```
modifiernotFrozen() {
require(!_frozen, "Inactive Contract.");
_;
}
```
functionfreeze()internal{
_frozen =true;
}
}

contract SimplePaymentChannel is Frozeable {
addresspayablepublicsender; // The account sending payments.
addresspayablepublicrecipient; // The account receiving the payments.
uint256 publicexpiration; // Timeout in case the recipient never closes.

```
constructor(addresspayable recipientAddress,uint256duration)
payable
{
sender =payable(msg.sender);
recipient = recipientAddress;
expiration =block.timestamp + duration;
}
```
```
/// the recipient can close the channel at any time by presenting a
/// signed amount from the sender. the recipient will be sent that amount,
/// and the remainder will go back to the sender
functionclose(uint256amount,bytesmemory signature)
external
notFrozen
(continues on next page)
```
**34 Chapter 3. Contents**


```
(continued from previous page)
{
require(msg.sender== recipient);
require(isValidSignature(amount, signature));
```
```
recipient.transfer(amount);
freeze();
sender.transfer(address(this).balance);
}
```
```
/// the sender can extend the expiration at any time
functionextend(uint256newExpiration)
external
notFrozen
{
require(msg.sender== sender);
require(newExpiration > expiration);
```
```
expiration = newExpiration;
}
```
```
/// if the timeout is reached without the recipient closing the channel,
/// then the Ether is released back to the sender.
functionclaimTimeout()
external
notFrozen
{
require(block.timestamp>= expiration);
freeze();
sender.transfer(address(this).balance);
}
```
```
functionisValidSignature(uint256amount,bytesmemory signature)
internal
view
returns(bool)
{
bytes32message = prefixed(keccak256(abi.encodePacked(this, amount)));
// check that the signature is from the payment sender
returnrecoverSigner(message, signature) == sender;
}
```
```
/// All functions below this are just taken from the chapter
///'creating and verifying signatures'chapter.
functionsplitSignature(bytes memory sig)
internal
pure
returns(uint8v, bytes32r, bytes32s)
{
require(sig.length == 65);
```
```
assembly {
// first 32 bytes, after the length prefix
(continues on next page)
```
**3.2. Solidity by Example 35**


```
(continued from previous page)
r := mload(add(sig, 32))
// second 32 bytes
s := mload(add(sig, 64))
// final byte (first byte of the next 32 bytes)
v := byte(0, mload(add(sig, 96)))
}
return(v, r, s);
}
```
```
functionrecoverSigner(bytes32message,bytes memory sig)
internal
pure
returns(address)
{
(uint8v, bytes32r, bytes32s) = splitSignature(sig);
returnecrecover(message, v, r, s);
}
```
/// builds a prefixed hash to mimic the behavior of eth_sign.
functionprefixed(bytes32hash)internalpure returns(bytes32) {
returnkeccak256(abi.encodePacked("\x19Ethereum Signed Message:\n32", hash));
}
}

**Note:** The functionsplitSignaturedoes not use all security checks. A real implementation should use a more
rigorously tested library, such as openzeppelin’s version of this code.

**Verifying Payments**

Unlike in the previous section, messages in a payment channel aren’t redeemed right away. The recipient keeps track of
the latest message and redeems it when it’s time to close the payment channel. This means it’s critical that the recipient
perform their own verification of each message. Otherwise there is no guarantee that the recipient will be able to get
paid in the end.

The recipient should verify each message using the following process:

1. Verify that the contract address in the message matches the payment channel.
2. Verify that the new total is the expected amount.
3. Verify that the new total does not exceed the amount of Ether escrowed.
4. Verify that the signature is valid and comes from the payment channel sender.

We’ll use the ethereumjs-util library to write this verification. The final step can be done a number of ways, and we use
JavaScript. The following code borrows theconstructPaymentMessagefunction from the signing **JavaScript code**
above:

// this mimics the prefixing behavior of the eth_sign JSON-RPC method.
functionprefixed(hash) {
return ethereumjs.ABI.soliditySHA3(
["string", "bytes32"],
(continues on next page)

**36 Chapter 3. Contents**


(continued from previous page)
["\x19Ethereum Signed Message:\n32", hash]
);
}

functionrecoverSigner(message, signature) {
varsplit = ethereumjs.Util.fromRpcSig(signature);
varpublicKey = ethereumjs.Util.ecrecover(message, split.v, split.r, split.s);
varsigner = ethereumjs.Util.pubToAddress(publicKey).toString("hex");
return signer;
}

functionisValidSignature(contractAddress, amount, signature, expectedSigner) {
varmessage = prefixed(constructPaymentMessage(contractAddress, amount));
varsigner = recoverSigner(message, signature);
return signer.toLowerCase() ==
ethereumjs.Util.stripHexPrefix(expectedSigner).toLowerCase();
}

**3.2.5 Modular Contracts**

A modular approach to building your contracts helps you reduce the complexity and improve the readability which will
help to identify bugs and vulnerabilities during development and code review. If you specify and control the behavior
of each module in isolation, the interactions you have to consider are only those between the module specifications
and not every other moving part of the contract. In the example below, the contract uses themovemethod of the
Balances _library_ to check that balances sent between addresses match what you expect. In this way, theBalances
library provides an isolated component that properly tracks balances of accounts. It is easy to verify that theBalances
library never produces negative balances or overflows and the sum of all balances is an invariant across the lifetime of
the contract.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

libraryBalances {
functionmove(mapping(address=> uint256) storage balances, addressfrom,addressto,
˓→uintamount)internal{
require(balances[from] >= amount);
require(balances[to] + amount >= balances[to]);
balances[from] -= amount;
balances[to] += amount;
}
}

contract Token{
mapping(address=>uint256) balances;
using Balancesfor*;
mapping(address=>mapping(address=> uint256)) allowed;

```
eventTransfer(addressfrom, addressto,uint amount);
eventApproval(addressowner, addressspender,uintamount);
```
```
functiontransfer(addressto,uintamount)external returns(boolsuccess) {
(continues on next page)
```
**3.2. Solidity by Example 37**


```
(continued from previous page)
balances.move(msg.sender, to, amount);
emit Transfer(msg.sender, to, amount);
return true;
```
```
}
```
```
functiontransferFrom(addressfrom,addressto,uintamount)external returns(bool␣
˓→success) {
require(allowed[from][msg.sender] >= amount);
allowed[from][msg.sender] -= amount;
balances.move(from, to, amount);
emit Transfer(from, to, amount);
return true;
}
```
```
functionapprove(addressspender,uinttokens)external returns(boolsuccess) {
require(allowed[msg.sender][spender] == 0, "");
allowed[msg.sender][spender] = tokens;
emit Approval(msg.sender, spender, tokens);
return true;
}
```
functionbalanceOf(addresstokenOwner)externalviewreturns(uintbalance) {
returnbalances[tokenOwner];
}
}

### 3.3 Installing the Solidity Compiler

**3.3.1 Versioning**

Solidity versions follow Semantic Versioning. In addition, patch-level releases with major release 0 (i.e. 0.x.y) will
not contain breaking changes. That means code that compiles with version 0.x.y can be expected to compile with 0.x.z
where z > y.

In addition to releases, we provide **nightly development builds** to make it easy for developers to try out upcoming
features and provide early feedback. Note, however, that while the nightly builds are usually very stable, they contain
bleeding-edge code from the development branch and are not guaranteed to be always working. Despite our best efforts,
they might contain undocumented and/or broken changes that will not become a part of an actual release. They are not
meant for production use.

When deploying contracts, you should use the latest released version of Solidity. This is because breaking changes, as
well as new features and bug fixes are introduced regularly. We currently use a 0.x version number to indicate this fast
pace of change.

**38 Chapter 3. Contents**


**3.3.2 Remix**

_We recommend Remix for small contracts and for quickly learning Solidity._

Access Remix online, you do not need to install anything. If you want to use it without connection to the Internet, go to
https://github.com/ethereum/remix-live/tree/gh-pages#readme and follow the instructions on that page. Remix is also
a convenient option for testing nightly builds without installing multiple Solidity versions.

Further options on this page detail installing command-line Solidity compiler software on your computer. Choose a
command-line compiler if you are working on a larger contract or if you require more compilation options.

**3.3.3 npm / Node.js**

Usenpmfor a convenient and portable way to installsolcjs, a Solidity compiler. The _solcjs_ program has fewer
features than the ways to access the compiler described further down this page. The _Using the Commandline Compiler_
documentation assumes you are using the full-featured compiler,solc. The usage ofsolcjsis documented inside its
own repository.

Note: The solc-js project is derived from the C++ _solc_ by using Emscripten, which means that both use the same
compiler source code. _solc-js_ can be used in JavaScript projects directly (such as Remix). Please refer to the solc-js
repository for instructions.

npm install -g solc

**Note:** The command-line executable is namedsolcjs.

The command-line options ofsolcjsare not compatible withsolcand tools (such asgeth) expecting the behavior
ofsolcwill not work withsolcjs.

**3.3.4 Docker**

Docker images of Solidity builds are available using thesolcimage from theethereumorganization. Use thestable
tag for the latest released version, andnightlyfor potentially unstable changes in thedevelopbranch.

The Docker image runs the compiler executable so that you can pass all compiler arguments to it. For example, the
command below pulls the stable version of thesolcimage (if you do not have it already), and runs it in a new container,
passing the--helpargument.

docker run ethereum/solc:stable --help

You can specify release build versions in the tag. For example:

docker run ethereum/solc:stable --help

Note

Specific compiler versions are supported as the Docker image tag such as _ethereum/solc:0.8.23_. We will be passing the
_stable_ tag here instead of specific version tag to ensure that users get the latest version by default and avoid the issue of
an out-of-date version.

To use the Docker image to compile Solidity files on the host machine, mount a local folder for input and output, and
specify the contract to compile. For example:

**3.3. Installing the Solidity Compiler 39**


docker run -v /local/path:/sources ethereum/solc:stable -o /sources/output --abi --bin /
˓→sources/Contract.sol

You can also use the standard JSON interface (which is recommended when using the compiler with tooling). When
using this interface, it is not necessary to mount any directories as long as the JSON input is self-contained (i.e. it does
not refer to any external files that would have to be _loaded by the import callback_ ).

docker run ethereum/solc:stable --standard-json < input.json > output.json

**3.3.5 Linux Packages**

Binary packages of Solidity are available at solidity/releases.

We also have PPAs for Ubuntu, you can get the latest stable version using the following commands:

sudo add-apt-repository ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install solc

The nightly version can be installed using these commands:

sudo add-apt-repository ppa:ethereum/ethereum
sudo add-apt-repository ppa:ethereum/ethereum-dev
sudo apt-get update
sudo apt-get install solc

Furthermore, some Linux distributions provide their own packages. These packages are not directly maintained by us
but usually kept up-to-date by the respective package maintainers.

For example, Arch Linux has packages for the latest development version as AUR packages: solidity and solidity-bin.

**Note:** Please be aware that AUR packages are user-produced content and unofficial packages. Exercise caution when
using them.

There is also a snap package, however, it is **currently unmaintained**. It is installable in all the supported Linux distros.
To install the latest stable version of solc:

sudo snap install solc

If you want to help testing the latest development version of Solidity with the most recent changes, please use the
following:

sudo snap install solc --edge

**Note:** Thesolcsnap uses strict confinement. This is the most secure mode for snap packages but it comes with limi-
tations, like accessing only the files in your/homeand/mediadirectories. For more information, go to Demystifying
Snap Confinement.

**40 Chapter 3. Contents**


**3.3.6 macOS Packages**

We distribute the Solidity compiler through Homebrew as a build-from-source version. Pre-built bottles are currently
not supported.

brew update
brew upgrade
brew tap ethereum/ethereum
brew install solidity

To install the most recent 0.4.x / 0.5.x version of Solidity you can also usebrew install solidity@4andbrew
install solidity@5, respectively.

If you need a specific version of Solidity you can install a Homebrew formula directly from Github.

View solidity.rb commits on GitHub.

Copy the commit hash of the version you want and check it out on your machine.

git clone https://github.com/ethereum/homebrew-ethereum.git
cd homebrew-ethereum
git checkout <your-hash-goes-here>

Install it usingbrew:

brew unlink solidity
# eg. Install 0.4.8
brew install solidity.rb

**3.3.7 Static Binaries**

We maintain a repository containing static builds of past and current compiler versions for all supported platforms at
solc-bin. This is also the location where you can find the nightly builds.

The repository is not only a quick and easy way for end users to get binaries ready to be used out-of-the-box but it is
also meant to be friendly to third-party tools:

- The content is mirrored to https://binaries.soliditylang.org where it can be easily downloaded over HTTPS with-
    out any authentication, rate limiting or the need to use git.
- Content is served with correct _Content-Type_ headers and lenient CORS configuration so that it can be directly
    loaded by tools running in the browser.
- Binaries do not require installation or unpacking (exception for older Windows builds bundled with necessary
    DLLs).
- We strive for a high level of backward-compatibility. Files, once added, are not removed or moved without
    providing a symlink/redirect at the old location. They are also never modified in place and should always match
    the original checksum. The only exception would be broken or unusable files with the potential to cause more
    harm than good if left as is.
- Files are served over both HTTP and HTTPS. As long as you obtain the file list in a secure way (via git, HTTPS,
    IPFS or just have it cached locally) and verify hashes of the binaries after downloading them, you do not have to
    use HTTPS for the binaries themselves.

The same binaries are in most cases available on the Solidity release page on GitHub. The difference is that we do
not generally update old releases on the GitHub release page. This means that we do not rename them if the naming

**3.3. Installing the Solidity Compiler 41**


convention changes and we do not add builds for platforms that were not supported at the time of release. This only
happens insolc-bin.

Thesolc-binrepository contains several top-level directories, each representing a single platform. Each one includes
alist.jsonfile listing the available binaries. For example inemscripten-wasm32/list.jsonyou will find the
following information about version 0.7.4:

{
"path": "solc-emscripten-wasm32-v0.7.4+commit.3f05b770.js",
"version": "0.7.4",
"build": "commit.3f05b770",
"longVersion": "0.7.4+commit.3f05b770",
"keccak256": "0x300330ecd127756b824aa13e843cb1f43c473cb22eaf3750d5fb9c99279af8c3",
"sha256": "0x2b55ed5fec4d9625b6c7b3ab1abd2b7fb7dd2a9c68543bf0323db2c7e2d55af2",
"urls": [
"dweb:/ipfs/QmTLs5MuLEWXQkths41HiACoXDiH8zxyqBHGFDRSzVE5CS"
]
}

This means that:

- You can find the binary in the same directory under the name solc-emscripten-wasm32-
    v0.7.4+commit.3f05b770.js. Note that the file might be a symlink, and you will need to resolve it yourself if
    you are not using git to download it or your file system does not support symlinks.
- The binary is also mirrored at https://binaries.soliditylang.org/emscripten-wasm32/
    solc-emscripten-wasm32-v0.7.4+commit.3f05b770.js. In this case git is not necessary and symlinks are
    resolved transparently, either by serving a copy of the file or returning a HTTP redirect.
- The file is also available on IPFS at QmTLs5MuLEWXQkths41HiACoXDiH8zxyqBHGFDRSzVE5CS. Please,
    be aware that the order of items in theurlsarray is not predetermined or guaranteed and users should not rely
    on it.
- You can verify the integrity of the binary by comparing its keccak256 hash to
    0x300330ecd127756b824aa13e843cb1f43c473cb22eaf3750d5fb9c99279af8c3. The hash can be
    computed on the command-line usingkeccak256sumutility provided by sha3sum or keccak256() function
    from ethereumjs-util in JavaScript.
- You can also verify the integrity of the binary by comparing its sha256 hash to
    0x2b55ed5fec4d9625b6c7b3ab1abd2b7fb7dd2a9c68543bf0323db2c7e2d55af2.

```
Warning: Due to the strong backwards compatibility requirement the repository contains some legacy elements
but you should avoid using them when writing new tools:
```
- Useemscripten-wasm32/(with a fallback toemscripten-asmjs/) instead ofbin/if you want the best
    performance. Until version 0.6.1 we only provided asm.js binaries. Starting with 0.6.2 we switched to We-
    bAssembly builds with much better performance. We have rebuilt the older versions for wasm but the original
    asm.js files remain inbin/. The new ones had to be placed in a separate directory to avoid name clashes.
- Useemscripten-asmjs/andemscripten-wasm32/instead ofbin/andwasm/directories if you want
    to be sure whether you are downloading a wasm or an asm.js binary.
- Uselist.jsoninstead oflist.jsandlist.txt. The JSON list format contains all the information from
    the old ones and more.
- Use https://binaries.soliditylang.org instead of https://solc-bin.ethereum.org. To keep things simple we
    moved almost everything related to the compiler under the newsoliditylang.orgdomain and this ap-

**42 Chapter 3. Contents**


```
plies tosolc-bintoo. While the new domain is recommended, the old one is still fully supported and
guaranteed to point at the same location.
```
```
Warning: The binaries are also available at https://ethereum.github.io/solc-bin/ but this page stopped being up-
dated just after the release of version 0.7.2, will not receive any new releases or nightly builds for any platform and
does not serve the new directory structure, including non-emscripten builds.
If you are using it, please switch to https://binaries.soliditylang.org, which is a drop-in replacement. This allows us
to make changes to the underlying hosting in a transparent way and minimize disruption. Unlike theethereum.
github.iodomain, which we do not have any control over,binaries.soliditylang.orgis guaranteed to work
and maintain the same URL structure in the long-term.
```
**3.3.8 Building from Source**

**Prerequisites - All Operating Systems**

The following are dependencies for all builds of Solidity:

```
Software Notes
CMake (version 3.21.3+ on Windows, 3.13+ otherwise) Cross-platform build file generator.
Boost (version 1.77+ on Windows, 1.65+ otherwise) C++ libraries.
Git Command-line tool for retrieving source code.
z3 (version 4.8.16+, Optional) For use with SMT checker.
```
**Note:** Solidity versions prior to 0.5.10 can fail to correctly link against Boost versions 1.70+. A possible workaround is
to temporarily rename<Boost install path>/lib/cmake/Boost-1.70.0prior to running the cmake command
to configure Solidity.

Starting from 0.5.10 linking against Boost 1.70+ should work without manual intervention.

**Note:** The default build configuration requires a specific Z3 version (the latest one at the time the code was last up-
dated). Changes introduced between Z3 releases often result in slightly different (but still valid) results being returned.
Our SMT tests do not account for these differences and will likely fail with a different version than the one they were
written for. This does not mean that a build using a different version is faulty. If you pass-DSTRICT_Z3_VERSION=OFF
option to CMake, you can build with any version that satisfies the requirement given in the table above. If you do this,
however, please remember to pass the--no-smtoption toscripts/tests.shto skip the SMT tests.

**Note:** By default the build is performed in _pedantic mode_ , which enables extra warnings and tells the compiler to
treat all warnings as errors. This forces developers to fix warnings as they arise, so they do not accumulate “to be fixed
later”. If you are only interested in creating a release build and do not intend to modify the source code to deal with
such warnings, you can pass-DPEDANTIC=OFFoption to CMake to disable this mode. Doing this is not recommended
for general use but may be necessary when using a toolchain we are not testing with or trying to build an older version
with newer tools. If you encounter such warnings, please consider reporting them.

**3.3. Installing the Solidity Compiler 43**


**Minimum Compiler Versions**

The following C++ compilers and their minimum versions can build the Solidity codebase:

- GCC, version 8+
- Clang, version 7+
- MSVC, version 2019+

**Prerequisites - macOS**

For macOS builds, ensure that you have the latest version of Xcode installed. This contains the Clang C++ compiler,
the Xcode IDE and other Apple development tools that are required for building C++ applications on OS X. If you are
installing Xcode for the first time, or have just installed a new version then you will need to agree to the license before
you can do command-line builds:

sudo xcodebuild -license accept

Our OS X build script uses the Homebrew package manager for installing external dependencies. Here’s how to unin-
stall Homebrew, if you ever want to start again from scratch.

**Prerequisites - Windows**

You need to install the following dependencies for Windows builds of Solidity:

```
Software Notes
Visual Studio 2019 Build Tools C++ compiler
Visual Studio 2019 (Optional) C++ compiler and dev environment.
Boost (version 1.77+) C++ libraries.
```
If you already have one IDE and only need the compiler and libraries, you could install Visual Studio 2019 Build Tools.

Visual Studio 2019 provides both IDE and necessary compiler and libraries. So if you have not got an IDE and prefer
to develop Solidity, Visual Studio 2019 may be a choice for you to get everything setup easily.

Here is the list of components that should be installed in Visual Studio 2019 Build Tools or Visual Studio 2019:

- Visual Studio C++ core features
- VC++ 2019 v141 toolset (x86,x64)
- Windows Universal CRT SDK
- Windows 8.1 SDK
- C++/CLI support

We have a helper script which you can use to install all required external dependencies:

scripts\install_deps.ps1

This will installboostandcmaketo thedepssubdirectory.

**44 Chapter 3. Contents**


**Clone the Repository**

To clone the source code, execute the following command:

git clone --recursive https://github.com/ethereum/solidity.git
cd solidity

If you want to help develop Solidity, you should fork Solidity and add your personal fork as a second remote:

git remote add personal git@github.com:[username]/solidity.git

**Note:** This method will result in a pre-release build leading to e.g. a flag being set in each bytecode produced by
such a compiler. If you want to re-build a released Solidity compiler, then please use the source tarball on the GitHub
release page:

https://github.com/ethereum/solidity/releases/download/v0.X.Y/solidity_0.X.Y.tar.gz

(not the “Source code” provided by GitHub).

**Command-Line Build**

**Be sure to install External Dependencies (see above) before build.**

Solidity project uses CMake to configure the build. You might want to install ccache to speed up repeated builds.
CMake will pick it up automatically. Building Solidity is quite similar on Linux, macOS and other Unices:

mkdir build
cd build
cmake .. && make

or even easier on Linux and macOS, you can run:

#note: this will install binaries solc and soltest at usr/local/bin
./scripts/build.sh

```
Warning: BSD builds should work, but are untested by the Solidity team.
```
And for Windows:

mkdir build
cd build
cmake -G "Visual Studio 16 2019" ..

In case you want to use the version of boost installed by scripts\install_deps.ps1,
you will additionally need to pass -DBoost_DIR="deps\boost\lib\cmake\Boost-*" and
-DCMAKE_MSVC_RUNTIME_LIBRARY=MultiThreadedas arguments to the call tocmake.

This should result in the creation of **solidity.sln** in that build directory. Double-clicking on that file should result in
Visual Studio firing up. We suggest building **Release** configuration, but all others work.

Alternatively, you can build for Windows on the command-line, like so:

**3.3. Installing the Solidity Compiler 45**


cmake --build. --config Release

**3.3.9 CMake Options**

If you are interested what CMake options are available runcmake .. -LH.

**SMT Solvers**

Solidity can be built against Z3 SMT solver and will do so by default if it is found in the system. Z3 can be disabled
by acmakeoption.

_Note: In some cases, this can also be a potential workaround for build failures._

Inside the build folder you can disable Z3, since it is enabled by default:

# disables Z3 SMT Solver.
cmake .. -DUSE_Z3=OFF

**Note:** Solidity can optionally use other solvers, namelycvc5andEldarica, but their presence is checked only at
runtime, they are not needed for the build to succeed.

**3.3.10 The Version String in Detail**

The Solidity version string contains four parts:

- the version number
- pre-release tag, usually set todevelop.YYYY.MM.DDornightly.YYYY.MM.DD
- commit in the format ofcommit.GITHASH
- platform, which has an arbitrary number of items, containing details about the platform and compiler

If there are local modifications, the commit will be postfixed with.mod.

These parts are combined as required by SemVer, where the Solidity pre-release tag equals to the SemVer pre-release
and the Solidity commit and platform combined make up the SemVer build metadata.

A release example:0.4.8+commit.60cc1668.Emscripten.clang.

A pre-release example:0.4.9-nightly.2017.1.17+commit.6ecb4aa3.Emscripten.clang

**3.3.11 Important Information About Versioning**

After a release is made, the patch version level is bumped, because we assume that only patch level changes follow.
When changes are merged, the version should be bumped according to SemVer and the severity of the change. Finally,
a release is always made with the version of the current nightly build, but without theprereleasespecifier.

Example:

1. The 0.4.0 release is made.
2. The nightly build has a version of 0.4.1 from now on.
3. Non-breaking changes are introduced –> no change in version.

**46 Chapter 3. Contents**


4. A breaking change is introduced –> version is bumped to 0.5.0.
5. The 0.5.0 release is made.

This behavior works well with the _version pragma_.

### 3.4 Layout of a Solidity Source File

Source files can contain an arbitrary number of _contract definitions_ , _import_ , _pragma_ and _using for_ directives and _struct_ ,
_enum_ , _function_ , _error_ and _constant variable_ definitions.

**3.4.1 SPDX License Identifier**

Trust in smart contracts can be better established if their source code is available. Since making source code available
always touches on legal problems with regards to copyright, the Solidity compiler encourages the use of machine-
readable SPDX license identifiers. Every source file should start with a comment indicating its license:

// SPDX-License-Identifier: MIT

The compiler does not validate that the license is part of the list allowed by SPDX, but it does include the supplied
string in the _bytecode metadata_.

If you do not want to specify a license or if the source code is not open-source, please use the special valueUNLICENSED.
Note thatUNLICENSED(no usage allowed, not present in SPDX license list) is different fromUNLICENSE(grants all
rights to everyone). Solidity follows the npm recommendation.

Supplying this comment of course does not free you from other obligations related to licensing like having to mention
a specific license header in each source file or the original copyright holder.

The comment is recognized by the compiler anywhere in the file at the file level, but it is recommended to put it at the
top of the file.

More information about how to use SPDX license identifiers can be found at the SPDX website.

**3.4.2 Pragmas**

Thepragmakeyword is used to enable certain compiler features or checks. A pragma directive is always local to a
source file, so you have to add the pragma to all your files if you want to enable it in your whole project. If you _import_
another file, the pragma from that file does _not_ automatically apply to the importing file.

**Version Pragma**

Source files can (and should) be annotated with a version pragma to reject compilation with future compiler versions
that might introduce incompatible changes. We try to keep these to an absolute minimum and introduce them in a way
that changes in semantics also require changes in the syntax, but this is not always possible. Because of this, it is always
a good idea to read through the changelog at least for releases that contain breaking changes. These releases always
have versions of the form0.x.0orx.0.0.

The version pragma is used as follows:pragma solidity ^0.5.2;

A source file with the line above does not compile with a compiler earlier than version 0.5.2, and it also does not work
on a compiler starting from version 0.6.0 (this second condition is added by using^). Because there will be no breaking
changes until version0.6.0, you can be sure that your code compiles the way you intended. The exact version of the
compiler is not fixed, so that bugfix releases are still possible.

**3.4. Layout of a Solidity Source File 47**


It is possible to specify more complex rules for the compiler version, these follow the same syntax used by npm.

**Note:** Using the version pragma _does not_ change the version of the compiler. It also _does not_ enable or disable features
of the compiler. It just instructs the compiler to check whether its version matches the one required by the pragma. If
it does not match, the compiler issues an error.

**ABI Coder Pragma**

By usingpragma abicoder v1orpragma abicoder v2you can select between the two implementations of the
ABI encoder and decoder.

The new ABI coder (v2) is able to encode and decode arbitrarily nested arrays and structs. Apart from supporting more
types, it involves more extensive validation and safety checks, which may result in higher gas costs, but also heightened
security. It is considered non-experimental as of Solidity 0.6.0 and it is enabled by default starting with Solidity 0.8.0.
The old ABI coder can still be selected usingpragma abicoder v1;.

The set of types supported by the new encoder is a strict superset of the ones supported by the old one. Contracts that
use it can interact with ones that do not without limitations. The reverse is possible only as long as the non-abicoder
v2contract does not try to make calls that would require decoding types only supported by the new encoder. The
compiler can detect this and will issue an error. Simply enablingabicoder v2for your contract is enough to make
the error go away.

**Note:** This pragma applies to all the code defined in the file where it is activated, regardless of where that code ends
up eventually. This means that a contract whose source file is selected to compile with ABI coder v1 can still contain
code that uses the new encoder by inheriting it from another contract. This is allowed if the new types are only used
internally and not in external function signatures.

**Note:** Up to Solidity 0.7.4, it was possible to select the ABI coder v2 by using pragma experimental
ABIEncoderV2, but it was not possible to explicitly select coder v1 because it was the default.

**Experimental Pragma**

The second pragma is the experimental pragma. It can be used to enable features of the compiler or language that are
not yet enabled by default. The following experimental pragmas are currently supported:

**ABIEncoderV2**

Because the ABI coder v2 is not considered experimental anymore, it can be selected viapragma abicoder v2
(please see above) since Solidity 0.7.4.

**48 Chapter 3. Contents**


**SMTChecker**

This component has to be enabled when the Solidity compiler is built and therefore it is not available in all Solidity
binaries. The _build instructions_ explain how to activate this option. It is activated for the Ubuntu PPA releases in most
versions, but not for the Docker images, Windows binaries or the statically-built Linux binaries. It can be activated for
solc-js via the smtCallback if you have an SMT solver installed locally and run solc-js via node (not via the browser).

If you usepragma experimental SMTChecker;, then you get additional _safety warnings_ which are obtained by
querying an SMT solver. The component does not yet support all features of the Solidity language and likely outputs
many warnings. In case it reports unsupported features, the analysis may not be fully sound.

**3.4.3 Importing other Source Files**

**Syntax and Semantics**

Solidity supports import statements to help modularise your code that are similar to those available in JavaScript (from
ES6 on). However, Solidity does not support the concept of a default export.

At a global level, you can use import statements of the following form:

import "filename";

Thefilenamepart is called an _import path_. This statement imports all global symbols from “filename” (and symbols
imported there) into the current global scope (different than in ES6 but backwards-compatible for Solidity). This form
is not recommended for use, because it unpredictably pollutes the namespace. If you add new top-level items inside
“filename”, they automatically appear in all files that import like this from “filename”. It is better to import specific
symbols explicitly.

The following example creates a new global symbolsymbolNamewhose members are all the global symbols from
"filename":

import * as symbolName from "filename";

which results in all global symbols being available in the formatsymbolName.symbol.

A variant of this syntax that is not part of ES6, but possibly useful is:

import "filename" as symbolName;

which is equivalent toimport * as symbolName from "filename";.

If there is a naming collision, you can rename symbols while importing. For example, the code below creates new
global symbolsaliasandsymbol2which referencesymbol1andsymbol2from inside"filename", respectively.

import {symbol1 as alias, symbol2} from "filename";

**3.4. Layout of a Solidity Source File 49**


**Import Paths**

In order to be able to support reproducible builds on all platforms, the Solidity compiler has to abstract away the details
of the filesystem where source files are stored. For this reason import paths do not refer directly to files in the host
filesystem. Instead the compiler maintains an internal database ( _virtual filesystem_ or _VFS_ for short) where each source
unit is assigned a unique _source unit name_ which is an opaque and unstructured identifier. The import path specified in
an import statement is translated into a source unit name and used to find the corresponding source unit in this database.

Using the _Standard JSON_ API it is possible to directly provide the names and content of all the source files as a
part of the compiler input. In this case source unit names are truly arbitrary. If, however, you want the compiler to
automatically find and load source code into the VFS, your source unit names need to be structured in a way that makes
it possible for an _import callback_ to locate them. When using the command-line compiler the default import callback
supports only loading source code from the host filesystem, which means that your source unit names must be paths.
Some environments provide custom callbacks that are more versatile. For example the Remix IDE provides one that
lets you import files from HTTP, IPFS and Swarm URLs or refer directly to packages in NPM registry.

For a complete description of the virtual filesystem and the path resolution logic used by the compiler see _Path Reso-
lution_.

**3.4.4 Comments**

Single-line comments (//) and multi-line comments (/*...*/) are possible.

// This is a single-line comment.

/*
This is a
multi-line comment.
*/

**Note:** A single-line comment is terminated by any unicode line terminator (LF, VF, FF, CR, NEL, LS or PS) in UTF-8
encoding. The terminator is still part of the source code after the comment, so if it is not an ASCII symbol (these are
NEL, LS and PS), it will lead to a parser error.

Additionally, there is another type of comment called a NatSpec comment, which is detailed in the _style guide_. They
are written with a triple slash (///) or a double asterisk block (/** ... */) and they should be used directly above
function declarations or statements.

### 3.5 Structure of a Contract

Contracts in Solidity are similar to classes in object-oriented languages. Each contract can contain declarations of _State
Variables_ , _Functions_ , _Function Modifiers_ , _Events_ , _Errors_ , _Struct Types_ and _Enum Types_. Furthermore, contracts can
inherit from other contracts.

There are also special kinds of contracts called _libraries_ and _interfaces_.

The section about _contracts_ contains more details than this section, which serves to provide a quick overview.

**50 Chapter 3. Contents**


**3.5.1 State Variables**

State variables are variables whose values are permanently stored in contract storage.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract SimpleStorage{
uintstoredData;// State variable
// ...
}

See the _Types_ section for valid state variable types and _Visibility and Getters_ for possible choices for visibility.

**3.5.2 Functions**

Functions are the executable units of code. Functions are usually defined inside a contract, but they can also be defined
outside of contracts.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

contract SimpleAuction{
functionbid()public payable {// Function
// ...
}
}

// Helper function defined outside of a contract
functionhelper(uintx) purereturns(uint) {
return x * 2;
}

_Function Calls_ can happen internally or externally and have different levels of _visibility_ towards other contracts. _Func-
tions_ accept _parameters and return variables_ to pass parameters and values between them.

**3.5.3 Function Modifiers**

Function modifiers can be used to amend the semantics of functions in a declarative way (see _Function Modifiers_ in the
contracts section).

Overloading, that is, having the same modifier name with different parameters, is not possible.

Like functions, modifiers can be _overridden_.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract Purchase{
address publicseller;

```
modifieronlySeller() {// Modifier
require(
(continues on next page)
```
**3.5. Structure of a Contract 51**


```
(continued from previous page)
msg.sender== seller,
"Only seller can call this."
);
_;
}
```
functionabort()publicview onlySeller { // Modifier usage
// ...
}
}

**3.5.4 Events**

Events are convenience interfaces with the EVM logging facilities.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.22;

eventHighestBidIncreased(addressbidder,uintamount);// Event

contract SimpleAuction{
functionbid()public payable {
// ...
emit HighestBidIncreased(msg.sender,msg.value); // Triggering event
}
}

See _Events_ in contracts section for information on how events are declared and can be used from within a dapp.

**3.5.5 Errors**

Errors allow you to define descriptive names and data for failure situations. Errors can be used in _revert statements_.
In comparison to string descriptions, errors are much cheaper and allow you to encode additional data. You can use
NatSpec to describe the error to the user.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

/// Not enough funds for transfer. Requested`requested`,
/// but only`available` available.
error NotEnoughFunds(uintrequested, uintavailable);

contract Token{
mapping(address=>uint) balances;
functiontransfer(addressto,uintamount)public{
uintbalance = balances[msg.sender];
if (balance < amount)
revert NotEnoughFunds(amount, balance);
balances[msg.sender] -= amount;
balances[to] += amount;
(continues on next page)

**52 Chapter 3. Contents**


(continued from previous page)
// ...
}
}

See _Custom Errors_ in the contracts section for more information.

**3.5.6 Struct Types**

Structs are custom defined types that can group several variables (see _Structs_ in types section).

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Ballot {
struct Voter {// Struct
uintweight;
boolvoted;
addressdelegate;
uintvote;
}
}

**3.5.7 Enum Types**

Enums can be used to create custom types with a finite set of ‘constant values’ (see _Enums_ in types section).

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Purchase{
enumState { Created, Locked, Inactive } // Enum
}

### 3.6 Types

Solidity is a statically typed language, which means that the type of each variable (state and local) needs to be specified.
Solidity provides several elementary types which can be combined to form complex types.

In addition, types can interact with each other in expressions containing operators. For a quick reference of the various
operators, see _Order of Precedence of Operators_.

The concept of “undefined” or “null” values does not exist in Solidity, but newly declared variables always have a
_default value_ dependent on its type. To handle any unexpected values, you should use the _revert function_ to revert the
whole transaction, or return a tuple with a secondboolvalue denoting success.

**3.6. Types 53**


**3.6.1 Value Types**

The following are called value types because their variables will always be passed by value, i.e. they are always copied
when they are used as function arguments or in assignments.

**Booleans**

bool: The possible values are constantstrueandfalse.

Operators:

- !(logical negation)
- &&(logical conjunction, “and”)
- ||(logical disjunction, “or”)
- ==(equality)
- !=(inequality)

The operators||and&&apply the common short-circuiting rules. This means that in the expressionf(x) || g(y),
iff(x)evaluates totrue,g(y)will not be evaluated even if it may have side-effects.

**Integers**

int/uint: Signed and unsigned integers of various sizes. Keywordsuint8touint256in steps of 8 (unsigned of 8
up to 256 bits) andint8toint256.uintandintare aliases foruint256andint256, respectively.

Operators:

- Comparisons:<=,<,==,!=,>=,>(evaluate tobool)
- Bit operators:&,|,^(bitwise exclusive or),~(bitwise negation)
- Shift operators:<<(left shift),>>(right shift)
- Arithmetic operators:+,-, unary-(only for signed integers),*,/,%(modulo),**(exponentiation)

For an integer typeX, you can usetype(X).minandtype(X).maxto access the minimum and maximum value
representable by the type.

```
Warning: Integers in Solidity are restricted to a certain range. For example, withuint32, this is 0 up to2**32
```
- 1. There are two modes in which arithmetic is performed on these types: The “wrapping” or “unchecked” mode
and the “checked” mode. By default, arithmetic is always “checked”, meaning that if an operation’s result falls
outside the value range of the type, the call is reverted through a _failing assertion_. You can switch to “unchecked”
mode usingunchecked { ... }. More details can be found in the section about _unchecked_.

**54 Chapter 3. Contents**


**Comparisons**

The value of a comparison is the one obtained by comparing the integer value.

**Bit operations**

Bit operations are performed on the two’s complement representation of the number. This means that, for example
~int256(0) == int256(-1).

**Shifts**

The result of a shift operation has the type of the left operand, truncating the result to match the type. The right operand
must be of unsigned type, trying to shift by a signed type will produce a compilation error.

Shifts can be “simulated” using multiplication by powers of two in the following way. Note that the truncation to the
type of the left operand is always performed at the end, but not mentioned explicitly.

- x << yis equivalent to the mathematical expressionx * 2**y.
- x >> yis equivalent to the mathematical expressionx / 2**y, rounded towards negative infinity.

```
Warning: Before version0.5.0a right shiftx >> yfor negativexwas equivalent to the mathematical expres-
sionx / 2**yrounded towards zero, i.e., right shifts used rounding up (towards zero) instead of rounding down
(towards negative infinity).
```
**Note:** Overflow checks are never performed for shift operations as they are done for arithmetic operations. Instead,
the result is always truncated.

**Addition, Subtraction and Multiplication**

Addition, subtraction and multiplication have the usual semantics, with two different modes in regard to over- and
underflow:

By default, all arithmetic is checked for under- or overflow, but this can be disabled using the _unchecked block_ , resulting
in wrapping arithmetic. More details can be found in that section.

The expression-xis equivalent to(T(0) - x)whereTis the type ofx. It can only be applied to signed types. The
value of-xcan be positive ifxis negative. There is another caveat also resulting from two’s complement representation:

If you haveint x = type(int).min;, then-xdoes not fit the positive range. This means thatunchecked {
assert(-x == x); }works, and the expression-xwhen used in checked mode will result in a failing assertion.

**3.6. Types 55**


**Division**

Since the type of the result of an operation is always the type of one of the operands, division on integers always results in
an integer. In Solidity, division rounds towards zero. This means thatint256(-5) / int256(2) == int256(-2).

Note that in contrast, division on _literals_ results in fractional values of arbitrary precision.

**Note:** Division by zero causes a _Panic error_. This check can **not** be disabled throughunchecked { ... }.

**Note:** The expressiontype(int).min / (-1)is the only case where division causes an overflow. In checked
arithmetic mode, this will cause a failing assertion, while in wrapping mode, the value will betype(int).min.

**Modulo**

The modulo operationa % nyields the remainderrafter the division of the operandaby the operandn, whereq =
int(a / n)andr = a - (n * q). This means that modulo results in the same sign as its left operand (or zero)
anda % n == -(-a % n)holds for negativea:

- int256(5) % int256(2) == int256(1)
- int256(5) % int256(-2) == int256(1)
- int256(-5) % int256(2) == int256(-1)
- int256(-5) % int256(-2) == int256(-1)

**Note:** Modulo with zero causes a _Panic error_. This check can **not** be disabled throughunchecked { ... }.

**Exponentiation**

Exponentiation is only available for unsigned types in the exponent. The resulting type of an exponentiation is always
equal to the type of the base. Please take care that it is large enough to hold the result and prepare for potential assertion
failures or wrapping behavior.

**Note:** In checked mode, exponentiation only uses the comparatively cheapexpopcode for small bases. For the cases
ofx**3, the expressionx*x*xmight be cheaper. In any case, gas cost tests and the use of the optimizer are advisable.

**Note:** Note that0**0is defined by the EVM as 1.

**56 Chapter 3. Contents**


**Fixed Point Numbers**

```
Warning: Fixed point numbers are not fully supported by Solidity yet. They can be declared, but cannot be
assigned to or from.
```
fixed/ufixed: Signed and unsigned fixed point number of various sizes. KeywordsufixedMxNandfixedMxN,
whereMrepresents the number of bits taken by the type andNrepresents how many decimal points are available.M
must be divisible by 8 and goes from 8 to 256 bits.Nmust be between 0 and 80, inclusive.ufixedandfixedare
aliases forufixed128x18andfixed128x18, respectively.

Operators:

- Comparisons:<=,<,==,!=,>=,>(evaluate tobool)
- Arithmetic operators:+,-, unary-,*,/,%(modulo)

**Note:** The main difference between floating point (floatanddoublein many languages, more precisely IEEE 754
numbers) and fixed point numbers is that the number of bits used for the integer and the fractional part (the part after
the decimal dot) is flexible in the former, while it is strictly defined in the latter. Generally, in floating point almost the
entire space is used to represent the number, while only a small number of bits define where the decimal point is.

**Address**

The address type comes in two largely identical flavors:

- address: Holds a 20 byte value (size of an Ethereum address).
- address payable: Same asaddress, but with the additional memberstransferandsend.

The idea behind this distinction is thataddress payableis an address you can send Ether to, while you are not
supposed to send Ether to a plainaddress, for example because it might be a smart contract that was not built to
accept Ether.

Type conversions:

Implicit conversions fromaddress payable toaddressare allowed, whereas conversions fromaddressto
address payablemust be explicit viapayable(<address>).

Explicit conversions to and fromaddressare allowed foruint160, integer literals,bytes20and contract types.

Only expressions of typeaddressand contract-type can be converted to the typeaddress payablevia the explicit
conversionpayable(...). For contract-type, this conversion is only allowed if the contract can receive Ether, i.e.,
the contract either has a _receive_ or a payable fallback function. Note thatpayable(0)is valid and is an exception to
this rule.

**Note:** If you need a variable of typeaddressand plan to send Ether to it, then declare its type asaddress payable
to make this requirement visible. Also, try to make this distinction or conversion as early as possible.

The distinction betweenaddressandaddress payablewas introduced with version 0.5.0. Also starting from that
version, contracts are not implicitly convertible to theaddresstype, but can still be explicitly converted toaddress
or toaddress payable, if they have a receive or payable fallback function.

Operators:

- <=,<,==,!=,>=and>

**3.6. Types 57**


```
Warning: If you convert a type that uses a larger byte size to an address, for example bytes32,
then theaddressis truncated. To reduce conversion ambiguity, starting with version 0.4.24, the com-
piler will force you to make the truncation explicit in the conversion. Take for example the 32-byte value
0x111122223333444455556666777788889999AAAABBBBCCCCDDDDEEEEFFFFCCCC.
You can useaddress(uint160(bytes20(b))), which results in0x111122223333444455556666777788889999aAaa,
or you can useaddress(uint160(uint256(b))), which results in0x777788889999AaAAbBbbCcccddDdeeeEfFFfCcCc.
```
**Note:** Mixed-case hexadecimal numbers conforming to EIP-55 are automatically treated as literals of theaddress
type. See _Address Literals_.

**Members of Addresses**

For a quick reference of all members of address, see _Members of Address Types_.

- balanceandtransfer

It is possible to query the balance of an address using the propertybalanceand to send Ether (in units of wei) to a
payable address using thetransferfunction:

addresspayable x =payable(0x123);
addressmyAddress =address(this);
if (x.balance < 10 && myAddress.balance >= 10) x.transfer(10);

Thetransferfunction fails if the balance of the current contract is not large enough or if the Ether transfer is rejected
by the receiving account. Thetransferfunction reverts on failure.

**Note:** Ifxis a contract address, its code (more specifically: its _Receive Ether Function_ , if present, or otherwise its
_Fallback Function_ , if present) will be executed together with thetransfercall (this is a feature of the EVM and cannot
be prevented). If that execution runs out of gas or fails in any way, the Ether transfer will be reverted and the current
contract will stop with an exception.

- send

sendis the low-level counterpart oftransfer. If the execution fails, the current contract will not stop with an excep-
tion, butsendwill returnfalse.

```
Warning: There are some dangers in usingsend: The transfer fails if the call stack depth is at 1024 (this can
always be forced by the caller) and it also fails if the recipient runs out of gas. So in order to make safe Ether
transfers, always check the return value ofsend, usetransferor even better: use a pattern where the recipient
withdraws the Ether.
```
- call,delegatecallandstaticcall

In order to interface with contracts that do not adhere to the ABI, or to get more direct control over the encoding,
the functionscall,delegatecallandstaticcallare provided. They all take a singlebytes memoryparameter
and return the success condition (as abool) and the returned data (bytes memory). The functionsabi.encode,
abi.encodePacked,abi.encodeWithSelectorandabi.encodeWithSignaturecan be used to encode struc-
tured data.

Example:

**58 Chapter 3. Contents**


bytesmemory payload = abi.encodeWithSignature("register(string)", "MyName");
(boolsuccess,bytes memory returnData) =address(nameReg).call(payload);
require(success);

```
Warning: All these functions are low-level functions and should be used with care. Specifically, any unknown
contract might be malicious and if you call it, you hand over control to that contract which could in turn call back
into your contract, so be prepared for changes to your state variables when the call returns. The regular way to
interact with other contracts is to call a function on a contract object (x.f()).
```
**Note:** Previous versions of Solidity allowed these functions to receive arbitrary arguments and would also handle a
first argument of typebytes4differently. These edge cases were removed in version 0.5.0.

It is possible to adjust the supplied gas with thegasmodifier:

address(nameReg).call{gas: 1000000}(abi.encodeWithSignature("register(string)", "MyName
˓→"));

Similarly, the supplied Ether value can be controlled too:

address(nameReg).call{value: 1 ether}(abi.encodeWithSignature("register(string)", "MyName
˓→"));

Lastly, these modifiers can be combined. Their order does not matter:

address(nameReg).call{gas: 1000000, value: 1 ether}(abi.encodeWithSignature(
˓→"register(string)", "MyName"));

In a similar way, the functiondelegatecallcan be used: the difference is that only the code of the given address is
used, all other aspects (storage, balance, ...) are taken from the current contract. The purpose ofdelegatecallis to
use library code which is stored in another contract. The user has to ensure that the layout of storage in both contracts
is suitable for delegatecall to be used.

**Note:** Prior to homestead, only a limited variant calledcallcodewas available that did not provide access to the
originalmsg.senderandmsg.valuevalues. This function was removed in version 0.5.0.

Since byzantiumstaticcallcan be used as well. This is basically the same ascall, but will revert if the called
function modifies the state in any way.

All three functionscall,delegatecallandstaticcallare very low-level functions and should only be used as a
_last resort_ as they break the type-safety of Solidity.

Thegasoption is available on all three methods, while thevalueoption is only available oncall.

**Note:** It is best to avoid relying on hardcoded gas values in your smart contract code, regardless of whether state is
read from or written to, as this can have many pitfalls. Also, access to gas might change in the future.

- codeandcodehash

You can query the deployed code for any smart contract. Use.codeto get the EVM bytecode as abytes memory,

**3.6. Types 59**


which might be empty. Use.codehashto get the Keccak-256 hash of that code (as abytes32). Note thataddr.
codehashis cheaper than usingkeccak256(addr.code).

**Note:** All contracts can be converted toaddresstype, so it is possible to query the balance of the current contract
usingaddress(this).balance.

**Contract Types**

Every _contract_ defines its own type. You can implicitly convert contracts to contracts they inherit from. Contracts can
be explicitly converted to and from theaddresstype.

Explicit conversion to and from theaddress payabletype is only possible if the contract type has a receive or payable
fallback function. The conversion is still performed usingaddress(x). If the contract type does not have a receive or
payable fallback function, the conversion toaddress payablecan be done usingpayable(address(x)). You can
find more information in the section about the _address type_.

**Note:** Before version 0.5.0, contracts directly derived from the address type and there was no distinction between
addressandaddress payable.

If you declare a local variable of contract type (MyContract c), you can call functions on that contract. Take care to
assign it from somewhere that is the same contract type.

You can also instantiate contracts (which means they are newly created). You can find more details in the _‘Contracts
via new’_ section.

The data representation of a contract is identical to that of theaddresstype and this type is also used in the _ABI_.

Contracts do not support any operators.

The members of contract types are the external functions of the contract including any state variables marked aspublic.

For a contractCyou can usetype(C)to access _type information_ about the contract.

**Fixed-size byte arrays**

The value typesbytes1,bytes2,bytes3, ...,bytes32hold a sequence of bytes from one to up to 32.

Operators:

- Comparisons:<=,<,==,!=,>=,>(evaluate tobool)
- Bit operators:&,|,^(bitwise exclusive or),~(bitwise negation)
- Shift operators:<<(left shift),>>(right shift)
- Index access: Ifxis of typebytesI, thenx[k]for0 <= k < Ireturns thekth byte (read-only).

The shifting operator works with unsigned integer type as right operand (but returns the type of the left operand), which
denotes the number of bits to shift by. Shifting by a signed type will produce a compilation error.

Members:

- .lengthyields the fixed length of the byte array (read-only).

**Note:** The typebytes1[]is an array of bytes, but due to padding rules, it wastes 31 bytes of space for each element
(except in storage). It is better to use thebytestype instead.

**60 Chapter 3. Contents**


**Note:** Prior to version 0.8.0,byteused to be an alias forbytes1.

**Address Literals**

Hexadecimal literals that pass the address checksum test, for example0xdCad3a6d3569DF655070DEd06cb7A1b2Ccd1D3AF
are ofaddresstype. Hexadecimal literals that are between 39 and 41 digits long and do not pass the checksum test
produce an error. You can prepend (for integer types) or append (for bytesNN types) zeros to remove the error.

**Note:** The mixed-case address checksum format is defined in EIP-55.

**Rational and Integer Literals**

Integer literals are formed from a sequence of digits in the range 0-9. They are interpreted as decimals. For example,
69 means sixty nine. Octal literals do not exist in Solidity and leading zeros are invalid.

Decimal fractional literals are formed by a.with at least one number after the decimal point. Examples include.1
and1.3(but not1.).

Scientific notation in the form of2e10is also supported, where the mantissa can be fractional but the exponent has to
be an integer. The literalMeEis equivalent toM * 10**E. Examples include2e10,-2e10,2e-10,2.5e1.

Underscores can be used to separate the digits of a numeric literal to aid readability. For example, decimal123_000,
hexadecimal0x2eff_abde, scientific decimal notation1_2e345_678are all valid. Underscores are only allowed
between two digits and only one consecutive underscore is allowed. There is no additional semantic meaning added to
a number literal containing underscores, the underscores are ignored.

Number literal expressions retain arbitrary precision until they are converted to a non-literal type (i.e. by using them
together with anything other than a number literal expression (like boolean literals) or by explicit conversion). This
means that computations do not overflow and divisions do not truncate in number literal expressions.

For example,(2**800 + 1) - 2**800results in the constant 1 (of typeuint8) although intermediate results would
not even fit the machine word size. Furthermore,.5 * 8results in the integer 4 (although non-integers were used in
between).

```
Warning: While most operators produce a literal expression when applied to literals, there are certain operators
that do not follow this pattern:
```
- Ternary operator (...? ... : ...),
- Array subscript (<array>[<index>]).
You might expect expressions like255 + (true? 1 : 0)or255 + [1, 2, 3][0]to be equivalent to using
the literal 256 directly, but in fact they are computed within the typeuint8and can overflow.

Any operator that can be applied to integers can also be applied to number literal expressions as long as the operands are
integers. If any of the two is fractional, bit operations are disallowed and exponentiation is disallowed if the exponent
is fractional (because that might result in a non-rational number).

Shifts and exponentiation with literal numbers as left (or base) operand and integer types as the right (exponent) operand
are always performed in theuint256(for non-negative literals) orint256(for a negative literals) type, regardless of
the type of the right (exponent) operand.

**3.6. Types 61**


```
Warning: Division on integer literals used to truncate in Solidity prior to version 0.4.0, but it now converts into a
rational number, i.e.5 / 2is not equal to 2 , but to2.5.
```
**Note:** Solidity has a number literal type for each rational number. Integer literals and rational number literals belong
to number literal types. Moreover, all number literal expressions (i.e. the expressions that contain only number literals
and operators) belong to number literal types. So the number literal expressions1 + 2and2 + 1both belong to the
same number literal type for the rational number three.

**Note:** Number literal expressions are converted into a non-literal type as soon as they are used with non-literal ex-
pressions. Disregarding types, the value of the expression assigned tobbelow evaluates to an integer. Becauseais of
typeuint128, the expression2.5 + ahas to have a proper type, though. Since there is no common type for the type
of2.5anduint128, the Solidity compiler does not accept this code.

uint128a = 1;
uint128b = 2.5 + a + 0.5;

**String Literals and Types**

String literals are written with either double or single-quotes ("foo"or'bar'), and they can also be split into multiple
consecutive parts ("foo" "bar"is equivalent to"foobar") which can be helpful when dealing with long strings.
They do not imply trailing zeroes as in C;"foo"represents three bytes, not four. As with integer literals, their type
can vary, but they are implicitly convertible tobytes1, ...,bytes32, if they fit, tobytesand tostring.

For example, withbytes32 samevar = "stringliteral"the string literal is interpreted in its raw byte form when
assigned to abytes32type.

String literals can only contain printable ASCII characters, which means the characters between and including 0x20 ..
0x7E.

Additionally, string literals also support the following escape characters:

- \<newline>(escapes an actual newline)
- \\(backslash)
- \'(single quote)
- \"(double quote)
- \n(newline)
- \r(carriage return)
- \t(tab)
- \xNN(hex escape, see below)
- \uNNNN(unicode escape, see below)

\xNNtakes a hex value and inserts the appropriate byte, while\uNNNNtakes a Unicode codepoint and inserts an UTF-8
sequence.

**Note:** Until version 0.8.0 there were three additional escape sequences:\b,\fand\v. They are commonly available
in other languages but rarely needed in practice. If you do need them, they can still be inserted via hexadecimal escapes,

**62 Chapter 3. Contents**


i.e.\x08,\x0cand\x0b, respectively, just as any other ASCII character.

The string in the following example has a length of ten bytes. It starts with a newline byte, followed by a double quote,
a single quote a backslash character and then (without separator) the character sequenceabcdef.

"\n\"\'\\abc\
def"

Any Unicode line terminator which is not a newline (i.e. LF, VF, FF, CR, NEL, LS, PS) is considered to terminate the
string literal. Newline only terminates the string literal if it is not preceded by a\.

**Unicode Literals**

While regular string literals can only contain ASCII, Unicode literals – prefixed with the keywordunicode– can
contain any valid UTF-8 sequence. They also support the very same escape sequences as regular string literals.

string memory a = unicode"Hello ";

**Hexadecimal Literals**

Hexadecimal literals are prefixed with the keywordhexand are enclosed in double or single-quotes (hex"001122FF",
hex'0011_22_FF'). Their content must be hexadecimal digits which can optionally use a single underscore as sepa-
rator between byte boundaries. The value of the literal will be the binary representation of the hexadecimal sequence.

Multiple hexadecimal literals separated by whitespace are concatenated into a single literal: hex"00112233"
hex"44556677"is equivalent tohex"0011223344556677"

Hexadecimal literals in some ways behave like _string literals_ but are not implicitly convertible to thestringtype.

**Enums**

Enums are one way to create a user-defined type in Solidity. They are explicitly convertible to and from all integer
types but implicit conversion is not allowed. The explicit conversion from integer checks at runtime that the value lies
inside the range of the enum and causes a _Panic error_ otherwise. Enums require at least one member, and its default
value when declared is the first member. Enums cannot have more than 256 members.

The data representation is the same as for enums in C: The options are represented by subsequent unsigned integer
values starting from 0.

Usingtype(NameOfEnum).minandtype(NameOfEnum).maxyou can get the smallest and respectively largest value
of the given enum.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.8;

contract test{
enumActionChoices { GoLeft, GoRight, GoStraight, SitStill }
ActionChoices choice;
ActionChoicesconstantdefaultChoice = ActionChoices.GoStraight;

```
functionsetGoStraight() public{
choice = ActionChoices.GoStraight;
}
(continues on next page)
```
**3.6. Types 63**


```
(continued from previous page)
```
```
// Since enum types are not part of the ABI, the signature of "getChoice"
// will automatically be changed to "getChoice() returns (uint8)"
// for all matters external to Solidity.
functiongetChoice()publicview returns(ActionChoices) {
returnchoice;
}
```
```
functiongetDefaultChoice()public purereturns(uint) {
return uint(defaultChoice);
}
```
```
functiongetLargestValue()public purereturns(ActionChoices) {
returntype(ActionChoices).max;
}
```
functiongetSmallestValue()public purereturns(ActionChoices) {
returntype(ActionChoices).min;
}
}

**Note:** Enums can also be declared on the file level, outside of contract or library definitions.

**User-defined Value Types**

A user-defined value type allows creating a zero cost abstraction over an elementary value type. This is similar to an
alias, but with stricter type requirements.

A user-defined value type is defined usingtype C is V, whereCis the name of the newly introduced type andVhas
to be a built-in value type (the “underlying type”). The functionC.wrapis used to convert from the underlying type to
the custom type. Similarly, the functionC.unwrapis used to convert from the custom type to the underlying type.

The typeCdoes not have any operators or attached member functions. In particular, even the operator==is not defined.
Explicit and implicit conversions to and from other types are disallowed.

The data-representation of values of such types are inherited from the underlying type and the underlying type is also
used in the ABI.

The following example illustrates a custom typeUFixed256x18representing a decimal fixed point type with 18 deci-
mals and a minimal library to do arithmetic operations on the type.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.8;

// Represent a 18 decimal, 256 bit wide fixed point type using a user-defined value type.
type UFixed256x18is uint256;

/// A minimal library to do fixed point operations on UFixed256x18.
libraryFixedMath {
uintconstant multiplier = 10**18;

```
(continues on next page)
```
**64 Chapter 3. Contents**


(continued from previous page)
/// Adds two UFixed256x18 numbers. Reverts on overflow, relying on checked
/// arithmetic on uint256.
functionadd(UFixed256x18 a, UFixed256x18 b)internalpure returns(UFixed256x18) {
returnUFixed256x18.wrap(UFixed256x18.unwrap(a) + UFixed256x18.unwrap(b));
}
/// Multiplies UFixed256x18 and uint256. Reverts on overflow, relying on checked
/// arithmetic on uint256.
functionmul(UFixed256x18 a, uint256b) internalpurereturns(UFixed256x18) {
returnUFixed256x18.wrap(UFixed256x18.unwrap(a) * b);
}
/// Take the floor of a UFixed256x18 number.
/// @return the largest integer that does not exceed`a`.
functionfloor(UFixed256x18 a)internalpurereturns(uint256) {
returnUFixed256x18.unwrap(a) / multiplier;
}
/// Turns a uint256 into a UFixed256x18 of the same value.
/// Reverts if the integer is too large.
functiontoUFixed256x18(uint256a) internalpurereturns(UFixed256x18) {
returnUFixed256x18.wrap(a * multiplier);
}
}

Notice howUFixed256x18.wrapandFixedMath.toUFixed256x18have the same signature but perform two very
different operations: TheUFixed256x18.wrapfunction returns aUFixed256x18that has the same data representation
as the input, whereastoUFixed256x18returns aUFixed256x18that has the same numerical value.

**Function Types**

Function types are the types of functions. Variables of function type can be assigned from functions and function
parameters of function type can be used to pass functions to and return functions from function calls. Function types
come in two flavours - _internal_ and _external_ functions:

Internal functions can only be called inside the current contract (more specifically, inside the current code unit, which
also includes internal library functions and inherited functions) because they cannot be executed outside of the context
of the current contract. Calling an internal function is realized by jumping to its entry label, just like when calling a
function of the current contract internally.

External functions consist of an address and a function signature and they can be passed via and returned from external
function calls.

Function types are notated as follows:

function(<parameter types>) {internal|external} [pure|view|payable] [returns(<return␣
˓→types>)]

In contrast to the parameter types, the return types cannot be empty - if the function type should not return anything,
the wholereturns (<return types>)part has to be omitted.

By default, function types are internal, so theinternalkeyword can be omitted. Note that this only applies to function
types. Visibility has to be specified explicitly for functions defined in contracts, they do not have a default.

Conversions:

A function typeAis implicitly convertible to a function typeBif and only if their parameter types are identical, their
return types are identical, their internal/external property is identical and the state mutability ofAis more restrictive

**3.6. Types 65**


than the state mutability ofB. In particular:

- purefunctions can be converted toviewandnon-payablefunctions
- viewfunctions can be converted tonon-payablefunctions
- payablefunctions can be converted tonon-payablefunctions

No other conversions between function types are possible.

The rule aboutpayableandnon-payablemight be a little confusing, but in essence, if a function ispayable, this
means that it also accepts a payment of zero Ether, so it also isnon-payable. On the other hand, anon-payable
function will reject Ether sent to it, sonon-payablefunctions cannot be converted topayablefunctions. To clarify,
rejecting ether is more restrictive than not rejecting ether. This means you can override a payable function with a
non-payable but not the other way around.

Additionally, When you define anon-payablefunction pointer, the compiler does not enforce that the pointed function
will actually reject ether. Instead, it enforces that the function pointer is never used to send ether. Which makes it
possible to assign apayablefunction pointer to anon-payablefunction pointer ensuring both types behave the
same way, i.e, both cannot be used to send ether.

If a function type variable is not initialised, calling it results in a _Panic error_. The same happens if you call a function
after usingdeleteon it.

If external function types are used outside of the context of Solidity, they are treated as thefunctiontype, which
encodes the address followed by the function identifier together in a singlebytes24type.

Note that public functions of the current contract can be used both as an internal and as an external function. To usef
as an internal function, just usef, if you want to use its external form, usethis.f.

A function of an internal type can be assigned to a variable of an internal function type regardless of where it is defined.
This includes private, internal and public functions of both contracts and libraries as well as free functions. External
function types, on the other hand, are only compatible with public and external contract functions.

**Note:** External functions withcalldataparameters are incompatible with external function types withcalldata
parameters. They are compatible with the corresponding types withmemoryparameters instead. For example, there
is no function that can be pointed at by a value of typefunction (string calldata) externalwhilefunction
(string memory) externalcan point at both function f(string memory) external {}andfunction
g(string calldata) external {}. This is because for both locations the arguments are passed to the function in
the same way. The caller cannot pass its calldata directly to an external function and always ABI-encodes the argu-
ments into memory. Marking the parameters ascalldataonly affects the implementation of the external function and
is meaningless in a function pointer on the caller’s side.

```
Warning: Comparison of internal function pointers can have unexpected results in the legacy pipeline with the
optimizer enabled, as it can collapse identical functions into one, which will then lead to said function pointers
comparing as equal instead of not. Such comparisons are not advised, and will lead to the compiler issuing a
warning, until the next breaking release (0.9.0), when the warning will be upgraded to an error, thereby making
such comparisons disallowed.
```
Libraries are excluded because they require adelegatecalland use _a different ABI convention for their selectors_.
Functions declared in interfaces do not have definitions so pointing at them does not make sense either.

Members:

External (or public) functions have the following members:

- .addressreturns the address of the contract of the function.

**66 Chapter 3. Contents**


- .selectorreturns the _ABI function selector_

**Note:** External (or public) functions used to have the additional members.gas(uint)and.value(uint). These
were deprecated in Solidity 0.6.2 and removed in Solidity 0.7.0. Instead use{gas: ...}and{value: ...}to
specify the amount of gas or the amount of wei sent to a function, respectively. See _External Function Calls_ for more
information.

Example that shows how to use the members:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.4 <0.9.0;

contract Example{
functionf()public payable returns(bytes4) {
assert(this.f.address== address(this));
return this.f.selector;
}

functiong()public {
this.f{gas: 10, value: 800}();
}
}

Example that shows how to use internal function types:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

libraryArrayUtils {
// internal functions can be used in internal library functions because
// they will be part of the same code context
functionmap(uint[] memoryself, function(uint) purereturns(uint) f)
internal
pure
returns(uint[] memoryr)
{
r =new uint[](self.length);
for(uinti = 0; i < self.length; i++) {
r[i] = f(self[i]);
}
}

```
functionreduce(
uint[]memory self,
function(uint, uint) pure returns(uint) f
)
internal
pure
returns(uintr)
{
r = self[0];
for(uinti = 1; i < self.length; i++) {
r = f(r, self[i]);
(continues on next page)
```
**3.6. Types 67**


```
(continued from previous page)
}
}
```
functionrange(uint length)internalpure returns(uint[]memory r) {
r =new uint[](length);
for(uinti = 0; i < r.length; i++) {
r[i] = i;
}
}
}

contract Pyramid{
using ArrayUtilsfor*;

```
functionpyramid(uintl) publicpurereturns(uint) {
returnArrayUtils.range(l).map(square).reduce(sum);
}
```
```
functionsquare(uintx)internal purereturns(uint) {
returnx * x;
}
```
functionsum(uintx, uinty) internalpurereturns(uint) {
returnx + y;
}
}

Another example that uses external function types:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract Oracle {
struct Request {
bytesdata;
function(uint)externalcallback;
}

```
Request[]privaterequests;
eventNewRequest(uint);
```
```
functionquery(bytes memory data,function(uint)externalcallback) public{
requests.push(Request(data, callback));
emit NewRequest(requests.length - 1);
}
```
```
functionreply(uint requestID,uintresponse) public{
// Here goes the check that the reply comes from a trusted source
requests[requestID].callback(response);
}
(continues on next page)
```
**68 Chapter 3. Contents**


```
(continued from previous page)
```
}

contract OracleUser {
Oracle constant privateORACLE_CONST =␣
˓→Oracle(address(0x00000000219ab540356cBB839Cbe05303d7705Fa));// known contract
uint privateexchangeRate;

```
functionbuySomething()public {
ORACLE_CONST.query("USD",this.oracleResponse);
}
```
functionoracleResponse(uint response)public {
require(
msg.sender== address(ORACLE_CONST),
"Only oracle can call this."
);
exchangeRate = response;
}
}

**Note:** Lambda or inline functions are planned but not yet supported.

**3.6.2 Reference Types**

Values of reference type can be modified through multiple different names. Contrast this with value types where you get
an independent copy whenever a variable of value type is used. Because of that, reference types have to be handled more
carefully than value types. Currently, reference types comprise structs, arrays and mappings. If you use a reference
type, you always have to explicitly provide the data area where the type is stored:memory(whose lifetime is limited to
an external function call),storage(the location where the state variables are stored, where the lifetime is limited to
the lifetime of a contract) orcalldata(special data location that contains the function arguments).

An assignment or type conversion that changes the data location will always incur an automatic copy operation, while
assignments inside the same data location only copy in some cases for storage types.

**Data location**

Every reference type has an additional annotation, the “data location”, about where it is stored. There are three data lo-
cations:memory,storageandcalldata. Calldata is a non-modifiable, non-persistent area where function arguments
are stored, and behaves mostly like memory.

**Note:** If you can, try to usecalldataas data location because it will avoid copies and also makes sure that the data
cannot be modified. Arrays and structs withcalldatadata location can also be returned from functions, but it is not
possible to allocate such types.

**Note:** Prior to version 0.6.9 data location for reference-type arguments was limited tocalldatain external functions,
memoryin public functions and eithermemoryorstoragein internal and private ones. Nowmemoryandcalldata

**3.6. Types 69**


are allowed in all functions regardless of their visibility.

**Note:** Prior to version 0.5.0 the data location could be omitted, and would default to different locations depending on
the kind of variable, function type, etc., but all complex types must now give an explicit data location.

**Data location and assignment behavior**

Data locations are not only relevant for persistency of data, but also for the semantics of assignments:

- Assignments betweenstorageandmemory(or fromcalldata) always create an independent copy.
- Assignments frommemorytomemoryonly create references. This means that changes to one memory variable
    are also visible in all other memory variables that refer to the same data.
- Assignments fromstorageto a **local** storage variable also only assign a reference.
- All other assignments tostoragealways copy. Examples for this case are assignments to state variables or to
    members of local variables of storage struct type, even if the local variable itself is just a reference.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
// The data location of x is storage.
// This is the only place where the
// data location can be omitted.
uint[] x;

```
// The data location of memoryArray is memory.
functionf(uint[] memory memoryArray)public{
x = memoryArray;// works, copies the whole array to storage
uint[] storage y = x;// works, assigns a pointer, data location of y is storage
y[7];// fine, returns the 8th element
y.pop();// fine, modifies x through y
delete x;// fine, clears the array, also modifies y
// The following does not work; it would need to create a new temporary /
// unnamed array in storage, but storage is "statically" allocated:
// y = memoryArray;
// Similarly, "delete y" is not valid, as assignments to local variables
// referencing storage objects can only be made from existing storage objects.
// It would "reset" the pointer, but there is no sensible location it could␣
˓→point to.
// For more details see the documentation of the "delete" operator.
// delete y;
g(x);// calls g, handing over a reference to x
h(x);// calls h and creates an independent, temporary copy in memory
}
```
functiong(uint[] storage)internalpure {}
functionh(uint[] memory) public pure {}
}

**70 Chapter 3. Contents**


**Arrays**

Arrays can have a compile-time fixed size, or they can have a dynamic size.

The type of an array of fixed sizekand element typeTis written asT[k], and an array of dynamic size asT[].

For example, an array of 5 dynamic arrays ofuintis written asuint[][5]. The notation is reversed compared to
some other languages. In Solidity,X[3]is always an array containing three elements of typeX, even ifXis itself an
array. This is not the case in other languages such as C.

Indices are zero-based, and access is in the opposite direction of the declaration.

For example, if you have a variableuint[][5] memory x, you access the seventhuintin the third dynamic array
usingx[2][6], and to access the third dynamic array, usex[2]. Again, if you have an arrayT[5] afor a typeTthat
can also be an array, thena[2]always has typeT.

Array elements can be of any type, including mapping or struct. The general restrictions for types apply, in that
mappings can only be stored in thestoragedata location and publicly-visible functions need parameters that are _ABI
types_.

It is possible to mark state variable arrayspublicand have Solidity create a _getter_. The numeric index becomes a
required parameter for the getter.

Accessing an array past its end causes a failing assertion. Methods.push()and.push(value)can be used to append
a new element at the end of a dynamically-sized array, where.push()appends a zero-initialized element and returns
a reference to it.

**Note:** Dynamically-sized arrays can only be resized in storage. In memory, such arrays can be of arbitrary size but
the size cannot be changed once an array is allocated.

bytes **and** string **as Arrays**

Variables of typebytesandstringare special arrays. Thebytestype is similar tobytes1[], but it is packed tightly
in calldata and memory.stringis equal tobytesbut does not allow length or index access.

Solidity does not have string manipulation functions, but there are third-party string libraries. You can also
compare two strings by their keccak256-hash usingkeccak256(abi.encodePacked(s1)) == keccak256(abi.
encodePacked(s2))and concatenate two strings usingstring.concat(s1, s2).

You should usebytesoverbytes1[]because it is cheaper, since usingbytes1[]inmemoryadds 31 padding bytes
between the elements. Note that instorage, the padding is absent due to tight packing, see _bytes and string_. As a
general rule, usebytesfor arbitrary-length raw byte data andstringfor arbitrary-length string (UTF-8) data. If you
can limit the length to a certain number of bytes, always use one of the value typesbytes1tobytes32because they
are much cheaper.

**Note:** If you want to access the byte-representation of a strings, usebytes(s).length/bytes(s)[7] = 'x';.
Keep in mind that you are accessing the low-level bytes of the UTF-8 representation, and not the individual characters.

**3.6. Types 71**


**The functions** bytes.concat **and** string.concat

You can concatenate an arbitrary number ofstringvalues usingstring.concat. The function returns a single
string memoryarray that contains the contents of the arguments without padding. If you want to use parameters of
other types that are not implicitly convertible tostring, you need to convert them tostringfirst.

Analogously, thebytes.concatfunction can concatenate an arbitrary number ofbytesorbytes1 ... bytes32
values. The function returns a singlebytes memoryarray that contains the contents of the arguments without padding.
If you want to use string parameters or other types that are not implicitly convertible tobytes, you need to convert
them tobytesorbytes1/.../bytes32first.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.12;

contract C {
string s = "Storage";
functionf(bytes calldata bc,stringmemory sm, bytes16b) publicview {
stringmemory concatString = string.concat(s,string(bc), "Literal", sm);
assert((bytes(s).length + bc.length + 7 + bytes(sm).length) ==␣
˓→bytes(concatString).length);

bytesmemory concatBytes =bytes.concat(bytes(s), bc, bc[:2], "Literal",␣
˓→bytes(sm), b);
assert((bytes(s).length + bc.length + 2 + 7 +bytes(sm).length + b.length) ==␣
˓→concatBytes.length);
}
}

If you callstring.concatorbytes.concatwithout arguments they return an empty array.

**Allocating Memory Arrays**

Memory arrays with dynamic length can be created using thenewoperator. As opposed to storage arrays, it is **not**
possible to resize memory arrays (e.g. the.pushmember functions are not available). You either have to calculate the
required size in advance or create a new memory array and copy every element.

As all variables in Solidity, the elements of newly allocated arrays are always initialized with the _default value_.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
functionf(uint len)publicpure {
uint[]memory a =new uint[](7);
bytesmemory b = new bytes(len);
assert(a.length == 7);
assert(b.length == len);
a[6] = 8;
}
}

**72 Chapter 3. Contents**


**Array Literals**

An array literal is a comma-separated list of one or more expressions, enclosed in square brackets ([...]). For example
[1, a, f(3)]. The type of the array literal is determined as follows:

It is always a statically-sized memory array whose length is the number of expressions.

The base type of the array is the type of the first expression on the list such that all other expressions can be implicitly
converted to it. It is a type error if this is not possible.

It is not enough that there is a type all the elements can be converted to. One of the elements has to be of that type.

In the example below, the type of[1, 2, 3]isuint8[3] memory, because the type of each of these constants is
uint8. If you want the result to be auint[3] memorytype, you need to convert the first element touint.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
functionf()public pure {
g([uint(1), 2, 3]);
}
functiong(uint[3]memory)public pure {
// ...
}
}

The array literal[1, -1]is invalid because the type of the first expression isuint8while the type of the second
isint8and they cannot be implicitly converted to each other. To make it work, you can use[int8(1), -1], for
example.

Since fixed-size memory arrays of different type cannot be converted into each other (even if the base types can), you
always have to specify a common base type explicitly if you want to use two-dimensional array literals:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
functionf()public purereturns(uint24[2][4] memory) {
uint24[2][4] memoryx = [[uint24(0x1), 1], [0xffffff, 2], [uint24(0xff), 3],␣
˓→[uint24(0xffff), 4]];
// The following does not work, because some of the inner arrays are not of the␣
˓→right type.
// uint[2][4] memory x = [[0x1, 1], [0xffffff, 2], [0xff, 3], [0xffff, 4]];
returnx;
}
}

Fixed size memory arrays cannot be assigned to dynamically-sized memory arrays, i.e. the following is not possible:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

// This will not compile.
contract C {
functionf()public {
(continues on next page)

**3.6. Types 73**


(continued from previous page)
// The next line creates a type error because uint[3] memory
// cannot be converted to uint[] memory.
uint[]memory x = [uint(1), 3, 4];
}
}

It is planned to remove this restriction in the future, but it creates some complications because of how arrays are passed
in the ABI.

If you want to initialize dynamically-sized arrays, you have to assign the individual elements:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
functionf()public pure {
uint[]memory x =new uint[](3);
x[0] = 1;
x[1] = 3;
x[2] = 4;
}
}

**Array Members**

**length:**
Arrays have alengthmember that contains their number of elements. The length of memory arrays is fixed
(but dynamic, i.e. it can depend on runtime parameters) once they are created.

**push():**
Dynamic storage arrays andbytes(notstring) have a member function calledpush()that you can use to
append a zero-initialised element at the end of the array. It returns a reference to the element, so that it can be
used likex.push().t = 2orx.push() = b.

**push(x):**
Dynamic storage arrays andbytes(notstring) have a member function calledpush(x)that you can use to
append a given element at the end of the array. The function returns nothing.

**pop():**
Dynamic storage arrays andbytes(notstring) have a member function calledpop()that you can use to
remove an element from the end of the array. This also implicitly calls _delete_ on the removed element. The
function returns nothing.

**Note:** Increasing the length of a storage array by callingpush()has constant gas costs because storage is zero-
initialised, while decreasing the length by callingpop()has a cost that depends on the “size” of the element being
removed. If that element is an array, it can be very costly, because it includes explicitly clearing the removed elements
similar to calling _delete_ on them.

**Note:** To use arrays of arrays in external (instead of public) functions, you need to activate ABI coder v2.

**74 Chapter 3. Contents**


**Note:** In EVM versions before Byzantium, it was not possible to access dynamic arrays returned from function calls.
If you call functions that return dynamic arrays, make sure to use an EVM that is set to Byzantium mode.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract ArrayContract{
uint[2**20] aLotOfIntegers;
// Note that the following is not a pair of dynamic arrays but a
// dynamic array of pairs (i.e. of fixed size arrays of length two).
// In Solidity, T[k] and T[] are always arrays with elements of type T,
// even if T itself is an array.
// Because of that, bool[2][] is a dynamic array of elements
// that are bool[2]. This is different from other languages, like C.
// Data location for all state variables is storage.
bool[2][] pairsOfFlags;

```
// newPairs is stored in memory
functionsetAllFlagPairs(bool[2][]memory newPairs)public {
// assignment to a storage array performs a copy of``newPairs``and
// replaces the complete array``pairsOfFlags``.
pairsOfFlags = newPairs;
}
```
```
struct StructType {
uint[] contents;
uintmoreInfo;
}
StructType s;
```
```
functionf(uint[] memory c)public {
// stores a reference to``s``in ``g``
StructType storage g = s;
// also changes ``s.moreInfo``.
g.moreInfo = 2;
// assigns a copy because``g.contents``
// is not a local variable, but a member of
// a local variable.
g.contents = c;
}
```
```
functionsetFlagPair(uintindex, boolflagA,boolflagB) public {
// access to a non-existing index will throw an exception
pairsOfFlags[index][0] = flagA;
pairsOfFlags[index][1] = flagB;
}
```
```
functionchangeFlagArraySize(uintnewSize)public{
// using push and pop is the only way to change the
// length of an array
if (newSize < pairsOfFlags.length) {
(continues on next page)
```
**3.6. Types 75**


```
(continued from previous page)
while(pairsOfFlags.length > newSize)
pairsOfFlags.pop();
}else if(newSize > pairsOfFlags.length) {
while(pairsOfFlags.length < newSize)
pairsOfFlags.push();
}
}
```
```
functionclear()public{
// these clear the arrays completely
delete pairsOfFlags;
delete aLotOfIntegers;
// identical effect here
pairsOfFlags =new bool[2][](0);
}
```
```
bytesbyteData;
```
```
functionbyteArrays(bytesmemory data)public {
// byte arrays ("bytes") are different as they are stored without padding,
// but can be treated identical to "uint8[]"
byteData = data;
for(uinti = 0; i < 7; i++)
byteData.push();
byteData[3] = 0x08;
delete byteData[2];
}
```
```
functionaddFlag(bool[2]memoryflag) public returns(uint) {
pairsOfFlags.push(flag);
returnpairsOfFlags.length;
}
```
```
functioncreateMemoryArray(uintsize) publicpurereturns(bytesmemory) {
// Dynamic memory arrays are created using`new`:
uint[2][]memory arrayOfPairs =new uint[2][](size);
```
```
// Inline arrays are always statically-sized and if you only
// use literals, you have to provide at least one type.
arrayOfPairs[0] = [uint(1), 2];
```
// Create a dynamic byte array:
bytesmemory b = new bytes(200);
for(uinti = 0; i < b.length; i++)
b[i] = bytes1(uint8(i));
returnb;
}
}

**76 Chapter 3. Contents**


**Dangling References to Storage Array Elements**

When working with storage arrays, you need to take care to avoid dangling references. A dangling reference is a
reference that points to something that no longer exists or has been moved without updating the reference. A dangling
reference can for example occur, if you store a reference to an array element in a local variable and then.pop()from
the containing array:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0 <0.9.0;

contract C {
uint[][] s;

functionf()public {
// Stores a pointer to the last array element of s.
uint[] storage ptr = s[s.length - 1];
// Removes the last array element of s.
s.pop();
// Writes to the array element that is no longer within the array.
ptr.push(0x42);
// Adding a new element to``s``now will not add an empty array, but
// will result in an array of length 1 with``0x42``as element.
s.push();
assert(s[s.length - 1][0] == 0x42);
}
}

The write inptr.push(0x42)will **not** revert, despite the fact thatptrno longer refers to a valid element ofs. Since
the compiler assumes that unused storage is always zeroed, a subsequents.push()will not explicitly write zeroes to
storage, so the last element ofsafter thatpush()will have length 1 and contain0x42as its first element.

Note that Solidity does not allow to declare references to value types in storage. These kinds of explicit dangling
references are restricted to nested reference types. However, dangling references can also occur temporarily when
using complex expressions in tuple assignments:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0 <0.9.0;

contract C {
uint[] s;
uint[] t;
constructor() {
// Push some initial values to the storage arrays.
s.push(0x07);
t.push(0x03);
}

```
functiong()internal returns(uint[] storage) {
s.pop();
returnt;
}
```
```
functionf()public returns(uint[]memory) {
// The following will first evaluate``s.push()``to a reference to a new element
(continues on next page)
```
**3.6. Types 77**


(continued from previous page)
// at index 1. Afterwards, the call to``g``pops this new element, resulting in
// the left-most tuple element to become a dangling reference. The assignment␣
˓→still
// takes place and will write outside the data area of ``s``.
(s.push(), g()[0]) = (0x42, 0x17);
// A subsequent push to``s``will reveal the value written by the previous
// statement, i.e. the last element of``s``at the end of this function will have
// the value``0x42``.
s.push();
returns;
}
}

It is always safer to only assign to storage once per statement and to avoid complex expressions on the left-hand-side
of an assignment.

You need to take particular care when dealing with references to elements ofbytesarrays, since a.push()on a bytes
array may switch _from short to long layout in storage_.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0 <0.9.0;

// This will report a warning
contract C {
bytesx = "012345678901234567890123456789";

functiontest() external returns(uint) {
(x.push(), x.push()) = (0x01, 0x02);
returnx.length;
}
}

Here, when the firstx.push()is evaluated,xis still stored in short layout, therebyx.push()returns a reference to
an element in the first storage slot ofx. However, the secondx.push()switches the bytes array to large layout. Now
the element thatx.push()referred to is in the data area of the array while the reference still points at its original
location, which is now a part of the length field and the assignment will effectively garble the length ofx. To be safe,
only enlarge bytes arrays by at most one element during a single assignment and do not simultaneously index-access
the array in the same statement.

While the above describes the behavior of dangling storage references in the current version of the compiler, any code
with dangling references should be considered to have _undefined behavior_. In particular, this means that any future
version of the compiler may change the behavior of code that involves dangling references.

Be sure to avoid dangling references in your code!

**78 Chapter 3. Contents**


**Array Slices**

Array slices are a view on a contiguous portion of an array. They are written asx[start:end], wherestartandend
are expressions resulting in a uint256 type (or implicitly convertible to it). The first element of the slice isx[start]
and the last element isx[end - 1].

Ifstartis greater thanendor ifendis greater than the length of the array, an exception is thrown.

Bothstartandendare optional:startdefaults to 0 andenddefaults to the length of the array.

Array slices do not have any members. They are implicitly convertible to arrays of their underlying type and support
index access. Index access is not absolute in the underlying array, but relative to the start of the slice.

Array slices do not have a type name which means no variable can have an array slices as type, they only exist in
intermediate expressions.

**Note:** As of now, array slices are only implemented for calldata arrays.

Array slices are useful to ABI-decode secondary data passed in function parameters:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.5 <0.9.0;
contract Proxy{
/// @dev Address of the client contract managed by proxy i.e., this contract
addressclient;

```
constructor(addressclient_) {
client = client_;
}
```
/// Forward call to "setOwner(address)" that is implemented by client
/// after doing basic validation on the address argument.
functionforward(bytescalldata payload)external{
bytes4 sig = bytes4(payload[:4]);
// Due to truncating behavior, bytes4(payload) performs identically.
// bytes4 sig = bytes4(payload);
if (sig == bytes4(keccak256("setOwner(address)"))) {
addressowner = abi.decode(payload[4:], (address));
require(owner != address(0), "Address of owner cannot be zero.");
}
(boolstatus,) = client.delegatecall(payload);
require(status, "Forwarded call failed.");
}
}

**3.6. Types 79**


**Structs**

Solidity provides a way to define new types in the form of structs, which is shown in the following example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

// Defines a new type with two fields.
// Declaring a struct outside of a contract allows
// it to be shared by multiple contracts.
// Here, this is not really needed.
struct Funder {
addressaddr;
uintamount;
}

contract CrowdFunding{
// Structs can also be defined inside contracts, which makes them
// visible only there and in derived contracts.
struct Campaign {
addresspayable beneficiary;
uintfundingGoal;
uintnumFunders;
uintamount;
mapping(uint=> Funder) funders;
}

```
uintnumCampaigns;
mapping(uint=> Campaign) campaigns;
```
```
functionnewCampaign(addresspayable beneficiary,uint goal)public returns(uint␣
˓→campaignID) {
campaignID = numCampaigns++; // campaignID is return variable
// We cannot use "campaigns[campaignID] = Campaign(beneficiary, goal, 0, 0)"
// because the right hand side creates a memory-struct "Campaign" that contains␣
˓→a mapping.
Campaign storage c = campaigns[campaignID];
c.beneficiary = beneficiary;
c.fundingGoal = goal;
}
```
```
functioncontribute(uintcampaignID)public payable {
Campaign storage c = campaigns[campaignID];
// Creates a new temporary memory struct, initialised with the given values
// and copies it over to storage.
// Note that you can also use Funder(msg.sender, msg.value) to initialise.
c.funders[c.numFunders++] = Funder({addr: msg.sender, amount:msg.value});
c.amount +=msg.value;
}
```
```
functioncheckGoalReached(uintcampaignID)public returns(boolreached) {
Campaign storage c = campaigns[campaignID];
if (c.amount < c.fundingGoal)
(continues on next page)
```
**80 Chapter 3. Contents**


(continued from previous page)
return false;
uintamount = c.amount;
c.amount = 0;
c.beneficiary.transfer(amount);
return true;
}
}

The contract does not provide the full functionality of a crowdfunding contract, but it contains the basic concepts
necessary to understand structs. Struct types can be used inside mappings and arrays and they can themselves contain
mappings and arrays.

It is not possible for a struct to contain a member of its own type, although the struct itself can be the value type of a
mapping member or it can contain a dynamically-sized array of its type. This restriction is necessary, as the size of the
struct has to be finite.

Note how in all the functions, a struct type is assigned to a local variable with data locationstorage. This does not
copy the struct but only stores a reference so that assignments to members of the local variable actually write to the
state.

Of course, you can also directly access the members of the struct without assigning it to a local variable, as in
campaigns[campaignID].amount = 0.

**Note:** Until Solidity 0.7.0, memory-structs containing members of storage-only types (e.g. mappings) were allowed
and assignments likecampaigns[campaignID] = Campaign(beneficiary, goal, 0, 0)in the example above
would work and just silently skip those members.

**3.6.3 Mapping Types**

Mapping types use the syntax mapping(KeyType KeyName? => ValueType ValueName?) and variables
of mapping type are declared using the syntax mapping(KeyType KeyName? => ValueType ValueName?)
VariableName. TheKeyTypecan be any built-in value type,bytes,string, or any contract or enum type. Other
user-defined or complex types, such as mappings, structs or array types are not allowed.ValueTypecan be any type, in-
cluding mappings, arrays and structs.KeyNameandValueNameare optional (somapping(KeyType => ValueType)
works as well) and can be any valid identifier that is not a type.

You can think of mappings as hash tables, which are virtually initialised such that every possible key exists and is
mapped to a value whose byte-representation is all zeros, a type’s _default value_. The similarity ends there, the key data
is not stored in a mapping, only itskeccak256hash is used to look up the value.

Because of this, mappings do not have a length or a concept of a key or value being set, and therefore cannot be erased
without extra information regarding the assigned keys (see _Clearing Mappings_ ).

Mappings can only have a data location ofstorageand thus are allowed for state variables, as storage reference types
in functions, or as parameters for library functions. They cannot be used as parameters or return parameters of contract
functions that are publicly visible. These restrictions are also true for arrays and structs that contain mappings.

You can mark state variables of mapping type aspublicand Solidity creates a _getter_ for you. TheKeyTypebecomes
a parameter with nameKeyName(if specified) for the getter. IfValueTypeis a value type or a struct, the getter returns
ValueTypewith nameValueName(if specified). IfValueTypeis an array or a mapping, the getter has one parameter
for eachKeyType, recursively.

In the example below, theMappingExamplecontract defines a publicbalancesmapping, with the key type an
address, and a value type auint, mapping an Ethereum address to an unsigned integer value. Asuintis a value

**3.6. Types 81**


type, the getter returns a value that matches the type, which you can see in theMappingUsercontract that returns the
value at the specified address.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract MappingExample {
mapping(address=>uint) publicbalances;

functionupdate(uintnewBalance)public{
balances[msg.sender] = newBalance;
}
}

contract MappingUser{
functionf()public returns(uint) {
MappingExample m =newMappingExample();
m.update(100);
returnm.balances(address(this));
}
}

The example below is a simplified version of an ERC20 token._allowancesis an example of a mapping type inside
another mapping type.

In the example below, the optionalKeyNameandValueNameare provided for the mapping. It does not affect any
contract functionality or bytecode, it only sets thenamefield for the inputs and outputs in the ABI for the mapping’s
getter.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.18;

contract MappingExampleWithNames {
mapping(addressuser =>uint balance)publicbalances;

functionupdate(uintnewBalance)public{
balances[msg.sender] = newBalance;
}
}

The example below uses_allowancesto record the amount someone else is allowed to withdraw from your account.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract MappingExample {

```
mapping(address=>uint256)private_balances;
mapping(address=>mapping(address=> uint256)) private_allowances;
```
```
eventTransfer(addressindexed from,addressindexed to,uint256value);
eventApproval(addressindexed owner, addressindexed spender,uint256value);
```
```
functionallowance(addressowner, addressspender)publicviewreturns(uint256) {
(continues on next page)
```
**82 Chapter 3. Contents**


```
(continued from previous page)
return_allowances[owner][spender];
}
```
```
functiontransferFrom(addresssender,addressrecipient,uint256amount)public␣
˓→returns(bool) {
require(_allowances[sender][msg.sender] >= amount, "ERC20: Allowance not high␣
˓→enough.");
_allowances[sender][msg.sender] -= amount;
_transfer(sender, recipient, amount);
return true;
}
```
```
functionapprove(addressspender,uint256amount)public returns (bool) {
require(spender !=address(0), "ERC20: approve to the zero address");
```
```
_allowances[msg.sender][spender] = amount;
emit Approval(msg.sender, spender, amount);
return true;
}
```
```
function_transfer(addresssender,addressrecipient,uint256amount)internal{
require(sender != address(0), "ERC20: transfer from the zero address");
require(recipient != address(0), "ERC20: transfer to the zero address");
require(_balances[sender] >= amount, "ERC20: Not enough funds.");
```
_balances[sender] -= amount;
_balances[recipient] += amount;
emit Transfer(sender, recipient, amount);
}
}

**Iterable Mappings**

You cannot iterate over mappings, i.e. you cannot enumerate their keys. It is possible, though, to implement a data
structure on top of them and iterate over that. For example, the code below implements anIterableMappinglibrary
that theUsercontract then adds data to, and thesumfunction iterates over to sum all the values.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.8;

struct IndexValue {uintkeyIndex;uintvalue; }
struct KeyFlag {uintkey;booldeleted; }

struct itmap {
mapping(uint=> IndexValue) data;
KeyFlag[] keys;
uintsize;
}

type Iteratoris uint;

```
(continues on next page)
```
**3.6. Types 83**


```
(continued from previous page)
```
libraryIterableMapping {
functioninsert(itmap storage self,uintkey, uintvalue)internal returns(bool␣
˓→replaced) {
uintkeyIndex = self.data[key].keyIndex;
self.data[key].value = value;
if (keyIndex > 0)
return true;
else{
keyIndex = self.keys.length;
self.keys.push();
self.data[key].keyIndex = keyIndex + 1;
self.keys[keyIndex].key = key;
self.size++;
return false;
}
}

```
functionremove(itmap storage self,uintkey) internal returns(boolsuccess) {
uintkeyIndex = self.data[key].keyIndex;
if (keyIndex == 0)
return false;
delete self.data[key];
self.keys[keyIndex - 1].deleted =true;
self.size --;
}
```
```
functioncontains(itmap storage self, uintkey)internalviewreturns(bool) {
returnself.data[key].keyIndex > 0;
}
```
```
functioniterateStart(itmap storage self) internalviewreturns(Iterator) {
returniteratorSkipDeleted(self, 0);
}
```
```
functioniterateValid(itmap storage self, Iterator iterator)internalviewreturns␣
˓→(bool) {
returnIterator.unwrap(iterator) < self.keys.length;
}
```
```
functioniterateNext(itmap storage self, Iterator iterator)internalviewreturns␣
˓→(Iterator) {
returniteratorSkipDeleted(self, Iterator.unwrap(iterator) + 1);
}
```
```
functioniterateGet(itmap storage self, Iterator iterator) internalviewreturns␣
˓→(uintkey,uintvalue) {
uintkeyIndex = Iterator.unwrap(iterator);
key = self.keys[keyIndex].key;
value = self.data[key].value;
}
```
```
functioniteratorSkipDeleted(itmap storage self,uintkeyIndex) privateviewreturns␣
(continues on next page)
```
**84 Chapter 3. Contents**


(continued from previous page)
˓→(Iterator) {
while(keyIndex < self.keys.length && self.keys[keyIndex].deleted)
keyIndex++;
returnIterator.wrap(keyIndex);
}
}

// How to use it
contract User{
// Just a struct holding our data.
itmap data;
// Apply library functions to the data type.
using IterableMappingforitmap;

```
// Insert something
functioninsert(uintk,uint v)public returns (uintsize) {
// This calls IterableMapping.insert(data, k, v)
data.insert(k, v);
// We can still access members of the struct,
// but we should take care not to mess with them.
returndata.size;
}
```
// Computes the sum of all stored data.
functionsum()public viewreturns(uints) {
for(
Iterator i = data.iterateStart();
data.iterateValid(i);
i = data.iterateNext(i)
) {
(,uint value) = data.iterateGet(i);
s += value;
}
}
}

**3.6.4 Operators**

Arithmetic and bit operators can be applied even if the two operands do not have the same type. For example, you can
computey = x + z, wherexis auint8andzhas the typeuint32. In these cases, the following mechanism will be
used to determine the type in which the operation is computed (this is important in case of overflow) and the type of
the operator’s result:

1. If the type of the right operand can be implicitly converted to the type of the left operand, use the type of the left
    operand,
2. if the type of the left operand can be implicitly converted to the type of the right operand, use the type of the
    right operand,
3. otherwise, the operation is not allowed.

In case one of the operands is a _literal number_ it is first converted to its “mobile type”, which is the smallest type that
can hold the value (unsigned types of the same bit-width are considered “smaller” than the signed types). If both are

**3.6. Types 85**


literal numbers, the operation is computed with effectively unlimited precision in that the expression is evaluated to
whatever precision is necessary so that none is lost when the result is used with a non-literal type.

The operator’s result type is the same as the type the operation is performed in, except for comparison operators where
the result is alwaysbool.

The operators**(exponentiation),<<and>>use the type of the left operand for the operation and the result.

**Ternary Operator**

The ternary operator is used in expressions of the form <expression>? <trueExpression> :
<falseExpression>. It evaluates one of the latter two given expressions depending upon the result of the
evaluation of the main<expression>. If<expression>evaluates totrue, then<trueExpression>will be
evaluated, otherwise<falseExpression>is evaluated.

The result of the ternary operator does not have a rational number type, even if all of its operands are rational number
literals. The result type is determined from the types of the two operands in the same way as above, converting to their
mobile type first if required.

As a consequence,255 + (true? 1 : 0)will revert due to arithmetic overflow. The reason is that(true? 1 :
0)is ofuint8type, which forces the addition to be performed inuint8as well, and 256 exceeds the range allowed
for this type.

Another consequence is that an expression like1.5 + 1.5is valid but1.5 + (true? 1.5 : 2.5)is not. This is
because the former is a rational expression evaluated in unlimited precision and only its final value matters. The latter
involves a conversion of a fractional rational number to an integer, which is currently disallowed.

**Compound and Increment/Decrement Operators**

Ifais an LValue (i.e. a variable or something that can be assigned to), the following operators are available as short-
hands:

a += eis equivalent toa = a + e. The operators-=,*=,/=,%=,|=,&=,^=,<<=and>>=are defined accordingly.
a++anda--are equivalent toa += 1/a -= 1but the expression itself still has the previous value ofa. In contrast,
--aand++ahave the same effect onabut return the value after the change.

**delete**

delete aassigns the initial value for the type toa. I.e. for integers it is equivalent toa = 0, but it can also be used
on arrays, where it assigns a dynamic array of length zero or a static array of the same length with all elements set to
their initial value.delete a[x]deletes the item at indexxof the array and leaves all other elements and the length
of the array untouched. This especially means that it leaves a gap in the array. If you plan to remove items, a _mapping_
is probably a better choice.

For structs, it assigns a struct with all members reset. In other words, the value ofaafterdelete ais the same as if
awould be declared without assignment, with the following caveat:

deletehas no effect on mappings (as the keys of mappings may be arbitrary and are generally unknown). So if
you delete a struct, it will reset all members that are not mappings and also recurse into the members unless they are
mappings. However, individual keys and what they map to can be deleted: Ifais a mapping, thendelete a[x]will
delete the value stored atx.

It is important to note thatdelete areally behaves like an assignment toa, i.e. it stores a new object ina. This
distinction is visible whenais reference variable: It will only resetaitself, not the value it referred to previously.

**86 Chapter 3. Contents**


// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract DeleteExample{
uintdata;
uint[] dataArray;

functionf()public {
uintx = data;
delete x;// sets x to 0, does not affect data
delete data;// sets data to 0, does not affect x
uint[] storage y = dataArray;
delete dataArray;// this sets dataArray.length to zero, but as uint[] is a␣
˓→complex object, also
// y is affected which is an alias to the storage object
// On the other hand: "delete y" is not valid, as assignments to local variables
// referencing storage objects can only be made from existing storage objects.
assert(y.length == 0);
}
}

**Order of Precedence of Operators**

The following is the order of precedence for operators, listed in order of evaluation.

```
Precedence Description Operator
1 Postfix increment and decrement ++,--
New expression new <typename>
Array subscripting <array>[<index>]
Member access <object>.<member>
Function-like call <func>(<args...>)
Parentheses (<statement>)
2 Prefix increment and decrement ++,--
Unary minus -
Unary operations delete
Logical NOT!
Bitwise NOT ~
3 Exponentiation **
4 Multiplication, division and modulo *,/,%
5 Addition and subtraction +,-
6 Bitwise shift operators <<,>>
7 Bitwise AND &
8 Bitwise XOR ^
9 Bitwise OR |
10 Inequality operators <,>,<=,>=
11 Equality operators ==,!=
12 Logical AND &&
13 Logical OR ||
14 Ternary operator <conditional>? <if-true> : <if-false>
Assignment operators =,|=,^=,&=,<<=,>>=,+=,-=,*=,/=,%=
15 Comma operator ,
```
**3.6. Types 87**


**3.6.5 Conversions between Elementary Types**

**Implicit Conversions**

An implicit type conversion is automatically applied by the compiler in some cases during assignments, when passing
arguments to functions and when applying operators. In general, an implicit conversion between value-types is possible
if it makes sense semantically and no information is lost.

For example,uint8is convertible touint16andint128toint256, butint8is not convertible touint256, because
uint256cannot hold values such as-1.

If an operator is applied to different types, the compiler tries to implicitly convert one of the operands to the type of
the other (the same is true for assignments). This means that operations are always performed in the type of one of the
operands.

For more details about which implicit conversions are possible, please consult the sections about the types themselves.

In the example below,yandz, the operands of the addition, do not have the same type, butuint8can be implicitly
converted touint16and not vice-versa. Because of that,yis converted to the type ofzbefore the addition is performed
in theuint16type. The resulting type of the expressiony + zisuint16. Because it is assigned to a variable of type
uint32another implicit conversion is performed after the addition.

uint8y;
uint16 z;
uint32 x = y + z;

**Explicit Conversions**

If the compiler does not allow implicit conversion but you are confident a conversion will work, an explicit type con-
version is sometimes possible. This may result in unexpected behavior and allows you to bypass some security features
of the compiler, so be sure to test that the result is what you want and expect!

Take the following example that converts a negativeintto auint:

int y = -3;
uintx =uint(y);

At the end of this code snippet,xwill have the value0xfffff..fd(64 hex characters), which is -3 in the two’s
complement representation of 256 bits.

If an integer is explicitly converted to a smaller type, higher-order bits are cut off:

uint32 a = 0x12345678;
uint16 b =uint16(a);// b will be 0x5678 now

If an integer is explicitly converted to a larger type, it is padded on the left (i.e., at the higher order end). The result of
the conversion will compare equal to the original integer:

uint16 a = 0x1234;
uint32 b =uint32(a);// b will be 0x00001234 now
assert(a == b);

Fixed-size bytes types behave differently during conversions. They can be thought of as sequences of individual bytes
and converting to a smaller type will cut off the sequence:

**88 Chapter 3. Contents**


bytes2 a = 0x1234;
bytes1 b = bytes1(a);// b will be 0x12

If a fixed-size bytes type is explicitly converted to a larger type, it is padded on the right. Accessing the byte at a fixed
index will result in the same value before and after the conversion (if the index is still in range):

bytes2 a = 0x1234;
bytes4 b = bytes4(a);// b will be 0x12340000
assert(a[0] == b[0]);
assert(a[1] == b[1]);

Since integers and fixed-size byte arrays behave differently when truncating or padding, explicit conversions between
integers and fixed-size byte arrays are only allowed, if both have the same size. If you want to convert between integers
and fixed-size byte arrays of different size, you have to use intermediate conversions that make the desired truncation
and padding rules explicit:

bytes2 a = 0x1234;
uint32 b =uint16(a);// b will be 0x00001234
uint32 c =uint32(bytes4(a));// c will be 0x12340000
uint8d =uint8(uint16(a));// d will be 0x34
uint8e =uint8(bytes1(a));// e will be 0x12

bytesarrays andbytescalldata slices can be converted explicitly to fixed bytes types (bytes1/.../bytes32). In case
the array is longer than the target fixed bytes type, truncation at the end will happen. If the array is shorter than the
target type, it will be padded with zeros at the end.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.5;

contract C {
bytess = "abcdefgh";
functionf(bytes calldata c,bytesmemory m)public viewreturns(bytes16, bytes3) {
require(c.length == 16, "");
bytes16b =bytes16(m); // if length of m is greater than 16, truncation will␣
˓→happen
b =bytes16(s); // padded on the right, so result is "abcdefgh\0\0\0\0\0\0\0\0"
bytes3 b1 = bytes3(s);// truncated, b1 equals to "abc"
b =bytes16(c[:8]); // also padded with zeros
return(b, b1);
}
}

**3.6.6 Conversions between Literals and Elementary Types**

**Integer Types**

Decimal and hexadecimal number literals can be implicitly converted to any integer type that is large enough to represent
it without truncation:

uint8a = 12;// fine
uint32 b = 1234;// fine
uint16 c = 0x123456;// fails, since it would have to truncate to 0x3456

**3.6. Types 89**


**Note:** Prior to version 0.8.0, any decimal or hexadecimal number literals could be explicitly converted to an integer
type. From 0.8.0, such explicit conversions are as strict as implicit conversions, i.e., they are only allowed if the literal
fits in the resulting range.

**Fixed-Size Byte Arrays**

Decimal number literals cannot be implicitly converted to fixed-size byte arrays. Hexadecimal number literals can be,
but only if the number of hex digits exactly fits the size of the bytes type. As an exception both decimal and hexadecimal
literals which have a value of zero can be converted to any fixed-size bytes type:

bytes2 a = 54321;// not allowed
bytes2 b = 0x12;// not allowed
bytes2 c = 0x123;// not allowed
bytes2 d = 0x1234;// fine
bytes2 e = 0x0012;// fine
bytes4 f = 0;// fine
bytes4 g = 0x0; // fine

String literals and hex string literals can be implicitly converted to fixed-size byte arrays, if their number of characters
is less than or equal to the size of the bytes type:

bytes2 a = hex"1234";// fine
bytes2 b = "xy";// fine
bytes2 c = hex"12"; // fine
bytes2 e = "x"; // fine
bytes2 f = "xyz";// not allowed

**Addresses**

As described in _Address Literals_ , hex literals of the correct size that pass the checksum test are ofaddresstype. No
other literals can be implicitly converted to theaddresstype.

Explicit conversions toaddressare allowed only frombytes20anduint160.

Anaddress acan be converted explicitly toaddress payableviapayable(a).

**Note:** Prior to version 0.8.0, it was possible to explicitly convert from any integer type (of any size, signed or unsigned)
toaddressoraddress payable. Starting with 0.8.0 only conversion fromuint160is allowed.

### 3.7 Units and Globally Available Variables

**3.7.1 Ether Units**

A literal number can take a suffix ofwei,gweioretherto specify a subdenomination of Ether, where Ether numbers
without a postfix are assumed to be Wei.

**90 Chapter 3. Contents**


assert(1 wei == 1);
assert(1 gwei == 1 e9);
assert(1 ether == 1 e18);

The only effect of the subdenomination suffix is a multiplication by a power of ten.

**Note:** The denominationsfinneyandszabohave been removed in version 0.7.0.

**3.7.2 Time Units**

Suffixes likeseconds,minutes,hours,daysandweeksafter literal numbers can be used to specify units of time
where seconds are the base unit and units are considered naively in the following way:

- 1 == 1 seconds
- 1 minutes == 60 seconds
- 1 hours == 60 minutes
- 1 days == 24 hours
- 1 weeks == 7 days

Take care if you perform calendar calculations using these units, because not every year equals 365 days and not even
every day has 24 hours because of leap seconds. Due to the fact that leap seconds cannot be predicted, an exact calendar
library has to be updated by an external oracle.

**Note:** The suffixyearshas been removed in version 0.5.0 due to the reasons above.

These suffixes cannot be applied to variables. For example, if you want to interpret a function parameter in days, you
can in the following way:

functionf(uintstart,uintdaysAfter) public {
if (block.timestamp >= start + daysAfter * 1 days) {
// ...
}
}

**3.7.3 Special Variables and Functions**

There are special variables and functions which always exist in the global namespace and are mainly used to provide
information about the blockchain or are general-use utility functions.

**3.7. Units and Globally Available Variables 91**


**Block and Transaction Properties**

- blockhash(uint blockNumber) returns (bytes32): hash of the given block whenblocknumberis one
    of the 256 most recent blocks; otherwise returns zero
- blobhash(uint index) returns (bytes32): versioned hash of theindex-th blob associated with the cur-
    rent transaction. A versioned hash consists of a single byte representing the version (currently0x01), followed
    by the last 31 bytes of the SHA256 hash of the KZG commitment (EIP-4844). Returns zero if no blob with the
    given index exists.
- block.basefee(uint): current block’s base fee (EIP-3198 and EIP-1559)
- block.blobbasefee(uint): current block’s blob base fee (EIP-7516 and EIP-4844)
- block.chainid(uint): current chain id
- block.coinbase(address payable): current block miner’s address
- block.difficulty(uint): current block difficulty (EVM < Paris). For other EVM versions it behaves as a
    deprecated alias forblock.prevrandao(EIP-4399 )
- block.gaslimit(uint): current block gaslimit
- block.number(uint): current block number
- block.prevrandao(uint): random number provided by the beacon chain (EVM >= Paris)
- block.timestamp(uint): current block timestamp as seconds since unix epoch
- gasleft() returns (uint256): remaining gas
- msg.data(bytes calldata): complete calldata
- msg.sender(address): sender of the message (current call)
- msg.sig(bytes4): first four bytes of the calldata (i.e. function identifier)
- msg.value(uint): number of wei sent with the message
- tx.gasprice(uint): gas price of the transaction
- tx.origin(address): sender of the transaction (full call chain)

**Note:** The values of all members ofmsg, includingmsg.senderandmsg.valuecan change for every **external**
function call. This includes calls to library functions.

**Note:** When contracts are evaluated off-chain rather than in context of a transaction included in a block, you should
not assume thatblock.*andtx.*refer to values from any specific block or transaction. These values are provided
by the EVM implementation that executes the contract and can be arbitrary.

**Note:** Do not rely onblock.timestamporblockhashas a source of randomness, unless you know what you are
doing.

Both the timestamp and the block hash can be influenced by miners to some degree. Bad actors in the mining community
can for example run a casino payout function on a chosen hash and just retry a different hash if they did not receive any
compensation, e.g. Ether.

The current block timestamp must be strictly larger than the timestamp of the last block, but the only guarantee is that
it will be somewhere between the timestamps of two consecutive blocks in the canonical chain.

**92 Chapter 3. Contents**


**Note:** The block hashes are not available for all blocks for scalability reasons. You can only access the hashes of the
most recent 256 blocks, all other values will be zero.

**Note:** The functionblockhashwas previously known asblock.blockhash, which was deprecated in version 0.4.22
and removed in version 0.5.0.

**Note:** The functiongasleftwas previously known asmsg.gas, which was deprecated in version 0.4.21 and removed
in version 0.5.0.

**Note:** In version 0.7.0, the aliasnow(forblock.timestamp) was removed.

**ABI Encoding and Decoding Functions**

- abi.decode(bytes memory encodedData, (...)) returns (...): ABI-decodes the given data, while
    the types are given in parentheses as second argument. Example: (uint a, uint[2] memory b, bytes
    memory c) = abi.decode(data, (uint, uint[2], bytes))
- abi.encode(...) returns (bytes memory): ABI-encodes the given arguments
- abi.encodePacked(...) returns (bytes memory): Performs _packed encoding_ of the given arguments.
    Note that packed encoding can be ambiguous!
- abi.encodeWithSelector(bytes4 selector, ...) returns (bytes memory): ABI-encodes the
    given arguments starting from the second and prepends the given four-byte selector
- abi.encodeWithSignature(string memory signature, ...) returns (bytes memory): Equiva-
    lent toabi.encodeWithSelector(bytes4(keccak256(bytes(signature))), ...)
- abi.encodeCall(function functionPointer, (...)) returns (bytes memory): ABI-encodes a
    call tofunctionPointerwith the arguments found in the tuple. Performs a full type-check, ensuring the types
    match the function signature. Result equalsabi.encodeWithSelector(functionPointer.selector, (.
    ..))

**Note:** These encoding functions can be used to craft data for external function calls without actually calling an
external function. Furthermore,keccak256(abi.encodePacked(a, b))is a way to compute the hash of structured
data (although be aware that it is possible to craft a “hash collision” using different function parameter types).

See the documentation about the _ABI_ and the _tightly packed encoding_ for details about the encoding.

**3.7. Units and Globally Available Variables 93**


**Members of bytes**

- bytes.concat(...) returns (bytes memory): _Concatenates variable number of bytes and bytes1, ...,_
    _bytes32 arguments to one byte array_

**Members of string**

- string.concat(...) returns (string memory): _Concatenates variable number of string arguments to_
    _one string array_

**Error Handling**

See the dedicated section on _assert and require_ for more details on error handling and when to use which function.

assert(bool condition)
causes a Panic error and thus state change reversion if the condition is not met - to be used for internal errors.

require(bool condition)
reverts if the condition is not met - to be used for errors in inputs or external components.

require(bool condition, string memory message)
reverts if the condition is not met - to be used for errors in inputs or external components. Also provides an error
message.

revert()
abort execution and revert state changes

revert(string memory reason)
abort execution and revert state changes, providing an explanatory string

**Mathematical and Cryptographic Functions**

addmod(uint x, uint y, uint k) returns (uint)
compute(x + y) % kwhere the addition is performed with arbitrary precision and does not wrap around at
2**256. Assert thatk != 0starting from version 0.5.0.

mulmod(uint x, uint y, uint k) returns (uint)
compute(x * y) % kwhere the multiplication is performed with arbitrary precision and does not wrap around
at2**256. Assert thatk != 0starting from version 0.5.0.

keccak256(bytes memory) returns (bytes32)
compute the Keccak-256 hash of the input

**Note:** There used to be an alias forkeccak256calledsha3, which was removed in version 0.5.0.

sha256(bytes memory) returns (bytes32)
compute the SHA-256 hash of the input

ripemd160(bytes memory) returns (bytes20)
compute RIPEMD-160 hash of the input

ecrecover(bytes32 hash, uint8 v, bytes32 r, bytes32 s) returns (address)
recover the address associated with the public key from elliptic curve signature or return zero on error. The
function parameters correspond to ECDSA values of the signature:

- r= first 32 bytes of signature

**94 Chapter 3. Contents**


- s= second 32 bytes of signature
- v= final 1 byte of signature
ecrecoverreturns anaddress, and not anaddress payable. See _address payable_ for conversion, in case
you need to transfer funds to the recovered address.
For further details, read example usage.

```
Warning: If you useecrecover, be aware that a valid signature can be turned into a different valid signature
without requiring knowledge of the corresponding private key. In the Homestead hard fork, this issue was fixed for
_transaction_ signatures (see EIP-2), but the ecrecover function remained unchanged.
This is usually not a problem unless you require signatures to be unique or use them to identify items. OpenZeppelin
has an ECDSA helper library that you can use as a wrapper forecrecoverwithout this issue.
```
**Note:** When runningsha256,ripemd160orecrecoveron a _private blockchain_ , you might encounter Out-of-Gas.
This is because these functions are implemented as “precompiled contracts” and only really exist after they receive
the first message (although their contract code is hardcoded). Messages to non-existing contracts are more expensive
and thus the execution might run into an Out-of-Gas error. A workaround for this problem is to first send Wei (1 for
example) to each of the contracts before you use them in your actual contracts. This is not an issue on the main or test
net.

**Members of Address Types**

<address>.balance **(** uint256 **)**
balance of the _Address_ in Wei

<address>.code **(** bytes memory **)**
code at the _Address_ (can be empty)

<address>.codehash **(** bytes32 **)**
the codehash of the _Address_

<address payable>.transfer(uint256 amount)
send given amount of Wei to _Address_ , reverts on failure, forwards 2300 gas stipend, not adjustable

<address payable>.send(uint256 amount) returns (bool)
send given amount of Wei to _Address_ , returnsfalseon failure, forwards 2300 gas stipend, not adjustable

<address>.call(bytes memory) returns (bool, bytes memory)
issue low-levelCALLwith the given payload, returns success condition and return data, forwards all available
gas, adjustable

<address>.delegatecall(bytes memory) returns (bool, bytes memory)
issue low-levelDELEGATECALLwith the given payload, returns success condition and return data, forwards all
available gas, adjustable

<address>.staticcall(bytes memory) returns (bool, bytes memory)
issue low-levelSTATICCALLwith the given payload, returns success condition and return data, forwards all
available gas, adjustable

For more information, see the section on _Address_.

**3.7. Units and Globally Available Variables 95**


```
Warning: You should avoid using.call()whenever possible when executing another contract function as it
bypasses type checking, function existence check, and argument packing.
```
```
Warning: There are some dangers in usingsend: The transfer fails if the call stack depth is at 1024 (this can
always be forced by the caller) and it also fails if the recipient runs out of gas. So in order to make safe Ether
transfers, always check the return value ofsend, usetransferor even better: Use a pattern where the recipient
withdraws the Ether.
```
```
Warning: Due to the fact that the EVM considers a call to a non-existing contract to always succeed, Solidity
includes an extra check using theextcodesizeopcode when performing external calls. This ensures that the
contract that is about to be called either actually exists (it contains code) or an exception is raised.
The low-level calls which operate on addresses rather than contract instances (i.e..call(),.delegatecall(),
.staticcall(),.send()and.transfer()) do not include this check, which makes them cheaper in terms of
gas but also less safe.
```
**Note:** Prior to version 0.5.0, Solidity allowed address members to be accessed by a contract instance, for example
this.balance. This is now forbidden and an explicit conversion to address must be done:address(this).balance.

**Note:** If state variables are accessed via a low-level delegatecall, the storage layout of the two contracts must align in
order for the called contract to correctly access the storage variables of the calling contract by name. This is of course
not the case if storage pointers are passed as function arguments as in the case for the high-level libraries.

**Note:** Prior to version 0.5.0,.call,.delegatecalland.staticcallonly returned the success condition and not
the return data.

**Note:** Prior to version 0.5.0, there was a member calledcallcodewith similar but slightly different semantics than
delegatecall.

**Contract-related**

this **(current contract’s type)**
The current contract, explicitly convertible to _Address_

super
A contract one level higher in the inheritance hierarchy

selfdestruct(address payable recipient)
Destroy the current contract, sending its funds to the given _Address_ and end execution. Note thatselfdestruct
has some peculiarities inherited from the EVM:

- the receiving contract’s receive function is not executed.
- the contract is only really destroyed at the end of the transaction andreverts might “undo” the destruction.

**96 Chapter 3. Contents**


Furthermore, all functions of the current contract are callable directly including the current function.

```
Warning: FromEVM >= Cancunonwards,selfdestructwill only send all Ether in the account to the given
recipient and not destroy the contract. However, whenselfdestructis called in the same transaction that creates
the contract calling it, the behaviour ofselfdestructbefore Cancun hardfork (i.e.,EVM <= Shanghai) is pre-
served and will destroy the current contract, deleting any data, including storage keys, code and the account itself.
See EIP-6780 for more details.
The new behaviour is the result of a network-wide change that affects all contracts present on the Ethereum mainnet
and testnets. It is important to note that this change is dependent on the EVM version of the chain on which the
contract is deployed. The--evm-versionsetting used when compiling the contract has no bearing on it.
Also, note that theselfdestructopcode has been deprecated in Solidity version 0.8.18, as recommended by
EIP-6049. The deprecation is still in effect and the compiler will still emit warnings on its use. Any use in newly
deployed contracts is strongly discouraged even if the new behavior is taken into account. Future changes to the
EVM might further reduce the functionality of the opcode.
```
**Note:** Prior to version 0.5.0, there was a function calledsuicidewith the same semantics asselfdestruct.

**Type Information**

The expressiontype(X)can be used to retrieve information about the typeX. Currently, there is limited support for
this feature (Xcan be either a contract or an integer type) but it might be expanded in the future.

The following properties are available for a contract typeC:

type(C).name
The name of the contract.

type(C).creationCode
Memory byte array that contains the creation bytecode of the contract. This can be used in inline assembly to
build custom creation routines, especially by using thecreate2opcode. This property can **not** be accessed in
the contract itself or any derived contract. It causes the bytecode to be included in the bytecode of the call site
and thus circular references like that are not possible.

type(C).runtimeCode
Memory byte array that contains the runtime bytecode of the contract. This is the code that is usually deployed
by the constructor ofC. IfChas a constructor that uses inline assembly, this might be different from the actually
deployed bytecode. Also note that libraries modify their runtime bytecode at time of deployment to guard against
regular calls. The same restrictions as with.creationCodealso apply for this property.

In addition to the properties above, the following properties are available for an interface typeI:

type(I).interfaceId
Abytes4value containing the EIP-165 interface identifier of the given interfaceI. This identifier is defined as
theXORof all function selectors defined within the interface itself - excluding all inherited functions.

The following properties are available for an integer typeT:

type(T).min
The smallest value representable by typeT.

type(T).max
The largest value representable by typeT.

**3.7. Units and Globally Available Variables 97**


**3.7.4 Reserved Keywords**

These keywords are reserved in Solidity. They might become part of the syntax in the future:

after,alias,apply,auto,byte,case,copyof,default,define,final,implements,in,inline,let,macro,
match,mutable,null,of,partial,promise,reference,relocatable,sealed,sizeof,static,supports,
switch,typedef,typeof,var.

### 3.8 Expressions and Control Structures

**3.8.1 Control Structures**

Most of the control structures known from curly-braces languages are available in Solidity:

There is:if,else,while,do,for,break,continue,return, with the usual semantics known from C or JavaScript.

Solidity also supports exception handling in the form oftry/catch-statements, but only for _external function calls_
and contract creation calls. Errors can be created using the _revert statement_.

Parentheses can _not_ be omitted for conditionals, but curly braces can be omitted around single-statement bodies.

Note that there is no type conversion from non-boolean to boolean types as there is in C and JavaScript, soif (1) {
... }is _not_ valid Solidity.

**3.8.2 Function Calls**

**Internal Function Calls**

Functions of the current contract can be called directly (“internally”), also recursively, as seen in this nonsensical
example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

// This will report a warning
contract C {
functiong(uint a)public purereturns(uintret) { return a + f(); }
functionf()internalpurereturns(uintret) { return g(7) + f(); }
}

These function calls are translated into simple jumps inside the EVM. This has the effect that the current memory is
not cleared, i.e. passing memory references to internally-called functions is very efficient. Only functions of the same
contract instance can be called internally.

You should still avoid excessive recursion, as every internal function call uses up at least one stack slot and there are
only 1024 slots available.

**98 Chapter 3. Contents**


**External Function Calls**

Functions can also be called using thethis.g(8);andc.g(2);notation, wherecis a contract instance andgis a
function belonging toc. Calling the functiongvia either way results in it being called “externally”, using a message
call and not directly via jumps. Please note that function calls onthiscannot be used in the constructor, as the actual
contract has not been created yet.

Functions of other contracts have to be called externally. For an external call, all function arguments have to be copied
to memory.

**Note:** A function call from one contract to another does not create its own transaction, it is a message call as part of
the overall transaction.

When calling functions of other contracts, you can specify the amount of Wei or gas sent with the call with the special
options{value: 10, gas: 10000}. Note that it is discouraged to specify gas values explicitly, since the gas costs
of opcodes can change in the future. Any Wei you send to the contract is added to the total balance of that contract:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

contract InfoFeed{
functioninfo() public payable returns(uintret) { return 42; }
}

contract Consumer{
InfoFeed feed;
functionsetFeed(InfoFeed addr)public { feed = addr; }
functioncallFeed() public{ feed.info{value: 10, gas: 800}(); }
}

You need to use the modifierpayablewith theinfofunction because otherwise, thevalueoption would not be
available.

```
Warning: Be careful thatfeed.info{value: 10, gas: 800}only locally sets thevalueand amount of
gassent with the function call, and the parentheses at the end perform the actual call. Sofeed.info{value:
10, gas: 800}does not call the function and thevalueandgassettings are lost, onlyfeed.info{value:
10, gas: 800}()performs the function call.
```
Due to the fact that the EVM considers a call to a non-existing contract to always succeed, Solidity uses the
extcodesizeopcode to check that the contract that is about to be called actually exists (it contains code) and causes
an exception if it does not. This check is skipped if the return data will be decoded after the call and thus the ABI
decoder will catch the case of a non-existing contract.

Note that this check is not performed in case of _low-level calls_ which operate on addresses rather than contract instances.

**Note:** Be careful when using high-level calls to _precompiled contracts_ , since the compiler considers them non-existing
according to the above logic even though they execute code and can return data.

Function calls also cause exceptions if the called contract itself throws an exception or goes out of gas.

**3.8. Expressions and Control Structures 99**


```
Warning: Any interaction with another contract imposes a potential danger, especially if the source code of the
contract is not known in advance. The current contract hands over control to the called contract and that may
potentially do just about anything. Even if the called contract inherits from a known parent contract, the inheriting
contract is only required to have a correct interface. The implementation of the contract, however, can be completely
arbitrary and thus, pose a danger. In addition, be prepared in case it calls into other contracts of your system or
even back into the calling contract before the first call returns. This means that the called contract can change
state variables of the calling contract via its functions. Write your functions in a way that, for example, calls to
external functions happen after any changes to state variables in your contract so your contract is not vulnerable to
a reentrancy exploit.
```
**Note:** Before Solidity 0.6.2, the recommended way to specify the value and gas was to usef.value(x).gas(g)().
This was deprecated in Solidity 0.6.2 and is no longer possible since Solidity 0.7.0.

**Function Calls with Named Parameters**

Function call arguments can be given by name, in any order, if they are enclosed in{ }as can be seen in the following
example. The argument list has to coincide by name with the list of parameters from the function declaration, but can
be in arbitrary order.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract C {
mapping(uint=> uint) data;

```
functionf()public {
set({value: 2, key: 3});
}
```
functionset(uintkey,uintvalue) public {
data[key] = value;
}
}

**Omitted Names in Function Definitions**

The names of parameters and return values in the function declaration can be omitted. Those items with omitted names
will still be present on the stack, but they are inaccessible by name. An omitted return value name can still return a
value to the caller by use of thereturnstatement.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract C {
// omitted name for parameter
functionfunc(uintk, uint)public purereturns(uint) {
returnk;
}
}

**100 Chapter 3. Contents**


**3.8.3 Creating Contracts via** new

A contract can create other contracts using thenewkeyword. The full code of the contract being created has to be
known when the creating contract is compiled so recursive creation-dependencies are not possible.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract D {
uint publicx;
constructor(uinta) payable{
x = a;
}
}

contract C {
D d =newD(4); // will be executed as part of C's constructor

```
functioncreateD(uintarg)public {
D newD =newD(arg);
newD.x();
}
```
functioncreateAndEndowD(uintarg,uintamount)public payable{
// Send ether along with the creation
D newD =newD{value: amount}(arg);
newD.x();
}
}

As seen in the example, it is possible to send Ether while creating an instance ofDusing thevalueoption, but it is not
possible to limit the amount of gas. If the creation fails (due to out-of-stack, not enough balance or other problems),
an exception is thrown.

**Salted contract creations / create2**

When creating a contract, the address of the contract is computed from the address of the creating contract and a counter
that is increased with each contract creation.

If you specify the optionsalt(a bytes32 value), then contract creation will use a different mechanism to come up with
the address of the new contract:

It will compute the address from the address of the creating contract, the given salt value, the (creation) bytecode of
the created contract and the constructor arguments.

In particular, the counter (“nonce”) is not used. This allows for more flexibility in creating contracts: You are able to
derive the address of the new contract before it is created. Furthermore, you can rely on this address also in case the
creating contracts creates other contracts in the meantime.

The main use-case here is contracts that act as judges for off-chain interactions, which only need to be created if there
is a dispute.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract D {
uint publicx;
(continues on next page)

**3.8. Expressions and Control Structures 101**


(continued from previous page)
constructor(uinta) {
x = a;
}
}

contract C {
functioncreateDSalted(bytes32salt,uint arg)public{
// This complicated expression just tells you how the address
// can be pre-computed. It is just there for illustration.
// You actually only need``new D{salt: salt}(arg)``.
addresspredictedAddress =address(uint160(uint(keccak256(abi.encodePacked(
bytes1(0xff),
address(this),
salt,
keccak256(abi.encodePacked(
type(D).creationCode,
abi.encode(arg)
))
)))));

D d =newD{salt: salt}(arg);
require(address(d) == predictedAddress);
}
}

```
Warning: There are some peculiarities in relation to salted creation. A contract can be re-created at the same
address after having been destroyed. Yet, it is possible for that newly created contract to have a different deployed
bytecode even though the creation bytecode has been the same (which is a requirement because otherwise the
address would change). This is due to the fact that the constructor can query external state that might have changed
between the two creations and incorporate that into the deployed bytecode before it is stored.
```
**3.8.4 Order of Evaluation of Expressions**

The evaluation order of expressions is not specified (more formally, the order in which the children of one node in
the expression tree are evaluated is not specified, but they are of course evaluated before the node itself). It is only
guaranteed that statements are executed in order and short-circuiting for boolean expressions is done.

**3.8.5 Assignment**

**Destructuring Assignments and Returning Multiple Values**

Solidity internally allows tuple types, i.e. a list of objects of potentially different types whose number is a constant at
compile-time. Those tuples can be used to return multiple values at the same time. These can then either be assigned
to newly declared variables or to pre-existing variables (or LValues in general).

Tuples are not proper types in Solidity, they can only be used to form syntactic groupings of expressions.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
(continues on next page)

**102 Chapter 3. Contents**


```
(continued from previous page)
```
contract C {
uintindex;

```
functionf()public purereturns(uint,bool, uint) {
return(7,true, 2);
}
```
functiong()public {
// Variables declared with type and assigned from the returned tuple,
// not all elements have to be specified (but the number must match).
(uintx, ,uint y) = f();
// Common trick to swap values -- does not work for non-value storage types.
(x, y) = (y, x);
// Components can be left out (also for variable declarations).
(index, , ) = f();// Sets the index to 7
}
}

It is not possible to mix variable declarations and non-declaration assignments, i.e. the following is not valid:(x,
uint y) = (1, 2);

**Note:** Prior to version 0.5.0 it was possible to assign to tuples of smaller size, either filling up on the left or on the
right side (which ever was empty). This is now disallowed, so both sides have to have the same number of components.

```
Warning: Be careful when assigning to multiple variables at the same time when reference types are involved,
because it could lead to unexpected copying behavior.
```
**Complications for Arrays and Structs**

The semantics of assignments are more complicated for non-value types like arrays and structs, includingbytesand
string, see _Data location and assignment behavior_ for details.

In the example below the call tog(x)has no effect onxbecause it creates an independent copy of the storage value in
memory. However,h(x)successfully modifiesxbecause only a reference and not a copy is passed.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract C {
uint[20] x;

```
functionf()public {
g(x);
h(x);
}
```
```
functiong(uint[20] memoryy) internalpure {
y[2] = 3;
(continues on next page)
```
**3.8. Expressions and Control Structures 103**


```
(continued from previous page)
}
```
functionh(uint[20] storage y) internal{
y[3] = 4;
}
}

**3.8.6 Scoping and Declarations**

A variable which is declared will have an initial default value whose byte-representation is all zeros. The “default
values” of variables are the typical “zero-state” of whatever the type is. For example, the default value for aboolis
false. The default value for theuintorinttypes is 0. For statically-sized arrays andbytes1tobytes32, each
individual element will be initialized to the default value corresponding to its type. For dynamically-sized arrays,bytes
andstring, the default value is an empty array or string. For theenumtype, the default value is its first member.

Scoping in Solidity follows the widespread scoping rules of C99 (and many other languages): Variables are visible
from the point right after their declaration until the end of the smallest{ }-block that contains the declaration. As
an exception to this rule, variables declared in the initialization part of a for-loop are only visible until the end of the
for-loop.

Variables that are parameter-like (function parameters, modifier parameters, catch parameters, ...) are visible inside
the code block that follows - the body of the function/modifier for a function and modifier parameter and the catch
block for a catch parameter.

Variables and other items declared outside of a code block, for example functions, contracts, user-defined types, etc.,
are visible even before they were declared. This means you can use state variables before they are declared and call
functions recursively.

As a consequence, the following examples will compile without warnings, since the two variables have the same name
but disjoint scopes.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
contract C {
functionminimalScoping() purepublic {
{
uintsame;
same = 1;
}

{
uintsame;
same = 3;
}
}
}

As a special example of the C99 scoping rules, note that in the following, the first assignment toxwill actually assign
the outer and not the inner variable. In any case, you will get a warning about the outer variable being shadowed.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
// This will report a warning
(continues on next page)

**104 Chapter 3. Contents**


```
(continued from previous page)
```
contract C {
functionf() purepublic returns (uint) {
uintx = 1;
{
x = 2;// this will assign to the outer variable
uintx;
}
returnx; // x has value 2
}
}

```
Warning: Before version 0.5.0 Solidity followed the same scoping rules as JavaScript, that is, a variable de-
clared anywhere within a function would be in scope for the entire function, regardless where it was declared. The
following example shows a code snippet that used to compile but leads to an error starting from version 0.5.0.
```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
// This will not compile
contract C {
functionf() purepublic returns (uint) {
x = 2;
uintx;
returnx;
}
}

**3.8.7 Checked or Unchecked Arithmetic**

An overflow or underflow is the situation where the resulting value of an arithmetic operation, when executed on an
unrestricted integer, falls outside the range of the result type.

Prior to Solidity 0.8.0, arithmetic operations would always wrap in case of under- or overflow leading to widespread
use of libraries that introduce additional checks.

Since Solidity 0.8.0, all arithmetic operations revert on over- and underflow by default, thus making the use of these
libraries unnecessary.

To obtain the previous behavior, anuncheckedblock can be used:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;
contract C {
functionf(uint a,uintb) purepublic returns (uint) {
// This subtraction will wrap on underflow.
unchecked {returna - b; }
}
functiong(uint a,uintb) purepublic returns (uint) {
// This subtraction will revert on underflow.
returna - b;
(continues on next page)

**3.8. Expressions and Control Structures 105**


(continued from previous page)
}
}

The call tof(2, 3)will return2**256-1, whileg(2, 3)will cause a failing assertion.

Theuncheckedblock can be used everywhere inside a block, but not as a replacement for a block. It also cannot be
nested.

The setting only affects the statements that are syntactically inside the block. Functions called from within an
uncheckedblock do not inherit the property.

**Note:** To avoid ambiguity, you cannot use_;inside anuncheckedblock.

The following operators will cause a failing assertion on overflow or underflow and will wrap without an error if used
inside an unchecked block:

++,--,+, binary-, unary-,*,/,%,**

+=,-=,*=,/=,%=

```
Warning: It is not possible to disable the check for division by zero or modulo by zero using theunchecked
block.
```
**Note:** Bitwise operators do not perform overflow or underflow checks. This is particularly visible when using bitwise
shifts (<<,>>,<<=,>>=) in place of integer division and multiplication by a power of 2. For exampletype(uint256).
max << 3does not revert even thoughtype(uint256).max * 8would.

**Note:** The second statement inint x = type(int).min; -x;will result in an overflow because the negative range
can hold one more value than the positive range.

Explicit type conversions will always truncate and never cause a failing assertion with the exception of a conversion
from an integer to an enum type.

**3.8.8 Error handling: Assert, Require, Revert and Exceptions**

Solidity uses state-reverting exceptions to handle errors. Such an exception undoes all changes made to the state in the
current call (and all its sub-calls) and flags an error to the caller.

When exceptions happen in a sub-call, they “bubble up” (i.e., exceptions are rethrown) automatically unless they are
caught in atry/catchstatement. Exceptions to this rule aresendand the low-level functionscall,delegatecall
andstaticcall: they returnfalseas their first return value in case of an exception instead of “bubbling up”.

```
Warning: The low-level functionscall,delegatecallandstaticcallreturntrueas their first return value
if the account called is non-existent, as part of the design of the EVM. Account existence must be checked prior to
calling if needed.
```
**106 Chapter 3. Contents**


Exceptions can contain error data that is passed back to the caller in the form of _error instances_. The built-in errors
Error(string)andPanic(uint256)are used by special functions, as explained below.Erroris used for “regular”
error conditions whilePanicis used for errors that should not be present in bug-free code.

**Panic via** assert **and Error via** require

The convenience functionsassertandrequirecan be used to check for conditions and throw an exception if the
condition is not met.

Theassertfunction creates an error of typePanic(uint256). The same error is created by the compiler in certain
situations as listed below.

Assert should only be used to test for internal errors, and to check invariants. Properly functioning code should never
create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should
fix. Language analysis tools can evaluate your contract to identify the conditions and function calls which will cause a
Panic.

A Panic exception is generated in the following situations. The error code supplied with the error data indicates the
kind of panic.

1. 0x00: Used for generic compiler inserted panics.
2. 0x01: If you callassertwith an argument that evaluates to false.
3. 0x11: If an arithmetic operation results in underflow or overflow outside of anunchecked { ... }block.
4. 0x12; If you divide or modulo by zero (e.g.5 / 0or23 % 0).
5. 0x21: If you convert a value that is too big or negative into an enum type.
6. 0x22: If you access a storage byte array that is incorrectly encoded.
7. 0x31: If you call.pop()on an empty array.
8. 0x32: If you access an array,bytesNor an array slice at an out-of-bounds or negative index (i.e.x[i]wherei
    >= x.lengthori < 0).
9. 0x41: If you allocate too much memory or create an array that is too large.
10. 0x51: If you call a zero-initialized variable of internal function type.

Therequirefunction provides three overloads:

1. require(bool)which will revert without any data (not even an error selector).
2. require(bool, string)which will revert with anError(string).
3. require(bool, error)which will revert with the custom, user supplied error provided as the second argu-
    ment.

**Note:** requirearguments are evaluated unconditionally, so take special care to make sure that they are not
expressions with unexpected side-effects. For example, inrequire(condition, CustomError(f()));and
require(condition, f());, functionf()will be called regardless of whether the supplied condition istrueor
false.

AnError(string)exception (or an exception without data) is generated by the compiler in the following situations:

1. Callingrequire(x)wherexevaluates tofalse.
2. If you userevert()orrevert("description").
3. If you perform an external function call targeting a contract that contains no code.

**3.8. Expressions and Control Structures 107**


4. If your contract receives Ether via a public function withoutpayablemodifier (including the constructor and
    the fallback function).
5. If your contract receives Ether via a public getter function.

For the following cases, the error data from the external call (if provided) is forwarded. This means that it can either
cause anErroror aPanic(or whatever else was given):

1. If a.transfer()fails.
2. If you call a function via a message call but it does not finish properly (i.e., it runs out of gas, has no match-
    ing function, or throws an exception itself), except when a low level operationcall,send,delegatecall,
    callcodeorstaticcallis used. The low level operations never throw exceptions but indicate failures by
    returningfalse.
3. If you create a contract using thenewkeyword but the contract creation _does not finish properly_.

You can optionally provide a message string or a custom error torequire, but not toassert.

**Note:** If you do not provide a string or custom error argument torequire, it will revert with empty error data, not
even including the error selector.

The following example shows how you can userequireto check conditions on inputs andassertfor internal error
checking.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract Sharer {
functionsendHalf(addresspayable addr)public payable returns(uintbalance) {
require(msg.value% 2 == 0, "Even value required.");
uintbalanceBeforeTransfer = address(this).balance;
addr.transfer(msg.value/ 2);
// Since transfer throws an exception on failure and
// cannot call back here, there should be no way for us to
// still have half of the Ether.
assert(address(this).balance == balanceBeforeTransfer - msg.value/ 2);
return address(this).balance;
}
}

Internally, Solidity performs a revert operation (instruction0xfd). This causes the EVM to revert all changes made to
the state. The reason for reverting is that there is no safe way to continue execution, because an expected effect did not
occur. Because we want to keep the atomicity of transactions, the safest action is to revert all changes and make the
whole transaction (or at least call) without effect.

In both cases, the caller can react on such failures usingtry/catch, but the changes in the callee will always be reverted.

**Note:** Panic exceptions used to use theinvalidopcode before Solidity 0.8.0, which consumed all gas available to
the call. Exceptions that userequireused to consume all gas until before the Metropolis release.

**108 Chapter 3. Contents**


revert

A direct revert can be triggered using therevertstatement and therevertfunction.

Therevertstatement takes a custom error as direct argument without parentheses:

```
revert CustomError(arg1, arg2);
```
For backward-compatibility reasons, there is also therevert()function, which uses parentheses and accepts a string:

```
revert(); revert(“description”);
```
The error data will be passed back to the caller and can be caught there. Usingrevert()causes a revert without any
error data whilerevert("description")will create anError(string)error.

Using a custom error instance will usually be much cheaper than a string description, because you can use the name of
the error to describe it, which is encoded in only four bytes. A longer description can be supplied via NatSpec which
does not incur any costs.

The following example shows how to use an error string and a custom error instance together withrevertand the
equivalentrequire:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract VendingMachine {
addressowner;
error Unauthorized();
functionbuy(uintamount)public payable{
if (amount >msg.value/ 2 ether)
revert("Not enough Ether provided.");
// Alternative way to do it:
require(
amount <=msg.value/ 2 ether,
"Not enough Ether provided."
);
// Perform the purchase.
}
functionwithdraw() public{
if (msg.sender != owner)
revert Unauthorized();

payable(msg.sender).transfer(address(this).balance);
}
}

The two waysif (!condition) revert(...);andrequire(condition, ...);are equivalent as long as the
arguments torevertandrequiredo not have side-effects, for example if they are just strings.

**Note:** Therequirefunction is evaluated just as any other function. This means that all arguments are evaluated
before the function itself is executed. In particular, inrequire(condition, f())the functionfis executed even if
conditionis true.

The provided string is _abi-encoded_ as if it were a call to a functionError(string). In the above example,
revert("Not enough Ether provided.");returns the following hexadecimal as error return data:

**3.8. Expressions and Control Structures 109**


0x08c379a0 // Function selector␣
˓→for Error(string)
0x0000000000000000000000000000000000000000000000000000000000000020// Data offset
0x000000000000000000000000000000000000000000000000000000000000001a// String length
0x4e6f7420656e6f7567682045746865722070726f76696465642e000000000000// String data

The provided message can be retrieved by the caller usingtry/catchas shown below.

**Note:** There used to be a keyword calledthrowwith the same semantics asrevert()which was deprecated in
version 0.4.13 and removed in version 0.5.0.

try **/** catch

A failure in an external call can be caught using a try/catch statement, as follows:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;

interface DataFeed {functiongetData(addresstoken)external returns(uint value); }

contract FeedConsumer{
DataFeed feed;
uinterrorCount;
functionrate(addresstoken) public returns(uintvalue, boolsuccess) {
// Permanently disable the mechanism if there are
// more than 10 errors.
require(errorCount < 10);
try feed.getData(token)returns(uint v) {
return(v,true);
} catch Error(string memory/*reason*/) {
// This is executed in case
// revert was called inside getData
// and a reason string was provided.
errorCount++;
return(0,false);
} catch Panic(uint/*errorCode*/) {
// This is executed in case of a panic,
// i.e. a serious error like division by zero
// or overflow. The error code can be used
// to determine the kind of error.
errorCount++;
return(0,false);
} catch (bytesmemory /*lowLevelData*/) {
// This is executed in case revert() was used.
errorCount++;
return(0,false);
}
}
}

Thetrykeyword has to be followed by an expression representing an external function call or a contract creation (new

**110 Chapter 3. Contents**


ContractName()). Errors inside the expression are not caught (for example if it is a complex expression that also
involves internal function calls), only a revert happening inside the external call itself. Thereturnspart (which is
optional) that follows declares return variables matching the types returned by the external call. In case there was no
error, these variables are assigned and the contract’s execution continues inside the first success block. If the end of the
success block is reached, execution continues after thecatchblocks.

Solidity supports different kinds of catch blocks depending on the type of error:

- catch Error(string memory reason) { ... }: This catch clause is executed if the error was caused by
    revert("reasonString")orrequire(false, "reasonString")(or an internal error that causes such an
    exception).
- catch Panic(uint errorCode) { ... }: If the error was caused by a panic, i.e. by a failingassert,
    division by zero, invalid array access, arithmetic overflow and others, this catch clause will be run.
- catch (bytes memory lowLevelData) { ... }: This clause is executed if the error signature does not
    match any other clause, if there was an error while decoding the error message, or if no error data was provided
    with the exception. The declared variable provides access to the low-level error data in that case.
- catch { ... }: If you are not interested in the error data, you can just usecatch { ... }(even as the only
    catch clause) instead of the previous clause.

It is planned to support other types of error data in the future. The stringsErrorandPanicare currently parsed as is
and are not treated as identifiers.

In order to catch all error cases, you have to have at least the clausecatch { ...}or the clausecatch (bytes
memory lowLevelData) { ... }.

The variables declared in thereturnsand thecatchclause are only in scope in the block that follows.

**Note:** If an error happens during the decoding of the return data inside a try/catch-statement, this causes an exception
in the currently executing contract and because of that, it is not caught in the catch clause. If there is an error during
decoding ofcatch Error(string memory reason)and there is a low-level catch clause, this error is caught there.

**Note:** If execution reaches a catch-block, then the state-changing effects of the external call have been reverted. If
execution reaches the success block, the effects were not reverted. If the effects have been reverted, then execution
either continues in a catch block or the execution of the try/catch statement itself reverts (for example due to decoding
failures as noted above or due to not providing a low-level catch clause).

**Note:** The reason behind a failed call can be manifold. Do not assume that the error message is coming directly from
the called contract: The error might have happened deeper down in the call chain and the called contract just forwarded
it. Also, it could be due to an out-of-gas situation and not a deliberate error condition: The caller always retains at least
1/64th of the gas in a call and thus even if the called contract goes out of gas, the caller still has some gas left.

**3.8. Expressions and Control Structures 111**


### 3.9 Contracts

Contracts in Solidity are similar to classes in object-oriented languages. They contain persistent data in state variables,
and functions that can modify these variables. Calling a function on a different contract (instance) will perform an EVM
function call and thus switch the context such that state variables in the calling contract are inaccessible. A contract
and its functions need to be called for anything to happen. There is no “cron” concept in Ethereum to call a function at
a particular event automatically.

**3.9.1 Creating Contracts**

Contracts can be created “from outside” via Ethereum transactions or from within Solidity contracts.

IDEs, such as Remix, make the creation process seamless using UI elements.

One way to create contracts programmatically on Ethereum is via the JavaScript API web3.js. It has a function called
web3.eth.Contract to facilitate contract creation.

When a contract is created, its _constructor_ (a function declared with theconstructorkeyword) is executed once.

A constructor is optional. Only one constructor is allowed, which means overloading is not supported.

After the constructor has executed, the final code of the contract is stored on the blockchain. This code includes all
public and external functions and all functions that are reachable from there through function calls. The deployed code
does not include the constructor code or internal functions only called from the constructor.

Internally, constructor arguments are passed _ABI encoded_ after the code of the contract itself, but you do not have to
care about this if you useweb3.js.

If a contract wants to create another contract, the source code (and the binary) of the created contract has to be known
to the creator. This means that cyclic creation dependencies are impossible.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.22 <0.9.0;

contract OwnedToken {
// `TokenCreator`is a contract type that is defined below.
// It is fine to reference it as long as it is not used
// to create a new contract.
TokenCreator creator;
addressowner;
bytes32name;

```
// This is the constructor which registers the
// creator and the assigned name.
constructor(bytes32name_) {
// State variables are accessed via their name
// and not via e.g.`this.owner`. Functions can
// be accessed directly or through`this.f`,
// but the latter provides an external view
// to the function. Especially in the constructor,
// you should not access functions externally,
// because the function does not exist yet.
// See the next section for details.
owner =msg.sender;
(continues on next page)
```
**112 Chapter 3. Contents**


```
(continued from previous page)
```
```
// We perform an explicit type conversion from`address`
// to`TokenCreator` and assume that the type of
// the calling contract is`TokenCreator`, there is
// no real way to verify that.
// This does not create a new contract.
creator = TokenCreator(msg.sender);
name = name_;
}
```
```
functionchangeName(bytes32newName)public {
// Only the creator can alter the name.
// We compare the contract based on its
// address which can be retrieved by
// explicit conversion to address.
if (msg.sender ==address(creator))
name = newName;
}
```
```
functiontransfer(addressnewOwner)public {
// Only the current owner can transfer the token.
if (msg.sender != owner)return;
```
// We ask the creator contract if the transfer
// should proceed by using a function of the
// `TokenCreator`contract defined below. If
// the call fails (e.g. due to out-of-gas),
// the execution also fails here.
if (creator.isTokenTransferOK(owner, newOwner))
owner = newOwner;
}
}

contract TokenCreator{
functioncreateToken(bytes32name)
public
returns(OwnedToken tokenAddress)
{
// Create a new `Token` contract and return its address.
// From the JavaScript side, the return type
// of this function is`address`, as this is
// the closest type available in the ABI.
return newOwnedToken(name);
}

```
functionchangeName(OwnedToken tokenAddress,bytes32name) public{
// Again, the external type of`tokenAddress` is
// simply`address`.
tokenAddress.changeName(name);
}
```
```
(continues on next page)
```
**3.9. Contracts 113**


(continued from previous page)
// Perform checks to determine if transferring a token to the
// `OwnedToken` contract should proceed
functionisTokenTransferOK(addresscurrentOwner,addressnewOwner)
public
pure
returns(boolok)
{
// Check an arbitrary condition to see if transfer should proceed
returnkeccak256(abi.encodePacked(currentOwner, newOwner))[0] == 0x7f;
}
}

**3.9.2 Visibility and Getters**

**State Variable Visibility**

public
Public state variables differ from internal ones only in that the compiler automatically generates _getter functions_
for them, which allows other contracts to read their values. When used within the same contract, the external
access (e.g.this.x) invokes the getter while internal access (e.g.x) gets the variable value directly from storage.
Setter functions are not generated so other contracts cannot directly modify their values.

internal
Internal state variables can only be accessed from within the contract they are defined in and in derived contracts.
They cannot be accessed externally. This is the default visibility level for state variables.

private
Private state variables are like internal ones but they are not visible in derived contracts.

```
Warning: Making somethingprivateorinternalonly prevents other contracts from reading or modifying the
information, but it will still be visible to the whole world outside of the blockchain.
```
**Function Visibility**

Solidity knows two kinds of function calls: external ones that do create an actual EVM message call and internal ones
that do not. Furthermore, internal functions can be made inaccessible to derived contracts. This gives rise to four types
of visibility for functions.

external
External functions are part of the contract interface, which means they can be called from other contracts and via
transactions. An external functionfcannot be called internally (i.e.f()does not work, butthis.f()works).

public
Public functions are part of the contract interface and can be either called internally or via message calls.

internal
Internal functions can only be accessed from within the current contract or contracts deriving from it. They
cannot be accessed externally. Since they are not exposed to the outside through the contract’s ABI, they can
take parameters of internal types like mappings or storage references.

private
Private functions are like internal ones but they are not visible in derived contracts.

**114 Chapter 3. Contents**


```
Warning: Making somethingprivateorinternalonly prevents other contracts from reading or modifying the
information, but it will still be visible to the whole world outside of the blockchain.
```
The visibility specifier is given after the type for state variables and between parameter list and return parameter list
for functions.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
functionf(uint a)privatepurereturns(uint b) {returna + 1; }
functionsetData(uinta) internal{ data = a; }
uint publicdata;
}

In the following example,D, can callc.getData()to retrieve the value ofdatain state storage, but is not able to call
f. ContractEis derived fromCand, thus, can callcompute.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
uint privatedata;

functionf(uint a)privatepurereturns(uintb) {return a + 1; }
functionsetData(uinta) public{ data = a; }
functiongetData()public viewreturns(uint) {returndata; }
functioncompute(uinta, uintb) internalpurereturns(uint) {returna + b; }
}

// This will not compile
contract D {
functionreadData() public{
C c =newC();
uintlocal = c.f(7); // error: member`f` is not visible
c.setData(3);
local = c.getData();
local = c.compute(3, 5);// error: member`compute` is not visible
}
}

contract E isC {
functiong()public {
C c =newC();
uintval = compute(3, 5);// access to internal member (from derived to parent␣
˓→contract)
}
}

**3.9. Contracts 115**


**Getter Functions**

The compiler automatically creates getter functions for all **public** state variables. For the contract given below, the
compiler will generate a function calleddatathat does not take any arguments and returns auint, the value of the
state variabledata. State variables can be initialized when they are declared.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract C {
uint publicdata = 42;
}

contract Caller {
C c =newC();
functionf()public viewreturns(uint) {
returnc.data();
}
}

The getter functions have external visibility. If the symbol is accessed internally (i.e. withoutthis.), it evaluates to a
state variable. If it is accessed externally (i.e. withthis.), it evaluates to a function.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract C {
uint publicdata;
functionx()public returns(uint) {
data = 3;// internal access
return this.data();// external access
}
}

If you have apublicstate variable of array type, then you can only retrieve single elements of the array via the generated
getter function. This mechanism exists to avoid high gas costs when returning an entire array. You can use arguments
to specify which individual element to return, for examplemyArray(0). If you want to return an entire array in one
call, then you need to write a function, for example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract arrayExample{
// public state variable
uint[] publicmyArray;

```
// Getter function generated by the compiler
/*
function myArray(uint i) public view returns (uint) {
return myArray[i];
}
*/
```
```
// function that returns entire array
(continues on next page)
```
**116 Chapter 3. Contents**


(continued from previous page)
functiongetArray() publicviewreturns(uint[] memory) {
returnmyArray;
}
}

Now you can usegetArray()to retrieve the entire array, instead ofmyArray(i), which returns a single element per
call.

The next example is more complex:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Complex{
struct Data {
uinta;
bytes3 b;
mapping(uint=> uint) map;
uint[3] c;
uint[] d;
bytese;
}
mapping(uint=> mapping(bool => Data[]))public data;
}

It generates a function of the following form. The mapping and arrays (with the exception of byte arrays) in the struct
are omitted because there is no good way to select individual struct members or provide a key for the mapping:

functiondata(uintarg1, boolarg2,uintarg3)
public
returns(uinta, bytes3 b,bytes memory e)
{
a = data[arg1][arg2][arg3].a;
b = data[arg1][arg2][arg3].b;
e = data[arg1][arg2][arg3].e;
}

**3.9.3 Function Modifiers**

Modifiers can be used to change the behavior of functions in a declarative way. For example, you can use a modifier to
automatically check a condition prior to executing the function.

Modifiers are inheritable properties of contracts and may be overridden by derived contracts, but only if they are marked
virtual. For details, please see _Modifier Overriding_.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

contract owned{
constructor() { owner =payable(msg.sender); }
addresspayable owner;

```
(continues on next page)
```
**3.9. Contracts 117**


(continued from previous page)
// This contract only defines a modifier but does not use
// it: it will be used in derived contracts.
// The function body is inserted where the special symbol
// `_;` in the definition of a modifier appears.
// This means that if the owner calls this function, the
// function is executed and otherwise, an exception is
// thrown.
modifieronlyOwner {
require(
msg.sender== owner,
"Only owner can call this function."
);
_;
}
}

contract priced {
// Modifiers can receive arguments:
modifiercosts(uint price) {
if (msg.value>= price) {
_;
}
}
}

contract Register ispriced, owned {
mapping(address=>bool) registeredAddresses;
uintprice;

```
constructor(uintinitialPrice) { price = initialPrice; }
```
```
// It is important to also provide the
// `payable`keyword here, otherwise the function will
// automatically reject all Ether sent to it.
functionregister() public payablecosts(price) {
registeredAddresses[msg.sender] =true;
}
```
// This contract inherits the`onlyOwner` modifier from
// the `owned` contract. As a result, calls to`changePrice`will
// only take effect if they are made by the stored owner.
functionchangePrice(uintprice_)publiconlyOwner {
price = price_;
}
}

contract Mutex{
boollocked;
modifiernoReentrancy() {
require(
!locked,
"Reentrant call."
(continues on next page)

**118 Chapter 3. Contents**


```
(continued from previous page)
);
locked =true;
_;
locked =false;
}
```
/// This function is protected by a mutex, which means that
/// reentrant calls from within`msg.sender.call` cannot call`f`again.
/// The`return 7`statement assigns 7 to the return value but still
/// executes the statement`locked = false`in the modifier.
functionf()public noReentrancyreturns(uint) {
(boolsuccess,) =msg.sender.call("");
require(success);
return7;
}
}

If you want to access a modifiermdefined in a contractC, you can useC.mto reference it without virtual lookup. It
is only possible to use modifiers defined in the current contract or its base contracts. Modifiers can also be defined in
libraries but their use is limited to functions of the same library.

Multiple modifiers are applied to a function by specifying them in a whitespace-separated list and are evaluated in the
order presented.

Modifiers cannot implicitly access or change the arguments and return values of functions they modify. Their values
can only be passed to them explicitly at the point of invocation.

In function modifiers, it is necessary to specify when you want the function to which the modifier is applied to be run.
The placeholder statement (denoted by a single underscore character_) is used to denote where the body of the function
being modified should be inserted. Note that the placeholder operator is different from using underscores as leading or
trailing characters in variable names, which is a stylistic choice.

Explicit returns from a modifier or function body only leave the current modifier or function body. Return variables
are assigned and control flow continues after the_in the preceding modifier.

```
Warning: In an earlier version of Solidity,returnstatements in functions having modifiers behaved differently.
```
An explicit return from a modifier withreturn;does not affect the values returned by the function. The modifier
can, however, choose not to execute the function body at all and in that case the return variables are set to their _default
values_ just as if the function had an empty body.

The_symbol can appear in the modifier multiple times. Each occurrence is replaced with the function body, and the
function returns the return value of the final occurrence.

Arbitrary expressions are allowed for modifier arguments and in this context, all symbols visible from the function are
visible in the modifier. Symbols introduced in the modifier are not visible in the function (as they might change by
overriding).

**3.9. Contracts 119**


**3.9.4 Constant and Immutable State Variables**

State variables can be declared asconstantorimmutable. In both cases, the variables cannot be modified after the
contract has been constructed. Forconstantvariables, the value has to be fixed at compile-time, while forimmutable,
it can still be assigned at construction time.

It is also possible to defineconstantvariables at the file level.

The compiler does not reserve a storage slot for these variables, and every occurrence is replaced by the respective
value.

Compared to regular state variables, the gas costs of constant and immutable variables are much lower. For a constant
variable, the expression assigned to it is copied to all the places where it is accessed and also re-evaluated each time.
This allows for local optimizations. Immutable variables are evaluated once at construction time and their value is
copied to all the places in the code where they are accessed. For these values, 32 bytes are reserved, even if they would
fit in fewer bytes. Due to this, constant values can sometimes be cheaper than immutable values.

Not all types for constants and immutables are implemented at this time. The only supported types are _strings_ (only
for constants) and _value types_.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.21;

uintconstant X = 32**22 + 8;

contract C {
string constant TEXT = "abc";
bytes32constant MY_HASH = keccak256("abc");
uintimmutable decimals = 18;
uintimmutable maxBalance;
addressimmutable owner =msg.sender;

```
constructor(uintdecimals_,addressref) {
if (decimals_ != 0)
// Immutables are only immutable when deployed.
// At construction time they can be assigned to any number of times.
decimals = decimals_;
```
```
// Assignments to immutables can even access the environment.
maxBalance = ref.balance;
}
```
functionisBalanceTooHigh(addressother)public viewreturns(bool) {
returnother.balance > maxBalance;
}
}

**120 Chapter 3. Contents**


**Constant**

Forconstantvariables, the value has to be a constant at compile time and it has to be assigned where the variable is
declared. Any expression that accesses storage, blockchain data (e.g.block.timestamp,address(this).balance
orblock.number) or execution data (msg.valueorgasleft()) or makes calls to external contracts is disallowed.
Expressions that might have a side-effect on memory allocation are allowed, but those that might have a side-effect
on other memory objects are not. The built-in functionskeccak256,sha256,ripemd160,ecrecover,addmodand
mulmodare allowed (even though, with the exception ofkeccak256, they do call external contracts).

The reason behind allowing side-effects on the memory allocator is that it should be possible to construct complex
objects like e.g. lookup-tables. This feature is not yet fully usable.

**Immutable**

Variables declared asimmutableare a bit less restricted than those declared asconstant: Immutable variables can
be assigned a value at construction time. The value can be changed at any time before deployment and then it becomes
permanent.

One additional restriction is that immutables can only be assigned to inside expressions for which there is no possibility
of being executed after creation. This excludes all modifier definitions and functions other than constructors.

There are no restrictions on reading immutable variables. The read is even allowed to happen before the variable is
written to for the first time because variables in Solidity always have a well-defined initial value. For this reason it is
also allowed to never explicitly assign a value to an immutable.

```
Warning: When accessing immutables at construction time, please keep the initialization order in mind. Even if
you provide an explicit initializer, some expressions may end up being evaluated before that initializer, especially
when they are at a different level in inheritance hierarchy.
```
**Note:** Before Solidity 0.8.21 initialization of immutable variables was more restrictive. Such variables had to be
initialized exactly once at construction time and could not be read before then.

The contract creation code generated by the compiler will modify the contract’s runtime code before it is returned by
replacing all references to immutables with the values assigned to them. This is important if you are comparing the
runtime code generated by the compiler with the one actually stored in the blockchain. The compiler outputs where
these immutables are located in the deployed bytecode in theimmutableReferencesfield of the _compiler JSON
standard output_.

**3.9.5 Functions**

Functions can be defined inside and outside of contracts.

Functions outside of a contract, also called “free functions”, always have implicitinternal _visibility_. Their code is
included in all contracts that call them, similar to internal library functions.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1 <0.9.0;

functionsum(uint[] memoryarr) pure returns(uints) {
for(uinti = 0; i < arr.length; i++)
s += arr[i];
(continues on next page)

**3.9. Contracts 121**


```
(continued from previous page)
```
}

contract ArrayExample{
boolfound;
functionf(uint[] memory arr)public{
// This calls the free function internally.
// The compiler will add its code to the contract.
uints = sum(arr);
require(s >= 10);
found =true;
}
}

**Note:** Functions defined outside a contract are still always executed in the context of a contract. They still can call
other contracts, send them Ether and destroy the contract that called them, among other things. The main difference to
functions defined inside a contract is that free functions do not have direct access to the variablethis, storage variables
and functions not in their scope.

**Function Parameters and Return Variables**

Functions take typed parameters as input and may, unlike in many other languages, also return an arbitrary number of
values as output.

**Function Parameters**

Function parameters are declared the same way as variables, and the name of unused parameters can be omitted.

For example, if you want your contract to accept one kind of external call with two integers, you would use something
like the following:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Simple {
uintsum;
functiontaker(uint a,uintb) public {
sum = a + b;
}
}

Function parameters can be used as any other local variable and they can also be assigned to.

**122 Chapter 3. Contents**


**Return Variables**

Function return variables are declared with the same syntax after thereturnskeyword.

For example, suppose you want to return two results: the sum and the product of two integers passed as function
parameters, then you use something like:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Simple {
functionarithmetic(uinta,uint b)
public
pure
returns(uintsum,uintproduct)
{
sum = a + b;
product = a * b;
}
}

The names of return variables can be omitted. Return variables can be used as any other local variable and they are
initialized with their _default value_ and have that value until they are (re-)assigned.

You can either explicitly assign to return variables and then leave the function as above, or you can provide return values
(either a single or _multiple ones_ ) directly with thereturnstatement:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Simple {
functionarithmetic(uinta,uint b)
public
pure
returns(uintsum,uintproduct)
{
return(a + b, a * b);
}
}

If you use an earlyreturnto leave a function that has return variables, you must provide return values together with
the return statement.

**Note:** You cannot return some types from non-internal functions. This includes the types listed below and any
composite types that recursively contain them:

- mappings,
- internal function types,
- reference types with location set tostorage,
- multi-dimensional arrays (applies only to _ABI coder v1_ ),
- structs (applies only to _ABI coder v1_ ).

This restriction does not apply to library functions because of their different _internal ABI_.

**3.9. Contracts 123**


**Returning Multiple Values**

When a function has multiple return types, the statementreturn (v0, v1, ..., vn)can be used to return multiple
values. The number of components must be the same as the number of return variables and their types have to match,
potentially after an _implicit conversion_.

**State Mutability**

**View Functions**

Functions can be declaredviewin which case they promise not to modify the state.

**Note:** If the compiler’s EVM target is Byzantium or newer (default) the opcodeSTATICCALLis used whenview
functions are called, which enforces the state to stay unmodified as part of the EVM execution. For libraryview
functionsDELEGATECALLis used, because there is no combinedDELEGATECALLandSTATICCALL. This means library
viewfunctions do not have run-time checks that prevent state modifications. This should not impact security negatively
because library code is usually known at compile-time and the static checker performs compile-time checks.

The following statements are considered modifying the state:

1. Writing to state variables.
2. _Emitting events_.
3. _Creating other contracts_.
4. Usingselfdestruct.
5. Sending Ether via calls.
6. Calling any function not markedvieworpure.
7. Using low-level calls.
8. Using inline assembly that contains certain opcodes.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
functionf(uint a,uintb) public viewreturns(uint) {
returna * (b + 42) + block.timestamp;
}
}

**Note:** constanton functions used to be an alias toview, but this was dropped in version 0.5.0.

**Note:** Getter methods are automatically markedview.

**Note:** Prior to version 0.5.0, the compiler did not use theSTATICCALLopcode forviewfunctions. This enabled state
modifications inviewfunctions through the use of invalid explicit type conversions. By usingSTATICCALLforview

**124 Chapter 3. Contents**


functions, modifications to the state are prevented on the level of the EVM.

**Pure Functions**

Functions can be declaredpurein which case they promise not to read from or modify the state. In particular, it should
be possible to evaluate apurefunction at compile-time given only its inputs andmsg.data, but without any knowledge
of the current blockchain state. This means that reading fromimmutablevariables can be a non-pure operation.

**Note:** If the compiler’s EVM target is Byzantium or newer (default) the opcodeSTATICCALLis used, which does not
guarantee that the state is not read, but at least that it is not modified.

In addition to the list of state modifying statements explained above, the following are considered reading from the
state:

1. Reading from state variables.
2. Accessingaddress(this).balanceor<address>.balance.
3. Accessing any of the members ofblock,tx,msg(with the exception ofmsg.sigandmsg.data).
4. Calling any function not markedpure.
5. Using inline assembly that contains certain opcodes.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

contract C {
functionf(uint a,uintb) public purereturns(uint) {
returna * (b + 42);
}
}

Pure functions are able to use therevert()andrequire()functions to revert potential state changes when an _error
occurs_.

Reverting a state change is not considered a “state modification”, as only changes to the state made previously in code
that did not have thevieworpurerestriction are reverted and that code has the option to catch therevertand not
pass it on.

This behavior is also in line with theSTATICCALLopcode.

```
Warning: It is not possible to prevent functions from reading the state at the level of the EVM, it is only possible
to prevent them from writing to the state (i.e. onlyviewcan be enforced at the EVM level,purecan not).
```
**Note:** Prior to version 0.5.0, the compiler did not use theSTATICCALLopcode forpurefunctions. This enabled state
modifications inpurefunctions through the use of invalid explicit type conversions. By usingSTATICCALLforpure
functions, modifications to the state are prevented on the level of the EVM.

**Note:** Prior to version 0.4.17 the compiler did not enforce thatpureis not reading the state. It is a compile-time type
check, which can be circumvented doing invalid explicit conversions between contract types, because the compiler can

**3.9. Contracts 125**


verify that the type of the contract does not do state-changing operations, but it cannot check that the contract that will
be called at runtime is actually of that type.

**Special Functions**

**Receive Ether Function**

A contract can have at most onereceivefunction, declared usingreceive() external payable { ... }(with-
out thefunctionkeyword). This function cannot have arguments, cannot return anything and must haveexternal
visibility andpayablestate mutability. It can be virtual, can override and can have modifiers.

The receive function is executed on a call to the contract with empty calldata. This is the function that is executed on
plain Ether transfers (e.g. via.send()or.transfer()). If no such function exists, but a payable _fallback function_
exists, the fallback function will be called on a plain Ether transfer. If neither a receive Ether nor a payable fallback
function is present, the contract cannot receive Ether through a transaction that does not represent a payable function
call and throws an exception.

In the worst case, thereceivefunction can only rely on 2300 gas being available (for example whensendortransfer
is used), leaving little room to perform other operations except basic logging. The following operations will consume
more gas than the 2300 gas stipend:

- Writing to storage
- Creating a contract
- Calling an external function which consumes a large amount of gas
- Sending Ether

```
Warning: When Ether is sent directly to a contract (without a function call, i.e. sender usessendortransfer)
but the receiving contract does not define a receive Ether function or a payable fallback function, an exception will
be thrown, sending back the Ether (this was different before Solidity v0.4.0). If you want your contract to receive
Ether, you have to implement a receive Ether function (using payable fallback functions for receiving Ether is not
recommended, since the fallback is invoked and would not fail for interface confusions on the part of the sender).
```
```
Warning: A contract without a receive Ether function can receive Ether as a recipient of a coinbase transaction
(aka miner block reward ) or as a destination of aselfdestruct.
A contract cannot react to such Ether transfers and thus also cannot reject them. This is a design choice of the EVM
and Solidity cannot work around it.
It also means thataddress(this).balancecan be higher than the sum of some manual accounting implemented
in a contract (i.e. having a counter updated in the receive Ether function).
```
Below you can see an example of a Sink contract that uses functionreceive.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

// This contract keeps all Ether sent to it with no way
// to get it back.
contract Sink{
(continues on next page)

**126 Chapter 3. Contents**


(continued from previous page)
eventReceived(address,uint);
receive()external payable{
emit Received(msg.sender, msg.value);
}
}

**Fallback Function**

A contract can have at most onefallbackfunction, declared using eitherfallback () external [payable]or
fallback (bytes calldata input) external [payable] returns (bytes memory output)(both with-
out thefunctionkeyword). This function must haveexternalvisibility. A fallback function can be virtual, can
override and can have modifiers.

The fallback function is executed on a call to the contract if none of the other functions match the given function
signature, or if no data was supplied at all and there is no _receive Ether function_. The fallback function always receives
data, but in order to also receive Ether it must be markedpayable.

If the version with parameters is used,inputwill contain the full data sent to the contract (equal tomsg.data) and can
return data inoutput. The returned data will not be ABI-encoded. Instead it will be returned without modifications
(not even padding).

In the worst case, if a payable fallback function is also used in place of a receive function, it can only rely on 2300 gas
being available (see _receive Ether function_ for a brief description of the implications of this).

Like any function, the fallback function can execute complex operations as long as there is enough gas passed on to it.

```
Warning: Apayablefallback function is also executed for plain Ether transfers, if no receive Ether function
is present. It is recommended to always define a receive Ether function as well, if you define a payable fallback
function to distinguish Ether transfers from interface confusions.
```
**Note:** If you want to decode the input data, you can check the first four bytes for the function selector and
then you can useabi.decodetogether with the array slice syntax to decode ABI-encoded data:(c, d) = abi.
decode(input[4:], (uint256, uint256));Note that this should only be used as a last resort and proper func-
tions should be used instead.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

contract Test{
uintx;
// This function is called for all messages sent to
// this contract (there is no other function).
// Sending Ether to this contract will cause an exception,
// because the fallback function does not have the`payable`
// modifier.
fallback()external { x = 1; }
}

contract TestPayable{
(continues on next page)

**3.9. Contracts 127**


```
(continued from previous page)
uintx;
uinty;
// This function is called for all messages sent to
// this contract, except plain Ether transfers
// (there is no other function except the receive function).
// Any call with non-empty calldata to this contract will execute
// the fallback function (even if Ether is sent along with the call).
fallback()external payable{ x = 1; y =msg.value; }
```
// This function is called for plain Ether transfers, i.e.
// for every call with empty calldata.
receive()external payable{ x = 2; y =msg.value; }
}

contract Caller {
functioncallTest(Test test) public returns(bool) {
(boolsuccess,) =address(test).call(abi.encodeWithSignature(
˓→"nonExistingFunction()"));
require(success);
// results in test.x becoming == 1.

```
// address(test) will not allow to call``send``directly, since ``test``has no␣
˓→payable
// fallback function.
// It has to be converted to the``address payable``type to even allow calling␣
˓→``send``on it.
addresspayable testPayable =payable(address(test));
```
```
// If someone sends Ether to that contract,
// the transfer will fail, i.e. this returns false here.
returntestPayable.send(2 ether);
}
```
```
functioncallTestPayable(TestPayable test)public returns(bool) {
(boolsuccess,) =address(test).call(abi.encodeWithSignature(
˓→"nonExistingFunction()"));
require(success);
// results in test.x becoming == 1 and test.y becoming 0.
(success,) =address(test).call{value: 1}(abi.encodeWithSignature(
˓→"nonExistingFunction()"));
require(success);
// results in test.x becoming == 1 and test.y becoming 1.
```
```
// If someone sends Ether to that contract, the receive function in TestPayable␣
˓→will be called.
// Since that function writes to storage, it takes more gas than is available␣
˓→with a
// simple``send``or``transfer``. Because of that, we have to use a low-level␣
˓→call.
(success,) =address(test).call{value: 2 ether}("");
require(success);
// results in test.x becoming == 2 and test.y becoming 2 ether.
(continues on next page)
```
**128 Chapter 3. Contents**


```
(continued from previous page)
```
return true;
}
}

**Function Overloading**

A contract can have multiple functions of the same name but with different parameter types. This process is called
“overloading” and also applies to inherited functions. The following example shows overloading of the functionfin
the scope of contractA.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract A {
functionf(uint value)public purereturns(uintout) {
out = value;
}

functionf(uint value,boolreally)public purereturns(uintout) {
if (really)
out = value;
}
}

Overloaded functions are also present in the external interface. It is an error if two externally visible functions differ
by their Solidity types but not by their external types.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

// This will not compile
contract A {
functionf(B value) publicpurereturns(B out) {
out = value;
}

functionf(addressvalue) public purereturns(addressout) {
out = value;
}
}

contract B {
}

Bothffunction overloads above end up accepting the address type for the ABI although they are considered different
inside Solidity.

**3.9. Contracts 129**


**Overload resolution and Argument matching**

Overloaded functions are selected by matching the function declarations in the current scope to the arguments supplied
in the function call. Functions are selected as overload candidates if all arguments can be implicitly converted to the
expected types. If there is not exactly one candidate, resolution fails.

**Note:** Return parameters are not taken into account for overload resolution.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract A {
functionf(uint8 val)public purereturns(uint8out) {
out = val;
}

functionf(uint256val)public purereturns(uint256out) {
out = val;
}
}

Callingf(50)would create a type error since 50 can be implicitly converted both touint8anduint256types. On
another handf(256)would resolve tof(uint256)overload as 256 cannot be implicitly converted touint8.

**3.9.6 Events**

Solidity events give an abstraction on top of the EVM’s logging functionality. Applications can subscribe and listen to
these events through the RPC interface of an Ethereum client.

Events can be defined at file level or as inheritable members of contracts (including interfaces and libraries). When
you call them, they cause the arguments to be stored in the transaction’s log - a special data structure in the blockchain.
These logs are associated with the address of the contract that emitted them, are incorporated into the blockchain, and
stay there as long as a block is accessible (forever as of now, but this might change in the future). The Log and its event
data is not accessible from within contracts (not even from the contract that created them).

It is possible to request a Merkle proof for logs, so if an external entity supplies a contract with such a proof, it can
check that the log actually exists inside the blockchain. You have to supply block headers because the contract can only
see the last 256 block hashes.

You can add the attributeindexedto up to three parameters which adds them to a special data structure known as
_“topics”_ instead of the data part of the log. A topic can only hold a single word (32 bytes) so if you use a _reference
type_ for an indexed argument, the Keccak-256 hash of the value is stored as a topic instead.

All parameters without theindexedattribute are _ABI-encoded_ into the data part of the log.

Topics allow you to search for events, for example when filtering a sequence of blocks for certain events. You can also
filter events by the address of the contract that emitted the event.

For example, the code below uses the web3.jssubscribe("logs")method to filter logs that match a topic with a
certain address value:

varoptions = {
fromBlock: 0,
address: web3.eth.defaultAccount,
(continues on next page)

**130 Chapter 3. Contents**


(continued from previous page)
topics: ["0x0000000000000000000000000000000000000000000000000000000000000000",null,␣
˓→null]
};
web3.eth.subscribe('logs', options,function(error, result) {
if (!error)
console.log(result);
})
.on("data",function(log) {
console.log(log);
})
.on("changed",function(log) {
});

The hash of the signature of the event is one of the topics, except if you declared the event with theanonymousspecifier.
This means that it is not possible to filter for specific anonymous events by name, you can only filter by the contract
address. The advantage of anonymous events is that they are cheaper to deploy and call. It also allows you to declare
four indexed arguments rather than three.

**Note:** Since the transaction log only stores the event data and not the type, you have to know the type of the event,
including which parameter is indexed and if the event is anonymous in order to correctly interpret the data. In particular,
it is possible to “fake” the signature of another event using an anonymous event.

**Members of Events**

- event.selector: For non-anonymous events, this is abytes32value containing thekeccak256hash of the
    event signature, as used in the default topic.

**Example**

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.21 <0.9.0;

contract ClientReceipt{
eventDeposit(
addressindexed from,
bytes32indexed id,
uintvalue
);

functiondeposit(bytes32id)public payable{
// Events are emitted using`emit`, followed by
// the name of the event and the arguments
// (if any) in parentheses. Any such invocation
// (even deeply nested) can be detected from
// the JavaScript API by filtering for`Deposit`.
emit Deposit(msg.sender, id, msg.value);
}
}

The use in the JavaScript API is as follows:

**3.9. Contracts 131**


varabi =/* abi as generated by the compiler */;
varClientReceipt = web3.eth.contract(abi);
varclientReceipt = ClientReceipt.at("0x1234...ab67"/* address */);

vardepositEvent = clientReceipt.Deposit();

// watch for changes
depositEvent.watch(function(error, result){
// result contains non-indexed arguments and topics
// given to the `Deposit`call.
if (!error)
console.log(result);
});

// Or pass a callback to start watching immediately
vardepositEvent = clientReceipt.Deposit(function(error, result) {
if (!error)
console.log(result);
});

The output of the above looks like the following (trimmed):

{
"returnValues": {
"from": "0x1111...FFFFCCCC",
"id": "0x50...sd5adb20",
"value": "0x420042"
},
"raw": {
"data": "0x7f...91385",
"topics": ["0xfd4...b4ead7", "0x7f...1a91385"]
}
}

**Additional Resources for Understanding Events**

- JavaScript documentation
- Example usage of events
- How to access them in js

**132 Chapter 3. Contents**


**3.9.7 Custom Errors**

Errors in Solidity provide a convenient and gas-efficient way to explain to the user why an operation failed. They can
be defined inside and outside of contracts (including interfaces and libraries).

They have to be used together with the _revert statement_ or the _require function_. In the case ofrevertstatements, or
requirecalls where the condition is evaluated to be false, all changes in the current call are reverted, and the error
data passed back to the caller.

The example below shows custom error usage with therevertstatement in functiontransferWithRevertError,
as well as the newer approach withrequirein functiontransferWithRequireError.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.27;

/// Insufficient balance for transfer. Needed `required`but only
///`available` available.
/// @param available balance available.
/// @param required requested amount to transfer.
error InsufficientBalance(uint256available,uint256required);

contract TestToken{
mapping(address=>uint) balance;
functiontransferWithRevertError(addressto,uint256amount)public {
if (amount > balance[msg.sender])
revert InsufficientBalance({
available: balance[msg.sender],
required: amount
});
balance[msg.sender] -= amount;
balance[to] += amount;
}
functiontransferWithRequireError(addressto,uint256amount)public {
require(amount <= balance[msg.sender], InsufficientBalance(balance[msg.sender],␣
˓→amount));
balance[msg.sender] -= amount;
balance[to] += amount;
}
// ...
}

Another important detail to mention when it comes to usingrequirewith custom errors, is that memory allocation
for the error-based revert reason will only happen in the reverting case, which, along with optimization of constants
and string literals makes this about as gas-efficient as theif (!condition) revert CustomError(args)pattern.

Errors cannot be overloaded or overridden but are inherited. The same error can be defined in multiple places as long
as the scopes are distinct. Instances of errors can only be created usingrevertstatements, or as the second argument
torequirefunctions.

The error creates data that is then passed to the caller with the revert operation to either return to the off-chain component
or catch it in a _try/catch statement_. Note that an error can only be caught when coming from an external call, reverts
happening in internal calls or inside the same function cannot be caught.

If you do not provide any parameters, the error only needs four bytes of data and you can use _NatSpec_ as above to
further explain the reasons behind the error, which is not stored on chain. This makes this a very cheap and convenient
error-reporting feature at the same time.

**3.9. Contracts 133**


More specifically, an error instance is ABI-encoded in the same way as a function call to a function of the same name
and types would be and then used as the return data in therevertopcode. This means that the data consists of a
4-byte selector followed by _ABI-encoded_ data. The selector consists of the first four bytes of the keccak256-hash of the
signature of the error type.

**Note:** It is possible for a contract to revert with different errors of the same name or even with errors defined in different
places that are indistinguishable by the caller. For the outside, i.e. the ABI, only the name of the error is relevant, not
the contract or file where it is defined.

The statement require(condition, "description");would be equivalent to if (!condition) revert
Error("description")if you could defineerror Error(string). Note, however, thatErroris a built-in type
and cannot be defined in user-supplied code.

Similarly, a failingassertor similar conditions will revert with an error of the built-in typePanic(uint256).

**Note:** Error data should only be used to give an indication of failure, but not as a means for control-flow. The reason
is that the revert data of inner calls is propagated back through the chain of external calls by default. This means that
an inner call can “forge” revert data that looks like it could have come from the contract that called it.

**Members of Errors**

- error.selector: Abytes4value containing the error selector.

**3.9.8 Inheritance**

Solidity supports multiple inheritance including polymorphism.

Polymorphism means that a function call (internal and external) always executes the function of the same name (and
parameter types) in the most derived contract in the inheritance hierarchy. This has to be explicitly enabled on each
function in the hierarchy using thevirtualandoverridekeywords. See _Function Overriding_ for more details.

It is possible to call functions further up in the inheritance hierarchy internally by explicitly specifying the contract
usingContractName.functionName()or usingsuper.functionName()if you want to call the function one level
higher up in the flattened inheritance hierarchy (see below).

When a contract inherits from other contracts, only a single contract is created on the blockchain, and the code from all
the base contracts is compiled into the created contract. This means that all internal calls to functions of base contracts
also just use internal function calls (super.f(..)will use JUMP and not a message call).

State variable shadowing is considered as an error. A derived contract can only declare a state variablex, if there is no
visible state variable with the same name in any of its bases.

The general inheritance system is very similar to Python’s, especially concerning multiple inheritance, but there are
also some _differences_.

Details are given in the following example.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned{
addresspayable owner;
constructor() { owner =payable(msg.sender); }
(continues on next page)

**134 Chapter 3. Contents**


```
(continued from previous page)
```
}

// Use `is` to derive from another contract. Derived
// contracts can access all non-private members including
// internal functions and state variables. These cannot be
// accessed externally via`this`, though.
contract Emittable isOwned {
eventEmitted();

// The keyword`virtual` means that the function can change
// its behavior in derived classes ("overriding").
functionemitEvent() virtual public{
if (msg.sender == owner)
emit Emitted();
}
}

// These abstract contracts are only provided to make the
// interface known to the compiler. Note the function
// without body. If a contract does not implement all
// functions it can only be used as an interface.
abstractcontract Config {
functionlookup(uintid)publicvirtualreturns(addressadr);
}

abstractcontract NameReg{
functionregister(bytes32name)public virtual;
functionunregister()public virtual;
}

// Multiple inheritance is possible. Note that`Owned` is
// also a base class of `Emittable`, yet there is only a single
// instance of`Owned`(as for virtual inheritance in C++).
contract Named isOwned, Emittable {
constructor(bytes32name) {
Config config = Config(0xD5f9D8D94886E70b06E474c3fB14Fd43E2f23970);
NameReg(config.lookup(1)).register(name);
}

```
// Functions can be overridden by another function with the same name and
// the same number/types of inputs. If the overriding function has different
// types of output parameters, that causes an error.
// Both local and message-based function calls take these overrides
// into account.
// If you want the function to override, you need to use the
// `override`keyword. You need to specify the `virtual`keyword again
// if you want this function to be overridden again.
functionemitEvent()publicvirtual override {
if (msg.sender == owner) {
Config config = Config(0xD5f9D8D94886E70b06E474c3fB14Fd43E2f23970);
NameReg(config.lookup(1)).unregister();
// It is still possible to call a specific
(continues on next page)
```
**3.9. Contracts 135**


(continued from previous page)
// overridden function.
Emittable.emitEvent();
}
}
}

// If a constructor takes an argument, it needs to be
// provided in the header or modifier-invocation-style at
// the constructor of the derived contract (see below).
contract PriceFeed isOwned, Emittable, Named("GoldFeed") {
uintinfo;

```
functionupdateInfo(uintnewInfo)public{
if (msg.sender == owner) info = newInfo;
}
```
// Here, we only specify`override`and not`virtual`.
// This means that contracts deriving from`PriceFeed`
// cannot change the behavior of `emitEvent`anymore.
functionemitEvent()publicoverride(Emittable, Named) { Named.emitEvent(); }
functionget()public viewreturns(uintr) {return info; }
}

Note that above, we callEmittable.emitEvent()to “forward” the emit event request. The way this is done is
problematic, as seen in the following example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned{
addresspayable owner;
constructor() { owner =payable(msg.sender); }
}

contract Emittable isOwned {
eventEmitted();

functionemitEvent() virtual public{
if (msg.sender == owner) {
emit Emitted();
}
}
}

contract Base1 isEmittable {
eventBase1Emitted();
functionemitEvent()publicvirtual override {
/* Here, we emit an event to simulate some Base1 logic */
emit Base1Emitted();
Emittable.emitEvent();
}
(continues on next page)

**136 Chapter 3. Contents**


```
(continued from previous page)
```
}

contract Base2 isEmittable {
eventBase2Emitted();
functionemitEvent()publicvirtual override {
/* Here, we emit an event to simulate some Base2 logic */
emit Base2Emitted();
Emittable.emitEvent();
}
}

contract Final isBase1, Base2 {
eventFinalEmitted();
functionemitEvent()publicoverride(Base1, Base2) {
/* Here, we emit an event to simulate some Final logic */
emit FinalEmitted();
Base2.emitEvent();
}
}

A call toFinal.emitEvent()will callBase2.emitEventbecause we specify it explicitly in the final override,
but this function will bypassBase1.emitEvent, resulting in the following sequence of events: FinalEmitted
-> Base2Emitted -> Emitted, instead of the expected sequence: FinalEmitted -> Base2Emitted ->
Base1Emitted -> Emitted. The way around this is to usesuper:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Owned{
addresspayable owner;
constructor() { owner =payable(msg.sender); }
}

contract Emittable isOwned {
eventEmitted();

functionemitEvent() virtual public{
if (msg.sender == owner) {
emit Emitted();
}
}
}

contract Base1 isEmittable {
eventBase1Emitted();
functionemitEvent()publicvirtual override {
/* Here, we emit an event to simulate some Base1 logic */
emit Base1Emitted();
super.emitEvent();
}
}

```
(continues on next page)
```
**3.9. Contracts 137**


```
(continued from previous page)
```
contract Base2 isEmittable {
eventBase2Emitted();
functionemitEvent()publicvirtual override {
/* Here, we emit an event to simulate some Base2 logic */
emit Base2Emitted();
super.emitEvent();
}
}

contract Final isBase1, Base2 {
eventFinalEmitted();
functionemitEvent()publicoverride(Base1, Base2) {
/* Here, we emit an event to simulate some Final logic */
emit FinalEmitted();
super.emitEvent();
}
}

IfFinalcalls a function ofsuper, it does not simply call this function on one of its base contracts. Rather, it calls
this function on the next base contract in the final inheritance graph, so it will callBase1.emitEvent()(note that the
final inheritance sequence is – starting with the most derived contract: Final, Base2, Base1, Emittable, Owned). The
actual function that is called when using super is not known in the context of the class where it is used, although its
type is known. This is similar for ordinary virtual method lookup.

**Function Overriding**

Base functions can be overridden by inheriting contracts to change their behavior if they are marked asvirtual. The
overriding function must then use theoverridekeyword in the function header. The overriding function may only
change the visibility of the overridden function fromexternaltopublic. The mutability may be changed to a more
strict one following the order:nonpayablecan be overridden byviewandpure.viewcan be overridden bypure.
payableis an exception and cannot be changed to any other mutability.

The following example demonstrates changing mutability and visibility:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Base
{
functionfoo() virtualexternalview {}
}

contract Middle isBase {}

contract Inherited isMiddle
{
functionfoo() overridepublic pure {}
}

For multiple inheritance, the most derived base contracts that define the same function must be specified explicitly
after theoverridekeyword. In other words, you have to specify all base contracts that define the same function and

**138 Chapter 3. Contents**


have not yet been overridden by another base contract (on some path through the inheritance graph). Additionally, if a
contract inherits the same function from multiple (unrelated) bases, it has to explicitly override it:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Base1
{
functionfoo() virtualpublic {}
}

contract Base2
{
functionfoo() virtualpublic {}
}

contract Inherited isBase1, Base2
{
// Derives from multiple bases defining foo(), so we must explicitly
// override it
functionfoo()public override(Base1, Base2) {}
}

An explicit override specifier is not required if the function is defined in a common base contract or if there is a unique
function in a common base contract that already overrides all other functions.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract A {functionf()public pure{} }
contract B isA {}
contract C isA {}
// No explicit override required
contract D isB, C {}

More formally, it is not required to override a function (directly or indirectly) inherited from multiple bases if there is a
base contract that is part of all override paths for the signature, and (1) that base implements the function and no paths
from the current contract to the base mentions a function with that signature or (2) that base does not implement the
function and there is at most one mention of the function in all paths from the current contract to that base.

In this sense, an override path for a signature is a path through the inheritance graph that starts at the contract under
consideration and ends at a contract mentioning a function with that signature that does not override.

If you do not mark a function that overrides asvirtual, derived contracts can no longer change the behavior of that
function.

**Note:** Functions with theprivatevisibility cannot bevirtual.

**Note:** Functions without implementation have to be markedvirtualoutside of interfaces. In interfaces, all functions
are automatically consideredvirtual.

**Note:** Starting from Solidity 0.8.8, theoverridekeyword is not required when overriding an interface function,

**3.9. Contracts 139**


except for the case where the function is defined in multiple bases.

Public state variables can override external functions if the parameter and return types of the function matches the
getter function of the variable:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract A
{
functionf()externalview virtualreturns(uint) {return5; }
}

contract B isA
{
uint publicoverride f;
}

**Note:** While public state variables can override external functions, they themselves cannot be overridden.

**Modifier Overriding**

Function modifiers can override each other. This works in the same way as _function overriding_ (except that there is no
overloading for modifiers). Thevirtualkeyword must be used on the overridden modifier and theoverridekeyword
must be used in the overriding modifier:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Base
{
modifierfoo() virtual {_;}
}

contract Inherited isBase
{
modifierfoo() override {_;}
}

In case of multiple inheritance, all direct base contracts must be specified explicitly:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Base1
{
modifierfoo() virtual {_;}
}

contract Base2
{
(continues on next page)

**140 Chapter 3. Contents**


(continued from previous page)
modifierfoo() virtual {_;}
}

contract Inherited isBase1, Base2
{
modifierfoo() override(Base1, Base2) {_;}
}

**Constructors**

A constructor is an optional function declared with theconstructorkeyword which is executed upon contract cre-
ation, and where you can run contract initialization code.

Before the constructor code is executed, state variables are initialised to their specified value if you initialise them
inline, or their _default value_ if you do not.

After the constructor has run, the final code of the contract is deployed to the blockchain. The deployment of the
code costs additional gas linear to the length of the code. This code includes all functions that are part of the public
interface and all functions that are reachable from there through function calls. It does not include the constructor code
or internal functions that are only called from the constructor.

If there is no constructor, the contract will assume the default constructor, which is equivalent toconstructor() {}.
For example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

abstractcontract A {
uint publica;

constructor(uinta_) {
a = a_;
}
}

contract B isA(1) {
constructor() {}
}

You can use internal parameters in a constructor (for example storage pointers). In this case, the contract has to be
marked _abstract_ , because these parameters cannot be assigned valid values from outside but only through the construc-
tors of derived contracts.

```
Warning: Prior to version 0.4.22, constructors were defined as functions with the same name as the contract. This
syntax was deprecated and is not allowed anymore in version 0.5.0.
```
```
Warning: Prior to version 0.7.0, you had to specify the visibility of constructors as eitherinternalorpublic.
```
**3.9. Contracts 141**


**Arguments for Base Constructors**

The constructors of all the base contracts will be called following the linearization rules explained below. If the base
constructors have arguments, derived contracts need to specify all of them. This can be done in two ways:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Base{
uintx;
constructor(uintx_) { x = x_; }
}

// Either directly specify in the inheritance list...
contract Derived1 isBase(7) {
constructor() {}
}

// or through a "modifier" of the derived constructor...
contract Derived2 isBase {
constructor(uinty) Base(y * y) {}
}

// or declare abstract...
abstractcontract Derived3 isBase {
}

// and have the next concrete derived contract initialize it.
contract DerivedFromDerived isDerived3 {
constructor() Base(10 + 10) {}
}

One way is directly in the inheritance list (is Base(7)). The other is in the way a modifier is invoked as part of the
derived constructor (Base(y * y)). The first way to do it is more convenient if the constructor argument is a constant
and defines the behavior of the contract or describes it. The second way has to be used if the constructor arguments
of the base depend on those of the derived contract. Arguments have to be given either in the inheritance list or in
modifier-style in the derived constructor. Specifying arguments in both places is an error.

If a derived contract does not specify the arguments to all of its base contracts’ constructors, it must be declared abstract.
In that case, when another contract derives from it, that other contract’s inheritance list or constructor must provide
the necessary parameters for all base classes that haven’t had their parameters specified (otherwise, that other contract
must be declared abstract as well). For example, in the above code snippet, seeDerived3andDerivedFromDerived.

**Multiple Inheritance and Linearization**

Languages that allow multiple inheritance have to deal with several problems. One is the Diamond Problem. Solidity
is similar to Python in that it uses “C3 Linearization” to force a specific order in the directed acyclic graph (DAG) of
base classes. This results in the desirable property of monotonicity but disallows some inheritance graphs. Especially,
the order in which the base classes are given in theisdirective is important: You have to list the direct base contracts
in the order from “most base-like” to “most derived”. Note that this order is the reverse of the one used in Python.

Another simplifying way to explain this is that when a function is called that is defined multiple times in different
contracts, the given bases are searched from right to left (left to right in Python) in a depth-first manner, stopping at the
first match. If a base contract has already been searched, it is skipped.

**142 Chapter 3. Contents**


In the following code, Solidity will give the error “Linearization of inheritance graph impossible”.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract X {}
contract A isX {}
// This will not compile
contract C isA, X {}

The reason for this is thatCrequestsXto overrideA(by specifyingA, Xin this order), butAitself requests to override
X, which is a contradiction that cannot be resolved.

Due to the fact that you have to explicitly override a function that is inherited from multiple bases without a unique
override, C3 linearization is not too important in practice.

One area where inheritance linearization is especially important and perhaps not as clear is when there are multiple
constructors in the inheritance hierarchy. The constructors will always be executed in the linearized order, regardless
of the order in which their arguments are provided in the inheriting contract’s constructor. For example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Base1{
constructor() {}
}

contract Base2{
constructor() {}
}

// Constructors are executed in the following order:
// 1 - Base1
// 2 - Base2
// 3 - Derived1
contract Derived1 isBase1, Base2 {
constructor() Base1() Base2() {}
}

// Constructors are executed in the following order:
// 1 - Base2
// 2 - Base1
// 3 - Derived2
contract Derived2 isBase2, Base1 {
constructor() Base2() Base1() {}
}

// Constructors are still executed in the following order:
// 1 - Base2
// 2 - Base1
// 3 - Derived3
contract Derived3 isBase2, Base1 {
constructor() Base1() Base2() {}
}

**3.9. Contracts 143**


**Inheriting Different Kinds of Members of the Same Name**

The only situations where, due to inheritance, a contract may contain multiple definitions sharing the same name are:

- Overloading of functions.
- Overriding of virtual functions.
- Overriding of external virtual functions by state variable getters.
- Overriding of virtual modifiers.
- Overloading of events.

**3.9.9 Abstract Contracts**

Contracts must be marked as abstract when at least one of their functions is not implemented or when they do not provide
arguments for all of their base contract constructors. Even if this is not the case, a contract may still be marked abstract,
such as when you do not intend for the contract to be created directly. Abstract contracts are similar to _Interfaces_ but
an interface is more limited in what it can declare.

An abstract contract is declared using theabstractkeyword as shown in the following example. Note that this contract
needs to be defined as abstract, because the functionutterance()is declared, but no implementation was provided
(no implementation body{ }was given).

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstractcontract Feline {
functionutterance()publicvirtualreturns(bytes32);
}

Such abstract contracts can not be instantiated directly. This is also true, if an abstract contract itself does implement
all defined functions. The usage of an abstract contract as a base class is shown in the following example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstractcontract Feline {
functionutterance()publicpure virtualreturns(bytes32);
}

contract Cat is Feline {
functionutterance()publicpure override returns(bytes32) {return "miaow"; }
}

If a contract inherits from an abstract contract and does not implement all non-implemented functions by overriding,
it needs to be marked as abstract as well.

Note that a function without implementation is different from a _Function Type_ even though their syntax looks very
similar.

Example of function without implementation (a function declaration):

functionfoo(address)external returns(address);

Example of a declaration of a variable whose type is a function type:

**144 Chapter 3. Contents**


function(address)external returns(address) foo;

Abstract contracts decouple the definition of a contract from its implementation providing better extensibility and self-
documentation and facilitating patterns like the Template method and removing code duplication. Abstract contracts
are useful in the same way that defining methods in an interface is useful. It is a way for the designer of the abstract
contract to say “any child of mine must implement this method”.

**Note:** Abstract contracts cannot override an implemented virtual function with an unimplemented one.

**3.9.10 Interfaces**

Interfaces are similar to abstract contracts, but they cannot have any functions implemented. There are further restric-
tions:

- They cannot inherit from other contracts, but they can inherit from other interfaces.
- All declared functions must be external in the interface, even if they are public in the contract.
- They cannot declare a constructor.
- They cannot declare state variables.
- They cannot declare modifiers.

Some of these restrictions might be lifted in the future.

Interfaces are basically limited to what the Contract ABI can represent, and the conversion between the ABI and an
interface should be possible without any information loss.

Interfaces are denoted by their own keyword:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

interface Token {
enumTokenType { Fungible, NonFungible }
struct Coin {string obverse;stringreverse; }
functiontransfer(addressrecipient,uint amount)external;
}

Contracts can inherit interfaces as they would inherit other contracts.

All functions declared in interfaces are implicitlyvirtualand any functions that override them do not need the
overridekeyword. This does not automatically mean that an overriding function can be overridden again - this
is only possible if the overriding function is markedvirtual.

Interfaces can inherit from other interfaces. This has the same rules as normal inheritance.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

interface ParentA {
functiontest() external returns(uint256);
}

interface ParentB {
(continues on next page)

**3.9. Contracts 145**


(continued from previous page)
functiontest() external returns(uint256);
}

interface SubInterfaceis ParentA, ParentB {
// Must redefine test in order to assert that the parent
// meanings are compatible.
functiontest() externaloverride(ParentA, ParentB)returns(uint256);
}

Types defined inside interfaces and other contract-like structures can be accessed from other contracts: Token.
TokenTypeorToken.Coin.

```
Warning: Interfaces have supportedenumtypes since Solidity version 0.5.0 , make sure the pragma version spec-
ifies this version as a minimum.
```
**3.9.11 Libraries**

Libraries are similar to contracts, but their purpose is that they are deployed only once at a specific address and their
code is reused using theDELEGATECALL(CALLCODEuntil Homestead) feature of the EVM. This means that if library
functions are called, their code is executed in the context of the calling contract, i.e.thispoints to the calling contract,
and especially the storage from the calling contract can be accessed. As a library is an isolated piece of source code,
it can only access state variables of the calling contract if they are explicitly supplied (it would have no way to name
them, otherwise). Library functions can only be called directly (i.e. without the use ofDELEGATECALL) if they do not
modify the state (i.e. if they arevieworpurefunctions), because libraries are assumed to be stateless. In particular,
it is not possible to destroy a library.

**Note:** Until version 0.4.20, it was possible to destroy libraries by circumventing Solidity’s type system. Starting from
that version, libraries contain a _mechanism_ that disallows state-modifying functions to be called directly (i.e. without
DELEGATECALL).

Libraries can be seen as implicit base contracts of the contracts that use them. They will not be explicitly visible in
the inheritance hierarchy, but calls to library functions look just like calls to functions of explicit base contracts (using
qualified access likeL.f()). Of course, calls to internal functions use the internal calling convention, which means that
all internal types can be passed and types _stored in memory_ will be passed by reference and not copied. To realize this in
the EVM, the code of internal library functions that are called from a contract and all functions called from therein will
at compile time be included in the calling contract, and a regularJUMPcall will be used instead of aDELEGATECALL.

**Note:** The inheritance analogy breaks down when it comes to public functions. Calling a public library function with
L.f()results in an external call (DELEGATECALLto be precise). In contrast,A.f()is an internal call whenAis a base
contract of the current contract.

The following example illustrates how to use libraries (but using a manual method, be sure to check out _using for_ for a
more advanced example to implement a set).

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

```
(continues on next page)
```
**146 Chapter 3. Contents**


```
(continued from previous page)
```
// We define a new struct datatype that will be used to
// hold its data in the calling contract.
struct Data {
mapping(uint=> bool) flags;
}

librarySet {
// Note that the first parameter is of type "storage
// reference" and thus only its storage address and not
// its contents is passed as part of the call. This is a
// special feature of library functions. It is idiomatic
// to call the first parameter`self`, if the function can
// be seen as a method of that object.
functioninsert(Data storage self,uintvalue)
public
returns(bool)
{
if (self.flags[value])
return false;// already there
self.flags[value] =true;
return true;
}

```
functionremove(Data storage self,uintvalue)
public
returns(bool)
{
if (!self.flags[value])
return false;// not there
self.flags[value] =false;
return true;
}
```
functioncontains(Data storage self,uint value)
public
view
returns(bool)
{
returnself.flags[value];
}
}

contract C {
Data knownValues;

```
functionregister(uintvalue) public{
// The library functions can be called without a
// specific instance of the library, since the
// "instance" will be the current contract.
require(Set.insert(knownValues, value));
}
(continues on next page)
```
**3.9. Contracts 147**


(continued from previous page)
// In this contract, we can also directly access knownValues.flags, if we want.
}

Of course, you do not have to follow this way to use libraries: they can also be used without defining struct data types.
Functions also work without any storage reference parameters, and they can have multiple storage reference parameters
and in any position.

The calls toSet.contains,Set.insertandSet.removeare all compiled as calls (DELEGATECALL) to an external
contract/library. If you use libraries, be aware that an actual external function call is performed.msg.sender,msg.
valueandthiswill retain their values in this call, though (prior to Homestead, because of the use ofCALLCODE,
msg.senderandmsg.valuechanged, though).

The following example shows how to use _types stored in memory_ and internal functions in libraries in order to implement
custom types without the overhead of external function calls:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;

struct bigint {
uint[] limbs;
}

libraryBigInt {
functionfromUint(uintx) internalpurereturns(bigintmemoryr) {
r.limbs =new uint[](1);
r.limbs[0] = x;
}

```
functionadd(bigint memorya, bigintmemory b) internalpurereturns(bigintmemory␣
˓→r) {
r.limbs =new uint[](max(a.limbs.length, b.limbs.length));
uintcarry = 0;
for(uinti = 0; i < r.limbs.length; ++i) {
uintlimbA = limb(a, i);
uintlimbB = limb(b, i);
unchecked {
r.limbs[i] = limbA + limbB + carry;
```
```
if (limbA + limbB < limbA || (limbA + limbB == type(uint).max && carry >␣
˓→0))
carry = 1;
else
carry = 0;
}
}
if (carry > 0) {
// too bad, we have to add a limb
uint[]memory newLimbs = new uint[](r.limbs.length + 1);
uinti;
for(i = 0; i < r.limbs.length; ++i)
newLimbs[i] = r.limbs[i];
newLimbs[i] = carry;
r.limbs = newLimbs;
(continues on next page)
```
**148 Chapter 3. Contents**


```
(continued from previous page)
}
}
```
```
functionlimb(bigintmemorya, uintindex) internalpurereturns(uint) {
returnindex < a.limbs.length? a.limbs[index] : 0;
}
```
functionmax(uinta, uintb) privatepure returns(uint) {
returna > b? a : b;
}
}

contract C {
using BigIntforbigint;

functionf()public pure {
bigintmemory x = BigInt.fromUint(7);
bigintmemory y = BigInt.fromUint(type(uint).max);
bigintmemory z = x.add(y);
assert(z.limb(1) > 0);
}
}

It is possible to obtain the address of a library by converting the library type to theaddresstype, i.e. using
address(LibraryName).

As the compiler does not know the address where the library will be deployed, the compiled hex code will contain
placeholders of the form__$30bbc0abd4d6364515865950d3e0d10953$__(format was different <v0.5.0). The
placeholder is a 34 character prefix of the hex encoding of the keccak256 hash of the fully qualified library name,
which would be for examplelibraries/bigint.sol:BigIntif the library was stored in a file calledbigint.sol
in alibraries/directory. Such bytecode is incomplete and should not be deployed. Placeholders need to be replaced
with actual addresses. You can do that by either passing them to the compiler when the library is being compiled or
by using the linker to update an already compiled binary. See _Library Linking_ for information on how to use the
commandline compiler for linking.

In comparison to contracts, libraries are restricted in the following ways:

- they cannot have state variables
- they cannot inherit nor be inherited
- they cannot receive Ether
- they cannot be destroyed

(These might be lifted at a later point.)

**3.9. Contracts 149**


**Function Signatures and Selectors in Libraries**

While external calls to public or external library functions are possible, the calling convention for such calls is con-
sidered to be internal to Solidity and not the same as specified for the regular _contract ABI_. External library functions
support more argument types than external contract functions, for example recursive structs and storage pointers. For
that reason, the function signatures used to compute the 4-byte selector are computed following an internal naming
schema and arguments of types not supported in the contract ABI use an internal encoding.

The following identifiers are used for the types in the signatures:

- Value types, non-storagestringand non-storagebytesuse the same identifiers as in the contract ABI.
- Non-storage array types follow the same convention as in the contract ABI, i.e.<type>[]for dynamic arrays
    and<type>[M]for fixed-size arrays ofMelements.
- Non-storage structs are referred to by their fully qualified name, i.e.C.Sforcontract C { struct S { ...
    } }.
- Storage pointer mappings usemapping(<keyType> => <valueType>) storagewhere<keyType>and
    <valueType>are the identifiers for the key and value types of the mapping, respectively.
- Other storage pointer types use the type identifier of their corresponding non-storage type, but append a single
    space followed bystorageto it.

The argument encoding is the same as for the regular contract ABI, except for storage pointers, which are encoded as
auint256value referring to the storage slot to which they point.

Similarly to the contract ABI, the selector consists of the first four bytes of the Keccak256-hash of the signature. Its
value can be obtained from Solidity using the.selectormember as follows:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.14 <0.9.0;

libraryL {
functionf(uint256) external{}
}

contract C {
functiong()public purereturns(bytes4) {
returnL.f.selector;
}
}

**Call Protection For Libraries**

As mentioned in the introduction, if a library’s code is executed using aCALLinstead of aDELEGATECALLorCALLCODE,
it will revert unless avieworpurefunction is called.

The EVM does not provide a direct way for a contract to detect whether it was called usingCALLor not, but a contract
can use theADDRESSopcode to find out “where” it is currently running. The generated code compares this address to
the address used at construction time to determine the mode of calling.

More specifically, the runtime code of a library always starts with a push instruction, which is a zero of 20 bytes at
compilation time. When the deploy code runs, this constant is replaced in memory by the current address and this
modified code is stored in the contract. At runtime, this causes the deploy time address to be the first constant to be
pushed onto the stack and the dispatcher code compares the current address against this constant for any non-view and
non-pure function.

**150 Chapter 3. Contents**


This means that the actual code stored on chain for a library is different from the code reported by the compiler as
deployedBytecode.

**3.9.12 Using For**

The directiveusing A for Bcan be used to attach functions (A) as operators to user-defined value types or as member
functions to any type (B). The member functions receive the object they are called on as their first parameter (like the
selfvariable in Python). The operator functions receive operands as parameters.

It is valid either at file level or inside a contract, at contract level.

The first part,A, can be one of:

- A list of functions, optionally with an operator name assigned (e.g. using {f, g as +, h, L.t} for
    uint). If no operator is specified, the function can be either a library function or a free function and is at-
    tached to the type as a member function. Otherwise it must be a free function and it becomes the definition of
    that operator on the type.
- The name of a library (e.g.using L for uint) - all non-private functions of the library are attached to the
    type as member functions

At file level, the second part,B, has to be an explicit type (without data location specifier). Inside contracts, you can also
use*in place of the type (e.g.using L for *;), which has the effect that all functions of the libraryLare attached
to _all_ types.

If you specify a library, _all_ non-private functions in the library get attached, even those where the type of the first
parameter does not match the type of the object. The type is checked at the point the function is called and function
overload resolution is performed.

If you use a list of functions (e.g. using {f, g, h, L.t} for uint), then the type (uint) has to be implicitly
convertible to the first parameter of each of these functions. This check is performed even if none of these functions
are called. Note that private library functions can only be specified whenusing foris inside a library.

If you define an operator (e.g.using {f as +} for T), then the type (T) must be a _user-defined value type_ and the
definition must be apurefunction. Operator definitions must be global. The following operators can be defined this
way:

```
Category Operator Possible signatures
Bitwise & function (T, T) pure returns (T)
| function (T, T) pure returns (T)
^ function (T, T) pure returns (T)
~ function (T) pure returns (T)
Arithmetic + function (T, T) pure returns (T)
```
- function (T, T) pure returns (T)
    function (T) pure returns (T)
* function (T, T) pure returns (T)
/ function (T, T) pure returns (T)
% function (T, T) pure returns (T)
Comparison == function (T, T) pure returns (bool)
!= function (T, T) pure returns (bool)
< function (T, T) pure returns (bool)
<= function (T, T) pure returns (bool)
> function (T, T) pure returns (bool)
>= function (T, T) pure returns (bool)

**3.9. Contracts 151**


Note that unary and binary-need separate definitions. The compiler will choose the right definition based on how the
operator is invoked.

Theusing A for B;directive is active only within the current scope (either the contract or the current module/source
unit), including within all of its functions, and has no effect outside of the contract or module in which it is used.

When the directive is used at file level and applied to a user-defined type which was defined at file level in the same
file, the wordglobalcan be added at the end. This will have the effect that the functions and operators are attached to
the type everywhere the type is available (including other files), not only in the scope of the using statement.

Let us rewrite the set example from the _Libraries_ section in this way, using file-level functions instead of library func-
tions.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.13;

struct Data {mapping(uint=> bool) flags; }
// Now we attach functions to the type.
// The attached functions can be used throughout the rest of the module.
// If you import the module, you have to
// repeat the using directive there, for example as
// import "flags.sol" as Flags;
// using {Flags.insert, Flags.remove, Flags.contains}
// for Flags.Data;
using {insert, remove, contains} forData;

functioninsert(Data storage self,uintvalue)
returns(bool)
{
if (self.flags[value])
return false;// already there
self.flags[value] = true;
return true;
}

functionremove(Data storage self,uintvalue)
returns(bool)
{
if (!self.flags[value])
return false;// not there
self.flags[value] = false;
return true;
}

functioncontains(Data storage self, uintvalue)
view
returns(bool)
{
return self.flags[value];
}

contract C {
Data knownValues;

```
(continues on next page)
```
**152 Chapter 3. Contents**


(continued from previous page)
functionregister(uintvalue) public{
// Here, all variables of type Data have
// corresponding member functions.
// The following function call is identical to
// `Set.insert(knownValues, value)`
require(knownValues.insert(value));
}
}

It is also possible to extend built-in types in that way. In this example, we will use a library.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.13;

librarySearch {
functionindexOf(uint[] storage self,uintvalue)
public
view
returns(uint)
{
for(uinti = 0; i < self.length; i++)
if (self[i] == value)return i;
returntype(uint).max;
}
}
using Searchfor uint[];

contract C {
uint[] data;

```
functionappend(uintvalue)public {
data.push(value);
}
```
functionreplace(uintfrom,uint to)public {
// This performs the library function call
uintindex = data.indexOf(from);
if (index == type(uint).max)
data.push(to);
else
data[index] = to;
}
}

Note that all external library calls are actual EVM function calls. This means that if you pass memory or value types,
a copy will be performed, even in case of theselfvariable. The only situation where no copy will be performed is
when storage reference variables are used or when internal library functions are called.

Another example shows how to define a custom operator for a user-defined type:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.19;

```
(continues on next page)
```
**3.9. Contracts 153**


```
(continued from previous page)
```
type UFixed16x2 is uint16;

using {
add as +,
div as /
}forUFixed16x2 global;

uint32 constant SCALE = 100;

functionadd(UFixed16x2 a, UFixed16x2 b) pure returns(UFixed16x2) {
return UFixed16x2.wrap(UFixed16x2.unwrap(a) + UFixed16x2.unwrap(b));
}

functiondiv(UFixed16x2 a, UFixed16x2 b) pure returns(UFixed16x2) {
uint32 a32 = UFixed16x2.unwrap(a);
uint32 b32 = UFixed16x2.unwrap(b);
uint32 result32 = a32 * SCALE / b32;
require(result32 <= type(uint16).max, "Divide overflow");
return UFixed16x2.wrap(uint16(a32 * SCALE / b32));
}

contract Math{
functionavg(UFixed16x2 a, UFixed16x2 b)public purereturns(UFixed16x2) {
return(a + b) / UFixed16x2.wrap(200);
}
}

### 3.10 Inline Assembly

You can interleave Solidity statements with inline assembly in a language close to the one of the Ethereum Virtual
Machine. This gives you more fine-grained control, which is especially useful when you are enhancing the language
by writing libraries or optimizing gas usage.

The language used for inline assembly in Solidity is called _Yul_ and it is documented in its own section. This section
will only cover how the inline assembly code can interface with the surrounding Solidity code.

```
Warning: Inline assembly is a way to access the Ethereum Virtual Machine at a low level. This bypasses several
important safety features and checks of Solidity. You should only use it for tasks that need it, and only if you are
confident with using it.
```
An inline assembly block is marked byassembly { ... }, where the code inside the curly braces is code in the _Yul_
language.

The inline assembly code can access local Solidity variables as explained below.

Different inline assembly blocks share no namespace, i.e. it is not possible to call a Yul function or access a Yul variable
defined in a different inline assembly block.

**154 Chapter 3. Contents**


**3.10.1 Example**

The following example provides library code to access the code of another contract and load it into abytesvariable.
This is possible with “plain Solidity” too, by using<address>.code. But the point here is that reusable assembly
libraries can enhance the Solidity language without a compiler change.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

libraryGetCode {
functionat(addressaddr)public viewreturns(bytesmemory code) {
assembly {
// retrieve the size of the code, this needs assembly
let size := extcodesize(addr)
// allocate output byte array - this could also be done without assembly
// by using code = new bytes(size)
code := mload(0x40)
// new "memory end" including padding
mstore(0x40, add(code, and(add(add(size, 0x20), 0x1f), not(0x1f))))
// store length in memory
mstore(code, size)
// actually retrieve the code, this needs assembly
extcodecopy(addr, add(code, 0x20), 0, size)
}
}
}

Inline assembly is also beneficial in cases where the optimizer fails to produce efficient code, for example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

libraryVectorSum {
// This function is less efficient because the optimizer currently fails to
// remove the bounds checks in array access.
functionsumSolidity(uint[]memory data)public purereturns(uintsum) {
for(uinti = 0; i < data.length; ++i)
sum += data[i];
}

```
// We know that we only access the array in bounds, so we can avoid the check.
// 0x20 needs to be added to an array because the first slot contains the
// array length.
functionsumAsm(uint[]memory data)public purereturns(uintsum) {
for(uinti = 0; i < data.length; ++i) {
assembly {
sum := add(sum, mload(add(add(data, 0x20), mul(i, 0x20))))
}
}
}
```
```
// Same as above, but accomplish the entire code within inline assembly.
functionsumPureAsm(uint[] memory data)public purereturns(uintsum) {
(continues on next page)
```
**3.10. Inline Assembly 155**


```
(continued from previous page)
assembly {
// Load the length (first 32 bytes)
let len := mload(data)
```
```
// Skip over the length field.
//
// Keep temporary variable so it can be incremented in place.
//
// NOTE: incrementing data would result in an unusable
// data variable after this assembly block
let dataElementLocation := add(data, 0x20)
```
// Iterate until the bound is not met.
for
{ let end := add(dataElementLocation, mul(len, 0x20)) }
lt(dataElementLocation, end)
{ dataElementLocation := add(dataElementLocation, 0x20) }
{
sum := add(sum, mload(dataElementLocation))
}
}
}
}

**3.10.2 Access to External Variables, Functions and Libraries**

You can access Solidity variables and other identifiers by using their name.

Local variables of value type are directly usable in inline assembly. They can both be read and assigned to.

Local variables that refer to memory evaluate to the address of the variable in memory, not the value itself. Such
variables can also be assigned to, but note that an assignment will only change the pointer and not the data and that it
is your responsibility to respect Solidity’s memory management. See _Conventions in Solidity_.

Similarly, local variables that refer to statically-sized calldata arrays or calldata structs evaluate to the address of the
variable in calldata, not the value itself. The variable can also be assigned a new offset, but note that no validation is
performed to ensure that the variable will not point beyondcalldatasize().

For external function pointers the address and the function selector can be accessed usingx.addressandx.selector.
The selector consists of four right-aligned bytes. Both values can be assigned to. For example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.10 <0.9.0;

contract C {
// Assigns a new selector and address to the return variable @fun
functioncombineToFunctionPointer(addressnewAddress,uint newSelector)publicpure␣
˓→returns(function() externalfun) {
assembly {
fun.selector := newSelector
fun.address := newAddress
}
(continues on next page)

**156 Chapter 3. Contents**


(continued from previous page)
}
}

For dynamic calldata arrays, you can access their calldata offset (in bytes) and length (number of elements) using
x.offsetandx.length. Both expressions can also be assigned to, but as for the static case, no validation will be
performed to ensure that the resulting data area is within the bounds ofcalldatasize().

For local storage variables or state variables, a single Yul identifier is not sufficient, since they do not necessarily occupy
a single full storage slot. Therefore, their “address” is composed of a slot and a byte-offset inside that slot. To retrieve
the slot pointed to by the variablex, you usex.slot, and to retrieve the byte-offset you usex.offset. Usingxitself
will result in an error.

You can also assign to the.slotpart of a local storage variable pointer. For these (structs, arrays or mappings), the
.offsetpart is always zero. It is not possible to assign to the.slotor.offsetpart of a state variable, though.

Local Solidity variables are available for assignments, for example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract C {
uintb;
functionf(uint x)public viewreturns(uintr) {
assembly {
// We ignore the storage slot offset, we know it is zero
// in this special case.
r := mul(x, sload(b.slot))
}
}
}

```
Warning: If you access variables of a type that spans less than 256 bits (for exampleuint64,address, or
bytes16), you cannot make any assumptions about bits not part of the encoding of the type. Especially, do not
assume them to be zero. To be safe, always clear the data properly before you use it in a context where this is im-
portant:uint32 x = f(); assembly { x := and(x, 0xffffffff) /* now use x */ }To clean signed
types, you can use thesignextendopcode:assembly { signextend(<num_bytes_of_x_minus_one>, x)
}
```
Since Solidity 0.6.0, the name of a inline assembly variable may not shadow any declaration visible in the scope of the
inline assembly block (including variable, contract and function declarations).

Since Solidity 0.7.0, variables and functions declared inside the inline assembly block may not contain., but using.
is valid to access Solidity variables from outside the inline assembly block.

**3.10. Inline Assembly 157**


**3.10.3 Things to Avoid**

Inline assembly might have a quite high-level look, but it actually is extremely low-level. Function calls, loops, ifs and
switches are converted by simple rewriting rules and after that, the only thing the assembler does for you is re-arranging
functional-style opcodes, counting stack height for variable access and removing stack slots for assembly-local variables
when the end of their block is reached.

**3.10.4 Conventions in Solidity**

**Values of Typed Variables**

In contrast to EVM assembly, Solidity has types which are narrower than 256 bits, e.g.uint24. For efficiency, most
arithmetic operations ignore the fact that types can be shorter than 256 bits, and the higher-order bits are cleaned when
necessary, i.e., shortly before they are written to memory or before comparisons are performed. This means that if you
access such a variable from within inline assembly, you might have to manually clean the higher-order bits first.

**Memory Management**

Solidity manages memory in the following way. There is a “free memory pointer” at position0x40in memory. If
you want to allocate memory, use the memory starting from where this pointer points at and update it. There is no
guarantee that the memory has not been used before and thus you cannot assume that its contents are zero bytes. There
is no built-in mechanism to release or free allocated memory. Here is an assembly snippet you can use for allocating
memory that follows the process outlined above:

functionallocate(length) -> pos {
pos := mload(0x40)
mstore(0x40, add(pos, length))
}

The first 64 bytes of memory can be used as “scratch space” for short-term allocation. The 32 bytes after the free
memory pointer (i.e., starting at0x60) are meant to be zero permanently and is used as the initial value for empty
dynamic memory arrays. This means that the allocatable memory starts at0x80, which is the initial value of the free
memory pointer.

Elements in memory arrays in Solidity always occupy multiples of 32 bytes (this is even true forbytes1[], but not for
bytesandstring). Multi-dimensional memory arrays are pointers to memory arrays. The length of a dynamic array
is stored at the first slot of the array and followed by the array elements.

```
Warning: Statically-sized memory arrays do not have a length field, but it might be added later to allow better
convertibility between statically and dynamically-sized arrays; so, do not rely on this.
```
**Memory Safety**

Without the use of inline assembly, the compiler can rely on memory to remain in a well-defined state at all times.
This is especially relevant for _the new code generation pipeline via Yul IR_ : this code generation path can move local
variables from stack to memory to avoid stack-too-deep errors and perform additional memory optimizations, if it can
rely on certain assumptions about memory use.

While we recommend to always respect Solidity’s memory model, inline assembly allows you to use memory in an
incompatible way. Therefore, moving stack variables to memory and additional memory optimizations are, by default,

**158 Chapter 3. Contents**


globally disabled in the presence of any inline assembly block that contains a memory operation or assigns to Solidity
variables in memory.

However, you can specifically annotate an assembly block to indicate that it in fact respects Solidity’s memory model
as follows:

assembly ("memory-safe") {
...
}

In particular, a memory-safe assembly block may only access the following memory ranges:

- Memory allocated by yourself using a mechanism like theallocatefunction described above.
- Memory allocated by Solidity, e.g. memory within the bounds of a memory array you reference.
- The scratch space between memory offset 0 and 64 mentioned above.
- Temporary memory that is located _after_ the value of the free memory pointer at the beginning of the assembly
    block, i.e. memory that is “allocated” at the free memory pointer without updating the free memory pointer.

Furthermore, if the assembly block assigns to Solidity variables in memory, you need to assure that accesses to the
Solidity variables only access these memory ranges.

Since this is mainly about the optimizer, these restrictions still need to be followed, even if the assembly block
reverts or terminates. As an example, the following assembly snippet is not memory safe, because the value of
returndatasize()may exceed the 64 byte scratch space:

assembly {
returndatacopy(0, 0, returndatasize())
revert(0, returndatasize())
}

On the other hand, the following code _is_ memory safe, because memory beyond the location pointed to by the free
memory pointer can safely be used as temporary scratch space:

assembly ("memory-safe") {
let p := mload(0x40)
returndatacopy(p, 0, returndatasize())
revert(p, returndatasize())
}

Note that you do not need to update the free memory pointer if there is no following allocation, but you can only use
memory starting from the current offset given by the free memory pointer.

If the memory operations use a length of zero, it is also fine to just use any offset (not only if it falls into the scratch
space):

assembly ("memory-safe") {
revert(0, 0)
}

Note that not only memory operations in inline assembly itself can be memory-unsafe, but also assignments to Solidity
variables of reference type in memory. For example the following is not memory-safe:

bytesmemory x;
assembly {
x := 0x40
(continues on next page)

**3.10. Inline Assembly 159**


```
(continued from previous page)
```
}
x[0x20] = 0x42;

Inline assembly that neither involves any operations that access memory nor assigns to any Solidity variables in memory
is automatically considered memory-safe and does not need to be annotated.

```
Warning: It is your responsibility to make sure that the assembly actually satisfies the memory model. If you
annotate an assembly block as memory-safe, but violate one of the memory assumptions, this will lead to incorrect
and undefined behavior that cannot easily be discovered by testing.
```
In case you are developing a library that is meant to be compatible across multiple versions of Solidity, you can use a
special comment to annotate an assembly block as memory-safe:

/// @solidity memory-safe-assembly
assembly {

}

Note that we will disallow the annotation via comment in a future breaking release; so, if you are not concerned with
backward-compatibility with older compiler versions, prefer using the dialect string.

### 3.11 Cheatsheet

**3.11.1 Order of Precedence of Operators**

The following is the order of precedence for operators, listed in order of evaluation.

**160 Chapter 3. Contents**


```
Precedence Description Operator
1 Postfix increment and decrement ++,--
New expression new <typename>
Array subscripting <array>[<index>]
Member access <object>.<member>
Function-like call <func>(<args...>)
Parentheses (<statement>)
2 Prefix increment and decrement ++,--
Unary minus -
Unary operations delete
Logical NOT!
Bitwise NOT ~
3 Exponentiation **
4 Multiplication, division and modulo *,/,%
5 Addition and subtraction +,-
6 Bitwise shift operators <<,>>
7 Bitwise AND &
8 Bitwise XOR ^
9 Bitwise OR |
10 Inequality operators <,>,<=,>=
11 Equality operators ==,!=
12 Logical AND &&
13 Logical OR ||
14 Ternary operator <conditional>? <if-true> : <if-false>
Assignment operators =,|=,^=,&=,<<=,>>=,+=,-=,*=,/=,%=
15 Comma operator ,
```
**3.11.2 ABI Encoding and Decoding Functions**

- abi.decode(bytes memory encodedData, (...)) returns (...): _ABI_ -decodes the provided data.
    The types are given in parentheses as second argument. Example:(uint a, uint[2] memory b, bytes
    memory c) = abi.decode(data, (uint, uint[2], bytes))
- abi.encode(...) returns (bytes memory): _ABI_ -encodes the given arguments
- abi.encodePacked(...) returns (bytes memory): Performs _packed encoding_ of the given arguments.
    Note that this encoding can be ambiguous!
- abi.encodeWithSelector(bytes4 selector, ...) returns (bytes memory): _ABI_ -encodes the
    given arguments starting from the second and prepends the given four-byte selector
- abi.encodeCall(function functionPointer, (...)) returns (bytes memory): ABI-encodes a
    call tofunctionPointerwith the arguments found in the tuple. Performs a full type-check, ensuring the types
    match the function signature. Result equalsabi.encodeWithSelector(functionPointer.selector, ..
    .)
- abi.encodeWithSignature(string memory signature, ...) returns (bytes memory): Equiva-
    lent toabi.encodeWithSelector(bytes4(keccak256(bytes(signature))), ...)

**3.11. Cheatsheet 161**


**3.11.3 Members of** bytes **and** string

- bytes.concat(...) returns (bytes memory): _Concatenates variable number of arguments to one byte_
    _array_
- string.concat(...) returns (string memory): _Concatenates variable number of arguments to one_
    _string array_

**3.11.4 Members of** address

- <address>.balance(uint256): balance of the _Address_ in Wei
- <address>.code(bytes memory): code at the _Address_ (can be empty)
- <address>.codehash(bytes32): the codehash of the _Address_
- <address>.call(bytes memory) returns (bool, bytes memory): issue low-levelCALLwith the given
    payload, returns success condition and return data
- <address>.delegatecall(bytes memory) returns (bool, bytes memory): issue low-level
    DELEGATECALLwith the given payload, returns success condition and return data
- <address>.staticcall(bytes memory) returns (bool, bytes memory): issue low-level
    STATICCALLwith the given payload, returns success condition and return data
- <address payable>.send(uint256 amount) returns (bool): send given amount of Wei to _Address_ ,
    returnsfalseon failure
- <address payable>.transfer(uint256 amount): send given amount of Wei to _Address_ , throws on failure

**3.11.5 Block and Transaction Properties**

- blockhash(uint blockNumber) returns (bytes32): hash of the given block - only works for 256 most
    recent blocks
- blobhash(uint index) returns (bytes32): versioned hash of theindex-th blob associated with the cur-
    rent transaction. A versioned hash consists of a single byte representing the version (currently0x01), followed
    by the last 31 bytes of the SHA256 hash of the KZG commitment (EIP-4844). Returns zero if no blob with the
    given index exists.
- block.basefee(uint): current block’s base fee (EIP-3198 and EIP-1559)
- block.blobbasefee(uint): current block’s blob base fee (EIP-7516 and EIP-4844)
- block.chainid(uint): current chain id
- block.coinbase(address payable): current block miner’s address
- block.difficulty(uint): current block difficulty (EVM < Paris). For other EVM versions it behaves as a
    deprecated alias forblock.prevrandaothat will be removed in the next breaking release
- block.gaslimit(uint): current block gaslimit
- block.number(uint): current block number
- block.prevrandao(uint): random number provided by the beacon chain (EVM >= Paris) (see EIP-4399 )
- block.timestamp(uint): current block timestamp in seconds since Unix epoch
- gasleft() returns (uint256): remaining gas
- msg.data(bytes): complete calldata

**162 Chapter 3. Contents**


- msg.sender(address): sender of the message (current call)
- msg.sig(bytes4): first four bytes of the calldata (i.e. function identifier)
- msg.value(uint): number of wei sent with the message
- tx.gasprice(uint): gas price of the transaction
- tx.origin(address): sender of the transaction (full call chain)

**3.11.6 Validations and Assertions**

- assert(bool condition): abort execution and revert state changes if condition isfalse(use for internal
    error)
- require(bool condition): abort execution and revert state changes if condition isfalse(use for malformed
    input or error in external component)
- require(bool condition, string memory message): abort execution and revert state changes if condi-
    tion isfalse(use for malformed input or error in external component). Also provide error message.
- revert(): abort execution and revert state changes
- revert(string memory message): abort execution and revert state changes providing an explanatory string

**3.11.7 Mathematical and Cryptographic Functions**

- keccak256(bytes memory) returns (bytes32): compute the Keccak-256 hash of the input
- sha256(bytes memory) returns (bytes32): compute the SHA-256 hash of the input
- ripemd160(bytes memory) returns (bytes20): compute the RIPEMD-160 hash of the input
- ecrecover(bytes32 hash, uint8 v, bytes32 r, bytes32 s) returns (address): recover address
    associated with the public key from elliptic curve signature, return zero on error
- addmod(uint x, uint y, uint k) returns (uint): compute(x + y) % kwhere the addition is per-
    formed with arbitrary precision and does not wrap around at2**256. Assert thatk != 0starting from version
    0.5.0.
- mulmod(uint x, uint y, uint k) returns (uint): compute(x * y) % kwhere the multiplication is
    performed with arbitrary precision and does not wrap around at2**256. Assert thatk != 0starting from
    version 0.5.0.

**3.11.8 Contract-related**

- this(current contract’s type): the current contract, explicitly convertible toaddressoraddress payable
- super: a contract one level higher in the inheritance hierarchy
- selfdestruct(address payable recipient): send all funds to the given address and (only on EVMs be-
    fore Cancun or when invoked within the transaction creating the contract) destroy the contract.

**3.11. Cheatsheet 163**


**3.11.9 Type Information**

- type(C).name(string): the name of the contract
- type(C).creationCode(bytes memory): creation bytecode of the given contract, see _Type Information_.
- type(C).runtimeCode(bytes memory): runtime bytecode of the given contract, see _Type Information_.
- type(I).interfaceId(bytes4): value containing the EIP-165 interface identifier of the given interface, see
    _Type Information_.
- type(T).min(T): the minimum value representable by the integer typeT, see _Type Information_.
- type(T).max(T): the maximum value representable by the integer typeT, see _Type Information_.

**3.11.10 Function Visibility Specifiers**

functionmyFunction() <visibility specifier>returns(bool) {
return true;
}

- public: visible externally and internally (creates a _getter function_ for storage/state variables)
- private: only visible in the current contract
- external: only visible externally (only for functions) - i.e. can only be message-called (viathis.func)
- internal: only visible internally

**3.11.11 Modifiers**

- purefor functions: Disallows modification or access of state.
- viewfor functions: Disallows modification of state.
- payablefor functions: Allows them to receive Ether together with a call.
- constantfor state variables: Disallows assignment (except initialization), does not occupy storage slot.
- immutablefor state variables: Allows assignment at construction time and is constant when deployed. Is stored
    in code.
- anonymousfor events: Does not store event signature as topic.
- indexedfor event parameters: Stores the parameter as topic.
- virtualfor functions and modifiers: Allows the function’s or modifier’s behavior to be changed in derived
    contracts.
- override: States that this function, modifier or public state variable changes the behavior of a function or
    modifier in a base contract.

**164 Chapter 3. Contents**


### 3.12 Language Grammar

parser grammar SolidityParser

```
Solidity is a statically typed, contract-oriented, high-level language for implementing smart contracts on the
Ethereum platform.
rule source-unit
On top level, Solidity allows pragmas, import directives, and definitions of contracts, interfaces, libraries,
structs, enums and constants.
```
```
pragma pragma-token ;
```
```
import-directive
using-directive
contract-definition
interface-definition
library-definition
function-definition
constant-variable-declaration
struct-definition
enum-definition
user-defined-value-type-definition
error-definition
event-definition
```
```
eof
```
```
rule import-directive
Import directives import identifiers from different files.
```
```
import path as identifier
symbol-aliases from path
* as identifier from path
```
```
;
```
```
rule path
Path of a file to be imported.
```
```
non-empty-string-literal
```
```
rule symbol-aliases
List of aliases for symbols to be imported.
```
```
{ identifier as identifier
,
```
```
}
```
```
rule contract-definition
Top-level definition of a contract.
```
**3.12. Language Grammar 165**


```
abstract contract identifier
```
```
is inheritance-specifier
,
```
```
{ contract-body-element }
```
```
rule interface-definition
Top-level definition of an interface.
```
```
interface identifier
```
```
is inheritance-specifier
,
```
```
{ contract-body-element }
```
```
rule library-definition
Top-level definition of a library.
```
```
library identifier { contract-body-element }
```
```
rule inheritance-specifier
Inheritance specifier for contracts and interfaces. Can optionally supply base constructor arguments.
```
```
identifier-path call-argument-list
```
```
rule contract-body-element
Declarations that can be used in contracts, interfaces and libraries.
Note that interfaces and libraries may not contain constructors, interfaces may not contain state variables
and libraries may not contain fallback, receive functions nor non-constant state variables.
```
**166 Chapter 3. Contents**


```
constructor-definition
function-definition
modifier-definition
fallback-function-definition
receive-function-definition
struct-definition
enum-definition
user-defined-value-type-definition
state-variable-declaration
event-definition
error-definition
using-directive
```
```
rule call-argument-list
Arguments when calling a function or a similar callable object. The arguments are either given as comma
separated list or as map of named arguments.
```
```
(
```
```
expression
,
```
```
{ identifier : expression
,
```
```
}
```
```
)
```
```
rule identifier-path
Qualified name.
identifier
.
```
```
rule modifier-invocation
Call to a modifier. If the modifier takes no arguments, the argument list can be skipped entirely (including
opening and closing parentheses).
```
```
identifier-path call-argument-list
```
```
rule visibility
Visibility for functions and function types.
```
```
internal
external
private
public
```
**3.12. Language Grammar 167**


```
rule parameter-list
A list of parameters, such as function arguments or return values.
```
```
type-name data-location identifier
,
```
```
rule constructor-definition
Definition of a constructor. Must always supply an implementation. Note that specifying internal or public
visibility is deprecated.
```
```
constructor ( parameter-list )
```
```
modifier-invocation
payable
internal
public
```
```
block
```
```
rule state-mutability
State mutability for function types. The default mutability ‘non-payable’ is assumed if no mutability is
specified.
```
```
pure
view
payable
```
```
rule override-specifier
An override specifier used for functions, modifiers or state variables. In cases where there are ambiguous
declarations in several base contracts being overridden, a complete list of base contracts has to be given.
```
```
override ( identifier-path
,
```
```
)
```
```
rule function-definition
The definition of contract, library, interface or free functions. Depending on the context in which the
function is defined, further restrictions may apply, e.g. functions in interfaces have to be unimplemented,
i.e. may not contain a body block.
```
**168 Chapter 3. Contents**


```
function identifier
fallback
receive
```
```
( parameter-list )
```
```
visibility
state-mutability
modifier-invocation
virtual
override-specifier
```
```
returns ( parameter-list ) ;
block
```
```
rule modifier-definition
The definition of a modifier. Note that within the body block of a modifier, the underscore cannot be used
as identifier, but is used as placeholder statement for the body of a function to which the modifier is applied.
```
```
modifier identifier ( parameter-list )
```
```
virtual
override-specifier
```
```
;
block
```
```
rule fallback-function-definition
Definition of the special fallback function.
```
```
fallback ( parameter-list )
```
```
external
state-mutability
modifier-invocation
virtual
override-specifier
```
```
returns ( parameter-list ) ;
block
```
**3.12. Language Grammar 169**


```
rule receive-function-definition
Definition of the special receive function.
```
```
receive ( ) external
payable
modifier-invocation
virtual
override-specifier
```
```
;
block
```
```
rule struct-definition
Definition of a struct. Can occur at top-level within a source unit or within a contract, library or interface.
struct identifier { struct-member }
```
```
rule struct-member
The declaration of a named struct member.
type-name identifier ;
```
```
rule enum-definition
Definition of an enum. Can occur at top-level within a source unit or within a contract, library or interface.
```
```
enum identifier { identifier
,
```
```
}
```
```
rule user-defined-value-type-definition
Definition of a user defined value type. Can occur at top-level within a source unit or within a contract,
library or interface.
```
```
type identifier is elementary-type-name ;
```
```
rule state-variable-declaration
The declaration of a state variable.
```
**170 Chapter 3. Contents**


```
type-name public
private
internal
constant
override-specifier
immutable
transient
```
```
identifier
```
```
= expression
```
```
;
```
```
rule constant-variable-declaration
The declaration of a constant variable.
type-name constant identifier = expression ;
```
```
rule event-parameter
Parameter of an event.
```
```
type-name indexed identifier
```
```
rule event-definition
Definition of an event. Can occur in contracts, libraries or interfaces.
```
```
event identifier ( event-parameter
,
```
```
)
```
```
anonymous
```
```
;
```
```
rule error-parameter
Parameter of an error.
```
```
type-name identifier
```
```
rule error-definition
Definition of an error.
```
```
error identifier ( error-parameter
,
```
```
) ;
```
```
rule user-definable-operator
Operators that users are allowed to implement for some types with using for.
```
**3.12. Language Grammar 171**


```
& ~ | ^ + / % * -
```
```
==
>
>=
<
<=
!=
```
```
rule using-directive
Using directive to attach library functions and free functions to types. Can occur within contracts and
libraries and at the file level.
using identifier-path
{ using-aliases
,
```
```
}
```
```
for
```
```
*
type-name
```
```
global ;
```
```
rule using-aliases
```
```
identifier-path as user-definable-operator
```
```
rule type-name
A type name can be an elementary type, a function type, a mapping type, a user-defined type (e.g. a contract
or struct) or an array type.
```
**172 Chapter 3. Contents**


```
elementary-type-name
function-type-name
mapping-type
identifier-path
```
```
type-name [ expression ]
```
```
rule elementary-type-name
```
```
address
address payable
bool
string
bytes
signed-integer-type
unsigned-integer-type
fixed-bytes
fixed
ufixed
```
```
rule function-type-name
```
```
function ( parameter-list )
```
```
visibility
state-mutability
```
```
returns ( parameter-list )
```
```
rule variable-declaration
The declaration of a single variable.
```
```
type-name data-location identifier
```
```
rule data-location
```
```
memory
storage
calldata
```
```
rule expression
Complex expression. Can be an index access, an index range access, a member access, a function call
(with optional function call options), a type conversion, an unary or binary expression, a comparison or
```
**3.12. Language Grammar 173**


```
assignment, a ternary expression, a new-expression (i.e. a contract creation or the allocation of a dynamic
memory array), a tuple, an inline array or a primary expression (i.e. an identifier, literal or type name).
```
**174 Chapter 3. Contents**


```
expression [ expression ]
```
```
expression [ expression : expression ]
expression. identifier
address
```
```
expression { identifier : expression
,
```
```
}
```
```
expression call-argument-list
payable call-argument-list
type ( type-name )
++
--
!
~
delete
```
-

```
expression
```
```
expression ++
--
expression ** expression
expression *
/
%
```
```
expression
```
```
expression +
```
-

```
expression
```
```
expression <<
>>
>>>
```
```
expression
```
```
expression & expression
expression ^ expression
expression | expression
expression <
>
<=
>=
```
```
expression
```
```
expression ==
!=
```
```
expression
```
```
expression && expression
expression || expression
expression? expression : expression
expression =
|=
^=
&=
<<=
>>=
>>>=
+=
-=
*=
/=
%=
```
```
expression
```
```
new type-name
tuple-expression
inline-array-expression
identifier
literal
literal-with-sub-denomination
elementary-type-name
```
**3.12. Language Grammar 175**


```
rule tuple-expression
```
```
( expression
,
```
```
)
```
```
rule inline-array-expression
An inline array expression denotes a statically sized array of the common type of the contained expressions.
```
```
[ expression
,
```
```
]
```
```
rule identifier
Besides regular non-keyword Identifiers, some keywords like ‘from’ and ‘error’ can also be used as iden-
tifiers.
identifier
from
error
revert
global
transient
```
```
rule literal
```
```
string-literal
number-literal
boolean-literal
hex-string-literal
unicode-string-literal
```
```
rule literal-with-sub-denomination
```
```
number-literal sub-denomination
```
```
rule boolean-literal
```
```
true
false
```
```
rule string-literal
A full string literal consists of either one or several consecutive quoted strings.
```
```
non-empty-string-literal
empty-string-literal
```
```
rule hex-string-literal
A full hex string literal that consists of either one or several consecutive hex strings.
```
**176 Chapter 3. Contents**


```
hex-string
```
```
rule unicode-string-literal
A full unicode string literal that consists of either one or several consecutive unicode strings.
unicode-string-literal
```
```
rule number-literal
Number literals can be decimal or hexadecimal numbers with an optional unit.
```
```
decimal-number
hex-number
```
```
rule block
A curly-braced block of statements. Opens its own scope.
```
```
{ statement
unchecked-block
```
```
}
```
```
rule unchecked-block
```
```
unchecked block
```
```
rule statement
```
```
block
variable-declaration-statement
expression-statement
if-statement
for-statement
while-statement
do-while-statement
continue-statement
break-statement
try-statement
return-statement
emit-statement
revert-statement
assembly-statement
```
```
rule if-statement
If statement with optional else part.
```
**3.12. Language Grammar 177**


```
if ( expression ) statement
```
```
else statement
```
```
rule for-statement
For statement with optional init, condition and post-loop part.
```
```
for ( variable-declaration-statement
expression-statement
;
```
```
expression-statement
;
```
```
expression ) statement
```
```
rule while-statement
```
```
while ( expression ) statement
```
```
rule do-while-statement
```
```
do statement while ( expression ) ;
```
```
rule continue-statement
A continue statement. Only allowed inside for, while or do-while loops.
continue ;
```
```
rule break-statement
A break statement. Only allowed inside for, while or do-while loops.
```
```
break ;
```
```
rule try-statement
A try statement. The contained expression needs to be an external function call or a contract creation.
```
```
try expression
```
```
returns ( parameter-list )
```
```
block catch-clause
```
```
rule catch-clause
The catch clause of a try statement.
```
**178 Chapter 3. Contents**


```
catch identifier ( parameter-list )
```
```
block
```
```
rule return-statement
```
```
return expression ;
```
```
rule emit-statement
An emit statement. The contained expression needs to refer to an event.
```
```
emit expression call-argument-list ;
```
```
rule revert-statement
A revert statement. The contained expression needs to refer to an error.
```
```
revert expression call-argument-list ;
```
```
rule assembly-statement
An inline assembly block. The contents of an inline assembly block use a separate scanner/lexer, i.e. the
set of keywords and allowed identifiers is different inside an inline assembly block.
```
```
assembly '"evmasm"' assembly-flags {
```
```
yul-statement
```
```
}
```
```
rule assembly-flags
Assembly flags. Comma-separated list of double-quoted strings as flags.
( assembly-flag-string
,
```
```
)
```
```
rule variable-declaration-tuple
A tuple of variable names to be used in variable declarations. May contain empty fields.
```
```
( , variable-declaration
```
```
, variable-declaration
```
```
)
```
```
rule variable-declaration-statement
A variable declaration statement. A single variable may be declared without initial value, whereas a tuple
of variables can only be declared with initial value.
```
**3.12. Language Grammar 179**


```
variable-declaration = expression
variable-declaration-tuple = expression
```
```
;
```
```
rule expression-statement
```
```
expression ;
```
```
rule mapping-type
```
```
mapping ( mapping-key-type identifier =>
```
```
type-name
```
```
identifier )
```
```
rule mapping-key-type
Only elementary types or user defined types are viable as mapping keys.
```
```
elementary-type-name
identifier-path
```
```
rule yul-statement
A Yul statement within an inline assembly block. continue and break statements are only valid within for
loops. leave statements are only valid within function bodies.
```
```
yul-block
yul-variable-declaration
yul-assignment
yul-function-call
yul-if-statement
yul-for-statement
yul-switch-statement
leave
break
continue
yul-function-definition
```
```
rule yul-block
```
```
{ yul-statement }
```
```
rule yul-variable-declaration
The declaration of one or more Yul variables with optional initial value. If multiple variables are declared,
only a function call is a valid initial value.
```
**180 Chapter 3. Contents**


```
let yul-identifier := yul-expression
```
```
let yul-identifier
,
```
```
:= yul-function-call
```
```
rule yul-assignment
Any expression can be assigned to a single Yul variable, whereas multi-assignments require a function call
on the right-hand side.
```
```
yul-path := yul-expression
yul-path , yul-path := yul-function-call
```
```
rule yul-if-statement
```
```
if yul-expression yul-block
```
```
rule yul-for-statement
```
```
for yul-block yul-expression yul-block yul-block
```
```
rule yul-switch-statement
A Yul switch statement can consist of only a default-case (deprecated) or one or more non-default cases
optionally followed by a default-case.
switch yul-expression
```
```
case yul-literal yul-block
```
```
default yul-block
```
```
default yul-block
```
```
rule yul-function-definition
```
```
function yul-identifier ( yul-identifier
,
```
```
)
```
```
-> yul-identifier
,
```
```
yul-block
```
```
rule yul-path
While only identifiers without dots can be declared within inline assembly, paths containing dots can refer
to declarations outside the inline assembly block.
```
**3.12. Language Grammar 181**


```
yul-identifier. yul-identifier
yul-evm-builtin
```
```
rule yul-function-call
A call to a function with return values can only occur as right-hand side of an assignment or a variable
declaration.
```
```
yul-identifier
yul-evm-builtin
```
```
( yul-expression
,
```
```
)
```
```
rule yul-boolean
```
```
true
false
```
```
rule yul-literal
```
```
yul-decimal-number
yul-string-literal
yul-hex-number
yul-boolean
hex-string
```
```
rule yul-expression
```
```
yul-path
yul-function-call
yul-literal
```
lexer grammar SolidityLexer

```
rule fixed-bytes
Bytes types of fixed length.
```
**182 Chapter 3. Contents**


```
'bytes1'
'bytes2'
'bytes3'
'bytes4'
'bytes5'
'bytes6'
'bytes7'
'bytes8'
'bytes9'
'bytes10'
'bytes11'
'bytes12'
'bytes13'
'bytes14'
'bytes15'
'bytes16'
'bytes17'
'bytes18'
'bytes19'
'bytes20'
'bytes21'
'bytes22'
'bytes23'
'bytes24'
'bytes25'
'bytes26'
'bytes27'
'bytes28'
'bytes29'
'bytes30'
'bytes31'
'bytes32'
```
```
rule sub-denomination
Unit denomination for numbers.
```
**3.12. Language Grammar 183**


```
'wei'
'gwei'
'ether'
'seconds'
'minutes'
'hours'
'days'
'weeks'
'years'
```
```
rule signed-integer-type
Sized signed integer types. int is an alias of int256.
```
**184 Chapter 3. Contents**


```
'int'
'int8'
'int16'
'int24'
'int32'
'int40'
'int48'
'int56'
'int64'
'int72'
'int80'
'int88'
'int96'
'int104'
'int112'
'int120'
'int128'
'int136'
'int144'
'int152'
'int160'
'int168'
'int176'
'int184'
'int192'
'int200'
'int208'
'int216'
'int224'
'int232'
'int240'
'int248'
'int256'
```
```
rule unsigned-integer-type
Sized unsigned integer types. uint is an alias of uint256.
```
**3.12. Language Grammar 185**


```
'uint'
'uint8'
'uint16'
'uint24'
'uint32'
'uint40'
'uint48'
'uint56'
'uint64'
'uint72'
'uint80'
'uint88'
'uint96'
'uint104'
'uint112'
'uint120'
'uint128'
'uint136'
'uint144'
'uint152'
'uint160'
'uint168'
'uint176'
'uint184'
'uint192'
'uint200'
'uint208'
'uint216'
'uint224'
'uint232'
'uint240'
'uint248'
'uint256'
```
```
rule non-empty-string-literal
A non-empty quoted string literal restricted to printable characters.
```
**186 Chapter 3. Contents**


```
'"' double-quoted-printable
escape-sequence
```
```
'"'
```
```
'\'' single-quoted-printable
escape-sequence
```
```
'\''
```
```
rule empty-string-literal
An empty string literal
```
```
'"' '"'
'\'' '\''
```
```
rule single-quoted-printable
Any printable character except single quote or back slash.
```
```
[\u0020-\u0026\u0028-\u005B\u005D-\u007E]
```
```
rule double-quoted-printable
Any printable character except double quote or back slash.
[\u0020-\u0021\u0023-\u005B\u005D-\u007E]
```
```
rule escape-sequence
Escape sequence. Apart from common single character escape sequences, line breaks can be escaped as
well as four hex digit unicode escapes \uXXXX and two digit hex escape sequences \xXX are allowed.
```
```
'\\'
```
```
['"\\nrt\n\r]
'u' [0-9A-Fa-f] [0-9A-Fa-f] [0-9A-Fa-f] [0-9A-Fa-f]
'x' [0-9A-Fa-f] [0-9A-Fa-f]
```
```
rule unicode-string-literal
A single quoted string literal allowing arbitrary unicode characters.
'unicode'
```
```
'"' ~["\r\n\\]
escape-sequence
```
```
'"'
```
```
'\'' ~['\r\n\\]
escape-sequence
```
```
'\''
```
```
rule hex-string
Hex strings need to consist of an even number of hex digits that may be grouped using underscores.
```
**3.12. Language Grammar 187**


```
'hex'
```
```
'"' [0-9A-Fa-f] [0-9A-Fa-f]
```
```
'_'
```
```
'"'
```
```
'\'' [0-9A-Fa-f] [0-9A-Fa-f]
```
```
'_'
```
```
'\''
```
```
rule hex-number
Hex numbers consist of a prefix and an arbitrary number of hex digits that may be delimited by underscores.
```
```
'0' 'x' [0-9A-Fa-f]
```
```
'_'
```
```
rule decimal-number
A decimal number literal consists of decimal digits that may be delimited by underscores and an optional
positive or negative exponent. If the digits contain a decimal point, the literal has fixed point type.
```
```
[0-9]
```
```
'_'
```
```
[0-9]
```
```
'_'
```
```
'.' [0-9]
```
```
'_'
```
```
[eE] '-' [0-9]
```
```
'_'
```
```
rule identifier
An identifier in solidity has to start with a letter, a dollar-sign or an underscore and may additionally contain
numbers after the first symbol.
```
```
[a-zA-Z$_] [a-zA-Z0-9$_]
```
```
rule yul-evm-builtin
Builtin functions in the EVM Yul dialect.
```
**188 Chapter 3. Contents**


```
'stop'
'add'
'sub'
'mul'
'div'
'sdiv'
'mod'
'smod'
'exp'
'not'
'lt'
'gt'
'slt'
'sgt'
'eq'
'iszero'
'and'
'or'
'xor'
'byte'
'shl'
'shr'
'sar'
'addmod'
'mulmod'
'signextend'
'keccak256'
'pop'
'mload'
'mstore'
'mstore8'
'sload'
'sstore'
'tload'
'tstore'
'msize'
'gas'
'address'
'balance'
'selfbalance'
'caller'
'callvalue'
'calldataload'
'calldatasize'
'calldatacopy'
'extcodesize'
'extcodecopy'
'returndatasize'
'returndatacopy'
'mcopy'
'extcodehash'
'create'
'create2'
'call'
'callcode'
'delegatecall'
'staticcall'
'return'
'revert'
'selfdestruct'
'invalid'
'log0'
'log1'
'log2'
'log3'
'log4'
'chainid'
'origin'
'gasprice'
'blockhash'
'blobhash'
'coinbase'
'timestamp'
'number'
'difficulty'
'prevrandao'
'gaslimit'
'basefee'
'blobbasefee'
```
**3.12. Language Grammar 189**


```
rule yul-identifier
Yul identifiers consist of letters, dollar signs, underscores and numbers, but may not start with a number.
In inline assembly there cannot be dots in user-defined identifiers. Instead see yulPath for expressions
consisting of identifiers with dots.
```
```
[a-zA-Z$_] [a-zA-Z0-9$_]
```
```
rule yul-hex-number
Hex literals in Yul consist of a prefix and one or more hexadecimal digits.
```
```
'0' 'x' [0-9a-fA-F]
```
```
rule yul-decimal-number
Decimal literals in Yul may be zero or any sequence of decimal digits without leading zeroes.
```
```
'0'
```
```
[1-9] [0-9]
```
```
rule yul-string-literal
String literals in Yul consist of one or more double-quoted or single-quoted strings that may contain escape
sequences and printable characters except unescaped line breaks or unescaped double-quotes or single-
quotes, respectively.
```
```
'"' double-quoted-printable
escape-sequence
```
```
'"'
```
```
'\'' single-quoted-printable
escape-sequence
```
```
'\''
```
```
rule pragma-token
Pragma token. Can contain any kind of symbol except a semicolon. Note that currently the solidity parser
only allows a subset of this.
```
### 3.13 Using the Compiler

**3.13.1 Using the Commandline Compiler**

**Note:** This section does not apply to _solcjs_ , not even if it is used in commandline mode.

**190 Chapter 3. Contents**


**Basic Usage**

One of the build targets of the Solidity repository issolc, the Solidity commandline compiler. Usingsolc --help
provides you with an explanation of all options. The compiler can produce various outputs, ranging from simple
binaries and assembly over an abstract syntax tree (parse tree) to estimations of gas usage. If you only want to compile
a single file, you run it assolc --bin sourceFile.soland it will print the binary. If you want to get some of the
more advanced output variants ofsolc, it is probably better to tell it to output everything to separate files usingsolc
-o outputDirectory --bin --ast-compact-json --asm sourceFile.sol.

**Optimizer Options**

Before you deploy your contract, activate the optimizer when compiling using solc --optimize --bin
sourceFile.sol. By default, the optimizer will optimize the contract assuming it is called 200 times across its
lifetime (more specifically, it assumes each opcode is executed around 200 times). If you want the initial contract de-
ployment to be cheaper and the later function executions to be more expensive, set it to--optimize-runs=1. If you
expect many transactions and do not care for higher deployment cost and output size, set--optimize-runsto a high
number. This parameter has effects on the following (this might change in the future):

- the size of the binary search in the function dispatch routine
- the way constants like large numbers or strings are stored

**Base Path and Import Remapping**

The commandline compiler will automatically read imported files from the filesystem, but it is also possible to provide
_path redirects_ usingprefix=pathin the following way:

solc github.com/ethereum/dapp-bin/=/usr/local/lib/dapp-bin/ file.sol

This essentially instructs the compiler to search for anything starting withgithub.com/ethereum/dapp-bin/under
/usr/local/lib/dapp-bin.

When accessing the filesystem to search for imports, _paths that do not start with ./ or ../_ are treated as relative to the
directories specified using--base-pathand--include-pathoptions (or the current working directory if base path
is not specified). Furthermore, the part of the path added via these options will not appear in the contract metadata.

For security reasons the compiler has _restrictions on what directories it can access_. Directories of source files specified
on the command-line and target paths of remappings are automatically allowed to be accessed by the file reader, but ev-
erything else is rejected by default. Additional paths (and their subdirectories) can be allowed via the--allow-paths
/sample/path,/another/sample/pathswitch. Everything inside the path specified via--base-pathis always
allowed.

The above is only a simplification of how the compiler handles import paths. For a detailed explanation with examples
and discussion of corner cases please refer to the section on _path resolution_.

**3.13. Using the Compiler 191**


**Library Linking**

If your contracts use _libraries_ , you will notice that the bytecode contains substrings of the form
__$53aea86b7d70b31448b230b20ae141a537$__(format was different <v0.5.0). These are placeholders for
the actual library addresses. The placeholder is a 34 character prefix of the hex encoding of the keccak256 hash of
the fully qualified library name. The bytecode file will also contain lines of the form// <placeholder> -> <fq
library name>at the end to help identify which libraries the placeholders represent. Note that the fully qualified
library name is the path of its source file and the library name separated by:. You can usesolcas a linker meaning
that it will insert the library addresses for you at those points:

Either add --libraries "file.sol:Math=0x1234567890123456789012345678901234567890 file.
sol:Heap=0xabCD567890123456789012345678901234567890"to your command to provide an address for each
library (use commas or spaces as separators) or store the string in a file (one library per line) and runsolcusing
--libraries fileName.

**Note:** Starting Solidity 0.8.1 accepts = as separator between library and address,
and : as a separator is deprecated. It will be removed in the future. Currently
--libraries "file.sol:Math:0x1234567890123456789012345678901234567890 file.
sol:Heap:0xabCD567890123456789012345678901234567890"will work too.

Ifsolcis called with the option--standard-json, it will expect a JSON input (as explained below) on the standard
input, and return a JSON output on the standard output. This is the recommended interface for more complex and
especially automated uses. The process will always terminate in a “success” state and report any errors via the JSON
output. The option--base-pathis also processed in standard-json mode.

Ifsolcis called with the option--link, all input files are interpreted to be unlinked binaries (hex-encoded) in the
__$53aea86b7d70b31448b230b20ae141a537$__-format given above and are linked in-place (if the input is read
from stdin, it is written to stdout). All options except--librariesare ignored (including-o) in this case.

```
Warning: Manually linking libraries on the generated bytecode is discouraged because it does not update contract
metadata. Since metadata contains a list of libraries specified at the time of compilation and bytecode contains a
metadata hash, you will get different binaries, depending on when linking is performed.
You should ask the compiler to link the libraries at the time a contract is compiled by either using the--libraries
option ofsolcor thelibrarieskey if you use the standard-JSON interface to the compiler.
```
**Note:** The library placeholder used to be the fully qualified name of the library itself instead of the hash of it. This
format is still supported bysolc --linkbut the compiler will no longer output it. This change was made to reduce
the likelihood of a collision between libraries, since only the first 36 characters of the fully qualified library name could
be used.

**192 Chapter 3. Contents**


**3.13.2 Setting the EVM Version to Target**

When you compile your contract code you can specify the Ethereum virtual machine version to compile for to avoid
particular features or behaviors.

```
Warning: Compiling for the wrong EVM version can result in wrong, strange and failing behavior. Please ensure,
especially if running a private chain, that you use matching EVM versions.
```
On the command-line, you can select the EVM version as follows:

solc --evm-version <VERSION> contract.sol

In the _standard JSON interface_ , use the"evmVersion"key in the"settings"field:

{
"sources": {/* ... */},
"settings": {
"optimizer": {/* ... */},
"evmVersion": "<VERSION>"
}
}

**Target Options**

Below is a list of target EVM versions and the compiler-relevant changes introduced at each version. Backward com-
patibility is not guaranteed between each version.

- homestead **(** **_support deprecated_** **)**
    **-** (oldest version)
- tangerineWhistle **(** **_support deprecated_** **)**
    **-** Gas cost for access to other accounts increased, relevant for gas estimation and the optimizer.
    **-** All gas sent by default for external calls, previously a certain amount had to be retained.
- spuriousDragon **(** **_support deprecated_** **)**
    **-** Gas cost for theexpopcode increased, relevant for gas estimation and the optimizer.
- byzantium **(** **_support deprecated_** **)**
    **-** Opcodesreturndatacopy,returndatasizeandstaticcallare available in assembly.
    **-** Thestaticcallopcode is used when calling non-library view or pure functions, which prevents
       the functions from modifying state at the EVM level, i.e., even applies when you use invalid type
       conversions.
    **-** It is possible to access dynamic data returned from function calls.
    **-** revertopcode introduced, which means thatrevert()will not waste gas.
- constantinople
    **-** Opcodescreate2,extcodehash,shl,shrandsarare available in assembly.
    **-** Shifting operators use shifting opcodes and thus need less gas.
- petersburg

**3.13. Using the Compiler 193**


**-** The compiler behaves the same way as with constantinople.
- istanbul
**-** Opcodeschainidandselfbalanceare available in assembly.
- berlin
**-** Gas costs forSLOAD,*CALL,BALANCE,EXT*andSELFDESTRUCTincreased. The compiler assumes
cold gas costs for such operations. This is relevant for gas estimation and the optimizer.
- london
**-** The block’s base fee (EIP-3198 and EIP-1559) can be accessed via the globalblock.basefeeor
basefee()in inline assembly.
- paris
**-** Introducesprevrandao()andblock.prevrandao, and changes the semantics of the now deprecated
block.difficulty, disallowingdifficulty()in inline assembly (see EIP-4399).
- shanghai
**-** Smaller code size and gas savings due to the introduction ofpush0(see EIP-3855).
- cancun **(default)
-** The block’s blob base fee (EIP-7516 and EIP-4844) can be accessed via the global block.
blobbasefeeorblobbasefee()in inline assembly.
**-** Introducesblobhash()in inline assembly and a corresponding global function to retrieve versioned
hashes of blobs associated with the transaction (see EIP-4844).
**-** Opcodemcopyis available in assembly (see EIP-5656).
**-** Opcodeststoreandtloadare available in assembly (see EIP-1153).
- prague( **experimental** )

**3.13.3 Compiler Input and Output JSON Description**

The recommended way to interface with the Solidity compiler especially for more complex and automated setups is
the so-called JSON-input-output interface. The same interface is provided by all distributions of the compiler.

The fields are generally subject to change, some are optional (as noted), but we try to only make backwards compatible
changes.

The compiler API expects a JSON formatted input and outputs the compilation result in a JSON formatted output. The
standard error output is not used and the process will always terminate in a “success” state, even if there were errors.
Errors are always reported as part of the JSON output.

The following subsections describe the format through an example. Comments are of course not permitted and used
here only for explanatory purposes.

**194 Chapter 3. Contents**


**Input Description**

#### {

```
// Required: Source code language. Currently supported are "Solidity", "Yul",
˓→"SolidityAST" (experimental), "EVMAssembly" (experimental).
"language": "Solidity",
// Required
"sources":
{
// The keys here are the "global" names of the source files,
// imports can use other files via remappings (see below).
"myFile.sol":
{
// Optional: keccak256 hash of the source file
// It is used to verify the retrieved content if imported via URLs.
"keccak256": "0x123...",
// Required (unless "content" is used, see below): URL(s) to the source file.
// URL(s) should be imported in this order and the result checked against the
// keccak256 hash (if available). If the hash doesn't match or none of the
// URL(s) result in success, an error should be raised.
// Using the commandline interface only filesystem paths are supported.
// With the JavaScript interface the URL will be passed to the user-supplied
// read callback, so any URL supported by the callback can be used.
"urls":
[
"bzzr://56ab...",
"ipfs://Qma...",
"/tmp/path/to/file.sol"
// If files are used, their directories should be added to the command-line via
// `--allow-paths <path>`.
]
},
"settable":
{
// Optional: keccak256 hash of the source file
"keccak256": "0x234...",
// Required (unless "urls" is used): literal contents of the source file
"content": "contract settable is owned { uint256 private x = 0; function␣
˓→set(uint256 _x) public { if (msg.sender == owner) x = _x; } }"
},
"myFile.sol_json.ast":
{
// If language is set to "SolidityAST", an AST needs to be supplied under the "ast
˓→" key
// and there can be only one source file present.
// The format is the same as used by the `ast`output.
// Note that importing ASTs is experimental and in particular that:
// - importing invalid ASTs can produce undefined results and
// - no proper error reporting is available on invalid ASTs.
// Furthermore, note that the AST import only consumes the fields of the AST as
// produced by the compiler in "stopAfter": "parsing" mode and then re-performs
// analysis, so any analysis-based annotations of the AST are ignored upon import.
"ast": { ... }
(continues on next page)
```
**3.13. Using the Compiler 195**


```
(continued from previous page)
},
"myFile_evm.json":
{
// If language is set to "EVMAssembly", an EVM Assembly JSON object needs to be␣
˓→supplied
// under the "assemblyJson" key and there can be only one source file present.
// The format is the same as used by the `evm.legacyAssembly` output or`--asm-json`
// output on the command line.
// Note that importing EVM assembly is experimental.
"assemblyJson":
{
".code": [ ... ],
".data": { ... },// optional
"sourceList": [ ... ]// optional (if no`source` node was defined in any`.code`␣
˓→object)
}
}
},
// Optional
"settings":
{
// Optional: Stop compilation after the given stage. Currently only "parsing" is␣
˓→valid here
"stopAfter": "parsing",
// Optional: Sorted list of remappings
"remappings": [ ":g=/dir" ],
// Optional: Optimizer settings
"optimizer": {
// Disabled by default.
// NOTE: enabled=false still leaves some optimizations on. See comments below.
// WARNING: Before version 0.8.6 omitting the 'enabled'key was not equivalent to␣
˓→setting
// it to false and would actually disable all the optimizations.
"enabled": true,
// Optimize for how many times you intend to run the code.
// Lower values will optimize more for initial deployment cost, higher
// values will optimize more for high-frequency usage.
"runs": 200,
// Switch optimizer components on or off in detail.
// The "enabled" switch above provides two defaults which can be
// tweaked here. If "details" is given, "enabled" can be omitted.
"details": {
// The peephole optimizer is always on if no details are given,
// use details to switch it off.
"peephole":true,
// The inliner is always off if no details are given,
// use details to switch it on.
"inliner":false,
// The unused jumpdest remover is always on if no details are given,
// use details to switch it off.
"jumpdestRemover":true,
// Sometimes re-orders literals in commutative operations.
(continues on next page)
```
**196 Chapter 3. Contents**


```
(continued from previous page)
"orderLiterals":false,
// Removes duplicate code blocks
"deduplicate":false,
// Common subexpression elimination, this is the most complicated step but
// can also provide the largest gain.
"cse":false,
// Optimize representation of literal numbers and strings in code.
"constantOptimizer":false,
// Use unchecked arithmetic when incrementing the counter of for loops
// under certain circumstances. It is always on if no details are given.
"simpleCounterForLoopUncheckedIncrement": true,
// The new Yul optimizer. Mostly operates on the code of ABI coder v2
// and inline assembly.
// It is activated together with the global optimizer setting
// and can be deactivated here.
// Before Solidity 0.6.0 it had to be activated through this switch.
"yul":false,
// Tuning options for the Yul optimizer.
"yulDetails": {
// Improve allocation of stack slots for variables, can free up stack slots␣
˓→early.
// Activated by default if the Yul optimizer is activated.
"stackAllocation": true,
// Select optimization steps to be applied. It is also possible to modify both␣
˓→the
// optimization sequence and the clean-up sequence. Instructions for each␣
˓→sequence
// are separated with the ":" delimiter and the values are provided in the␣
˓→form of
// optimization-sequence:clean-up-sequence. For more information see
// "The Optimizer > Selecting Optimizations".
// This field is optional, and if not provided, the default sequences for both
// optimization and clean-up are used. If only one of the sequences is provided
// the other will not be run.
// If only the delimiter ":" is provided then neither the optimization nor the␣
˓→clean-up
// sequence will be run.
// If set to an empty value, only the default clean-up sequence is used and
// no optimization steps are applied.
"optimizerSteps": "dhfoDgvulfnTUtnIf..."
}
}
},
// Version of the EVM to compile for.
// Affects type checking and code generation. Can be homestead,
// tangerineWhistle, spuriousDragon, byzantium, constantinople,
// petersburg, istanbul, berlin, london, paris, shanghai, cancun (default) or prague.
"evmVersion": "cancun",
// Optional: Change compilation pipeline to go through the Yul intermediate␣
˓→representation.
// This is false by default.
"viaIR":true,
(continues on next page)
```
**3.13. Using the Compiler 197**


```
(continued from previous page)
// Optional: Debugging settings
"debug": {
// How to treat revert (and require) reason strings. Settings are
// "default", "strip", "debug" and "verboseDebug".
// "default" does not inject compiler-generated revert strings and keeps user-
˓→supplied ones.
// "strip" removes all revert strings (if possible, i.e. if literals are used)␣
˓→keeping side-effects
// "debug" injects strings for compiler-generated internal reverts, implemented␣
˓→for ABI encoders V1 and V2 for now.
// "verboseDebug" even appends further information to user-supplied revert strings␣
˓→(not yet implemented)
"revertStrings": "default",
// Optional: How much extra debug information to include in comments in the␣
˓→produced EVM
// assembly and Yul code. Available components are:
// - `location`: Annotations of the form`@src <index>:<start>:<end>` indicating the
// location of the corresponding element in the original Solidity file, where:
// -`<index>` is the file index matching the`@use-src` annotation,
// -`<start>` is the index of the first byte at that location,
// -`<end>`is the index of the first byte after that location.
// - `snippet`: A single-line code snippet from the location indicated by`@src`.
// The snippet is quoted and follows the corresponding `@src` annotation.
// - `*`: Wildcard value that can be used to request everything.
"debugInfo": ["location", "snippet"]
},
// Metadata settings (optional)
"metadata": {
// The CBOR metadata is appended at the end of the bytecode by default.
// Setting this to false omits the metadata from the runtime and deploy time code.
"appendCBOR": true,
// Use only literal content and not URLs (false by default)
"useLiteralContent":true,
// Use the given hash method for the metadata hash that is appended to the␣
˓→bytecode.
// The metadata hash can be removed from the bytecode via option "none".
// The other options are "ipfs" and "bzzr1".
// If the option is omitted, "ipfs" is used by default.
"bytecodeHash": "ipfs"
},
// Addresses of the libraries. If not all libraries are given here,
// it can result in unlinked objects whose output data is different.
"libraries": {
// The top level key is the name of the source file where the library is used.
// If remappings are used, this source file should match the global path
// after remappings were applied.
// If this key is an empty string, that refers to a global level.
"myFile.sol": {
"MyLib": "0x123123..."
}
},
// The following can be used to select desired outputs based
(continues on next page)
```
**198 Chapter 3. Contents**


```
(continued from previous page)
// on file and contract names.
// If this field is omitted, then the compiler loads and does type checking,
// but will not generate any outputs apart from errors.
// The first level key is the file name and the second level key is the contract␣
˓→name.
// An empty contract name is used for outputs that are not tied to a contract
// but to the whole source file like the AST.
// A star as contract name refers to all contracts in the file.
// Similarly, a star as a file name matches all files.
// To select all outputs the compiler can possibly generate, with the exclusion of
// Yul intermediate representation outputs, use
// "outputSelection: { "*": { "*": [ "*" ], "": [ "*" ] } }"
// but note that this might slow down the compilation process needlessly.
//
// The available output types are as follows:
//
// File level (needs empty string as contract name):
// ast - AST of all source files
//
// Contract level (needs the contract name or "*"):
// abi - ABI
// devdoc - Developer documentation (natspec)
// userdoc - User documentation (natspec)
// metadata - Metadata
// ir - Yul intermediate representation of the code before optimization
// irAst - AST of Yul intermediate representation of the code before optimization
// irOptimized - Intermediate representation after optimization
// irOptimizedAst - AST of intermediate representation after optimization
// storageLayout - Slots, offsets and types of the contract's state variables in␣
˓→storage.
// transientStorageLayout - Slots, offsets and types of the contract's state␣
˓→variables in transient storage.
// evm.assembly - New assembly format
// evm.legacyAssembly - Old-style assembly format in JSON
// evm.bytecode.functionDebugData - Debugging information at function level
// evm.bytecode.object - Bytecode object
// evm.bytecode.opcodes - Opcodes list
// evm.bytecode.sourceMap - Source mapping (useful for debugging)
// evm.bytecode.linkReferences - Link references (if unlinked object)
// evm.bytecode.generatedSources - Sources generated by the compiler
// evm.deployedBytecode* - Deployed bytecode (has all the options that evm.
˓→bytecode has)
// evm.deployedBytecode.immutableReferences - Map from AST ids to bytecode ranges␣
˓→that reference immutables
// evm.methodIdentifiers - The list of function hashes
// evm.gasEstimates - Function gas estimates
//
// Note that using`evm`,`evm.bytecode`, etc. will select every
// target part of that output. Additionally,`*`can be used as a wildcard to request␣
˓→everything.
//
"outputSelection": {
(continues on next page)
```
**3.13. Using the Compiler 199**


```
(continued from previous page)
"*": {
"*": [
"metadata", "evm.bytecode" // Enable the metadata and bytecode outputs of␣
˓→every single contract.
, "evm.bytecode.sourceMap" // Enable the source map output of every single␣
˓→contract.
],
"": [
"ast" // Enable the AST output of every single file.
]
},
// Enable the abi and opcodes output of MyContract defined in file def.
"def": {
"MyContract": [ "abi", "evm.bytecode.opcodes" ]
}
},
// The modelChecker object is experimental and subject to changes.
"modelChecker":
{
// Chose which contracts should be analyzed as the deployed one.
"contracts":
{
"source1.sol": ["contract1"],
"source2.sol": ["contract2", "contract3"]
},
// Choose how division and modulo operations should be encoded.
// When using `false` they are replaced by multiplication with slack
// variables. This is the default.
// Using`true`here is recommended if you are using the CHC engine
// and not using Spacer as the Horn solver (using Eldarica, for example).
// See the Formal Verification section for a more detailed explanation of this␣
˓→option.
"divModNoSlacks": false,
// Choose which model checker engine to use: all (default), bmc, chc, none.
"engine": "chc",
// Choose whether external calls should be considered trusted in case the
// code of the called function is available at compile-time.
// For details see the SMTChecker section.
"extCalls": "trusted",
// Choose which types of invariants should be reported to the user: contract,␣
˓→reentrancy.
"invariants": ["contract", "reentrancy"],
// Choose whether to output all proved targets. The default is `false`.
"showProved": true,
// Choose whether to output all unproved targets. The default is`false`.
"showUnproved": true,
// Choose whether to output all unsupported language features. The default is␣
˓→`false`.
"showUnsupported": true,
// Choose which solvers should be used, if available.
// See the Formal Verification section for the solvers description.
"solvers": ["cvc5", "smtlib2", "z3"],
(continues on next page)
```
**200 Chapter 3. Contents**


(continued from previous page)
// Choose which targets should be checked: constantCondition,
// underflow, overflow, divByZero, balance, assert, popEmptyArray, outOfBounds.
// If the option is not given all targets are checked by default,
// except underflow/overflow for Solidity >=0.8.7.
// See the Formal Verification section for the targets description.
"targets": ["underflow", "overflow", "assert"],
// Timeout for each SMT query in milliseconds.
// If this option is not given, the SMTChecker will use a deterministic
// resource limit by default.
// A given timeout of 0 means no resource/time restrictions for any query.
"timeout": 20000
}
}
}

**Output Description**

#### {

```
// Optional: not present if no errors/warnings/infos were encountered
"errors": [
{
// Optional: Location within the source file.
"sourceLocation": {
"file": "sourceFile.sol",
"start": 0,
"end": 100
},
// Optional: Further locations (e.g. places of conflicting declarations)
"secondarySourceLocations": [
{
"file": "sourceFile.sol",
"start": 64,
"end": 92,
"message": "Other declaration is here:"
}
],
// Mandatory: Error type, such as "TypeError", "InternalCompilerError", "Exception
˓→", etc.
// See below for complete list of types.
"type": "TypeError",
// Mandatory: Component where the error originated, such as "general" etc.
"component": "general",
// Mandatory ("error", "warning" or "info", but please note that this may be␣
˓→extended in the future)
"severity": "error",
// Optional: unique code for the cause of the error
"errorCode": "3141",
// Mandatory
"message": "Invalid keyword",
// Optional: the message formatted with source location
(continues on next page)
```
**3.13. Using the Compiler 201**


```
(continued from previous page)
"formattedMessage": "sourceFile.sol:100: Invalid keyword"
}
],
// This contains the file-level outputs.
// It can be limited/filtered by the outputSelection settings.
"sources": {
"sourceFile.sol": {
// Identifier of the source (used in source maps)
"id": 1,
// The AST object
"ast": {}
}
},
// This contains the contract-level outputs.
// It can be limited/filtered by the outputSelection settings.
"contracts": {
"sourceFile.sol": {
// If the language used has no contract names, this field should equal to an empty␣
˓→string.
"ContractName": {
// The Ethereum Contract ABI. If empty, it is represented as an empty array.
// See https://docs.soliditylang.org/en/develop/abi-spec.html
"abi": [],
// See the Metadata Output documentation (serialised JSON string)
"metadata": "{/* ... */}",
// User documentation (natspec)
"userdoc": {},
// Developer documentation (natspec)
"devdoc": {},
// Intermediate representation before optimization (string)
"ir": "",
// AST of intermediate representation before optimization
"irAst": {/* ... */},
// Intermediate representation after optimization (string)
"irOptimized": "",
// AST of intermediate representation after optimization
"irOptimizedAst": {/* ... */},
// See the Storage Layout documentation.
"storageLayout": {"storage": [/* ... */], "types": {/* ... */} },
// See the Storage Layout documentation.
"transientStorageLayout": {"storage": [/* ... */], "types": {/* ... */} },
// EVM-related outputs
"evm": {
// Assembly (string)
"assembly": "",
// Old-style assembly (object)
"legacyAssembly": {},
// Bytecode and related details.
"bytecode": {
// Debugging data at the level of functions.
"functionDebugData": {
// Now follows a set of functions including compiler-internal and
(continues on next page)
```
**202 Chapter 3. Contents**


```
(continued from previous page)
// user-defined function. The set does not have to be complete.
"@mint_13": {// Internal name of the function
"entryPoint": 128,// Byte offset into the bytecode where the function␣
˓→starts (optional)
"id": 13,// AST ID of the function definition or null for compiler-
˓→internal functions (optional)
"parameterSlots": 2,// Number of EVM stack slots for the function␣
˓→parameters (optional)
"returnSlots": 1// Number of EVM stack slots for the return values␣
˓→(optional)
}
},
// The bytecode as a hex string.
"object": "00fe",
// Opcodes list (string)
"opcodes": "",
// The source mapping as a string. See the source mapping definition.
"sourceMap": "",
// Array of sources generated by the compiler. Currently only
// contains a single Yul file.
"generatedSources": [{
// Yul AST
"ast": {/* ... */},
// Source file in its text form (may contain comments)
"contents":"{ function abi_decode(start, end) -> data { data :=␣
˓→calldataload(start) } }",
// Source file ID, used for source references, same "namespace" as the␣
˓→Solidity source files
"id": 2,
"language": "Yul",
"name": "#utility.yul"
}],
// If given, this is an unlinked object.
"linkReferences": {
"libraryFile.sol": {
// Byte offsets into the bytecode.
// Linking replaces the 20 bytes located there.
"Library1": [
{ "start": 0, "length": 20 },
{ "start": 200, "length": 20 }
]
}
}
},
"deployedBytecode": {
/* ..., */ // The same layout as above.
"immutableReferences": {
// There are two references to the immutable with AST ID 3, both 32 bytes␣
˓→long. One is
// at bytecode offset 42, the other at bytecode offset 80.
"3": [{ "start": 42, "length": 32 }, { "start": 80, "length": 32 }]
}
(continues on next page)
```
**3.13. Using the Compiler 203**


(continued from previous page)
},
// The list of function hashes
"methodIdentifiers": {
"delegate(address)": "5c19a95c"
},
// Function gas estimates
"gasEstimates": {
"creation": {
"codeDepositCost": "420000",
"executionCost": "infinite",
"totalCost": "infinite"
},
"external": {
"delegate(address)": "25000"
},
"internal": {
"heavyLifting()": "infinite"
} } } } } } }

**Error Types**

1. JSONError: JSON input doesn’t conform to the required format, e.g. input is not a JSON object, the language
    is not supported, etc.
2. IOError: IO and import processing errors, such as unresolvable URL or hash mismatch in supplied sources.
3. ParserError: Source code doesn’t conform to the language rules.
4. DocstringParsingError: The NatSpec tags in the comment block cannot be parsed.
5. SyntaxError: Syntactical error, such ascontinueis used outside of aforloop.
6. DeclarationError: Invalid, unresolvable or clashing identifier names. e.g.Identifier not found
7. TypeError: Error within the type system, such as invalid type conversions, invalid assignments, etc.
8. UnimplementedFeatureError: Feature is not supported by the compiler, but is expected to be supported in
    future versions.
9. InternalCompilerError: Internal bug triggered in the compiler - this should be reported as an issue.
10. Exception: Unknown failure during compilation - this should be reported as an issue.
11. CompilerError: Invalid use of the compiler stack - this should be reported as an issue.
12. FatalError: Fatal error not processed correctly - this should be reported as an issue.
13. YulException: Error during Yul code generation - this should be reported as an issue.
14. Warning: A warning, which didn’t stop the compilation, but should be addressed if possible.

**204 Chapter 3. Contents**


15. Info: Information that the compiler thinks the user might find useful, but is not dangerous and does not neces-
    sarily need to be addressed.

### 3.14 Analysing the Compiler Output

It is often useful to look at the assembly code generated by the compiler. The generated binary, i.e., the output of
solc --bin contract.sol, is generally difficult to read. It is recommended to use the flag--asmto analyse the
assembly output. Even for large contracts, looking at a visual diff of the assembly before and after a change is often
very enlightening.

Consider the following contract (named, saycontract.sol):

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
contract C {
functionone()public purereturns(uint) {
return1;
}
}

The following would be the output ofsolc --asm contract.sol

======= contract.sol:C =======
EVM assembly:
/* "contract.sol":0:86 contract C {... */
mstore(0x40, 0x80)
callvalue
dup1
iszero
tag_1
jumpi
0x00
dup1
revert
tag_1:
pop
dataSize(sub_0)
dup1
dataOffset(sub_0)
0x00
codecopy
0x00
return
stop

sub_0: assembly {
/* "contract.sol":0:86 contract C {... */
mstore(0x40, 0x80)
callvalue
dup1
iszero
tag_1
(continues on next page)

**3.14. Analysing the Compiler Output 205**


```
(continued from previous page)
jumpi
0x00
dup1
revert
tag_1:
pop
jumpi(tag_2, lt(calldatasize, 0x04))
shr(0xe0, calldataload(0x00))
dup1
0x901717d1
eq
tag_3
jumpi
tag_2:
0x00
dup1
revert
/* "contract.sol":17:84 function one() public pure returns (uint) {... */
tag_3:
tag_4
tag_5
jump // in
tag_4:
mload(0x40)
tag_6
swap2
swap1
tag_7
jump // in
tag_6:
mload(0x40)
dup1
swap2
sub
swap1
return
tag_5:
/* "contract.sol":53:57 uint */
0x00
/* "contract.sol":76:77 1 */
0x01
/* "contract.sol":69:77 return 1 */
swap1
pop
/* "contract.sol":17:84 function one() public pure returns (uint) {... */
swap1
jump // out
/* "#utility.yul":7:125 */
tag_10:
/* "#utility.yul":94:118 */
tag_12
/* "#utility.yul":112:117 */
(continues on next page)
```
**206 Chapter 3. Contents**


```
(continued from previous page)
dup2
/* "#utility.yul":94:118 */
tag_13
jump // in
tag_12:
/* "#utility.yul":89:92 */
dup3
/* "#utility.yul":82:119 */
mstore
/* "#utility.yul":72:125 */
pop
pop
jump // out
/* "#utility.yul":131:353 */
tag_7:
0x00
/* "#utility.yul":262:264 */
0x20
/* "#utility.yul":251:260 */
dup3
/* "#utility.yul":247:265 */
add
/* "#utility.yul":239:265 */
swap1
pop
/* "#utility.yul":275:346 */
tag_15
/* "#utility.yul":343:344 */
0x00
/* "#utility.yul":332:341 */
dup4
/* "#utility.yul":328:345 */
add
/* "#utility.yul":319:325 */
dup5
/* "#utility.yul":275:346 */
tag_10
jump // in
tag_15:
/* "#utility.yul":229:353 */
swap3
swap2
pop
pop
jump // out
/* "#utility.yul":359:436 */
tag_13:
0x00
/* "#utility.yul":425:430 */
dup2
/* "#utility.yul":414:430 */
swap1
(continues on next page)
```
**3.14. Analysing the Compiler Output 207**


```
(continued from previous page)
pop
/* "#utility.yul":404:436 */
swap2
swap1
pop
jump // out
```
auxdata:␣
˓→0xa2646970667358221220a5874f19737ddd4c5d77ace1619e5160c67b3d4bedac75fce908fed32d98899864736f6c637827302e382e342d646576656c6f702e323032312e332e33302b636f6d6d69742e65613065363933380058
}

Alternatively, the above output can also be obtained from Remix, under the option “Compilation Details” after com-
piling a contract.

Notice that theasmoutput starts with the creation / constructor code. The deploy code is provided as part of the
sub object (in the above example, it is part of the sub-objectsub_0). Theauxdatafield corresponds to the contract
_metadata_. The comments in the assembly output point to the source location. Note that#utility.yulis an internally
generated file of utility functions that can be obtained using the flags--combined-json generated-sources,
generated-sources-runtime.

Similarly, the optimized assembly can be obtained with the command:solc --optimize --asm contract.sol.
Often times, it is interesting to see if two different sources in Solidity result in the same optimized code. For example,
to see if the expressions(a * b) / c,a * b / cgenerates the same bytecode. This can be easily done by taking a
diffof the corresponding assembly output, after potentially stripping comments that reference the source locations.

**Note:** The--asmoutput is not designed to be machine readable. Therefore, there may be breaking changes on the
output between minor versions of solc.

### 3.15 Solidity IR-based Codegen Changes

Solidity can generate EVM bytecode in two different ways: Either directly from Solidity to EVM opcodes (“old code-
gen”) or through an intermediate representation (“IR”) in Yul (“new codegen” or “IR-based codegen”).

The IR-based code generator was introduced with an aim to not only allow code generation to be more transparent and
auditable but also to enable more powerful optimization passes that span across functions.

You can enable it on the command-line using--via-iror with the option{"viaIR": true}in standard-json and
we encourage everyone to try it out!

For several reasons, there are tiny semantic differences between the old and the IR-based code generator, mostly in
areas where we would not expect people to rely on this behavior anyway. This section highlights the main differences
between the old and the IR-based codegen.

**208 Chapter 3. Contents**


**3.15.1 Semantic Only Changes**

This section lists the changes that are semantic-only, thus potentially hiding new and different behavior in existing code.

- The order of state variable initialization has changed in case of inheritance.
    The order used to be:
       **-** All state variables are zero-initialized at the beginning.
       **-** Evaluate base constructor arguments from most derived to most base contract.
       **-** Initialize all state variables in the whole inheritance hierarchy from most base to most derived.
       **-** Run the constructor, if present, for all contracts in the linearized hierarchy from most base to most derived.
    New order:
       **-** All state variables are zero-initialized at the beginning.
       **-** Evaluate base constructor arguments from most derived to most base contract.
       **-** For every contract in order from most base to most derived in the linearized hierarchy:
          1. Initialize state variables.
          2. Run the constructor (if present).
    This causes differences in contracts where the initial value of a state variable relies on the result of the constructor
    in another contract:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1;
```
```
contract A{
uintx;
constructor() {
x = 42;
}
functionf()publicview returns(uint256) {
returnx;
}
}
contract B isA {
uint publicy = f();
}
```
```
Previously,ywould be set to 0. This is due to the fact that we would first initialize state variables: First,xis set
to 0, and when initializingy,f()would return 0 causingyto be 0 as well. With the new rules,ywill be set to
```
42. We first initializexto 0, then call A’s constructor which setsxto 42. Finally, when initializingy,f()returns
42 causingyto be 42.
- When storage structs are deleted, every storage slot that contains a member of the struct is set to zero entirely.
Formerly, padding space was left untouched. Consequently, if the padding space within a struct is used to store
data (e.g. in the context of a contract upgrade), you have to be aware thatdeletewill now also clear the added
member (while it wouldn’t have been cleared in the past).

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1;
```
```
(continues on next page)
```
**3.15. Solidity IR-based Codegen Changes 209**


```
(continued from previous page)
contract C{
structS {
uint64y;
uint64z;
}
S s;
functionf()public{
// ...
delete s;
// s occupies only first 16 bytes of the 32 bytes slot
// delete will write zero to the full slot
}
}
```
```
We have the same behavior for implicit delete, for example when array of structs is shortened.
```
- Function modifiers are implemented in a slightly different way regarding function parameters and return vari-
    ables. This especially has an effect if the placeholder_;is evaluated multiple times in a modifier. In the old code
    generator, each function parameter and return variable has a fixed slot on the stack. If the function is run multiple
    times because_;is used multiple times or used in a loop, then a change to the function parameter’s or return
    variable’s value is visible in the next execution of the function. The new code generator implements modifiers
    using actual functions and passes function parameters on. This means that multiple evaluations of a function’s
    body will get the same values for the parameters, and the effect on return variables is that they are reset to their
    default (zero) value for each execution.

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0;
contract C{
functionf(uint a)public pure mod()returns(uint r) {
r = a++;
}
modifiermod() { _; _; }
}
```
```
If you executef(0)in the old code generator, it will return 1 , while it will return 0 when using the new code
generator.
```
```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.1<0.9.0;
```
```
contract C{
boolactive =true;
modifiermod()
{
_;
active =false;
_;
}
functionfoo()externalmod() returns(uintret)
{
if (active)
ret = 1;// Same as``return 1``
}
(continues on next page)
```
**210 Chapter 3. Contents**


```
(continued from previous page)
}
```
```
The functionC.foo()returns the following values:
```
**-** Old code generator: 1 as the return variable is initialized to 0 only once before the first_;evaluation and
    then overwritten by thereturn 1;. It is not initialized again for the second_;evaluation andfoo()does
    not explicitly assign it either (due toactive == false), thus it keeps its first value.
**-** New code generator: 0 as all parameters, including return parameters, will be re-initialized before each_;
    evaluation.
- For the old code generator, the evaluation order of expressions is unspecified. For the new code generator, we
try to evaluate in source order (left to right), but do not guarantee it. This can lead to semantic differences.
For example:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C{
functionpreincr_u8(uint8 a) publicpurereturns(uint8) {
return++a + a;
}
}
```
```
The functionpreincr_u8(1)returns the following values:
```
**-** Old code generator: 3 (1 + 2) but the return value is unspecified in general
**-** New code generator: 4 (2 + 2) but the return value is not guaranteed
On the other hand, function argument expressions are evaluated in the same order by both code generators with
the exception of the global functionsaddmodandmulmod. For example:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C{
functionadd(uint8a, uint8b) public purereturns(uint8) {
returna + b;
}
functiong(uint8 a,uint8 b) publicpurereturns(uint8) {
returnadd(++a + ++b, a + b);
}
}
```
```
The functiong(1, 2)returns the following values:
```
**-** Old code generator: 10 (add(2 + 3, 2 + 3)) but the return value is unspecified in general
**-** New code generator: 10 but the return value is not guaranteed
The arguments to the global functionsaddmodandmulmodare evaluated right-to-left by the old code generator
and left-to-right by the new code generator. For example:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C{
functionf()publicpure returns(uint256aMod,uint256mMod) {
(continues on next page)
```
**3.15. Solidity IR-based Codegen Changes 211**


```
(continued from previous page)
uint256x = 3;
// Old code gen: add/mulmod(5, 4, 3)
// New code gen: add/mulmod(4, 5, 5)
aMod = addmod(++x, ++x, x);
mMod = mulmod(++x, ++x, x);
}
}
```
```
The functionf()returns the following values:
```
**-** Old code generator:aMod = 0andmMod = 2
**-** New code generator:aMod = 4andmMod = 0
- The new code generator imposes a hard limit oftype(uint64).max(0xffffffffffffffff) for the free mem-
ory pointer. Allocations that would increase its value beyond this limit revert. The old code generator does not
have this limit.
For example:

```
// SPDX-License-Identifier: GPL-3.0
pragma solidity > 0. 8. 0 ;
contract C{
functionf()public{
uint[]memory arr;
// allocation size: 576460752303423481
// assumes freeMemPtr points to 0x80 initially
uintsolYulMaxAllocationBeforeMemPtrOverflow = (type(uint64).max - 0x80 -␣
˓→31) / 32;
// freeMemPtr overflows UINT64_MAX
arr =new uint[](solYulMaxAllocationBeforeMemPtrOverflow);
}
}
```
```
The functionf()behaves as follows:
```
**-** Old code generator: runs out of gas while zeroing the array contents after the large memory allocation
**-** New code generator: reverts due to free memory pointer overflow (does not run out of gas)

**3.15.2 Internals**

**Internal function pointers**

The old code generator uses code offsets or tags for values of internal function pointers. This is especially complicated
since these offsets are different at construction time and after deployment and the values can cross this border via
storage. Because of that, both offsets are encoded at construction time into the same value (into different bytes).

In the new code generator, function pointers use internal IDs that are allocated in sequence. Since calls via jumps
are not possible, calls through function pointers always have to use an internal dispatch function that uses theswitch
statement to select the right function.

The ID 0 is reserved for uninitialized function pointers which then cause a panic in the dispatch function when called.

In the old code generator, internal function pointers are initialized with a special function that always causes a panic.
This causes a storage write at construction time for internal function pointers in storage.

**212 Chapter 3. Contents**


**Cleanup**

The old code generator only performs cleanup before an operation whose result could be affected by the values of the
dirty bits. The new code generator performs cleanup after any operation that can result in dirty bits. The hope is that
the optimizer will be powerful enough to eliminate redundant cleanup operations.

For example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.1;
contract C {
functionf(uint8 a) publicpurereturns(uint r1,uint r2)
{
a = ~a;
assembly {
r1 := a
}
r2 = a;
}
}

The functionf(1)returns the following values:

- Old code generator: (fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffe,
    00000000000000000000000000000000000000000000000000000000000000fe)
- New code generator: (00000000000000000000000000000000000000000000000000000000000000fe,
    00000000000000000000000000000000000000000000000000000000000000fe)

Note that, unlike the new code generator, the old code generator does not perform a cleanup after the bit-not assignment
(a = ~a). This results in different values being assigned (within the inline assembly block) to return valuer1between
the old and new code generators. However, both code generators perform a cleanup before the new value ofais assigned
tor2.

### 3.16 Layout of State Variables in Storage and Transient Storage

**Note:** The rules described in this section apply for both storage and transient storage data locations. The layouts are
completely independent and don’t interfere with each other’s variable locations. Thus storage and transient storage
state variables can be safely interleaved without any side effects. Only value types are supported for transient storage.

State variables of contracts are stored in storage in a compact way such that multiple values sometimes use the same
storage slot. Except for dynamically-sized arrays and mappings (see below), data is stored contiguously item after item
starting with the first state variable, which is stored in slot 0. For each variable, a size in bytes is determined according
to its type. Multiple, contiguous items that need less than 32 bytes are packed into a single storage slot if possible,
according to the following rules:

- The first item in a storage slot is stored lower-order aligned.
- Value types use only as many bytes as are necessary to store them.
- If a value type does not fit the remaining part of a storage slot, it is stored in the next storage slot.
- Structs and array data always start a new slot and their items are packed tightly according to these rules.
- Items following struct or array data always start a new storage slot.

**3.16. Layout of State Variables in Storage and Transient Storage 213**


For contracts that use inheritance, the ordering of state variables is determined by the C3-linearized order of contracts
starting with the most base-ward contract. If allowed by the above rules, state variables from different contracts do
share the same storage slot.

The elements of structs and arrays are stored after each other, just as if they were given as individual values.

```
Warning: When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher. This is
because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use
more operations in order to reduce the size of the element from 32 bytes to the desired size.
It might be beneficial to use reduced-size types if you are dealing with storage values because the compiler will
pack multiple elements into one storage slot, and thus, combine multiple reads or writes into a single operation. If
you are not reading or writing all the values in a slot at the same time, this can have the opposite effect, though:
When one value is written to a multi-value storage slot, the storage slot has to be read first and then combined with
the new value such that other data in the same slot is not destroyed.
When dealing with function arguments or memory values, there is no inherent benefit because the compiler does
not pack these values.
Finally, in order to allow the EVM to optimize for this, ensure that you try to order your storage variables and
structmembers such that they can be packed tightly. For example, declaring your storage variables in the order of
uint128, uint128, uint256instead ofuint128, uint256, uint128, as the former will only take up two
slots of storage whereas the latter will take up three.
```
**Note:** The layout of state variables in storage is considered to be part of the external interface of Solidity due to the
fact that storage pointers can be passed to libraries. This means that any change to the rules outlined in this section is
considered a breaking change of the language and due to its critical nature should be considered very carefully before
being executed. In the event of such a breaking change, we would want to release a compatibility mode in which the
compiler would generate bytecode supporting the old layout.

**3.16.1 Mappings and Dynamic Arrays**

Due to their unpredictable size, mappings and dynamically-sized array types cannot be stored “in between” the state
variables preceding and following them. Instead, they are considered to occupy only 32 bytes with regards to the _rules
above_ and the elements they contain are stored starting at a different storage slot that is computed using a Keccak-256
hash.

Assume the storage location of the mapping or array ends up being a slotpafter applying _the storage layout rules_.
For dynamic arrays, this slot stores the number of elements in the array (byte arrays and strings are an exception, see
_below_ ). For mappings, the slot stays empty, but it is still needed to ensure that even if there are two mappings next to
each other, their content ends up at different storage locations.

Array data is located starting atkeccak256(p)and it is laid out in the same way as statically-sized array data would:
One element after the other, potentially sharing storage slots if the elements are not longer than 16 bytes. Dynamic arrays
of dynamic arrays apply this rule recursively. The location of elementx[i][j], where the type ofxisuint24[][],
is computed as follows (again, assumingxitself is stored at slotp): The slot iskeccak256(keccak256(p) +
i) + floor(j / floor(256 / 24))and the element can be obtained from the slot datavusing(v >> ((j %
floor(256 / 24)) * 24)) & type(uint24).max.

The value corresponding to a mapping keykis located atkeccak256(h(k). p)where.is concatenation andhis
a function that is applied to the key depending on its type:

- for value types,hpads the value to 32 bytes in the same way as when storing the value in memory.

**214 Chapter 3. Contents**


- for strings and byte arrays,h(k)is just the unpadded data.

If the mapping value is a non-value type, the computed slot marks the start of the data. If the value is of struct type, for
example, you have to add an offset corresponding to the struct member to reach the member.

As an example, consider the following contract:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract C {
struct S {uint16 a; uint16b; uint256c; }
uintx;
mapping(uint=> mapping(uint => S)) data;
}

Let us compute the storage location ofdata[4][9].c. The position of the mapping itself is 1 (the variablex
with 32 bytes precedes it). This meansdata[4]is stored atkeccak256(uint256(4). uint256(1)). The
type of data[4]is again a mapping and the data fordata[4][9]starts at slot keccak256(uint256(9).
keccak256(uint256(4). uint256(1))). The slot offset of the membercinside the structSis 1 because
aand bare packed in a single slot. This means the slot fordata[4][9].ciskeccak256(uint256(9).
keccak256(uint256(4). uint256(1))) + 1. The type of the value isuint256, so it uses a single slot.

bytes **and** string

bytesandstringare encoded identically. In general, the encoding is similar tobytes1[], in the sense that there is
a slot for the array itself and a data area that is computed using akeccak256hash of that slot’s position. However, for
short values (shorter than 32 bytes) the array elements are stored together with the length in the same slot.

In particular: if the data is at most 31 bytes long, the elements are stored in the higher-order bytes (left aligned) and
the lowest-order byte stores the valuelength * 2. For byte arrays that store data which is 32 or more bytes long,
the main slotpstoreslength * 2 + 1and the data is stored as usual inkeccak256(p). This means that you can
distinguish a short array from a long array by checking if the lowest bit is set: short (not set) and long (set).

**Note:** Handling invalidly encoded slots is currently not supported but may be added in the future. If you are compiling
via IR, reading an invalidly encoded slot results in aPanic(0x22)error.

**3.16.2 JSON Output**

The storage layout of a contract can be requested via the _standard JSON interface_. The output is a JSON object
containing two keys,storageandtypes. Thestorageobject is an array where each element has the following form:

{
"astId": 2,
"contract": "fileA:A",
"label": "x",
"offset": 0,
"slot": "0",
"type": "t_uint256"
}

The example above is the storage layout ofcontract A { uint x; }from source unitfileAand

**3.16. Layout of State Variables in Storage and Transient Storage 215**


- astIdis the id of the AST node of the state variable’s declaration
- contractis the name of the contract including its path as prefix
- labelis the name of the state variable
- offsetis the offset in bytes within the storage slot according to the encoding
- slotis the storage slot where the state variable resides or starts. This number may be very large and therefore
    its JSON value is represented as a string.
- typeis an identifier used as key to the variable’s type information (described in the following)

The giventype, in this caset_uint256represents an element intypes, which has the form:

{
"encoding": "inplace",
"label": "uint256",
"numberOfBytes": "32",
}

where

- encodinghow the data is encoded in storage, where the possible values are:
    **-** inplace: data is laid out contiguously in storage (see _above_ ).
    **-** mapping: Keccak-256 hash-based method (see _above_ ).
    **-** dynamic_array: Keccak-256 hash-based method (see _above_ ).
    **-** bytes: single slot or Keccak-256 hash-based depending on the data size (see _above_ ).
- labelis the canonical type name.
- numberOfBytesis the number of used bytes (as a decimal string). Note that ifnumberOfBytes > 32this
    means that more than one slot is used.

Some types have extra information besides the four above. Mappings contain itskeyandvaluetypes (again referencing
an entry in this mapping of types), arrays have itsbasetype, and structs list theirmembersin the same format as the
top-levelstorage(see _above_ ).

**Note:** The JSON output format of a contract’s storage layout is still considered experimental and is subject to change
in non-breaking releases of Solidity.

The following example shows a contract and its storage layout, containing value and reference types, types that are
encoded packed, and nested types.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;
contract A {
struct S {
uint128a;
uint128b;
uint[2] staticArray;
uint[] dynArray;
}

```
uintx;
(continues on next page)
```
**216 Chapter 3. Contents**


(continued from previous page)
uinty;
S s;
addressaddr;
mapping(uint=> mapping(address=> bool)) map;
uint[] array;
string s1;
bytesb1;
}

#### {

```
"storage": [
{
"astId": 15,
"contract": "fileA:A",
"label": "x",
"offset": 0,
"slot": "0",
"type": "t_uint256"
},
{
"astId": 17,
"contract": "fileA:A",
"label": "y",
"offset": 0,
"slot": "1",
"type": "t_uint256"
},
{
"astId": 20,
"contract": "fileA:A",
"label": "s",
"offset": 0,
"slot": "2",
"type": "t_struct(S)13_storage"
},
{
"astId": 22,
"contract": "fileA:A",
"label": "addr",
"offset": 0,
"slot": "6",
"type": "t_address"
},
{
"astId": 28,
"contract": "fileA:A",
"label": "map",
"offset": 0,
"slot": "7",
"type": "t_mapping(t_uint256,t_mapping(t_address,t_bool))"
},
{
(continues on next page)
```
**3.16. Layout of State Variables in Storage and Transient Storage 217**


```
(continued from previous page)
"astId": 31,
"contract": "fileA:A",
"label": "array",
"offset": 0,
"slot": "8",
"type": "t_array(t_uint256)dyn_storage"
},
{
"astId": 33,
"contract": "fileA:A",
"label": "s1",
"offset": 0,
"slot": "9",
"type": "t_string_storage"
},
{
"astId": 35,
"contract": "fileA:A",
"label": "b1",
"offset": 0,
"slot": "10",
"type": "t_bytes_storage"
}
],
"types": {
"t_address": {
"encoding": "inplace",
"label": "address",
"numberOfBytes": "20"
},
"t_array(t_uint256)2_storage": {
"base": "t_uint256",
"encoding": "inplace",
"label": "uint256[2]",
"numberOfBytes": "64"
},
"t_array(t_uint256)dyn_storage": {
"base": "t_uint256",
"encoding": "dynamic_array",
"label": "uint256[]",
"numberOfBytes": "32"
},
"t_bool": {
"encoding": "inplace",
"label": "bool",
"numberOfBytes": "1"
},
"t_bytes_storage": {
"encoding": "bytes",
"label": "bytes",
"numberOfBytes": "32"
},
(continues on next page)
```
**218 Chapter 3. Contents**


```
(continued from previous page)
"t_mapping(t_address,t_bool)": {
"encoding": "mapping",
"key": "t_address",
"label": "mapping(address => bool)",
"numberOfBytes": "32",
"value": "t_bool"
},
"t_mapping(t_uint256,t_mapping(t_address,t_bool))": {
"encoding": "mapping",
"key": "t_uint256",
"label": "mapping(uint256 => mapping(address => bool))",
"numberOfBytes": "32",
"value": "t_mapping(t_address,t_bool)"
},
"t_string_storage": {
"encoding": "bytes",
"label": "string",
"numberOfBytes": "32"
},
"t_struct(S)13_storage": {
"encoding": "inplace",
"label": "struct A.S",
"members": [
{
"astId": 3,
"contract": "fileA:A",
"label": "a",
"offset": 0,
"slot": "0",
"type": "t_uint128"
},
{
"astId": 5,
"contract": "fileA:A",
"label": "b",
"offset": 16,
"slot": "0",
"type": "t_uint128"
},
{
"astId": 9,
"contract": "fileA:A",
"label": "staticArray",
"offset": 0,
"slot": "1",
"type": "t_array(t_uint256)2_storage"
},
{
"astId": 12,
"contract": "fileA:A",
"label": "dynArray",
"offset": 0,
(continues on next page)
```
**3.16. Layout of State Variables in Storage and Transient Storage 219**


(continued from previous page)
"slot": "3",
"type": "t_array(t_uint256)dyn_storage"
}
],
"numberOfBytes": "128"
},
"t_uint128": {
"encoding": "inplace",
"label": "uint128",
"numberOfBytes": "16"
},
"t_uint256": {
"encoding": "inplace",
"label": "uint256",
"numberOfBytes": "32"
}
}
}

### 3.17 Layout in Memory

Solidity reserves four 32-byte slots, with specific byte ranges (inclusive of endpoints) being used as follows:

- 0x00-0x3f(64 bytes): scratch space for hashing methods
- 0x40-0x5f(32 bytes): currently allocated memory size (aka. free memory pointer)
- 0x60-0x7f(32 bytes): zero slot

Scratch space can be used between statements (i.e. within inline assembly). The zero slot is used as initial value for
dynamic memory arrays and should never be written to (the free memory pointer points to0x80initially).

Solidity always places new objects at the free memory pointer and memory is never freed (this might change in the
future).

Elements in memory arrays in Solidity always occupy multiples of 32 bytes (this is even true forbytes1[], but not for
bytesandstring). Multi-dimensional memory arrays are pointers to memory arrays. The length of a dynamic array
is stored at the first slot of the array and followed by the array elements.

```
Warning: There are some operations in Solidity that need a temporary memory area larger than 64 bytes and
therefore will not fit into the scratch space. They will be placed where the free memory points to, but given their
short lifetime, the pointer is not updated. The memory may or may not be zeroed out. Because of this, one should
not expect the free memory to point to zeroed out memory.
While it may seem like a good idea to usemsizeto arrive at a definitely zeroed out memory area, using such a
pointer non-temporarily without updating the free memory pointer can have unexpected results.
```
**220 Chapter 3. Contents**


**3.17.1 Differences to Layout in Storage**

As described above the layout in memory is different from the layout in _storage_. Below there are some examples.

**Example for Difference in Arrays**

The following array occupies 32 bytes (1 slot) in storage, but 128 bytes (4 items with 32 bytes each) in memory.

uint8[4] a;

**Example for Difference in Struct Layout**

The following struct occupies 96 bytes (3 slots of 32 bytes) in storage, but 128 bytes (4 items with 32 bytes each) in
memory.

struct S {
uinta;
uintb;
uint8c;
uint8d;
}

### 3.18 Layout of Call Data

The input data for a function call is assumed to be in the format defined by the _ABI specification_. Among others, the
ABI specification requires arguments to be padded to multiples of 32 bytes. The internal function calls use a different
convention.

Arguments for the constructor of a contract are directly appended at the end of the contract’s code, also in ABI encoding.
The constructor will access them through a hard-coded offset, and not by using thecodesizeopcode, since this of
course changes when appending data to the code.

### 3.19 Cleaning Up Variables

Ultimately, all values in the EVM are stored in 256 bit words. Thus, in some cases, when the type of a value has
less than 256 bits, it is necessary to clean the remaining bits. The Solidity compiler is designed to do such cleaning
before any operations that might be adversely affected by the potential garbage in the remaining bits. For example,
before writing a value to memory, the remaining bits need to be cleared because the memory contents can be used for
computing hashes or sent as the data of a message call. Similarly, before storing a value in the storage, the remaining
bits need to be cleaned because otherwise the garbled value can be observed.

Note that access via inline assembly is not considered such an operation: If you use inline assembly to access Solidity
variables shorter than 256 bits, the compiler does not guarantee that the value is properly cleaned up.

Moreover, we do not clean the bits if the immediately following operation is not affected. For instance, since any non-
zero value is consideredtruebyJUMPIinstruction, we do not clean the boolean values before they are used as the
condition forJUMPI.

In addition to the design principle above, the Solidity compiler cleans input data when it is loaded onto the stack.

**3.18. Layout of Call Data 221**


The following table describes the cleaning rules applied to different types, wherehigher bitsrefers to the remaining
bits in case the type has less than 256 bits.

```
Type Valid Values Cleanup of Invalid Values
enum of n
members
```
```
0 until n - 1 throws exception
```
```
bool 0 or 1 results in 1
signed inte-
gers
```
```
higher bits set to
the sign bit
```
```
currently silently signextends to a valid value, i.e. all higher bits are set to the
sign bit; may throw an exception in the future
unsigned in-
tegers
```
```
higher bits zeroed currently silently masks to a valid value, i.e. all higher bits are set to zero; may
throw an exception in the future
```
Note that valid and invalid values are dependent on their type size. Consideruint8, the unsigned 8-bit type, which
has the following valid values:

0000...0000 0000 0000
0000...0000 0000 0001
0000...0000 0000 0010
....
0000...0000 1111 1111

Any invalid value will have the higher bits set to zero:

0101...1101 0010 1010 invalid value
0000...0000 0010 1010 cleaned value

Forint8, the signed 8-bit type, the valid values are:

Negative

1111...1111 1111 1111
1111...1111 1111 1110
....
1111...1111 1000 0000

Positive

0000...0000 0000 0000
0000...0000 0000 0001
0000...0000 0000 0010
....
0000...0000 1111 1111

The compiler willsignextendthe sign bit, which is 1 for negative and 0 for positive values, overwriting the higher
bits:

Negative

0010...1010 1111 1111 invalid value
1111...1111 1111 1111 cleaned value

Positive

1101...0101 0000 0100 invalid value
0000...0000 0000 0100 cleaned value

**222 Chapter 3. Contents**


### 3.20 Source Mappings

As part of the AST output, the compiler provides the range of the source code that is represented by the respective node
in the AST. This can be used for various purposes ranging from static analysis tools that report errors based on the AST
and debugging tools that highlight local variables and their uses.

Furthermore, the compiler can also generate a mapping from the bytecode to the range in the source code that generated
the instruction. This is again important for static analysis tools that operate on bytecode level and for displaying the
current position in the source code inside a debugger or for breakpoint handling. This mapping also contains other
information, like the jump type and the modifier depth (see below).

Both kinds of source mappings use integer identifiers to refer to source files. The identifier of a source file is stored
inoutput['sources'][sourceName]['id']whereoutputis the output of the standard-json compiler interface
parsed as JSON. For some utility routines, the compiler generates “internal” source files that are not part of the original
input but are referenced from the source mappings. These source files together with their identifiers can be obtained
viaoutput['contracts'][sourceName][contractName]['evm']['bytecode']['generatedSources'].

**Note:** In the case of instructions that are not associated with any particular source file, the source mapping assigns
an integer identifier of-1. This may happen for bytecode sections stemming from compiler-generated inline assembly
statements.

The source mappings inside the AST use the following notation:

s:l:f

Wheresis the byte-offset to the start of the range in the source file,lis the length of the source range in bytes andf
is the source index mentioned above.

The encoding in the source mapping for the bytecode is more complicated: It is a list ofs:l:f:j:mseparated by;.
Each of these elements corresponds to an instruction, i.e. you cannot use the byte offset but have to use the instruction
offset (push instructions are longer than a single byte). The fieldss,landfare as above.jcan be eitheri,oor-
signifying whether a jump instruction goes into a function, returns from a function or is a regular jump as part of e.g. a
loop. The last field,m, is an integer that denotes the “modifier depth”. This depth is increased whenever the placeholder
statement (_) is entered in a modifier and decreased when it is left again. This allows debuggers to track tricky cases
like the same modifier being used twice or multiple placeholder statements being used in a single modifier.

In order to compress these source mappings especially for bytecode, the following rules are used:

- If a field is empty, the value of the preceding element is used.
- If a:is missing, all following fields are considered empty.

This means the following source mappings represent the same information:

1:2:1;1:9:1;2:1:2;2:1:2;2:1:2

1:2:1;:9;2:1:2;;

Important to note is that when the _verbatim_ builtin is used, the source mappings will be invalid: The builtin is considered
a single instruction instead of potentially multiple.

**3.20. Source Mappings 223**


### 3.21 The Optimizer

The Solidity compiler involves optimizations at three different levels (in order of execution):

- Optimizations during code generation based on a direct analysis of Solidity code.
- Optimizing transformations on the Yul IR code.
- Optimizations at the opcode level.

The opcode-based optimizer applies a set of simplification rules to opcodes. It also combines equal code sets and
removes unused code.

The Yul-based optimizer is much more powerful, because it can work across function calls. For example, arbitrary
jumps are not possible in Yul, so it is possible to compute the side-effects of each function. Consider two function
calls, where the first does not modify storage and the second does modify storage. If their arguments and return values
do not depend on each other, we can reorder the function calls. Similarly, if a function is side-effect free and its result
is multiplied by zero, you can remove the function call completely.

The codegen-based optimizer affects the initial low-level code produced from the Solidity input. In the legacy pipeline,
the bytecode is generated immediately and most of the optimizations of this kind are implicit and not configurable, the
only exception being an optimization which changes the order of literals in binary operations. The IR-based pipeline
takes a different approach and produces Yul IR closely matching the structure of the Solidity code, with nearly all
optimizations deferred to the Yul optimizer module. In that case codegen-level optimization is done only in very limited
cases which are difficult to handle in Yul IR, but are straightforward with the high-level information from analysis phase
at hand. An example of such an optimization is the bypass of checked arithmetic when incrementing the counter in
certain idiomaticforloops.

Currently, the parameter--optimizeactivates the opcode-based optimizer for the generated bytecode and the Yul
optimizer for the Yul code generated internally, for example for ABI coder v2. One can usesolc --ir-optimized
--optimizeto produce an optimized Yul IR for a Solidity source. Similarly, one can usesolc --strict-assembly
--optimizefor a stand-alone Yul mode.

**Note:** Some optimizer steps, such as, for example, the peephole optimizer and the _unchecked loop increment optimizer_
are always enabled by default and can only be turned off via the _Standard JSON_.

**Note:** An empty optimizer sequence, i.e:, is accepted even without--optimizein order to fully disable the user-
supplied portion of the Yul _optimizer sequence_ , as by default, even when the optimizer is not turned on, the _unused
pruner_ step will be run.

You can find more details on both optimizer modules and their optimization steps below.

**3.21.1 Benefits of Optimizing Solidity Code**

Overall, the optimizer tries to simplify complicated expressions, which reduces both code size and execution cost, i.e.,
it can reduce gas needed for contract deployment as well as for external calls made to the contract. It also specializes
or inlines functions. Especially function inlining is an operation that can cause much bigger code, but it is often done
because it results in opportunities for more simplifications.

**224 Chapter 3. Contents**


**3.21.2 Differences between Optimized and Non-Optimized Code**

Generally, the most visible difference is that constant expressions are evaluated at compile time. When it comes to
the ASM output, one can also notice a reduction of equivalent or duplicate code blocks (compare the output of the
flags--asmand--asm --optimize). However, when it comes to the Yul/intermediate-representation, there can be
significant differences, for example, functions may be inlined, combined, or rewritten to eliminate redundancies, etc.
(compare the output between the flags--irand--optimize --ir-optimized).

**3.21.3 Optimizer Parameter Runs**

The number of runs (--optimize-runs) specifies roughly how often each opcode of the deployed code will be exe-
cuted across the life-time of the contract. This means it is a trade-off parameter between code size (deploy cost) and
code execution cost (cost after deployment). A “runs” parameter of “1” will produce short but expensive code. In con-
trast, a larger “runs” parameter will produce longer but more gas efficient code. The maximum value of the parameter
is2**32-1.

**Note:** A common misconception is that this parameter specifies the number of iterations of the optimizer. This is not
true: The optimizer will always run as many times as it can still improve the code.

**3.21.4 Opcode-Based Optimizer Module**

The opcode-based optimizer module operates on assembly code. It splits the sequence of instructions into basic blocks
atJUMPsandJUMPDESTs. Inside these blocks, the optimizer analyzes the instructions and records every modification
to the stack, memory, or storage as an expression which consists of an instruction and a list of arguments which are
pointers to other expressions.

Additionally, the opcode-based optimizer uses a component called “CommonSubexpressionEliminator” that, amongst
other tasks, finds expressions that are always equal (on every input) and combines them into an expression class. It
first tries to find each new expression in a list of already known expressions. If no such matches are found, it simplifies
the expression according to rules likeconstant + constant = sum_of_constantsorX * 1 = X. Since this is a
recursive process, we can also apply the latter rule if the second factor is a more complex expression which we know
always evaluates to one.

Certain optimizer steps symbolically track the storage and memory locations. For example, this information is used to
compute Keccak-256 hashes that can be evaluated during compile time. Consider the sequence:

PUSH 32
PUSH 0
CALLDATALOAD
PUSH 100
DUP2
MSTORE
KECCAK256

or the equivalent Yul

letx := calldataload(0)
mstore(x, 100)
letvalue := keccak256(x, 32)

In this case, the optimizer tracks the value at a memory locationcalldataload(0)and then realizes that the Keccak-
256 hash can be evaluated at compile time. This only works if there is no other instruction that modifies memory

**3.21. The Optimizer 225**


between themstoreandkeccak256. So if there is an instruction that writes to memory (or storage), then we need to
erase the knowledge of the current memory (or storage). There is, however, an exception to this erasing, when we can
easily see that the instruction doesn’t write to a certain location.

For example,

letx := calldataload(0)
mstore(x, 100)
// Current knowledge memory location x -> 100
lety := add(x, 32)
// Does not clear the knowledge that x -> 100, since y does not write to [x, x + 32)
mstore(y, 200)
// This Keccak-256 can now be evaluated
letvalue := keccak256(x, 32)

Therefore, modifications to storage and memory locations, of say locationl, must erase knowledge about storage or
memory locations which may be equal tol. More specifically, for storage, the optimizer has to erase all knowledge
of symbolic locations, that may be equal toland for memory, the optimizer has to erase all knowledge of symbolic
locations that may not be at least 32 bytes away. Ifmdenotes an arbitrary location, then this decision on erasure is done
by computing the valuesub(l, m). For storage, if this value evaluates to a literal that is non-zero, then the knowledge
aboutmwill be kept. For memory, if the value evaluates to a literal that is between 32 and2**256 - 32, then the
knowledge aboutmwill be kept. In all other cases, the knowledge aboutmwill be erased.

After this process, we know which expressions have to be on the stack at the end, and have a list of modifications to
memory and storage. This information is stored together with the basic blocks and is used to link them. Furthermore,
knowledge about the stack, storage and memory configuration is forwarded to the next block(s).

If we know the targets of allJUMPandJUMPIinstructions, we can build a complete control flow graph of the program. If
there is only one target we do not know (this can happen as in principle, jump targets can be computed from inputs), we
have to erase all knowledge about the input state of a block as it can be the target of the unknownJUMP. If the opcode-
based optimizer module finds aJUMPIwhose condition evaluates to a constant, it transforms it to an unconditional
jump.

As the last step, the code in each block is re-generated. The optimizer creates a dependency graph from the expressions
on the stack at the end of the block, and it drops every operation that is not part of this graph. It generates code
that applies the modifications to memory and storage in the order they were made in the original code (dropping
modifications which were found not to be needed). Finally, it generates all values that are required to be on the stack
in the correct place.

These steps are applied to each basic block and the newly generated code is used as replacement if it is smaller. If a
basic block is split at aJUMPIand during the analysis, the condition evaluates to a constant, theJUMPIis replaced
based on the value of the constant. Thus code like

uintx = 7;
data[7] = 9;
if (data[x] != x + 2)// this condition is never true
return 2;
else
return 1;

simplifies to this:

data[7] = 9;
return 1;

**226 Chapter 3. Contents**


**Simple Inlining**

Since Solidity version 0.8.2, there is another optimizer step that replaces certain jumps to blocks containing “simple”
instructions ending with a “jump” by a copy of these instructions. This corresponds to inlining of simple, small Solidity
or Yul functions. In particular, the sequencePUSHTAG(tag) JUMPmay be replaced, whenever theJUMPis marked as
jump “into” a function and behindtagthere is a basic block (as described above for the “CommonSubexpressionE-
liminator”) that ends in anotherJUMPwhich is marked as a jump “out of” a function.

In particular, consider the following prototypical example of assembly generated for a call to an internal Solidity func-
tion:

tag_return
tag_f
jump // in
tag_return:
...opcodes after call to f...

tag_f:
...body of function f...
jump // out

As long as the body of the function is a continuous basic block, the “Inliner” can replacetag_f jumpby the block at
tag_fresulting in:

tag_return
...body of function f...
jump
tag_return:
...opcodes after call to f...

tag_f:
...body of function f...
jump // out

Now ideally, the other optimizer steps described above will result in the return tag push being moved towards the
remaining jump resulting in:

...body of function f...
tag_return
jump
tag_return:
...opcodes after call to f...

tag_f:
...body of function f...
jump // out

In this situation the “PeepholeOptimizer” will remove the return jump. Ideally, all of this can be done for all references
totag_fleaving it unused, s.t. it can be removed, yielding:

...body of function f...
...opcodes after call to f...

So the call to functionfis inlined and the original definition offcan be removed.

**3.21. The Optimizer 227**


Inlining like this is attempted, whenever a heuristics suggests that inlining is cheaper over the lifetime of a contract
than not inlining. This heuristics depends on the size of the function body, the number of other references to its tag
(approximating the number of calls to the function) and the expected number of executions of the contract (the global
optimizer parameter “runs”).

**3.21.5 Yul-Based Optimizer Module**

The Yul-based optimizer consists of several stages and components that all transform the AST in a semantically equiv-
alent way. The goal is to end up either with code that is shorter or at least only marginally longer but will allow further
optimization steps.

```
Warning: Since the optimizer is under heavy development, the information here might be outdated. If you rely
on a certain functionality, please reach out to the team directly.
```
The optimizer currently follows a purely greedy strategy and does not do any backtracking.

All components of the Yul-based optimizer module are explained below. The following transformation steps are the
main components:

- SSATransform
- CommonSubexpressionEliminator
- ExpressionSimplifier
- UnusedAssignEliminator
- FullInliner

**Optimizer Steps**

This is a list of all steps the Yul-based optimizer sorted alphabetically. You can find more information on the individual
steps and their sequence below.

```
Abbreviation Full name
f BlockFlattener
l CircularReferencesPruner
c CommonSubexpressionEliminator
C ConditionalSimplifier
U ConditionalUnsimplifier
n ControlFlowSimplifier
D DeadCodeEliminator
E EqualStoreEliminator
v EquivalentFunctionCombiner
e ExpressionInliner
j ExpressionJoiner
s ExpressionSimplifier
x ExpressionSplitter
I ForLoopConditionIntoBody
O ForLoopConditionOutOfBody
o ForLoopInitRewriter
i FullInliner
continues on next page
```
**228 Chapter 3. Contents**


```
Table 1 – continued from previous page
Abbreviation Full name
g FunctionGrouper
h FunctionHoister
F FunctionSpecializer
T LiteralRematerialiser
L LoadResolver
M LoopInvariantCodeMotion
m Rematerialiser
V SSAReverser
a SSATransform
t StructuralSimplifier
r UnusedAssignEliminator
p UnusedFunctionParameterPruner
S UnusedStoreEliminator
u UnusedPruner
d VarDeclInitializer
```
Some steps depend on properties ensured byBlockFlattener,FunctionGrouper,ForLoopInitRewriter. For
this reason the Yul optimizer always applies them before applying any steps supplied by the user.

**Selecting Optimizations**

By default the optimizer applies its predefined sequence of optimization steps to the generated assembly. You can
override this sequence and supply your own using the--yul-optimizationsoption:

solc --optimize --ir-optimized --yul-optimizations'dhfoD[xarrscLMcCTU]uljmul:fDnTOcmu'

The order of steps is significant and affects the quality of the output. Moreover, applying a step may uncover new
optimization opportunities for others that were already applied, so repeating steps is often beneficial.

The sequence inside[...]will be applied multiple times in a loop until the Yul code remains unchanged or until the
maximum number of rounds (currently 12) has been reached. Brackets ([]) may be used multiple times in a sequence,
but can not be nested.

An important thing to note, is that there are some hardcoded steps that are always run before and after the user-supplied
sequence, or the default sequence if one was not supplied by the user.

The cleanup sequence delimiter:is optional, and is used to supply a custom cleanup sequence in order to replace the
default one. If omitted, the optimizer will simply apply the default cleanup sequence. In addition, the delimiter may
be placed at the beginning of the user-supplied sequence, which will result in the optimization sequence being empty,
whereas conversely, if placed at the end of the sequence, will be treated as an empty cleanup sequence.

**Preprocessing**

The preprocessing components perform transformations to get the program into a certain normal form that is easier to
work with. This normal form is kept during the rest of the optimization process.

**3.21. The Optimizer 229**


**Disambiguator**

The disambiguator takes an AST and returns a fresh copy where all identifiers have unique names in the input AST.
This is a prerequisite for all other optimizer stages. One of the benefits is that identifier lookup does not need to take
scopes into account which simplifies the analysis needed for other steps.

All subsequent stages have the property that all names stay unique. This means if a new identifier needs to be introduced,
a new unique name is generated.

**FunctionHoister**

The function hoister moves all function definitions to the end of the topmost block. This is a semantically equivalent
transformation as long as it is performed after the disambiguation stage. The reason is that moving a definition to a
higher-level block cannot decrease its visibility and it is impossible to reference variables defined in a different function.

The benefit of this stage is that function definitions can be looked up more easily and functions can be optimized in
isolation without having to traverse the AST completely.

**FunctionGrouper**

The function grouper has to be applied after the Disambiguator and the FunctionHoister. Its effect is that all topmost
elements that are not function definitions are moved into a single block which is the first statement of the root block.

After this step, a program has the following normal form:

{ I F... }

WhereIis a (potentially empty) block that does not contain any function definitions (not even recursively) andFis a
list of function definitions such that no function contains a function definition.

The benefit of this stage is that we always know where the list of functions begins.

**ForLoopConditionIntoBody**

This transformation moves the loop-iteration condition of aforloop into loop body. We need this transformation
because _ExpressionSplitter_ will not apply to iteration condition expressions (theCin the following example).

for { Init... } C { Post... } {
Body...
}

is transformed to

for { Init... } 1 { Post... } {
if iszero(C) { break }
Body...
}

This transformation can also be useful when paired with LoopInvariantCodeMotion, since invariants in the loop-
invariant conditions can then be taken outside the loop.

**230 Chapter 3. Contents**


**ForLoopInitRewriter**

This transformation moves the initialization part of aforloop to before the loop:

for { Init... } C { Post... } {
Body...
}

is transformed to

Init...
for {} C { Post... } {
Body...
}

This eases the rest of the optimization process because we can ignore the complicated scoping rules of theforloop
initialization block.

**VarDeclInitializer**

This step rewrites variable declarations so that all of them are initialized. Declarations likelet x, yare split into
multiple declaration statements.

Only supports initializing with the zero literal for now.

**Pseudo-SSA Transformation**

The purpose of this components is to get the program into a longer form, so that other components can more easily
work with it. The final representation will be similar to a static-single-assignment (SSA) form, with the difference
that it does not make use of explicit “phi” functions which combines the values from different branches of control flow
because such a feature does not exist in the Yul language. Instead, when control flow merges, if a variable is re-assigned
in one of the branches, a new SSA variable is declared to hold its current value, so that the following expressions still
only need to reference SSA variables.

An example transformation is the following:

{
leta := calldataload(0)
letb := calldataload(0x20)
if gt(a, 0) {
b := mul(b, 0x20)
}
a := add(a, 1)
sstore(a, add(b, 0x20))
}

When all the following transformation steps are applied, the program will look as follows:

{
let_1 := 0
leta_9 := calldataload(_1)
leta := a_9
let_2 := 0x20
(continues on next page)

**3.21. The Optimizer 231**


(continued from previous page)
letb_10 := calldataload(_2)
letb := b_10
let_3 := 0
let_4 := gt(a_9, _3)
if _4
{
let_5 := 0x20
letb_11 := mul(b_10, _5)
b := b_11
}
letb_12 := b
let_6 := 1
leta_13 := add(a_9, _6)
let_7 := 0x20
let_8 := add(b_12, _7)
sstore(a_13, _8)
}

Note that the only variable that is re-assigned in this snippet isb. This re-assignment cannot be avoided becausebhas
different values depending on the control flow. All other variables never change their value once they are defined. The
advantage of this property is that variables can be freely moved around and references to them can be exchanged by
their initial value (and vice-versa), as long as these values are still valid in the new context.

Of course, the code here is far from being optimized. To the contrary, it is much longer. The hope is that this code
will be easier to work with and furthermore, there are optimizer steps that undo these changes and make the code more
compact again at the end.

**ExpressionSplitter**

The expression splitter turns expressions likeadd(mload(0x123), mul(mload(0x456), 0x20))into a sequence
of declarations of unique variables that are assigned sub-expressions of that expression so that each function call has
only variables as arguments.

The above would be transformed into

{
let_1 := 0x20
let_2 := 0x456
let_3 := mload(_2)
let_4 := mul(_3, _1)
let_5 := 0x123
let_6 := mload(_5)
letz := add(_6, _4)
}

Note that this transformation does not change the order of opcodes or function calls.

It is not applied to loop iteration-condition, because the loop control flow does not allow this “outlining” of the inner
expressions in all cases. We can sidestep this limitation by applying _ForLoopConditionIntoBody_ to move the iteration
condition into loop body.

The final program should be in an _expression-split form_ , where (with the exception of loop conditions) function calls
cannot appear nested inside expressions and all function call arguments have to be variables.

**232 Chapter 3. Contents**


The benefits of this form are that it is much easier to re-order the sequence of opcodes and it is also easier to perform
function call inlining. Furthermore, it is simpler to replace individual parts of expressions or re-organize the “expression
tree”. The drawback is that such code is much harder to read for humans.

**SSATransform**

This stage tries to replace repeated assignments to existing variables by declarations of new variables as much as
possible. The reassignments are still there, but all references to the reassigned variables are replaced by the newly
declared variables.

Example:

{
leta := 1
mstore(a, 2)
a := 3
}

is transformed to

{
leta_1 := 1
leta := a_1
mstore(a_1, 2)
leta_3 := 3
a := a_3
}

Exact semantics:

For any variableathat is assigned to somewhere in the code (variables that are declared with value and never re-assigned
are not modified) perform the following transforms:

- replacelet a := vbylet a_i := v let a := a_i
- replacea := vbylet a_i := v a := a_iwhereiis a number such thata_iis yet unused.

Furthermore, always record the current value ofiused foraand replace each reference toabya_i. The current value
mapping is cleared for a variableaat the end of each block in which it was assigned to and at the end of theforloop init
block if it is assigned inside theforloop body or post block. If a variable’s value is cleared according to the rule above
and the variable is declared outside the block, a new SSA variable will be created at the location where control flow
joins, this includes the beginning of loop post/body block and the location right afterif/switch/for/block statement.

After this stage, the UnusedAssignEliminator is recommended to remove the unnecessary intermediate assignments.

This stage provides best results if the ExpressionSplitter and the CommonSubexpressionEliminator are run right before
it, because then it does not generate excessive amounts of variables. On the other hand, the CommonSubexpressionE-
liminator could be more efficient if run after the SSA transform.

**3.21. The Optimizer 233**


**UnusedAssignEliminator**

The SSA transform always generates an assignment of the forma := a_i, even though these might be unnecessary
in many cases, like the following example:

{
leta := 1
a := mload(a)
a := sload(a)
sstore(a, 1)
}

The SSA transform converts this snippet to the following:

{
leta_1 := 1
leta := a_1
leta_2 := mload(a_1)
a := a_2
leta_3 := sload(a_2)
a := a_3
sstore(a_3, 1)
}

The UnusedAssignEliminator removes all the three assignments toa, because the value ofais not used and thus turn
this snippet into strict SSA form:

{
leta_1 := 1
leta_2 := mload(a_1)
leta_3 := sload(a_2)
sstore(a_3, 1)
}

Of course the intricate parts of determining whether an assignment is unused or not are connected to joining control
flow.

The component works as follows in detail:

The AST is traversed twice: in an information gathering step and in the actual removal step. During information
gathering, we maintain a mapping from assignment statements to the three states “unused”, “undecided” and “used”
which signifies whether the assigned value will be used later by a reference to the variable.

When an assignment is visited, it is added to the mapping in the “undecided” state (see remark aboutforloops below)
and every other assignment to the same variable that is still in the “undecided” state is changed to “unused”. When a
variable is referenced, the state of any assignment to that variable still in the “undecided” state is changed to “used”.

At points where control flow splits, a copy of the mapping is handed over to each branch. At points where control flow
joins, the two mappings coming from the two branches are combined in the following way: Statements that are only in
one mapping or have the same state are used unchanged. Conflicting values are resolved in the following way:

- “unused”, “undecided” -> “undecided”
- “unused”, “used” -> “used”
- “undecided”, “used” -> “used”

**234 Chapter 3. Contents**


Forforloops, the condition, body and post-part are visited twice, taking the joining control-flow at the condition into
account. In other words, we create three control flow paths: Zero runs of the loop, one run and two runs and then
combine them at the end.

Simulating a third run or even more is unnecessary, which can be seen as follows:

A state of an assignment at the beginning of the iteration will deterministically result in a state of that assignment at the
end of the iteration. Let this state mapping function be calledf. The combination of the three different statesunused,
undecidedandusedas explained above is themaxoperation whereunused = 0,undecided = 1andused = 2.

The proper way would be to compute

max(s, f(s), f(f(s)), f(f(f(s))), ...)

as state after the loop. Sincefjust has a range of three different values, iterating it has to reach a cycle after at most
three iterations, and thusf(f(f(s)))has to equal one ofs,f(s), orf(f(s))and thus

max(s, f(s), f(f(s))) = max(s, f(s), f(f(s)), f(f(f(s))), ...)

In summary, running the loop at most twice is enough because there are only three different states.

Forswitchstatements that have a default case, there is no control-flow part that skips theswitch.

When a variable goes out of scope, all statements still in the “undecided” state are changed to “unused”, unless the
variable is the return parameter of a function - there, the state changes to “used”.

In the second traversal, all assignments that are in the “unused” state are removed.

This step is usually run right after the SSA transform to complete the generation of the pseudo-SSA.

**Tools**

**Movability**

Movability is a property of an expression. It roughly means that the expression is side-effect free and its evaluation
only depends on the values of variables and the call-constant state of the environment. Most expressions are movable.
The following parts make an expression non-movable:

- function calls (might be relaxed in the future if all statements in the function are movable)
- opcodes that (can) have side-effects (likecallorselfdestruct)
- opcodes that read or write memory, storage or external state information
- opcodes that depend on the current PC, memory size or returndata size

**DataflowAnalyzer**

The DataflowAnalyzer is not an optimizer step itself but is used as a tool by other components. While traversing the
AST, it tracks the current value of each variable, as long as that value is a movable expression. It records the variables
that are part of the expression that is currently assigned to each other variable. Upon each assignment to a variablea,
the current stored value ofais updated and all stored values of all variablesbare cleared wheneverais part of the
currently stored expression forb.

At control-flow joins, knowledge about variables is cleared if they have or would be assigned in any of the control-flow
paths. For instance, upon entering aforloop, all variables are cleared that will be assigned during the body or the post
block.

**3.21. The Optimizer 235**


**Expression-Scale Simplifications**

These simplification passes change expressions and replace them by equivalent and hopefully simpler expressions.

**CommonSubexpressionEliminator**

This step uses the DataflowAnalyzer and replaces subexpressions that syntactically match the current value of a variable
by a reference to that variable. This is an equivalence transform because such subexpressions have to be movable.

All subexpressions that are identifiers themselves are replaced by their current value if the value is an identifier.

The combination of the two rules above allow to compute a local value numbering, which means that if two variables
have the same value, one of them will always be unused. The UnusedPruner or the UnusedAssignEliminator will then
be able to fully eliminate such variables.

This step is especially efficient if the ExpressionSplitter is run before. If the code is in pseudo-SSA form, the values of
variables are available for a longer time and thus we have a higher chance of expressions to be replaceable.

The ExpressionSimplifier will be able to perform better replacements if the CommonSubexpressionEliminator was run
right before it.

**ExpressionSimplifier**

The ExpressionSimplifier uses the DataflowAnalyzer and makes use of a list of equivalence transforms on expressions
likeX + 0 -> Xto simplify the code.

It tries to match patterns likeX + 0on each subexpression. During the matching procedure, it resolves variables to their
currently assigned expressions to be able to match more deeply nested patterns even when the code is in pseudo-SSA
form.

Some of the patterns likeX - X -> 0can only be applied as long as the expressionXis movable, because otherwise it
would remove its potential side-effects. Since variable references are always movable, even if their current value might
not be, the ExpressionSimplifier is again more powerful in split or pseudo-SSA form.

**LiteralRematerialiser**

To be documented.

**LoadResolver**

Optimisation stage that replaces expressions of typesload(x)andmload(x)by the value currently stored in storage
resp. memory, if known.

Works best if the code is in SSA form.

Prerequisites: Disambiguator, ForLoopInitRewriter.

**236 Chapter 3. Contents**


**Statement-Scale Simplifications**

**CircularReferencesPruner**

This stage removes functions that call each other but are neither externally referenced nor referenced from the outermost
context.

**ConditionalSimplifier**

The ConditionalSimplifier inserts assignments to condition variables if the value can be determined from the control-
flow.

Destroys SSA form.

Currently, this tool is very limited, mostly because we do not yet have support for boolean types. Since conditions only
check for expressions being nonzero, we cannot assign a specific value.

Current features:

- switchcases: insert<condition> := <caseLabel>
- afterifstatement with terminating control-flow, insert<condition> := 0

Future features:

- allow replacements by 1
- take termination of user-defined functions into account

Works best with SSA form and if dead code removal has run before.

Prerequisite: Disambiguator.

**ConditionalUnsimplifier**

Reverse of ConditionalSimplifier.

**ControlFlowSimplifier**

Simplifies several control-flow structures:

- replaceifwith empty body withpop(condition)
- remove empty defaultswitchcase
- remove emptyswitchcase if no default case exists
- replaceswitchwith no cases withpop(expression)
- turnswitchwith single case intoif
- replaceswitchwith only default case withpop(expression)and body
- replaceswitchwith const expr with matching case body
- replaceforwith terminating control flow and without otherbreak/continuebyif
- removeleaveat the end of a function.

**3.21. The Optimizer 237**


None of these operations depend on the data flow. The StructuralSimplifier performs similar tasks that do depend on
data flow.

The ControlFlowSimplifier does record the presence or absence ofbreakandcontinuestatements during its traversal.

Prerequisite: Disambiguator, FunctionHoister, ForLoopInitRewriter.

Important: Introduces EVM opcodes and thus can only be used on EVM code for now.

**DeadCodeEliminator**

This optimization stage removes unreachable code.

Unreachable code is any code within a block which is preceded by aleave,return,invalid,break,continue,
selfdestruct,revertor by a call to a user-defined function that recurses infinitely.

Function definitions are retained as they might be called by earlier code and thus are considered reachable.

Because variables declared in aforloop’s init block have their scope extended to the loop body, we require ForLoop-
InitRewriter to run before this step.

Prerequisites: ForLoopInitRewriter, FunctionHoister, FunctionGrouper.

**EqualStoreEliminator**

This steps removesmstore(k, v)and sstore(k, v)calls if there was a previous call tomstore(k, v)/
sstore(k, v), no other store in between and the values ofkandvdid not change.

This simple step is effective if run after the SSATransform and the CommonSubexpressionEliminator, because SSA
will make sure that the variables will not change and the CommonSubexpressionEliminator re-uses exactly the same
variable if the value is known to be the same.

Prerequisites: Disambiguator, ForLoopInitRewriter.

**UnusedPruner**

This step removes the definitions of all functions that are never referenced.

It also removes declarations of variables that are never referenced. If a declaration assigns a value that is not movable,
the expression is retained, but its value is discarded.

All movable expression statements (expressions that are not assigned) are removed.

**StructuralSimplifier**

This is a general step that performs various kinds of simplifications on a structural level:

- replaceifstatement with empty body bypop(condition)
- replaceifstatement with true condition by its body
- removeifstatement with false condition
- turnswitchwith single case intoif
- replaceswitchwith only default case bypop(expression)and body
- replaceswitchwith literal expression by matching case body

**238 Chapter 3. Contents**


- replaceforloop with false condition by its initialization part

This component uses the DataflowAnalyzer.

**BlockFlattener**

This stage eliminates nested blocks by inserting the statements in the inner block at the appropriate place in the outer
block. It depends on the FunctionGrouper and does not flatten the outermost block to keep the form produced by the
FunctionGrouper.

{
{
letx := 2
{
lety := 3
mstore(x, y)
}
}
}

is transformed to

{
{
letx := 2
lety := 3
mstore(x, y)
}
}

As long as the code is disambiguated, this does not cause a problem because the scopes of variables can only grow.

**LoopInvariantCodeMotion**

This optimization moves movable SSA variable declarations outside the loop.

Only statements at the top level in a loop’s body or post block are considered, i.e variable declarations inside conditional
branches will not be moved out of the loop.

ExpressionSplitter and SSATransform should be run upfront to obtain better results.

Prerequisites: Disambiguator, ForLoopInitRewriter, FunctionHoister.

**Function-Level Optimizations**

**FunctionSpecializer**

This step specializes the function with its literal arguments.

If a function, say,function f(a, b) { sstore (a, b) }, is called with literal arguments, for example,f(x, 5),
wherexis an identifier, it could be specialized by creating a new functionf_1that takes only one argument, i.e.,

**3.21. The Optimizer 239**


functionf_1(a_1) {
letb_1 := 5
sstore(a_1, b_1)
}

Other optimization steps will be able to make more simplifications to the function. The optimization step is mainly
useful for functions that would not be inlined.

Prerequisites: Disambiguator, FunctionHoister.

LiteralRematerialiser is recommended as a prerequisite, even though it’s not required for correctness.

**UnusedFunctionParameterPruner**

This step removes unused parameters in a function.

If a parameter is unused, likecandyin,function f(a,b,c) -> x, y { x := div(a,b) }, we remove the pa-
rameter and create a new “linking” function as follows:

functionf(a,b) -> x { x := div(a,b) }
functionf2(a,b,c) -> x, y { x := f(a,b) }

and replace all references tofbyf2. The inliner should be run afterwards to make sure that all references tof2are
replaced byf.

Prerequisites: Disambiguator, FunctionHoister, LiteralRematerialiser.

The step LiteralRematerialiser is not required for correctness. It helps deal with cases such as:function f(x) ->
y { revert(y, y} }where the literalywill be replaced by its value 0 , allowing us to rewrite the function.

**UnusedStoreEliminator**

Optimizer component that removes redundantsstoreand memory store statements. In case of ansstore, if all
outgoing code paths revert (due to an explicitrevert(),invalid(), or infinite recursion) or lead to anothersstore
for which the optimizer can tell that it will overwrite the first store, the statement will be removed. However, if there
is a read operation between the initialsstoreand the revert, or the overwritingsstore, the statement will not be
removed. Such read operations include: external calls, user-defined functions with any storage access, andsloadof a
slot that cannot be proven to differ from the slot written by the initialsstore.

For example, the following code

{
letc := calldataload(0)
sstore(c, 1)
if c {
sstore(c, 2)
}
sstore(c, 3)
}

will be transformed into the code below after the UnusedStoreEliminator step is run

{
letc := calldataload(0)
(continues on next page)

**240 Chapter 3. Contents**


(continued from previous page)
if c { }
sstore(c, 3)
}

For memory store operations, things are generally simpler, at least in the outermost Yul block as all such statements will
be removed if they are never read from in any code path. At function analysis level, however, the approach is similar
tosstore, as we do not know whether the memory location will be read once we leave the function’s scope, so the
statement will be removed only if all code paths lead to a memory overwrite.

Best run in SSA form.

Prerequisites: Disambiguator, ForLoopInitRewriter.

**EquivalentFunctionCombiner**

If two functions are syntactically equivalent, while allowing variable renaming but not any re-ordering, then any refer-
ence to one of the functions is replaced by the other.

The actual removal of the function is performed by the UnusedPruner.

**Function Inlining**

**ExpressionInliner**

This component of the optimizer performs restricted function inlining by inlining functions that can be inlined inside
functional expressions, i.e. functions that:

- return a single value.
- have a body liker := <functional expression>.
- neither reference themselves norrin the right hand side.

Furthermore, for all parameters, all of the following need to be true:

- The argument is movable.
- The parameter is either referenced less than twice in the function body, or the argument is rather cheap (“cost”
    of at most 1, like a constant up to0xff).

Example: The function to be inlined has the form offunction f(...) -> r { r := E }whereEis an expression
that does not referencerand all arguments in the function call are movable expressions.

The result of this inlining is always a single expression.

This component can only be used on sources with unique names.

**3.21. The Optimizer 241**


**FullInliner**

The FullInliner replaces certain calls of certain functions by the function’s body. This is not very helpful in most cases,
because it just increases the code size but does not have a benefit. Furthermore, code is usually very expensive and
we would often rather have shorter code than more efficient code. In some cases, though, inlining a function can have
positive effects on subsequent optimizer steps. This is the case if one of the function arguments is a constant, for
example.

During inlining, a heuristic is used to tell if the function call should be inlined or not. The current heuristic does not
inline into “large” functions unless the called function is tiny. Functions that are only used once are inlined, as well as
medium-sized functions, while function calls with constant arguments allow slightly larger functions.

In the future, we may include a backtracking component that, instead of inlining a function right away, only specializes
it, which means that a copy of the function is generated where a certain parameter is always replaced by a constant.
After that, we can run the optimizer on this specialized function. If it results in heavy gains, the specialized function is
kept, otherwise the original function is used instead.

FunctionHoister and ExpressionSplitter are recommended as prerequisites since they make the step more efficient, but
are not required for correctness. In particular, function calls with other function calls as arguments are not inlined, but
running ExpressionSplitter beforehand ensures that there are no such calls in the input.

**Cleanup**

The cleanup is performed at the end of the optimizer run. It tries to combine split expressions into deeply nested ones
again and also improves the “compilability” for stack machines by eliminating variables as much as possible.

**ExpressionJoiner**

This is the opposite operation of the ExpressionSplitter. It turns a sequence of variable declarations that have exactly
one reference into a complex expression. This stage fully preserves the order of function calls and opcode executions.
It does not make use of any information concerning the commutativity of the opcodes; if moving the value of a variable
to its place of use would change the order of any function call or opcode execution, the transformation is not performed.

Note that the component will not move the assigned value of a variable assignment or a variable that is referenced more
than once.

The snippetlet x := add(0, 2) let y := mul(x, mload(2))is not transformed, because it would cause the
order of the call to the opcodesaddandmloadto be swapped - even though this would not make a difference because
addis movable.

When reordering opcodes like that, variable references and literals are ignored. Because of that, the snippetlet x :=
add(0, 2) let y := mul(x, 3)is transformed tolet y := mul(add(0, 2), 3), even though theaddopcode
would be executed after the evaluation of the literal 3.

**SSAReverser**

This is a tiny step that helps in reversing the effects of the SSATransform if it is combined with the CommonSubex-
pressionEliminator and the UnusedPruner.

The SSA form we generate is detrimental to code generation because it produces many local variables. It would be
better to just re-use existing variables with assignments instead of fresh variable declarations.

The SSATransform rewrites

**242 Chapter 3. Contents**


leta := calldataload(0)
mstore(a, 1)

to

leta_1 := calldataload(0)
leta := a_1
mstore(a_1, 1)
leta_2 := calldataload(0x20)
a := a_2

The problem is that instead ofa, the variablea_1is used wheneverawas referenced. The SSATransform changes
statements of this form by just swapping out the declaration and the assignment. The above snippet is turned into

leta := calldataload(0)
leta_1 := a
mstore(a_1, 1)
a := calldataload(0x20)
leta_2 := a

This is a very simple equivalence transform, but when we now run the CommonSubexpressionEliminator, it will replace
all occurrences ofa_1bya(untilais re-assigned). The UnusedPruner will then eliminate the variablea_1altogether
and thus fully reverse the SSATransform.

**StackCompressor**

One problem that makes code generation for the Ethereum Virtual Machine hard is the fact that there is a hard limit of
16 slots for reaching down the expression stack. This more or less translates to a limit of 16 local variables. The stack
compressor takes Yul code and compiles it to EVM bytecode. Whenever the stack difference is too large, it records the
function this happened in.

For each function that caused such a problem, the Rematerialiser is called with a special request to aggressively elimi-
nate specific variables sorted by the cost of their values.

On failure, this procedure is repeated multiple times.

**Rematerialiser**

The rematerialisation stage tries to replace variable references by the expression that was last assigned to the variable.
This is of course only beneficial if this expression is comparatively cheap to evaluate. Furthermore, it is only semanti-
cally equivalent if the value of the expression did not change between the point of assignment and the point of use. The
main benefit of this stage is that it can save stack slots if it leads to a variable being eliminated completely (see below),
but it can also save aDUPopcode on the EVM if the expression is very cheap.

The Rematerialiser uses the DataflowAnalyzer to track the current values of variables, which are always movable. If
the value is very cheap or the variable was explicitly requested to be eliminated, the variable reference is replaced by
its current value.

**3.21. The Optimizer 243**


**ForLoopConditionOutOfBody**

Reverses the transformation of ForLoopConditionIntoBody.

For any movablec, it turns

for { ... } 1 { ... } {
if iszero(c) { break }
...
}

into

for { ... } c { ... } {
...
}

and it turns

for { ... } 1 { ... } {
if c { break }
...
}

into

for { ... } iszero(c) { ... } {
...
}

The LiteralRematerialiser should be run before this step.

**3.21.6 Codegen-Based Optimizer Module**

Currently, the codegen-based optimizer module provides two optimizations.

The first one, available in the legacy code generator, moves literals to the right side of commutative binary operators,
which helps exploit their associativity.

The other one, available in the IR-based code generator, enables the use of unchecked arithmetic when generating
code for incrementing the counter variable of certain idiomaticforloops. This avoids wasting gas by identifying some
conditions that guarantee that the counter variable cannot overflow. This eliminates the need to use a verbose unchecked
arithmetic block inside the loop body to increment the counter variable.

**Unchecked Loop Increment**

Introduced in Solidity0.8.22, the overflow check optimization step is concerned with identifying the conditions under
which theforloop counter can be safely incremented without overflow checks.

This optimization is **only** applied toforloops of the general form:

for(uinti = X; i < Y; ++i) {
// variable i is not modified in the loop body
}

**244 Chapter 3. Contents**


The condition and the fact that the counter variable is only ever incremented guarantee that it never overflows. The
precise requirements for the loop to be eligible for the optimization are as follows:

- The loop condition is a comparison of the formi < Y, for a local counter variablei(called the “loop counter”
    hereon) and an expressionY.
- The built-in operator<is necessarily used in the loop condition and is the only operator that triggers the opti-
    mization.<=and the like are intentionally excluded. Additionally, user-defined operators are **not** eligible.
- The loop expression is a prefix or postfix increment of the counter variable, i.e,i++or++i.
- The loop counter is a local variable of a built-in integer type.
- The loop counter is **not** modified by the loop body or by the expression used as the loop condition.
- The comparison is performed on the same type as the loop counter, meaning that the type of the right-hand-side
    expression is implicitly convertible to the type of the counter, such that the latter is not implicitly widened before
    the comparison.

To clarify the last condition, consider the following example:

for(uint8 i = 0; i <uint16(1000); i++) {
// ...
}

In this case, the counterihas its type implicitly converted fromuint8touint16before the comparison and the
condition is in fact never false, so the overflow check for the increment cannot be removed.

### 3.22 Contract Metadata

The Solidity compiler automatically generates a JSON file. The file contains two kinds of information about the com-
piled contract:

- How to interact with the contract: ABI, and NatSpec documentation.
- How to reproduce the compilation and verify a deployed contract: compiler version, compiler settings, and source
    files used.

The compiler appends by default the IPFS hash of the metadata file to the end of the runtime bytecode (not necessarily
the creation bytecode) of each contract, so that, if published, you can retrieve the file in an authenticated way without
having to resort to a centralized data provider. The other available options are the Swarm hash and not appending the
metadata hash to the bytecode. These can be configured via the _Standard JSON Interface_.

You have to publish the metadata file to IPFS, Swarm, or another service so that others can access it. You create the
file by using thesolc --metadatacommand together with the--output-dirparameter. Without the parameter,
the metadata will be written to standard output. The metadata contains IPFS and Swarm references to the source code,
so you have to upload all source files in addition to the metadata file. For IPFS, the hash contained in the CID returned
byipfs add(not the direct sha2-256 hash of the file) shall match with the one contained in the bytecode.

The metadata file has the following format. The example below is presented in a human-readable way. Properly
formatted metadata should use quotes correctly, reduce whitespace to a minimum, and sort the keys of all objects
in alphabetical order to arrive at a canonical formatting. Comments are not permitted and are used here only for
explanatory purposes.

{
// Required: Details about the compiler, contents are specific
// to the language.
"compiler": {
(continues on next page)

**3.22. Contract Metadata 245**


```
(continued from previous page)
// Optional: Hash of the compiler binary which produced this output
"keccak256": "0x123...",
// Required for Solidity: Version of the compiler
"version": "0.8.2+commit.661d1103"
},
// Required: Source code language, basically selects a "sub-version"
// of the specification
"language": "Solidity",
// Required: Generated information about the contract.
"output": {
// Required: ABI definition of the contract. See "Contract ABI Specification"
"abi": [/* ... */],
// Required: NatSpec developer documentation of the contract. See https://docs.
˓→soliditylang.org/en/latest/natspec-format.html for details.
"devdoc": {
// Contents of the @author NatSpec field of the contract
"author": "John Doe",
// Contents of the @dev NatSpec field of the contract
"details": "Interface of the ERC20 standard as defined in the EIP. See https://
˓→eips.ethereum.org/EIPS/eip-20 for details",
"errors": {
"MintToZeroAddress()" : {
"details": "Cannot mint to zero address"
}
},
"events": {
"Transfer(address,address,uint256)": {
"details": "Emitted when`value` tokens are moved from one account (`from`)␣
˓→toanother (`to`).",
"params": {
"from": "The sender address",
"to": "The receiver address",
"value": "The token amount"
}
}
},
"kind": "dev",
"methods": {
"transfer(address,uint256)": {
// Contents of the @dev NatSpec field of the method
"details": "Returns a boolean value indicating whether the operation succeeded.
˓→Must be called by the token holder address",
// Contents of the @param NatSpec fields of the method
"params": {
"_value": "The amount tokens to be transferred",
"_to": "The receiver address"
},
// Contents of the @return NatSpec field.
"returns": {
// Return var name (here "success") if exists. "_0" as key if return var is␣
˓→unnamed
"success": "a boolean value indicating whether the operation succeeded"
(continues on next page)
```
**246 Chapter 3. Contents**


```
(continued from previous page)
}
}
},
"stateVariables": {
"owner": {
// Contents of the @dev NatSpec field of the state variable
"details": "Must be set during contract creation. Can then only be changed by␣
˓→the owner"
}
},
// Contents of the @title NatSpec field of the contract
"title": "MyERC20: an example ERC20",
"version": 1// NatSpec version
},
// Required: NatSpec user documentation of the contract. See "NatSpec Format"
"userdoc": {
"errors": {
"ApprovalCallerNotOwnerNorApproved()": [
{
"notice": "The caller must own the token or be an approved operator."
}
]
},
"events": {
"Transfer(address,address,uint256)": {
"notice": "`_value` tokens have been moved from`from`to `to`"
}
},
"kind": "user",
"methods": {
"transfer(address,uint256)": {
"notice": "Transfers`_value`tokens to address`_to`"
}
},
"version": 1// NatSpec version
}
},
// Required: Compiler settings. Reflects the settings in the JSON input during␣
˓→compilation.
// Check the documentation of standard JSON input's "settings" field
"settings": {
// Required for Solidity: File path and the name of the contract or library this
// metadata is created for.
"compilationTarget": {
"myDirectory/myFile.sol": "MyContract"
},
// Required for Solidity.
"evmVersion": "london",
// Required for Solidity: Addresses for libraries used.
"libraries": {
"MyLib": "0x123123..."
},
(continues on next page)
```
**3.22. Contract Metadata 247**


```
(continued from previous page)
"metadata": {
// Reflects the setting used in the input json, defaults to "true"
"appendCBOR": true,
// Reflects the setting used in the input json, defaults to "ipfs"
"bytecodeHash": "ipfs",
// Reflects the setting used in the input json, defaults to "false"
"useLiteralContent":true
},
// Optional: Optimizer settings. The fields "enabled" and "runs" are deprecated
// and are only given for backward-compatibility.
"optimizer": {
"details": {
"constantOptimizer":false,
"cse":false,
"deduplicate":false,
// inliner defaults to "false"
"inliner":false,
// jumpdestRemover defaults to "true"
"jumpdestRemover":true,
"orderLiterals":false,
// peephole defaults to "true"
"peephole":true,
"yul":true,
// Optional: Only present if "yul" is "true"
"yulDetails": {
"optimizerSteps": "dhfoDgvulfnTUtnIf...",
"stackAllocation": false
}
},
"enabled": true,
"runs": 500
},
// Required for Solidity: Sorted list of import remappings.
"remappings": [ ":g=/dir" ]
},
// Required: Compilation source files/source units, keys are file paths
"sources": {
"settable": {
// Required (unless "url" is used): literal contents of the source file
"content": "contract settable is owned { uint256 private x = 0; function␣
˓→set(uint256 _x) public { if (msg.sender == owner) x = _x; } }",
// Required: keccak256 hash of the source file
"keccak256": "0x234..."
},
"myDirectory/myFile.sol": {
// Required: keccak256 hash of the source file
"keccak256": "0x123...",
// Optional: SPDX license identifier as given in the source file
"license": "MIT",
// Required (unless "content" is used, see above): Sorted URL(s)
// to the source file, protocol is more or less arbitrary, but an
// IPFS URL is recommended
(continues on next page)
```
**248 Chapter 3. Contents**


(continued from previous page)
"urls": [ "bzz-raw://7d7a...", "dweb:/ipfs/QmN..." ]
}
},
// Required: The version of the metadata format
"version": 1
}

```
Warning: Since the bytecode of the resulting contract contains the metadata hash by default, any change to the
metadata might result in a change of the bytecode. This includes changes to a filename or path, and since the
metadata includes a hash of all the sources used, a single whitespace change results in different metadata, and
different bytecode.
```
**Note:** The ABI definition above has no fixed order. It can change with compiler versions. Starting from Solidity
version 0.5.12, though, the array maintains a certain order.

**3.22.1 Encoding of the Metadata Hash in the Bytecode**

The compiler currently by default appends the IPFS hash (in CID v0) of the canonical metadata file and the compiler
version to the end of the bytecode. Optionally, a Swarm hash instead of the IPFS, or an experimental flag is used.
Below are all the possible fields:

{
"ipfs": "<metadata hash>",
// If "bytecodeHash" was "bzzr1" in compiler settings not "ipfs" but "bzzr1"
"bzzr1": "<metadata hash>",
// Previous versions were using "bzzr0" instead of "bzzr1"
"bzzr0": "<metadata hash>",
// If any experimental features that affect code generation are used
"experimental": true,
"solc": "<compiler version>"
}

Because we might support other ways to retrieve the metadata file in the future, this information is stored CBOR-
encoded. The last two bytes in the bytecode indicate the length of the CBOR encoded information. By looking at this
length, the relevant part of the bytecode can be decoded with a CBOR decoder.

Check the Metadata Playground to see it in action.

Whereas release builds of solc use a 3 byte encoding of the version as shown above (one byte each for major, minor and
patch version number), pre-release builds will instead use a complete version string including commit hash and build
date.

The commandline flag--no-cbor-metadatacan be used to skip metadata from getting appended at the end of the
deployed bytecode. Equivalently, the boolean fieldsettings.metadata.appendCBORin Standard JSON input can
be set to false.

**Note:** The CBOR mapping can also contain other keys, so it is better to fully decode the data by looking at the end of
the bytecode for the CBOR length, and to use a proper CBOR parser. Do not rely on it starting with0xa264or0xa2

**3.22. Contract Metadata 249**


0x64'i' 'p' 'f' 's'.

**3.22.2 Usage for Automatic Interface Generation and NatSpec**

The metadata is used in the following way: A component that wants to interact with a contract (e.g. a wallet) retrieves
the code of the contract. It decodes the CBOR encoded section containing the IPFS/Swarm hash of the metadata file.
With that hash, the metadata file is retrieved. That file is JSON-decoded into a structure like above.

The component can then use the ABI to automatically generate a rudimentary user interface for the contract.

Furthermore, the wallet can use the NatSpec user documentation to display a human-readable confirmation message to
the user whenever they interact with the contract, together with requesting authorization for the transaction signature.

For additional information, read _Ethereum Natural Language Specification (NatSpec) format_.

**3.22.3 Usage for Source Code Verification**

If pinned/published, it is possible to retrieve the metadata of the contract from IPFS/Swarm. The metadata file also
contains the URLs or the IPFS hashes of the source files, as well as the compilation settings, i.e. everything needed to
reproduce a compilation.

With this information it is then possible to verify the source code of a contract by reproducing the compilation, and
comparing the bytecode from the compilation with the bytecode of the deployed contract.

This automatically verifies the metadata since its hash is part of the bytecode, as well as the source codes, because
their hashes are part of the metadata. Any change in the files or settings would result in a different metadata hash. The
metadata here serves as a fingerprint of the whole compilation.

Sourcify makes use of this feature for “full/perfect verification”, as well as pinning the files publicly on IPFS to be
accessed with the metadata hash.

### 3.23 Contract ABI Specification

**3.23.1 Basic Design**

The Contract Application Binary Interface (ABI) is the standard way to interact with contracts in the Ethereum ecosys-
tem, both from outside the blockchain and for contract-to-contract interaction. Data is encoded according to its type,
as described in this specification. The encoding is not self describing and thus requires a schema in order to decode.

We assume that the interface functions of a contract are strongly typed, known at compilation time and static. We
assume that all contracts will have the interface definitions of any contracts they call available at compile-time.

This specification does not address contracts whose interface is dynamic or otherwise known only at run-time. Also,
the ABI specification for libraries is _slightly different_.

**250 Chapter 3. Contents**


**3.23.2 Function Selector**

The first four bytes of the call data for a function call specifies the function to be called. It is the first (left, high-order in
big-endian) four bytes of the Keccak-256 hash of the signature of the function. The signature is defined as the canonical
expression of the basic prototype without data location specifier, i.e. the function name with the parenthesised list of
parameter types. Parameter types are split by a single comma — no spaces are used.

**Note:** The return type of a function is not part of this signature. In _Solidity’s function overloading_ return types are
not considered. The reason is to keep function call resolution context-independent. The _JSON description of the ABI_
however contains both inputs and outputs.

**3.23.3 Argument Encoding**

Starting from the fifth byte, the encoded arguments follow. This encoding is also used in other places, e.g. the return
values and also event arguments are encoded in the same way, without the four bytes specifying the function.

**3.23.4 Types**

Note that the library ABIs can take types different than below e.g. for non-storage structs. See _library selectors_ for
details.

The following elementary types exist:

- uint<M>: unsigned integer type ofMbits,0 < M <= 256,M % 8 == 0. e.g.uint32,uint8,uint256.
- int<M>: two’s complement signed integer type ofMbits,0 < M <= 256,M % 8 == 0.
- address: equivalent touint160, except for the assumed interpretation and language typing. For computing the
    function selector,addressis used.
- uint,int: synonyms foruint256,int256respectively. For computing the function selector,uint256and
    int256have to be used.
- bool: equivalent touint8restricted to the values 0 and 1. For computing the function selector,boolis used.
- fixed<M>x<N>: signed fixed-point decimal number ofMbits,8 <= M <= 256,M % 8 == 0, and0 < N <=
    80 , which denotes the valuevasv / (10 ** N).
- ufixed<M>x<N>: unsigned variant offixed<M>x<N>.
- fixed,ufixed: synonyms forfixed128x18,ufixed128x18respectively. For computing the function selector,
    fixed128x18andufixed128x18have to be used.
- bytes<M>: binary type ofMbytes,0 < M <= 32.
- function: an address (20 bytes) followed by a function selector (4 bytes). Encoded identical tobytes24.

The following (fixed-size) array type exists:

- <type>[M]: a fixed-length array ofMelements,M >= 0, of the given type.

```
Note: While this ABI specification can express fixed-length arrays with zero elements, they’re not supported
by the compiler.
```
The following non-fixed-size types exist:

- bytes: dynamic sized byte sequence.

**3.23. Contract ABI Specification 251**


- string: dynamic sized unicode string assumed to be UTF-8 encoded.
- <type>[]: a variable-length array of elements of the given type.

Types can be combined to a tuple by enclosing them inside parentheses, separated by commas:

- (T1,T2,...,Tn): tuple consisting of the typesT1, ...,Tn,n >= 0

It is possible to form tuples of tuples, arrays of tuples and so on. It is also possible to form zero-tuples (wheren ==
0 ).

**Mapping Solidity to ABI types**

Solidity supports all the types presented above with the same names with the exception of tuples. On the other hand,
some Solidity types are not supported by the ABI. The following table shows on the left column Solidity types that are
not part of the ABI, and on the right column the ABI types that represent them.

```
Solidity ABI
address payable address
contract address
enum uint8
user defined value types its underlying value type
struct tuple
```
```
Warning: Before version0.8.0enums could have more than 256 members and were represented by the smallest
integer type just big enough to hold the value of any member.
```
**3.23.5 Design Criteria for the Encoding**

The encoding is designed to have the following properties, which are especially useful if some arguments are nested
arrays:

1. The number of reads necessary to access a value is at most the depth of the value inside the argument array
    structure, i.e. four reads are needed to retrievea_i[k][l][r]. In a previous version of the ABI, the number of
    reads scaled linearly with the total number of dynamic parameters in the worst case.
2. The data of a variable or an array element is not interleaved with other data and it is relocatable, i.e. it only uses
    relative “addresses”.

**3.23.6 Formal Specification of the Encoding**

We distinguish static and dynamic types. Static types are encoded in-place and dynamic types are encoded at a sepa-
rately allocated location after the current block.

**Definition:** The following types are called “dynamic”:

- bytes
- string
- T[]for anyT
- T[k]for any dynamicTand anyk >= 0
- (T1,...,Tk)ifTiis dynamic for some1 <= i <= k

**252 Chapter 3. Contents**


All other types are called “static”.

**Definition:** len(a)is the number of bytes in a binary stringa. The type oflen(a)is assumed to beuint256.

We defineenc, the actual encoding, as a mapping of values of the ABI types to binary strings such thatlen(enc(X))
depends on the value ofXif and only if the type ofXis dynamic.

**Definition:** For any ABI valueX, we recursively defineenc(X), depending on the type ofXbeing

- (T1,...,Tk)fork >= 0and any typesT1, ...,Tk
    enc(X) = head(X(1)) ... head(X(k)) tail(X(1)) ... tail(X(k))
    whereX = (X(1), ..., X(k))andheadandtailare defined forTias follows:
    ifTiis static:
       head(X(i)) = enc(X(i))andtail(X(i)) = ""(the empty string)
    otherwise, i.e. ifTiis dynamic:
       head(X(i)) = enc(len( head(X(1)) ... head(X(k)) tail(X(1)) ... tail(X(i-1))
       )) tail(X(i)) = enc(X(i))
    Note that in the dynamic case,head(X(i))is well-defined since the lengths of the head parts only depend on
    the types and not the values. The value ofhead(X(i))is the offset of the beginning oftail(X(i))relative to
    the start ofenc(X).
- T[k]for anyTandk:
    enc(X) = enc((X[0], ..., X[k-1]))
    i.e. it is encoded as if it were a tuple withkelements of the same type.
- T[]whereXhaskelements (kis assumed to be of typeuint256):
    enc(X) = enc(k) enc((X[0], ..., X[k-1]))
    i.e. it is encoded as if it were a tuple withkelements of the same type (resp. an array of static sizek), prefixed
    with the number of elements.
- bytes, of lengthk(which is assumed to be of typeuint256):
    enc(X) = enc(k) pad_right(X), i.e. the number of bytes is encoded as auint256followed by the actual
    value ofXas a byte sequence, followed by the minimum number of zero-bytes such thatlen(enc(X))is a
    multiple of 32.
- string:
    enc(X) = enc(enc_utf8(X)), i.e.Xis UTF-8 encoded and this value is interpreted as ofbytestype and
    encoded further. Note that the length used in this subsequent encoding is the number of bytes of the UTF-8
    encoded string, not its number of characters.
- uint<M>:enc(X)is the big-endian encoding ofX, padded on the higher-order (left) side with zero-bytes such
    that the length is 32 bytes.
- address: as in theuint160case
- int<M>:enc(X)is the big-endian two’s complement encoding ofX, padded on the higher-order (left) side with
    0xffbytes for negativeXand with zero-bytes for non-negativeXsuch that the length is 32 bytes.
- bool: as in theuint8case, where 1 is used fortrueand 0 forfalse
- fixed<M>x<N>:enc(X)isenc(X * 10**N)whereX * 10**Nis interpreted as aint256.
- fixed: as in thefixed128x18case
- ufixed<M>x<N>:enc(X)isenc(X * 10**N)whereX * 10**Nis interpreted as auint256.

**3.23. Contract ABI Specification 253**


- ufixed: as in theufixed128x18case
- bytes<M>:enc(X)is the sequence of bytes inXpadded with trailing zero-bytes to a length of 32 bytes.

Note that for anyX,len(enc(X))is a multiple of 32.

**3.23.7 Function Selector and Argument Encoding**

All in all, a call to the functionfwith parametersa_1, ..., a_nis encoded as

```
function_selector(f) enc((a_1, ..., a_n))
```
and the return valuesv_1, ..., v_koffare encoded as

```
enc((v_1, ..., v_k))
```
i.e. the values are combined into a tuple and encoded.

**3.23.8 Examples**

Given the contract:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

contract Foo{
functionbar(bytes3[2]memory)public pure {}
functionbaz(uint32 x,booly) public purereturns(boolr) { r = x > 32 || y; }
functionsam(bytesmemory,bool, uint[] memory)public pure {}
}

Thus, for ourFooexample, if we wanted to callbarwith the argument["abc", "def"], we would pass 68 bytes
total, broken down into:

- 0xfce353f6: the Method ID. This is derived from the signaturebar(bytes3[2]).
- 0x6162630000000000000000000000000000000000000000000000000000000000: the first part of the first
    parameter, abytes3value"abc"(left-aligned).
- 0x6465660000000000000000000000000000000000000000000000000000000000: the second part of the
    first parameter, abytes3value"def"(left-aligned).

In total:

0xfce353f661626300000000000000000000000000000000000000000000000000000000006465660000000000000000000000000000000000000000000000000000000000

If we wanted to callbazwith the parameters 69 andtrue, we would pass 68 bytes total, which can be broken down
into:

- 0xcdcd77c0: the Method ID. This is derived as the first 4 bytes of the Keccak hash of the ASCII form of the
    signaturebaz(uint32,bool).
- 0x0000000000000000000000000000000000000000000000000000000000000045: the first parameter, a
    uint32 value 69 padded to 32 bytes
- 0x0000000000000000000000000000000000000000000000000000000000000001: the second parameter -
    booleantrue, padded to 32 bytes

In total:

**254 Chapter 3. Contents**


0xcdcd77c000000000000000000000000000000000000000000000000000000000000000450000000000000000000000000000000000000000000000000000000000000001

It returns a singlebool. If, for example, it were to returnfalse, its output would be the single byte array
0x0000000000000000000000000000000000000000000000000000000000000000, a single bool.

If we wanted to callsamwith the arguments"dave",trueand[1,2,3], we would pass 292 bytes total, broken down
into:

- 0xa5643bf2: the Method ID. This is derived from the signaturesam(bytes,bool,uint256[]). Note that
    uintis replaced with its canonical representationuint256.
- 0x0000000000000000000000000000000000000000000000000000000000000060: the location of the data
    part of the first parameter (dynamic type), measured in bytes from the start of the arguments block. In this case,
    0x60.
- 0x0000000000000000000000000000000000000000000000000000000000000001: the second parameter:
    boolean true.
- 0x00000000000000000000000000000000000000000000000000000000000000a0: the location of the data
    part of the third parameter (dynamic type), measured in bytes. In this case,0xa0.
- 0x0000000000000000000000000000000000000000000000000000000000000004: the data part of the first
    argument, it starts with the length of the byte array in elements, in this case, 4.
- 0x6461766500000000000000000000000000000000000000000000000000000000: the contents of the first
    argument: the UTF-8 (equal to ASCII in this case) encoding of"dave", padded on the right to 32 bytes.
- 0x0000000000000000000000000000000000000000000000000000000000000003: the data part of the third
    argument, it starts with the length of the array in elements, in this case, 3.
- 0x0000000000000000000000000000000000000000000000000000000000000001: the first entry of the
    third parameter.
- 0x0000000000000000000000000000000000000000000000000000000000000002: the second entry of the
    third parameter.
- 0x0000000000000000000000000000000000000000000000000000000000000003: the third entry of the
    third parameter.

In total:

0xa5643bf20000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000000464617665000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000003

**3.23.9 Use of Dynamic Types**

A call to a function with the signaturef(uint256,uint32[],bytes10,bytes)with values(0x123, [0x456,
0x789], "1234567890", "Hello, world!")is encoded in the following way:

We take the first four bytes ofkeccak("f(uint256,uint32[],bytes10,bytes)"), i.e.0x8be65246. Then we
encode the head parts of all four arguments. For the static typesuint256andbytes10, these are directly the values
we want to pass, whereas for the dynamic typesuint32[]andbytes, we use the offset in bytes to the start of their
data area, measured from the start of the value encoding (i.e. not counting the first four bytes containing the hash of
the function signature). These are:

- 0x0000000000000000000000000000000000000000000000000000000000000123 (0x123 padded to 32
    bytes)
- 0x0000000000000000000000000000000000000000000000000000000000000080(offset to start of data
    part of second parameter, 4*32 bytes, exactly the size of the head part)

**3.23. Contract ABI Specification 255**


- 0x3132333435363738393000000000000000000000000000000000000000000000 ("1234567890"
    padded to 32 bytes on the right)
- 0x00000000000000000000000000000000000000000000000000000000000000e0(offset to start of data
    part of fourth parameter = offset to start of data part of first dynamic parameter + size of data part of first dynamic
    parameter = 4*32 + 3*32 (see below))

After this, the data part of the first dynamic argument,[0x456, 0x789]follows:

- 0x0000000000000000000000000000000000000000000000000000000000000002(number of elements of
    the array, 2)
- 0x0000000000000000000000000000000000000000000000000000000000000456(first element)
- 0x0000000000000000000000000000000000000000000000000000000000000789(second element)

Finally, we encode the data part of the second dynamic argument,"Hello, world!":

- 0x000000000000000000000000000000000000000000000000000000000000000d (number of elements
    (bytes in this case): 13)
- 0x48656c6c6f2c20776f726c642100000000000000000000000000000000000000 ("Hello, world!"
    padded to 32 bytes on the right)

All together, the encoding is (newline after function selector and each 32-bytes for clarity):

0x8be65246
0000000000000000000000000000000000000000000000000000000000000123
0000000000000000000000000000000000000000000000000000000000000080
3132333435363738393000000000000000000000000000000000000000000000
00000000000000000000000000000000000000000000000000000000000000e0
0000000000000000000000000000000000000000000000000000000000000002
0000000000000000000000000000000000000000000000000000000000000456
0000000000000000000000000000000000000000000000000000000000000789
000000000000000000000000000000000000000000000000000000000000000d
48656c6c6f2c20776f726c642100000000000000000000000000000000000000

Let us apply the same principle to encode the data for a function with a signatureg(uint256[][],string[])with
values([[1, 2], [3]], ["one", "two", "three"])but start from the most atomic parts of the encoding:

First we encode the length and data of the first embedded dynamic array[1, 2]of the first root array[[1, 2], [3]]:

- 0x0000000000000000000000000000000000000000000000000000000000000002(number of elements in
    the first array, 2; the elements themselves are 1 and 2 )
- 0x0000000000000000000000000000000000000000000000000000000000000001(first element)
- 0x0000000000000000000000000000000000000000000000000000000000000002(second element)

Then we encode the length and data of the second embedded dynamic array[3]of the first root array[[1, 2], [3]]:

- 0x0000000000000000000000000000000000000000000000000000000000000001(number of elements in
    the second array, 1; the element is 3 )
- 0x0000000000000000000000000000000000000000000000000000000000000003(first element)

Then we need to find the offsetsaandbfor their respective dynamic arrays[1, 2]and[3]. To calculate the offsets
we can take a look at the encoded data of the first root array[[1, 2], [3]]enumerating each line in the encoding:

0 - a - offset of [1, 2]
1 - b - offset of [3]
2 - 0000000000000000000000000000000000000000000000000000000000000002 - count for [1, 2]
(continues on next page)

**256 Chapter 3. Contents**


```
(continued from previous page)
```
3 - 0000000000000000000000000000000000000000000000000000000000000001 - encoding of 1
4 - 0000000000000000000000000000000000000000000000000000000000000002 - encoding of 2
5 - 0000000000000000000000000000000000000000000000000000000000000001 - count for [3]
6 - 0000000000000000000000000000000000000000000000000000000000000003 - encoding of 3

Offset a points to the start of the content of the array [1, 2] which is line 2 (64 bytes); thus a =
0x0000000000000000000000000000000000000000000000000000000000000040.

Offset b points to the start of the content of the array [3] which is line 5 (160 bytes); thus b =
0x00000000000000000000000000000000000000000000000000000000000000a0.

Then we encode the embedded strings of the second root array:

- 0x0000000000000000000000000000000000000000000000000000000000000003(number of characters in
    word"one")
- 0x6f6e650000000000000000000000000000000000000000000000000000000000(utf8 representation of
    word"one")
- 0x0000000000000000000000000000000000000000000000000000000000000003(number of characters in
    word"two")
- 0x74776f0000000000000000000000000000000000000000000000000000000000(utf8 representation of
    word"two")
- 0x0000000000000000000000000000000000000000000000000000000000000005(number of characters in
    word"three")
- 0x7468726565000000000000000000000000000000000000000000000000000000(utf8 representation of
    word"three")

In parallel to the first root array, since strings are dynamic elements we need to find their offsetsc,dande:

0 - c - offset for "one"
1 - d - offset for "two"
2 - e - offset for "three"
3 - 0000000000000000000000000000000000000000000000000000000000000003 - count for "one"
4 - 6f6e650000000000000000000000000000000000000000000000000000000000 - encoding of "one"
5 - 0000000000000000000000000000000000000000000000000000000000000003 - count for "two"
6 - 74776f0000000000000000000000000000000000000000000000000000000000 - encoding of "two"
7 - 0000000000000000000000000000000000000000000000000000000000000005 - count for "three"
8 - 7468726565000000000000000000000000000000000000000000000000000000 - encoding of "three
˓→"

Offset c points to the start of the content of the string "one" which is line 3 (96 bytes); thus c =
0x0000000000000000000000000000000000000000000000000000000000000060.

Offset d points to the start of the content of the string "two" which is line 5 (160 bytes); thus d =
0x00000000000000000000000000000000000000000000000000000000000000a0.

Offset e points to the start of the content of the string "three"which is line 7 (224 bytes); thus e =
0x00000000000000000000000000000000000000000000000000000000000000e0.

Note that the encodings of the embedded elements of the root arrays are not dependent on each other and have the same
encodings for a function with a signatureg(string[],uint256[][]).

Then we encode the length of the first root array:

- 0x0000000000000000000000000000000000000000000000000000000000000002(number of elements in
    the first root array, 2; the elements themselves are[1, 2]and[3])

**3.23. Contract ABI Specification 257**


Then we encode the length of the second root array:

- 0x0000000000000000000000000000000000000000000000000000000000000003(number of strings in the
    second root array, 3; the strings themselves are"one","two"and"three")

Finally we find the offsetsfandgfor their respective root dynamic arrays[[1, 2], [3]]and["one", "two",
"three"], and assemble parts in the correct order:

0x2289b18c - function␣
˓→signature
0 - f - offset of [[1,␣
˓→2], [3]]
1 - g - offset of ["one",
˓→"two", "three"]
2 - 0000000000000000000000000000000000000000000000000000000000000002 - count for [[1,␣
˓→2], [3]]
3 - 0000000000000000000000000000000000000000000000000000000000000040 - offset of [1, 2]
4 - 00000000000000000000000000000000000000000000000000000000000000a0 - offset of [3]
5 - 0000000000000000000000000000000000000000000000000000000000000002 - count for [1, 2]
6 - 0000000000000000000000000000000000000000000000000000000000000001 - encoding of 1
7 - 0000000000000000000000000000000000000000000000000000000000000002 - encoding of 2
8 - 0000000000000000000000000000000000000000000000000000000000000001 - count for [3]
9 - 0000000000000000000000000000000000000000000000000000000000000003 - encoding of 3
10 - 0000000000000000000000000000000000000000000000000000000000000003 - count for ["one",
˓→"two", "three"]
11 - 0000000000000000000000000000000000000000000000000000000000000060 - offset for "one"
12 - 00000000000000000000000000000000000000000000000000000000000000a0 - offset for "two"
13 - 00000000000000000000000000000000000000000000000000000000000000e0 - offset for "three
˓→"
14 - 0000000000000000000000000000000000000000000000000000000000000003 - count for "one"
15 - 6f6e650000000000000000000000000000000000000000000000000000000000 - encoding of "one"
16 - 0000000000000000000000000000000000000000000000000000000000000003 - count for "two"
17 - 74776f0000000000000000000000000000000000000000000000000000000000 - encoding of "two"
18 - 0000000000000000000000000000000000000000000000000000000000000005 - count for "three"
19 - 7468726565000000000000000000000000000000000000000000000000000000 - encoding of
˓→"three"

Offsetfpoints to the start of the content of the array[[1, 2], [3]]which is line 2 (64 bytes); thusf =
0x0000000000000000000000000000000000000000000000000000000000000040.

Offsetgpoints to the start of the content of the array["one", "two", "three"]which is line 10 (320 bytes); thus
g = 0x0000000000000000000000000000000000000000000000000000000000000140.

**3.23.10 Events**

Events are an abstraction of the Ethereum logging/event-watching protocol. Log entries provide the contract’s address,
a series of up to four topics and some arbitrary length binary data. Events leverage the existing function ABI in order
to interpret this (together with an interface spec) as a properly typed structure.

Given an event name and series of event parameters, we split them into two sub-series: those which are indexed and
those which are not. Those which are indexed, which may number up to 3 (for non-anonymous events) or 4 (for
anonymous ones), are used alongside the Keccak hash of the event signature to form the topics of the log entry. Those
which are not indexed form the byte array of the event.

In effect, a log entry using this ABI is described as:

**258 Chapter 3. Contents**


- address: the address of the contract (intrinsically provided by Ethereum);
- topics[0]: keccak(EVENT_NAME+"("+EVENT_ARGS.map(canonical_type_of).join(",")+")")
    (canonical_type_ofis a function that simply returns the canonical type of a given argument, e.g. foruint
    indexed foo, it would returnuint256). This value is only present intopics[0]if the event is not declared
    asanonymous;
- topics[n]: abi_encode(EVENT_INDEXED_ARGS[n - 1])if the event is not declared asanonymousor
    abi_encode(EVENT_INDEXED_ARGS[n])if it is (EVENT_INDEXED_ARGSis the series ofEVENT_ARGSthat
    are indexed);
- data: ABI encoding ofEVENT_NON_INDEXED_ARGS(EVENT_NON_INDEXED_ARGSis the series ofEVENT_ARGS
    that are not indexed,abi_encodeis the ABI encoding function used for returning a series of typed values from
    a function, as described above).

For all types of length at most 32 bytes, theEVENT_INDEXED_ARGSarray contains the value directly, padded or sign-
extended (for signed integers) to 32 bytes, just as for regular ABI encoding. However, for all “complex” types or types of
dynamic length, including all arrays,string,bytesand structs,EVENT_INDEXED_ARGSwill contain the _Keccak hash_
of a special in-place encoded value (see _Encoding of Indexed Event Parameters_ ), rather than the encoded value directly.
This allows applications to efficiently query for values of dynamic-length types (by setting the hash of the encoded value
as the topic), but leaves applications unable to decode indexed values they have not queried for. For dynamic-length
types, application developers face a trade-off between fast search for predetermined values (if the argument is indexed)
and legibility of arbitrary values (which requires that the arguments not be indexed). Developers may overcome this
tradeoff and achieve both efficient search and arbitrary legibility by defining events with two arguments — one indexed,
one not — intended to hold the same value.

**3.23.11 Errors**

In case of a failure inside a contract, the contract can use a special opcode to abort execution and revert all state changes.
In addition to these effects, descriptive data can be returned to the caller. This descriptive data is the encoding of an
error and its arguments in the same way as data for a function call.

As an example, let us consider the following contract whosetransferfunction always reverts with a custom error of
“insufficient balance”:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract TestToken{
error InsufficientBalance(uint256available,uint256required);
functiontransfer(address/*to*/, uintamount)publicpure {
revert InsufficientBalance(0, amount);
}
}

The return data would be encoded in the same way as the function callInsufficientBalance(0, amount)to the
functionInsufficientBalance(uint256,uint256), i.e.0xcf479181,uint256(0),uint256(amount).

The error selectors0x00000000and0xffffffffare reserved for future use.

```
Warning: Never trust error data. The error data by default bubbles up through the chain of external calls, which
means that a contract may receive an error not defined in any of the contracts it calls directly. Furthermore, any
contract can fake any error by returning data that matches an error signature, even if the error is not defined any-
where.
```
**3.23. Contract ABI Specification 259**


**3.23.12 JSON**

The JSON format for a contract’s interface is given by an array of function, event and error descriptions. A function
description is a JSON object with the fields:

- type:"function","constructor","receive"(the _“receive Ether” function_ ) or"fallback"(the _“de-_
    _fault” function_ );
- name: the name of the function;
- inputs: an array of objects, each of which contains:
    **-** name: the name of the parameter.
    **-** type: the canonical type of the parameter (more below).
    **-** components: used for tuple types (more below).
- outputs: an array of objects similar toinputs.
- stateMutability: a string with one of the following values:pure( _specified to not read blockchain state_ ),
    view( _specified to not modify the blockchain state_ ),nonpayable(function does not accept Ether - the default)
    andpayable(function accepts Ether).

Constructor, receive, and fallback never havenameoroutputs. Receive and fallback do not haveinputseither.

**Note:** Sending non-zero Ether to non-payable function will revert the transaction.

**Note:** The state mutabilitynonpayableis reflected in Solidity by not specifying a state mutability modifier at all.

An event description is a JSON object with fairly similar fields:

- type: always"event"
- name: the name of the event.
- inputs: an array of objects, each of which contains:
    **-** name: the name of the parameter.
    **-** type: the canonical type of the parameter (more below).
    **-** components: used for tuple types (more below).
    **-** indexed:trueif the field is part of the log’s topics,falseif it is one of the log’s data segments.
- anonymous:trueif the event was declared asanonymous.

Errors look as follows:

- type: always"error"
- name: the name of the error.
- inputs: an array of objects, each of which contains:
    **-** name: the name of the parameter.
    **-** type: the canonical type of the parameter (more below).
    **-** components: used for tuple types (more below).

**260 Chapter 3. Contents**


**Note:** There can be multiple errors with the same name and even with identical signature in the JSON array; for
example, if the errors originate from different files in the smart contract or are referenced from another smart contract.
For the ABI, only the name of the error itself is relevant and not where it is defined.

For example,

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract Test{
constructor() { b = hex"12345678901234567890123456789012"; }
eventEvent(uintindexed a,bytes32b);
eventEvent2(uintindexed a, bytes32b);
error InsufficientBalance(uint256available,uint256required);
functionfoo(uinta) public{ emit Event(a, b); }
bytes32b;
}

would result in the JSON:

[{
"type":"error",
"inputs": [{"name":"available","type":"uint256"},{"name":"required","type":"uint256"}],
"name":"InsufficientBalance"
}, {
"type":"event",
"inputs": [{"name":"a","type":"uint256","indexed":true},{"name":"b","type":"bytes32",
˓→"indexed":false}],
"name":"Event"
}, {
"type":"event",
"inputs": [{"name":"a","type":"uint256","indexed":true},{"name":"b","type":"bytes32",
˓→"indexed":false}],
"name":"Event2"
}, {
"type":"function",
"inputs": [{"name":"a","type":"uint256"}],
"name":"foo",
"outputs": []
}]

**3.23. Contract ABI Specification 261**


**Handling tuple types**

Despite the fact that names are intentionally not part of the ABI encoding, they do make a lot of sense to be included
in the JSON to enable displaying it to the end user. The structure is nested in the following way:

An object with membersname,typeand potentiallycomponentsdescribes a typed variable. The canonical type is
determined until a tuple type is reached and the string description up to that point is stored intypeprefix with the word
tuple, i.e. it will betuplefollowed by a sequence of[]and[k]with integersk. The components of the tuple are
then stored in the membercomponents, which is of an array type and has the same structure as the top-level object
except thatindexedis not allowed there.

As an example, the code

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.5 <0.9.0;
pragma abicoder v2;

contract Test{
struct S {uint a;uint[] b; T[] c; }
struct T {uint x;uinty; }
functionf(Smemory, Tmemory,uint)public pure {}
functiong()public purereturns(Smemory, Tmemory,uint) {}
}

would result in the JSON:

[
{
"name": "f",
"type": "function",
"inputs": [
{
"name": "s",
"type": "tuple",
"components": [
{
"name": "a",
"type": "uint256"
},
{
"name": "b",
"type": "uint256[]"
},
{
"name": "c",
"type": "tuple[]",
"components": [
{
"name": "x",
"type": "uint256"
},
{
"name": "y",
"type": "uint256"
}
(continues on next page)

**262 Chapter 3. Contents**


(continued from previous page)
]
}
]
},
{
"name": "t",
"type": "tuple",
"components": [
{
"name": "x",
"type": "uint256"
},
{
"name": "y",
"type": "uint256"
}
]
},
{
"name": "a",
"type": "uint256"
}
],
"outputs": []
}
]

**3.23.13 Strict Encoding Mode**

Strict encoding mode is the mode that leads to exactly the same encoding as defined in the formal specification above.
This means that offsets have to be as small as possible while still not creating overlaps in the data areas, and thus no
gaps are allowed.

Usually, ABI decoders are written in a straightforward way by just following offset pointers, but some decoders might
enforce strict mode. The Solidity ABI decoder currently does not enforce strict mode, but the encoder always creates
data in strict mode.

**3.23.14 Non-standard Packed Mode**

Throughabi.encodePacked(), Solidity supports a non-standard packed mode where:

- types shorter than 32 bytes are concatenated directly, without padding or sign extension
- dynamic types are encoded in-place and without the length.
- array elements are padded, but still encoded in-place

Furthermore, structs as well as nested arrays are not supported.

As an example, the encoding ofint16(-1), bytes1(0x42), uint16(0x03), string("Hello, world!")re-
sults in:

**3.23. Contract ABI Specification 263**


0xffff42000348656c6c6f2c20776f726c6421
^^^^ int16(-1)
^^ bytes1(0x42)
^^^^ uint16(0x03)
^^^^^^^^^^^^^^^^^^^^^^^^^^ string("Hello, world!") without a length field

More specifically:

- During the encoding, everything is encoded in-place. This means that there is no distinction between head and
    tail, as in the ABI encoding, and the length of an array is not encoded.
- The direct arguments ofabi.encodePackedare encoded without padding, as long as they are not arrays (or
    stringorbytes).
- The encoding of an array is the concatenation of the encoding of its elements **with** padding.
- Dynamically-sized types likestring,bytesoruint[]are encoded without their length field.
- The encoding ofstringorbytesdoes not apply padding at the end, unless it is part of an array or struct (then
    it is padded to a multiple of 32 bytes).

In general, the encoding is ambiguous as soon as there are two dynamically-sized elements, because of the missing
length field.

If padding is needed, explicit type conversions can be used:abi.encodePacked(uint16(0x12)) == hex"0012".

Since packed encoding is not used when calling functions, there is no special support for prepending a function selector.
Since the encoding is ambiguous, there is no decoding function.

```
Warning: If you usekeccak256(abi.encodePacked(a, b))and bothaandbare dynamic types, it is
easy to craft collisions in the hash value by moving parts ofaintoband vice-versa. More specifically,abi.
encodePacked("a", "bc") == abi.encodePacked("ab", "c"). If you useabi.encodePackedfor signa-
tures, authentication or data integrity, make sure to always use the same types and check that at most one of them
is dynamic. Unless there is a compelling reason,abi.encodeshould be preferred.
```
**3.23.15 Encoding of Indexed Event Parameters**

Indexed event parameters that are not value types, i.e. arrays and structs are not stored directly but instead a Keccak-256
hash of an encoding is stored. This encoding is defined as follows:

- the encoding of abytesandstringvalue is just the string contents without any padding or length prefix.
- the encoding of a struct is the concatenation of the encoding of its members, always padded to a multiple of 32
    bytes (evenbytesandstring).
- the encoding of an array (both dynamically- and statically-sized) is the concatenation of the encoding of its
    elements, always padded to a multiple of 32 bytes (evenbytesandstring) and without any length prefix

In the above, as usual, a negative number is padded by sign extension and not zero padded.bytesNNtypes are padded
on the right whileuintNN/intNNare padded on the left.

```
Warning: The encoding of a struct is ambiguous if it contains more than one dynamically-sized array. Because
of that, always re-check the event data and do not rely on the search result based on the indexed parameters alone.
```
**264 Chapter 3. Contents**


### 3.24 Security Considerations

While it is usually quite easy to build software that works as expected, it is much harder to check that nobody can use
it in a way that was **not** anticipated.

In Solidity, this is even more important because you can use smart contracts to handle tokens or, possibly, even more
valuable things. Furthermore, every execution of a smart contract happens in public and, in addition to that, the source
code is often available.

Of course, you always have to consider how much is at stake: You can compare a smart contract with a web service that
is open to the public (and thus, also to malicious actors) and perhaps even open-source. If you only store your grocery
list on that web service, you might not have to take too much care, but if you manage your bank account using that web
service, you should be more careful.

This section will list some pitfalls and general security recommendations but can, of course, never be complete. Also,
keep in mind that even if your smart contract code is bug-free, the compiler or the platform itself might have a bug. A
list of some publicly known security-relevant bugs of the compiler can be found in the _list of known bugs_ , which is also
machine-readable. Note that there is a Bug Bounty Program that covers the code generator of the Solidity compiler.

As always, with open-source documentation, please help us extend this section (especially, some examples would not
hurt)!

NOTE: In addition to the list below, you can find more security recommendations and best practices in Guy Lando’s
knowledge list and the Consensys GitHub repo.

**3.24.1 Pitfalls**

**Private Information and Randomness**

Everything you use in a smart contract is publicly visible, even local variables and state variables markedprivate.

Using random numbers in smart contracts is quite tricky if you do not want block builders to be able to cheat.

**Reentrancy**

Any interaction from a contract (A) with another contract (B) and any transfer of Ether hands over control to that
contract (B). This makes it possible for B to call back into A before this interaction is completed. To give an example,
the following code contains a bug (it is just a snippet and not a complete contract):

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

// THIS CONTRACT CONTAINS A BUG - DO NOT USE
contract Fund{
/// @dev Mapping of ether shares of the contract.
mapping(address=>uint) shares;
/// Withdraw your share.
functionwithdraw() public{
if (payable(msg.sender).send(shares[msg.sender]))
shares[msg.sender] = 0;
}
}

The problem is not too serious here because of the limited gas as part ofsend, but it still exposes a weakness: Ether
transfer can always include code execution, so the recipient could be a contract that calls back intowithdraw. This

**3.24. Security Considerations 265**


would let it get multiple refunds and, basically, retrieve all the Ether in the contract. In particular, the following contract
will allow an attacker to refund multiple times as it usescallwhich forwards all remaining gas by default:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.2 <0.9.0;

// THIS CONTRACT CONTAINS A BUG - DO NOT USE
contract Fund{
/// @dev Mapping of ether shares of the contract.
mapping(address=>uint) shares;
/// Withdraw your share.
functionwithdraw() public{
(boolsuccess,) =msg.sender.call{value: shares[msg.sender]}("");
if (success)
shares[msg.sender] = 0;
}
}

To avoid reentrancy, you can use the Checks-Effects-Interactions pattern as demonstrated below:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Fund{
/// @dev Mapping of ether shares of the contract.
mapping(address=>uint) shares;
/// Withdraw your share.
functionwithdraw() public{
uintshare = shares[msg.sender];
shares[msg.sender] = 0;
payable(msg.sender).transfer(share);
}
}

The Checks-Effects-Interactions pattern ensures that all code paths through a contract complete all required checks of
the supplied parameters before modifying the contract’s state (Checks); only then it makes any changes to the state
(Effects); it may make calls to functions in other contracts _after_ all planned state changes have been written to storage
(Interactions). This is a common foolproof way to prevent _reentrancy attacks_ , where an externally called malicious
contract can double-spend an allowance, double-withdraw a balance, among other things, by using logic that calls back
into the original contract before it has finalized its transaction.

Note that reentrancy is not only an effect of Ether transfer but of any function call on another contract. Furthermore,
you also have to take multi-contract situations into account. A called contract could modify the state of another contract
you depend on.

**266 Chapter 3. Contents**


**Gas Limit and Loops**

Loops that do not have a fixed number of iterations, for example, loops that depend on storage values, have to be used
carefully: Due to the block gas limit, transactions can only consume a certain amount of gas. Either explicitly or just
due to normal operation, the number of iterations in a loop can grow beyond the block gas limit which can cause the
complete contract to be stalled at a certain point. This may not apply toviewfunctions that are only executed to read
data from the blockchain. Still, such functions may be called by other contracts as part of on-chain operations and stall
those. Please be explicit about such cases in the documentation of your contracts.

**Sending and Receiving Ether**

- Neither contracts nor “external accounts” are currently able to prevent someone from sending them Ether. Con-
    tracts can react on and reject a regular transfer, but there are ways to move Ether without creating a message call.
    One way is to simply “mine to” the contract address and the second way is usingselfdestruct(x).
- If a contract receives Ether (without a function being called), either the _receive Ether_ or the _fallback_ function is
    executed. If it does not have areceivenor afallbackfunction, the Ether will be rejected (by throwing an
    exception). During the execution of one of these functions, the contract can only rely on the “gas stipend” it is
    passed (2300 gas) being available to it at that time. This stipend is not enough to modify storage (do not take this
    for granted though, the stipend might change with future hard forks). To be sure that your contract can receive
    Ether in that way, check the gas requirements of the receive and fallback functions (for example in the “details”
    section in Remix).
- There is a way to forward more gas to the receiving contract usingaddr.call{value: x}(""). This is
    essentially the same asaddr.transfer(x), only that it forwards all remaining gas and opens up the ability for
    the recipient to perform more expensive actions (and it returns a failure code instead of automatically propagating
    the error). This might include calling back into the sending contract or other state changes you might not have
    thought of. So it allows for great flexibility for honest users but also for malicious actors.
- Use the most precise units to represent the Wei amount as possible, as you lose any that is rounded due to a lack
    of precision.
- If you want to send Ether usingaddress.transfer, there are certain details to be aware of:
    1. If the recipient is a contract, it causes its receive or fallback function to be executed which can, in turn, call
       back the sending contract.
    2. Sending Ether can fail due to the call depth going above 1024. Since the caller is in total control of the
       call depth, they can force the transfer to fail; take this possibility into account or usesendand make sure
       to always check its return value. Better yet, write your contract using a pattern where the recipient can
       withdraw Ether instead.
    3. Sending Ether can also fail because the execution of the recipient contract requires more than the allotted
       amount of gas (explicitly by using _require_ , _assert_ , _revert_ or because the operation is too expensive) - it
       “runs out of gas” (OOG). If you usetransferorsendwith a return value check, this might provide a
       means for the recipient to block progress in the sending contract. Again, the best practice here is to use a
       _“withdraw” pattern instead of a “send” pattern_.

**3.24. Security Considerations 267**


**Call Stack Depth**

External function calls can fail at any time because they exceed the maximum call stack size limit of 1024. In such
situations, Solidity throws an exception. Malicious actors might be able to force the call stack to a high value before
they interact with your contract. Note that, since Tangerine Whistle hardfork, the 63/64 rule makes call stack depth
attack impractical. Also note that the call stack and the expression stack are unrelated, even though both have a size
limit of 1024 stack slots.

Note that.send()does **not** throw an exception if the call stack is depleted but rather returnsfalsein that case. The
low-level functions.call(),.delegatecall()and.staticcall()behave in the same way.

**Authorized Proxies**

If your contract can act as a proxy, i.e. if it can call arbitrary contracts with user-supplied data, then the user can
essentially assume the identity of the proxy contract. Even if you have other protective measures in place, it is best to
build your contract system such that the proxy does not have any permissions (not even for itself). If needed, you can
accomplish that using a second proxy:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;
contract ProxyWithMoreFunctionality{
PermissionlessProxy proxy;

functioncallOther(addressaddr, bytesmemory payload) public
returns(bool,bytes memory) {
returnproxy.callOther(addr, payload);
}
// Other functions and other functionality
}

// This is the full contract, it has no other functionality and
// requires no privileges to work.
contract PermissionlessProxy {
functioncallOther(addressaddr, bytesmemory payload) public
returns(bool,bytes memory) {
returnaddr.call(payload);
}
}

**tx.origin**

Never usetx.originfor authorization. Let’s say you have a wallet contract like this:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
// THIS CONTRACT CONTAINS A BUG - DO NOT USE
contract TxUserWallet{
addressowner;

```
constructor() {
owner =msg.sender;
}
(continues on next page)
```
**268 Chapter 3. Contents**


```
(continued from previous page)
```
functiontransferTo(addresspayable dest, uintamount)public{
// THE BUG IS RIGHT HERE, you must use msg.sender instead of tx.origin
require(tx.origin== owner);
dest.transfer(amount);
}
}

Now someone tricks you into sending Ether to the address of this attack wallet:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
interface TxUserWallet {
functiontransferTo(addresspayable dest, uintamount)external;
}

contract TxAttackWallet {
addresspayable owner;

```
constructor() {
owner =payable(msg.sender);
}
```
receive()external payable{
TxUserWallet(msg.sender).transferTo(owner, msg.sender.balance);
}
}

If your wallet had checkedmsg.senderfor authorization, it would get the address of the attack wallet, instead of the
owner’s address. But by checkingtx.origin, it gets the original address that kicked off the transaction, which is still
the owner’s address. The attack wallet instantly drains all your funds.

**Two’s Complement / Underflows / Overflows**

As in many programming languages, Solidity’s integer types are not actually integers. They resemble integers when
the values are small, but cannot represent arbitrarily large numbers.

The following code causes an overflow because the result of the addition is too large to be stored in the typeuint8:

uint8x = 255;
uint8y = 1;
return x + y;

Solidity has two modes in which it deals with these overflows: Checked and Unchecked or “wrapping” mode.

The default checked mode will detect overflows and cause a failing assertion. You can disable this check using
unchecked { ... }, causing the overflow to be silently ignored. The above code would return 0 if wrapped in
unchecked { ... }.

Even in checked mode, do not assume you are protected from overflow bugs. In this mode, overflows will always revert.
If it is not possible to avoid the overflow, this can lead to a smart contract being stuck in a certain state.

In general, read about the limits of two’s complement representation, which even has some more special edge cases for
signed numbers.

**3.24. Security Considerations 269**


Try to userequireto limit the size of inputs to a reasonable range and use the _SMT checker_ to find potential overflows.

**Clearing Mappings**

The Solidity typemapping(see _Mapping Types_ ) is a storage-only key-value data structure that does not keep track of
the keys that were assigned a non-zero value. Because of that, cleaning a mapping without extra information about
the written keys is not possible. If amappingis used as the base type of a dynamic storage array, deleting or popping
the array will have no effect over themappingelements. The same happens, for example, if amappingis used as the
type of a member field of astructthat is the base type of a dynamic storage array. Themappingis also ignored in
assignments of structs or arrays containing amapping.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

contract Map{
mapping(uint=> uint)[] array;

```
functionallocate(uintnewMaps)public {
for(uinti = 0; i < newMaps; i++)
array.push();
}
```
```
functionwriteMap(uintmap,uint key,uintvalue)public {
array[map][key] = value;
}
```
```
functionreadMap(uintmap,uintkey)public viewreturns(uint) {
returnarray[map][key];
}
```
functioneraseMaps()public{
delete array;
}
}

Consider the example above and the following sequence of calls:allocate(10),writeMap(4, 128, 256). At this
point, callingreadMap(4, 128)returns 256. If we calleraseMaps, the length of the state variablearrayis zeroed,
but since itsmappingelements cannot be zeroed, their information stays alive in the contract’s storage. After deleting
array, callingallocate(5)allows us to accessarray[4]again, and callingreadMap(4, 128)returns 256 even
without another call towriteMap.

If yourmappinginformation must be deleted, consider using a library similar to iterable mapping, allowing you to
traverse the keys and delete their values in the appropriatemapping.

**270 Chapter 3. Contents**


**Minor Details**

- Types that do not occupy the full 32 bytes might contain “dirty higher order bits”. This is especially important if
    you accessmsg.data- it poses a malleability risk: You can craft transactions that call a functionf(uint8 x)
    with a raw byte argument of0xff000001and with0x00000001. Both are fed to the contract and both will look
    like the number 1 as far asxis concerned, butmsg.datawill be different, so if you usekeccak256(msg.data)
    for anything, you will get different results.

**3.24.2 Recommendations**

**Take Warnings Seriously**

If the compiler warns you about something, you should change it. Even if you do not think that this particular warning
has security implications, there might be another issue buried beneath it. Any compiler warning we issue can be
silenced by slight changes to the code.

Always use the latest version of the compiler to be notified about all recently introduced warnings.

Messages of typeinfo, issued by the compiler, are not dangerous and simply represent extra suggestions and optional
information that the compiler thinks might be useful to the user.

**Restrict the Amount of Ether**

Restrict the amount of Ether (or other tokens) that can be stored in a smart contract. If your source code, the compiler
or the platform has a bug, these funds may be lost. If you want to limit your loss, limit the amount of Ether.

**Keep it Small and Modular**

Keep your contracts small and easily understandable. Single out unrelated functionality in other contracts or into
libraries. General recommendations about the source code quality of course apply: Limit the amount of local variables,
the length of functions and so on. Document your functions so that others can see what your intention was and whether
it is different than what the code does.

**Use the Checks-Effects-Interactions Pattern**

Most functions will first perform some checks and they should be done first (who called the function, are the arguments
in range, did they send enough Ether, does the person have tokens, etc.).

As the second step, if all checks passed, effects to the state variables of the current contract should be made. Interaction
with other contracts should be the very last step in any function.

Early contracts delayed some effects and waited for external function calls to return in a non-error state. This is often
a serious mistake because of the reentrancy problem explained above.

Note that, also, calls to known contracts might in turn cause calls to unknown contracts, so it is probably better to just
always apply this pattern.

**3.24. Security Considerations 271**


**Include a Fail-Safe Mode**

While making your system fully decentralized will remove any intermediary, it might be a good idea, especially for
new code, to include some kind of fail-safe mechanism:

You can add a function in your smart contract that performs some self-checks like “Has any Ether leaked?”, “Is the
sum of the tokens equal to the balance of the contract?” or similar things. Keep in mind that you cannot use too much
gas for that, so help through off-chain computations might be needed there.

If the self-check fails, the contract automatically switches into some kind of “failsafe” mode, which, for example,
disables most of the features, hands over control to a fixed and trusted third party or just converts the contract into a
simple “give me back my Ether” contract.

**Ask for Peer Review**

The more people examine a piece of code, the more issues are found. Asking people to review your code also helps as
a cross-check to find out whether your code is easy to understand - a very important criterion for good smart contracts.

### 3.25 List of Known Bugs

Below, you can find a JSON-formatted list of some of the known security-relevant bugs in the Solidity compiler. The
file itself is hosted in the GitHub repository. The list stretches back as far as version 0.3.0, bugs known to be present
only in versions preceding that are not listed.

There is another file called bugs_by_version.json, which can be used to check which bugs affect a specific version of
the compiler.

Contract source verification tools and also other tools interacting with contracts should consult this list according to
the following criteria:

- It is mildly suspicious if a contract was compiled with a nightly compiler version instead of a released version.
    This list does not keep track of unreleased or nightly versions.
- It is also mildly suspicious if a contract was compiled with a version that was not the most recent at the time the
    contract was created. For contracts created from other contracts, you have to follow the creation chain back to a
    transaction and use the date of that transaction as creation date.
- It is highly suspicious if a contract was compiled with a compiler that contains a known bug and the contract was
    created at a time where a newer compiler version containing a fix was already released.

The JSON file of known bugs below is an array of objects, one for each bug, with the following keys:

**uid**
Unique identifier given to the bug in the form ofSOL-<year>-<number>. It is possible that multiple entries
exists with the same uid. This means multiple version ranges are affected by the same bug.

**name**
Unique name given to the bug

**summary**
Short description of the bug

**description**
Detailed description of the bug

**link**
URL of a website with more detailed information, optional

**272 Chapter 3. Contents**


**introduced**
The first published compiler version that contained the bug, optional

**fixed**
The first published compiler version that did not contain the bug anymore

**publish**
The date at which the bug became known publicly, optional

**severity**
Severity of the bug: very low, low, medium, high. Takes into account discoverability in contract tests, likelihood
of occurrence and potential damage by exploits.

**conditions**
Conditions that have to be met to trigger the bug. The following keys can be used:optimizer, Boolean value
which means that the optimizer has to be switched on to enable the bug.evmVersion, a string that indicates
which EVM version compiler settings trigger the bug. The string can contain comparison operators. For example,
">=constantinople"means that the bug is present when the EVM version is set toconstantinopleor later.
If no conditions are given, assume that the bug is present.

**check**
This field contains different checks that report whether the smart contract contains the bug or not. The first type
of check are JavaScript regular expressions that are to be matched against the source code (“source-regex”) if the
bug is present. If there is no match, then the bug is very likely not present. If there is a match, the bug might be
present. For improved accuracy, the checks should be applied to the source code after stripping comments. The
second type of check are patterns to be checked on the compact AST of the Solidity program (“ast-compact-json-
path”). The specified search query is a JsonPath expression. If at least one path of the Solidity AST matches the
query, the bug is likely present.

[
{
"uid": "SOL-2023-3",
"name": "VerbatimInvalidDeduplication",
"summary": "All ``verbatim`` blocks are considered identical by deduplicator and␣
˓→can incorrectly be unified when surrounded by identical opcodes.",
"description": "The block deduplicator is a step of the opcode-based optimizer␣
˓→which identifies equivalent assembly blocks and merges them into a single one. However,
˓→when blocks contained``verbatim``, their comparison was performed incorrectly,␣
˓→leading to the collapse of assembly blocks which are identical except for the contents␣
˓→of the ``verbatim`` items. Since``verbatim`` is only available in Yul, compilation of␣
˓→Solidity sources is not affected.",
"link": "https://blog.soliditylang.org/2023/11/08/verbatim-invalid-deduplication-
˓→bug/",
"introduced": "0.8.5",
"fixed": "0.8.23",
"severity": "low"
},
{
"uid": "SOL-2023-2",
"name": "FullInlinerNonExpressionSplitArgumentEvaluationOrder",
"summary": "Optimizer sequences containing FullInliner do not preserve the␣
˓→evaluation order of arguments of inlined function calls in code that is not in␣
˓→expression-split form.",
"description": "Function call arguments in Yul are evaluated right to left. This␣
˓→order matters when the argument expressions have side-effects, and changing it may␣
˓→change contract behavior. FullInliner is an optimizer step that can replace a function␣
(continues on next page)

**3.25. List of Known Bugs 273**


```
(continued from previous page)
˓→call with the body of that function. The transformation involves assigning argument␣
˓→expressions to temporary variables, which imposes an explicit evaluation order.␣
˓→FullInliner was written with the assumption that this order does not necessarily have␣
˓→to match usual argument evaluation order because the argument expressions have no side-
˓→effects. In most circumstances this assumption is true because the default␣
˓→optimization step sequence contains the ExpressionSplitter step. ExpressionSplitter␣
˓→ensures that the code is in *expression-split form*, which means that function calls␣
˓→cannot appear nested inside expressions, and all function call arguments have to be␣
˓→variables. The assumption is, however, not guaranteed to be true in general. Version 0.
˓→6.7 introduced a setting allowing users to specify an arbitrary optimization step␣
˓→sequence, making it possible for the FullInliner to actually encounter argument␣
˓→expressions with side-effects, which can result in behavior differences between␣
˓→optimized and unoptimized bytecode. Contracts compiled without optimization or with␣
˓→the default optimization sequence are not affected. To trigger the bug the user has to␣
˓→explicitly choose compiler settings that contain a sequence with FullInliner step not␣
˓→preceded by ExpressionSplitter.",
"link": "https://blog.soliditylang.org/2023/07/19/full-inliner-non-expression-
˓→split-argument-evaluation-order-bug/",
"introduced": "0.6.7",
"fixed": "0.8.21",
"severity": "low",
"conditions": {
"yulOptimizer":true
}
},
{
"uid": "SOL-2023-1",
"name": "MissingSideEffectsOnSelectorAccess",
"summary": "Accessing the``.selector`` member on complex expressions leaves the␣
˓→expression unevaluated in the legacy code generation.",
"description": "When accessing the``.selector`` member on an expression with␣
˓→side-effects, like an assignment, a function call or a conditional, the expression␣
˓→would not be evaluated in the legacy code generation. This would happen in expressions␣
˓→where the functions used in the expression were all known at compilation time,␣
˓→regardless of whether the whole expression could be evaluated at compilation time or␣
˓→not. Note that the code generated by the IR pipeline was unaffected and would behave␣
˓→as expected.",
"link": "https://blog.soliditylang.org/2023/07/19/missing-side-effects-on-
˓→selector-access-bug/",
"introduced": "0.6.2",
"fixed": "0.8.21",
"severity": "low",
"conditions": {
"viaIR":false
}
},
{
"uid": "SOL-2022-7",
"name": "StorageWriteRemovalBeforeConditionalTermination",
"summary": "Calling functions that conditionally terminate the external EVM call␣
˓→using the assembly statements``return(...)`` or ``stop()``may result in incorrect␣
˓→removals of prior storage writes.",
(continues on next page)
```
**274 Chapter 3. Contents**


```
(continued from previous page)
"description": "A call to a Yul function that conditionally terminates the␣
˓→external EVM call could result in prior storage writes being incorrectly removed by␣
˓→the Yul optimizer. This used to happen in cases in which it would have been valid to␣
˓→remove the store, if the Yul function in question never actually terminated the␣
˓→external call, and the control flow always returned back to the caller instead.␣
˓→Conditional termination within the same Yul block instead of within a called function␣
˓→was not affected. In Solidity with optimized via-IR code generation, any storage write␣
˓→before a function conditionally calling ``return(...)``or ``stop()`` in inline␣
˓→assembly, may have been incorrectly removed, whenever it would have been valid to␣
˓→remove the write without the ``return(...)`` or ``stop()``. In optimized legacy code␣
˓→generation, only inline assembly that did not refer to any Solidity variables and that␣
˓→involved conditionally-terminating user-defined assembly functions could be affected.",
"link": "https://blog.soliditylang.org/2022/09/08/storage-write-removal-before-
˓→conditional-termination/",
"introduced": "0.8.13",
"fixed": "0.8.17",
"severity": "medium/high",
"conditions": {
"yulOptimizer":true
}
},
{
"uid": "SOL-2022-6",
"name": "AbiReencodingHeadOverflowWithStaticArrayCleanup",
"summary": "ABI-encoding a tuple with a statically-sized calldata array in the␣
˓→last component would corrupt 32 leading bytes of its first dynamically encoded␣
˓→component.",
"description": "When ABI-encoding a statically-sized calldata array, the␣
˓→compiler always pads the data area to a multiple of 32-bytes and ensures that the␣
˓→padding bytes are zeroed. In some cases, this cleanup used to be performed by always␣
˓→writing exactly 32 bytes, regardless of how many needed to be zeroed. This was done␣
˓→with the assumption that the data that would eventually occupy the area past the end␣
˓→of the array had not yet been written, because the encoder processes tuple components␣
˓→in the order they were given. While this assumption is mostly true, there is an␣
˓→important corner case: dynamically encoded tuple components are stored separately from␣
˓→the statically-sized ones in an area called the *tail* of the encoding and the tail␣
˓→immediately follows the *head*, which is where the statically-sized components are␣
˓→placed. The aforementioned cleanup, if performed for the last component of the head␣
˓→would cross into the tail and overwrite up to 32 bytes of the first component stored␣
˓→there with zeros. The only array type for which the cleanup could actually result in␣
˓→an overwrite were arrays with``uint256`` or ``bytes32`` as the base element type and␣
˓→in this case the size of the corrupted area was always exactly 32 bytes. The problem␣
˓→affected tuples at any nesting level. This included also structs, which are encoded as␣
˓→tuples in the ABI. Note also that lists of parameters and return values of functions,␣
˓→events and errors are encoded as tuples.",
"link": "https://blog.soliditylang.org/2022/08/08/calldata-tuple-reencoding-head-
˓→overflow-bug/",
"introduced": "0.5.8",
"fixed": "0.8.16",
"severity": "medium",
"conditions": {
"ABIEncoderV2":true
(continues on next page)
```
**3.25. List of Known Bugs 275**


```
(continued from previous page)
}
},
{
"uid": "SOL-2022-5",
"name": "DirtyBytesArrayToStorage",
"summary": "Copying``bytes`` arrays from memory or calldata to storage may␣
˓→result in dirty storage values.",
"description": "Copying``bytes`` arrays from memory or calldata to storage is␣
˓→done in chunks of 32 bytes even if the length is not a multiple of 32. Thereby, extra␣
˓→bytes past the end of the array may be copied from calldata or memory to storage.␣
˓→These dirty bytes may then become observable after a ``.push()``without arguments to␣
˓→the bytes array in storage, i.e. such a push will not result in a zero value at the␣
˓→end of the array as expected. This bug only affects the legacy code generation␣
˓→pipeline, the new code generation pipeline via IR is not affected.",
"link": "https://blog.soliditylang.org/2022/06/15/dirty-bytes-array-to-storage-
˓→bug/",
"introduced": "0.0.1",
"fixed": "0.8.15",
"severity": "low"
},
{
"uid": "SOL-2022-4",
"name": "InlineAssemblyMemorySideEffects",
"summary": "The Yul optimizer may incorrectly remove memory writes from inline␣
˓→assembly blocks, that do not access solidity variables.",
"description": "The Yul optimizer considers all memory writes in the outermost␣
˓→Yul block that are never read from as unused and removes them. This is valid when that␣
˓→Yul block is the entire Yul program, which is always the case for the Yul code␣
˓→generated by the new via-IR pipeline. Inline assembly blocks are never optimized in␣
˓→isolation when using that pipeline. Instead they are optimized as a part of the whole␣
˓→Yul input. However, the legacy code generation pipeline (which is still the default)␣
˓→runs the Yul optimizer individually on an inline assembly block if the block does not␣
˓→refer to any local variables defined in the surrounding Solidity code. Consequently,␣
˓→memory writes in such inline assembly blocks are removed as well, if the written␣
˓→memory is never read from in the same assembly block, even if the written memory is␣
˓→accessed later, for example by a subsequent inline assembly block.",
"link": "https://blog.soliditylang.org/2022/06/15/inline-assembly-memory-side-
˓→effects-bug/",
"introduced": "0.8.13",
"fixed": "0.8.15",
"severity": "medium",
"conditions": {
"yulOptimizer":true
}
},
{
"uid": "SOL-2022-3",
"name": "DataLocationChangeInInternalOverride",
"summary": "It was possible to change the data location of the parameters or␣
˓→return variables from ``calldata`` to``memory`` and vice-versa while overriding␣
˓→internal and public functions. This caused invalid code to be generated when calling␣
˓→such a function internally through virtual function calls.",
(continues on next page)
```
**276 Chapter 3. Contents**


```
(continued from previous page)
"description": "When calling external functions, it is irrelevant if the data␣
˓→location of the parameters is``calldata``or ``memory``, the encoding of the data␣
˓→does not change. Because of that, changing the data location when overriding external␣
˓→functions is allowed. The compiler incorrectly also allowed a change in the data␣
˓→location for overriding public and internal functions. Since public functions can be␣
˓→called internally as well as externally, this causes invalid code to be generated when␣
˓→such an incorrectly overridden function is called internally through the base contract.
˓→The caller provides a memory pointer, but the called function interprets it as a␣
˓→calldata pointer or vice-versa.",
"link": "https://blog.soliditylang.org/2022/05/17/data-location-inheritance-bug/
˓→",
"introduced": "0.6.9",
"fixed": "0.8.14",
"severity": "very low"
},
{
"uid": "SOL-2022-2",
"name": "NestedCalldataArrayAbiReencodingSizeValidation",
"summary": "ABI-reencoding of nested dynamic calldata arrays did not always␣
˓→perform proper size checks against the size of calldata and could read beyond␣
˓→``calldatasize()``.",
"description": "Calldata validation for nested dynamic types is deferred until␣
˓→the first access to the nested values. Such an access may for example be a copy to␣
˓→memory or an index or member access to the outer type. While in most such accesses␣
˓→calldata validation correctly checks that the data area of the nested array is␣
˓→completely contained in the passed calldata (i.e. in the range [0, calldatasize()]),␣
˓→this check may not be performed, when ABI encoding such nested types again directly␣
˓→from calldata. For instance, this can happen, if a value in calldata with a nested␣
˓→dynamic array is passed to an external call, used in ``abi.encode`` or emitted as␣
˓→event. In such cases, if the data area of the nested array extends beyond␣
˓→``calldatasize()``, ABI encoding it did not revert, but continued reading values from␣
˓→beyond ``calldatasize()``(i.e. zero values).",
"link": "https://blog.soliditylang.org/2022/05/17/calldata-reencode-size-check-
˓→bug/",
"introduced": "0.5.8",
"fixed": "0.8.14",
"severity": "very low"
},
{
"uid": "SOL-2022-1",
"name": "AbiEncodeCallLiteralAsFixedBytesBug",
"summary": "Literals used for a fixed length bytes parameter in``abi.
˓→encodeCall``were encoded incorrectly.",
"description": "For the encoding, the compiler only considered the types of the␣
˓→expressions in the second argument of``abi.encodeCall`` itself, but not the parameter␣
˓→types of the function given as first argument. In almost all cases the abi encoding of␣
˓→the type of the expression matches the abi encoding of the parameter type of the given␣
˓→function. This is because the type checker ensures the expression is implicitly␣
˓→convertible to the respective parameter type. However this is not true for number␣
˓→literals used for fixed bytes types shorter than 32 bytes, nor for string literals␣
˓→used for any fixed bytes type. Number literals were encoded as numbers instead of␣
˓→being shifted to become left-aligned. String literals were encoded as dynamically␣
(continues on next page)
```
**3.25. List of Known Bugs 277**


```
(continued from previous page)
˓→sized memory strings instead of being converted to a left-aligned bytes value.",
"link": "https://blog.soliditylang.org/2022/03/16/encodecall-bug/",
"introduced": "0.8.11",
"fixed": "0.8.13",
"severity": "very low"
```
```
},
{
"uid": "SOL-2021-4",
"name": "UserDefinedValueTypesBug",
"summary": "User defined value types with underlying type shorter than 32 bytes␣
˓→used incorrect storage layout and wasted storage",
"description": "The compiler did not correctly compute the storage layout of␣
˓→user defined value types based on types that are shorter than 32 bytes. It would␣
˓→always use a full storage slot for these types, even if the underlying type was␣
˓→shorter. This was wasteful and might have problems with tooling or contract upgrades.",
"link": "https://blog.soliditylang.org/2021/09/29/user-defined-value-types-bug/",
"introduced": "0.8.8",
"fixed": "0.8.9",
"severity": "very low"
},
{
"uid": "SOL-2021-3",
"name": "SignedImmutables",
"summary": "Immutable variables of signed integer type shorter than 256 bits can␣
˓→lead to values with invalid higher order bits if inline assembly is used.",
"description": "When immutable variables of signed integer type shorter than 256␣
˓→bits are read, their higher order bits were unconditionally set to zero. The correct␣
˓→operation would be to sign-extend the value, i.e. set the higher order bits to one if␣
˓→the sign bit is one. This sign-extension is performed by Solidity just prior to when␣
˓→it matters, i.e. when a value is stored in memory, when it is compared or when a␣
˓→division is performed. Because of that, to our knowledge, the only way to access the␣
˓→value in its unclean state is by reading it through inline assembly.",
"link": "https://blog.soliditylang.org/2021/09/29/signed-immutables-bug/",
"introduced": "0.6.5",
"fixed": "0.8.9",
"severity": "very low"
},
{
"uid": "SOL-2021-2",
"name": "ABIDecodeTwoDimensionalArrayMemory",
"summary": "If used on memory byte arrays, result of the function``abi.decode``␣
˓→can depend on the contents of memory outside of the actual byte array that is decoded.
˓→",
"description": "The ABI specification uses pointers to data areas for everything␣
˓→that is dynamically-sized. When decoding data from memory (instead of calldata), the␣
˓→ABI decoder did not properly validate some of these pointers. More specifically, it␣
˓→was possible to use large values for the pointers inside arrays such that computing␣
˓→the offset resulted in an undetected overflow. This could lead to these pointers␣
˓→targeting areas in memory outside of the actual area to be decoded. This way, it was␣
˓→possible for``abi.decode`` to return different values for the same encoded byte array.
˓→",
(continues on next page)
```
**278 Chapter 3. Contents**


```
(continued from previous page)
"link": "https://blog.soliditylang.org/2021/04/21/decoding-from-memory-bug/",
"introduced": "0.4.16",
"fixed": "0.8.4",
"conditions": {
"ABIEncoderV2":true
},
"severity": "very low"
},
{
"uid": "SOL-2021-1",
"name": "KeccakCaching",
"summary": "The bytecode optimizer incorrectly re-used previously evaluated␣
˓→Keccak-256 hashes. You are unlikely to be affected if you do not compute Keccak-256␣
˓→hashes in inline assembly.",
"description": "Solidity's bytecode optimizer has a step that can compute Keccak-
˓→256 hashes, if the contents of the memory are known during compilation time. This step␣
˓→also has a mechanism to determine that two Keccak-256 hashes are equal even if the␣
˓→values in memory are not known during compile time. This mechanism had a bug where␣
˓→Keccak-256 of the same memory content, but different sizes were considered equal. More␣
˓→specifically, ``keccak256(mpos1, length1)`` and``keccak256(mpos2, length2)``in some␣
˓→cases were considered equal if ``length1``and``length2``, when rounded up to nearest␣
˓→multiple of 32 were the same, and when the memory contents at ``mpos1`` and``mpos2``␣
˓→can be deduced to be equal. You maybe affected if you compute multiple Keccak-256␣
˓→hashes of the same content, but with different lengths inside inline assembly. You are␣
˓→unaffected if your code uses ``keccak256``with a length that is not a compile-time␣
˓→constant or if it is always a multiple of 32.",
"link": "https://blog.soliditylang.org/2021/03/23/keccak-optimizer-bug/",
"fixed": "0.8.3",
"conditions": {
"optimizer":true
},
"severity": "medium"
},
{
"uid": "SOL-2020-11",
"name": "EmptyByteArrayCopy",
"summary": "Copying an empty byte array (or string) from memory or calldata to␣
˓→storage can result in data corruption if the target array's length is increased␣
˓→subsequently without storing new data.",
"description": "The routine that copies byte arrays from memory or calldata to␣
˓→storage stores unrelated data from after the source array in the storage slot if the␣
˓→source array is empty. If the storage array's length is subsequently increased either␣
˓→by using ``.push()``or by assigning to its ``.length``attribute (only before 0.6.0),␣
˓→the newly created byte array elements will not be zero-initialized, but contain the␣
˓→unrelated data. You are not affected if you do not assign to ``.length``and do not␣
˓→use``.push()`` on byte arrays, or only use ``.push(<arg>)`` or manually initialize␣
˓→the new elements.",
"link": "https://blog.soliditylang.org/2020/10/19/empty-byte-array-copy-bug/",
"fixed": "0.7.4",
"severity": "medium"
},
{
(continues on next page)
```
**3.25. List of Known Bugs 279**


```
(continued from previous page)
"uid": "SOL-2020-10",
"name": "DynamicArrayCleanup",
"summary": "When assigning a dynamically-sized array with types of size at most␣
˓→16 bytes in storage causing the assigned array to shrink, some parts of deleted slots␣
˓→were not zeroed out.",
"description": "Consider a dynamically-sized array in storage whose base-type is␣
˓→small enough such that multiple values can be packed into a single slot, such as␣
˓→`uint128[]`. Let us define its length to be `l`. When this array gets assigned from␣
˓→another array with a smaller length, say `m`, the slots between elements`m`and`l`␣
˓→have to be cleaned by zeroing them out. However, this cleaning was not performed␣
˓→properly. Specifically, after the slot corresponding to`m`, only the first packed␣
˓→value was cleaned up. If this array gets resized to a length larger than`m`, the␣
˓→indices corresponding to the unclean parts of the slot contained the original value,␣
˓→instead of 0. The resizing here is performed by assigning to the array `length`, by a␣
˓→`push()` or via inline assembly. You are not affected if you are only using`.push(
˓→<arg>)`or if you assign a value (even zero) to the new elements after increasing the␣
˓→length of the array.",
"link": "https://blog.soliditylang.org/2020/10/07/solidity-dynamic-array-cleanup-
˓→bug/",
"fixed": "0.7.3",
"severity": "medium"
},
{
"uid": "SOL-2020-9",
"name": "FreeFunctionRedefinition",
"summary": "The compiler does not flag an error when two or more free functions␣
˓→with the same name and parameter types are defined in a source unit or when an␣
˓→imported free function alias shadows another free function with a different name but␣
˓→identical parameter types.",
"description": "In contrast to functions defined inside contracts, free␣
˓→functions with identical names and parameter types did not create an error. Both␣
˓→definition of free functions with identical name and parameter types and an imported␣
˓→free function with an alias that shadows another function with a different name but␣
˓→identical parameter types were permitted due to which a call to either the multiply␣
˓→defined free function or the imported free function alias within a contract led to the␣
˓→execution of that free function which was defined first within the source unit.␣
˓→Subsequently defined identical free function definitions were silently ignored and␣
˓→their code generation was skipped.",
"introduced": "0.7.1",
"fixed": "0.7.2",
"severity": "low"
},
{
"uid": "SOL-2020-8",
"name": "UsingForCalldata",
"summary": "Function calls to internal library functions with calldata␣
˓→parameters called via ``using for`` can result in invalid data being read.",
"description": "Function calls to internal library functions using the``using␣
˓→for`` mechanism copied all calldata parameters to memory first and passed them on like␣
˓→that, regardless of whether it was an internal or an external call. Due to that, the␣
˓→called function would receive a memory pointer that is interpreted as a calldata␣
˓→pointer. Since dynamically sized arrays are passed using two stack slots for calldata,␣
(continues on next page)
```
**280 Chapter 3. Contents**


```
(continued from previous page)
˓→but only one for memory, this can lead to stack corruption. An affected library call␣
˓→will consider the JUMPDEST to which it is supposed to return as part of its arguments␣
˓→and will instead jump out to whatever was on the stack before the call.",
"introduced": "0.6.9",
"fixed": "0.6.10",
"severity": "very low"
},
{
"uid": "SOL-2020-7",
"name": "MissingEscapingInFormatting",
"summary": "String literals containing double backslash characters passed␣
˓→directly to external or encoding function calls can lead to a different string being␣
˓→used when ABIEncoderV2 is enabled.",
"description": "When ABIEncoderV2 is enabled, string literals passed directly to␣
˓→encoding functions or external function calls are stored as strings in the intemediate␣
˓→code. Characters outside the printable range are handled correctly, but backslashes␣
˓→are not escaped in this procedure. This leads to double backslashes being reduced to␣
˓→single backslashes and consequently re-interpreted as escapes potentially resulting in␣
˓→a different string being encoded.",
"introduced": "0.5.14",
"fixed": "0.6.8",
"severity": "very low",
"conditions": {
"ABIEncoderV2":true
}
},
{
"uid": "SOL-2020-6",
"name": "ArraySliceDynamicallyEncodedBaseType",
"summary": "Accessing array slices of arrays with dynamically encoded base types␣
˓→(e.g. multi-dimensional arrays) can result in invalid data being read.",
"description": "For arrays with dynamically sized base types, index range␣
˓→accesses that use a start expression that is non-zero will result in invalid array␣
˓→slices. Any index access to such array slices will result in data being read from␣
˓→incorrect calldata offsets. Array slices are only supported for dynamic calldata types␣
˓→and all problematic type require ABIEncoderV2 to be enabled.",
"introduced": "0.6.0",
"fixed": "0.6.8",
"severity": "very low",
"conditions": {
"ABIEncoderV2":true
}
},
{
"uid": "SOL-2020-5",
"name": "ImplicitConstructorCallvalueCheck",
"summary": "The creation code of a contract that does not define a constructor␣
˓→but has a base that does define a constructor did not revert for calls with non-zero␣
˓→value.",
"description": "Starting from Solidity 0.4.5 the creation code of contracts␣
˓→without explicit payable constructor is supposed to contain a callvalue check that␣
˓→results in contract creation reverting, if non-zero value is passed. However, this␣
(continues on next page)
```
**3.25. List of Known Bugs 281**


```
(continued from previous page)
˓→check was missing in case no explicit constructor was defined in a contract at all,␣
˓→but the contract has a base that does define a constructor. In these cases it is␣
˓→possible to send value in a contract creation transaction or using inline assembly␣
˓→without revert, even though the creation code is supposed to be non-payable.",
"introduced": "0.4.5",
"fixed": "0.6.8",
"severity": "very low"
},
{
"uid": "SOL-2020-4",
"name": "TupleAssignmentMultiStackSlotComponents",
"summary": "Tuple assignments with components that occupy several stack slots, i.
˓→e. nested tuples, pointers to external functions or references to dynamically sized␣
˓→calldata arrays, can result in invalid values.",
"description": "Tuple assignments did not correctly account for tuple components␣
˓→that occupy multiple stack slots in case the number of stack slots differs between␣
˓→left-hand-side and right-hand-side. This can either happen in the presence of nested␣
˓→tuples or if the right-hand-side contains external function pointers or references to␣
˓→dynamic calldata arrays, while the left-hand-side contains an omission.",
"introduced": "0.1.6",
"fixed": "0.6.6",
"severity": "very low"
},
{
"uid": "SOL-2020-3",
"name": "MemoryArrayCreationOverflow",
"summary": "The creation of very large memory arrays can result in overlapping␣
˓→memory regions and thus memory corruption.",
"description": "No runtime overflow checks were performed for the length of␣
˓→memory arrays during creation. In cases for which the memory size of an array in bytes,
˓→i.e. the array length times 32, is larger than 2^256-1, the memory allocation will␣
˓→overflow, potentially resulting in overlapping memory areas. The length of the array␣
˓→is still stored correctly, so copying or iterating over such an array will result in␣
˓→out-of-gas.",
"link": "https://blog.soliditylang.org/2020/04/06/memory-creation-overflow-bug/",
"introduced": "0.2.0",
"fixed": "0.6.5",
"severity": "low"
},
{
"uid": "SOL-2020-1",
"name": "YulOptimizerRedundantAssignmentBreakContinue",
"summary": "The Yul optimizer can remove essential assignments to variables␣
˓→declared inside for loops when Yul's continue or break statement is used. You are␣
˓→unlikely to be affected if you do not use inline assembly with for loops and continue␣
˓→and break statements.",
"description": "The Yul optimizer has a stage that removes assignments to␣
˓→variables that are overwritten again or are not used in all following control-flow␣
˓→branches. This logic incorrectly removes such assignments to variables declared inside␣
˓→a for loop if they can be removed in a control-flow branch that ends with ``break`` or␣
˓→``continue``even though they cannot be removed in other control-flow branches.␣
˓→Variables declared outside of the respective for loop are not affected.",
(continues on next page)
```
**282 Chapter 3. Contents**


```
(continued from previous page)
"introduced": "0.6.0",
"fixed": "0.6.1",
"severity": "medium",
"conditions": {
"yulOptimizer":true
}
},
{
"uid": "SOL-2020-2",
"name": "privateCanBeOverridden",
"summary": "Private methods can be overridden by inheriting contracts.",
"description": "While private methods of base contracts are not visible and␣
˓→cannot be called directly from the derived contract, it is still possible to declare a␣
˓→function of the same name and type and thus change the behaviour of the base contract
˓→'s function.",
"introduced": "0.3.0",
"fixed": "0.5.17",
"severity": "low"
},
{
"uid": "SOL-2020-1",
"name": "YulOptimizerRedundantAssignmentBreakContinue0.5",
"summary": "The Yul optimizer can remove essential assignments to variables␣
˓→declared inside for loops when Yul's continue or break statement is used. You are␣
˓→unlikely to be affected if you do not use inline assembly with for loops and continue␣
˓→and break statements.",
"description": "The Yul optimizer has a stage that removes assignments to␣
˓→variables that are overwritten again or are not used in all following control-flow␣
˓→branches. This logic incorrectly removes such assignments to variables declared inside␣
˓→a for loop if they can be removed in a control-flow branch that ends with ``break`` or␣
˓→``continue``even though they cannot be removed in other control-flow branches.␣
˓→Variables declared outside of the respective for loop are not affected.",
"introduced": "0.5.8",
"fixed": "0.5.16",
"severity": "low",
"conditions": {
"yulOptimizer":true
}
},
{
"uid": "SOL-2019-10",
"name": "ABIEncoderV2LoopYulOptimizer",
"summary": "If both the experimental ABIEncoderV2 and the experimental Yul␣
˓→optimizer are activated, one component of the Yul optimizer may reuse data in memory␣
˓→that has been changed in the meantime.",
"description": "The Yul optimizer incorrectly replaces ``mload`` and``sload``␣
˓→calls with values that have been previously written to the load location (and␣
˓→potentially changed in the meantime) if all of the following conditions are met: (1)␣
˓→there is a matching ``mstore`` or``sstore`` call before; (2) the contents of memory␣
˓→or storage is only changed in a function that is called (directly or indirectly) in␣
˓→between the first store and the load call; (3) called function contains a for loop␣
˓→where the same memory location is changed in the condition or the post or body block.␣
(continues on next page)
```
**3.25. List of Known Bugs 283**


```
(continued from previous page)
˓→When used in Solidity mode, this can only happen if the experimental ABIEncoderV2 is␣
˓→activated and the experimental Yul optimizer has been activated manually in addition␣
˓→to the regular optimizer in the compiler settings.",
"introduced": "0.5.14",
"fixed": "0.5.15",
"severity": "low",
"conditions": {
"ABIEncoderV2":true,
"optimizer":true,
"yulOptimizer":true
}
},
{
"uid": "SOL-2019-9",
"name":
˓→"ABIEncoderV2CalldataStructsWithStaticallySizedAndDynamicallyEncodedMembers",
"summary": "Reading from calldata structs that contain dynamically encoded, but␣
˓→statically-sized members can result in incorrect values.",
"description": "When a calldata struct contains a dynamically encoded, but␣
˓→statically-sized member, the offsets for all subsequent struct members are calculated␣
˓→incorrectly. All reads from such members will result in invalid values. Only calldata␣
˓→structs are affected, i.e. this occurs in external functions with such structs as␣
˓→argument. Using affected structs in storage or memory or as arguments to public␣
˓→functions on the other hand works correctly.",
"introduced": "0.5.6",
"fixed": "0.5.11",
"severity": "low",
"conditions": {
"ABIEncoderV2":true
}
},
{
"uid": "SOL-2019-8",
"name": "SignedArrayStorageCopy",
"summary": "Assigning an array of signed integers to a storage array of␣
˓→different type can lead to data corruption in that array.",
"description": "In two's complement, negative integers have their higher order␣
˓→bits set. In order to fit into a shared storage slot, these have to be set to zero.␣
˓→When a conversion is done at the same time, the bits to set to zero were incorrectly␣
˓→determined from the source and not the target type. This means that such copy␣
˓→operations can lead to incorrect values being stored.",
"link": "https://blog.soliditylang.org/2019/06/25/solidity-storage-array-bugs/",
"introduced": "0.4.7",
"fixed": "0.5.10",
"severity": "low/medium"
},
{
"uid": "SOL-2019-7",
"name": "ABIEncoderV2StorageArrayWithMultiSlotElement",
"summary": "Storage arrays containing structs or other statically-sized arrays␣
˓→are not read properly when directly encoded in external function calls or in abi.
˓→encode*.",
(continues on next page)
```
**284 Chapter 3. Contents**


```
(continued from previous page)
"description": "When storage arrays whose elements occupy more than a single␣
˓→storage slot are directly encoded in external function calls or using abi.encode*,␣
˓→their elements are read in an overlapping manner, i.e. the element pointer is not␣
˓→properly advanced between reads. This is not a problem when the storage data is first␣
˓→copied to a memory variable or if the storage array only contains value types or␣
˓→dynamically-sized arrays.",
"link": "https://blog.soliditylang.org/2019/06/25/solidity-storage-array-bugs/",
"introduced": "0.4.16",
"fixed": "0.5.10",
"severity": "low",
"conditions": {
"ABIEncoderV2":true
}
},
{
"uid": "SOL-2019-6",
"name": "DynamicConstructorArgumentsClippedABIV2",
"summary": "A contract's constructor that takes structs or arrays that contain␣
˓→dynamically-sized arrays reverts or decodes to invalid data.",
"description": "During construction of a contract, constructor parameters are␣
˓→copied from the code section to memory for decoding. The amount of bytes to copy was␣
˓→calculated incorrectly in case all parameters are statically-sized but contain␣
˓→dynamically-sized arrays as struct members or inner arrays. Such types are only␣
˓→available if ABIEncoderV2 is activated.",
"introduced": "0.4.16",
"fixed": "0.5.9",
"severity": "very low",
"conditions": {
"ABIEncoderV2":true
}
},
{
"uid": "SOL-2019-5",
"name": "UninitializedFunctionPointerInConstructor",
"summary": "Calling uninitialized internal function pointers created in the␣
˓→constructor does not always revert and can cause unexpected behaviour.",
"description": "Uninitialized internal function pointers point to a special␣
˓→piece of code that causes a revert when called. Jump target positions are different␣
˓→during construction and after deployment, but the code for setting this special jump␣
˓→target only considered the situation after deployment.",
"introduced": "0.5.0",
"fixed": "0.5.8",
"severity": "very low"
},
{
"uid": "SOL-2019-5",
"name": "UninitializedFunctionPointerInConstructor_0.4.x",
"summary": "Calling uninitialized internal function pointers created in the␣
˓→constructor does not always revert and can cause unexpected behaviour.",
"description": "Uninitialized internal function pointers point to a special␣
˓→piece of code that causes a revert when called. Jump target positions are different␣
˓→during construction and after deployment, but the code for setting this special jump␣
(continues on next page)
```
**3.25. List of Known Bugs 285**


```
(continued from previous page)
˓→target only considered the situation after deployment.",
"introduced": "0.4.5",
"fixed": "0.4.26",
"severity": "very low"
},
{
"uid": "SOL-2019-4",
"name": "IncorrectEventSignatureInLibraries",
"summary": "Contract types used in events in libraries cause an incorrect event␣
˓→signature hash",
"description": "Instead of using the type `address` in the hashed signature, the␣
˓→actual contract name was used, leading to a wrong hash in the logs.",
"introduced": "0.5.0",
"fixed": "0.5.8",
"severity": "very low"
},
{
"uid": "SOL-2019-4",
"name": "IncorrectEventSignatureInLibraries_0.4.x",
"summary": "Contract types used in events in libraries cause an incorrect event␣
˓→signature hash",
"description": "Instead of using the type `address` in the hashed signature, the␣
˓→actual contract name was used, leading to a wrong hash in the logs.",
"introduced": "0.3.0",
"fixed": "0.4.26",
"severity": "very low"
},
{
"uid": "SOL-2019-3",
"name": "ABIEncoderV2PackedStorage",
"summary": "Storage structs and arrays with types shorter than 32 bytes can␣
˓→cause data corruption if encoded directly from storage using the experimental␣
˓→ABIEncoderV2.",
"description": "Elements of structs and arrays that are shorter than 32 bytes␣
˓→are not properly decoded from storage when encoded directly (i.e. not via a memory␣
˓→type) using ABIEncoderV2. This can cause corruption in the values themselves but can␣
˓→also overwrite other parts of the encoded data.",
"link": "https://blog.soliditylang.org/2019/03/26/solidity-optimizer-and-
˓→abiencoderv2-bug/",
"introduced": "0.5.0",
"fixed": "0.5.7",
"severity": "low",
"conditions": {
"ABIEncoderV2":true
}
},
{
"uid": "SOL-2019-3",
"name": "ABIEncoderV2PackedStorage_0.4.x",
"summary": "Storage structs and arrays with types shorter than 32 bytes can␣
˓→cause data corruption if encoded directly from storage using the experimental␣
˓→ABIEncoderV2.",
(continues on next page)
```
**286 Chapter 3. Contents**


```
(continued from previous page)
"description": "Elements of structs and arrays that are shorter than 32 bytes␣
˓→are not properly decoded from storage when encoded directly (i.e. not via a memory␣
˓→type) using ABIEncoderV2. This can cause corruption in the values themselves but can␣
˓→also overwrite other parts of the encoded data.",
"link": "https://blog.soliditylang.org/2019/03/26/solidity-optimizer-and-
˓→abiencoderv2-bug/",
"introduced": "0.4.19",
"fixed": "0.4.26",
"severity": "low",
"conditions": {
"ABIEncoderV2":true
}
},
{
"uid": "SOL-2019-2",
"name": "IncorrectByteInstructionOptimization",
"summary": "The optimizer incorrectly handles byte opcodes whose second argument␣
˓→is 31 or a constant expression that evaluates to 31. This can result in unexpected␣
˓→values.",
"description": "The optimizer incorrectly handles byte opcodes that use the␣
˓→constant 31 as second argument. This can happen when performing index access on␣
˓→bytesNN types with a compile-time constant value (not index) of 31 or when using the␣
˓→byte opcode in inline assembly.",
"link": "https://blog.soliditylang.org/2019/03/26/solidity-optimizer-and-
˓→abiencoderv2-bug/",
"introduced": "0.5.5",
"fixed": "0.5.7",
"severity": "very low",
"conditions": {
"optimizer":true
}
},
{
"uid": "SOL-2019-1",
"name": "DoubleShiftSizeOverflow",
"summary": "Double bitwise shifts by large constants whose sum overflows 256␣
˓→bits can result in unexpected values.",
"description": "Nested logical shift operations whose total shift size is 2**256␣
˓→or more are incorrectly optimized. This only applies to shifts by numbers of bits that␣
˓→are compile-time constant expressions.",
"link": "https://blog.soliditylang.org/2019/03/26/solidity-optimizer-and-
˓→abiencoderv2-bug/",
"introduced": "0.5.5",
"fixed": "0.5.6",
"severity": "low",
"conditions": {
"optimizer":true,
"evmVersion": ">=constantinople"
}
},
{
"uid": "SOL-2018-4",
(continues on next page)
```
**3.25. List of Known Bugs 287**


```
(continued from previous page)
"name": "ExpExponentCleanup",
"summary": "Using the ** operator with an exponent of type shorter than 256 bits␣
˓→can result in unexpected values.",
"description": "Higher order bits in the exponent are not properly cleaned␣
˓→before the EXP opcode is applied if the type of the exponent expression is smaller␣
˓→than 256 bits and not smaller than the type of the base. In that case, the result␣
˓→might be larger than expected if the exponent is assumed to lie within the value range␣
˓→of the type. Literal numbers as exponents are unaffected as are exponents or bases of␣
˓→type uint256.",
"link": "https://blog.soliditylang.org/2018/09/13/solidity-bugfix-release/",
"fixed": "0.4.25",
"severity": "medium/high",
"check": {"regex-source": "[^/]\\*\\* *[^/0-9 ]"}
},
{
"uid": "SOL-2018-3",
"name": "EventStructWrongData",
"summary": "Using structs in events logged wrong data.",
"description": "If a struct is used in an event, the address of the struct is␣
˓→logged instead of the actual data.",
"link": "https://blog.soliditylang.org/2018/09/13/solidity-bugfix-release/",
"introduced": "0.4.17",
"fixed": "0.4.25",
"severity": "very low",
"check": {"ast-compact-json-path": "$..[?(@.nodeType ==='EventDefinition')]..[?
˓→(@.nodeType === 'UserDefinedTypeName'&& @.typeDescriptions.typeString.startsWith(
˓→'struct'))]"}
},
{
"uid": "SOL-2018-2",
"name": "NestedArrayFunctionCallDecoder",
"summary": "Calling functions that return multi-dimensional fixed-size arrays␣
˓→can result in memory corruption.",
"description": "If Solidity code calls a function that returns a multi-
˓→dimensional fixed-size array, array elements are incorrectly interpreted as memory␣
˓→pointers and thus can cause memory corruption if the return values are accessed.␣
˓→Calling functions with multi-dimensional fixed-size arrays is unaffected as is␣
˓→returning fixed-size arrays from function calls. The regular expression only checks if␣
˓→such functions are present, not if they are called, which is required for the contract␣
˓→to be affected.",
"link": "https://blog.soliditylang.org/2018/09/13/solidity-bugfix-release/",
"introduced": "0.1.4",
"fixed": "0.4.22",
"severity": "medium",
"check": {"regex-source": "returns[^;{]*\\[\\s*[^\\] \\t\\r\\n\\v\\f][^\\]]*\\]\\
˓→s*\\[\\s*[^\\] \\t\\r\\n\\v\\f][^\\]]*\\][^{;]*[;{]"}
},
{
"uid": "SOL-2018-1",
"name": "OneOfTwoConstructorsSkipped",
"summary": "If a contract has both a new-style constructor (using the␣
˓→constructor keyword) and an old-style constructor (a function with the same name as␣
(continues on next page)
```
**288 Chapter 3. Contents**


```
(continued from previous page)
˓→the contract) at the same time, one of them will be ignored.",
"description": "If a contract has both a new-style constructor (using the␣
˓→constructor keyword) and an old-style constructor (a function with the same name as␣
˓→the contract) at the same time, one of them will be ignored. There will be a compiler␣
˓→warning about the old-style constructor, so contracts only using new-style␣
˓→constructors are fine.",
"introduced": "0.4.22",
"fixed": "0.4.23",
"severity": "very low"
},
{
"uid": "SOL-2017-5",
"name": "ZeroFunctionSelector",
"summary": "It is possible to craft the name of a function such that it is␣
˓→executed instead of the fallback function in very specific circumstances.",
"description": "If a function has a selector consisting only of zeros, is␣
˓→payable and part of a contract that does not have a fallback function and at most five␣
˓→external functions in total, this function is called instead of the fallback function␣
˓→if Ether is sent to the contract without data.",
"fixed": "0.4.18",
"severity": "very low"
},
{
"uid": "SOL-2017-4",
"name": "DelegateCallReturnValue",
"summary": "The low-level .delegatecall() does not return the execution outcome,␣
˓→but converts the value returned by the functioned called to a boolean instead.",
"description": "The return value of the low-level .delegatecall() function is␣
˓→taken from a position in memory, where the call data or the return data resides. This␣
˓→value is interpreted as a boolean and put onto the stack. This means if the called␣
˓→function returns at least 32 zero bytes, .delegatecall() returns false even if the␣
˓→call was successful.",
"introduced": "0.3.0",
"fixed": "0.4.15",
"severity": "low"
},
{
"uid": "SOL-2017-3",
"name": "ECRecoverMalformedInput",
"summary": "The ecrecover() builtin can return garbage for malformed input.",
"description": "The ecrecover precompile does not properly signal failure for␣
˓→malformed input (especially in the 'v'argument) and thus the Solidity function can␣
˓→return data that was previously present in the return area in memory.",
"fixed": "0.4.14",
"severity": "medium"
},
{
"uid": "SOL-2017-2",
"name": "SkipEmptyStringLiteral",
"summary": "If \"\" is used in a function call, the following function arguments␣
˓→will not be correctly passed to the function.",
"description": "If the empty string literal \"\" is used as an argument in a␣
(continues on next page)
```
**3.25. List of Known Bugs 289**


```
(continued from previous page)
˓→function call, it is skipped by the encoder. This has the effect that the encoding of␣
˓→all arguments following this is shifted left by 32 bytes and thus the function call␣
˓→data is corrupted.",
"fixed": "0.4.12",
"severity": "low"
},
{
"uid": "SOL-2017-1",
"name": "ConstantOptimizerSubtraction",
"summary": "In some situations, the optimizer replaces certain numbers in the␣
˓→code with routines that compute different numbers.",
"description": "The optimizer tries to represent any number in the bytecode by␣
˓→routines that compute them with less gas. For some special numbers, an incorrect␣
˓→routine is generated. This could allow an attacker to e.g. trick victims about a␣
˓→specific amount of ether, or function calls to call different functions (or none at␣
˓→all).",
"link": "https://blog.soliditylang.org/2017/05/03/solidity-optimizer-bug/",
"fixed": "0.4.11",
"severity": "low",
"conditions": {
"optimizer":true
}
},
{
"uid": "SOL-2016-11",
"name": "IdentityPrecompileReturnIgnored",
"summary": "Failure of the identity precompile was ignored.",
"description": "Calls to the identity contract, which is used for copying memory,
˓→ignored its return value. On the public chain, calls to the identity precompile can␣
˓→be made in a way that they never fail, but this might be different on private chains.",
"severity": "low",
"fixed": "0.4.7"
},
{
"uid": "SOL-2016-10",
"name": "OptimizerStateKnowledgeNotResetForJumpdest",
"summary": "The optimizer did not properly reset its internal state at jump␣
˓→destinations, which could lead to data corruption.",
"description": "The optimizer performs symbolic execution at certain stages. At␣
˓→jump destinations, multiple code paths join and thus it has to compute a common state␣
˓→from the incoming edges. Computing this common state was simplified to just use the␣
˓→empty state, but this implementation was not done properly. This bug can cause data␣
˓→corruption.",
"severity": "medium",
"introduced": "0.4.5",
"fixed": "0.4.6",
"conditions": {
"optimizer":true
}
},
{
"uid": "SOL-2016-9",
(continues on next page)
```
**290 Chapter 3. Contents**


```
(continued from previous page)
"name": "HighOrderByteCleanStorage",
"summary": "For short types, the high order bytes were not cleaned properly and␣
˓→could overwrite existing data.",
"description": "Types shorter than 32 bytes are packed together into the same 32␣
˓→byte storage slot, but storage writes always write 32 bytes. For some types, the␣
˓→higher order bytes were not cleaned properly, which made it sometimes possible to␣
˓→overwrite a variable in storage when writing to another one.",
"link": "https://blog.soliditylang.org/2016/11/01/security-alert-solidity-
˓→variables-can-overwritten-storage/",
"severity": "high",
"introduced": "0.1.6",
"fixed": "0.4.4"
},
{
"uid": "SOL-2016-8",
"name": "OptimizerStaleKnowledgeAboutSHA3",
"summary": "The optimizer did not properly reset its knowledge about SHA3␣
˓→operations resulting in some hashes (also used for storage variable positions) not␣
˓→being calculated correctly.",
"description": "The optimizer performs symbolic execution in order to save re-
˓→evaluating expressions whose value is already known. This knowledge was not properly␣
˓→reset across control flow paths and thus the optimizer sometimes thought that the␣
˓→result of a SHA3 operation is already present on the stack. This could result in data␣
˓→corruption by accessing the wrong storage slot.",
"severity": "medium",
"fixed": "0.4.3",
"conditions": {
"optimizer":true
}
},
{
"uid": "SOL-2016-7",
"name": "LibrariesNotCallableFromPayableFunctions",
"summary": "Library functions threw an exception when called from a call that␣
˓→received Ether.",
"description": "Library functions are protected against sending them Ether␣
˓→through a call. Since the DELEGATECALL opcode forwards the information about how much␣
˓→Ether was sent with a call, the library function incorrectly assumed that Ether was␣
˓→sent to the library and threw an exception.",
"severity": "low",
"introduced": "0.4.0",
"fixed": "0.4.2"
},
{
"uid": "SOL-2016-6",
"name": "SendFailsForZeroEther",
"summary": "The send function did not provide enough gas to the recipient if no␣
˓→Ether was sent with it.",
"description": "The recipient of an Ether transfer automatically receives a␣
˓→certain amount of gas from the EVM to handle the transfer. In the case of a zero-
˓→transfer, this gas is not provided which causes the recipient to throw an exception.",
"severity": "low",
(continues on next page)
```
**3.25. List of Known Bugs 291**


```
(continued from previous page)
"fixed": "0.4.0"
},
{
"uid": "SOL-2016-5",
"name": "DynamicAllocationInfiniteLoop",
"summary": "Dynamic allocation of an empty memory array caused an infinite loop␣
˓→and thus an exception.",
"description": "Memory arrays can be created provided a length. If this length␣
˓→is zero, code was generated that did not terminate and thus consumed all gas.",
"severity": "low",
"fixed": "0.3.6"
},
{
"uid": "SOL-2016-4",
"name": "OptimizerClearStateOnCodePathJoin",
"summary": "The optimizer did not properly reset its internal state at jump␣
˓→destinations, which could lead to data corruption.",
"description": "The optimizer performs symbolic execution at certain stages. At␣
˓→jump destinations, multiple code paths join and thus it has to compute a common state␣
˓→from the incoming edges. Computing this common state was not done correctly. This bug␣
˓→can cause data corruption, but it is probably quite hard to use for targeted attacks.",
"severity": "low",
"fixed": "0.3.6",
"conditions": {
"optimizer":true
}
},
{
"uid": "SOL-2016-3",
"name": "CleanBytesHigherOrderBits",
"summary": "The higher order bits of short bytesNN types were not cleaned before␣
˓→comparison.",
"description": "Two variables of type bytesNN were considered different if their␣
˓→higher order bits, which are not part of the actual value, were different. An attacker␣
˓→might use this to reach seemingly unreachable code paths by providing incorrectly␣
˓→formatted input data.",
"severity": "medium/high",
"fixed": "0.3.3"
},
{
"uid": "SOL-2016-2",
"name": "ArrayAccessCleanHigherOrderBits",
"summary": "Access to array elements for arrays of types with less than 32 bytes␣
˓→did not correctly clean the higher order bits, causing corruption in other array␣
˓→elements.",
"description": "Multiple elements of an array of values that are shorter than 17␣
˓→bytes are packed into the same storage slot. Writing to a single element of such an␣
˓→array did not properly clean the higher order bytes and thus could lead to data␣
˓→corruption.",
"severity": "medium/high",
"fixed": "0.3.1"
},
(continues on next page)
```
**292 Chapter 3. Contents**


(continued from previous page)
{
"uid": "SOL-2016-1",
"name": "AncientCompiler",
"summary": "This compiler version is ancient and might contain several␣
˓→undocumented or undiscovered bugs.",
"description": "The list of bugs is only kept for compiler versions starting␣
˓→from 0.3.0, so older versions might contain undocumented bugs.",
"severity": "high",
"fixed": "0.3.0"
}
]

### 3.26 Solidity v0.5.0 Breaking Changes

This section highlights the main breaking changes introduced in Solidity version 0.5.0, along with the reasoning behind
the changes and how to update affected code. For the full list check the release changelog.

**Note:** Contracts compiled with Solidity v0.5.0 can still interface with contracts and even libraries compiled with older
versions without recompiling or redeploying them. Changing the interfaces to include data locations and visibility and
mutability specifiers suffices. See the _Interoperability With Older Contracts_ section below.

**3.26.1 Semantic Only Changes**

This section lists the changes that are semantic-only, thus potentially hiding new and different behavior in existing code.

- Signed right shift now uses proper arithmetic shift, i.e. rounding towards negative infinity, instead of rounding
    towards zero. Signed and unsigned shift will have dedicated opcodes in Constantinople, and are emulated by
    Solidity for the moment.
- Thecontinuestatement in ado...whileloop now jumps to the condition, which is the common behavior in
    such cases. It used to jump to the loop body. Thus, if the condition is false, the loop terminates.
- The functions.call(),.delegatecall()and.staticcall()do not pad anymore when given a single
    bytesparameter.
- Pure and view functions are now called using the opcodeSTATICCALLinstead ofCALLif the EVM version is
    Byzantium or later. This disallows state changes on the EVM level.
- The ABI encoder now properly pads byte arrays and strings from calldata (msg.dataand external function
    parameters) when used in external function calls and inabi.encode. For unpadded encoding, useabi.
    encodePacked.
- The ABI decoder reverts in the beginning of functions and inabi.decode()if passed calldata is too short or
    points out of bounds. Note that dirty higher order bits are still simply ignored.
- Forward all available gas with external function calls starting from Tangerine Whistle.

**3.26. Solidity v0.5.0 Breaking Changes 293**


**3.26.2 Semantic and Syntactic Changes**

This section highlights changes that affect syntax and semantics.

- The functions.call(),.delegatecall(),staticcall(),keccak256(),sha256()andripemd160()
    now accept only a single bytes argument. Moreover, the argument is not padded. This was
    changed to make more explicit and clear how the arguments are concatenated. Change every.
    call() (and family) to a .call("") and every .call(signature, a, b, c) to use .call(abi.
    encodeWithSignature(signature, a, b, c))(the last one only works for value types). Change every
    keccak256(a, b, c)tokeccak256(abi.encodePacked(a, b, c)). Even though it is not a breaking
    change, it is suggested that developers changex.call(bytes4(keccak256("f(uint256)")), a, b)tox.
    call(abi.encodeWithSignature("f(uint256)", a, b)).
- Functions.call(),.delegatecall()and.staticcall()now return(bool, bytes memory)to pro-
    vide access to the return data. Changebool success = otherContract.call("f")to(bool success,
    bytes memory data) = otherContract.call("f").
- Solidity now implements C99-style scoping rules for function local variables, that is, variables can only be used
    after they have been declared and only in the same or nested scopes. Variables declared in the initialization block
    of aforloop are valid at any point inside the loop.

**3.26.3 Explicitness Requirements**

This section lists changes where the code now needs to be more explicit. For most of the topics the compiler will
provide suggestions.

- Explicit function visibility is now mandatory. Addpublicto every function and constructor, andexternalto
    every fallback or interface function that does not specify its visibility already.
- Explicit data location for all variables of struct, array or mapping types is now mandatory. This is also applied
    to function parameters and return variables. For example, changeuint[] x = ztouint[] storage x =
    z, andfunction f(uint[][] x)tofunction f(uint[][] memory x)wherememoryis the data location
    and might be replaced bystorageorcalldataaccordingly. Note thatexternalfunctions require parameters
    with a data location ofcalldata.
- Contract types do not includeaddressmembers anymore in order to separate the namespaces. Therefore, it
    is now necessary to explicitly convert values of contract type to addresses before using anaddressmember.
    Example: ifcis a contract, changec.transfer(...)toaddress(c).transfer(...), andc.balanceto
    address(c).balance.
- Explicit conversions between unrelated contract types are now disallowed. You can only convert from a contract
    type to one of its base or ancestor types. If you are sure that a contract is compatible with the contract type you
    want to convert to, although it does not inherit from it, you can work around this by converting toaddressfirst.
    Example: ifAandBare contract types,Bdoes not inherit fromAandbis a contract of typeB, you can still
    convertbto typeAusingA(address(b)). Note that you still need to watch out for matching payable fallback
    functions, as explained below.
- Theaddresstype was split intoaddressandaddress payable, where onlyaddress payableprovides
    thetransferfunction. Anaddress payablecan be directly converted to anaddress, but the other way
    around is not allowed. Convertingaddresstoaddress payableis possible via conversion throughuint160.
    Ifcis a contract,address(c)results inaddress payableonly ifchas a payable fallback function. If you
    use the _withdraw pattern_ , you most likely do not have to change your code becausetransferis only used on
    msg.senderinstead of stored addresses andmsg.senderis anaddress payable.
- Conversions betweenbytesXanduintYof different size are now disallowed due tobytesXpadding on the right
    anduintYpadding on the left which may cause unexpected conversion results. The size must now be adjusted
    within the type before the conversion. For example, you can convert abytes4(4 bytes) to auint64(8 bytes)

**294 Chapter 3. Contents**


```
by first converting thebytes4variable tobytes8and then touint64. You get the opposite padding when con-
verting throughuint32. Before v0.5.0 any conversion betweenbytesXanduintYwould go throughuint8X.
For exampleuint8(bytes3(0x291807))would be converted touint8(uint24(bytes3(0x291807)))(the
result is0x07).
```
- Usingmsg.valuein non-payable functions (or introducing it via a modifier) is disallowed as a security feature.
    Turn the function intopayableor create a new internal function for the program logic that usesmsg.value.
- For clarity reasons, the command-line interface now requires-if the standard input is used as source.

**3.26.4 Deprecated Elements**

This section lists changes that deprecate prior features or syntax. Note that many of these changes were already enabled
in the experimental modev0.5.0.

**Command-line and JSON Interfaces**

- The command-line option--formal(used to generate Why3 output for further formal verification) was dep-
    recated and is now removed. A new formal verification module, the SMTChecker, is enabled viapragma
    experimental SMTChecker;.
- The command-line option--juliawas renamed to--yuldue to the renaming of the intermediate language
    JuliatoYul.
- The--clone-binand--combined-json clone-bincommand-line options were removed.
- Remappings with empty prefix are disallowed.
- The JSON AST fieldsconstantand payablewere removed. The information is now present in the
    stateMutabilityfield.
- The JSON AST fieldisConstructorof theFunctionDefinitionnode was replaced by a field calledkind
    which can have the value"constructor","fallback"or"function".
- In unlinked binary hex files, library address placeholders are now the first 36 hex characters of the keccak256
    hash of the fully qualified library name, surrounded by$...$. Previously, just the fully qualified library name
    was used. This reduces the chances of collisions, especially when long paths are used. Binary files now also
    contain a list of mappings from these placeholders to the fully qualified names.

**Constructors**

- Constructors must now be defined using theconstructorkeyword.
- Calling base constructors without parentheses is now disallowed.
- Specifying base constructor arguments multiple times in the same inheritance hierarchy is now disallowed.
- Calling a constructor with arguments but with wrong argument count is now disallowed. If you only want to
    specify an inheritance relation without giving arguments, do not provide parentheses at all.

**3.26. Solidity v0.5.0 Breaking Changes 295**


**Functions**

- Functioncallcodeis now disallowed (in favor ofdelegatecall). It is still possible to use it via inline assem-
    bly.
- suicideis now disallowed (in favor ofselfdestruct).
- sha3is now disallowed (in favor ofkeccak256).
- throwis now disallowed (in favor ofrevert,requireandassert).

**Conversions**

- Explicit and implicit conversions from decimal literals tobytesXXtypes is now disallowed.
- Explicit and implicit conversions from hex literals tobytesXXtypes of different size is now disallowed.

**Literals and Suffixes**

- The unit denominationyearsis now disallowed due to complications and confusions about leap years.
- Trailing dots that are not followed by a number are now disallowed.
- Combining hex numbers with unit denominations (e.g.0x1e wei) is now disallowed.
- The prefix0Xfor hex numbers is disallowed, only0xis possible.

**Variables**

- Declaring empty structs is now disallowed for clarity.
- Thevarkeyword is now disallowed to favor explicitness.
- Assignments between tuples with different number of components is now disallowed.
- Values for constants that are not compile-time constants are disallowed.
- Multi-variable declarations with mismatching number of values are now disallowed.
- Uninitialized storage variables are now disallowed.
- Empty tuple components are now disallowed.
- Detecting cyclic dependencies in variables and structs is limited in recursion to 256.
- Fixed-size arrays with a length of zero are now disallowed.

**Syntax**

- Usingconstantas function state mutability modifier is now disallowed.
- Boolean expressions cannot use arithmetic operations.
- The unary+operator is now disallowed.
- Literals cannot anymore be used withabi.encodePackedwithout prior conversion to an explicit type.
- Empty return statements for functions with one or more return values are now disallowed.
- The “loose assembly” syntax is now disallowed entirely, that is, jump labels, jumps and non-functional instruc-
    tions cannot be used anymore. Use the newwhile,switchandifconstructs instead.

**296 Chapter 3. Contents**


- Functions without implementation cannot use modifiers anymore.
- Function types with named return values are now disallowed.
- Single statement variable declarations inside if/while/for bodies that are not blocks are now disallowed.
- New keywords:calldataandconstructor.
- New reserved keywords:alias,apply,auto,copyof,define,immutable,implements,macro,mutable,
    override,partial,promise,reference,sealed,sizeof,supports,typedefandunchecked.

**3.26.5 Interoperability With Older Contracts**

It is still possible to interface with contracts written for Solidity versions prior to v0.5.0 (or the other way around) by
defining interfaces for them. Consider you have the following pre-0.5.0 contract already deployed:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.4.25;
// This will report a warning until version 0.4.25 of the compiler
// This will not compile after 0.5.0
contract OldContract{
functionsomeOldFunction(uint8a) {
//...
}
functionanotherOldFunction()constant returns(bool) {
//...
}
// ...
}

This will no longer compile with Solidity v0.5.0. However, you can define a compatible interface for it:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;
interface OldContract {
functionsomeOldFunction(uint8a) external;
functionanotherOldFunction()external returns(bool);
}

Note that we did not declareanotherOldFunctionto beview, despite it being declaredconstantin the original
contract. This is due to the fact that starting with Solidity v0.5.0staticcallis used to callviewfunctions. Prior to
v0.5.0 theconstantkeyword was not enforced, so calling a function declaredconstantwithstaticcallmay still
revert, since theconstantfunction may still attempt to modify storage. Consequently, when defining an interface for
older contracts, you should only useviewin place ofconstantin case you are absolutely sure that the function will
work withstaticcall.

Given the interface defined above, you can now easily use the already deployed pre-0.5.0 contract:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.5.0 <0.9.0;

interface OldContract {
functionsomeOldFunction(uint8a) external;
functionanotherOldFunction()external returns(bool);
}
(continues on next page)

**3.26. Solidity v0.5.0 Breaking Changes 297**


```
(continued from previous page)
```
contract NewContract{
functiondoSomething(OldContract a)public returns (bool) {
a.someOldFunction(0x42);
returna.anotherOldFunction();
}
}

Similarly, pre-0.5.0 libraries can be used by defining the functions of the library without implementation and sup-
plying the address of the pre-0.5.0 library during linking (see _Using the Commandline Compiler_ for how to use the
commandline compiler for linking):

// This will not compile after 0.6.0
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.5.0;

libraryOldLibrary {
functionsomeFunction(uint8a) public returns(bool);
}

contract NewContract{
functionf(uint8 a) public returns(bool) {
returnOldLibrary.someFunction(a);
}
}

**3.26.6 Example**

The following example shows a contract and its updated version for Solidity v0.5.0 with some of the changes listed in
this section.

Old version:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.4.25;
// This will not compile after 0.5.0

contract OtherContract{
uintx;
functionf(uint y)external{
x = y;
}
function()payable external{}
}

contract Old{
OtherContract other;
uintmyNumber;

```
// Function mutability not provided, not an error.
functionsomeInteger()internal returns(uint) {return 2; }
(continues on next page)
```
**298 Chapter 3. Contents**


```
(continued from previous page)
```
```
// Function visibility not provided, not an error.
// Function mutability not provided, not an error.
functionf(uint x)returns(bytes) {
// Var is fine in this version.
varz = someInteger();
x += z;
// Throw is fine in this version.
if (x > 100)
throw;
bytesmemory b = new bytes(x);
y = -3 >> 1;
// y == -1 (wrong, should be -2)
do {
x += 1;
if (x > 10)continue;
//'Continue'causes an infinite loop.
}while (x < 11);
// Call returns only a Bool.
boolsuccess =address(other).call("f");
if (!success)
revert();
else{
// Local variables could be declared after their use.
inty;
}
returnb;
}
```
```
// No need for an explicit data location for'arr'
functiong(uint[] arr,bytes8 x, OtherContract otherContract)public {
otherContract.transfer(1 ether);
```
// Since uint32 (4 bytes) is smaller than bytes8 (8 bytes),
// the first 4 bytes of x will be lost. This might lead to
// unexpected behavior since bytesX are right padded.
uint32y =uint32(x);
myNumber += y + msg.value;
}
}

New version:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.5.0;
// This will not compile after 0.6.0

contract OtherContract{
uintx;
functionf(uint y)external{
x = y;
}
(continues on next page)

**3.26. Solidity v0.5.0 Breaking Changes 299**


(continued from previous page)
function()payable external{}
}

contract New{
OtherContract other;
uintmyNumber;

```
// Function mutability must be specified.
functionsomeInteger()internalpurereturns(uint) {return 2; }
```
```
// Function visibility must be specified.
// Function mutability must be specified.
functionf(uint x)public returns (bytesmemory) {
// The type must now be explicitly given.
uintz = someInteger();
x += z;
// Throw is now disallowed.
require(x <= 100);
inty = -3 >> 1;
require(y == -2);
do {
x += 1;
if (x > 10)continue;
//'Continue'jumps to the condition below.
}while (x < 11);
```
```
// Call returns (bool, bytes).
// Data location must be specified.
(boolsuccess,bytes memory data) =address(other).call("f");
if (!success)
revert();
returndata;
}
```
```
using AddressMakePayablefor address;
// Data location for'arr'must be specified
functiong(uint[] memory /* arr */,bytes8 x, OtherContract otherContract,address␣
˓→unknownContract)public payable {
// 'otherContract.transfer'is not provided.
// Since the code of'OtherContract'is known and has the fallback
// function, address(otherContract) has type'address payable'.
address(otherContract).transfer(1 ether);
```
```
// 'unknownContract.transfer'is not provided.
// 'address(unknownContract).transfer'is not provided
// since'address(unknownContract)'is not 'address payable'.
// If the function takes an'address'which you want to send
// funds to, you can convert it to'address payable'via'uint160'.
// Note: This is not recommended and the explicit type
// 'address payable'should be used whenever possible.
// To increase clarity, we suggest the use of a library for
// the conversion (provided after the contract in this example).
(continues on next page)
```
**300 Chapter 3. Contents**


```
(continued from previous page)
addresspayable addr = unknownContract.makePayable();
require(addr.send(1 ether));
```
// Since uint32 (4 bytes) is smaller than bytes8 (8 bytes),
// the conversion is not allowed.
// We need to convert to a common size first:
bytes4 x4 = bytes4(x);// Padding happens on the right
uint32y =uint32(x4);// Conversion is consistent
// 'msg.value'cannot be used in a 'non-payable'function.
// We need to make the function payable
myNumber += y + msg.value;
}
}

// We can define a library for explicitly converting``address``
// to``address payable``as a workaround.
libraryAddressMakePayable {
functionmakePayable(addressx)internalpure returns(addresspayable) {
return address(uint160(x));
}
}

### 3.27 Solidity v0.6.0 Breaking Changes

This section highlights the main breaking changes introduced in Solidity version 0.6.0, along with the reasoning behind
the changes and how to update affected code. For the full list check the release changelog.

**3.27.1 Changes the Compiler Might not Warn About**

This section lists changes where the behavior of your code might change without the compiler telling you about it.

- The resulting type of an exponentiation is the type of the base. It used to be the smallest type that can hold both
    the type of the base and the type of the exponent, as with symmetric operations. Additionally, signed types are
    allowed for the base of the exponentiation.

**3.27.2 Explicitness Requirements**

This section lists changes where the code now needs to be more explicit, but the semantics do not change. For most of
the topics the compiler will provide suggestions.

- Functions can now only be overridden when they are either marked with thevirtualkeyword or defined in an
    interface. Functions without implementation outside an interface have to be markedvirtual. When overriding
    a function or modifier, the new keywordoverridemust be used. When overriding a function or modifier defined
    in multiple parallel bases, all bases must be listed in parentheses after the keyword like so:override(Base1,
    Base2).
- Member-access tolengthof arrays is now always read-only, even for storage arrays. It is no longer possible
    to resize storage arrays by assigning a new value to their length. Usepush(),push(value)orpop()instead,
    or assign a full array, which will of course overwrite the existing content. The reason behind this is to prevent
    storage collisions of gigantic storage arrays.

**3.27. Solidity v0.6.0 Breaking Changes 301**


- The new keywordabstractcan be used to mark contracts as abstract. It has to be used if a contract does not
    implement all its functions. Abstract contracts cannot be created using thenewoperator, and it is not possible to
    generate bytecode for them during compilation.
- Libraries have to implement all their functions, not only the internal ones.
- The names of variables declared in inline assembly may no longer end in_slotor_offset.
- Variable declarations in inline assembly may no longer shadow any declaration outside the inline assembly block.
    If the name contains a dot, its prefix up to the dot may not conflict with any declaration outside the inline assembly
    block.
- In inline assembly, opcodes that do not take arguments are now represented as “built-in functions” instead of
    standalone identifiers. Sogasis nowgas().
- State variable shadowing is now disallowed. A derived contract can only declare a state variablex, if there is no
    visible state variable with the same name in any of its bases.

**3.27.3 Semantic and Syntactic Changes**

This section lists changes where you have to modify your code and it does something else afterwards.

- Conversions from external function types toaddressare now disallowed. Instead external function types have
    a member calledaddress, similar to the existingselectormember.
- The functionpush(value)for dynamic storage arrays does not return the new length anymore (it returns noth-
    ing).
- The unnamed function commonly referred to as “fallback function” was split up into a new fallback function that
    is defined using thefallbackkeyword and a receive ether function defined using thereceivekeyword.
       **-** If present, the receive ether function is called whenever the call data is empty (whether or not ether is
          received). This function is implicitlypayable.
       **-** The new fallback function is called when no other function matches (if the receive ether function does not
          exist then this includes calls with empty call data). You can make this functionpayableor not. If it is not
          payablethen transactions not matching any other function which send value will revert. You should only
          need to implement the new fallback function if you are following an upgrade or proxy pattern.

**3.27.4 New Features**

This section lists things that were not possible prior to Solidity 0.6.0 or were more difficult to achieve.

- The _try/catch statement_ allows you to react on failed external calls.
- structandenumtypes can be declared at file level.
- Array slices can be used for calldata arrays, for exampleabi.decode(msg.data[4:], (uint, uint))is a
    low-level way to decode the function call payload.
- Natspec supports multiple return parameters in developer documentation, enforcing the same naming check as
    @param.
- Yul and Inline Assembly have a new statement calledleavethat exits the current function.
- Conversions fromaddresstoaddress payableare now possible viapayable(x), wherexmust be of type
    address.

**302 Chapter 3. Contents**


**3.27.5 Interface Changes**

This section lists changes that are unrelated to the language itself, but that have an effect on the interfaces of the compiler.
These may change the way how you use the compiler on the command-line, how you use its programmable interface,
or how you analyze the output produced by it.

**New Error Reporter**

A new error reporter was introduced, which aims at producing more accessible error messages on the command-line.
It is enabled by default, but passing--old-reporterfalls back to the deprecated old error reporter.

**Metadata Hash Options**

The compiler now appends the IPFS hash of the metadata file to the end of the bytecode by default (for details, see
documentation on _contract metadata_ ). Before 0.6.0, the compiler appended the Swarm hash by default, and in order to
still support this behavior, the new command-line option--metadata-hashwas introduced. It allows you to select the
hash to be produced and appended, by passing eitheripfsorswarmas value to the--metadata-hashcommand-line
option. Passing the valuenonecompletely removes the hash.

These changes can also be used via the _Standard JSON Interface_ and effect the metadata JSON generated by the
compiler.

The recommended way to read the metadata is to read the last two bytes to determine the length of the CBOR encoding
and perform a proper decoding on that data block as explained in the _metadata section_.

**Yul Optimizer**

Together with the legacy bytecode optimizer, the _Yul_ optimizer is now enabled by default when you call the compiler
with--optimize. It can be disabled by calling the compiler with--no-optimize-yul. This mostly affects code
that uses ABI coder v2.

**C API Changes**

The client code that uses the C API oflibsolcis now in control of the memory used by the compiler. To
make this change consistent,solidity_freewas renamed tosolidity_reset, the functionssolidity_alloc
andsolidity_freewere added andsolidity_compilenow returns a string that must be explicitly freed via
solidity_free().

**3.27.6 How to update your code**

This section gives detailed instructions on how to update prior code for every breaking change.

- Changeaddress(f)tof.addressforfbeing of external function type.
- Replacefunction () external [payable] { ... }by eitherreceive() external payable { ...
    },fallback() external [payable] { ... }or both. Prefer using areceivefunction only, whenever
    possible.
- Changeuint length = array.push(value)toarray.push(value);. The new length can be accessed
    viaarray.length.
- Changearray.length++toarray.push()to increase, and usepop()to decrease the length of a storage array.

**3.27. Solidity v0.6.0 Breaking Changes 303**


- For every named return parameter in a function’s@devdocumentation define a@returnentry which contains
    the parameter’s name as the first word. E.g. if you have functionf()defined likefunction f() public
    returns (uint value)and a@devannotating it, document its return parameters like so:@return value
    The return value.. You can mix named and un-named return parameters documentation so long as the
    notices are in the order they appear in the tuple return type.
- Choose unique identifiers for variable declarations in inline assembly that do not conflict with declarations outside
    the inline assembly block.
- Addvirtualto every non-interface function you intend to override. Addvirtualto all functions without
    implementation outside interfaces. For single inheritance, addoverrideto every overriding function. For
    multiple inheritance, addoverride(A, B, ..), where you list all contracts that define the overridden function
    in the parentheses. When multiple bases define the same function, the inheriting contract must override all
    conflicting functions.
- In inline assembly, add()to all opcodes that do not otherwise accept an argument. For example, changepcto
    pc(), andgastogas().

### 3.28 Solidity v0.7.0 Breaking Changes

This section highlights the main breaking changes introduced in Solidity version 0.7.0, along with the reasoning behind
the changes and how to update affected code. For the full list check the release changelog.

**3.28.1 Silent Changes of the Semantics**

- Exponentiation and shifts of literals by non-literals (e.g. 1 << xor2 ** x) will always use either the type
    uint256(for non-negative literals) orint256(for negative literals) to perform the operation. Previously, the
    operation was performed in the type of the shift amount / the exponent which can be misleading.

**3.28.2 Changes to the Syntax**

- In external function and contract creation calls, Ether and gas is now specified using a new syntax:x.f{gas:
    10000, value: 2 ether}(arg1, arg2). The old syntax –x.f.gas(10000).value(2 ether)(arg1,
    arg2)– will cause an error.
- The global variablenowis deprecated,block.timestampshould be used instead. The single identifiernow
    is too generic for a global variable and could give the impression that it changes during transaction processing,
    whereasblock.timestampcorrectly reflects the fact that it is just a property of the block.
- NatSpec comments on variables are only allowed for public state variables and not for local or internal variables.
- The tokengweiis a keyword now (used to specify, e.g.2 gweias a number) and cannot be used as an identifier.
- String literals now can only contain printable ASCII characters and this also includes a variety of escape se-
    quences, such as hexadecimal (\xff) and unicode escapes (\u20ac).
- Unicode string literals are supported now to accommodate valid UTF-8 sequences. They are identified with the
    unicodeprefix:unicode"Hello ".
- State Mutability: The state mutability of functions can now be restricted during inheritance: Functions with
    default state mutability can be overridden bypureandviewfunctions whileviewfunctions can be overridden
    bypurefunctions. At the same time, public state variables are consideredviewand evenpureif they are
    constants.

**304 Chapter 3. Contents**


**Inline Assembly**

- Disallow.in user-defined function and variable names in inline assembly. It is still valid if you use Solidity in
    Yul-only mode.
- Slot and offset of storage pointer variablexare accessed viax.slotandx.offsetinstead ofx_slotand
    x_offset.

**3.28.3 Removal of Unused or Unsafe Features**

**Mappings outside Storage**

- If a struct or array contains a mapping, it can only be used in storage. Previously, mapping members were silently
    skipped in memory, which is confusing and error-prone.
- Assignments to structs or arrays in storage does not work if they contain mappings. Previously, mappings were
    silently skipped during the copy operation, which is misleading and error-prone.

**Functions and Events**

- Visibility (public/internal) is not needed for constructors anymore: To prevent a contract from being created,
    it can be markedabstract. This makes the visibility concept for constructors obsolete.
- Type Checker: Disallowvirtualfor library functions: Since libraries cannot be inherited from, library func-
    tions should not be virtual.
- Multiple events with the same name and parameter types in the same inheritance hierarchy are disallowed.
- using A for Bonly affects the contract it is mentioned in. Previously, the effect was inherited. Now, you have
    to repeat theusingstatement in all derived contracts that make use of the feature.

**Expressions**

- Shifts by signed types are disallowed. Previously, shifts by negative amounts were allowed, but reverted at
    runtime.
- Thefinneyandszabodenominations are removed. They are rarely used and do not make the actual amount
    readily visible. Instead, explicit values like1e20or the very commongweican be used.

**Declarations**

- The keywordvarcannot be used anymore. Previously, this keyword would parse but result in a type error and a
    suggestion about which type to use. Now, it results in a parser error.

**3.28. Solidity v0.7.0 Breaking Changes 305**


**3.28.4 Interface Changes**

- JSON AST: Mark hex string literals withkind: "hexString".
- JSON AST: Members with valuenullare removed from JSON output.
- NatSpec: Constructors and functions have consistent userdoc output.

**3.28.5 How to update your code**

This section gives detailed instructions on how to update prior code for every breaking change.

- Change x.f.value(...)() to x.f{value: ...}(). Similarly (new C).value(...)() to new
    C{value: ...}()andx.f.gas(...).value(...)()tox.f{gas: ..., value: ...}().
- Changenowtoblock.timestamp.
- Change types of right operand in shift operators to unsigned types. For example changex >> (256 - y)tox
    >> uint(256 - y).
- Repeat theusing A for Bstatements in all derived contracts if needed.
- Remove thepublickeyword from every constructor.
- Remove theinternalkeyword from every constructor and addabstractto the contract (if not already present).
- Change_slotand_offsetsuffixes in inline assembly to.slotand.offset, respectively.

### 3.29 Solidity v0.8.0 Breaking Changes

This section highlights the main breaking changes introduced in Solidity version 0.8.0. For the full list check the release
changelog.

**3.29.1 Silent Changes of the Semantics**

This section lists changes where existing code changes its behavior without the compiler notifying you about it.

- Arithmetic operations revert on underflow and overflow. You can useunchecked { ... }to use the previous
    wrapping behavior.
    Checks for overflow are very common, so we made them the default to increase readability of code, even if it
    comes at a slight increase of gas costs.
- ABI coder v2 is activated by default.
    You can choose to use the old behavior usingpragma abicoder v1;. The pragmapragma experimental
    ABIEncoderV2;is still valid, but it is deprecated and has no effect. If you want to be explicit, please usepragma
    abicoder v2;instead.
    Note that ABI coder v2 supports more types than v1 and performs more sanity checks on the inputs. ABI coder
    v2 makes some function calls more expensive and it can also make contract calls revert that did not revert with
    ABI coder v1 when they contain data that does not conform to the parameter types.
- Exponentiation is right associative, i.e., the expressiona**b**cis parsed asa**(b**c). Before 0.8.0, it was
    parsed as(a**b)**c.
    This is the common way to parse the exponentiation operator.

**306 Chapter 3. Contents**


- Failing assertions and other internal checks like division by zero or arithmetic overflow do not use the invalid
    opcode but instead the revert opcode. More specifically, they will use error data equal to a function call to
    Panic(uint256)with an error code specific to the circumstances.
    This will save gas on errors while it still allows static analysis tools to distinguish these situations from a revert
    on invalid input, like a failingrequire.
- If a byte array in storage is accessed whose length is encoded incorrectly, a panic is caused. A contract cannot
    get into this situation unless inline assembly is used to modify the raw representation of storage byte arrays.
- If constants are used in array length expressions, previous versions of Solidity would use arbitrary precision in
    all branches of the evaluation tree. Now, if constant variables are used as intermediate expressions, their values
    will be properly rounded in the same way as when they are used in run-time expressions.
- The typebytehas been removed. It was an alias ofbytes1.

**3.29.2 New Restrictions**

This section lists changes that might cause existing contracts to not compile anymore.

- There are new restrictions related to explicit conversions of literals. The previous behavior in the following cases
    was likely ambiguous:
       1. Explicit conversions from negative literals and literals larger thantype(uint160).maxtoaddressare
          disallowed.
       2. Explicit conversions between literals and an integer typeTare only allowed if the literal lies between
          type(T).minandtype(T).max. In particular, replace usages ofuint(-1)withtype(uint).max.
       3. Explicit conversions between literals and enums are only allowed if the literal can represent a value in the
          enum.
       4. Explicit conversions between literals andaddresstype (e.g.address(literal)) have the typeaddress
          instead ofaddress payable. One can get a payable address type by using an explicit conversion, i.e.,
          payable(literal).
- _Address literals_ have the type address instead of address payable. They
    can be converted to address payable by using an explicit conversion, e.g.
    payable(0xdCad3a6d3569DF655070DEd06cb7A1b2Ccd1D3AF).
- There are new restrictions on explicit type conversions. The conversion is only allowed when there is at most
    one change in sign, width or type-category (int,address,bytesNN, etc.). To perform multiple changes, use
    multiple conversions.
    Let us use the notationT(S)to denote the explicit conversionT(x), where,TandSare types, andxis any
    arbitrary variable of typeS. An example of such a disallowed conversion would beuint16(int8)since it
    changes both width (8 bits to 16 bits) and sign (signed integer to unsigned integer). In order to do the conversion,
    one has to go through an intermediate type. In the previous example, this would beuint16(uint8(int8))
    oruint16(int16(int8)). Note that the two ways to convert will produce different results e.g., for-1. The
    following are some examples of conversions that are disallowed by this rule.
       **-** address(uint)anduint(address): converting both type-category and width. Replace this by
          address(uint160(uint))anduint(uint160(address))respectively.
       **-** payable(uint160), payable(bytes20) and payable(integer-literal): converting
          both type-category and state-mutability. Replace this by payable(address(uint160)),
          payable(address(bytes20)) and payable(address(integer-literal)) respectively. Note
          thatpayable(0)is valid and is an exception to the rule.
       **-** int80(bytes10)andbytes10(int80): converting both type-category and sign. Replace this by
          int80(uint80(bytes10))andbytes10(uint80(int80)respectively.

**3.29. Solidity v0.8.0 Breaking Changes 307**


**-** Contract(uint): converting both type-category and width. Replace this by
    Contract(address(uint160(uint))).
These conversions were disallowed to avoid ambiguity. For example, in the expression uint16 x =
uint16(int8(-1)), the value ofxwould depend on whether the sign or the width conversion was applied
first.
- Function call options can only be given once, i.e.c.f{gas: 10000}{value: 1}()is invalid and has to be
changed toc.f{gas: 10000, value: 1}().
- The global functionslog0,log1,log2,log3andlog4have been removed.
These are low-level functions that were largely unused. Their behavior can be accessed from inline assembly.
- enumdefinitions cannot contain more than 256 members.
This will make it safe to assume that the underlying type in the ABI is alwaysuint8.
- Declarations with the namethis,superand_are disallowed, with the exception of public functions and events.
The exception is to make it possible to declare interfaces of contracts implemented in languages other than
Solidity that do permit such function names.
- Remove support for the\b,\f, and\vescape sequences in code. They can still be inserted via hexadecimal
escapes, e.g.\x08,\x0c, and\x0b, respectively.
- The global variablestx.originandmsg.senderhave the typeaddressinstead ofaddress payable.
One can convert them intoaddress payableby using an explicit conversion, i.e.,payable(tx.origin)
orpayable(msg.sender).
This change was done since the compiler cannot determine whether or not these addresses are payable or not, so
it now requires an explicit conversion to make this requirement visible.
- Explicit conversion intoaddresstype always returns a non-payableaddresstype. In particular, the following
explicit conversions have the typeaddressinstead ofaddress payable:
**-** address(u)whereuis a variable of typeuint160. One can convertuinto the typeaddress payable
by using two explicit conversions, i.e.,payable(address(u)).
**-** address(b)wherebis a variable of typebytes20. One can convertbinto the typeaddress payable
by using two explicit conversions, i.e.,payable(address(b)).
**-** address(c)wherecis a contract. Previously, the return type of this conversion depended on whether
the contract can receive Ether (either by having a receive function or a payable fallback function). The
conversionpayable(c)has the typeaddress payableand is only allowed when the contractccan
receive Ether. In general, one can always convertcinto the typeaddress payableby using the following
explicit conversion:payable(address(c)). Note thataddress(this)falls under the same category as
address(c)and the same rules apply for it.
- Thechainidbuiltin in inline assembly is now consideredviewinstead ofpure.
- Unary negation cannot be used on unsigned integers anymore, only on signed integers.

**308 Chapter 3. Contents**


**3.29.3 Interface Changes**

- The output of--combined-jsonhas changed: JSON fieldsabi,devdoc,userdocandstorage-layoutare
    sub-objects now. Before 0.8.0 they used to be serialised as strings.
- The “legacy AST” has been removed (--ast-jsonon the commandline interface andlegacyASTfor standard
    JSON). Use the “compact AST” (--ast-compact-jsonresp.AST) as replacement.
- The old error reporter (--old-reporter) has been removed.

**3.29.4 How to update your code**

- If you rely on wrapping arithmetic, surround each operation withunchecked { ... }.
- Optional: If you use SafeMath or a similar library, changex.add(y)tox + y,x.mul(y)tox * yetc.
- Addpragma abicoder v1;if you want to stay with the old ABI coder.
- Optionally removepragma experimental ABIEncoderV2orpragma abicoder v2since it is redundant.
- Changebytetobytes1.
- Add intermediate explicit type conversions if required.
- Combinec.f{gas: 10000}{value: 1}()toc.f{gas: 10000, value: 1}().
- Changemsg.sender.transfer(x)topayable(msg.sender).transfer(x)or use a stored variable of
    address payabletype.
- Changex**y**zto(x**y)**z.
- Use inline assembly as a replacement forlog0, ...,log4.
- Negate unsigned integers by subtracting them from the maximum value of the type and adding 1 (e.g.
    type(uint256).max - x + 1, while ensuring thatxis not zero)

### 3.30 NatSpec Format

Solidity contracts can use a special form of comments to provide rich documentation for functions, return variables
and more. This special form is named the Ethereum Natural Language Specification Format (NatSpec).

**Note:** NatSpec was inspired by Doxygen. While it uses Doxygen-style comments and tags, there is no intention to
keep strict compatibility with Doxygen. Please carefully examine the supported tags listed below.

This documentation is segmented into developer-focused messages and end-user-facing messages. These messages
may be shown to the end user (the human) at the time that they will interact with the contract (i.e. sign a transaction).

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the
ABI).

NatSpec includes the formatting for comments that the smart contract author will use, and which are understood by
the Solidity compiler. Also detailed below is output of the Solidity compiler, which extracts these comments into a
machine-readable format.

NatSpec may also include annotations used by third-party tools. These are most likely accomplished via the
@custom:<name>tag, and a good use case is analysis and verification tools.

**3.30. NatSpec Format 309**


**3.30.1 Documentation Example**

Documentation is inserted above eachcontract,interface,library,function, andeventusing the Doxygen
notation format. Apublicstate variable is equivalent to afunctionfor the purposes of NatSpec.

- For Solidity you may choose///for single or multi-line comments, or/**and ending with*/.
- For Vyper, use"""indented to the inner contents with bare comments. See the Vyper documentation.

The following example shows a contract and a function using all available tags.

**Note:** The Solidity compiler only interprets tags if they are external or public. You are welcome to use similar
comments for your internal and private functions, but those will not be parsed.

This may change in the future.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.2 <0.9.0;

/// @title A simulator for trees
/// @author Larry A. Gardner
/// @notice You can use this contract for only the most basic simulation
/// @dev All function calls are currently implemented without side effects
/// @custom:experimental This is an experimental contract.
contract Tree{
/// @notice Calculate tree age in years, rounded up, for live trees
/// @dev The Alexandr N. Tetearing algorithm could increase precision
/// @param rings The number of rings from dendrochronological sample
/// @return Age in years, rounded up for partial years
functionage(uint256rings)externalvirtual purereturns(uint256) {
returnrings + 1;
}

/// @notice Returns the amount of leaves the tree has.
/// @dev Returns only a fixed number.
functionleaves()externalvirtual purereturns(uint256) {
return2;
}
}

contract Plant{
functionleaves()externalvirtual purereturns(uint256) {
return3;
}
}

contract KumquatTree is Tree, Plant {
functionage(uint256rings)externaloverride pure returns(uint256) {
returnrings + 2;
}

```
/// Return the amount of leaves that this specific kind of tree has
/// @inheritdoc Tree
functionleaves()externaloverride(Tree, Plant) purereturns(uint256) {
(continues on next page)
```
**310 Chapter 3. Contents**


(continued from previous page)
return3;
}
}

**3.30.2 Tags**

All tags are optional. The following table explains the purpose of each NatSpec tag and where it may be used. As a
special case, if no tags are used then the Solidity compiler will interpret a///or/**comment in the same way as if
it were tagged with@notice.

```
Tag Context
@title A title that should describe the contract/interface contract, library, interface, struct, enum
@author The name of the author contract, library, interface, struct, enum
@notice Explain to an end user what this does contract, library, interface, function, public state
variable, event, struct, enum, error
@dev Explain to a developer any extra details contract, library, interface, function, state vari-
able, event, struct, enum, error
@param Documents a parameter just like in Doxygen (must
be followed by parameter name)
```
```
function, event, error
```
```
@return Documents the return variables of a contract’s func-
tion
```
```
function, public state variable
```
```
@inheritdocCopies all missing tags from the base function (must
be followed by the contract name)
```
```
function, public state variable
```
```
@custom:.
..
```
```
Custom tag, semantics is application-defined everywhere
```
If your function returns multiple values, like(int quotient, int remainder)then use multiple@returnstate-
ments in the same format as the@paramstatements.

Custom tags start with@custom:and must be followed by one or more lowercase letters or hyphens. It cannot start
with a hyphen however. They can be used everywhere and are part of the developer documentation.

**Dynamic expressions**

The Solidity compiler will pass through NatSpec documentation from your Solidity source code to the JSON output as
described in this guide. The consumer of this JSON output, for example the end-user client software, may present this
to the end-user directly or it may apply some pre-processing.

For example, some client software will render:

/// @notice This function will multiply`a` by 7

to the end-user as:

This function will multiply 10 by 7

if a function is being called and the inputais assigned a value of 10.

**3.30. NatSpec Format 311**


**Inheritance Notes**

Functions without NatSpec will automatically inherit the documentation of their base function. Exceptions to this are:

- When the parameter names are different.
- When there is more than one base function.
- When there is an explicit@inheritdoctag which specifies which contract should be used to inherit.

**3.30.3 Documentation Output**

When parsed by the compiler, documentation such as the one from the above example will produce two different JSON
files. One is meant to be consumed by the end user as a notice when a function is executed and the other to be used by
the developer.

If the above contract is saved asex1.solthen you can generate the documentation using:

solc --userdoc --devdoc ex1.sol

And the output is below.

**Note:** Starting Solidity version 0.6.11 the NatSpec output also contains aversionand akindfield. Currently the
versionis set to 1 andkindmust be one ofuserordev. In the future it is possible that new versions will be
introduced, deprecating older ones.

**User Documentation**

The above documentation will produce the following user documentation JSON file as output:

{
"version" : 1,
"kind" : "user",
"methods" :
{
"age(uint256)":
{
"notice": "Calculate tree age in years, rounded up, for live trees"
}
},
"notice" : "You can use this contract for only the most basic simulation"
}

Note that the key by which to find the methods is the function’s canonical signature as defined in the _Contract ABI_ and
not simply the function’s name.

**312 Chapter 3. Contents**


**Developer Documentation**

Apart from the user documentation file, a developer documentation JSON file should also be produced and should look
like this:

{
"version" : 1,
"kind" : "dev",
"author" : "Larry A. Gardner",
"details" : "All function calls are currently implemented without side effects",
"custom:experimental" : "This is an experimental contract.",
"methods" :
{
"age(uint256)":
{
"details" : "The Alexandr N. Tetearing algorithm could increase precision",
"params":
{
"rings": "The number of rings from dendrochronological sample"
},
"return": "age in years, rounded up for partial years"
}
},
"title": "A simulator for trees"
}

### 3.31 SMTChecker and Formal Verification

Using formal verification it is possible to perform an automated mathematical proof that your source code fulfills a
certain formal specification. The specification is still formal (just as the source code), but usually much simpler.

Note that formal verification itself can only help you understand the difference between what you did (the specification)
and how you did it (the actual implementation). You still need to check whether the specification is what you wanted
and that you did not miss any unintended effects of it.

Solidity implements a formal verification approach based on SMT (Satisfiability Modulo Theories) and Horn solving.
The SMTChecker module automatically tries to prove that the code satisfies the specification given byrequireand
assertstatements. That is, it considersrequirestatements as assumptions and tries to prove that the conditions
insideassertstatements are always true. If an assertion failure is found, a counterexample may be given to the user
showing how the assertion can be violated. If no warning is given by the SMTChecker for a property, it means that the
property is safe.

The other verification targets that the SMTChecker checks at compile time are:

- Arithmetic underflow and overflow.
- Division by zero.
- Trivial conditions and unreachable code.
- Popping an empty array.
- Out of bounds index access.
- Insufficient funds for a transfer.

**3.31. SMTChecker and Formal Verification 313**


All the targets above are automatically checked by default if all engines are enabled, except underflow and overflow for
Solidity >=0.8.7.

The potential warnings that the SMTChecker reports are:

- <failing property> happens here.. This means that the SMTChecker proved that a certain property fails.
    A counterexample may be given, however in complex situations it may also not show a counterexample. This
    result may also be a false positive in certain cases, when the SMT encoding adds abstractions for Solidity code
    that is either hard or impossible to express.
- <failing property> might happen here. This means that the solver could not prove either case within
    the given timeout. Since the result is unknown, the SMTChecker reports the potential failure for soundness. This
    may be solved by increasing the query timeout, but the problem might also simply be too hard for the engine to
    solve.

To enable the SMTChecker, you must select _which engine should run_ , where the default is no engine. Selecting the
engine enables the SMTChecker on all files.

**Note:** Prior to Solidity 0.8.4, the default way to enable the SMTChecker was via pragma experimental
SMTChecker;and only the contracts containing the pragma would be analyzed. That pragma has been deprecated,
and although it still enables the SMTChecker for backwards compatibility, it will be removed in Solidity 0.9.0. Note
also that now using the pragma even in a single file enables the SMTChecker for all files.

**Note:** The lack of warnings for a verification target represents an undisputed mathematical proof of correctness,
assuming no bugs in the SMTChecker and the underlying solver. Keep in mind that these problems are _very hard_ and
sometimes _impossible_ to solve automatically in the general case. Therefore, several properties might not be solved or
might lead to false positives for large contracts. Every proven property should be seen as an important achievement.
For advanced users, see _SMTChecker Tuning_ to learn a few options that might help proving more complex properties.

**3.31.1 Tutorial**

**Overflow**

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Overflow{
uintimmutable x;
uintimmutable y;

```
functionadd(uintx_,uinty_)internalpurereturns(uint) {
returnx_ + y_;
}
```
```
constructor(uintx_,uinty_) {
(x, y) = (x_, y_);
}
```
```
functionstateAdd() publicviewreturns(uint) {
returnadd(x, y);
(continues on next page)
```
**314 Chapter 3. Contents**


(continued from previous page)
}
}

The contract above shows an overflow check example. The SMTChecker does not check underflow and overflow by
default for Solidity >=0.8.7, so we need to use the command-line option--model-checker-targets "underflow,
overflow"or the JSON optionsettings.modelChecker.targets = ["underflow", "overflow"]. See _this
section for targets configuration_. Here, it reports the following:

Warning: CHC: Overflow (resulting value larger than 2**256 - 1) happens here.
Counterexample:
x = 1, y = 115792089237316195423570985008687907853269984665640564039457584007913129639935
= 0

Transaction trace:
Overflow.constructor(1,␣
˓→115792089237316195423570985008687907853269984665640564039457584007913129639935)
State: x = 1, y =␣
˓→ 115792089237316195423570985008687907853269984665640564039457584007913129639935
Overflow.stateAdd()
Overflow.add(1,␣
˓→115792089237316195423570985008687907853269984665640564039457584007913129639935) --␣
˓→internal call
--> o.sol:9:20:
|
9 | return x_ + y_;
| ^^^^^^^

If we addrequirestatements that filter out overflow cases, the SMTChecker proves that no overflow is reachable (by
not reporting warnings):

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Overflow{
uintimmutable x;
uintimmutable y;

```
functionadd(uintx_,uinty_)internalpurereturns(uint) {
returnx_ + y_;
}
```
```
constructor(uintx_,uinty_) {
(x, y) = (x_, y_);
}
```
functionstateAdd() publicviewreturns(uint) {
require(x < type(uint128).max);
require(y < type(uint128).max);
returnadd(x, y);
}
}

**3.31. SMTChecker and Formal Verification 315**


**Assert**

An assertion represents an invariant in your code: a property that must be true _for all transactions, including all input
and storage values_ , otherwise there is a bug.

The code below defines a functionfthat guarantees no overflow. Functioninvdefines the specification thatfis mono-
tonically increasing: for every possible pair(a, b), ifb > athenf(b) > f(a). Sincefis indeed monotonically
increasing, the SMTChecker proves that our property is correct. You are encouraged to play with the property and the
function definition to see what results come out!

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Monotonic{
functionf(uint x)internalpure returns(uint) {
require(x < type(uint128).max);
returnx * 42;
}

functioninv(uinta, uintb) publicpure {
require(b > a);
assert(f(b) > f(a));
}
}

We can also add assertions inside loops to verify more complicated properties. The following code searches for the
maximum element of an unrestricted array of numbers, and asserts the property that the found element must be greater
or equal every element in the array.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Max{
functionmax(uint[] memorya) publicpure returns(uint) {
uintm = 0;
for(uinti = 0; i < a.length; ++i)
if (a[i] > m)
m = a[i];

```
for(uinti = 0; i < a.length; ++i)
assert(m >= a[i]);
```
returnm;
}
}

Note that in this example the SMTChecker will automatically try to prove three properties:

1. ++iin the first loop does not overflow.
2. ++iin the second loop does not overflow.
3. The assertion is always true.

**Note:** The properties involve loops, which makes it _much much_ harder than the previous examples, so beware of loops!

**316 Chapter 3. Contents**


All the properties are correctly proven safe. Feel free to change the properties and/or add restrictions on the array to
see different results. For example, changing the code to

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Max{
functionmax(uint[] memorya) publicpure returns(uint) {
require(a.length >= 5);
uintm = 0;
for(uinti = 0; i < a.length; ++i)
if (a[i] > m)
m = a[i];

```
for(uinti = 0; i < a.length; ++i)
assert(m > a[i]);
```
returnm;
}
}

gives us:

Warning: CHC: Assertion violation happens here.
Counterexample:

a = [0, 0, 0, 0, 0]
= 0

Transaction trace:
Test.constructor()
Test.max([0, 0, 0, 0, 0])
--> max.sol:14:4:
|
14 | assert(m > a[i]);

**State Properties**

So far the examples only demonstrated the use of the SMTChecker over pure code, proving properties about specific
operations or algorithms. A common type of properties in smart contracts are properties that involve the state of the
contract. Multiple transactions might be needed to make an assertion fail for such a property.

As an example, consider a 2D grid where both axis have coordinates in the range (-2^128, 2^128 - 1). Let us place a
robot at position (0, 0). The robot can only move diagonally, one step at a time, and cannot move outside the grid. The
robot’s state machine can be represented by the smart contract below.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Robot{
intx = 0;
inty = 0;

```
(continues on next page)
```
**3.31. SMTChecker and Formal Verification 317**


```
(continued from previous page)
modifierwall {
require(x > type(int128).min && x < type(int128).max);
require(y > type(int128).min && y < type(int128).max);
_;
}
```
```
functionmoveLeftUp() wallpublic {
--x;
++y;
}
```
```
functionmoveLeftDown() wall public{
--x;
--y;
}
```
```
functionmoveRightUp() wallpublic {
++x;
++y;
}
```
```
functionmoveRightDown() wallpublic{
++x;
--y;
}
```
functioninv()public view {
assert((x + y) % 2 == 0);
}
}

Functioninvrepresents an invariant of the state machine thatx + ymust be even. The SMTChecker manages to
prove that regardless how many commands we give the robot, even if infinitely many, the invariant can _never_ fail. The
interested reader may want to prove that fact manually as well. Hint: this invariant is inductive.

We can also trick the SMTChecker into giving us a path to a certain position we think might be reachable. We can add
the property that (2, 4) is _not_ reachable, by adding the following function.

functionreach_2_4()publicview {
assert(!(x == 2 && y == 4));
}

This property is false, and while proving that the property is false, the SMTChecker tells us exactly _how_ to reach (2, 4):

Warning: CHC: Assertion violation happens here.
Counterexample:
x = 2, y = 4

Transaction trace:
Robot.constructor()
State: x = 0, y = 0
Robot.moveLeftUp()
State: x = (- 1), y = 1
(continues on next page)

**318 Chapter 3. Contents**


```
(continued from previous page)
```
Robot.moveRightUp()
State: x = 0, y = 2
Robot.moveRightUp()
State: x = 1, y = 3
Robot.moveRightUp()
State: x = 2, y = 4
Robot.reach_2_4()
--> r.sol:35:4:
|
35 | assert(!(x == 2 && y == 4));
| ^^^^^^^^^^^^^^^^^^^^^^^^^^^

Note that the path above is not necessarily deterministic, as there are other paths that could reach (2, 4). The choice of
which path is shown might change depending on the used solver, its version, or just randomly.

**External Calls and Reentrancy**

Every external call is treated as a call to unknown code by the SMTChecker. The reasoning behind that is that even if
the code of the called contract is available at compile time, there is no guarantee that the deployed contract will indeed
be the same as the contract where the interface came from at compile time.

In some cases, it is possible to automatically infer properties over state variables that are still true even if the externally
called code can do anything, including reenter the caller contract.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

interface Unknown {
functionrun()external;
}

contract Mutex{
uintx;
boollock;

```
Unknown immutable unknown;
```
```
constructor(Unknown u) {
require(address(u) != address(0));
unknown = u;
}
```
```
modifiermutex {
require(!lock);
lock =true;
_;
lock =false;
}
```
```
functionset(uintx_) mutexpublic {
x = x_;
}
(continues on next page)
```
**3.31. SMTChecker and Formal Verification 319**


```
(continued from previous page)
```
functionrun() mutexpublic{
uintxPre = x;
unknown.run();
assert(xPre == x);
}
}

The example above shows a contract that uses a mutex flag to forbid reentrancy. The solver is able to infer that when
unknown.run()is called, the contract is already “locked”, so it would not be possible to change the value ofx,
regardless of what the unknown called code does.

If we “forget” to use themutexmodifier on functionset, the SMTChecker is able to synthesize the behavior of the
externally called code so that the assertion fails:

Warning: CHC: Assertion violation happens here.
Counterexample:
x = 1, lock = true, unknown = 1

Transaction trace:
Mutex.constructor(1)
State: x = 0, lock = false, unknown = 1
Mutex.run()
unknown.run() -- untrusted external call, synthesized as:
Mutex.set(1) -- reentrant call
--> m.sol:32:3:
|
32 | assert(xPre == x);
| ^^^^^^^^^^^^^^^^^

**3.31.2 SMTChecker Options and Tuning**

**Timeout**

The SMTChecker uses a hardcoded resource limit (rlimit) chosen per solver, which is not precisely related to time.
We chose therlimitoption as the default because it gives more determinism guarantees than time inside the solver.

This options translates roughly to “a few seconds timeout” per query. Of course many properties are very complex
and need a lot of time to be solved, where determinism does not matter. If the SMTChecker does not manage to
solve the contract properties with the defaultrlimit, a timeout can be given in milliseconds via the CLI option
--model-checker-timeout <time>or the JSON optionsettings.modelChecker.timeout=<time>, where 0
means no timeout.

**320 Chapter 3. Contents**


**Verification Targets**

The types of verification targets created by the SMTChecker can also be customized via the CLI option
--model-checker-target <targets>or the JSON optionsettings.modelChecker.targets=<targets>. In
the CLI case,<targets>is a no-space-comma-separated list of one or more verification targets, and an array of one
or more targets as strings in the JSON input. The keywords that represent the targets are:

- Assertions:assert.
- Arithmetic underflow:underflow.
- Arithmetic overflow:overflow.
- Division by zero:divByZero.
- Trivial conditions and unreachable code:constantCondition.
- Popping an empty array:popEmptyArray.
- Out of bounds array/fixed bytes index access:outOfBounds.
- Insufficient funds for a transfer:balance.
- All of the above:default(CLI only).

A common subset of targets might be, for example:--model-checker-targets assert,overflow.

All targets are checked by default, except underflow and overflow for Solidity >=0.8.7.

There is no precise heuristic on how and when to split verification targets, but it can be useful especially when dealing
with large contracts.

**Proved Targets**

If there are any proved targets, the SMTChecker issues one warning per engine stating how many targets were proved. If
the user wishes to see all the specific proved targets, the CLI option--model-checker-show-provedand the JSON
optionsettings.modelChecker.showProved = truecan be used.

**Unproved Targets**

If there are any unproved targets, the SMTChecker issues one warning stating how many unproved targets there are. If
the user wishes to see all the specific unproved targets, the CLI option--model-checker-show-unprovedand the
JSON optionsettings.modelChecker.showUnproved = truecan be used.

**Unsupported Language Features**

Certain Solidity language features are not completely supported by the SMT encoding that the SMTChecker applies,
for example assembly blocks. The unsupported construct is abstracted via overapproximation to preserve soundness,
meaning any properties reported safe are safe even though this feature is unsupported. However such abstraction may
cause false positives when the target properties depend on the precise behavior of the unsupported feature. If the encoder
encounters such cases it will by default report a generic warning stating how many unsupported features it has seen. If
the user wishes to see all the specific unsupported features, the CLI option--model-checker-show-unsupported
and the JSON optionsettings.modelChecker.showUnsupported = truecan be used, where their default value
isfalse.

**3.31. SMTChecker and Formal Verification 321**


**Verified Contracts**

By default all the deployable contracts in the given sources are analyzed separately as the one that will be deployed.
This means that if a contract has many direct and indirect inheritance parents, all of them will be analyzed on their own,
even though only the most derived will be accessed directly on the blockchain. This causes an unnecessary burden on
the SMTChecker and the solver. To aid cases like this, users can specify which contracts should be analyzed as the
deployed one. The parent contracts are of course still analyzed, but only in the context of the most derived contract,
reducing the complexity of the encoding and generated queries. Note that abstract contracts are by default not analyzed
as the most derived by the SMTChecker.

The chosen contracts can be given via a comma-separated list (whitespace is not allowed) of <source>:<contract>
pairs in the CLI:--model-checker-contracts "<source1.sol:contract1>,<source2.sol:contract2>,
<source2.sol:contract3>", and via the objectsettings.modelChecker.contractsin the _JSON input_ , which
has the following form:

"contracts": {
"source1.sol": ["contract1"],
"source2.sol": ["contract2", "contract3"]
}

**Trusted External Calls**

By default, the SMTChecker does not assume that compile-time available code is the same as the runtime code for
external calls. Take the following contracts as an example:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Ext{
uint publicx;
functionsetX(uint_x)public { x = _x; }
}
contract MyContract {
functioncallExt(Ext _e) public{
_e.setX(42);
assert(_e.x() == 42);
}
}

WhenMyContract.callExtis called, an address is given as the argument. At deployment time, we cannot know for
sure that address_eactually contains a deployment of contractExt. Therefore, the SMTChecker will warn that the
assertion above can be violated, which is true, if_econtains another contract thanExt.

However, it can be useful to treat these external calls as trusted, for example, to test that different implementations of
an interface conform to the same property. This means assuming that address_eindeed was deployed as contractExt.
This mode can be enabled via the CLI option--model-checker-ext-calls=trustedor the JSON fieldsettings.
modelChecker.extCalls: "trusted".

Please be aware that enabling this mode can make the SMTChecker analysis much more computationally costly.

An important part of this mode is that it is applied to contract types and high level external calls to contracts, and
not low level calls such ascallanddelegatecall. The storage of an address is stored per contract type, and the
SMTChecker assumes that an externally called contract has the type of the caller expression. Therefore, casting an
addressor a contract to different contract types will yield different storage values and can give unsound results if the
assumptions are inconsistent, such as the example below:

**322 Chapter 3. Contents**


// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract D {
constructor(uint_x) { x = _x; }
uint publicx;
functionsetX(uint_x)public { x = _x; }
}

contract E {
constructor() { x = 2; }
uint publicx;
functionsetX(uint_x)public { x = _x; }
}

contract C {
functionf()public {
addressd =address(newD(42));

```
// `d` was deployed as`D`, so its`x`should be 42 now.
assert(D(d).x() == 42);// should hold
assert(D(d).x() == 43);// should fail
```
```
// E and D have the same interface, so the following
// call would also work at runtime.
// However, the change to`E(d)` is not reflected in`D(d)`.
E(d).setX(1024);
```
// Reading from `D(d)`now will show old values.
// The assertion below should fail at runtime,
// but succeeds in this mode's analysis (unsound).
assert(D(d).x() == 42);
// The assertion below should succeed at runtime,
// but fails in this mode's analysis (false positive).
assert(D(d).x() == 1024);
}
}

Due to the above, make sure that the trusted external calls to a certain variable ofaddressorcontracttype always
have the same caller expression type.

It is also helpful to cast the called contract’s variable as the type of the most derived type in case of inheritance.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

interface Token {
functionbalanceOf(address_a)externalviewreturns(uint);
functiontransfer(address_to,uint_amt) external;
}

contract TokenCorrect isToken {
mapping(address=> uint) balance;
(continues on next page)

**3.31. SMTChecker and Formal Verification 323**


(continued from previous page)
constructor(address_a,uint _b) {
balance[_a] = _b;
}
functionbalanceOf(address_a)public view overridereturns(uint) {
returnbalance[_a];
}
functiontransfer(address_to,uint_amt) publicoverride {
require(balance[msg.sender] >= _amt);
balance[msg.sender] -= _amt;
balance[_to] += _amt;
}
}

contract Test{
functionproperty_transfer(address_token,address_to,uint_amt)public {
require(_to !=address(this));

```
TokenCorrect t = TokenCorrect(_token);
```
```
uintxPre = t.balanceOf(address(this));
require(xPre >= _amt);
uintyPre = t.balanceOf(_to);
```
```
t.transfer(_to, _amt);
uintxPost = t.balanceOf(address(this));
uintyPost = t.balanceOf(_to);
```
assert(xPost == xPre - _amt);
assert(yPost == yPre + _amt);
}
}

Note that in functionproperty_transfer, the external calls are performed on variablet.

Another caveat of this mode are calls to state variables of contract type outside the analyzed contract. In the code
below, even thoughBdeploysA, it is also possible for the address stored inB.ato be called by anyone outside ofB
in between transactions toBitself. To reflect the possible changes toB.a, the encoding allows an unbounded number
of calls to be made toB.aexternally. The encoding will keep track ofB.a’s storage, therefore assertion (2) should
hold. However, currently the encoding allows such calls to be made fromBconceptually, therefore assertion (3) fails.
Making the encoding stronger logically is an extension of the trusted mode and is under development. Note that the
encoding does not keep track of storage foraddressvariables, therefore ifB.ahad typeaddressthe encoding would
assume that its storage does not change in between transactions toB.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract A {
uint publicx;
addressimmutablepublic owner;
constructor() {
owner =msg.sender;
}
functionsetX(uint_x)public {
(continues on next page)

**324 Chapter 3. Contents**


(continued from previous page)
require(msg.sender== owner);
x = _x;
}
}

contract B {
A a;
constructor() {
a =newA();
assert(a.x() == 0);// (1) should hold
}
functiong()public view {
assert(a.owner() ==address(this));// (2) should hold
assert(a.x() == 0);// (3) should hold, but fails due to a false positive
}
}

**Reported Inferred Inductive Invariants**

For properties that were proved safe with the CHC engine, the SMTChecker can retrieve inductive invariants that were
inferred by the Horn solver as part of the proof. Currently only two types of invariants can be reported to the user:

- Contract Invariants: these are properties over the contract’s state variables that are true before and after every
    possible transaction that the contract may ever run. For example,x >= y, wherexandyare a contract’s state
    variables.
- Reentrancy Properties: they represent the behavior of the contract in the presence of external calls to unknown
    code. These properties can express a relation between the value of the state variables before and after the external
    call, where the external call is free to do anything, including making reentrant calls to the analyzed contract.
    Primed variables represent the state variables’ values after said external call. Example:lock -> x = x'.

The user can choose the type of invariants to be reported using the CLI option--model-checker-invariants
"contract,reentrancy"or as an array in the fieldsettings.modelChecker.invariantsin the _JSON input_. By
default the SMTChecker does not report invariants.

**Division and Modulo With Slack Variables**

Spacer, the default Horn solver used by the SMTChecker, often dislikes division and modulo operations inside Horn
rules. Because of that, by default the Solidity division and modulo operations are encoded using the constrainta = b
* d + mwhered = a / bandm = a % b. However, other solvers, such as Eldarica, prefer the syntactically pre-
cise operations. The command-line flag--model-checker-div-mod-no-slacksand the JSON optionsettings.
modelChecker.divModNoSlackscan be used to toggle the encoding depending on the used solver preferences.

**3.31. SMTChecker and Formal Verification 325**


**Natspec Function Abstraction**

Certain functions including common math methods such aspowandsqrtmay be too complex to be analyzed in a
fully automated way. These functions can be annotated with Natspec tags that indicate to the SMTChecker that these
functions should be abstracted. This means that the body of the function is not used, and when called, the function
will:

- Return a nondeterministic value, and either keep the state variables unchanged if the abstracted function is
    view/pure, or also set the state variables to nondeterministic values otherwise. This can be used via the an-
    notation/// @custom:smtchecker abstract-function-nondet.
- Act as an uninterpreted function. This means that the semantics of the function (given by the body) are ig-
    nored, and the only property this function has is that given the same input it guarantees the same output.
    This is currently under development and will be available via the annotation/// @custom:smtchecker
    abstract-function-uf.

**Model Checking Engines**

The SMTChecker module implements two different reasoning engines, a Bounded Model Checker (BMC) and a system
of Constrained Horn Clauses (CHC). Both engines are currently under development, and have different characteristics.
The engines are independent and every property warning states from which engine it came. Note that all the examples
above with counterexamples were reported by CHC, the more powerful engine.

By default both engines are used, where CHC runs first, and every property that was not proven is passed over to BMC.
You can choose a specific engine via the CLI option--model-checker-engine {all,bmc,chc,none}or the JSON
optionsettings.modelChecker.engine={all,bmc,chc,none}.

**Bounded Model Checker (BMC)**

The BMC engine analyzes functions in isolation, that is, it does not take the overall behavior of the contract over
multiple transactions into account when analyzing each function. Loops are also ignored in this engine at the moment.
Internal function calls are inlined as long as they are not recursive, directly or indirectly. External function calls are
inlined if possible. Knowledge that is potentially affected by reentrancy is erased.

The characteristics above make BMC prone to reporting false positives, but it is also lightweight and should be able to
quickly find small local bugs.

**Constrained Horn Clauses (CHC)**

A contract’s Control Flow Graph (CFG) is modelled as a system of Horn clauses, where the life cycle of the contract is
represented by a loop that can visit every public/external function non-deterministically. This way, the behavior of the
entire contract over an unbounded number of transactions is taken into account when analyzing any function. Loops
are fully supported by this engine. Internal function calls are supported, and external function calls assume the called
code is unknown and can do anything.

The CHC engine is much more powerful than BMC in terms of what it can prove, and might require more computing
resources.

**326 Chapter 3. Contents**


**SMT and Horn solvers**

The two engines detailed above use automated theorem provers as their logical backends. BMC uses an SMT solver,
whereas CHC uses a Horn solver. Often the same tool can act as both, as seen in z3, which is primarily an SMT solver
and makes Spacer available as a Horn solver, and Eldarica which does both.

The user can choose which solvers should be used, if available, via the CLI option--model-checker-solvers
{all,cvc5,eld,smtlib2,z3}or the JSON optionsettings.modelChecker.solvers=[smtlib2,z3], where:

- cvc5is used via its binary which must be installed in the system. Only BMC usescvc5.
- eldis used via its binary which must be installed in the system. Only CHC useseld, and only ifz3is not
    enabled.
- smtlib2outputs SMT/Horn queries in the smtlib2 format. These can be used together with the compiler’s
    callback mechanism so that any solver binary from the system can be employed to synchronously return the
    results of the queries to the compiler. This can be used by both BMC and CHC depending on which solvers are
    called.
- z3is available
    **-** ifsolcis compiled with it;
    **-** if a dynamicz3library of version >=4.8.x is installed in a Linux system (from Solidity 0.7.6);
    **-** statically insoljson.js(from Solidity 0.6.9), that is, the JavaScript binary of the compiler.

**Note:** z3 version 4.8.16 broke ABI compatibility with previous versions and cannot be used with solc <=0.8.13. If
you are using z3 >=4.8.16 please use solc >=0.8.14, and conversely, only use older z3 with older solc releases. We also
recommend using the latest z3 release which is what SMTChecker also does.

Since both BMC and CHC usez3, andz3is available in a greater variety of environments, including in the browser,
most users will almost never need to be concerned about this option. More advanced users might apply this option to
try alternative solvers on more complex problems.

Please note that certain combinations of chosen engine and solver will lead to the SMTChecker doing nothing, for
example choosing CHC andcvc5.

**3.31.3 Abstraction and False Positives**

The SMTChecker implements abstractions in an incomplete and sound way: If a bug is reported, it might be a false
positive introduced by abstractions (due to erasing knowledge or using a non-precise type). If it determines that a
verification target is safe, it is indeed safe, that is, there are no false negatives (unless there is a bug in the SMTChecker).

If a target cannot be proven you can try to help the solver by using the tuning options in the previous section. If you
are sure of a false positive, addingrequirestatements in the code with more information may also give some more
power to the solver.

**3.31. SMTChecker and Formal Verification 327**


**SMT Encoding and Types**

The SMTChecker encoding tries to be as precise as possible, mapping Solidity types and expressions to their closest
SMT-LIB representation, as shown in the table below.

```
Solidity type SMT sort Theories
Boolean Bool Bool
intN, uintN, address, bytesN, enum, contract Integer LIA, NIA
array, mapping, bytes, string Tuple (Array elements, Integer length) Datatypes, Arrays, LIA
struct Tuple Datatypes
other types Integer LIA
```
Types that are not yet supported are abstracted by a single 256-bit unsigned integer, where their unsupported operations
are ignored.

For more details on how the SMT encoding works internally, see the paper SMT-based Verification of Solidity Smart
Contracts.

**Function Calls**

In the BMC engine, function calls to the same contract (or base contracts) are inlined when possible, that is, when their
implementation is available. Calls to functions in other contracts are not inlined even if their code is available, since
we cannot guarantee that the actual deployed code is the same.

The CHC engine creates nonlinear Horn clauses that use summaries of the called functions to support internal function
calls. External function calls are treated as calls to unknown code, including potential reentrant calls.

Complex pure functions are abstracted by an uninterpreted function (UF) over the arguments.

```
Functions BMC/CHC behavior
assert Verification target.
require Assumption.
internal call BMC: Inline function call. CHC: Function summaries.
external call to known code BMC: Inline function call or erase knowledge about state variables and local storage
references. CHC: Assume called code is unknown. Try to infer invariants that hold
after the call returns.
Storage array push/pop Supported precisely. Checks whether it is popping an empty array.
ABI functions Abstracted with UF.
addmod,mulmod Supported precisely.
gasleft, blockhash,
keccak256, ecrecover
ripemd160
```
```
Abstracted with UF.
```
```
pure functions without im-
plementation (external or
complex)
```
```
Abstracted with UF
```
```
external functions without
implementation
```
```
BMC: Erase state knowledge and assume result is nondeterministic. CHC: Nonde-
terministic summary. Try to infer invariants that hold after the call returns.
transfer BMC: Checks whether the contract’s balance is sufficient. CHC: does not yet perform
the check.
others Currently unsupported
```
Using abstraction means loss of precise knowledge, but in many cases it does not mean loss of proving power.

**328 Chapter 3. Contents**


// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Recover
{
functionf(
bytes32hash,
uint8v1,uint8 v2,
bytes32r1,bytes32r2,
bytes32s1,bytes32s2
)public purereturns(address) {
addressa1 = ecrecover(hash, v1, r1, s1);
require(v1 == v2);
require(r1 == r2);
require(s1 == s2);
addressa2 = ecrecover(hash, v2, r2, s2);
assert(a1 == a2);
returna1;
}
}

In the example above, the SMTChecker is not expressive enough to actually computeecrecover, but by modelling
the function calls as uninterpreted functions we know that the return value is the same when called on equivalent
parameters. This is enough to prove that the assertion above is always true.

Abstracting a function call with an UF can be done for functions known to be deterministic, and can be easily done
for pure functions. It is however difficult to do this with general external functions, since they might depend on state
variables.

**Reference Types and Aliasing**

Solidity implements aliasing for reference types with the same _data location_. That means one variable may be modified
through a reference to the same data area. The SMTChecker does not keep track of which references refer to the same
data. This implies that whenever a local reference or state variable of reference type is assigned, all knowledge regarding
variables of the same type and data location is erased. If the type is nested, the knowledge removal also includes all
the prefix base types.

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.0;

contract Aliasing
{
uint[] array1;
uint[][] array2;
functionf(
uint[]memory a,
uint[]memory b,
uint[][]memory c,
uint[] storage d
)internal{
array1[0] = 42;
a[0] = 2;
c[0][0] = 2;
(continues on next page)

**3.31. SMTChecker and Formal Verification 329**


(continued from previous page)
b[0] = 1;
// Erasing knowledge about memory references should not
// erase knowledge about state variables.
assert(array1[0] == 42);
// However, an assignment to a storage reference will erase
// storage knowledge accordingly.
d[0] = 2;
// Fails as false positive because of the assignment above.
assert(array1[0] == 42);
// Fails because`a == b` is possible.
assert(a[0] == 2);
// Fails because`c[i] == b` is possible.
assert(c[0][0] == 2);
assert(d[0] == 2);
assert(b[0] == 1);
}
functiong(
uint[]memory a,
uint[]memory b,
uint[][]memory c,
uintx
)public {
f(a, b, c, array2[x]);
}
}

After the assignment tob[0], we need to clear knowledge aboutasince it has the same type (uint[]) and data location
(memory). We also need to clear knowledge aboutc, since its base type is also auint[]located in memory. This
implies that somec[i]could refer to the same data asbora.

Notice that we do not clear knowledge aboutarrayanddbecause they are located in storage, even though they also
have typeuint[]. However, ifdwas assigned, we would need to clear knowledge aboutarrayand vice-versa.

**Contract Balance**

A contract may be deployed with funds sent to it, ifmsg.value> 0 in the deployment transaction. However, the con-
tract’s address may already have funds before deployment, which are kept by the contract. Therefore, the SMTChecker
assumes thataddress(this).balance >= msg.valuein the constructor in order to be consistent with the EVM
rules. The contract’s balance may also increase without triggering any calls to the contract, if

- selfdestructis executed by another contract with the analyzed contract as the target of the remaining funds,
- the contract is the coinbase (i.e.,block.coinbase) of some block.

To model this properly, the SMTChecker assumes that at every new transaction the contract’s balance may grow by at
leastmsg.value.

**330 Chapter 3. Contents**


**3.31.4 Real World Assumptions**

Some scenarios can be expressed in Solidity and the EVM, but are expected to never occur in practice. One of such
cases is the length of a dynamic storage array overflowing during a push: If thepushoperation is applied to an array
of length 2^256 - 1, its length silently overflows. However, this is unlikely to happen in practice, since the operations
required to grow the array to that point would take billions of years to execute. Another similar assumption taken by
the SMTChecker is that an address’ balance can never overflow.

A similar idea was presented in EIP-1985.

### 3.32 Yul

Yul (previously also called JULIA or IULIA) is an intermediate language that can be compiled to bytecode for different
backends.

It can be used in stand-alone mode and for “inline assembly” inside Solidity. The compiler uses Yul as an intermediate
language in the IR-based code generator (“new codegen” or “IR-based codegen”). Yul is a good target for high-level
optimisation stages that can benefit all target platforms equally.

**3.32.1 Motivation and High-level Description**

The design of Yul tries to achieve several goals:

1. Programs written in Yul should be readable, even if the code is generated by a compiler from Solidity or another
    high-level language.
2. Control flow should be easy to understand to help in manual inspection, formal verification and optimization.
3. The translation from Yul to bytecode should be as straightforward as possible.
4. Yul should be suitable for whole-program optimization.

In order to achieve the first and second goal, Yul provides high-level constructs likeforloops,ifandswitchstate-
ments and function calls. These should be sufficient for adequately representing the control flow for assembly programs.
Therefore, no explicit statements forSWAP,DUP,JUMPDEST,JUMPandJUMPIare provided, because the first two obfus-
cate the data flow and the last two obfuscate control flow. Furthermore, functional statements of the formmul(add(x,
y), 7)are preferred over pure opcode statements like7 y x add mulbecause in the first form, it is much easier to
see which operand is used for which opcode.

Even though it was designed for stack machines, Yul does not expose the complexity of the stack itself. The programmer
or auditor should not have to worry about the stack.

The third goal is achieved by compiling the higher level constructs to bytecode in a very regular way. The only non-
local operation performed by the assembler is name lookup of user-defined identifiers (functions, variables, ...) and
cleanup of local variables from the stack.

To avoid confusions between concepts like values and references, Yul is statically typed. At the same time, there is a
default type (usually the integer word of the target machine) that can always be omitted to help readability.

To keep the language simple and flexible, Yul does not have any built-in operations, functions or types in its pure form.
These are added together with their semantics when specifying a dialect of Yul, which allows specializing Yul to the
requirements of different target platforms and feature sets.

Currently, there is only one specified dialect of Yul. This dialect uses the EVM opcodes as builtin functions (see below)
and defines only the typeu256, which is the native 256-bit type of the EVM. Because of that, we will not provide types
in the examples below.

**3.32. Yul 331**


**3.32.2 Simple Example**

The following example program is written in the EVM dialect and computes exponentiation. It can be compiled using
solc --strict-assembly. The builtin functionsmulanddivcompute product and division, respectively.

{
functionpower(base, exponent) -> result
{
switchexponent
case0 { result := 1 }
case1 { result := base }
default
{
result := power(mul(base, base), div(exponent, 2))
switchmod(exponent, 2)
case1 { result := mul(base, result) }
}
}
}

It is also possible to implement the same function using a for-loop instead of with recursion. Here,lt(a, b)computes
whetherais less thanb.

{
functionpower(base, exponent) -> result
{
result := 1
for{leti := 0 } lt(i, exponent) { i := add(i, 1) }
{
result := mul(result, base)
}
}
}

At the _end of the section_ , a complete implementation of the ERC-20 standard can be found.

**3.32.3 Stand-Alone Usage**

You can use Yul in its stand-alone form in the EVM dialect using the Solidity compiler. This will use the _Yul object
notation_ so that it is possible to refer to code as data to deploy contracts. This Yul mode is available for the commandline
compiler (use--strict-assembly) and for the _standard-json interface_ :

{
"language": "Yul",
"sources": {"input.yul": {"content": "{ sstore(0, 1) }" } },
"settings": {
"outputSelection": {"*": {"*": ["*"],"": [ "*" ] } },
"optimizer": {"enabled": true,"details": {"yul": true} }
}
}

**332 Chapter 3. Contents**


```
Warning: Yul is in active development and bytecode generation is only fully implemented for the EVM dialect of
Yul with EVM 1.0 as target.
```
**3.32.4 Informal Description of Yul**

In the following, we will talk about each individual aspect of the Yul language. In examples, we will use the default
EVM dialect.

**Syntax**

Yul parses comments, literals and identifiers in the same way as Solidity, so you can e.g. use//and/* */to denote
comments. There is one exception: Identifiers in Yul can contain dots:..

Yul can specify “objects” that consist of code, data and sub-objects. Please see _Yul Objects_ below for details on that. In
this section, we are only concerned with the code part of such an object. This code part always consists of a curly-braces
delimited block. Most tools support specifying just a code block where an object is expected.

Inside a code block, the following elements can be used (see the later sections for more details):

- literals, e.g.0x123, 42 or"abc"(strings up to 32 characters)
- calls to builtin functions, e.g.add(1, mload(0))
- variable declarations, e.g.let x := 7,let x := add(y, 3)orlet x(initial value of 0 is assigned)
- identifiers (variables), e.g.add(3, x)
- assignments, e.g.x := add(y, 3)
- blocks where local variables are scoped inside, e.g.{ let x := 3 { let y := add(x, 1) } }
- if statements, e.g.if lt(a, b) { sstore(0, 1) }
- switch statements, e.g.switch mload(0) case 0 { revert() } default { mstore(0, 1) }
- for loops, e.g.for { let i := 0} lt(i, 10) { i := add(i, 1) } { mstore(i, 7) }
- function definitions, e.g.function f(a, b) -> c { c := add(a, b) }

Multiple syntactical elements can follow each other simply separated by whitespace, i.e. there is no terminating;or
newline required.

**Literals**

As literals, you can use:

- Integer constants in decimal or hexadecimal notation.
- ASCII strings (e.g."abc"), which may contain hex escapes\xNNand Unicode escapes\uNNNNwhereNare
    hexadecimal digits.
- Hex strings (e.g.hex"616263").

In the EVM dialect of Yul, literals represent 256-bit words as follows:

- Decimal or hexadecimal constants must be less than2**256. They represent the 256-bit word with that value as
    an unsigned integer in big endian encoding.

**3.32. Yul 333**


- An ASCII string is first viewed as a byte sequence, by viewing a non-escape ASCII character as a single byte
    whose value is the ASCII code, an escape\xNNas single byte with that value, and an escape\uNNNNas the
    UTF-8 sequence of bytes for that code point. The byte sequence must not exceed 32 bytes. The byte sequence is
    padded with zeros on the right to reach 32 bytes in length; in other words, the string is stored left-aligned. The
    padded byte sequence represents a 256-bit word whose most significant 8 bits are the ones from the first byte,
    i.e. the bytes are interpreted in big endian form.
- A hex string is first viewed as a byte sequence, by viewing each pair of contiguous hex digits as a byte. The byte
    sequence must not exceed 32 bytes (i.e. 64 hex digits), and is treated as above.

When compiling for the EVM, this will be translated into an appropriatePUSHiinstruction. In the following example,
3 and 2 are added resulting in 5 and then the bitwiseandwith the string “abc” is computed. The final value is assigned
to a local variable calledx.

The 32-byte limit above does not apply to string literals passed to builtin functions that require literal arguments (e.g.
setimmutableorloadimmutable). Those strings never end up in the generated bytecode.

letx := and("abc", add(3, 2))

Unless it is the default type, the type of a literal has to be specified after a colon:

// This will not compile (u32 and u256 type not implemented yet)
letx := and("abc":u32, add(3:u256, 2:u256))

**Function Calls**

Both built-in and user-defined functions (see below) can be called in the same way as shown in the previous example.
If the function returns a single value, it can be directly used inside an expression again. If it returns multiple values,
they have to be assigned to local variables.

functionf(x, y) -> a, b {/* ... */ }
mstore(0x80, add(mload(0x80), 3))
// Here, the user-defined function`f`returns two values.
letx, y := f(1, mload(0))

For built-in functions of the EVM, functional expressions can be directly translated to a stream of opcodes: You just
read the expression from right to left to obtain the opcodes. In the case of the second line in the example, this isPUSH1
3 PUSH1 0x80 MLOAD ADD PUSH1 0x80 MSTORE.

For calls to user-defined functions, the arguments are also put on the stack from right to left and this is the order in
which argument lists are evaluated. The return values, though, are expected on the stack from left to right, i.e. in this
example,yis on top of the stack andxis below it.

**Variable Declarations**

You can use theletkeyword to declare variables. A variable is only visible inside the{...}-block it was defined in.
When compiling to the EVM, a new stack slot is created that is reserved for the variable and automatically removed
again when the end of the block is reached. You can provide an initial value for the variable. If you do not provide a
value, the variable will be initialized to zero.

Since variables are stored on the stack, they do not directly influence memory or storage, but they can be used as
pointers to memory or storage locations in the built-in functionsmstore,mload,sstoreandsload. Future dialects
might introduce specific types for such pointers.

When a variable is referenced, its current value is copied. For the EVM, this translates to aDUPinstruction.

**334 Chapter 3. Contents**


#### {

letzero := 0
letv := calldataload(zero)
{
lety := add(sload(v), 1)
v := y
}// y is "deallocated" here
sstore(v, zero)
}// v and zero are "deallocated" here

If the declared variable should have a type different from the default type, you denote that following a colon. You can
also declare multiple variables in one statement when you assign from a function call that returns multiple values.

// This will not compile (u32 and u256 type not implemented yet)
{
letzero:u32 := 0:u32
letv:u256, t:u32 := f()
letx, y := g()
}

Depending on the optimiser settings, the compiler can free the stack slots already after the variable has been used for
the last time, even though it is still in scope.

**Assignments**

Variables can be assigned to after their definition using the:=operator. It is possible to assign multiple variables at
the same time. For this, the number and types of the values have to match. If you want to assign the values returned
from a function that has multiple return parameters, you have to provide multiple variables. The same variable may
not occur multiple times on the left-hand side of an assignment, e.g.x, x := f()is invalid.

letv := 0
// re-assign v
v := 2
lett := add(v, 2)
functionf() -> a, b { }
// assign multiple values
v, t := f()

**If**

The if statement can be used for conditionally executing code. No “else” block can be defined. Consider using “switch”
instead (see below) if you need multiple alternatives.

if lt(calldatasize(), 4) { revert(0, 0) }

The curly braces for the body are required.

**3.32. Yul 335**


**Switch**

You can use a switch statement as an extended version of the if statement. It takes the value of an expression and
compares it to several literal constants. The branch corresponding to the matching constant is taken. Contrary to other
programming languages, for safety reasons, control flow does not continue from one case to the next. There can be a
fallback or default case calleddefaultwhich is taken if none of the literal constants matches.

{
letx := 0
switch calldataload(4)
case0 {
x := calldataload(0x24)
}
default{
x := calldataload(0x44)
}
sstore(0, div(x, 2))
}

The list of cases is not enclosed by curly braces, but the body of a case does require them.

**Loops**

Yul supports for-loops which consist of a header containing an initializing part, a condition, a post-iteration part and
a body. The condition has to be an expression, while the other three are blocks. If the initializing part declares any
variables at the top level, the scope of these variables extends to all other parts of the loop.

Thebreakandcontinuestatements can be used in the body to exit the loop or skip to the post-part, respectively.

The following example computes the sum of an area in memory.

{
letx := 0
for{leti := 0 } lt(i, 0x100) { i := add(i, 0x20) } {
x := add(x, mload(i))
}
}

For loops can also be used as a replacement for while loops: Simply leave the initialization and post-iteration parts
empty.

{
letx := 0
leti := 0
for{ } lt(i, 0x100) { } { // while(i < 0x100)
x := add(x, mload(i))
i := add(i, 0x20)
}
}

**336 Chapter 3. Contents**


**Function Declarations**

Yul allows the definition of functions. These should not be confused with functions in Solidity since they are never
part of an external interface of a contract and are part of a namespace separate from the one for Solidity functions.

For the EVM, Yul functions take their arguments (and a return PC) from the stack and also put the results onto the
stack. User-defined functions and built-in functions are called in exactly the same way.

Functions can be defined anywhere and are visible in the block they are declared in. Inside a function, you cannot
access local variables defined outside of that function.

Functions declare parameters and return variables, similar to Solidity. To return a value, you assign it to the return
variable(s).

If you call a function that returns multiple values, you have to assign them to multiple variables usinga, b := f(x)
orlet a, b := f(x).

Theleavestatement can be used to exit the current function. It works like thereturnstatement in other languages
just that it does not take a value to return, it just exits the functions and the function will return whatever values are
currently assigned to the return variable(s).

Note that the EVM dialect has a built-in function calledreturnthat quits the full execution context (internal message
call) and not just the current yul function.

The following example implements the power function by square-and-multiply.

{
functionpower(base, exponent) -> result {
switchexponent
case0 { result := 1 }
case1 { result := base }
default{
result := power(mul(base, base), div(exponent, 2))
switchmod(exponent, 2)
case1 { result := mul(base, result) }
}
}
}

**3.32.5 Specification of Yul**

This chapter describes Yul code formally. Yul code is usually placed inside Yul objects, which are explained in their
own chapter.

Block ='{' Statement*'}'
Statement =
Block |
FunctionDefinition |
VariableDeclaration |
Assignment |
If |
Expression |
Switch |
ForLoop |
BreakContinue |
Leave
(continues on next page)

**3.32. Yul 337**


```
(continued from previous page)
```
FunctionDefinition =
'function'Identifier '(' TypedIdentifierList?')'
('->' TypedIdentifierList )? Block
VariableDeclaration =
'let'TypedIdentifierList (':=' Expression )?
Assignment =
IdentifierList':=' Expression
Expression =
FunctionCall | Identifier | Literal
If =
'if'Expression Block
Switch =
'switch'Expression ( Case+ Default? | Default )
Case =
'case' Literal Block
Default =
'default'Block
ForLoop =
'for'Block Expression Block Block
BreakContinue =
'break' |'continue'
Leave ='leave'
FunctionCall =
Identifier'('( Expression ( ',' Expression )* )?')'
Identifier = [a-zA-Z_$] [a-zA-Z_$0-9.]*
IdentifierList = Identifier (',' Identifier)*
TypeName = Identifier
TypedIdentifierList = Identifier (':'TypeName )? (','Identifier (':'TypeName )? )*
Literal =
(NumberLiteral | StringLiteral | TrueLiteral | FalseLiteral) (':'TypeName )?
NumberLiteral = HexNumber | DecimalNumber
StringLiteral = '"' ([^"\r\n\\] |'\\'.)*'"'
TrueLiteral ='true'
FalseLiteral ='false'
HexNumber ='0x' [0-9a-fA-F]+
DecimalNumber = [0-9]+

**Restrictions on the Grammar**

Apart from those directly imposed by the grammar, the following restrictions apply:

Switches must have at least one case (including the default case). All case values need to have the same type and distinct
values. If all possible values of the expression type are covered, a default case is not allowed (i.e. a switch with abool
expression that has both a true and a false case do not allow a default case).

Every expression evaluates to zero or more values. Identifiers and Literals evaluate to exactly one value and function
calls evaluate to a number of values equal to the number of return variables of the function called.

In variable declarations and assignments, the right-hand-side expression (if present) has to evaluate to a number of
values equal to the number of variables on the left-hand-side. This is the only situation where an expression evaluating
to more than one value is allowed. The same variable name cannot occur more than once in the left-hand-side of an
assignment or variable declaration.

**338 Chapter 3. Contents**


Expressions that are also statements (i.e. at the block level) have to evaluate to zero values.

In all other situations, expressions have to evaluate to exactly one value.

Acontinueorbreakstatement can only be used inside the body of a for-loop, as follows. Consider the innermost
loop that contains the statement. The loop and the statement must be in the same function, or both must be at the top
level. The statement must be in the loop’s body block; it cannot be in the loop’s initialization block or update block.
It is worth emphasizing that this restriction applies just to the innermost loop that contains thecontinueorbreak
statement: this innermost loop, and therefore thecontinueorbreakstatement, may appear anywhere in an outer
loop, possibly in an outer loop’s initialization block or update block. For example, the following is legal, because the
breakoccurs in the body block of the inner loop, despite also occurring in the update block of the outer loop:

for{} true {for{} true {} { break } }
{
}

The condition part of the for-loop has to evaluate to exactly one value.

Theleavestatement can only be used inside a function.

Functions cannot be defined anywhere inside for loop init blocks.

Literals cannot be larger than their type. The largest type defined is 256-bit wide.

During assignments and function calls, the types of the respective values have to match. There is no implicit type
conversion. Type conversion in general can only be achieved if the dialect provides an appropriate built-in function
that takes a value of one type and returns a value of a different type.

**Scoping Rules**

Scopes in Yul are tied to Blocks (exceptions are functions and the for loop as explained below) and all declarations
(FunctionDefinition,VariableDeclaration) introduce new identifiers into these scopes.

Identifiers are visible in the block they are defined in (including all sub-nodes and sub-blocks): Functions are visible
in the whole block (even before their definitions) while variables are only visible starting from the statement after the
VariableDeclaration.

In particular, variables cannot be referenced in the right hand side of their own variable declaration. Functions can be
referenced already before their declaration (if they are visible).

As an exception to the general scoping rule, the scope of the “init” part of the for-loop (the first block) extends across
all other parts of the for loop. This means that variables (and functions) declared in the init part (but not inside a block
inside the init part) are visible in all other parts of the for-loop.

Identifiers declared in the other parts of the for loop respect the regular syntactical scoping rules.

This means a for-loop of the formfor { I... } C { P... } { B... }is equivalent to{ I... for {} C {
P... } { B... } }.

The parameters and return parameters of functions are visible in the function body and their names have to be distinct.

Inside functions, it is not possible to reference a variable that was declared outside of that function.

Shadowing is disallowed, i.e. you cannot declare an identifier at a point where another identifier with the same name
is also visible, even if it is not possible to reference it because it was declared outside the current function.

**3.32. Yul 339**


**Formal Specification**

We formally specify Yul by providing an evaluation function E overloaded on the various nodes of the AST. As builtin
functions can have side effects, E takes two state objects and the AST node and returns two new state objects and a
variable number of other values. The two state objects are the global state object (which in the context of the EVM is
the memory, storage and state of the blockchain) and the local state object (the state of local variables, i.e. a segment
of the stack in the EVM).

If the AST node is a statement, E returns the two state objects and a “mode”, which is used for thebreak,continue
andleavestatements. If the AST node is an expression, E returns the two state objects and as many values as the
expression evaluates to.

The exact nature of the global state is unspecified for this high level description. The local stateLis a mapping of
identifiersito valuesv, denoted asL[i] = v.

For an identifierv, let$vbe the name of the identifier.

We will use a destructuring notation for the AST nodes.

E(G, L, <{St1, ..., Stn}>: Block) =
let G1, L1, mode = E(G, L, St1, ..., Stn)
let L2 be a restriction of L1 to the identifiers of L
G1, L2, mode
E(G, L, St1, ..., Stn: Statement) =
if n is zero:
G, L, regular
else:
let G1, L1, mode = E(G, L, St1)
if mode is regular then
E(G1, L1, St2, ..., Stn)
otherwise
G1, L1, mode
E(G, L, FunctionDefinition) =
G, L, regular
E(G, L, <let var_1, ..., var_n := rhs>: VariableDeclaration) =
E(G, L, <var_1, ..., var_n := rhs>: Assignment)
E(G, L, <let var_1, ..., var_n>: VariableDeclaration) =
let L1 be a copy of L where L1[$var_i] = 0 for i = 1, ..., n
G, L1, regular
E(G, L, <var_1, ..., var_n := rhs>: Assignment) =
let G1, L1, v1, ..., vn = E(G, L, rhs)
let L2 be a copy of L1 where L2[$var_i] = vi for i = 1, ..., n
G1, L2, regular
E(G, L, <for { i1, ..., in } condition post body>: ForLoop) =
if n >= 1:
let G1, L1, mode = E(G, L, i1, ..., in)
// mode has to be regular or leave due to the syntactic restrictions
if mode is leave then
G1, L1 restricted to variables of L, leave
otherwise
let G2, L2, mode = E(G1, L1, for {} condition post body)
G2, L2 restricted to variables of L, mode
else:
let G1, L1, v = E(G, L, condition)
if v is false:
(continues on next page)

**340 Chapter 3. Contents**


(continued from previous page)
G1, L1, regular
else:
let G2, L2, mode = E(G1, L, body)
if mode is break:
G2, L2, regular
otherwise if mode is leave:
G2, L2, leave
else:
G3, L3, mode = E(G2, L2, post)
if mode is leave:
G3, L3, leave
otherwise
E(G3, L3, for {} condition post body)
E(G, L, break: BreakContinue) =
G, L, break
E(G, L, continue: BreakContinue) =
G, L, continue
E(G, L, leave: Leave) =
G, L, leave
E(G, L, <if condition body>: If) =
let G0, L0, v = E(G, L, condition)
if v is true:
E(G0, L0, body)
else:
G0, L0, regular
E(G, L, <switch condition case l1:t1 st1 ... case ln:tn stn>: Switch) =
E(G, L, switch condition case l1:t1 st1 ... case ln:tn stn default {})
E(G, L, <switch condition case l1:t1 st1 ... case ln:tn stn default st'>: Switch) =
let G0, L0, v = E(G, L, condition)
// i = 1 .. n
// Evaluate literals, context doesn't matter
let _, _, v1 = E(G0, L0, l1)
...
let _, _, vn = E(G0, L0, ln)
if there exists smallest i such that vi = v:
E(G0, L0, sti)
else:
E(G0, L0, st')

E(G, L, <name>: Identifier) =
G, L, L[$name]
E(G, L, <fname(arg1, ..., argn)>: FunctionCall) =
G1, L1, vn = E(G, L, argn)
...
G(n-1), L(n-1), v2 = E(G(n-2), L(n-2), arg2)
Gn, Ln, v1 = E(G(n-1), L(n-1), arg1)
Let <function fname (param1, ..., paramn) -> ret1, ..., retm block>
be the function of name $fname visible at the point of the call.
Let L' be a new local state such that
L'[$parami] = vi and L'[$reti] = 0 for all i.
Let G'', L'', mode = E(Gn, L', block)
G'', Ln, L''[$ret1], ..., L''[$retm]
(continues on next page)

**3.32. Yul 341**


```
(continued from previous page)
```
E(G, L, l: StringLiteral) = G, L, str(l),
where str is the string evaluation function,
which for the EVM dialect is defined in the section'Literals'above
E(G, L, n: HexNumber) = G, L, hex(n)
where hex is the hexadecimal evaluation function,
which turns a sequence of hexadecimal digits into their big endian value
E(G, L, n: DecimalNumber) = G, L, dec(n),
where dec is the decimal evaluation function,
which turns a sequence of decimal digits into their big endian value

**EVM Dialect**

The default dialect of Yul currently is the EVM dialect for the currently selected version of the EVM. The only type
available in this dialect isu256, the 256-bit native type of the Ethereum Virtual Machine. Since it is the default type
of this dialect, it can be omitted.

The following table lists all builtin functions (depending on the EVM version) and provides a short description of the
semantics of the function / opcode. This document does not want to be a full description of the Ethereum virtual
machine. Please refer to a different document if you are interested in the precise semantics.

Opcodes marked with-do not return a result and all others return exactly one value. Opcodes marked withF,H,B,
C,I,L,PandNare present since Frontier, Homestead, Byzantium, Constantinople, Istanbul, London, Paris or Cancun
respectively.

In the following,mem[a...b)signifies the bytes of memory starting at positionaup to but not including position
b,storage[p]signifies the storage contents at slotp, and similarly,transientStorage[p]signifies the transient
storage contents at slotp.

Since Yul manages local variables and control-flow, opcodes that interfere with these features are not available. This
includes thedupandswapinstructions as well asjumpinstructions, labels and thepushinstructions.

```
Instruction Explanation
stop() - F stop execution, identical to return(0, 0)
add(x, y) F x + y
sub(x, y) F x - y
mul(x, y) F x * y
div(x, y) F x / y or 0 if y == 0
sdiv(x, y) F x / y, for signed numbers in two’s complement, 0 if y == 0
mod(x, y) F x % y, 0 if y == 0
smod(x, y) F x % y, for signed numbers in two’s complement, 0 if y == 0
exp(x, y) F x to the power of y
not(x) F bitwise “not” of x (every bit of x is negated)
lt(x, y) F 1 if x < y, 0 otherwise
gt(x, y) F 1 if x > y, 0 otherwise
slt(x, y) F 1 if x < y, 0 otherwise, for signed numbers in two’s complement
sgt(x, y) F 1 if x > y, 0 otherwise, for signed numbers in two’s complement
eq(x, y) F 1 if x == y, 0 otherwise
iszero(x) F 1 if x == 0, 0 otherwise
and(x, y) F bitwise “and” of x and y
or(x, y) F bitwise “or” of x and y
xor(x, y) F bitwise “xor” of x and y
continues on next page
```
**342 Chapter 3. Contents**


```
Table 2 – continued from previous page
Instruction Explanation
byte(n, x) F nth byte of x, where the most significant byte is the 0th byte
shl(x, y) C logical shift left y by x bits
shr(x, y) C logical shift right y by x bits
sar(x, y) C signed arithmetic shift right y by x bits
addmod(x, y, m) F (x + y) % m with arbitrary precision arithmetic, 0 if m == 0
mulmod(x, y, m) F (x * y) % m with arbitrary precision arithmetic, 0 if m == 0
signextend(i, x) F sign extend from (i*8+7)th bit counting from least significant
keccak256(p, n) F keccak(mem[p...(p+n)))
pop(x) - F discard value x
mload(p) F mem[p...(p+32))
mstore(p, v) - F mem[p...(p+32)) := v
mstore8(p, v) - F mem[p] := v & 0xff (only modifies a single byte)
sload(p) F storage[p]
sstore(p, v) - F storage[p] := v
tload(p) N transientStorage[p]
tstore(p, v) - N transientStorage[p] := v
msize() F size of memory, i.e. largest accessed memory index
gas() F gas still available to execution
address() F address of the current contract / execution context
balance(a) F wei balance at address a
selfbalance() I equivalent to balance(address()), but cheaper
caller() F call sender (excludingdelegatecall)
callvalue() F wei sent together with the current call
calldataload(p) F call data starting from position p (32 bytes)
calldatasize() F size of call data in bytes
calldatacopy(t, f, s) - F copy s bytes from calldata at position f to mem at position t
codesize() F size of the code of the current contract / execution context
codecopy(t, f, s) - F copy s bytes from code at position f to mem at position t
extcodesize(a) F size of the code at address a
extcodecopy(a, t, f, s) - F like codecopy(t, f, s) but take code at address a
returndatasize() B size of the last returndata
returndatacopy(t, f, s) - B copy s bytes from returndata at position f to mem at position t
mcopy(t, f, s) - N copy s bytes from mem at position f to mem at position t
extcodehash(a) C code hash of address a
create(v, p, n) F create new contract with code mem[p...(p+n)) and send v wei and return the new address; returns 0 on error
create2(v, p, n, s) C create new contract with code mem[p...(p+n)) at address keccak256(0xff. this. s. keccak256(mem[p...(p+n))) and send v wei and return the new address, where0xffis a 1 byte value,thisis the current contract’s address as a 20 byte value andsis a big-endian 256-bit value; returns 0 on error
call(g, a, v, in, insize, out, outsize) F call contract at address a with input mem[in...(in+insize)) providing g gas and v wei and output area mem[out...(out+outsize)) returning 0 on error (eg. out of gas) and 1 on success See more
callcode(g, a, v, in, insize, out, outsize) F identical tocallbut only use the code from a and stay in the context of the current contract otherwise See more
delegatecall(g, a, in, insize, out, outsize) H identical tocallcodebut also keepcallerandcallvalue See more
staticcall(g, a, in, insize, out, outsize) B identical tocall(g, a, 0, in, insize, out, outsize)but do not allow state modifications See more
return(p, s) - F end execution, return data mem[p...(p+s))
revert(p, s) - B end execution, revert state changes, return data mem[p...(p+s))
selfdestruct(a) - F end execution, destroy current contract and send funds to a (deprecated)
invalid() - F end execution with invalid instruction
log0(p, s) - F log data mem[p...(p+s))
log1(p, s, t1) - F log data mem[p...(p+s)) with topic t1
log2(p, s, t1, t2) - F log data mem[p...(p+s)) with topics t1, t2
log3(p, s, t1, t2, t3) - F log data mem[p...(p+s)) with topics t1, t2, t3
log4(p, s, t1, t2, t3, t4) - F log data mem[p...(p+s)) with topics t1, t2, t3, t4
continues on next page
```
**3.32. Yul 343**


```
Table 2 – continued from previous page
Instruction Explanation
chainid() I ID of the executing chain (EIP-1344)
basefee() L current block’s base fee (EIP-3198 and EIP-1559)
blobbasefee() N current block’s blob base fee (EIP-7516 and EIP-4844)
origin() F transaction sender
gasprice() F gas price of the transaction
blockhash(b) F hash of block nr b - only for last 256 blocks excluding current
blobhash(i) N versioned hash of transaction’s i-th blob, 0 if blob does not exist
coinbase() F current mining beneficiary
timestamp() F timestamp of the current block in seconds since the epoch
number() F current block number
difficulty() F difficulty of the current block (see note below)
prevrandao() P randomness provided by the beacon chain (see note below)
gaslimit() F block gas limit of the current block
```
**Note:** Thecall*instructions use theoutandoutsizeparameters to define an area in memory where the return or
failure data is placed. This area is written to depending on how many bytes the called contract returns. If it returns
more data, only the firstoutsizebytes are written. You can access the rest of the data using thereturndatacopy
opcode. If it returns less data, then the remaining bytes are not touched at all. You need to use thereturndatasize
opcode to check which part of this memory area contains the return data. The remaining bytes will retain their values
as of before the call.

**Note:** Thedifficulty()instruction is disallowed in EVM version >= Paris. With the Paris network upgrade the
semantics of the instruction that was previously calleddifficultyhave been changed and the instruction was renamed
toprevrandao. It can now return arbitrary values in the full 256-bit range, whereas the highest recorded difficulty
value within Ethash was ~54 bits. This change is described in EIP-4399. Please note that irrelevant to which EVM
version is selected in the compiler, the semantics of instructions depend on the final chain of deployment.

```
Warning: From version 0.8.18 and up, the use ofselfdestructin both Solidity and Yul will trigger a deprecation
warning, since theSELFDESTRUCTopcode will eventually undergo breaking changes in behavior as stated in EIP-
6049.
```
In some internal dialects, there are additional functions:

**344 Chapter 3. Contents**


**datasize, dataoffset, datacopy**

The functionsdatasize(x),dataoffset(x)anddatacopy(t, f, l)are used to access other parts of a Yul object.

datasizeanddataoffsetcan only take string literals (the names of other objects) as arguments and return the size
and offset in the data area, respectively. For the EVM, thedatacopyfunction is equivalent tocodecopy.

**setimmutable, loadimmutable**

The functionssetimmutable(offset, "name", value)andloadimmutable("name")are used for the im-
mutable mechanism in Solidity and do not nicely map to pure Yul. The call tosetimmutable(offset, "name",
value)assumes that the runtime code of the contract containing the given named immutable was copied to memory
at offsetoffsetand will writevalueto all positions in memory (relative tooffset) that contain the placeholder that
was generated for calls toloadimmutable("name")in the runtime code.

**linkersymbol**

The functionlinkersymbol("library_id")is a placeholder for an address literal to be substituted by the linker.
Its first and only argument must be a string literal and uniquely represents the address to be inserted. Identifiers can
be arbitrary but when the compiler produces Yul code from Solidity sources, it uses a library name qualified with the
name of the source unit that defines that library. To link the code with a particular library address, the same identifier
must be provided to the--librariesoption on the command-line.

For example this code

leta := linkersymbol("file.sol:Math")

is equivalent to

leta := 0x1234567890123456789012345678901234567890

when the linker is invoked with--libraries "file.sol:Math=0x1234567890123456789012345678901234567890
option.

See _Using the Commandline Compiler_ for details about the Solidity linker.

**memoryguard**

This function is available in the EVM dialect with objects. The caller oflet ptr := memoryguard(size)(where
sizehas to be a literal number) promises that they only use memory in either the range[0, size)or the unbounded
range starting atptr.

Since the presence of amemoryguardcall indicates that all memory access adheres to this restriction, it allows the
optimizer to perform additional optimization steps, for example the stack limit evader, which attempts to move stack
variables that would otherwise be unreachable to memory.

The Yul optimizer promises to only use the memory range[size, ptr)for its purposes. If the optimizer does not
need to reserve any memory, it holds thatptr == size.

memoryguardcan be called multiple times, but needs to have the same literal as argument within one Yul subobject.
If at least onememoryguardcall is found in a subobject, the additional optimiser steps will be run on it.

**3.32. Yul 345**


**verbatim**

The set ofverbatim...builtin functions lets you create bytecode for opcodes that are not known to the Yul compiler.
It also allows you to create bytecode sequences that will not be modified by the optimizer.

The functions areverbatim_<n>i_<m>o("<data>", ...), where

- nis a decimal between 0 and 99 that specifies the number of input stack slots / variables
- mis a decimal between 0 and 99 that specifies the number of output stack slots / variables
- datais a string literal that contains the sequence of bytes

If you for example want to define a function that multiplies the input by two, without the optimizer touching the constant
two, you can use

letx := calldataload(0)
letdouble := verbatim_1i_1o(hex"600202", x)

This code will result in adup1opcode to retrievex(the optimizer might directly re-use result of thecalldataload
opcode, though) directly followed by 600202. The code is assumed to consume the copied value ofxand produce the
result on the top of the stack. The compiler then generates code to allocate a stack slot fordoubleand store the result
there.

As with all opcodes, the arguments are arranged on the stack with the leftmost argument on the top, while the return
values are assumed to be laid out such that the rightmost variable is at the top of the stack.

Sinceverbatimcan be used to generate arbitrary opcodes or even opcodes unknown to the Solidity compiler, care
has to be taken when usingverbatimtogether with the optimizer. Even when the optimizer is switched off, the code
generator has to determine the stack layout, which means that e.g. usingverbatimto modify the stack height can lead
to undefined behavior.

The following is a non-exhaustive list of restrictions on verbatim bytecode that are not checked by the compiler. Vio-
lations of these restrictions can result in undefined behavior.

- Control-flow should not jump into or out of verbatim blocks, but it can jump within the same verbatim block.
- Stack contents apart from the input and output parameters should not be accessed.
- The stack height difference should be exactlym - n(output slots minus input slots).
- Verbatim bytecode cannot make any assumptions about the surrounding bytecode. All required parameters have
    to be passed in as stack variables.

The optimizer does not analyze verbatim bytecode and always assumes that it modifies all aspects of state and thus can
only do very few optimizations acrossverbatimfunction calls.

The optimizer treats verbatim bytecode as an opaque block of code. It will not split it but might move, duplicate or
combine it with identical verbatim bytecode blocks. If a verbatim bytecode block is unreachable by the control-flow, it
can be removed.

```
Warning: During discussions about whether or not EVM improvements might break existing smart contracts,
features insideverbatimcannot receive the same consideration as those used by the Solidity compiler itself.
```
**Note:** To avoid confusion, all identifiers starting with the stringverbatimare reserved and cannot be used for user-
defined identifiers.

**346 Chapter 3. Contents**


**3.32.6 Specification of Yul Object**

Yul objects are used to group named code and data sections. The functionsdatasize,dataoffsetanddatacopy
can be used to access these sections from within code. Hex strings can be used to specify data in hex encoding, regular
strings in native encoding. For code,datacopywill access its assembled binary representation.

Object ='object'StringLiteral'{'Code ( Object | Data )* '}'
Code = 'code'Block
Data = 'data'StringLiteral ( HexLiteral | StringLiteral )
HexLiteral ='hex'('"' ([0-9a-fA-F]{2})*'"' |'\''([0-9a-fA-F]{2})*'\'')
StringLiteral = '"' ([^"\r\n\\] |'\\'.)*'"'

Above,Blockrefers toBlockin the Yul code grammar explained in the previous chapter.

**Note:** An object with a name that ends in_deployedis treated as deployed code by the Yul optimizer. The only
consequence of this is a different gas cost heuristic in the optimizer.

**Note:** Data objects or sub-objects whose names contain a.can be defined but it is not possible to access them through
datasize,dataoffsetordatacopybecause.is used as a separator to access objects inside another object.

**Note:** The data object called".metadata"has a special meaning: It cannot be accessed from code and is always
appended to the very end of the bytecode, regardless of its position in the object.

Other data objects with special significance might be added in the future, but their names will always start with a..

An example Yul Object is shown below:

// A contract consists of a single object with sub-objects representing
// the code to be deployed or other contracts it can create.
// The single "code" node is the executable code of the object.
// Every (other) named object or data section is serialized and
// made accessible to the special built-in functions datacopy / dataoffset /␣
˓→datasize
// The current object, sub-objects and data items inside the current object
// are in scope.
object "Contract1" {
// This is the constructor code of the contract.
code{
functionallocate(size) -> ptr {
ptr := mload(0x40)
// Note that Solidity generated IR code reserves memory offset``0x60``␣
˓→as well, but a pure Yul object is free to use memory as it chooses.
if iszero(ptr) { ptr := 0x60 }
mstore(0x40, add(ptr, size))
}

```
// first create "Contract2"
letsize :=datasize("Contract2")
letoffset := allocate(size)
// This will turn into codecopy for EVM
(continues on next page)
```
**3.32. Yul 347**


```
(continued from previous page)
datacopy(offset,dataoffset("Contract2"), size)
// constructor parameter is a single number 0x1234
mstore(add(offset, size), 0x1234)
pop(create(0, offset, add(size, 32)))
```
```
// now return the runtime object (the currently
// executing code is the constructor code)
size :=datasize("Contract1_deployed")
offset := allocate(size)
// This will turn into a codecopy for EVM
datacopy(offset,dataoffset("Contract1_deployed"), size)
return(offset, size)
}
```
```
data"Table2" hex"4123"
```
```
object "Contract1_deployed" {
code{
functionallocate(size) -> ptr {
ptr := mload(0x40)
// Note that Solidity generated IR code reserves memory offset␣
˓→``0x60``as well, but a pure Yul object is free to use memory as it chooses.
if iszero(ptr) { ptr := 0x60 }
mstore(0x40, add(ptr, size))
}
```
```
// runtime code
```
```
mstore(0, "Hello, World!")
return(0, 0x20)
}
}
```
```
// Embedded object. Use case is that the outside is a factory contract,
// and Contract2 is the code to be created by the factory
object "Contract2" {
code{
// code here ...
}
```
```
object"Contract2_deployed" {
code{
// code here ...
}
}
```
data"Table1" hex"4123"
}
}

**348 Chapter 3. Contents**


**3.32.7 Yul Optimizer**

The Yul optimizer operates on Yul code and uses the same language for input, output and intermediate states. This
allows for easy debugging and verification of the optimizer.

Please refer to the general _optimizer documentation_ for more details about the different optimization stages and how to
use the optimizer.

If you want to use Solidity in stand-alone Yul mode, you activate the optimizer using--optimizeand optionally
specify the _expected number of contract executions_ with--optimize-runs:

solc --strict-assembly --optimize --optimize-runs 200

In Solidity mode, the Yul optimizer is activated together with the regular optimizer.

**Optimization Step Sequence**

Detailed information regarding the optimization sequence as well as a list of abbreviations is available in the _optimizer
docs_.

**3.32.8 Complete ERC20 Example**

object "Token" {
code{
// Store the creator in slot zero.
sstore(0, caller())

```
// Deploy the contract
datacopy(0,dataoffset("runtime"),datasize("runtime"))
return(0,datasize("runtime"))
}
object "runtime" {
code{
// Protection against sending Ether
require(iszero(callvalue()))
```
```
// Dispatcher
switchselector()
case0x70a08231/* "balanceOf(address)" */ {
returnUint(balanceOf(decodeAsAddress(0)))
}
case0x18160ddd/* "totalSupply()" */ {
returnUint(totalSupply())
}
case0xa9059cbb/* "transfer(address,uint256)" */ {
transfer(decodeAsAddress(0), decodeAsUint(1))
returnTrue()
}
case0x23b872dd/* "transferFrom(address,address,uint256)" */ {
transferFrom(decodeAsAddress(0), decodeAsAddress(1), decodeAsUint(2))
returnTrue()
}
(continues on next page)
```
**3.32. Yul 349**


```
(continued from previous page)
case0x095ea7b3/* "approve(address,uint256)" */ {
approve(decodeAsAddress(0), decodeAsUint(1))
returnTrue()
}
case0xdd62ed3e/* "allowance(address,address)" */ {
returnUint(allowance(decodeAsAddress(0), decodeAsAddress(1)))
}
case0x40c10f19/* "mint(address,uint256)" */ {
mint(decodeAsAddress(0), decodeAsUint(1))
returnTrue()
}
default{
revert(0, 0)
}
```
```
functionmint(account, amount) {
require(calledByOwner())
```
```
mintTokens(amount)
addToBalance(account, amount)
emitTransfer(0, account, amount)
}
functiontransfer(to, amount) {
executeTransfer(caller(), to, amount)
}
functionapprove(spender, amount) {
revertIfZeroAddress(spender)
setAllowance(caller(), spender, amount)
emitApproval(caller(), spender, amount)
}
functiontransferFrom(from, to, amount) {
decreaseAllowanceBy(from, caller(), amount)
executeTransfer(from, to, amount)
}
```
```
functionexecuteTransfer(from, to, amount) {
revertIfZeroAddress(to)
deductFromBalance(from, amount)
addToBalance(to, amount)
emitTransfer(from, to, amount)
}
```
```
/* ---------- calldata decoding functions ----------- */
functionselector() -> s {
s := div(calldataload(0),␣
˓→0x100000000000000000000000000000000000000000000000000000000)
}
```
```
functiondecodeAsAddress(offset) -> v {
v := decodeAsUint(offset)
if iszero(iszero(and(v,␣
(continues on next page)
```
**350 Chapter 3. Contents**


```
(continued from previous page)
˓→not(0xffffffffffffffffffffffffffffffffffffffff)))) {
revert(0, 0)
}
}
functiondecodeAsUint(offset) -> v {
letpos := add(4, mul(offset, 0x20))
if lt(calldatasize(), add(pos, 0x20)) {
revert(0, 0)
}
v := calldataload(pos)
}
/* ---------- calldata encoding functions ---------- */
functionreturnUint(v) {
mstore(0, v)
return(0, 0x20)
}
functionreturnTrue() {
returnUint(1)
}
```
```
/* -------- events ---------- */
functionemitTransfer(from, to, amount) {
letsignatureHash :=␣
˓→0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
emitEvent(signatureHash, from, to, amount)
}
functionemitApproval(from, spender, amount) {
letsignatureHash :=␣
˓→0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925
emitEvent(signatureHash, from, spender, amount)
}
functionemitEvent(signatureHash, indexed1, indexed2, nonIndexed) {
mstore(0, nonIndexed)
log3(0, 0x20, signatureHash, indexed1, indexed2)
}
```
```
/* -------- storage layout ---------- */
functionownerPos() -> p { p := 0 }
functiontotalSupplyPos() -> p { p := 1 }
functionaccountToStorageOffset(account) -> offset {
offset := add(0x1000, account)
}
functionallowanceStorageOffset(account, spender) -> offset {
offset := accountToStorageOffset(account)
mstore(0, offset)
mstore(0x20, spender)
offset := keccak256(0, 0x40)
}
```
```
/* -------- storage access ---------- */
functionowner() -> o {
o := sload(ownerPos())
(continues on next page)
```
**3.32. Yul 351**


```
(continued from previous page)
}
functiontotalSupply() -> supply {
supply := sload(totalSupplyPos())
}
functionmintTokens(amount) {
sstore(totalSupplyPos(), safeAdd(totalSupply(), amount))
}
functionbalanceOf(account) -> bal {
bal := sload(accountToStorageOffset(account))
}
functionaddToBalance(account, amount) {
letoffset := accountToStorageOffset(account)
sstore(offset, safeAdd(sload(offset), amount))
}
functiondeductFromBalance(account, amount) {
letoffset := accountToStorageOffset(account)
letbal := sload(offset)
require(lte(amount, bal))
sstore(offset, sub(bal, amount))
}
functionallowance(account, spender) -> amount {
amount := sload(allowanceStorageOffset(account, spender))
}
functionsetAllowance(account, spender, amount) {
sstore(allowanceStorageOffset(account, spender), amount)
}
functiondecreaseAllowanceBy(account, spender, amount) {
letoffset := allowanceStorageOffset(account, spender)
letcurrentAllowance := sload(offset)
require(lte(amount, currentAllowance))
sstore(offset, sub(currentAllowance, amount))
}
```
```
/* ---------- utility functions ---------- */
functionlte(a, b) -> r {
r := iszero(gt(a, b))
}
functiongte(a, b) -> r {
r := iszero(lt(a, b))
}
functionsafeAdd(a, b) -> r {
r := add(a, b)
if or(lt(r, a), lt(r, b)) { revert(0, 0) }
}
functioncalledByOwner() -> cbo {
cbo := eq(owner(), caller())
}
functionrevertIfZeroAddress(addr) {
require(addr)
}
functionrequire(condition) {
if iszero(condition) { revert(0, 0) }
(continues on next page)
```
**352 Chapter 3. Contents**


(continued from previous page)
}
}
}
}

### 3.33 Import Path Resolution

In order to be able to support reproducible builds on all platforms, the Solidity compiler has to abstract away the details
of the filesystem where source files are stored. Paths used in imports must work the same way everywhere while the
command-line interface must be able to work with platform-specific paths to provide good user experience. This section
aims to explain in detail how Solidity reconciles these requirements.

**3.33.1 Virtual Filesystem**

The compiler maintains an internal database ( _virtual filesystem_ or _VFS_ for short) where each source unit is assigned
a unique _source unit name_ which is an opaque and unstructured identifier. When you use the _import statement_ , you
specify an _import path_ that references a source unit name.

**Import Callback**

The VFS is initially populated only with files the compiler has received as input. Additional files can be loaded during
compilation using an _import callback_ , which is different depending on the type of compiler you use (see below). If the
compiler does not find any source unit name matching the import path in the VFS, it invokes the callback, which is
responsible for obtaining the source code to be placed under that name. An import callback is free to interpret source
unit names in an arbitrary way, not just as paths. If there is no callback available when one is needed or if it fails to
locate the source code, compilation fails.

By default, the command-line compiler provides the _Host Filesystem Loader_ - a rudimentary callback that interprets a
source unit name as a path in the local filesystem. This callback can be disabled using the--no-import-callback
command-line option. The JavaScript interface does not provide any by default, but one can be provided by the user.
This mechanism can be used to obtain source code from locations other than the local filesystem (which may not even
be accessible, e.g. when the compiler is running in a browser). For example the Remix IDE provides a versatile callback
that lets you import files from HTTP, IPFS and Swarm URLs or refer directly to packages in NPM registry.

**Note:** Host Filesystem Loader’s file lookup is platform-dependent. For example backslashes in a source unit name can
be interpreted as directory separators or not and the lookup can be case-sensitive or not, depending on the underlying
platform.

For portability it is recommended to avoid using import paths that will work correctly only with a specific import
callback or only on one platform. For example you should always use forward slashes since they work as path separators
also on platforms that support backslashes.

**3.33. Import Path Resolution 353**


**Initial Content of the Virtual Filesystem**

The initial content of the VFS depends on how you invoke the compiler:

1. **solc / command-line interface**
    When you compile a file using the command-line interface of the compiler, you provide one or more paths to
    files containing Solidity code:

```
solc contract.sol /usr/local/dapp-bin/token.sol
```
```
The source unit name of a file loaded this way is constructed by converting its path to a canonical form and, if
possible, making it relative to either the base path or one of the include paths. See CLI Path Normalization and
Stripping for a detailed description of this process.
```
2. **Standard JSON**
    When using the _Standard JSON_ API (via either the JavaScript interface or the--standard-jsoncommand-line
    option) you provide input in JSON format, containing, among other things, the content of all your source files:

```
{
"language": "Solidity",
"sources": {
"contract.sol": {
"content": "import \"./util.sol\";\ncontract C {}"
},
"util.sol": {
"content": "library Util {}"
},
"/usr/local/dapp-bin/token.sol": {
"content": "contract Token {}"
}
},
"settings": {"outputSelection": {"*": {"*": ["metadata", "evm.bytecode"]}}}
}
```
```
Thesourcesdictionary becomes the initial content of the virtual filesystem and its keys are used as source unit
names.
```
3. **Standard JSON (via import callback)**
    With Standard JSON it is also possible to tell the compiler to use the import callback to obtain the source code:

```
{
"language": "Solidity",
"sources": {
"/usr/local/dapp-bin/token.sol": {
"urls": [
"/projects/mytoken.sol",
"https://example.com/projects/mytoken.sol"
]
}
},
"settings": {"outputSelection": {"*": {"*": ["metadata", "evm.bytecode"]}}}
}
```
```
If an import callback is available, the compiler will give it the strings specified inurlsone by one, until one is
loaded successfully or the end of the list is reached.
```
**354 Chapter 3. Contents**


```
The source unit names are determined the same way as when usingcontent- they are keys of thesources
dictionary and the content ofurlsdoes not affect them in any way.
```
4. **Standard input**
    On the command-line it is also possible to provide the source by sending it to compiler’s standard input:

```
echo'import "./util.sol"; contract C {}' | solc -
```
- used as one of the arguments instructs the compiler to place the content of the standard input in the virtual
filesystem under a special source unit name:<stdin>.

Once the VFS is initialized, additional files can still be added to it only through the import callback.

**3.33.2 Imports**

The import statement specifies an _import path_. Based on how the import path is specified, we can divide imports into
two categories:

- _Direct imports_ , where you specify the full source unit name directly.
- _Relative imports_ , where you specify a path starting with./or../to be combined with the source unit name of
    the importing file.

```
Listing 1: contracts/contract.sol
```
import "./math/math.sol";
import "contracts/tokens/token.sol";

In the above./math/math.solandcontracts/tokens/token.solare import paths while the source unit names
they translate to arecontracts/math/math.solandcontracts/tokens/token.solrespectively.

**Direct Imports**

An import that does not start with./or../is a _direct import_.

import "/project/lib/util.sol"; // source unit name: /project/lib/util.sol
import "lib/util.sol"; // source unit name: lib/util.sol
import "@openzeppelin/address.sol"; // source unit name: @openzeppelin/address.sol
import "https://example.com/token.sol";// source unit name: https://example.com/token.
˓→sol

After applying any _import remappings_ the import path simply becomes the source unit name.

**Note:** A source unit name is just an identifier and even if its value happens to look like a path, it is not subject to the
normalization rules you would typically expect in a shell. Any/./or/../segments or sequences of multiple slashes
remain a part of it. When the source is provided via Standard JSON interface it is entirely possible to associate different
content with source unit names that would refer to the same file on disk.

When the source is not available in the virtual filesystem, the compiler passes the source unit name to the import
callback. The Host Filesystem Loader will attempt to use it as a path and look up the file on disk. At this point the
platform-specific normalization rules kick in and names that were considered different in the VFS may actually result
in the same file being loaded. For example/project/lib/math.soland/project/lib/../lib///math.solare
considered completely different in the VFS even though they refer to the same file on disk.

**3.33. Import Path Resolution 355**


**Note:** Even if an import callback ends up loading source code for two different source unit names from the same file
on disk, the compiler will still see them as separate source units. It is the source unit name that matters, not the physical
location of the code.

**Relative Imports**

An import starting with./or../is a _relative import_. Such imports specify a path relative to the source unit name of
the importing source unit:

```
Listing 2: /project/lib/math.sol
```
import "./util.sol" as util; // source unit name: /project/lib/util.sol
import "../token.sol" as token;// source unit name: /project/token.sol

```
Listing 3: lib/math.sol
```
import "./util.sol" as util; // source unit name: lib/util.sol
import "../token.sol" as token;// source unit name: token.sol

**Note:** Relative imports **always** start with./or../soimport "util.sol", unlikeimport "./util.sol", is a
direct import. While both paths would be considered relative in the host filesystem,util.solis actually absolute in
the VFS.

Let us define a _path segment_ as any non-empty part of the path that does not contain a separator and is bounded by two
path separators. A separator is a forward slash or the beginning/end of the string. For example in./abc/..//there
are three path segments:.,abcand...

The compiler resolves the import into a source unit name based on the import path, in the following way:

1. We start with the source unit name of the importing source unit.
2. The last path segment with preceding slashes is removed from the resolved name.
3. Then, for every segment in the import path, starting from the leftmost one:
    - If the segment is., it is skipped.
    - If the segment is.., the last path segment with preceding slashes is removed from the resolved name.
    - Otherwise, the segment (preceded by a single slash if the resolved name is not empty), is appended to the
       resolved name.

The removal of the last path segment with preceding slashes is understood to work as follows:

1. Everything past the last slash is removed (i.e.a/b//c.solbecomesa/b//).
2. All trailing slashes are removed (i.e.a/b//becomesa/b).

Note that the process normalizes the part of the resolved source unit name that comes from the import path according
to the usual rules for UNIX paths, i.e. all.and..are removed and multiple slashes are squashed into a single one. On
the other hand, the part that comes from the source unit name of the importing module remains unnormalized. This
ensures that theprotocol://part does not turn intoprotocol:/if the importing file is identified with a URL.

If your import paths are already normalized, you can expect the above algorithm to produce very intuitive results. Here
are some examples of what you can expect if they are not:

**356 Chapter 3. Contents**


```
Listing 4: lib/src/../contract.sol
```
import "./util/./util.sol"; // source unit name: lib/src/../util/util.sol
import "./util//util.sol"; // source unit name: lib/src/../util/util.sol
import "../util/../array/util.sol";// source unit name: lib/src/array/util.sol
import "../.././../util.sol"; // source unit name: util.sol
import "../../.././../util.sol"; // source unit name: util.sol

**Note:** The use of relative imports containing leading..segments is not recommended. The same effect can be
achieved in a more reliable way by using direct imports with _base path and include paths_.

**3.33.3 Base Path and Include Paths**

The base path and include paths represent directories that the Host Filesystem Loader will load files from. When a
source unit name is passed to the loader, it prepends the base path to it and performs a filesystem lookup. If the lookup
does not succeed, the same is done with all directories on the include path list.

It is recommended to set the base path to the root directory of your project and use include paths to specify additional
locations that may contain libraries your project depends on. This lets you import from these libraries in a uniform
way, no matter where they are located in the filesystem relative to your project. For example, if you use npm to install
packages and your contract imports@openzeppelin/contracts/utils/Strings.sol, you can use these options
to tell the compiler that the library can be found in one of the npm package directories:

solc contract.sol\
--base-path .\
--include-path node_modules/ \
--include-path /usr/local/lib/node_modules/

Your contract will compile (with the same exact metadata) no matter whether you install the library in the local or
global package directory or even directly under your project root.

By default the base path is empty, which leaves the source unit name unchanged. When the source unit name is a
relative path, this results in the file being looked up in the directory the compiler has been invoked from. It is also the
only value that results in absolute paths in source unit names being actually interpreted as absolute paths on disk. If
the base path itself is relative, it is interpreted as relative to the current working directory of the compiler.

**Note:** Include paths cannot have empty values and must be used together with a non-empty base path.

**Note:** Include paths and base path can overlap as long as it does not make import resolution ambiguous. For example,
you can specify a directory inside base path as an include directory or have an include directory that is a subdirectory of
another include directory. The compiler will only issue an error if the source unit name passed to the Host Filesystem
Loader represents an existing path when combined with multiple include paths or an include path and base path.

**3.33. Import Path Resolution 357**


**CLI Path Normalization and Stripping**

On the command-line the compiler behaves just as you would expect from any other program: it accepts paths in a
format native to the platform and relative paths are relative to the current working directory. The source unit names
assigned to files whose paths are specified on the command-line, however, should not change just because the project is
being compiled on a different platform or because the compiler happens to have been invoked from a different directory.
To achieve this, paths to source files coming from the command-line must be converted to a canonical form, and, if
possible, made relative to the base path or one of the include paths.

The normalization rules are as follows:

- If a path is relative, it is made absolute by prepending the current working directory to it.
- Internal.and..segments are collapsed.
- Platform-specific path separators are replaced with forward slashes.
- Sequences of multiple consecutive path separators are squashed into a single separator (unless they are the leading
    slashes of an UNC path).
- If the path includes a root name (e.g. a drive letter on Windows) and the root is the same as the root of the current
    working directory, the root is replaced with/.
- Symbolic links in the path are **not** resolved.
    **-** The only exception is the path to the current working directory prepended to relative paths in the process
       of making them absolute. On some platforms the working directory is reported always with symbolic links
       resolved so for consistency the compiler resolves them everywhere.
- The original case of the path is preserved even if the filesystem is case-insensitive but case-preserving and the
    actual case on disk is different.

**Note:** There are situations where paths cannot be made platform-independent. For example on Windows the compiler
can avoid using drive letters by referring to the root directory of the current drive as/but drive letters are still necessary
for paths leading to other drives. You can avoid such situations by ensuring that all the files are available within a single
directory tree on the same drive.

After normalization the compiler attempts to make the source file path relative. It tries the base path first and then the
include paths in the order they were given. If the base path is empty or not specified, it is treated as if it was equal to the
path to the current working directory (with all symbolic links resolved). The result is accepted only if the normalized
directory path is the exact prefix of the normalized file path. Otherwise the file path remains absolute. This makes the
conversion unambiguous and ensures that the relative path does not start with../. The resulting file path becomes the
source unit name.

**Note:** The relative path produced by stripping must remain unique within the base path and include paths. For example
the compiler will issue an error for the following command if both/project/contract.soland/lib/contract.
solexist:

solc /project/contract.sol --base-path /project --include-path /lib

**Note:** Prior to version 0.8.8, CLI path stripping was not performed and the only normalization applied was the
conversion of path separators. When working with older versions of the compiler it is recommended to invoke the
compiler from the base path and to only use relative paths on the command-line.

**358 Chapter 3. Contents**


**3.33.4 Allowed Paths**

As a security measure, the Host Filesystem Loader will refuse to load files from outside of a few locations that are
considered safe by default:

- Outside of Standard JSON mode:
    **-** The directories containing input files listed on the command-line.
    **-** The directories used as _remapping_ targets. If the target is not a directory (i.e does not end with/,/.or
       /..) the directory containing the target is used instead.
    **-** Base path and include paths.
- In Standard JSON mode:
    **-** Base path and include paths.

Additional directories can be whitelisted using the--allow-pathsoption. The option accepts a comma-separated
list of paths:

cd /home/user/project/
solc token/contract.sol \
lib/util.sol=libs/util.sol\
--base-path=token/\
--include-path=/lib/\
--allow-paths=../utils/,/tmp/libraries

When the compiler is invoked with the command shown above, the Host Filesystem Loader will allow importing files
from the following directories:

- /home/user/project/token/(becausetoken/contains the input file and also because it is the base path),
- /lib/(because/lib/is one of the include paths),
- /home/user/project/libs/(becauselibs/is a directory containing a remapping target),
- /home/user/utils/(because of../utils/passed to--allow-paths),
- /tmp/libraries/(because of/tmp/librariespassed to--allow-paths),

**Note:** The working directory of the compiler is one of the paths allowed by default only if it happens to be the base
path (or the base path is not specified or has an empty value).

**Note:** The compiler does not check if allowed paths actually exist and whether they are directories. Non-existent
or empty paths are simply ignored. If an allowed path matches a file rather than a directory, the file is considered
whitelisted, too.

**Note:** Allowed paths are case-sensitive even if the filesystem is not. The case must exactly match the one used in your
imports. For example--allow-paths tokenswill not matchimport "Tokens/IERC20.sol".

```
Warning: Files and directories only reachable through symbolic links from allowed directories are not automati-
cally whitelisted. For example iftoken/contract.solin the example above was actually a symlink pointing at
/etc/passwdthe compiler would refuse to load it unless/etc/was one of the allowed paths too.
```
**3.33. Import Path Resolution 359**


**3.33.5 Import Remapping**

Import remapping allows you to redirect imports to a different location in the virtual filesystem. The mechanism works
by changing the translation between import paths and source unit names. For example you can set up a remapping so
that any import from the virtual directorygithub.com/ethereum/dapp-bin/library/would be seen as an import
fromdapp-bin/library/instead.

You can limit the scope of a remapping by specifying a _context_. This allows creating remappings that apply only to
imports located in a specific library or a specific file. Without a context a remapping is applied to every matching
import in all the files in the virtual filesystem.

Import remappings have the form ofcontext:prefix=target:

- contextmust match the beginning of the source unit name of the file containing the import.
- prefixmust match the beginning of the source unit name resulting from the import.
- targetis the value the prefix is replaced with.

For example, if you clone https://github.com/ethereum/dapp-bin/ locally to/project/dapp-binand run the compiler
with:

solc github.com/ethereum/dapp-bin/=dapp-bin/ --base-path /project source.sol

you can use the following in your source file:

import "github.com/ethereum/dapp-bin/library/math.sol";// source unit name: dapp-bin/
˓→library/math.sol

The compiler will look for the file in the VFS underdapp-bin/library/math.sol. If the file is not available there,
the source unit name will be passed to the Host Filesystem Loader, which will then look in/project/dapp-bin/
library/math.sol.

```
Warning: Information about remappings is stored in contract metadata. Since the binary produced by the compiler
has a hash of the metadata embedded in it, any modification to the remappings will result in different bytecode.
For this reason you should be careful not to include any local information in remapping targets. For example if
your library is located in/home/user/packages/mymath/math.sol, a remapping like@math/=/home/user/
packages/mymath/would result in your home directory being included in the metadata. To be able to reproduce
the same bytecode with such a remapping on a different machine, you would need to recreate parts of your local
directory structure in the VFS and (if you rely on Host Filesystem Loader) also in the host filesystem.
To avoid having your local directory structure embedded in the metadata, it is recommended to designate the direc-
tories containing libraries as include paths instead. For example, in the example above--include-path /home/
user/packages/would let you use imports starting withmymath/. Unlike remapping, the option on its own will
not makemymathappear as@mathbut this can be achieved by creating a symbolic link or renaming the package
subdirectory.
```
As a more complex example, suppose you rely on a module that uses an old version of dapp-bin that you checked out
to/project/dapp-bin_old, then you can run:

solc module1:github.com/ethereum/dapp-bin/=dapp-bin/\
module2:github.com/ethereum/dapp-bin/=dapp-bin_old/\
--base-path /project\
source.sol

This means that all imports inmodule2point to the old version but imports inmodule1point to the new version.

**360 Chapter 3. Contents**


Here are the detailed rules governing the behavior of remappings:

1. **Remappings only affect the translation between import paths and source unit names.**
    Source unit names added to the VFS in any other way cannot be remapped. For example the paths you specify
    on the command-line and the ones insources.urlsin Standard JSON are not affected.

```
solc /project/=/contracts/ /project/contract.sol# source unit name: /project/
˓→contract.sol
```
```
In the example above the compiler will load the source code from/project/contract.soland place it under
that exact source unit name in the VFS, not under/contract/contract.sol.
```
2. **Context and prefix must match source unit names, not import paths.**
    - This means that you cannot remap./or../directly since they are replaced during the translation to source
       unit name but you can remap the part of the name they are replaced with:

```
solc ./=a/ /project/=b/ /project/contract.sol# source unit name: /project/
˓→contract.sol
```
```
Listing 5: /project/contract.sol
import"./util.sol" as util; // source unit name: b/util.sol
```
- You cannot remap base path or any other part of the path that is only added internally by an import callback:

```
solc /project/=/contracts/ /project/contract.sol --base-path /project# source␣
˓→unit name: contract.sol
```
```
Listing 6: /project/contract.sol
import"util.sol" as util; // source unit name: util.sol
```
3. **Target is inserted directly into the source unit name and does not necessarily have to be a valid path.**
    - It can be anything as long as the import callback can handle it. In case of the Host Filesystem Loader
       this includes also relative paths. When using the JavaScript interface you can even use URLs and abstract
       identifiers if your callback can handle them.
    - Remapping happens after relative imports have already been resolved into source unit names. This means
       that targets starting with./and../have no special meaning and are relative to the base path rather than
       to the location of the source file.
    - Remapping targets are not normalized so@root/=./a/b//will remap@root/contract.solto./a/b/
       /contract.soland nota/b/contract.sol.
    - If the target does not end with a slash, the compiler will not add one automatically:

```
solc /project/=/contracts /project/contract.sol# source unit name: /project/
˓→contract.sol
```
```
Listing 7: /project/contract.sol
import"/project/util.sol" as util; // source unit name: /contractsutil.sol
```
4. **Context and prefix are patterns and matches must be exact.**
    - a//b=cwill not matcha/b.

**3.33. Import Path Resolution 361**


- source unit names are not normalized soa/b=cwill not matcha//beither.
- Parts of file and directory names can match as well. /newProject/con:/new=oldwill match/
    newProject/contract.soland remap it tooldProject/contract.sol.
5. **At most one remapping is applied to a single import.**
- If multiple remappings match the same source unit name, the one with the longest matching prefix is chosen.
- If prefixes are identical, the one specified last wins.
- Remappings do not work on other remappings. For examplea=b b=c c=dwill not result inabeing
remapped tod.
6. **Prefix cannot be empty but context and target are optional.**
- Iftargetis the empty string,prefixis simply removed from import paths.
- Emptycontextmeans that the remapping applies to all imports in all source units.

**3.33.6 Using URLs in imports**

Most URL prefixes such ashttps://ordata://have no special meaning in import paths. The only exception is
file://which is stripped from source unit names by the Host Filesystem Loader.

When compiling locally you can use import remapping to replace the protocol and domain part with a local path:

solc :https://github.com/ethereum/dapp-bin=/usr/local/dapp-bin contract.sol

Note the leading:, which is necessary when the remapping context is empty. Otherwise thehttps:part would be
interpreted by the compiler as the context.

### 3.34 Style Guide

**3.34.1 Introduction**

This guide is intended to provide coding conventions for writing Solidity code. This guide should be thought of as
an evolving document that will change over time as useful conventions are found and old conventions are rendered
obsolete.

Many projects will implement their own style guides. In the event of conflicts, project specific style guides take prece-
dence.

The structure and many of the recommendations within this style guide were taken from Python’s pep8 style guide.

The goal of this guide is _not_ to be the right way or the best way to write Solidity code. The goal of this guide is
_consistency_. A quote from Python’s pep8 captures this concept well.

**Note:** A style guide is about consistency. Consistency with this style guide is important. Consistency within a project
is more important. Consistency within one module or function is most important.

But most importantly: **know when to be inconsistent** – sometimes the style guide just doesn’t apply. When in doubt,
use your best judgment. Look at other examples and decide what looks best. And do not hesitate to ask!

**362 Chapter 3. Contents**


**3.34.2 Code Layout**

**Indentation**

Use 4 spaces per indentation level.

**Tabs or Spaces**

Spaces are the preferred indentation method.

Mixing tabs and spaces should be avoided.

**Blank Lines**

Surround top level declarations in Solidity source with two blank lines.

Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract A {
// ...
}

contract B {
// ...
}

contract C {
// ...
}

No:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract A {
// ...
}
contract B {
// ...
}

contract C {
// ...
}

Within a contract surround function declarations with a single blank line.

Blank lines may be omitted between groups of related one-liners (such as stub functions for an abstract contract)

**3.34. Style Guide 363**


Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstractcontract A {
functionspam() publicvirtual pure;
functionham()public virtual pure;
}

contract B isA {
functionspam() publicpure override {
// ...
}

functionham()public pure override {
// ...
}
}

No:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.6.0 <0.9.0;

abstractcontract A {
functionspam() virtual pure public;
functionham()public virtual pure;
}

contract B isA {
functionspam() publicpure override {
// ...
}
functionham()public pure override {
// ...
}
}

**Maximum Line Length**

Maximum suggested line length is 120 characters.

Wrapped lines should conform to the following guidelines.

1. The first argument should not be attached to the opening parenthesis.
2. One, and only one, indent should be used.
3. Each argument should fall on its own line.
4. The terminating element,);, should be placed on the final line by itself.

Function Calls

**364 Chapter 3. Contents**


Yes:

thisFunctionCallIsReallyLong(
longArgument1,
longArgument2,
longArgument3
);

No:

thisFunctionCallIsReallyLong(longArgument1,
longArgument2,
longArgument3
);

thisFunctionCallIsReallyLong(longArgument1,
longArgument2,
longArgument3
);

thisFunctionCallIsReallyLong(
longArgument1, longArgument2,
longArgument3
);

thisFunctionCallIsReallyLong(
longArgument1,
longArgument2,
longArgument3
);

thisFunctionCallIsReallyLong(
longArgument1,
longArgument2,
longArgument3);

Assignment Statements

Yes:

thisIsALongNestedMapping[being][set][toSomeValue] = someFunction(
argument1,
argument2,
argument3,
argument4
);

No:

thisIsALongNestedMapping[being][set][toSomeValue] = someFunction(argument1,
argument2,
argument3,
argument4);

Event Definitions and Event Emitters

**3.34. Style Guide 365**


Yes:

eventLongAndLotsOfArgs(
addresssender,
addressrecipient,
uint256publicKey,
uint256amount,
bytes32[] options
);

emit LongAndLotsOfArgs(
sender,
recipient,
publicKey,
amount,
options
);

No:

eventLongAndLotsOfArgs(addresssender,
addressrecipient,
uint256publicKey,
uint256amount,
bytes32[] options);

emit LongAndLotsOfArgs(sender,
recipient,
publicKey,
amount,
options);

**Source File Encoding**

UTF-8 or ASCII encoding is preferred.

**Imports**

Import statements should always be placed at the top of the file.

Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

import "./Owned.sol";

contract A {
// ...
}

```
(continues on next page)
```
**366 Chapter 3. Contents**


```
(continued from previous page)
```
contract B isOwned {
// ...
}

No:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract A {
// ...
}

import "./Owned.sol";

contract B isOwned {
// ...
}

**Order of Functions**

Ordering helps readers identify which functions they can call and to find the constructor and fallback definitions easier.

Functions should be grouped according to their visibility and ordered:

- constructor
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private

Within a grouping, place theviewandpurefunctions last.

Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract A {
constructor() {
// ...
}

```
receive()external payable{
// ...
}
```
```
(continues on next page)
```
**3.34. Style Guide 367**


```
(continued from previous page)
fallback()external {
// ...
}
```
```
// External functions
// ...
```
```
// External functions that are view
// ...
```
```
// External functions that are pure
// ...
```
```
// Public functions
// ...
```
```
// Internal functions
// ...
```
// Private functions
// ...
}

No:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract A {

```
// External functions
// ...
```
```
fallback()external {
// ...
}
receive()external payable{
// ...
}
```
```
// Private functions
// ...
```
```
// Public functions
// ...
```
```
constructor() {
// ...
}
```
// Internal functions
// ...
}

**368 Chapter 3. Contents**


**Whitespace in Expressions**

Avoid extraneous whitespace in the following situations:

Immediately inside parenthesis, brackets or braces, with the exception of single line function declarations.

Yes:

spam(ham[1], Coin({name: "ham"}));

No:

spam( ham[ 1 ], Coin( { name: "ham" } ) );

Exception:

functionsingleLine()public { spam(); }

Immediately before a comma, semicolon:

Yes:

functionspam(uinti, Coin coin) public;

No:

functionspam(uinti , Coin coin) public;

More than one space around an assignment or other operator to align with another:

Yes:

x = 1;
y = 2;
longVariable = 3;

No:

x = 1;
y = 2;
longVariable = 3;

Do not include a whitespace in the receive and fallback functions:

Yes:

receive()external payable{
...
}

fallback() external{
...
}

No:

**3.34. Style Guide 369**


receive () external payable{
...
}

fallback ()external{
...
}

**Control Structures**

The braces denoting the body of a contract, library, functions and structs should:

- open on the same line as the declaration
- close on their own line at the same indentation level as the beginning of the declaration.
- The opening brace should be preceded by a single space.

Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Coin{
struct Bank {
addressowner;
uintbalance;
}
}

No:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

contract Coin
{
struct Bank {
addressowner;
uintbalance;
}
}

The same recommendations apply to the control structuresif,else,while, andfor.

Additionally there should be a single space between the control structuresif,while, andforand the parenthetic block
representing the conditional, as well as a single space between the conditional parenthetic block and the opening brace.

Yes:

if (...) {
...
}

for(...) {
(continues on next page)

**370 Chapter 3. Contents**


(continued from previous page)
...
}

No:

if (...)
{
...
}

while(...){
}

for(...) {
...;}

For control structures whose body contains a single statement, omitting the braces is ok _if_ the statement is contained
on a single line.

Yes:

if (x < 10)
x += 1;

No:

if (x < 10)
someArray.push(Coin({
name:'spam',
value: 42
}));

Forifblocks which have anelseorelse ifclause, theelseshould be placed on the same line as theif’s closing
brace. This is an exception compared to the rules of other block-like structures.

Yes:

if (x < 3) {
x += 1;
}else if (x > 7) {
x -= 1;
}else {
x = 5;
}

if (x < 3)
x += 1;
else
x -= 1;

No:

**3.34. Style Guide 371**


if (x < 3) {
x += 1;
}
else{
x -= 1;
}

**Function Declaration**

For short function declarations, it is recommended for the opening brace of the function body to be kept on the same
line as the function declaration.

The closing brace should be at the same indentation level as the function declaration.

The opening brace should be preceded by a single space.

Yes:

functionincrement(uint x)public purereturns(uint) {
return x + 1;
}

functionincrement(uint x)public pure onlyOwnerreturns(uint) {
return x + 1;
}

No:

functionincrement(uint x)public purereturns(uint)
{
return x + 1;
}

functionincrement(uint x)public purereturns(uint){
return x + 1;
}

functionincrement(uint x)public purereturns(uint) {
return x + 1;
}

functionincrement(uint x)public purereturns(uint) {
return x + 1;}

The modifier order for a function should be:

1. Visibility
2. Mutability
3. Virtual
4. Override
5. Custom modifiers

Yes:

**372 Chapter 3. Contents**


functionbalance(uintfrom)public view overridereturns(uint) {
return balanceOf[from];
}

functionincrement(uint x)public pure onlyOwnerreturns(uint) {
return x + 1;
}

No:

functionbalance(uintfrom)public override viewreturns(uint) {
return balanceOf[from];
}

functionincrement(uint x) onlyOwnerpublicpurereturns(uint) {
return x + 1;
}

For long function declarations, it is recommended to drop each argument onto its own line at the same indentation level
as the function body. The closing parenthesis and opening bracket should be placed on their own line as well at the
same indentation level as the function declaration.

Yes:

functionthisFunctionHasLotsOfArguments(
addressa,
addressb,
addressc,
addressd,
addresse,
addressf
)
public
{
doSomething();
}

No:

functionthisFunctionHasLotsOfArguments(addressa, addressb,addressc,
addressd,addresse, addressf) public{
doSomething();
}

functionthisFunctionHasLotsOfArguments(addressa,
addressb,
addressc,
addressd,
addresse,
addressf) public{
doSomething();
}

functionthisFunctionHasLotsOfArguments(
(continues on next page)

**3.34. Style Guide 373**


(continued from previous page)
addressa,
addressb,
addressc,
addressd,
addresse,
addressf)public {
doSomething();
}

If a long function declaration has modifiers, then each modifier should be dropped to its own line.

Yes:

functionthisFunctionNameIsReallyLong(addressx,addressy, addressz)
public
onlyOwner
priced
returns(address)
{
doSomething();
}

functionthisFunctionNameIsReallyLong(
addressx,
addressy,
addressz
)
public
onlyOwner
priced
returns(address)
{
doSomething();
}

No:

functionthisFunctionNameIsReallyLong(addressx,addressy, addressz)
public
onlyOwner
priced
returns(address) {
doSomething();
}

functionthisFunctionNameIsReallyLong(addressx,addressy, addressz)
public onlyOwner pricedreturns(address)
{
doSomething();
}

functionthisFunctionNameIsReallyLong(addressx,addressy, addressz)
public
(continues on next page)

**374 Chapter 3. Contents**


(continued from previous page)
onlyOwner
priced
returns(address) {
doSomething();
}

Multiline output parameters and return statements should follow the same style recommended for wrapping long lines
found in the _Maximum Line Length_ section.

Yes:

functionthisFunctionNameIsReallyLong(
addressa,
addressb,
addressc
)
public
returns(
addresssomeAddressName,
uint256LongArgument,
uint256Argument
)
{
doSomething()

return (
veryLongReturnArg1,
veryLongReturnArg2,
veryLongReturnArg3
);
}

No:

functionthisFunctionNameIsReallyLong(
addressa,
addressb,
addressc
)
public
returns(addresssomeAddressName,
uint256LongArgument,
uint256Argument)
{
doSomething()

return (veryLongReturnArg1,
veryLongReturnArg1,
veryLongReturnArg1);
}

For constructor functions on inherited contracts whose bases require arguments, it is recommended to drop the base
constructors onto new lines in the same manner as modifiers if the function declaration is long or hard to read.

**3.34. Style Guide 375**


Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
// Base contracts just to make this compile
contract B {
constructor(uint) {
}
}

contract C {
constructor(uint,uint) {
}
}

contract D {
constructor(uint) {
}
}

contract A isB, C, D {
uintx;

constructor(uintparam1,uintparam2,uintparam3,uintparam4,uintparam5)
B(param1)
C(param2, param3)
D(param4)
{
// do something with param5
x = param5;
}
}

No:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// Base contracts just to make this compile
contract B {
constructor(uint) {
}
}

contract C {
constructor(uint,uint) {
}
}

```
(continues on next page)
```
**376 Chapter 3. Contents**


```
(continued from previous page)
```
contract D {
constructor(uint) {
}
}

contract A isB, C, D {
uintx;

constructor(uintparam1,uintparam2,uintparam3,uintparam4,uintparam5)
B(param1)
C(param2, param3)
D(param4) {
x = param5;
}
}

contract X isB, C, D {
uintx;

constructor(uintparam1,uintparam2,uintparam3,uintparam4,uintparam5)
B(param1)
C(param2, param3)
D(param4) {
x = param5;
}
}

When declaring short functions with a single statement, it is permissible to do it on a single line.

Permissible:

functionshortFunction() public{ doSomething(); }

These guidelines for function declarations are intended to improve readability. Authors should use their best judgment
as this guide does not try to cover all possible permutations for function declarations.

**Mappings**

In variable declarations, do not separate the keywordmappingfrom its type by a space. Do not separate any nested
mappingkeyword from its type by whitespace.

Yes:

mapping(uint=> uint) map;
mapping(address=>bool) registeredAddresses;
mapping(uint=> mapping(bool=> Data[]))public data;
mapping(uint=> mapping(uint=> s)) data;

No:

**3.34. Style Guide 377**


mapping(uint=> uint) map;
mapping(address=> bool) registeredAddresses;
mapping(uint=> mapping(bool=> Data[]))public data;
mapping(uint=> mapping(uint=> s)) data;

**Variable Declarations**

Declarations of array variables should not have a space between the type and the brackets.

Yes:

uint[] x;

No:

uint[] x;

**Other Recommendations**

- Strings should be quoted with double-quotes instead of single-quotes.

Yes:

str = "foo";
str = "Hamlet says, 'To be or not to be...'";

No:

str ='bar';
str ='"Be yourself; everyone else is already taken." -Oscar Wilde';

- Surround operators with a single space on either side.

Yes:

x = 3;
x = 100 / 10;
x += 3 + 4;
x |= y && z;

No:

x=3;
x = 100/10;
x += 3+4;
x |= y&&z;

- Operators with a higher priority than others can exclude surrounding whitespace in order to denote precedence.
    This is meant to allow for improved readability for complex statements. You should always use the same amount
    of whitespace on either side of an operator:

Yes:

**378 Chapter 3. Contents**


x = 2**3 + 5;
x = 2*y + 3*z;
x = (a+b) * (a-b);

No:

x = 2** 3 + 5;
x = y+z;
x +=1;

**3.34.3 Order of Layout**

Contract elements should be laid out in the following order:

1. Pragma statements
2. Import statements
3. Events
4. Errors
5. Interfaces
6. Libraries
7. Contracts

Inside each contract, library or interface, use the following order:

1. Type declarations
2. State variables
3. Events
4. Errors
5. Modifiers
6. Functions

**Note:** It might be clearer to declare types close to their use in events or state variables.

Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.4 <0.9.0;

abstractcontract Math{
error DivideByZero();
functiondivide(int256numerator, int256denominator)public virtualreturns␣
˓→(uint256);
}

No:

**3.34. Style Guide 379**


// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.8.4 <0.9.0;

abstractcontract Math{
functiondivide(int256numerator, int256denominator)public virtualreturns␣
˓→(uint256);
error DivideByZero();
}

**3.34.4 Naming Conventions**

Naming conventions are powerful when adopted and used broadly. The use of different conventions can convey signif-
icant _meta_ information that would otherwise not be immediately available.

The naming recommendations given here are intended to improve the readability, and thus they are not rules, but rather
guidelines to try and help convey the most information through the names of things.

Lastly, consistency within a codebase should always supersede any conventions outlined in this document.

**Naming Styles**

To avoid confusion, the following names will be used to refer to different naming styles.

- b(single lowercase letter)
- B(single uppercase letter)
- lowercase
- UPPERCASE
- UPPER_CASE_WITH_UNDERSCORES
- CapitalizedWords(or CapWords)
- mixedCase(differs from CapitalizedWords by initial lowercase character!)

**Note:** When using initialisms in CapWords, capitalize all the letters of the initialisms. Thus HTTPServerError is better
than HttpServerError. When using initialisms in mixedCase, capitalize all the letters of the initialisms, except keep the
first one lower case if it is the beginning of the name. Thus xmlHTTPRequest is better than XMLHTTPRequest.

**Names to Avoid**

- l- Lowercase letter el
- O- Uppercase letter oh
- I- Uppercase letter eye

Never use any of these for single letter variable names. They are often indistinguishable from the numerals one and
zero.

**380 Chapter 3. Contents**


**Contract and Library Names**

- Contracts and libraries should be named using the CapWords style. Examples: SimpleToken,SmartBank,
    CertificateHashRepository,Player,Congress,Owned.
- Contract and library names should also match their filenames.
- If a contract file includes multiple contracts and/or libraries, then the filename should match the _core contract_.
    This is not recommended however if it can be avoided.

As shown in the example below, if the contract name isCongressand the library name isOwned, then their associated
filenames should beCongress.solandOwned.sol.

Yes:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// Owned.sol
contract Owned{
address publicowner;

```
modifieronlyOwner {
require(msg.sender== owner);
_;
}
```
```
constructor() {
owner =msg.sender;
}
```
functiontransferOwnership(addressnewOwner)public onlyOwner {
owner = newOwner;
}
}

and inCongress.sol:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.0 <0.9.0;

import "./Owned.sol";

contract Congress isOwned, TokenRecipient {
//...
}

No:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

// owned.sol
contract owned{
address publicowner;
(continues on next page)

**3.34. Style Guide 381**


```
(continued from previous page)
```
```
modifieronlyOwner {
require(msg.sender== owner);
_;
}
```
```
constructor() {
owner =msg.sender;
}
```
functiontransferOwnership(addressnewOwner)public onlyOwner {
owner = newOwner;
}
}

and inCongress.sol:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.7.0;

import "./owned.sol";

contract Congress isowned, tokenRecipient {
//...
}

**Struct Names**

Structs should be named using the CapWords style. Examples:MyCoin,Position,PositionXY.

**Event Names**

Events should be named using the CapWords style. Examples:Deposit,Transfer,Approval,BeforeTransfer,
AfterTransfer.

**Function Names**

Functions should use mixedCase. Examples:getBalance,transfer,verifyOwner,addMember,changeOwner.

**382 Chapter 3. Contents**


**Function Argument Names**

Function arguments should use mixedCase. Examples: initialSupply, account, recipientAddress,
senderAddress,newOwner.

When writing library functions that operate on a custom struct, the struct should be the first argument and should always
be namedself.

**Local and State Variable Names**

Use mixedCase. Examples: totalSupply,remainingSupply, balancesOf, creatorAddress,isPreSale,
tokenExchangeRate.

**Constants**

Constants should be named with all capital letters with underscores separating words. Examples: MAX_BLOCKS,
TOKEN_NAME,TOKEN_TICKER,CONTRACT_VERSION.

**Modifier Names**

Use mixedCase. Examples:onlyBy,onlyAfter,onlyDuringThePreSale.

**Enums**

Enums, in the style of simple type declarations, should be named using the CapWords style. Examples:TokenGroup,
Frame,HashStyle,CharacterLocation.

**Avoiding Naming Collisions**

- singleTrailingUnderscore_

This convention is suggested when the desired name collides with that of an existing state variable, function, built-in
or otherwise reserved name.

**Underscore Prefix for Non-external Functions and Variables**

- _singleLeadingUnderscore

This convention is suggested for non-external functions and state variables (privateorinternal). State variables
without a specified visibility areinternalby default.

When designing a smart contract, the public-facing API (functions that can be called by any account) is an important
consideration. Leading underscores allow you to immediately recognize the intent of such functions, but more im-
portantly, if you change a function from non-external to external (includingpublic) and rename it accordingly, this
forces you to review every call site while renaming. This can be an important manual check against unintended external
functions and a common source of security vulnerabilities (avoid find-replace-all tooling for this change).

**3.34. Style Guide 383**


**3.34.5 NatSpec**

Solidity contracts can also contain NatSpec comments. They are written with a triple slash (///) or a double asterisk
block (/** ... */) and they should be used directly above function declarations or statements.

For example, the contract from _a simple smart contract_ with the comments added looks like the one below:

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

/// @author The Solidity Team
/// @title A simple storage example
contract SimpleStorage{
uintstoredData;

```
/// Store`x`.
/// @param x the new value to store
/// @dev stores the number in the state variable`storedData`
functionset(uintx) public{
storedData = x;
}
```
/// Return the stored value.
/// @dev retrieves the value of the state variable`storedData`
/// @return the stored value
functionget()public viewreturns(uint) {
returnstoredData;
}
}

It is recommended that Solidity contracts are fully annotated using _NatSpec_ for all public interfaces (everything in the
ABI).

Please see the section about _NatSpec_ for a detailed explanation.

### 3.35 Common Patterns

**3.35.1 Withdrawal from Contracts**

The recommended method of sending funds after an effect is using the withdrawal pattern. Although the most intuitive
method of sending Ether, as a result of an effect, is a directtransfercall, this is not recommended as it introduces a
potential security risk. You may read more about this on the _Security Considerations_ page.

The following is an example of the withdrawal pattern in practice in a contract where the goal is to send the most of
some compensation, e.g. Ether, to the contract in order to become the “richest”, inspired by King of the Ether.

In the following contract, if you are no longer the richest, you receive the funds of the person who is now the richest.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract WithdrawalContract{
address publicrichest;
uint publicmostSent;
(continues on next page)

**384 Chapter 3. Contents**


```
(continued from previous page)
```
```
mapping(address=>uint) pendingWithdrawals;
```
```
/// The amount of Ether sent was not higher than
/// the currently highest amount.
error NotEnoughEther();
```
```
constructor() payable{
richest =msg.sender;
mostSent =msg.value;
}
```
```
functionbecomeRichest() public payable{
if (msg.value<= mostSent) revert NotEnoughEther();
pendingWithdrawals[richest] +=msg.value;
richest =msg.sender;
mostSent =msg.value;
}
```
functionwithdraw() public{
uintamount = pendingWithdrawals[msg.sender];
// Remember to zero the pending refund before
// sending to prevent reentrancy attacks
pendingWithdrawals[msg.sender] = 0;
payable(msg.sender).transfer(amount);
}
}

This is as opposed to the more intuitive sending pattern:

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract SendContract{
addresspayablepublicrichest;
uint publicmostSent;

```
/// The amount of Ether sent was not higher than
/// the currently highest amount.
error NotEnoughEther();
```
```
constructor() payable{
richest =payable(msg.sender);
mostSent =msg.value;
}
```
```
functionbecomeRichest() public payable{
if (msg.value<= mostSent) revert NotEnoughEther();
// This line can cause problems (explained below).
richest.transfer(msg.value);
richest =payable(msg.sender);
mostSent =msg.value;
(continues on next page)
```
**3.35. Common Patterns 385**


(continued from previous page)
}
}

Notice that, in this example, an attacker could trap the contract into an unusable state by causingrichestto be the
address of a contract that has a receive or fallback function which fails (e.g. by usingrevert()or by just consuming
more than the 2300 gas stipend transferred to them). That way, whenevertransferis called to deliver funds to the
“poisoned” contract, it will fail and thus alsobecomeRichestwill fail, with the contract being stuck forever.

In contrast, if you use the “withdraw” pattern from the first example, the attacker can only cause his or her own withdraw
to fail and not the rest of the contract’s workings.

**3.35.2 Restricting Access**

Restricting access is a common pattern for contracts. Note that you can never restrict any human or computer from
reading the content of your transactions or your contract’s state. You can make it a bit harder by using encryption, but
if your contract is supposed to read the data, so will everyone else.

You can restrict read access to your contract’s state by **other contracts**. That is actually the default unless you declare
your state variablespublic.

Furthermore, you can restrict who can make modifications to your contract’s state or call your contract’s functions and
this is what this section is about.

The use of **function modifiers** makes these restrictions highly readable.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

contract AccessRestriction{
// These will be assigned at the construction
// phase, where `msg.sender` is the account
// creating this contract.
address publicowner =msg.sender;
uint publiccreationTime =block.timestamp;

```
// Now follows a list of errors that
// this contract can generate together
// with a textual explanation in special
// comments.
```
```
/// Sender not authorized for this
/// operation.
error Unauthorized();
```
```
/// Function called too early.
error TooEarly();
```
```
/// Not enough Ether sent with function call.
error NotEnoughEther();
```
```
// Modifiers can be used to change
// the body of a function.
// If this modifier is used, it will
(continues on next page)
```
**386 Chapter 3. Contents**


```
(continued from previous page)
// prepend a check that only passes
// if the function is called from
// a certain address.
modifieronlyBy(addressaccount)
{
if (msg.sender != account)
revert Unauthorized();
// Do not forget the "_;"! It will
// be replaced by the actual function
// body when the modifier is used.
_;
}
```
```
/// Make`newOwner` the new owner of this
/// contract.
functionchangeOwner(addressnewOwner)
public
onlyBy(owner)
{
owner = newOwner;
}
```
```
modifieronlyAfter(uinttime) {
if (block.timestamp < time)
revert TooEarly();
_;
}
```
```
/// Erase ownership information.
/// May only be called 6 weeks after
/// the contract has been created.
functiondisown()
public
onlyBy(owner)
onlyAfter(creationTime + 6 weeks)
{
delete owner;
}
```
```
// This modifier requires a certain
// fee being associated with a function call.
// If the caller sent too much, he or she is
// refunded, but only after the function body.
// This was dangerous before Solidity version 0.4.0,
// where it was possible to skip the part after`_;`.
modifiercosts(uint amount) {
if (msg.value< amount)
revert NotEnoughEther();
```
```
_;
if (msg.value> amount)
payable(msg.sender).transfer(msg.value - amount);
(continues on next page)
```
**3.35. Common Patterns 387**


```
(continued from previous page)
}
```
functionforceOwnerChange(addressnewOwner)
public
payable
costs(200 ether)
{
owner = newOwner;
// just some example condition
if (uint160(owner) & 0 == 1)
// This did not refund for Solidity
// before version 0.4.0.
return;
// refund overpaid fees
}
}

A more specialised way in which access to function calls can be restricted will be discussed in the next example.

**3.35.3 State Machine**

Contracts often act as a state machine, which means that they have certain **stages** in which they behave differently or
in which different functions can be called. A function call often ends a stage and transitions the contract into the next
stage (especially if the contract models **interaction** ). It is also common that some stages are automatically reached at
a certain point in **time**.

An example for this is a blind auction contract which starts in the stage “accepting blinded bids”, then transitions to
“revealing bids” which is ended by “determine auction outcome”.

Function modifiers can be used in this situation to model the states and guard against incorrect usage of the contract.

**Example**

In the following example, the modifieratStageensures that the function can only be called at a certain stage.

Automatic timed transitions are handled by the modifiertimedTransitions, which should be used for all functions.

**Note: Modifier Order Matters**. If atStage is combined with timedTransitions, make sure that you mention it after
the latter, so that the new stage is taken into account.

Finally, the modifiertransitionNextcan be used to automatically go to the next stage when the function finishes.

**Note: Modifier May be Skipped**. This only applies to Solidity before version 0.4.0: Since modifiers are applied by
simply replacing code and not by using a function call, the code in the transitionNext modifier can be skipped if the
function itself uses return. If you want to do that, make sure to call nextStage manually from those functions. Starting
with version 0.4.0, modifier code will run even if the function explicitly returns.

// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;

```
(continues on next page)
```
**388 Chapter 3. Contents**


```
(continued from previous page)
```
contract StateMachine{
enumStages {
AcceptingBlindedBids,
RevealBids,
AnotherStage,
AreWeDoneYet,
Finished
}
/// Function cannot be called at this time.
error FunctionInvalidAtThisStage();

```
// This is the current stage.
Stages publicstage = Stages.AcceptingBlindedBids;
```
```
uint publiccreationTime =block.timestamp;
```
```
modifieratStage(Stages stage_) {
if (stage != stage_)
revert FunctionInvalidAtThisStage();
_;
}
```
```
functionnextStage()internal{
stage = Stages(uint(stage) + 1);
}
```
```
// Perform timed transitions. Be sure to mention
// this modifier first, otherwise the guards
// will not take the new stage into account.
modifiertimedTransitions() {
if (stage == Stages.AcceptingBlindedBids &&
block.timestamp>= creationTime + 10 days)
nextStage();
if (stage == Stages.RevealBids &&
block.timestamp>= creationTime + 12 days)
nextStage();
// The other stages transition by transaction
_;
}
```
```
// Order of the modifiers matters here!
functionbid()
public
payable
timedTransitions
atStage(Stages.AcceptingBlindedBids)
{
// We will not implement that here
}
```
```
functionreveal()
public
(continues on next page)
```
**3.35. Common Patterns 389**


```
(continued from previous page)
timedTransitions
atStage(Stages.RevealBids)
{
}
```
```
// This modifier goes to the next stage
// after the function is done.
modifiertransitionNext()
{
_;
nextStage();
}
```
```
functiong()
public
timedTransitions
atStage(Stages.AnotherStage)
transitionNext
{
}
```
```
functionh()
public
timedTransitions
atStage(Stages.AreWeDoneYet)
transitionNext
{
}
```
functioni()
public
timedTransitions
atStage(Stages.Finished)
{
}
}

### 3.36 Resources

**3.36.1 General Resources**

- Ethereum.org Developer Portal
- Ethereum StackExchange
- Solidity Portal
- Solidity Changelog
- Solidity Source Code on GitHub
- Solidity Language Users Chat

**390 Chapter 3. Contents**


- Solidity Compiler Developers Chat
- Awesome Solidity
- Solidity by Example
- Solidity Documentation Community Translations

**3.36.2 Integrated (Ethereum) Development Environments**

- **Brownie**
    Python-based development and testing framework for smart contracts targeting the Ethereum Virtual Ma-
    chine.
- **Dapp**
    Tool for building, testing and deploying smart contracts from the command-line.
- **Foundry**
    Fast, portable and modular toolkit for Ethereum application development written in Rust.
- **Hardhat**
    Ethereum development environment with local Ethereum network, debugging features and plugin ecosys-
    tem.
- **Remix**
    Browser-based IDE with integrated compiler and Solidity runtime environment without server-side com-
    ponents.
- **Truffle**
    Ethereum development framework.

**3.36.3 Editor Integrations**

- Emacs
    **- Emacs Solidity**
       Plugin for the Emacs editor providing syntax highlighting and compilation error reporting.
- IntelliJ
    **- IntelliJ IDEA plugin**
       Solidity plugin for IntelliJ IDEA (and all other JetBrains IDEs).
- Sublime Text
    **- Package for SublimeText - Solidity language syntax**
       Solidity syntax highlighting for SublimeText editor.
- Vim
    **- Vim Solidity by Thesis**
       Syntax highlighting for Solidity in Vim.
    **- Vim Solidity by TovarishFin**
       Vim syntax file for Solidity.
    **- Vim Syntastic**
       Plugin for the Vim editor providing compile checking.
- Visual Studio Code (VS Code)

**3.36. Resources 391**


**- Ethereum Remix Visual Studio Code extension**
    Ethereum Remix extension pack for VS Code
**- Solidity Visual Studio Code extension, by Juan Blanco**
    Solidity plugin for Microsoft Visual Studio Code that includes syntax highlighting and the Solidity
    compiler.
**- Solidity Visual Studio Code extension, by Nomic Foundation**
    Solidity and Hardhat support by the Hardhat team, including: syntax highlighting, jump to definition,
    renames, quick fixes and inline solc warnings and errors.
**- Solidity Visual Auditor extension**
    Adds security centric syntax and semantic highlighting to Visual Studio Code.
**- Truffle for VS Code**
    Build, debug and deploy smart contracts on Ethereum and EVM-compatible blockchains.

**3.36.4 Solidity Tools**

- **ABI to Solidity interface converter**
    A script for generating contract interfaces from the ABI of a smart contract.
- **abi-to-sol**
    Tool to generate Solidity interface source from a given ABI JSON.
- **Doxity**
    Documentation Generator for Solidity.
- **Ethlint**
    Linter to identify and fix style and security issues in Solidity.
- **evmdis**
    EVM Disassembler that performs static analysis on the bytecode to provide a higher level of abstraction
    than raw EVM operations.
- **EVM Lab**
    Rich tool package to interact with the EVM. Includes a VM, Etherchain API, and a trace-viewer with gas
    cost display.
- **hevm**
    EVM debugger and symbolic execution engine.
- **leafleth**
    A documentation generator for Solidity smart-contracts.
- **Scaffold-ETH 2**
    Forkable Ethereum development stack focused on fast product iterations.
- **sol2uml**
    Unified Modeling Language (UML) class diagram generator for Solidity contracts.
- **solc-select**
    A script to quickly switch between Solidity compiler versions.
- **Solidity prettier plugin**
    A Prettier Plugin for Solidity.
- **Solidity REPL**
    Try Solidity instantly with a command-line Solidity console.

**392 Chapter 3. Contents**


- **solgraph**
    Visualize Solidity control flow and highlight potential security vulnerabilities.
- **Solhint**
    Solidity linter that provides security, style guide and best practice rules for smart contract validation.
- **Sourcify**
    Decentralized automated contract verification service and public repository of contract metadata.
- **Surya ̄**
    Utility tool for smart contract systems, offering a number of visual outputs and information about the con-
    tracts’ structure. Also supports querying the function call graph.
- **Universal Mutator**
    A tool for mutation generation, with configurable rules and support for Solidity and Vyper.

**3.36.5 Third-Party Solidity Parsers and Grammars**

- **Solidity Parser for JavaScript**
    A Solidity parser for JS built on top of a robust ANTLR4 grammar.

### 3.37 Contributing

Help is always welcome and there are plenty of options to contribute to Solidity.

In particular, we appreciate support in the following areas:

- Reporting issues.
- Fixing and responding to Solidity’s GitHub issues, especially those tagged as “good first issue” which are meant
    as introductory issues for external contributors.
- Improving the documentation.
- Translating the documentation into more languages.
- Responding to questions from other users on StackExchange and the Solidity Gitter Chat.
- Getting involved in the language design process by proposing language changes or new features in the Solidity
    forum and providing feedback.

To get started, you can try _Building from Source_ in order to familiarize yourself with the components of Solidity and
the build process. Also, it may be useful to become well-versed at writing smart-contracts in Solidity.

Please note that this project is released with a Contributor Code of Conduct. By participating in this project — in the
issues, pull requests, or Gitter channels — you agree to abide by its terms.

**3.37.1 Team Calls**

If you have issues or pull requests to discuss, or are interested in hearing what the team and contributors are working
on, you can join our public team call:

- Wednesdays at 3PM CET/CEST.

The call takes place on Jitsi.

**3.37. Contributing 393**


**3.37.2 How to Report Issues**

To report an issue, please use the GitHub issues tracker. When reporting issues, please mention the following details:

- Solidity version.
- Source code (if applicable).
- Operating system.
- Steps to reproduce the issue.
- Actual vs. expected behavior.

Reducing the source code that caused the issue to a bare minimum is always very helpful, and sometimes even clarifies
a misunderstanding.

For technical discussions about language design, a post in the Solidity forum is the correct place (see _Solidity Language
Design_ ).

**3.37.3 Workflow for Pull Requests**

In order to contribute, please fork off of thedevelopbranch and make your changes there. Your commit messages
should detail _why_ you made your change in addition to _what_ you did (unless it is a tiny change).

If you need to pull in any changes fromdevelopafter making your fork (for example, to resolve potential merge
conflicts), please avoid usinggit mergeand instead,git rebaseyour branch. This will help us review your change
more easily.

Additionally, if you are writing a new feature, please ensure you add appropriate test cases undertest/(see below).

However, if you are making a larger change, please consult with the Solidity Development Gitter channel (different from
the one mentioned above — this one is focused on compiler and language development instead of language usage) first.

New features and bugfixes should be added to theChangelog.mdfile: please follow the style of previous entries, when
applicable.

Finally, please make sure you respect the coding style for this project. Also, even though we do CI testing, please test
your code and ensure that it builds locally before submitting a pull request.

We highly recommend going through our review checklist before submitting the pull request. We thoroughly review
every PR and will help you get it right, but there are many common problems that can be easily avoided, making the
review much smoother.

Thank you for your help!

**3.37.4 Running the Compiler Tests**

**Prerequisites**

For running all compiler tests you may want to optionally install a few dependencies (evmone, libz3, Eldarica, _cvc5
<https://github.com/cvc5/cvc5>_ ).

On macOS systems, some of the testing scripts expect GNU coreutils to be installed. This can be easiest accomplished
using Homebrew:brew install coreutils.

On Windows systems, make sure that you have a privilege to create symlinks, otherwise several tests may fail. Admin-
istrators should have that privilege, but you may also grant it to other users or enable Developer Mode.

**394 Chapter 3. Contents**


**Running the Tests**

Solidity includes different types of tests, most of them bundled into the Boost C++ Test Framework application
soltest. Runningbuild/test/soltestor its wrapperscripts/soltest.shis sufficient for most changes.

The./scripts/tests.shscript executes most Solidity tests automatically, including those bundled into the Boost
C++ Test Framework applicationsoltest(or its wrapperscripts/soltest.sh), as well as command-line tests and
compilation tests.

The test system automatically tries to discover the location of the evmone for running the semantic tests.

Theevmonelibrary must be located in thedepsordeps/libdirectory relative to the current working directory, to its
parent or its parent’s parent. Alternatively, an explicit location for theevmoneshared object can be specified via the
ETH_EVMONEenvironment variable.

evmoneis needed mainly for running semantic and gas tests. If you do not have it installed, you can skip these tests by
passing the--no-semantic-testsflag toscripts/soltest.sh.

Theevmonelibrary should end with the file name extension.soon Linux,.dllon Windows systems and.dylibon
macOS.

For running SMT tests, thelibz3library must be installed and locatable bycmakeduring compiler configure stage. A
few SMT tests useEldaricainstead ofZ3.Eldaricais a runtime dependency, its executable (eld) must be present
inPATHfor the tests to pass. However, ifEldaricais not found, these tests will be automatically skipped.

If the libz3 library is not installed on your system, you should disable the SMT tests by exporting
SMT_FLAGS=--no-smtbefore running./scripts/tests.shor running ./scripts/soltest.sh --no-smt.
These tests arelibsolidity/smtCheckerTests.

**Note:** To get a list of all unit tests run by Soltest, run./build/test/soltest --list_content=HRF.

For quicker results you can run a subset of, or specific tests.

To run a subset of tests, you can use filters:./scripts/soltest.sh -t TestSuite/TestName, whereTestName
can be a wildcard*.

Or, for example, to run all the tests for the yul disambiguator:./scripts/soltest.sh -t "yulOptimizerTests/
disambiguator/*" --no-smt.

./build/test/soltest --helphas extensive help on all of the options available.

See especially:

- show_progress (-p) to show test completion,
- run_test (-t) to run specific tests cases, and
- report-level (-r) give a more detailed report.

**Note:** Those working in a Windows environment wanting to run the above basic sets without libz3. Using Git Bash,
you use:./build/test/Release/soltest.exe -- --no-smt. If you are running this in plain Command Prompt,
use.\build\test\Release\soltest.exe -- --no-smt.

If you want to debug using GDB, make sure you build differently than the “usual”. For example, you could run the
following command in yourbuildfolder:

cmake -DCMAKE_BUILD_TYPE=Debug ..
make

**3.37. Contributing 395**


This creates symbols so that when you debug a test using the--debugflag, you have access to functions and variables
in which you can break or print with.

The CI runs additional tests (includingsolc-jsand testing third party Solidity frameworks) that require compiling
the Emscripten target.

**Writing and Running Syntax Tests**

Syntax tests check that the compiler generates the correct error messages for invalid code and properly accepts valid
code. They are stored in individual files inside thetests/libsolidity/syntaxTestsfolder. These files must
contain annotations, stating the expected result(s) of the respective test. The test suite compiles and checks them
against the given expectations.

For example:./test/libsolidity/syntaxTests/double_stateVariable_declaration.sol

contract test{
uint256variable;
uint128variable;
}
// ----
// DeclarationError: (36-52): Identifier already declared.

A syntax test must contain at least the contract under test itself, followed by the separator// ----. The comments
that follow the separator are used to describe the expected compiler errors or warnings. The number range denotes the
location in the source where the error occurred. If you want the contract to compile without any errors or warning you
can leave out the separator and the comments that follow it.

In the above example, the state variablevariablewas declared twice, which is not allowed. This results in a
DeclarationErrorstating that the identifier was already declared.

Theisoltesttool is used for these tests and you can find it under./build/test/tools/. It is an interactive tool
which allows editing of failing contracts using your preferred text editor. Let’s try to break this test by removing the
second declaration ofvariable:

contract test{
uint256variable;
}
// ----
// DeclarationError: (36-52): Identifier already declared.

Running./build/test/tools/isoltestagain results in a test failure:

syntaxTests/double_stateVariable_declaration.sol: FAIL
Contract:
contract test {
uint256 variable;
}

```
Expected result:
DeclarationError: (36-52): Identifier already declared.
Obtained result:
Success
```
isoltestprints the expected result next to the obtained result, and also provides a way to edit, update or skip the
current contract file, or quit the application.

**396 Chapter 3. Contents**


It offers several options for failing tests:

- edit:isoltesttries to open the contract in an editor so you can adjust it. It either uses the editor given on
    the command-line (asisoltest --editor /path/to/editor), in the environment variableEDITORor just
    /usr/bin/editor(in that order).
- update: Updates the expectations for contract under test. This updates the annotations by removing unmet
    expectations and adding missing expectations. The test is then run again.
- skip: Skips the execution of this particular test.
- quit: Quitsisoltest.

All of these options apply to the current contract, exceptquitwhich stops the entire testing process.

Automatically updating the test above changes it to

contract test{
uint256variable;
}
// ----

and re-run the test. It now passes again:

Re-running test case...
syntaxTests/double_stateVariable_declaration.sol: OK

**Note:** Choose a name for the contract file that explains what it tests, e.g.double_variable_declaration.sol.
Do not put more than one contract into a single file, unless you are testing inheritance or cross-contract calls. Each file
should test one aspect of your new feature.

**Command-line Tests**

Our suite of end-to-end command-line tests checks the behaviour of the compiler binary as a whole in various scenarios.
These tests are located in test/cmdlineTests/, one per subdirectory, and can be executed using thecmdlineTests.sh
script.

By default the script runs all available tests. You can also provide one or more file name patterns, in which case only
the tests matching at least one pattern will be executed. It is also possible to exclude files matching a specific pattern
by prefixing it with--exclude.

By default the script assumes that asolcbinary is available inside thebuild/subdirectory inside the working copy.
If you build the compiler outside of the source tree, you can use theSOLIDITY_BUILD_DIRenvironment variable to
specify a different location for the build directory.

Example:

export SOLIDITY_BUILD_DIR=~/solidity/build/
test/cmdlineTests.sh "standard_*" "*_yul_*" --exclude "standard_yul_*"

The commands above will run tests from directories starting withtest/cmdlineTests/standard_and subdi-
rectories oftest/cmdlineTests/that have_yul_somewhere in the name, but no test whose name starts with
standard_yul_will be executed. It will also assume that the filesolidity/build/solc/solcinside your home
directory is the compiler binary (unless you are on Windows – thensolidity/build/solc/Release/solc.exe).

There are several kinds of command-line tests:

**3.37. Contributing 397**


- _Standard JSON test_ : contains at least aninput.jsonfile. In general may contain:
    **-** input.json: input file to be passed to the--standard-jsonoption on the command line.
    **-** output.json: expected Standard JSON output.
    **-** args: extra command-line arguments passed tosolc.
- _CLI test_ : contains at least aninput.*file (other thaninput.json). In general may contain:
    **-** input.*: a single input file, whose name will be supplied tosolcon the command line. Usuallyinput.
       solorinput.yul.
    **-** args: extra command-line arguments passed tosolc.
    **-** stdin: content to be passed tosolcvia standard input.
    **-** output: expected content of the standard output.
    **-** err: expected content of the standard error output.
    **-** exit: expected exit code. If not provided, zero is expected.
- _Script test_ : contains atest.*file. In general may contain:
    **-** test.*: a single script to run, usuallytest.shortest.py. The script must be executable.

**3.37.5 Running the Fuzzer via AFL**

Fuzzing is a technique that runs programs on more or less random inputs to find exceptional execution states (seg-
mentation faults, exceptions, etc). Modern fuzzers are clever and run a directed search inside the input. We have a
specialized binary calledsolfuzzerwhich takes source code as input and fails whenever it encounters an internal
compiler error, segmentation fault or similar, but does not fail if e.g., the code contains an error. This way, fuzzing
tools can find internal problems in the compiler.

We mainly use AFL for fuzzing. You need to download and install the AFL packages from your repositories (afl,
afl-clang) or build them manually. Next, build Solidity (or just thesolfuzzerbinary) with AFL as your compiler:

cd build
# if needed
make clean
cmake .. -DCMAKE_C_COMPILER=path/to/afl-gcc -DCMAKE_CXX_COMPILER=path/to/afl-g++
make solfuzzer

At this stage, you should be able to see a message similar to the following:

Scanning dependencies of target solfuzzer
[ 98%] Building CXX object test/tools/CMakeFiles/solfuzzer.dir/fuzzer.cpp.o
afl-cc 2.52b by <lcamtuf@google.com>
afl-as 2.52b by <lcamtuf@google.com>
[+] Instrumented 1949 locations (64-bit, non-hardened mode, ratio 100%).
[100%] Linking CXX executable solfuzzer

If the instrumentation messages did not appear, try switching the cmake flags pointing to AFL’s clang binaries:

# if previously failed
make clean
cmake .. -DCMAKE_C_COMPILER=path/to/afl-clang -DCMAKE_CXX_COMPILER=path/to/afl-clang++
make solfuzzer

**398 Chapter 3. Contents**


Otherwise, upon execution the fuzzer halts with an error saying binary is not instrumented:

afl-fuzz 2.52b by <lcamtuf@google.com>
... (truncated messages)
[*] Validating target binary...

[-] Looks like the target binary is not instrumented! The fuzzer depends on
compile-time instrumentation to isolate interesting test cases while
mutating the input data. For more information, and for tips on how to
instrument binaries, please see /usr/share/doc/afl-doc/docs/README.

```
When source code is not available, you may be able to leverage QEMU
mode support. Consult the README for tips on how to enable this.
(It is also possible to use afl-fuzz as a traditional, "dumb" fuzzer.
For that, you can use the -n option - but expect much worse results.)
```
[-] PROGRAM ABORT : No instrumentation detected
Location : check_binary(), afl-fuzz.c:6920

Next, you need some example source files. This makes it much easier for the fuzzer to find errors. You can either copy
some files from the syntax tests or extract test files from the documentation or the other tests:

mkdir /tmp/test_cases
cd /tmp/test_cases
# extract from tests:
path/to/solidity/scripts/isolate_tests.py path/to/solidity/test/libsolidity/
˓→SolidityEndToEndTest.cpp
# extract from documentation:
path/to/solidity/scripts/isolate_tests.py path/to/solidity/docs

The AFL documentation states that the corpus (the initial input files) should not be too large. The files themselves
should not be larger than 1 kB and there should be at most one input file per functionality, so better start with a small
number of. There is also a tool calledafl-cminthat can trim input files that result in similar behavior of the binary.

Now run the fuzzer (the-mextends the size of memory to 60 MB):

afl-fuzz -m 60 -i /tmp/test_cases -o /tmp/fuzzer_reports -- /path/to/solfuzzer

The fuzzer creates source files that lead to failures in/tmp/fuzzer_reports. Often it finds many similar source files
that produce the same error. You can use the toolscripts/uniqueErrors.shto filter out the unique errors.

**3.37.6 Whiskers**

_Whiskers_ is a string templating system similar to Mustache. It is used by the compiler in various places to aid readability,
and thus maintainability and verifiability, of the code.

The syntax comes with a substantial difference to Mustache. The template markers{{and}}are replaced by<and>
in order to aid parsing and avoid conflicts with _Yul_ (The symbols<and>are invalid in inline assembly, while{and}
are used to delimit blocks). Another limitation is that lists are only resolved one depth and they do not recurse. This
may change in the future.

A rough specification is the following:

Any occurrence of<name>is replaced by the string-value of the supplied variablenamewithout any escaping and
without iterated replacements. An area can be delimited by<#name>...</name>. It is replaced by as many concate-

**3.37. Contributing 399**


nations of its contents as there were sets of variables supplied to the template system, each time replacing any<inner>
items by their respective value. Top-level variables can also be used inside such areas.

There are also conditionals of the form<?name>...<!name>...</name>, where template replacements continue
recursively either in the first or the second segment depending on the value of the boolean parametername. If<?
+name>...<!+name>...</+name>is used, then the check is whether the string parameternameis non-empty.

**3.37.7 Documentation Style Guide**

In the following section you find style recommendations specifically focusing on documentation contributions to So-
lidity.

**English Language**

Use International English, unless using project or brand names. Try to reduce the usage of local slang and references,
making your language as clear to all readers as possible. Below are some references to help:

- Simplified technical English
- International English

**Note:** While the official Solidity documentation is written in English, there are community contributed _Translations_ in
other languages available. Please refer to the translation guide for information on how to contribute to the community
translations.

**Title Case for Headings**

Use title case for headings. This means capitalise all principal words in titles, but not articles, conjunctions, and
prepositions unless they start the title.

For example, the following are all correct:

- Title Case for Headings.
- For Headings Use Title Case.
- Local and State Variable Names.
- Order of Layout.

**Expand Contractions**

Use expanded contractions for words, for example:

- “Do not” instead of “Don’t”.
- “Can not” instead of “Can’t”.

**400 Chapter 3. Contents**


**Active and Passive Voice**

Active voice is typically recommended for tutorial style documentation as it helps the reader understand who or what
is performing a task. However, as the Solidity documentation is a mixture of tutorials and reference content, passive
voice is sometimes more applicable.

As a summary:

- Use passive voice for technical reference, for example language definition and internals of the Ethereum VM.
- Use active voice when describing recommendations on how to apply an aspect of Solidity.

For example, the below is in passive voice as it specifies an aspect of Solidity:

```
Functions can be declaredpurein which case they promise not to read from or modify the state.
```
For example, the below is in active voice as it discusses an application of Solidity:

```
When invoking the compiler, you can specify how to discover the first element of a path, and also path
prefix remappings.
```
**Common Terms**

- “Function parameters” and “return variables”, not input and output parameters.

**Code Examples**

A CI process tests all code block formatted code examples that begin withpragma solidity,contract,libraryor
interfaceusing the./test/cmdlineTests.shscript when you create a PR. If you are adding new code examples,
ensure they work and pass tests before creating the PR.

Ensure that all code examples begin with apragmaversion that spans the largest where the contract code is valid. For
examplepragma solidity >=0.4.0 <0.9.0;.

**Running Documentation Tests**

Make sure your contributions pass our documentation tests by running./docs/docs.shthat installs dependencies
needed for documentation and checks for any problems such as broken links or syntax issues.

**3.37.8 Solidity Language Design**

To actively get involved in the language design process and to share your ideas concerning the future of Solidity, please
join the Solidity forum.

The Solidity forum serves as the place to propose and discuss new language features and their implementation in the
early stages of ideation or modifications of existing features.

As soon as proposals get more tangible, their implementation will also be discussed in the Solidity GitHub repository
in the form of issues.

In addition to the forum and issue discussions, we regularly host language design discussion calls in which selected
topics, issues or feature implementations are debated in detail. The invitation to those calls is shared via the forum.

We are also sharing feedback surveys and other content that is relevant to language design in the forum.

If you want to know where the team is standing in terms or implementing new features, you can follow the implemen-
tation status in the Solidity GitHub project. Issues in the design backlog need further specification and will either be

**3.37. Contributing 401**


discussed in a language design call or in a regular team call. You can see the upcoming changes for the next breaking
release by changing from the default branch ( _develop_ ) to the breaking branch.

For ad-hoc cases and questions, you can reach out to us via the Solidity-dev Gitter channel — a dedicated chatroom for
conversations around the Solidity compiler and language development.

We are happy to hear your thoughts on how we can improve the language design process to be even more collaborative
and transparent.

### 3.38 Language Influences

Solidity is a curly-bracket language that has been influenced and inspired by several well-known programming lan-
guages.

Solidity is most profoundly influenced by C++, but also borrowed concepts from languages like Python, JavaScript,
and others.

The influence from C++ can be seen in the syntax for variable declarations, for loops, the concept of overloading
functions, implicit and explicit type conversions and many other details.

In the early days of the language, Solidity used to be partly influenced by JavaScript. This was due to function-level
scoping of variables and the use of the keywordvar. The JavaScript influence was reduced starting from version
0.4.0. Now, the main remaining similarity to JavaScript is that functions are defined using the keywordfunction.
Solidity also supports import syntax and semantics that are similar to those available in JavaScript. Besides those
points, Solidity looks like most other curly-bracket languages and has no major JavaScript influence anymore.

Another influence to Solidity was Python. Solidity’s modifiers were added trying to model Python’s decorators with
a much more restricted functionality. Furthermore, multiple inheritance, C3 linearization, and thesuperkeyword are
taken from Python as well as the general assignment and copy semantics of value and reference types.

### 3.39 Solidity Brand Guide

This brand guide features information on Solidity’s brand policy and logo usage guidelines.

**3.39.1 The Solidity Brand**

The Solidity programming language is an open-source, community project governed by a core team. The core team is
sponsored by the Ethereum Foundation.

This document aims to provide information about how to best use the Solidity brand name and logo.

We encourage you to read this document carefully before using the brand name or the logo. Your cooperation is highly
appreciated!

**402 Chapter 3. Contents**


**3.39.2 Solidity Brand Name**

“Solidity” should be used to refer to the Solidity programming language solely.

Please do not use “Solidity”:

- To refer to any other programming language.
- In a way that is misleading or may imply association of unrelated modules, tools, documentation, or other re-
    sources with the Solidity programming language.
- In ways that confuse the community as to whether the Solidity programming language is open-source and free
    to use.

**3.39.3 Solidity Logo License**

The Solidity logo is distributed and licensed under a Creative Commons Attribution 4.0 International License.

This is the most permissive Creative Commons license and allows reuse and modifications for any purpose.

You are free to:

- **Share** — Copy and redistribute the material in any medium or format.
- **Adapt** — Remix, transform, and build upon the material for any purpose, even commercially.

Under the following terms:

- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made.
    You may do so in any reasonable manner, but not in any way that suggests that the Solidity core team endorses
    you or your use.

When using the Solidity logo, please respect the Solidity logo guidelines.

**3.39.4 Solidity Logo Guidelines**

_(Right click on the logo to download it.)_

**3.39. Solidity Brand Guide 403**


Please do not:

- Change the ratio of the logo (do not stretch it or cut it).
- Change the colors of the logo, unless it is absolutely necessary.

**3.39.5 Credits**

This document was, in parts, derived from the Python Software Foundation Trademark Usage Policy and the Rust
Media Guide.

**404 Chapter 3. Contents**


## Index

### Symbols

--allow-paths, 191, **358**
--base-path, 191, 192, **357**
--include-path, 191, **357**
--libraries, **191**
--link, **191**
--no-import-callback, **353**
--standard-json, 192, **194**
<stdin>, 355

### A

abi, 91, 93, 250
decode, 161
encode, 161
encodeCall, 161
encodePacked, 161
encodeWithSelector, 161
encodeWithSignature, 161
ABI coder, **48**
abstract contract, 141, **144**
access
restricting, 386
account, **12**
addmod, 94, 163
address, 12, 57, 61
balance, 162
code, 162
codehash, 162
send, 162
transfer, 162
allowed paths, 191, **358**
analyse, 205
anonymous, 164
application binary interface, 250
array, 69, **70** , 122
allocating, **72**
dangling storage references, **76**
length, **74**
pop, **74**
push, **74**
slice, **78**
array of strings, 122

```
asm, 154 , 205, 331
assembly, 154 , 331
assembly-flags( Antlr4 production rule ), 179
assembly-statement( Antlr4 production rule ), 179
assert, 94, 106 , 163
assignment, 86, 102
destructuring, 102
auction
blind, 19
open, 19
```
### B

```
balance, 12, 57, 95
ballot, 15
base
constructor, 141
base class, 134
base path, 191, 357
blind auction, 19
blobhash, 162
block, 11 , 91, 162
basefee, 91, 162
blobbasefee, 91, 162
chainid, 162
coinbase, 162
difficulty, 162
gaslimit, 162
number, 91, 162
prevrandao, 162
timestamp, 91, 162
block( Antlr4 production rule ), 177
blockhash, 162
bool, 54
boolean-literal( Antlr4 production rule ), 176
break, 98
break-statement( Antlr4 production rule ), 178
Bugs, 272
byte array, 60
bytes, 63, 71
concat, 161
bytes members, 93
bytes32, 60
```
#### 405


bytes-concat, **71**

### C

C3 linearization, **142**
call, 57, 95
call-argument-list( _Antlr4 production rule_ ), 167
callcode, 95, 146
cast, **88**
catch-clause( _Antlr4 production rule_ ), 178
checked, 105
cleanup, 213
codehash, 95
coding style, 362
coin, 10
coinbase, 91
commandline compiler, **190**
comment, **50**
common subexpression elimination, 223
compile target, 192
compiler
commandline, 190
compound operators, **86**
constant, **119** , 164
constant propagation, 223
constant-variable-declaration( _Antlr4 production
rule_ ), 171
constructor, 112, **141**
arguments, 112
constructor-definition ( _Antlr4 production rule_ ),
168
continue, 98
continue-statement( _Antlr4 production rule_ ), 178
contract, 50, **111**
abstract, 141, **144**
base, **134**
creation, **112**
interface, **145**
modular, 37
precompiled, **15**
contract creation, 14
contract type, **60**
contract verification, 245
contract-body-element( _Antlr4 production rule_ ), 166
contract-definition( _Antlr4 production rule_ ), 165
contracts
creating, 100
creationCode, 97
cryptography, 94, 163
custom type, 64

### D

data, 91
data-location( _Antlr4 production rule_ ), 173
days, **91**

```
deactivate, 14
decimal-number( Antlr4 production rule ), 188
declarations, 104
default value, 104
delegatecall, 14, 57, 95, 146
delete, 86
denomination, 90
ether, 90
time, 91
deriving, 134
difficulty, 91
direct import, 355
dirty bits, 213
do/while, 98
do-while-statement( Antlr4 production rule ), 178
double-quoted-printable( Antlr4 production rule ),
187
dynamic array, 122
```
### E

```
ecrecover, 94, 163
elementary-type-name( Antlr4 production rule ), 173
else, 98
emit-statement( Antlr4 production rule ), 179
empty-string-literal( Antlr4 production rule ), 187
encode, 91
encoding, 93
enum, 50, 63
enum-definition( Antlr4 production rule ), 170
error, 132 , 259
error-definition( Antlr4 production rule ), 171
error-parameter( Antlr4 production rule ), 171
errors, 106
escape-sequence( Antlr4 production rule ), 187
escrow, 25
ether, 90
ethereum virtual machine, 11
evaluation order
expression, 211
function arguments, 211
event, 9, 50, 130
anonymous, 130
indexed, 130
topic, 130
event-definition( Antlr4 production rule ), 171
event-parameter( Antlr4 production rule ), 171
evm, 11
EVM version, 192
evmasm, 154 , 331
exception, 106
expression( Antlr4 production rule ), 173
expression-statement( Antlr4 production rule ), 180
external, 114, 164
```
**406 Index**


### F

fallback function, **127**
fallback-function-definition ( _Antlr4 production
rule_ ), 169
false, **54**
file://, 362
filesystem path, 49
finney, **90**
fixed, **56**
fixed point number, **56**
fixed-bytes( _Antlr4 production rule_ ), 182
for, 98
for-statement( _Antlr4 production rule_ ), 178
function, 50
call, 13, **98**
external, 98
fallback, 127
free, **121** , 151
getter, **115**
internal, 98
modifier, 50, **117** , 386, 388
pure, 125
receive, 126
view, 124
function parameter, 98
function pointers, 212
function type, **65**
function-definition( _Antlr4 production rule_ ), 168
function-type-name( _Antlr4 production rule_ ), 173
functions, **121**

### G

gas, **12** , 91
gas price, **12** , 91
gasleft, 162
getter
function, **115**
goto, 98
gwei, **90**

### H

hex-number( _Antlr4 production rule_ ), 188
hex-string( _Antlr4 production rule_ ), 187
hex-string-literal( _Antlr4 production rule_ ), 176
Host Filesystem Loader, **353**
hours, **91**

### I

identifier( _Antlr4 production rule_ ), 176, 188
identifier-path( _Antlr4 production rule_ ), 167
if, 98
if-statement( _Antlr4 production rule_ ), 177
import, **49**

```
direct, 355
path, 49, 355
relative, 356
remapping, 359
import callback, 49, 353
import-directive( Antlr4 production rule ), 165
include paths, 191, 357
indexed, 164
inheritance, 134
multiple, 142
inheritance list, 141
inheritance-specifier( Antlr4 production rule ), 166
inline
arrays, 72
inline-array-expression( Antlr4 production rule ),
176
installing, 38
instruction, 13
int, 54
integer, 54 , 61
interface contract, 145
interface-definition( Antlr4 production rule ), 166
internal, 114, 164
iterable mappings, 83
iulia, 331
```
### J

```
julia, 331
```
### K

```
keccak256, 94, 163
```
### L

```
length, 74
library, 14, 146 , 151
library-definition( Antlr4 production rule ), 166
license, 47
linearization, 142
linker, 191
literal
address, 61 , 90
array, 72
conversion, 89
hexadecimal, 63 , 90
hexadecimal number, 89
in Yul, 333
rational, 61 , 89
string, 62 , 90
unicode, 63
literal( Antlr4 production rule ), 176
literal-with-sub-denomination( Antlr4 production
rule ), 176
location, 69
log, 14
```
**Index 407**


lvalue, 86

### M

mapping, 9, **81** , 213
mapping-key-type( _Antlr4 production rule_ ), 180
mapping-type( _Antlr4 production rule_ ), 180
memory, **13** , 69
message call, **13**
metadata, 245
minutes, **91**
modifier-definition( _Antlr4 production rule_ ), 169
modifier-invocation( _Antlr4 production rule_ ), 167
modifiers, 164
modular contract, 37
module, 49
msg, 91
data, 162
sender, 162
sig, 162
value, 162
mulmod, 94, 163

### N

natspec, 50
new, 72, **100**
non-empty-string-literal( _Antlr4 production rule_ ),
186
number, 91
number-literal( _Antlr4 production rule_ ), 177

### O

open auction, 19
operator, **85**
precedence, **87** , 160
user-defined, **151**
optimiser, 223
optimizer, 223
origin, 91
overload, **129**
override-specifier( _Antlr4 production rule_ ), 168
overriding
function, **138**
modifier, **140**

### P

packed, 93
parameter, **98**
function, 98
input, 98
output, 98
parameter-list( _Antlr4 production rule_ ), 167
path( _Antlr4 production rule_ ), 165
payable, 164

```
pop, 74
pragma, 47
abicoder, 48
ABIEncoderV2, 48 , 48
experimental, 48
SMTChecker, 48
version, 47
pragma-token( Antlr4 production rule ), 190
precompiled contracts, 15
precompiles, 15
prevrandao, 91
private, 114, 164
public, 114, 164
purchase, 25
pure, 164
pure function, 125
push, 74
```
### R

```
rational number, 61
receive, 126
receive ether function, 126
receive-function-definition ( Antlr4 production
rule ), 169
reference type, 69
relative import, 356
remapping
context, 359
import, 359
prefix, 359
target, 358, 359
Remix IDE, 49, 362
remote purchase, 25
require, 94, 106 , 132, 163
return, 98
return array, 122
return string, 122
return struct, 122
return variable, 98
return-statement( Antlr4 production rule ), 179
revert, 94, 106 , 132, 163
revert-statement( Antlr4 production rule ), 179
ripemd160, 94, 163
runtimeCode, 97
```
### S

```
safe math, 105
safemath, 105
scoping, 104
seconds, 91
selector
of a function, 156, 250
of a library function, 149
of an error, 132 , 259
```
**408 Index**


of an event, **131**
selfdestruct, **14** , 96, 163
send, 57, 95
sender, 91
set, 146
sha256, 94, 163
signed-integer-type( _Antlr4 production rule_ ), 184
single-quoted-printable( _Antlr4 production rule_ ),
187
solc, **190**
SolidityLexer( _Antlr4 lexer grammar_ ), 182
SolidityParser( _Antlr4 parser grammar_ ), 165
source file, 49
source mappings, 222
source unit, 49
source unit name, 49, **353**
source-unit( _Antlr4 production rule_ ), 165
spdx, 47
stack, **13**
standard input, 355
standard JSON, **194** , 354
state machine, 388
state variable, 50, 213
state-mutability( _Antlr4 production rule_ ), 168
state-variable-declaration ( _Antlr4 production
rule_ ), 170
statement( _Antlr4 production rule_ ), 177
staticcall, 57, 95
stdin, 355
storage, 12, **13** , 69, 213
string, 62, **71** , 122
concat, 161
string members, 94
string-concat, **71**
string-literal( _Antlr4 production rule_ ), 176
struct, 50, 69, **79** , 122
struct-definition( _Antlr4 production rule_ ), 170
struct-member( _Antlr4 production rule_ ), 170
style, 362
sub-denomination( _Antlr4 production rule_ ), 183
subcurrency, **8**
super, 96, 163
switch, 98
symbol-aliases( _Antlr4 production rule_ ), 165
szabo, **90**

### T

this, 96, 163
throw, **106**
timestamp, 91
transaction, 11, **12**
transfer, 57, 95
transient storage, 213
true, **54**

```
try-statement( Antlr4 production rule ), 178
tuple-expression( Antlr4 production rule ), 176
tx
gasprice, 162
origin, 162
type, 53, 97
contract, 60
conversion, 88
creationCode, 163
function, 65
interfaceId, 163
max, 163
min, 163
name, 163
reference, 69
runtimeCode, 163
struct, 79
value, 53
type-name( Antlr4 production rule ), 172
```
### U

```
ufixed, 56
uint, 54
unchecked, 105
unchecked-block( Antlr4 production rule ), 177
unicode-string-literal ( Antlr4 production rule ),
177, 187
unsigned-integer-type( Antlr4 production rule ), 185
UnusedStoreEliminator, 240
user defined value type, 64
user-definable-operator( Antlr4 production rule ),
171
user-defined-value-type-definition( Antlr4 pro-
duction rule ), 170
using for, 146, 151
using-aliases( Antlr4 production rule ), 172
using-directive( Antlr4 production rule ), 172
```
### V

```
value, 91
value type, 53
variable
return, 98
variable-declaration( Antlr4 production rule ), 173
variable-declaration-statement ( Antlr4 produc-
tion rule ), 179
variable-declaration-tuple ( Antlr4 production
rule ), 179
variably sized array, 122
VFS, 353
view, 164
view function, 124
virtual filesystem, 49, 353
visibility, 114 , 164
```
**Index 409**


visibility( _Antlr4 production rule_ ), 167
voting, 15

### W

weeks, **91**
wei, **90**
while, 98
while-statement( _Antlr4 production rule_ ), 178
withdrawal, 384

### Y

years, **91**
yul, **331**
yul-assignment( _Antlr4 production rule_ ), 181
yul-block( _Antlr4 production rule_ ), 180
yul-boolean( _Antlr4 production rule_ ), 182
yul-decimal-number( _Antlr4 production rule_ ), 190
yul-evm-builtin( _Antlr4 production rule_ ), 188
yul-expression( _Antlr4 production rule_ ), 182
yul-for-statement( _Antlr4 production rule_ ), 181
yul-function-call( _Antlr4 production rule_ ), 182
yul-function-definition( _Antlr4 production rule_ ),
181
yul-hex-number( _Antlr4 production rule_ ), 190
yul-identifier( _Antlr4 production rule_ ), 190
yul-if-statement( _Antlr4 production rule_ ), 181
yul-literal( _Antlr4 production rule_ ), 182
yul-path( _Antlr4 production rule_ ), 181
yul-statement( _Antlr4 production rule_ ), 180
yul-string-literal( _Antlr4 production rule_ ), 190
yul-switch-statement( _Antlr4 production rule_ ), 181
yul-variable-declaration( _Antlr4 production rule_ ),
180

**410 Index**



