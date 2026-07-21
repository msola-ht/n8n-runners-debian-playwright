# n8n Runners (Debian)

基于 Debian 11 的 n8n Task Runners 镜像，从官方源码构建。

## 镜像

| 镜像 | 基于镜像 | 新增内容 |
|------|----------|----------|
| `lunare/n8n-runners-debian` | - | 基础运行时（Node.js + Python） |
| `lunare/n8n-runners-python` | Debian | 数据处理库 |
| `lunare/n8n-runners-playwright` | Python | Playwright 浏览器自动化 |

**数据处理库**包括：`markdown`、`Pillow`、`imageio-ffmpeg`、`numpy`
**架构支持**：amd64、arm64

## 使用方法

### 快速开始

```bash
# 拉取镜像
docker pull lunare/n8n-runners-debian:2.30.8stable

# 运行
docker run -d \
  -e N8N_RUNNERS_AUTH_TOKEN=your-token \
  -e N8N_RUNNERS_TASK_BROKER_URI=http://your-n8n:5679 \
  -p 5680:5680 \
  lunare/n8n-runners-debian:2.30.8stable
```

### 选择镜像

**基础镜像** - 适合常规使用
```bash
docker pull lunare/n8n-runners-debian:2.30.8stable
```

**Playwright 镜像** - 需要浏览器自动化时使用
```bash
docker pull lunare/n8n-runners-playwright:2.30.8stable
```

**Python 镜像** - 需要 numpy 等 Python 数据处理库时使用
```bash
docker pull lunare/n8n-runners-python:2.30.8stable
```

### 离线安装

从 [Release](https://github.com/msola-ht/n8n-runners-debian-playwright/releases) 下载 tar 文件：

```bash
# 加载镜像
docker load -i n8n-runners-debian-2.1.4-amd64.tar
docker load -i n8n-runners-debian-2.1.4-arm64.tar
docker load -i n8n-runners-playwright-2.1.4-amd64.tar
docker load -i n8n-runners-playwright-2.1.4-arm64.tar
docker load -i n8n-runners-python-2.1.4-amd64.tar
docker load -i n8n-runners-python-2.1.4-arm64.tar
```

## 镜像详细说明

### 1. Debian 基础镜像
**基础系统**：Debian 11 bullseye-slim
**运行时**：Node.js 22 + Python 3.13
**功能**：JavaScript 和 Python 代码执行
**系统工具**：FFMPEG

### 2. Python 扩展镜像
**基于**：Debian 基础镜像
**新增 Python 库**：`markdown`、`Pillow`、`imageio-ffmpeg`、`numpy`
**适用场景**：需要数据处理、图像处理、视频处理等功能

### 3. Playwright 扩展镜像
**基于**：Python 扩展镜像
**新增**：`playwright` 浏览器自动化库（支持 Chromium、Firefox、WebKit）
**适用场景**：需要浏览器自动化、网页截图、爬虫等功能

## 构建

本项目通过 GitHub Actions 自动从 [n8n-io/n8n](https://github.com/n8n-io/n8n) 官方源码构建并发布镜像。

- **自动触发**：每日 UTC 00:00 检查新版本
- **手动触发**：支持强制重建和仅发布 Release
- **多架构**：同时构建 amd64 和 arm64 镜像

## 版本

- n8n 版本：2.1.4
- Node.js 版本：22.21.0
- Python 版本：3.13

## 相关链接

- [n8n 官方仓库](https://github.com/n8n-io/n8n)
- [Docker Hub](https://hub.docker.com/r/lunare/n8n-runners-debian)
- [GitHub Releases](https://github.com/msola-ht/n8n-runners-debian-playwright/releases)
