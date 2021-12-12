---
id: howToApply
title:  How to Apply for Multichain
description: How to apply for Multichain
sidebar_label: How to Apply for Multichain
---

This section covers how to apply for either a token Bridge listing, Router listing or integration of a new block chain into the Multichain SMPC Network. 

Listing a Cross Chain Token
===========================

Applying for a Bridge Listing
-----------------------------

To apply for a token Bridge listing, a member of the project team needs to complete this form [Applying for a Multichain Token Bridge](https://dard6erxu8t.typeform.com/to/C7RwF08A).

Before completing this Listing Application form, the team should read this [How to Apply for Cross Chain Bridges](https://anyswap.medium.com/how-to-apply-for-cross-chain-bridges-on-anyswap-82fcb6c9f0d2).

We do require that project teams can reassure us that there will be sufficient liquidity on the chain that the token will be bridged to. This is to avoid the situation that a user bridges a token, but they are then unable to swap it and must bridge it back, for which they are charged.

Please note that Bridge listing is usually free for established projects that appear on [Coingecko](https://www.coingecko.com/en) and when they are prepared to wait for 2 weeks for Bridge listing.

If the bridge is to or from Ethereum however, we do need to prefund the smart contract with ETH gas and we seek payment of 2 ETH to do this.

For new projects that are not yet listed at Coingecko, we perform due diligence, which can take 2 or more weeks, depending on how quickly we can gather the information we need to do this. A new project can bypass this requirement by paying a 5 ETH fee.

It normally takes about 2 weeks for a new Bridge to go live. Occasionally a project may need a listing more quickly than this. If this is the case and to compensate us for the disruption to our work schedule, we charge a Rapid Listing fee of 2 ETH.


Applying for Inclusion in the Router
------------------------------------

Normally we insist that a project first applies for a Bridge listing before we will include them in the Router (See [How It Works](/HowItWorks/howItWorks.md) if you are not sure of the difference between a Bridge and the Router).

After a period of time when we are confident that a project's bridges are working well, we can upgrade the Bridges to the Router, so that users can transfer tokens between any two chains, without having to first return them to the chain that they were originally minted. Avoiding the additional step can save the user a lot of fees, especially if they had to bridge back to Ethereum.

Once a project's token is on the Router, the project team can simply ask us to add additional chains and we will do this quickly.

Occasionally for larger projects, we will make exceptions and implement their token directly to the Router.


Applying to Add a New Block Chain
=================================

Please reach out to one of our team and we can talk you through the process of integrating new chains into our SMPC network. Please note that we are very busy and that it can take some time before we can schedule integration of new chains. We ask for an up front deposit of a few ETH to secure scheduling.

For EVM's we have some requirements to be met [Adding EVM's to Multichain](https://github.com/anyswap/CrossChain-Bridge/wiki/New-EVM-Chain-Listing-Requirement)


We can integrate any chain that uses ECDSA or EdDSA encryption, but some factors make it easier and quicker to implement

- A well functioning block explorer, preferably one that has the functionality of etherscan.io

- A wallet that is well recognised. It is easiest for us if the new chain supports MetaMask as a bare minimum, but we can also work with Coin98 or TerraStation for COSMOS ecosystem chains.

- Standard RPC calls to the EVM. If these have been altered, then we must check that the functionality is still there for us to be able to integrate. We only require quite basic calls.

- Concurrent with a recent EVM, such as London.

- An easy to implement Full Node. We will need to run a full node. If there is stable code to do this with well written instructions, then this will speed up the process.

- Well functioning RPC Gateways. 


Selection of Tokens to Bridge
-----------------------------

In the first instance we will not include the bridged tokens in our Router. This step usually can be taken after a few months when we are confident of the security and stability of the neewly added blockchain.

Whilst our engineers are integrating the chain, we will talk to you about which assets we will include to Bridge in the first instance. We will need assurance that these assets will have good liquidity provided by DEXes. We will make contact with DEXes on the new chain, with a Multichain partnership very much something that we consider worthwhile for the ecosystem.

For existing assets on the new chain, we can include them in the Router once that is implemented, following a period to ensure stability for the Bridges.