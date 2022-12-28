# TON Fingerprint service an audit of a The Open Network smart contract

* Fast | less than 24 hours
* Affordable | from 1 000 000 [Donation](https://tonscan.org/jetton/EQDEcJlTPBymzUqOJ15QR44vIlPIHhsWllrIafWpPdeHiuNR) ~ 100 TON
* Quality | 3.5+ years of experience in TON

# What is the TON
TON or The Open Network is a layer-1 blockchain developed by Telegram. The developers state that the network is fully decentralized, ultra-fast, cheap, and environmentally friendly.

TON is a relatively new blockchain that brings certain changes to the established paradigm. While Making speed and efficiency its priorities, TON does consider its environmental impact.
This approach attracts crypto developers as well as users to the blockchain.

## Lively Ecosystem
An actively developing TON ecosystem includes wallets, TON with staking possibility, apps, bridges to other blockchains and so much more.

## Active Сommunity
An ecosystem of communities, publishers, and businesses opened to hundreds of experts and winners of Telegram contests from all over the world.

## Future Plans
Not only the blockchain is actively growing, but its future plans include multiple features and additions to the chain.

# Why is an audit important for TON projects?
Choosing TON blockchain opens up a lot of doors for developers. Among them, is access to a loyal audience. With that, comes the responsibility to deliver the best dApps and services, and protect project owners as well as the users of the TON blockchain. TON security audits can help maintain security in the network.

1. Developing Chain

    With the speedy popularization and attention TON is getting, more and more developers turn to this blockchain, building many new projects that may require security analysis.

2. Complex Languages

    TON uses С++ as well as FunC languages. Compared to Solidity, they are more complex and require a more careful approach in order to avoid errors that may lead to a contract malfunction.

3. Vulnerabilities

    Aside from risks from malicious members within developer teams, new projects have to be protected from external attacks.

[TON Figerprints](https://github.com/mir-one/fingerprints) provides smart contract audits for TON projects, relying on its experience in С++ and FunC.

Working with TON, you will interact with two programming languages: Func and Fift. Func is a C-like language developed for writing smart contracts. Although it might look a bit confusing, once you get used to it, the language makes sense and in fact, seems quite comprehensive. Fift is a stack-based language that serves as a language of interaction with TON. It contains TVM and Fift assembly instructions that TON "understands".

Both languages are relatively new, which results in multiple potential errors, especially from newby developers. Here’s a checklist for TON.

1. Name collisions
    
    Func variables and functions may contain almost any legit character. I.e. var++, ~bits, foo-bar+baz including commas are valid variables' and functions' names.

    When writing and inspecting a Func code, Linter should be used

2. Check the throw values

    Each time the TVM execution stops normally, it stops with exit codes 0 or 1. Although it is done automatically, TVM execution can be interrupted directly in an unexpected way if exit codes 0 and 1 are thrown directly by either throw(0) or throw(1) command.

3. Func is a strictly typed language with data structures holding exactly what they are supposed to store

    It is crucial to keep track of what the code does and what it may return. Keep in mind that the compiler cares only about the code and only in its initial state. After certain operations stored values of some variables can change.

    Reading unexpected variables' values and calling methods on data types that are not supposed to have such methods (or their return values are not stored properly) are errors and are not skipped as "warnings" or "notices" but lead to unreachable code. Keep in mind that storing an unexpected value may be okay, however, reading it may cause problems e.g. error code 5 (integer out of expected range) may be thrown for an integer variable.

4. You should have a notion about Fift and TVM assembly instructions

    Func functions are frequently built with direct Fift "asm" directives. The auditor must know what they do and observe keenly what the stack contains.

5. Unlike other blockchains, TON does not contain revert messages, only exit codes

    It is helpful to think through the roadmap of exit codes for the code flow (and have it documented) before starting programming your TON smart contract.

6. Messages have modes

    (a collection of flags represented as a single number), one of them may serve as self-destruct and one serves to send all remaining coins on balance. It is essential for the TON blockchain auditor to check the message mode.

7. TON fully implements the actor model

    It means the code of the contract can be changed. It can either be changed permanently, using SETCODE TVM directive, or in runtime, setting the TVM code registry to a new cell value until the end of execution.

8. TON Blockchain has several transaction phases: computational phase, actions phase, and a bounce phase among them

    The computational phase executes the code of smart contracts and only then the actions are performed (sending messages, code modification, changing libraries, and others). So, unlike on Ethereum-based blockchains, you won't see the computational phase exit code if you expected the sent message to fail, as it was performed not in the computational phase, but later, during the action phase

9. Func functions that have medhod_id identifiers have method IDs

    They can be either set explicitly "method_id(5)", or implicitly by a func compiler. In this case, they can be found among methods declarations in the .fift assembly file. Two of them are predefined: one for receiving messages inside of blockchain (0), commonly named recv_internal, and one for receiving messages from outside (-1), recv_external.

10. TON Crypto address may not have any coins or code

    Smart contracts' addresses in TON blockchain are deterministic and can be precomputed. Ton Accounts, associated with addresses may even contain no code which means they are uninitialized (if not deployed) or frozen while having no more storage or TON coins if the message with special flags was sent.

11. TON addresses may have three representations

    A full representation can either be "raw" (workchain:address) or "user-friendly". The last one is the one users encounter most often. It contains a tag byte, indicating whether the address is bounceable or not bounceable, and a workchain id byte. This information should be noted.

12. Keep track of the flaws in code execution

    Unlike Solidity where it's up to you to set methods visibility, in the case of Func, the visibility is restricted in a more intricate way either by showing errors or by "if" statements.

13. Keep an eye on gas before sending bounced messages

    In case the smart contract sends the bounced messages with the value, provided by a user, make sure that the corresponding gas fees are subtracted from the returned amount not to be drained.

14. Monitor the callbacks and their failures

    TON blockchain is asynchronous. That means the messages do not have to arrive successively. e.g. when a fail notification of an action arrives, it should be handled properly.

15. Check if the bounced flag was sent receiving internal messages

    You may receive bounced messages (error notifications), which should be handled.

16. Write replay protection for external messages:

    there are two custom solutions for wallets (smart contracts, storing users' money): seqno-based (check the counter not to process message twice) and high-load(storing processes' identifiers and its expirations).

TON might seem like a complicated chain to an unprepared auditor or developer, but knowing what to expect gives you a clear advantage. The 16 tips above can make a huge difference for any smart contract deployed to TON.

# How Does It Work

## CONTACT
Send us the specification of the code by e-mail: dao@mir.one

## PRICE
We agree on the price and the deadline

## AUDIT
We start the auditing process

## PRELIMINARY REPORT
We privately send the preliminary report to your team

## FIXES
Your team fixes the issues

## FINAL REPORT
We examine your fixes, update, share and publish (optional) the final report.
