---
title: 收集人
description: 通过此教程学习运行节点后在Moonbeam网络上成为收集人
---

# 在Moonbeam上运行收集人节点

![Collator Moonbeam Banner](/images/fullnode/collator-banner.png)

## 概览 {: #introduction } 

收集人在网络上维护其所参与的平行链。他们运行（所在平行链及中继链的）完整节点，并为中继链验证人创建状态转移证明。

Users can spin up full nodes on Moonbase Alpha and Moonriver and activate the `collate` feature to participate in the ecosystem as collators.

Moonbeam使用[Nimbus平行链共识框架](/learn/consensus/)，通过一个两步过滤器将收集人分配到区块生产插槽：

 - The parachain staking filter selects the top {{ networks.moonbase.staking.max_collators }} collators on Moonbase Alpha and the top {{ networks.moonriver.staking.max_collators }} collators on Moonriver in terms of tokens staked in each network. This filtered pool is called selected candidates, and selected candidates are rotated every round
 - The fixed size subset filter picks a pseudo-random subset of the previously selected candidates for each block production slot

此教程将带您完成以下步骤：

 - **[技术要求](#技术要求)** —— 展示如何从技术角度满足技术标准
 - **[账户与质押要求](#账户与质押要求)** —— 如何完成您的帐户设置并绑定代币成为候选收集人
 - **[生成会话密钥](#会话密钥)** —— 解释说明如何生成会话密钥（用于将您的author ID映射到您的H160帐户）
 - **[映射author ID至您的账户](#映射AuthorID到您的账户)** —— 概述如何将您的公共会话密钥映射到您的 H160帐户（用于接收区块奖励）

## 技术要求 {: #technical-requirements } 

收集人必须满足以下技术要求：

 - 必须运行带有验证选项的完整节点。可根据[此教程](/node-operators/networks/full-node/)选择收集人的特定代码段
 - 启动完整节点的telemetry服务器。具体操作步骤请见[此教程](/node-operators/networks/telemetry/)

## 账户与质押要求 {: #accounts-and-staking-requirements } 

Similar to Polkadot validators, you need to create an account. For Moonbeam, this is an H160 account or basically an Ethereum style account from which you hold the private keys. In addition, you will need a minimum amount of tokens staked to be considered eligible (become a candidate). Only a certain amount of the top collators by nominated stake will be in the active set.

=== "Moonbase Alpha"
    |    Variable     |                          Value                          |
    |:---------------:|:-------------------------------------------------------:|
    |  Minimum stake  | {{ networks.moonbase.staking.collator_min_stake }} DEV  |
    | Active set size | {{ networks.moonbase.staking.max_collators }} collators |

=== "Moonriver"
    |    Variable     |                          Value                           |
    |:---------------:|:--------------------------------------------------------:|
    |  Minimum stake  | {{ networks.moonriver.staking.collator_min_stake }} MOVR |
    | Active set size | {{ networks.moonriver.staking.max_collators }} collators |

### PolkadotJS账户 {: #account-in-polkadotjs } 

每个收集人都有一个与收集活动相关的账户。该账户用于识别收集人作为区块生产者的身份，并从区块奖励中发送相关款项。

目前，创建[PolkadotJS](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.testnet.moonbeam.network#/accounts)账户有两种方法：

 - 从[MetaMask](/integrations/wallets/metamask/)或[MathWallet](/integrations/wallets/mathwallet/)等外部钱包或服务中导入现有的（或创建新的）H160账户
 - 使用[PolkadotJS](/integrations/wallets/polkadotjs/)创建新的H160账户

将H160账户导入到PolkadotJS后，就可以在“Accounts”标签下看到该账户。请确保手上已有公共地址（`PUBLIC_KEY`），我们在设置[部署完整节点](/node-operators/networks/full-node/)的收集选项时需要用到它。

![Account in PolkadotJS](/images/fullnode/collator-polkadotjs1.png)

## 成为候选收集人  {: #become-a-collator-candidate } 

Before getting started, it's important to note some of the timings of different actions related to collation activities:

=== "Moonbase Alpha"
    |               Variable                |       Value        |
    |:-------------------------------------:|:------------------:|
    |    Join/leave collator candidates     | {{ networks.moonbase.collator_timings.join_leave_candidates.rounds }} rounds ({{ networks.moonbase.collator_timings.join_leave_candidates.hours }} hours) |
    |        Add/remove nominations         | {{ networks.moonbase.collator_timings.add_remove_nominations.rounds }} rounds ({{ networks.moonbase.collator_timings.add_remove_nominations.hours }} hours) |
    | Rewards payouts (after current round) | {{ networks.moonbase.collator_timings.rewards_payouts.rounds }} rounds ({{ networks.moonbase.collator_timings.rewards_payouts.hours }} hours) |

=== "Moonriver"
    |               Variable                |       Value        |
    |:-------------------------------------:|:------------------:|
    |    Join/leave collator candidates     | {{ networks.moonriver.collator_timings.join_leave_candidates.rounds }} rounds ({{ networks.moonriver.collator_timings.join_leave_candidates.hours }} hours) |
    |        Add/remove nominations         | {{ networks.moonriver.collator_timings.add_remove_nominations.rounds }} rounds ({{ networks.moonriver.collator_timings.add_remove_nominations.hours }} hours) |
    | Rewards payouts (after current round) | {{ networks.moonriver.collator_timings.rewards_payouts.rounds }} rounds ({{ networks.moonriver.collator_timings.rewards_payouts.hours }} hours) |


!!! note 
    The values presented in the previous table are subject to change in future releases.
### 获取候选池的大小  {: #get-the-size-of-the-candidate-pool } 

首先，您需要获取 `candidatePool`的大小（可通过治理更改），该参数将用于后续的交易中。为此，您必须从[PolkadotJS](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.testnet.moonbeam.network# 中运行以下 JavaScript 代码片段/js)中运行以下JavaScript代码段:

```js
// Simple script to get candidate pool size
const candidatePool = await api.query.parachainStaking.candidatePool();
console.log(`Candidate pool size is: ${candidatePool.length}`);
```

 1. 进入“Developers”标签
 2. 点击"JavaScript"
 3. 复制上述代码段并粘贴至编辑框内
 4. （可选）点击保存图标，并为代码段设置一个名称，如”Get candidatePool size“。这将在本地保存代码段
 5. 点击运行图标，以执行编辑框内的代码
 6. 点击复制图标复制结果，将在加入候选人池时使用

![Get Number of Candidates](/images/fullnode/collator-polkadotjs2.png)

### 加入候选人池 {: #join-the-candidate-pool } 

Once your node is running and in sync with the network, you become a collator candidate (and join the candidate pool). Depending on which network you are connected to, head to PolkadotJS for [Moonbase Alpha](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.testnet.moonbeam.network#/accounts) or [Moonriver](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fwss.moonriver.moonbeam.network#/accounts) and take the following steps:

 1. 进入“Developers”标签，点击“Extrinsics”
 2. 选择您用于参与收集活动的账户
 3. Confirm your collator account is funded with at least the [minimum stake required](#accounts-and-staking-requirements) plus some extra for transaction fees 
 4. 在“submit the following extrinsics”菜单中选择`parachainStaking`模块
 5. 打开下拉菜单，在质押相关的所有外部参数中，选择`joinCandidates()`函数
 6. Set the bond to at least the [minimum amount](#accounts-and-staking-requirements) to be considered a collator candidate. Only collator bond counts for this check. Additional nominations do not count
 7. 设置候选人数量即候选人池大小。如何设置该数值请查看[此文档](https://docs.moonbeam.network/node-operators/networks/collato #get-the-size-of-the-candidate-pool)
 8. 提交交易。根据向导指引使用创建账户时的密码进行交易签名

![Join Collators pool PolkadotJS](/images/fullnode/collator-polkadotjs3.png)

!!! 注意事项
    函数名称和最低绑定金额要求可能会在未来发布新版本时有所调整。
  
As mentioned before, only the top {{ networks.moonbase.staking.max_collators }} collators on Moonbase Alpha and the top {{ networks.moonriver.staking.max_collators }} collators on Moonriver by nominated stake will be in the active set. 

### 停止参与收集活动 {: #stop-collating } 

与波卡（Polkadot）的`chill()`函数相似，按照前述相同步骤进行操作，便可离开候选收集人池，但在第5步时需要选择`leaveCandidates()`函数。

## 会话密钥 {: #session-keys } 

随着[Moonbase Alpha v8](/networks/moonbase/)版本的发布，收集人将使用author ID（基本上是[会话密钥](https://wiki.polkadot.network/docs/learn-keys#session-keys)）签名区块。为了符合Substrate标准，Moonbeam收集人的会话密钥为[SR25519](https://wiki.polkadot.network/docs/learn-keys#what-is-sr25519-and-where-did-it-come-from)。本教程将向您展示如何创建/转换与收集人节点相关的会话密钥。

首先，请确保您正在[运行收集人节点](/node-operators/networks/full-node/)并已公开RPC端口。一旦您开始运行收集人节点，您的终端应出现类似以下日志：

![Collator Terminal Logs](/images/fullnode/collator-terminal1.png)

接着，通过使用`author_rotateKeys`方法将RPC调用发送到HTTP端点来转换会话密钥。若收集人的HTTP端点位于端口`9933`，则JSON-RPC调用可能如下所示：

```
curl http://127.0.0.1:9933 -H \
"Content-Type:application/json;charset=utf-8" -d \
  '{
    "jsonrpc":"2.0",
    "id":1,
    "method":"author_rotateKeys",
    "params": []
  }'
```

收集人节点应使用新的author ID（会话密钥）的相应公共密钥进行响应。

![Collator Terminal Logs RPC Rotate Keys](/images/fullnode/collator-terminal2.png)

请确保您已记下author ID的公钥。接下来，这将被映射到H160以太坊式地址（用于接收区块奖励）。

## 映射Author ID到您的账户 {: #map-author-id-to-your-account } 

生成author ID（会话密钥）后，将其映射到您的H160帐户（以太坊式地址）。该账户将用于接收区块奖励，请确保您拥有其私钥。

There is a bond that is sent when mapping your author ID with your account. This bond is per author ID registered. The bond set is as follows:

 - Moonbase Alpha - {{ networks.moonbase.staking.collator_map_bond }} DEV tokens 
 - Moonriver - {{ networks.moonriver.staking.collator_map_bond }} MOVR tokens. 

`authorMapping`模块具有以下外部编程：

 - **addAssociation**(*address* authorID) — maps your author ID to the H160 account from which the transaction is being sent, ensuring is the true owner of its private keys. It requires a bond
 - **clearAssociation**(*address* authorID) — clears the association of an author ID to the H160 account from which the transaction is being sent, which needs to be the owner of that author ID. Also refunds the bond
 - **updateAssociation**(*address* oldAuthorID, *address* newAuthorID) —  updates the mapping from an old author ID to a new one. Useful after a key rotation or migration. It executes both the `add` and `clear` association extrinsics atomically, enabling key rotation without needing a second bond

这个模块同时也新增以下RPC调用（链状态）：

- **mapping** — 一个自选输入值：author ID。将显示所有储存在链上的映射内容，或是根据您的输入显示相关内容。

### 映射外部信息 {: #mapping-extrinsic } 

To map your author ID to your account, you need to be inside the [candidate pool](#become-a-collator-candidate). Once you are a collator candidate, you need to send a mapping extrinsic (transaction). Note that this will bond tokens per author ID registered. To do so, take the following steps:

 1. 进入“Developer“标签
 2. 选择”Extrinsics”
 3. 选取您想要映射author ID的目标账户（用于签署此交易）。
 4. 选取`authorMapping`外部信息
 5. 将方法设置为`addAssociation()` 
 6. 输入author ID。在这个情况下，这在前一个部分通过RPC调用`author_rotateKeys`获得
 7. 点击“Submit Transaction”

![Author ID Mapping to Account Extrinsic](/images/fullnode/collator-polkadotjs4.png)

如果交易成功，您将在您的屏幕上看到确认通知。相反，请确认您是否加入[候选人池](https://docs.moonbeam.network/node-operators/networks/collator/#become-a-collator-candidate)。

![Author ID Mapping to Account Extrinsic Successful](/images/fullnode/collator-polkadotjs5.png)

### 检查映射设定 {: #checking-the-mappings } 

您也可以通过验证链上状态来确认目前的链上映射情况，请根据以下步骤进行操作：

 1. 进入“Developer”标签
 2. 选择“Chain State”
 3. 选择`authorMapping`作为查询状态
 4. 选择`mapping`方法
 5. 提供author ID进行查询。您也可以通过关闭按钮以停止检索所有链上的映射情况。
 6. 点击“+”按钮来传送RPC调用

![Author ID Mapping Chain State](/images/fullnode/collator-polkadotjs6.png)

如果没有特定的author ID，将会显示所有储存在链上的映射，您可以通过映射您的H160账户来验证您的author ID。