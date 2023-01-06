# lego-docs

## Contents
- [lego-docs](#lego-docs)
  - [Contents](#contents)
  - [Introduction](#introduction)
    - [What is Sybil defense?](#what-is-sybil-defense)
    - [What are Legos?](#what-are-legos)
  - [What does a lego look like?](#what-does-a-lego-look-like)
  - [What Legos are already available?](#what-legos-are-already-available)
  - [Building Legos](#building-legos)
    - [How do I build a Lego?](#how-do-i-build-a-lego)
    - [Lego spec](#lego-spec)
    - [contribution guidelines](#contribution-guidelines)
    - [Handling Gitcoin data](#handling-gitcoin-data)
    - [documenting a new Lego](#documenting-a-new-lego)
  - [Roadmap](#roadmap)
    - [Lego ideas](#lego-ideas)
    - [UX/UI](#uxui)
    - [Performance](#performance)
  - [Downloads](#downloads)
  - [Lego Documentation](#lego-documentation)
    - [Gitcoin passport](#gitcoin-passport)
    - [Levenstein Distance](#levenstein-distance)
    - [Shared IP](#shared-ip)
    - [SAD model](#sad-model)
    - [DonorDNA](#donordna)
    - [GrantDNA](#grantdna)
    - [Onchain Intersectionality](#onchain-intersectionality)
  - [Resources](#resources)
    - [FAQs](#faqs)
    - [Read/Watch/Listen](#readwatchlisten)


## Introduction

### What is Sybil defense?

Sybils are "fake" users. They are users that do not represent real humans. Sybils are created in order to make a single human appear to be many in order to have outsized weight in a voting protocol or to receive more than a single person's worth of some reward (e.g. an airdrop). These Sybils should be eliminated from a fair voting/funding protocol, but theyare no always easy to detect.

![]()

Do Androids Dream of Electric Sheep tells the story of a detective tasked with eliminating humanoid "replicants" that are almost indistinguishable from natural humans. They do this using a system of tests, including an instrumented interview that look for subtle "tells" such as a limited ability to make complex moral judgments in hypothetical scenarios. Sybil defenders are similarly tasked with distinguishing real and virtual humans in a mixed population where they are difficult to tell apart. They too look for subtle "tells" that give Sybils away. Sometimes the Sybil signals are obvious and unambiguous, sometimes they are not. The additional complication for Sybil hunters is that the entire population exists in a digital space where a human's physical existence cannot be proven by their presence- it can only be demonstrated using forgeable proxies. Reliably linking actions to identities is therefore a subtle science that pieces together multiple lines of evidence to build a personhood profile.

For Gitcoin grants, Sybil detection is extremely important because minimizing the influence of Sybils creates a funding environment that more accurately represents the true preferences of the community of donors. Sybils skew the allocated funds in favour of individual projects to benefit some specific user or group, rather than efficiently distributing funds to genuine public goods. Gitcoin aims to solve for one-human one-vote, while Sybils actuively try to subvert that and unfairly allocate more votes to fewer humans.

To date, Sybil defense has been executed by a small group of Gitcoin data scientists manually applying algorithms to user data and reviewing disputes. Now, as Gitcoion becomes a protocol, Sybil defense will be executed in a more decentralized way. This requires composable tools for Sybil defense that can be applied to open data. These composable tools are known as Sybil defense Legos because they can be recombined and reconfigured to built bespoke defense strategies fit for specific purposes.

### What are Legos?

Gitcoin is decentralizing by converting the core Sybil defense functions into a set of tools that can easily be implemented by users or eventually forked and recombined in creative ways in other projects. This requires the Sybil defense procedures currently managed by humans to be broken down into discrete units, defined in code, documented and made accessible as composable building blocks. These are known as "Legos". Lego bricks are simple building blocks that can be connected to each other in creative combinations to form all kinds of structures or even machines that are much more complex than their component parts. Similarly, modular, composable software tools can be used to build imaginative systems for defending against Sybils. 

![honest user vs Sybil](/assets/man-with-multiple-shadows.webp)

For Gitcoin grants, Legos start as useful insights from analysis of Gitcoin data - some metric that reveals users to be Sybils. Then, this finding is expressed algorithmically and turned into some executable code. At the moment, most Legos exist in this form - shareable scripts in a Github repository. However, the ideal scenario is to make these Legos executable with no coding required, probably through a web interface where Lego's can be selected to be executed remotely, returning a simple result to the user. 

## What does a lego look like?

A "Lego"is a discrete unit that performs one, specific function in the Gitcoin protocol. It should work as a building block, meaning that it should be deployable on its own, taking well defined inputs and returning some known outputs. It should also connect to other Legos, which requires some standardization of types and formats for inputs and outputs so that tools can be chained together in intuitive pipelines. Making these Lego's available empowers the community to build on top of them and saves developers from having to repeatedly reinvent the wheel when building out new products.

For a truly composable Lego, the code should be:

- **Tightly scoped**: the tool should fulfill one single function without side-effects so that it can be deployed in a variety of contexts with reliable outcomes.
- **Free and open**: open source codes that is publicly available, auditable, able to run on normal consumer hardware.
- **Permissionless**: not requiring special credentials or licenses to view, download or deploy, and users have the ability to fork the code any time.
- **Accessible**: sufficiently well-documented and with intuitive UX to enable a wide community of users
- **Minimal dependencies**: protect the "supply chain" by minimizing the dependencies. Where dependencies are unavoidable, bundle them or make them very easy to access.
- **Modular**: uses common formats and types so that outputs of one Lego can become inputs to another in pipelines - i.e. the legos are designed to be used as building blocks for larger systems with no specific predetermined structure.
- **Open governance**: Decisions about the development of the Lego's should not be gated by individuals or centralized groups - instead governance should be open so that users can trust that the code will be developed and maintained with integrity and community participation. 

Some examples of Lego's that conform to these norms are smart contracts on Ethereum. Smart contracts, or even individual functions of smart contracts, can be forked and rewritten, or stacked on top of each other in creative ways to build new protocols. This is common practise in DeFi, where primitives such as asset borrowing, lending and staking contracts are combined in many different ways by teams aiming to create protocols optimized for yield, or resilience, or security. Token standards such as ERC-20 (Ethereum token standard) and ERC-721 (Ethereum NFT standard) are composable primitives that can be built on top of - there is a huge diversity of token and NFT projects built on top of these original standards, often in combination with DeFi Legos, creating a diverse landscape of decentralized financial products and a community with freedom and agency to create new versions and implement new ideas.

We want to bring that freedom and agency to public goods funding. Rather than being centralized overseers of public goods funding, we want to share tools that empower the community to do it in clever and creative new ways.

## What Legos are already available?

Several Lego's are already being used to manage Sybils in Gitcoin grants. These are:

- **Gitcoin Passport:** When a user connects a passport, a trust score can be calculated for them which is used as evidence of personhood - the greater the score the more likely they are to be a genuine user.
- **Levenstein distance:** Every user has a username - when they sign up to Gitcoin grants the similarity of their name can be compared against all other usernames to generate a likelihood of the username being auto-generated - evidence of a Sybil account. This Lego **will be deprecated** in the grants protocol because usernames will no longer be available - only Ethereum addresses, wallet IDs and grant/round nonce. 
- **Shared IP**: User IP addresses can also be checked to see if they are shared with many other users. Lots of addresses originating from the same IP could be a marker for Sybil attackers.
- **SAD model:** The user also has a Gitcoin account whose history can be analyzed using the SAD model to give another Sybil-likelihood score.
- **DonorDNA**: When a donor connects their wallet their profile of past donations can be analyzed to see whether it is similar to groups of other users, which may be indicatative of Sybil rings.
- **GrantDNA**: Each grant has a set of donors that can be represented as a set of binary data. This can be used to compare grants against flagged grants to see if they have similar donor profiles.
- **Onchain Intersectionality**: How many out of a set of on-chain credentials does a user have?

The outputs from these Legos are collated into a single dataset where each user has a Sybil likelihood as measured across several dimensions. A threshold value that separates "suspicious" and "not suspicious" users can be applied to each metric individually such that the final dataset is a set of Booleans for each user, and the final decision about whether to omit or allow a particular user is a simple summation (e.g. if sum > 3, squelch). Alternatively, the actual value from each metric can be propagated to the final dataset and a (weighted) average applied there to identify Sybils. Either way, the outputs from the Legos themselves are aggregated and used collectively to come to a decision about the trustability of the user. In summary, the Legos are run independently and the results passed to an aggregator. The user sees the result of each independent Lego and also the result of the aggregator - i.e. they get an overall Sybil likelihood score/trust score and also a break down of the individual Sybil "dimensions".


## Building Legos
### How do I build a Lego?
### Lego spec
### contribution guidelines
### Handling Gitcoin data
### documenting a new Lego

## Roadmap
### Lego ideas
### UX/UI
### Performance

## Downloads

## Lego Documentation
### Gitcoin passport
### Levenstein Distance
### Shared IP
### SAD model
### DonorDNA
### GrantDNA
### Onchain Intersectionality


## Resources
### FAQs
### Read/Watch/Listen