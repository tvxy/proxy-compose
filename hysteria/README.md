# Hysteria2 指南

## 1. 配置文件说明

Hysteria2 的核心配置文件为 **`hysteria.yaml`**。

* **建议：** 除非有进阶定制需求，通常情况下仅需修改 `password` 字段即可。

## 2. 生成自签名证书

在启动服务前，需要生成加密通信所需的证书文件。请按顺序执行以下步骤：

1. **进入证书目录：**
```bash
cd certs
```

2. **生成证书命令：**
执行以下命令生成有效期为 100 年的自签名证书：
```bash
openssl req -x509 -nodes -newkey ec:<(openssl ecparam -name prime256v1) -keyout server.key -out server.crt -subj "/CN=bing.com" -days 36500
```

3. **确认结果：**
执行完毕后，请确认 `certs` 文件夹内已生成 `server.key` 和 `server.crt` 两个文件。

## 3. 启动服务

使用 Docker Compose 在后台运行服务：

```bash
docker compose up -d
```
