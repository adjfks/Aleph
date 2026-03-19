---
date created: Friday, March 20th 2026, 12:51:13 am
date modified: Friday, March 20th 2026, 12:54:04 am
tags:
  - git
  - worktree
---


## 优势

| 本质优势           | 说明                                              |
| :------------- | :---------------------------------------------- |
| **共享 Git 数据库** | 多个工作目录共用同一个 `.git`，避免重复克隆                       |
| **分支真正并行**     | 各 worktree 独立检出不同分支，切换零成本，AI Agent 上下文不中断       |
| **秒级创建**       | 本地命令完成，无需网络下载                                   |
| **磁盘高效**       | 4 分支场景下，Worktree 方案（~85 GB）vs 重复 Clone（~328 GB） |
| **一键清理**       |                                                 |


## Worktrunk 安装与常用命令

```
# ========== 安装 ==========
# macOS / Linux（Homebrew）
brew install max-sixty/tap/worktrunk

# 或使用 cargo 从源码构建
cargo install worktrunk

# 命令行工具名为 wt


# ========== 常用命令 ==========

# 创建新分支并生成 worktree，自动切换目录
# 基于当前分支创建 feature-A，同级目录生成 my-project.feature-A/
wt switch -c feature-A

# 创建并自动启动 Claude（可选）
wt switch -x claude -c feature-A -- '实现功能 A'

# 查看当前所有 worktree 列表
wt list

# 切换到已有 worktree（模糊匹配）
wt switch feature-A

# 删除 worktree 并清理分支（配置了 hook 则自动清理 DerivedData）
wt remove feature-A

# 手动清理残留记录（若直接 rm -rf 删过目录）
git worktree prune
```