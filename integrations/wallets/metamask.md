---
title: MetaMask
description: 通过此教程学习如何将MetaMask，一个以浏览器为基础的以太坊钱包连接至Moonbeam。
---

# 如何使用MetaMask与Moonbeam交互

![Intro diagram](/images/integrations/integrations-metamask-banner.png)

## 概览 {: #introduction } 

开发人员可以利用Moonbeam与以太坊兼容的特色，将一些如[MetaMask](https://metamask.io/)的工具整合至DApps中。如此一来，就可以使用MetaMask提供的库与要部署的链相交互。

目前为止，MetaMask可以配置并连接到两个网络：一个是Moonbeam独立节点，另一个是Moonbase Alpha测试网。

若您已安装MetaMask，您可轻松将MetaMask链接至Moonbase Alpha测试网络：

<div class="button-wrapper">
    <a href="#" class="md-button connectMetaMask">Connect MetaMask</a>
</div>
!!! 注意事项
    MetaMask将会跳出弹框，要求授权将Moonbase Alpha添加为自定义网络。经授权后，MetaMask会将您当前的网络切换到Moonbase Alpha。


## 如何将MetaMask连接至Moonbeam {: #connect-metamask-to-moonbeam } 

当您成功安装了[MetaMask](https://metamask.io/)，您可以点击右上角的logo和设置来将其连接至Moonbeam。

![MetaMask3](/images/testnet/testnet-metamask3.png)

接着，进入Networks标签并点击“Add Network“按钮。

![MetaMask4](/images/testnet/testnet-metamask4.png)

您可以为以下网络配置MetaMask：

=== "Moonbeam Development Node"

    - Network Name: `Moonbeam Dev`
    - RPC URL: `{{ networks.development.rpc_url }}`
    - ChainID: `{{ networks.development.chain_id }}`
    - Symbol (Optional): `DEV`
    - Block Explorer (Optional): `{{ networks.development.block_explorer }}`

=== "Moonbase Alpha TestNet"

    - Network Name: `Moonbase Alpha`
    - RPC URL: `{{ networks.moonbase.rpc_url }}`
    - ChainID: `{{ networks.moonbase.chain_id }}`
    - Symbol (Optional): `DEV`
    - Block Explorer (Optional): `{{ networks.moonbase.block_explorer }}`

=== "Moonriver"

    - Network Name: `Moonriver`
    - RPC URL: `{{ networks.moonriver.rpc_url }}`
    - ChainID: `{{ networks.moonriver.chain_id }}`
    - Symbol (Optional): `MOVR`
    - Block Explorer (Optional): `{{ networks.moonriver.block_explorer }}`

## 分步教程 {: #step-by-step-tutorials }

如果您想获得更加详细的分步教程，你可以查看以下的特定教程：

 - [Moonbeam开发节点](/getting-started/local-node/using-metamask/)上的MetaMask
 - [Moonbase Alpha](/getting-started/moonbase/metamask/)上的MetaMask

