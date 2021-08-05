---
title: MathWallet
description: 通过此教程学习如何将Mathwallet（浏览器版）钱包连接至Moonbeam。
---

# 使用MathWallet与Moonbeam交互

![Intro banner](/images/mathwallet/mathwallet-banner.png)

## 概览 {: #introduction } 

MathWallet [announced](https://mathwallet.org/moonbeam-wallet/en/) that is now natively supporting the [Moonbase Alpha TestNet](/networks/moonbase/) and [Moonriver](/networks/moonriver/). This means that you are now able to interact with Moonbase Alpha and Moonriver using another wallet besides MetaMask.

In this tutorial, we'll go through how to setup MathWallet to connect to our [TestNet](#connect-to-moonbase-alpha) and [Moonriver](#connect-to-moonriver). We'll also present a brief example of using MathWallet as a Web3 provider for other tools such as [Remix](/integrations/remix/).

## Checking Prerequisites {: #checking-prerequisites } 

首先您需要安装MathWallet浏览器插件，您可以通过此[网站](https://mathwallet.org/en-us/)安装。

成功安装之后，请打开它并且设置密码。

![Set wallet password](/images/mathwallet/mathwallet-images-1.png)

## Connect to Moonbase Alpha {: #connect-to-moonbase-alpha } 

In this part, we'll go through the process of connecting MathWallet to Moonbase Alpha. Enable Moonbase Alpha under Settings (top right gear icon) -> Networks -> Ethereum.

![Enable Moonbase Alpha](/images/mathwallet/mathwallet-images-2.png)

最后，在主界面点击Switch Network并选取Moonbase Alpha.

![Connect to Moonbase Alpha](/images/mathwallet/mathwallet-images-3.png)

就这样，您已经成功将MathWallet连接至Moonbase Alpha测试网了！您的钱包应如以下所示：

![Wallet Connected to Moonbase Alpha](/images/mathwallet/mathwallet-images-4.png)

## Connect to Moonriver

Getting started with Moonriver is a straightforward process. All you have to do is click Switch Network and select Moonriver

![Connect to Moonriver](/images/mathwallet/mathwallet-images-5.png)

And that is it, you now have MathWallet connected to Moonriver! Your wallet should look like this:

![Wallet Connected to Moonriver](/images/mathwallet/mathwallet-images-6.png)

## Adding a Wallet

The following steps will show you how to interact with the Moonbase Alpha TestNet, but can also be used to interact with Moonriver.

After you are connected to Moonbase Alpha, you can now create a wallet to get an account and start interacting with the TestNet. Currently, there are three ways to add a wallet:

 - 创建一个钱包
 - 使用助记词或私钥来导入一个已存在的钱包
- 连接硬钱包（_目前尚未支持_）

### 创建一个钱包 {: #create-a-wallet}

The following steps for creating a wallet can be modified for Moonriver.

如果希望建立一个新的钱包，请点击"Moonbase Alpha"左边的:heavy_plus_sign:图示并且选取"Create Wallet"。

![MathWallet create a wallet](/images/mathwallet/mathwallet-images-7.png)

设置并确认您的钱包名字。接着，请确认您已安全地记下您的助记词，因为它可以有直接的权限进入您的钱包并使用您的资产。当您完成了整个过程之后，您应当能够在新建立的钱包看到与其相连的公开地址。

![MathWallet wallet created](/images/mathwallet/mathwallet-images-8.png)

### 导入一个钱包 {: #import-a-wallet } 

如果希望建立一个新的钱包，请点击"Moonbase Alpha"左边的:heavy_plus_sign:图示并且选取"Import Wallet"。

![MathWallet import a wallet](/images/mathwallet/mathwallet-images-9.png)

接着，选取使用助记词或是私钥来导入钱包。如果选择的是助记词，请逐字输入助记词并以空格分格。至于第二个选项，请输入私钥（可以使用或不使用为`0x`开头输入，两者皆能运作）

![MathWallet private key or mnemonic import](/images/mathwallet/mathwallet-images-10.png)

接着点击下一步，设定好钱包名字之后就完成了！您应当可以在您输入的钱包上看到其相应的公共地址。

![MathWallet imported wallet](/images/mathwallet/mathwallet-images-11.png)

## 如何使用MathWallet {: #using-mathwallet } 

MathWallet serves as a Web3 provider in tools such as [Remix](/integrations/remix/). By having MathWallet connected to Moonbase Alpha or Moonriver, you can deploy contracts as you would like using MetaMask, signing the transactions with MathWallet instead.

For example, in Remix, when deploying a smart contract to Moonbase Alpha, make sure you select the "Injected Web3" option in the "Environment" menu. If you have MathWallet connected, you will see the TestNet chain ID just below the box (_1287_) and your MathWallet account injected into Remix as well. When sending a transaction, you should see a similar pop-up from MathWallet:

![MathWallet sign transaction](/images/mathwallet/mathwallet-images-12.png)

点击"Accept"代表您正在签名这项交易，接着合约即将被部署至Moonbase Alpha测试网。
