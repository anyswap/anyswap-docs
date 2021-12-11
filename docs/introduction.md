---
id: introduction
title: Introduction
description: Introduction
sidebar_label: Introduction
---


Multichain was born as Anyswap on the 20th July 2020 to service the clear needs of different and diverse blockchains to communicate with each other. Each blockchain has its own unique services that it provides, its own community and its own development ecosystem. For our industry to reach the next level for consumers, we need a fast, secure, inexpensive and reliable way to exchange value, data and exercise control between the chains. 

The solutions developed by Multichain allow almost all blockchains to inter-operate. There is no restriction to Ethereum like chains (e.g. Binance Smart Chain), or different Layer 2 chains requiring finality to Ethereum (e.g. Polygon), or a network of Parachains (e.g. Moonbeam in the PolkaDot system), or Bitcoin types of chain (e.g. Litecoin), or COSMOS chains (e.g. Terra). These are either now all integrated, or on course for integration. With support for all ECDSA and EdDSA encrypted chains, Multichain is almost universally applicable as an interoperable layer.

Multichain is now the leader in the crosschain field, with a rapidly expanding family of chains (currently 26) and daily volumes well in excess of $100 million (URL of anyswap.net). Its sustained daily volume of more than $100 million, its Total Value Locked in excess of $5 billion and its thousands of daily users is testament to its popularity and security.

We take pride that we are an open source protocol. Indeed to be properly described as decentralized as we are, it is essential to be open source, since otherwise how would anyone know that this was the case? We also have a strong belief in the principle of trustlessness. Anyone can use our crosschain services. They are controlled by code and there are no Externally Owned Addresses acting as a weak link.


The SMPC Network
===============

The Multichain network comprises what are called SMPC nodes. They exist separately from any blockchain and collectively sign transactions, but a group of them must do so together and they each only ever know part of the key to make this happen. The SMPC nodes are run by different organisations, institutions and individuals and they are incentivized to perform their functions properly.


The Multichain Services
=======================

There are some different services that use the SMPC network

(1) Custodial 'Bridge'
----------------------

An asset is locked up in a smart contract on the source chain and then a corresponding wrapped asset is minted on the target chain. The reverse process (called Redeeming) sees the wrapped asset being burned and then the custodial asset being released back to the chain from where it originally came from. A bridge can therefore only ever operate between two blockchains. This was the first crosschain service developed back in July 2020, which we call V2. There are now more than 600 bridged assets and it is easy to deploy new ones, a process that takes about 2 weeks, which we can perform upon request and is free.

For many projects, our custodial bridges are still the best solution, since they do not require liquidity on each chain. They remain alongside our other non-custodial methods of crosschain transfer. They are most useful when projects are launching straightforward ERC20 like tokens on new chains where they do not already have tokens. Several two way bridges can be deployed for each token.




(2) Multichain 'Router'
-----------------------

On June 4th 2021, Multichain launched its Multichain router V3 beta mainnet. The Router has these significant features:

- It can allow assets transfers between any two or more chains.

- It can work with pre-existing assets on block chains, by using liquidity pools for those assets.

- It can also work with Bridged assets, where Multichain is responsible for minting assets on chains. This allows a generalisation of Bridges, so that assets are not restricted to having to return to their source chain before being sent to another chain. This makes for a cost effective solution for users, especially if the asset originated on Ethereum.

 - The Router can include both native and Bridged assets. This allows inclusion of assets that might have been generated with a third party bridge (though we would need to understand what bridges were originally used).

    


(3) 'anyCall' Crosschain Contract Calls
---------------------------------------

With the anyCall smart contract function, projects can now make crosschain contract calls, all with the security of Multichain's MPC network.

(4) Crosschain NFT Bridges and Router
-------------------------------------

Multichain now offers a bridge for NFT's (both ERC721 and ERC1155 smart contract standards). We also now have a Router ofr NFT's.


Please see [How it Works](/HowItWorks/howItWorks.md) for a more in depth discussion about SMPC networks and how Bridges and the Router work.


