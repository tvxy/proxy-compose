# AnyTLS 指南

使用 sing-box 官方稳定版镜像 `ghcr.io/sagernet/sing-box:latest`。

以下操作均从 `anytls` 目录开始。

## 1. 修改密码

打开 `config.json`，将 `password` 中的 `CHANGE_ME_TO_A_RANDOM_PASSWORD` 替换为自己的密码。

## 2. 生成自签名证书

进入证书目录，在 Bash 或 Zsh 中执行以下命令，也可直接复制 `certs/command.txt` 中的命令：

```bash
cd certs
openssl req -x509 -nodes -newkey ec:<(openssl ecparam -name prime256v1) -keyout server.key -out server.crt -subj "/CN=bing.com" -addext "subjectAltName=DNS:bing.com" -days 36500
cd ..
```

生成后，`certs` 目录内应有 `server.crt` 和 `server.key`。

## 3. 启动服务

在服务器安全组和防火墙中放行 **TCP 10443**，然后启动：

```bash
docker compose up -d
```

## 4. 客户端连接

| 参数 | 内容 |
| --- | --- |
| 协议 | AnyTLS |
| 服务器 | 服务器公网 IP |
| 端口 | `10443` |
| 密码 | 与 `config.json` 中一致 |
| SNI | `bing.com` |
| TLS | 开启 |
| 允许不安全 / 跳过证书验证 | 开启 |
