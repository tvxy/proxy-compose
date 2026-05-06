# Xray-core 指南

配置文件是：`config.json`，里面的配置来自官方的 `Xray-examples` 项目，熟悉配置的也可自行配置。

## 1. 生成必要凭证

在修改配置之前，请运行以下命令获取 UUID 和密钥。

### A. 生成 UUID

用于配置文件中的用户 ID，确保连接的唯一性。

```bash
docker run --rm ghcr.io/xtls/xray-core:latest uuid
```

### B. 生成 X25519 密钥对

用于 Reality 等协议的加密。执行后会返回一对 **Private key** (私钥) 和 **Password** (密码)。

```bash
docker run --rm ghcr.io/xtls/xray-core:latest x25519
```

---

## 2. 修改配置文件 `config.json`

使用编辑器打开 `config.json`，根据生成的结果修改以下行：

* **第 29 行：** 填写上面生成的 **UUID**。
* **第 43 行：** 填写上面生成的 **PrivateKey** (私钥)。
* *注意：`Password` 用于客户端连接时的身份验证，不需要填写到配置文件。*

---

## 3. 启动服务

完成配置修改后，在当前目录下执行以下命令启动容器：

```bash
docker compose up -d
```
