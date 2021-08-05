---
title: 概述
description: 作为波卡（Polkadot）平行链，Moonbeam将通过链上治理机制，来允许公众进行权重投票。
---

# Moonbeam治理

![Governance Moonbeam Banner](/images/governance/governance-overview-banner.png)

## 概览 {: #introduction } 

Moonbeam作为去中心化网络，将由核心开发者、应用程序开发者、校验者、用户及其它贡献者等代币持有者社区进行治理。

我们致力于鼓励这些领域的代币持有者参与网络上线过程。

## 般定义 {: #general-definitions } 

权力越大，责任越大。在参与Moonbeam治理之前，请先了解一些重要参数：

 - **提案 **—— 代币持有者提出的行动方案或事项，需获其它用户赞成才可进入公投环节
 - **公投** —— 获得赞成数最多的提案将由社区进行公投。除非有紧急公投正在进行，否则最多只能同时进行5个公投
 - **发起期** —— 两次公投之间的时间间隔
 - **投票期** —— 代币持有者对提案进行公投的时期（一次公投的时长）
- **投票** —— 代币持有者根据权益和信念值进行公投。信念值指的是代币持有者参与投票的代币被锁定的时长：锁定期越长，相同数量的代币投票权重越高。公投通过后，提案将进入延迟执行期，因此不同意该提案的用户可以在这期间退出网络
 - **执行期** —— 提案获得同意到正式执行（写入法律）之间的时期，也是进行提案所需的最低代币锁定时长
 - **锁定期** —— 赢得投票用户的代币锁定期（提案执行后）。在此期间，用户仍可使用锁定代币进行质押或投票
 - **委托** —— 将自己的投票权委托给其他账户，以积累一定信念值的行为

=== "Moonbase Alpha"

    |         Variable         |  |                                                              Value                                                              |
    |:------------------------:|::|:-------------------------------------------------------------------------------------------------------------------------------:|
    |      Voting Period       |  |       {{ networks.moonbase.democracy.vote_period.blocks}} blocks ({{ networks.moonbase.democracy.vote_period.days}} days)       |
    | Fast-Track Voting Period |  | {{ networks.moonbase.democracy.fast_vote_period.blocks}} blocks ({{ networks.moonbase.democracy.fast_vote_period.hours}} hours) |
    |     Enactment Period     |  |      {{ networks.moonbase.democracy.enact_period.blocks}} blocks ({{ networks.moonbase.democracy.enact_period.days}} day)       |
    |     Cool-off Period      |  |       {{ networks.moonbase.democracy.cool_period.blocks}} blocks ({{ networks.moonbase.democracy.cool_period.days}} days)       |
    |     Minimum Deposit      |  |                                        {{ networks.moonbase.democracy.min_deposit }} DEV                                        |

=== "Moonriver"

    |         Variable         |  |                                                              Value                                                              |
    |:------------------------:|::|:-------------------------------------------------------------------------------------------------------------------------------:|
    |      Voting Period       |  |      {{ networks.moonriver.democracy.vote_period.blocks}} blocks ({{ networks.moonriver.democracy.vote_period.days}} days)      |
    | Fast-Track Voting Period |  | {{ networks.moonriver.democracy.fast_vote_period.blocks}} blocks ({{ networks.moonriver.democracy.fast_vote_period.days}} day) |
    |     Enactment Period     |  |     {{ networks.moonriver.democracy.enact_period.blocks}} blocks ({{ networks.moonriver.democracy.enact_period.days}} day)      |
    |     Cool-off Period      |  |      {{ networks.moonriver.democracy.cool_period.blocks}} blocks ({{ networks.moonriver.democracy.cool_period.days}} days)      |
    |     Minimum Deposit      |  |                                       {{ networks.moonriver.democracy.min_deposit }} MOVR                                       |

## 原则 {: #principles } 

在参与Moonbeam治理流程中，我们还希望用户做到以下几点：

 - 对希望参与Moonbeam网络的和受到治理决策影响的代币持有者持开放包容的态度。
 - 欢迎其他代币持有者一同参与，而不是冷漠相待，即使他们的观点可能与您本身的相反。
 - 在决策过程中保持开放透明。
 - 将网络的良好发展置于个人利益之上。
 - 任何时候都做一位道德行动者，时刻考虑自身作为（或不作为）的道德影响。
 - 在与其他代币持有者互动的过程中保持耐心与大度，但绝不容忍语言、行动或行为上的暴力和伤害。

以上原则很大程度上受到Vlad Zamfir先生关于区块链治理的著作的启发。如需了解更多详情，请参阅他撰写的文章，[尤其是这一篇](https://medium.com/@Vlad_Zamfir/how-to-participate-in-blockchain-governance-in-good-faith-and-with-good-manners-bd4e16846434)。

## 链上治理机制 {: #on-chain-governance-mechanics } 

Moonbeam的“硬性”治理流程将由链上流程驱动，并采用由民主权利、理事会、财政库组成的[Substrate框架模块](/resources/glossary/#substrate-frame-pallets)，和Kusama、Polkadot中继链的治理方式相似。该方式能确保与Moonbeam网络相关的关键决策由多数代币作出。提案进入公投后，根据投票权重得出投票结果，从而执行决策。

这一治理机制的主要组成部分包括：

 - **Referendum** — a proposal for a change to the Moonbeam system including values for key parameters, code upgrades, or changes to the governance system itself
 - **Voting** — referenda will be voted on by token holders on a stake-weighted basis. Referenda which pass are subject to delayed enactment such that people that disagree with the direction of the decision have time to exit the network
 - **Council** — a group of elected individuals who have special voting rights within the system. Council members are expected to propose referenda for voting and have an ability to veto publicly-sourced referenda. There are rolling elections for council members where GLMR holders will vote on new or existing council members. The Council is also responsible for electing the technical committee
 - **Technical Committee** — a group of individuals elected by the Council who have special voting rights. As in Polkadot and Kusama, the Technical Committee has the ability to (along with the Council) fast-track emergency referenda voting and implementation in urgent circumstances. A fast-tracked referendum can be created alongside existing active referenda. That is to say, an emergency referendum does not replace currently active referenda
 - **Treasury** — A collection of funds that can be spent by submitting a proposal along with a deposit. Spending proposals must be approved by the council. Rejected proposals will result in the proposer losing their deposit

更多关于Substrate框架模块的链上治理详情，请查阅[Polkadot网站概述](https://polkadot.network/a-walkthrough-of-polkadots-governance/)和[wiki博客](https://wiki.polkadot.network/docs/learn-governance)。

## Voting Rights of the Council and the Technical Committee {: #voting-rights-of-the-council-and-the-technical-committee } 

This section covers some background information on voting rights. There is a limit to the amount of time in blocks that the technical committee and the council have to vote on motions. Motions may end in fewer blocks if there are already enough votes submitted to determine the outcome. A maximum of {{ networks.moonbase.democracy.max_proposals}} proposals can be open each in the technical committee and in the council.

**Voting Rights to Cancel:**

 * The technical committee may cancel a proposal before it has been passed only by unanimous vote
 * A single technical committee member may veto an inbound council proposal, however, they can only veto it once, and it only lasts for the cool-off period ({{ networks.moonbase.democracy.cool_period.days}} days)

## Try it out {: #try-it-out } 

目前，Moonbase Alpha测试网上的代币持有者可以提交提案并进行投票。具体步骤请查阅以下教程：

 - [提案](/governance/proposals/)
 - [投票](/governance/voting/)

--8<-- 'text/moonriver-launch/governance-phase-2.md'

理事会和财政库相关功能尚未部署。
