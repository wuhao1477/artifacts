# 🚀 官方构建产物分发中心

本仓库**只托管构建产物**，不放任何源码。源码在各私有仓库开发，构建完成后由 CI 跨仓库投递到这里。

- **公开**：任何人不登录即可下载
- **隔离**：一个项目一个**孤立分支**（Orphan Branch），项目之间没有共同 Git 祖先，互不污染
- **不抢 Latest**：所有 Release 都 `make_latest=false`，避免 A 项目的小更新冲掉 B 项目的高亮状态
- **机器可读**：`index.json` 汇总所有项目的最新版本；`<project>/version.json` 是单项目清单（供自动更新客户端直接读取）

---

## 📦 项目下载导航

| 项目 | 说明 | 支持平台 | 下载 | 自动更新清单 |
| :--- | :--- | :--- | :--- | :--- |
| **baidupan-checkin** | 百度网盘自动签到（纯协议，Bun/TS） | 🐧 Linux x64/arm64 (glibc/musl)<br>🍏 macOS arm64/x64<br>🪟 Windows x64 | [📂 浏览所有版本](https://github.com/wuhao1477/artifacts/releases?q=baidupan-checkin-) | [`baidupan-checkin/version.json`](./baidupan-checkin/version.json) |

> 💡 点上面的「浏览所有版本」，GitHub 会按 `baidupan-checkin-` 前缀过滤，得到完全独立的单项目版本页。

---

## 🔗 直链规则（可写进脚本/自动更新客户端）

```
Release 页  : https://github.com/wuhao1477/artifacts/releases/tag/<project>-v<version>
下载某产物  : https://github.com/wuhao1477/artifacts/releases/download/<project>-v<version>/<asset>
校验和      : https://github.com/wuhao1477/artifacts/releases/download/<project>-v<version>/SHA256SUMS.txt
单项目清单  : https://raw.githubusercontent.com/wuhao1477/artifacts/main/<project>/version.json
```

Tag 命名规范：**`<project>-v<semver>`**（例：`baidupan-checkin-v0.6.0-alpha.6`）。
产物名规范：**`<project>-<平台>-<架构>[-<libc>][.exe]`**（例：`baidupan-checkin-linux-x64-musl`），保证同一个项目的产物在版本间保持同名，客户端才能自动更新。

---

## 🧭 分支说明

| 分支 | 作用 | 内容 |
| :--- | :--- | :--- |
| `main` | 全局门户 + 版本管理 | 本 `README.md`、`index.json`、各项目 `version.json`。**不放任何二进制** |
| `<project>-release` | 单项目发布锚点（孤立分支） | 仅一个占位 `README.md`。Release 的 `target_commitish` 指向它，保证项目间 Git 树完全平行 |

新增项目时**不要新建仓库**，只要：`git checkout --orphan <project>-release` → push → 在 `main/README.md` 加一行 → 在 CI 里把 `target_commitish` 指向该分支。
