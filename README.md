# n8n Runners (Debian)

基于 Debian 11 的 n8n Task Runners 镜像，从官方源码构建。

## 镜像

| 镜像 | 说明 |
|------|------|
| `lunare/n8n-runners-debian` | Debian 基础镜像，支持 JavaScript 和 Python 代码执行 |
| `lunare/n8n-runners-playwright` | 扩展镜像，额外包含 Playwright 浏览器自动化支持 |
| `lunare/n8n-runners-python` | 扩展镜像，包含数据处理常用库（numpy、Pillow、FFMPEG 等） |

## 使用方法

### 拉取镜像

```bash
# 拉取基础镜像
docker pull lunare/n8n-runners-debian:2.1.4

# 拉取 Playwright 镜像
docker pull lunare/n8n-runners-playwright:2.1.4

# 拉取 Python 镜像
docker pull lunare/n8n-runners-python:2.1.4
```

### 运行

**基础镜像：**
```bash
docker run -d \
  -e N8N_RUNNERS_AUTH_TOKEN=your-token \
  -e N8N_RUNNERS_TASK_BROKER_URI=http://your-n8n:5679 \
  -p 5680:5680 \
  lunare/n8n-runners-debian:2.1.4
```

**Playwright 镜像（支持浏览器自动化）：**
```bash
docker run -d \
  -e N8N_RUNNERS_AUTH_TOKEN=your-token \
  -e N8N_RUNNERS_TASK_BROKER_URI=http://your-n8n:5679 \
  -p 5680:5680 \
  lunare/n8n-runners-playwright:2.1.4
```

**Python 镜像（包含数据处理库）：**
```bash
docker run -d \
  -e N8N_RUNNERS_AUTH_TOKEN=your-token \
  -e N8N_RUNNERS_TASK_BROKER_URI=http://your-n8n:5679 \
  -p 5680:5680 \
  lunare/n8n-runners-python:2.1.4
```

## 镜像特性

### Debian 基础镜像
- 基于 Debian 11 bullseye-slim
- 支持 JavaScript 和 Python 代码执行
- 包含系统级 FFMPEG

### Playwright 扩展镜像
基于基础镜像，额外包含：
- `playwright` - 浏览器自动化
- `markdown` - Markdown 处理
- `Pillow` - 图像处理
- `imageio-ffmpeg` - FFMPEG Python 库

### Python 扩展镜像
基于基础镜像，额外包含：
- `markdown` - Markdown 处理
- `Pillow` - 图像处理
- `imageio-ffmpeg` - FFMPEG Python 库
- `numpy` - 数据科学库

### 离线安装

下载 Release 中的 tar 文件，然后加载：

```bash
# 加载基础镜像
docker load -i n8n-runners-debian-amd64.tar
docker load -i n8n-runners-debian-arm64.tar

# 加载 Playwright 镜像
docker load -i n8n-runners-playwright-amd64.tar
docker load -i n8n-runners-playwright-arm64.tar

# 加载 Python 镜像
docker load -i n8n-runners-python-amd64.tar
docker load -i n8n-runners-python-arm64.tar
```

## 构建

本项目通过 GitHub Actions 自动从 [n8n-io/n8n](https://github.com/n8n-io/n8n) 官方源码构建并发布镜像。
