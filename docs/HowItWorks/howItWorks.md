---
id: howItWorks
title: How Cross Chain Works
description: How cross chain works
sidebar_label: How Cross Chain Works
---

Some Background
---------------

The distributed key algorithm used by Multichain was derived from the ground breaking work of Steven Goldfeder (Offchain Labs, Cornell Tech) and Rosario Gennero (City College, CUNY). Their paper of 2019, referred to as GG19, has been implemented in new code by Multichain and continuously improved.

The use of a single signature to send assets, or interact with smart contracts cross chain, results in a single point of failure. This Externally Owned Address can be compromised with poor key custody. One approach has been to use Multi Signature Wallets, so that several signatures are required to make a transaction. The problems here are :-

(a) These keys are still Externally Owned Addresses, 

(b) The signers have to be pre-defined and this is inflexible, 

(c) The signing addresses are public, so that the access structure is known to everyone and 

(d) The data for signing is large, possibly requiring many keys.

The solution is to use Threshold Signature Schemes (TSS), splitting the key up. From *n* possible signatories, a minimum of any *t+1* signatories can sign a transaction. No t colluding players can forge the signature. This has these advantages :-

(a) It is private so that no one knows which *t+1* signers were used, 

(b) If there are many possible signatories, then well performing ones can be chosen, 

(c) It is efficient since only a single signature goes on the chain, looking like a regular signature.


Multichain's SMPC Network
-------------------------

At the heart of Multichain is its Secure Multi Party Computation (SMPC) [Multichain network of nodes](https://anyswap.net), which uses a TSS Distributed Key Generation algorithm. This code has been completely and freshly written by Multichain's engineers and is optimised for multichain applications. Each node in a set, selected from the network, works independently from the others to generate part of the private key responsible for signing transactions. They collectively sign transactions, but crucially they cannot individually do so and the key is not reconstructed when signing.

This is accomplished by several rounds of communication between the t+1 nodes. If one sends a bad message, then it is important that this node can be recognised, or else there is the possibility of a Dedicated Denial of Service Attack. GG19 solves this using an elegant property of the ECDSA algorithm, so that the part of the signature from a node can be used to query whether it was at fault (the 'bad actor'). Other features present in GG19 that increase efficiency are the ability to have Asynchronous Approval, where a large number of signatures can be pre-computed before thay are needed, with only the final round of communication necessary to actually sign the message. This also means that there is no longer the need for all nodes to be online simulataneously with the implication that some network latency can be accommodated.

The SMPC network is responsible for signing transactions on each supported blockchain to perform a multitude of tasks comprising the management of asset accounts and smart contracts. A Threshold, will be needed to sign the transaction. This Threshold Signature (TSS) is denoted 15/9, 21/15, 31/21 etc., where the first number is the total number of nodes in the set *n*, and the second is the number of them needed to sign, t+1.

The nodes are run by different organisations, institutions and individuals, which independently run Multichain's protocol. The end result is a decentralized and trustless service. Multichains's code is completely open source, which is a pre-requisite of any system that describes itself as being decentralized. There is an inevitable tradeoff between security and performance as the total number nodes and the threshold are changed. For the security of the system to be broken, *t+1* TSS nodes would have to collude to assemble the private key, but as *t* increases, this eventuality becomes vanishingly rare and this has not happened despite the length of time the network has been running and the huge TVL and daily volume that exists today on Multichain's network. Another possible security flaw rests on each blockchain itself. It is necessary to wait for a sufficient number of confirmations before finality can be agreed upon and so that any short lived forks cannot result in a double spend. These are the issues that ultimately limit the potential speed of cross chain transactions.

As mentioned in the Introduction, the SMPC network is currently used for a number of functions:- 



The Multichain Bridges
----------------------

![Bridge Schematic](/img/Bridge-schematic.jpg)

Each Bridge is a link between two block chains. On the asset origin chain, the asset to be bridged is sent to a special SMPC wallet address and held securely there. This is the Decentralized Custody Management Account. On the destination chain, a smart contract mints tokens 1:1 with those held in Custody Management Account and sends them to the user's wallet. The opposite also happens when tokens are sent to the smart contract; they are burned and then the SMPC nodes release them on the origin chain.

The SMPC nodes perform several functions in linking an origin block chain with a destination block chain, completely autonomously and without human intervention :-

(a) When a new bridge between two block chains is created, the SMPC nodes generate the Decentralized Custody Management Account. This address is used to send assets to. These assets are held securely whilst assets are minted on the destination chain. This address is only controlled by the SMPC nodes and by no human or any other Extaernally Owned Address.

(b) Also when a new bridge between two block chains is created, the SMPC nodes link to a new smart contract on the destination chain for Wrapped Assets. This contract can be created by individuals or the Multichain team. It is used to mint new tokens on the destination chain, or to burn them when assets are redeemed to their origin chain. This contract is either AnyswapV5ERC20.sol, or a contract adapted form this to include custom code required by a project, such as transaction tax etc. The smart contract is not owned or controlled by Multichain, or anyone else. 

(c) The MPC nodes monitor the Decentralized Custody Management Account. When a new assets arrives there, it triggers the Wrapped Asset smart contract on the destination chain to mint tokens on the blockchain.

(d) If assets are redeemed, the Wrapped Asset smart contract is triggered by the MPC nodes to burn the tokens. The MPC nodes then release the assets from the Decentralized Custody Management Account and sends them to the user on the origin chain.

The wrapped asset token contract AnyswapV5ERC20 on the destination chain is a superset of the standard ERC20 type of contract. This contract allows minting of assets from the Wrapped Asset smart contract, but no other address can mint assets, since this could permit a non-equivalence between assets held by the SMPC address and those wrapped assets created. For this reason, some common asset types are not suitable for Bridges, including Elastic tokens.




The Multichain Router
---------------------

Multichain's Router allows assets to be transferred between two or more blockchains. There are three categories of Routing transfer that we can consider :-

**(a) Native to Native**


When a token ***already exists*** on a chain, we refer to it as a *native* asset. An example is USDC. In this instance, Multichain cannot mint the asset, so instead we use *liquidity pools*. A number of tokens are added by Multichain, a project team, or individuals to the pool on each chain. These tokens are then available for a user when they move cross chain. Ideally there are enough on each chain so that no matter how many tokens are transferred, there are enough in the pool for them. When a user moves say N XYZ tokens from chain A to chain B, those N tokens are available for another user who is transferring XYX from chain B (or chains C, D, E etc.) to chain A. They enter the liquidity pool on chain A. The total number of XYZ in the liquidity pools on all chains remains the same (unless extra XYZ are specifically added or removed by someone to the pools).

This would work well except that it is necessary to cope with the case where a user sends XYZ to a chain, but there is *not enough XYZ in the pool for them to withdraw*. This is why there are anyXYZ tokens created. These CAN be minted by Multichain on each chain and they represent the number of XYZ that the user SHOULD receive on that chain. If there are enough XYZ on the chain, then the anyXYZ are automatically swapped for those XYZ and the anyXYZ are burned. If there are not enough XYZ on the chain, then the user is left with their anyXYZ (called 'Your Pool Share') and they have to manually 'Remove' them, converting anyXYZ to XYZ when sufficient XYZ become available again. Remember - the number of XYZ in the pool on a chain increases when someone Routes XYZ away from that chain to another chain, or when someone specifically adds XYZ to the pool on that chain. 

The sequence that is followed when a user transfers XYZ from chain A to chain B is :- 
    (i) The XYZ is added to the pool on chain A.
    (ii) The same number of anyXYZ are minted on chain A.
    (iii) The SMPC node network detects this and causes anyXYZ to be minted on chain B, burning those on chain A.
    (iv) If the number of XYZ on chain B is greater than the anyXYZ created, then the XYZ are sent to the user's wallet on chain B and the anyXYZ are burned on chain B. If the number of XYZ is less than anyXYZ, then the user is left with their anyXYZ and this represents their pool share to be redeemed later by them for XYZ when there are enough again (by 'Removing' them).



![Router cross chain](/img/Router-liquidity-pools.jpg)



**(b) Router using Bridged Assets**


When the Router uses assets which are created using AnyswapV5ERC20.sol (Bridged assets), There is no need for a liquidity pool for the asset, since Multichain controls the supply of the asset on the chain where the contract resides. In this case the pool size is 'Unlimited'. For a Routed asset whose cross chain minting is entirely controlled by AnyswapV5ERC20, all that is required, is that a supply of that asset is added to the pool on the chain where the token was originally minted. A good example of this is MIM, which is created on Ethereum as a collateralized asset, but which has a series of bridges other chains (using AnyswapV5ERC20). These bridges are incorporated into the Router.

![Router with Bridged Assets](/img/Router-MIM-bridged-assets.png)

The use of exclusively Bridged assets in the Router leads to the best user experience, since they do not need to be concerned about the liquidity supply on the target chain.


**(c) Router using Hybrid Native/Bridged Assets**


Sometimes it is necessary to combine native assets on some chains with assets controlled by Multichain's Bridges (AnyswapV5ERC20.sol). This often happens when a project already had a third party bridge for an asset on another chain, but after joining the Router, wished to add tokens on extra chains. In this instance, the pre-existing tokens are 'native', but the tokens on new chains are 'Bridged'. It is the responsibility of the project team to ensure that there is sufficient liquidity in the pool for assets which are native on a chain, but the liquidity on chains for which Bridges exist is 'Unlimited'. here is an example of a Router hybrid asset.



![Router with Hybrid Assets](/img/Router-FTM-hybrid-assets.png)


For FTM, The Router uses native FTM on Ethereum, Binance Smart Chain and Fantom Opera, but is Bridged to Cronos, Telos, Boba, Celo and Harmony.




