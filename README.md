# pageos-apps

pageos-apps 是一个为 PageOS 操作系统设计的官方网页应用仓库。它托管了登录界面、用户界面和各种依赖的软件包，旨在为这个基于 Arch Linux 的图形化发行版提供一个完整的网页应用生态系统。

- [应用列表](index.html)

## 架构概述

PageOS 采用了一种独特的架构：

- **显示层**：使用 Wayland 下的 cage 作为全屏显示管理器，启动 Firefox 浏览器在 kiosk 模式下运行。
- **用户界面**：整个用户交互界面是一个单页 HTML 应用，运行在 Firefox 中。
- **服务层**：通过 Rust 编写的双向服务端程序（如 `pageos-core`）使用 WebSocket 与前端页面进行双向通信，实现系统级功能（如重启、文件操作等）。

## 仓库结构

本仓库遵循特定的目录结构，以支持本地和在线应用仓库的功能：

```plaintext
.
├── config.toml               # 软件源配置文件
├── index.json                # 全局索引文件
└── packages/                 # 已安装的软件包
    └── pageos-hello/         # 软件包ID
        ├── 0.1.0/            # 版本号
        │   ├── index.html    # 应用入口文件
        │   └── metadata.json # 应用元信息
        └── versions.txt      # 版本清单
```

### 配置文件 (`config.toml`)

```toml
cache_dir = "/tmp/pageos-pkgr/cache"
source = []
```

### 索引文件 (`index.json`)

包含已安装包和软件源的全局索引：

```json
{
  "packages": [
    {
      "id": "pageos-hello",
      "name": "pageos-hello",
      "icon": "",
      "author": "PJ568",
      "latest_version": "0.1.0",
      "description": "A PageOS web application",
      "location": "./packages/pageos-hello/0.1.0"
    }
  ],
  "source": []
}
```

### 应用元信息 (`metadata.json`)

每个应用包都包含一个 `metadata.json` 文件，定义了应用的元数据：

```json
{
  "name": "PageOS Hello",
  "id": "pageos-hello",
  "version": "0.1.0",
  "description": "A PageOS web application",
  "icon": "",
  "author": "PJ568",
  "type": "webapp",
  "category": "",
  "permissions": [],
  "entry": "index.html",
  "all_files": {
    "index.html": "ecc74040554cea8ecb44458cfcd5757f1bd8c53c9bf2955d8c1f6fbf46e1497c"
  }
}
```

## 相关工具

### [`pageos-pkgr`](https://github.com/swaybien/pageos-pkgr)

Rust 语言编写的网页应用仓库管理程序，提供以下命令：

- `pageos-pkgr app init`: 初始化软件包
- `pageos-pkgr repo install`: 从源安装软件
- `pageos-pkgr repo upgrade`: 升级软件包
- `pageos-pkgr repo sync`: 同步软件源

## 开发与贡献

欢迎贡献新的网页应用。请遵循以下步骤：

0. 安装 [pageos-pkgr](https://github.com/swaybien/pageos-pkgr)
1. Fork 本仓库
2. 创建新分支 (`git checkout -b app/your-app`)
3. 实现你的功能或修复
4. 提交更改 (`git commit -am '【新增】Add my app'`)
5. 推送到分支 (`git push origin app/your-app`)
6. 创建 Pull Request

## 相关项目

- [pageos](https://github.com/swaybien/pageos): 基于 Arch Linux 的 PageOS 镜像维护仓库
- [pageos-core](https://github.com/swaybien/pageos-core): Web-Centric OS Framework
- [pageos-pkgr](https://github.com/swaybien/pageos-pkgr): 网页应用仓库管理程序
- [pageos-greet](https://github.com/swaybien/pageos-greet): 登录界面服务器
- [pageos-pkgr-ui](https://github.com/swaybien/pageos-pkgr-ui): 网页应用仓库管理程序 GUI
