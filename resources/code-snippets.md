---
title: 代码段
description: 本文包含资料库所有教程中出现的代码段合集，以便您更好地参与Moonbeam。
---

# 代码段

## 设置本地Moonbeam节点 {: #setting-up-a-local-moonbeam-node } 

**克隆Moonbeam教程的Repo：**

```
git clone -b {{ networks.development.build_tag }} https://github.com/PureStake/moonbeam
cd moonbeam
```

**安装Substrate及其基础要求：**

```
--8<-- 'code/setting-up-node/substrate.md'
```

**将Rust添加到系统路径：**

```
--8<-- 'code/setting-up-node/cargoerror.md'
```

**构建独立节点：**

```
--8<-- 'code/setting-up-node/build.md'
```

**在dev模式下运行节点：**

```
--8<-- 'code/setting-up-node/runnode.md'
```

**清除链，清除过去运行“dev”节点的所有旧数据：**

```
./target/release/moonbeam-development purge-chain --dev
```

**以dev模式运行节点可禁止显示块信息，但会在控制台中显示错误：**

```
./target/release/moonbeam-development --dev -lerror
```

## 创世账户 {: #genesis-account } 

--8<-- 'text/metamask-local/dev-account.md'

## 开发账户 {: #development-accounts } 

--8<-- 'text/setting-up-node/dev-accounts.md'

--8<-- 'code/setting-up-node/dev-testing-account.md'

## MetaMask {: #metamask } 

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
