# 使用 Docker Compose 快速搭建代理

这是一个基于 Docker Compose 的快速代理服务部署方案。通过预设的配置，你可以一键搭建并运行多种主流代理协议。

## 🚀 支持协议

目前已支持以下协议的快速部署：

| 协议 | 实现 | 目录与部署说明 |
| --- | --- | --- |
| VLESS | Xray-core | [vless](./vless/README.md) |
| Hysteria2 | Hysteria | [hysteria2](./hysteria2/README.md) |
| AnyTLS | sing-box | [anytls](./anytls/README.md) |

---

## 🛠️ 准备工作

### 1. 操作系统

本方案不限制操作系统，只要能安装 **Docker** 即可。

> **推荐：** 使用 **Debian** 系统以获得最佳兼容性。

### 2. 校准系统时间

某些代理软件对系统时间要求严格，时间误差可能导致连接失败。建议设置一下服务器的时间：

```bash
# 设置时区为上海
sudo timedatectl set-timezone Asia/Shanghai
# 开启网络时间同步
sudo timedatectl set-ntp true
# 查看状态
timedatectl
```

### 3. 配置防火墙

根据你的需求开放对应端口。以下是以 Debian 系统的 `ufw` 为例的常用命令：

```bash
sudo ufw enable                    # 开启防火墙
sudo ufw allow 22                  # 必须放行 SSH 端口
sudo ufw allow 10000:20000/tcp     # 放行自定义 TCP 端口范围
sudo ufw allow 10000:20000/udp     # 放行自定义 UDP 端口范围
sudo ufw status                    # 查看防火墙状态
```

---

## 💾 安装环境

使用官方一键脚本安装 Docker：

```bash
curl -fsSL https://get.docker.com | sh
```

**验证安装：**
输入 `docker version`，若能看到版本信息，则说明安装成功。

---

## 📂 部署步骤

1. **克隆项目到本地**：`git clone https://github.com/tvxy/proxy-compose.git`
2. **进入协议目录**：`cd proxy-compose/vless`、`cd proxy-compose/hysteria2` 或 `cd proxy-compose/anytls`。
3. **修改配置**：按照对应目录的 README 设置密码或密钥，并按需生成证书、放行端口。
4. **启动服务**：在对应协议目录执行 `docker compose up -d`。

### 常用命令

| 动作 | 命令 |
| --- | --- |
| **启动容器** | `docker compose up -d` |
| **停止并移除容器** | `docker compose down -v` |
| **查看运行状态** | `docker compose ps` |
| **查看实时日志** | `docker compose logs -f` |

---
