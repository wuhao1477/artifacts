# baidupan-checkin — 发布专属孤立分支

这个分支**不是给人看的代码分支**，它只是 `baidupan-checkin` 这个项目在公开产物库里的
**发布锚点（target_commitish）**。

## 为什么需要它

`wuhao1477/artifacts` 用**一个项目一个孤立分支**来隔离：

- 孤立分支（Orphan Branch）没有父提交，与其他项目**没有共同 Git 祖先**
- 每次发布时 Release 的 `target_commitish` 指向本分支
- 于是 `baidupan-checkin` 的 tag/commit 历史**永远不会**和别的项目交织在一起
- 也让 `git log`、`git tag`、发布页过滤都保持干净

## 产物在哪

产物在 **Releases**（不放在这个分支的文件树里 —— 单个二进制 ~100MB，
放进 Git 树会让仓库膨胀到不可用）：

- Tag 规范：`baidupan-checkin-v<semver>`，例如 `baidupan-checkin-v0.6.0-alpha.6`
- 产物名规范：`baidupan-checkin-<平台>-<架构>[-<libc>][.exe]`，**版本间保持同名**，
  这样自动更新客户端才能按固定名字取到新版本

## 相关链接

- 下载大厅：<https://github.com/wuhao1477/artifacts>
- 机器可读清单：<https://raw.githubusercontent.com/wuhao1477/artifacts/main/baidupan-checkin/version.json>
- 源码库（私有）：`wuhao1477/baidu-netdisk-checkin`
