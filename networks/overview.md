---
title: 概况
description: 本文将简要描述Moonbeam计划建立的网络，一个位于Polkadot上并与以太坊兼容的智能合约平行链。
---

# 网络

我们计划建立数个以Moonbeam为基础，且长期发展的网络。因此除了Polkadot之外，Moonbeam也会在Kuasama上面部署。

以下是我们关于部署平行链的路线图：

 - Moonbase Alpha: PureStake主导平行链测试网（2020 九月)
 - Moonrock: 部署于Rococo测试网上 (_May 2021_)
 - Moonriver: 部署于Kusama上(_June 2021_)
 - Moonbeam: 部署于Polkadot上（2021 Q3末）

这个策略能让我们在保持适当的更新速度同时，降低Polkadot 主网上Moonbeam软件升级的风险。同时，我们会在网络开放的时候提供更多关于如何使用不同以Moonbeam为基础的网络细节。

## Moonbase Alpha {: #moonbase-alpha } 

这个测试网由PureStake所主导，其特色是使用平行链以及中继链方案。目标是让开发者在不用运行自己的节点或是网络的前提下，能够在一个共享平行链的环境中，测试Moonbeam与以太坊的兼容性。

[在这里了解更多Moonbase Alpha的资讯](/networks/moonbase/)

## Moonrock {: #moonrock } 

We decided not to participate in the first parachain deployments to Rococo because we have been running our own parachain/relay chain setup since we launched our TestNet in September 2020.

However, Moonrock was deployed to Rococo for the first time in May 2021. 


## Moonriver {: #moonriver } 

In advance of deploying to the Polkadot MainNet, [Moonbeam launched Moonriver](https://moonbeam.network/announcements/moonriver-launch-kusama/) as a parachain on the Kusama network. The parachain functionality is live on Kusama and features are progressively being released according to the [Moonriver launch schedule](https://moonbeam.network/networks/moonriver/launch/). 

We plan to exercise parachain-related functionality such as [XCMP](https://wiki.polkadot.network/docs/learn-crosschain) and [SPREE](https://wiki.polkadot.network/docs/learn-spree) on Moonriver as those features become available.

[Learn more about Moonriver](/networks/moonriver/).

## Moonbeam的Polkadot主网 {: #moonbeam-polkadot-mainnet } 

Moonbeam的生产主网同样会以平行链的形式部署在Polkadot上，这个Moonbeam网络将有最高级别的安全性和可用性，其在主网上运行的代码基本上将通过上面列出的一个或多个其他网络来进行审查。