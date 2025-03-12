# Git 完全指南

![Git Logo](https://git-scm.com/images/logo@2x.png)

> 本文档适用于 Git 2.x 及以上版本，涵盖日常开发中最常用的 90% 场景。

---

## 目录

1. [安装与配置](#安装与配置)
2. [仓库基础操作](#仓库基础操作)
3. [提交管理](#提交管理)
4. [分支管理](#分支管理)
5. [远程仓库](#远程仓库)
6. [撤销操作](#撤销操作)
7. [标签管理](#标签管理)
8. [高级技巧](#高级技巧)
9. [最佳实践](#最佳实践)
10. [学习资源](#学习资源)

---

## 安装与配置

### 1. 安装 Git

- **Windows**: [官网下载](https://git-scm.com/downloads)
- **macOS**:

  ```bash
  brew install git
  ```

- **Linux**:

  ```bash
  sudo apt-get install git  # Ubuntu/Debian
  sudo yum install git      # CentOS/Fedora
  ```

### 2. 全局配置

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global core.editor "code --wait"  # 设置VS Code为默认编辑器
git config --global init.defaultBranch main    # 设置默认分支为main
```

### 3. 查看配置

```bash
git config --list
```

---

## 仓库基础操作

### 1. 初始化仓库

```bash
mkdir my-project && cd my-project
git init
```

### 2. 克隆仓库

```bash
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git my-folder  # 克隆到指定目录
```

### 3. 文件状态

| 命令 | 说明 |
|------|------|
| `git status` | 查看工作区状态 |
| `git status -s` | 简洁状态显示 |

---

## 提交管理

### 1. 添加文件到暂存区

```bash
git add file.txt        # 添加单个文件
git add .               # 添加所有修改
git add *.js            # 添加所有js文件
git add -u              # 添加已跟踪文件的修改
```

### 2. 提交更改

```bash
git commit -m "描述信息"           # 标准提交
git commit -a -m "快速提交"       # 跳过git add，直接提交已跟踪文件
git commit --amend               # 修改最后一次提交
```

### 3. 查看提交历史

```bash
git log
git log --oneline                # 简洁模式
git log -p                       # 显示差异
git log --graph --all --decorate # 图形化分支历史
```

---

## 分支管理

### 1. 分支操作

| 命令 | 说明 |
|------|------|
| `git branch` | 查看本地分支 |
| `git branch feature` | 创建新分支 |
| `git checkout feature` | 切换分支 |
| `git checkout -b feature` | 创建并切换分支 |
| `git branch -d feature` | 删除分支 |
| `git branch -m old new` | 重命名分支 |

### 2. 合并分支

```bash
git checkout main
git merge feature
```

### 3. 解决冲突

1. 打开冲突文件，手动修改标记：

   ```text
   <<<<<<< HEAD
   Current change
   =======
   Incoming change
   >>>>>>> feature
   ```

2. 解决后提交：

   ```bash
   git add .
   git commit -m "解决合并冲突"
   ```

---

## 远程仓库

### 1. 管理远程

```bash
git remote add origin https://github.com/user/repo.git  # 添加远程仓库
git remote -v                                          # 查看远程仓库
git remote remove origin                               # 删除远程仓库
```

### 2. 推送与拉取

```bash
git push origin main           # 推送到远程分支
git push -u origin main        # 设置上游分支（首次推送）
git pull origin main           # 拉取并合并远程更改
git fetch origin               # 仅获取远程更新不合并
```

### 3. 多人协作流程

```bash
# 1. 获取最新代码
git fetch origin

# 2. 合并到本地分支
git merge origin/main

# 3. 或使用 rebase 保持历史整洁
git rebase origin/main

# 4. 解决冲突后推送
git push origin main
```

---

## 撤销操作

### 1. 工作区撤销

```bash
git restore file.txt          # 撤销工作区修改
git restore --staged file.txt # 撤销暂存区修改
```

### 2. 提交历史修改

```bash
git reset HEAD~1             # 软重置（保留修改）
git reset --hard HEAD~1      # 硬重置（丢弃修改）
git revert HEAD              # 创建新提交来撤销旧提交
```

---

## 标签管理

### 1. 创建标签

```bash
git tag v1.0.0               # 轻量标签
git tag -a v1.0.0 -m "正式版" # 附注标签
```

### 2. 推送标签

```bash
git push origin v1.0.0        # 推送单个标签
git push origin --tags        # 推送所有标签
```

---

## 高级技巧

### 1. 储藏修改

```bash
git stash                     # 储藏当前修改
git stash list                # 查看储藏列表
git stash apply               # 恢复最新储藏
git stash pop                 # 恢复并删除储藏
```

### 2. 二分查找

```bash
git bisect start
git bisect bad                # 标记当前为错误提交
git bisect good <commit-id>   # 标记已知正常提交
# Git会自动进行二分定位问题提交
git bisect reset              # 退出二分模式
```

### 3. 子模块管理

```bash
git submodule add https://github.com/user/repo.git
git submodule update --init --recursive
```

---

## 最佳实践

1. **提交规范**
   - 使用 [Conventional Commits](https://www.conventionalcommits.org/) 规范
   - 示例：`feat: 添加用户登录功能`

2. **分支策略**
   - `main`：生产环境代码
   - `develop`：开发分支
   - `feature/xxx`：功能分支
   - `hotfix/xxx`：紧急修复分支

3. **.gitignore 文件**

   ```text
   # 示例
   node_modules/
   *.log
   .env
   ```

---

## 学习资源

1. [Pro Git 中文版](https://git-scm.com/book/zh/v2)
2. [Git 官方文档](https://git-scm.com/docs)
3. [Learn Git Branching](https://learngitbranching.js.org/)
4. [Git 可视化学习](https://github.com/pcottle/learnGitBranching)
5. [Git Flight Rules](https://github.com/k88hudson/git-flight-rules)

---

> 最后更新：2023年8月 | 作者：AI助手 | 许可证：CC BY-NC-SA 4.0

这份文档包含：

1. 安装配置的详细步骤
2. 日常操作的命令速查
3. 分支管理的最佳实践
4. 高级功能的实用技巧
5. 可视化表格和代码示例
6. 延伸学习资源

可以通过以下方式使用：

1. 保存为 `Git-CheatSheet.md` 随时查阅
2. 打印成 PDF 作为速查手册
3. 配合实际项目操作练习
4. 根据团队需求定制内容
