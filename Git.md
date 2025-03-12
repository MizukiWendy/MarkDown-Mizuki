# Git 完全指南

![Git Logo](https://git-scm.com/images/logo@2x.png)

> 本文档适用于 Git 2.x 及以上版本，涵盖日常开发中最常用的 90% 场景。

---

## 目录

1. [示例流程](#示例流程)
2. [仓库基础操作](#仓库基础操作)
3. [提交管理](#提交管理)
4. [分支管理](#分支管理)
5. [远程仓库](#远程仓库)
6. [撤销操作](#撤销操作)
7. [标签管理](#标签管理)
8. [高级技巧](#高级技巧)
9. [工作流程原理](#工作流程原理)
10. [工作流程示例](#工作流程示例)

---

## 示例流程

### 1. 代码托管平台创建仓库

- **GitHub**: 官网登录后点击绿色的**New**按钮创建仓库即可
注：若出现创建Repository name Couldn't check availability，切换浏览器或加速器节点即可。
- **Gitee**:官网登录后点击右上角+号并在二级菜单点击**新建仓库**即可

### 2. Git上传代码至仓库

- 在需要上传的文件目录下右键菜单选择**Open Git Bash here**打开Git控制台
- 初始化仓库

```bash
git init
```

   初始化之后可检查仓库状态

```bash
git status
```

   如果成功初始化，你会看到类似以下的输出：

```bash
On branch main
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

- 添加远程仓库

```bash
git remote add origin https://github.com//你的用户名/项目名称.git
```

- 重命名分支
将当前分支重命名为 main（如果默认分支不是 main），据说不用master是因为不尊重黑人？

```bash
git branch -M main
```

- 将文件添加到暂存区

```bash
git add .
```

- 提交更改

```bash
git commit -m "Your commit message"
```

注：**Your commit message**可以选择你完成的功能开发，比如**UI界面搭建**

- 推送代码到代码托管平台

```bash
git push -u origin main
```

   这里可能会报各种各样的错

```bash
fatal: unable to access 'https://github.com/MizukiWendy/MarkDown-Mizuki.git/': Failure when receiving data from the peer
```

   fatal: unable to access 错误表明 Git 无法连接到远程仓库，通常是由于网络问题或连接被阻止引起的。简单来讲就是与GitHub断开连接了。

```bash
fatal: unable to access 'https://github.com/MizukiWendy/MarkDown-Mizuki.git/': Failed to connect to github.com port 443 after 21081 ms: Couldn't connect to server
```

   fatal: unable to access 错误表明 Git 无法连接到 GitHub 服务器（github.com），具体原因是无法连接到端口 443，这通常与网络环境、防火墙、代理或 GitHub 服务问题有关。

至于**解决方法**嘛，等一段时间再试，或者换加速器节点

---

### 修改远程仓库平台

- 查看当前远程仓库

```bash
git remote -v
```

   如果原本是GitHub仓库，输出示例：

```bash
origin  https://github.com/你的用户名/项目名称.git (fetch)
origin  https://github.com/你的用户名/项目名称.git (push)
```

- 添加 Gitee 的远程仓库

```bash
git remote add gitee https://gitee.com/你的用户名/项目名称.git
```

   此时输入检查远程仓库就会多出来Gitee的远程仓库地址

```bash
git remote -v
```

```bash
origin  https://github.com/你的用户名/项目名称.git (fetch)
origin  https://github.com/你的用户名/项目名称.git (push)
gitee   https://gitee.com/你的用户名/项目名称.git (fetch)
gitee   https://gitee.com/你的用户名/项目名称.git (push)
```

- 推送代码到代码托管平台

```bash
git push -u gitee main
```

   这里大概弹窗让你再填写一下你的用户名和密码，正常填写之后就可以正常提交。

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
git push origin main           # 推送到GitHub
git push gitee main            # 推送到Gitee
git push --all                 # 推送到全部平台
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

## 工作流程原理

**每次修改都需要先提交到本地仓库，然后再推送到远程仓库**。这是 Git 的标准工作流程，分为以下几个步骤：

---

### **1. Git 的工作流程**

1. **修改文件**：在工作目录中编辑、添加或删除文件。
2. **添加到暂存区**：使用 `git add` 将修改的文件添加到暂存区（可以理解为“准备提交”）。
3. **提交到本地仓库**：使用 `git commit` 将暂存区的修改提交到本地仓库。
4. **推送到远程仓库**：使用 `git push` 将本地仓库的更改同步到远程仓库（如 GitHub 或 Gitee）。

---

### **2. 为什么需要先提交到本地仓库？**

- **版本控制**：Git 的核心功能是版本控制。提交到本地仓库会记录一个历史快照，方便你回滚或查看历史更改。
- **离线工作**：你可以在没有网络的情况下提交到本地仓库，等有网络时再推送。
- **灵活性**：本地提交可以在推送前多次修改或整理（如使用 `git commit --amend`），确保推送的提交是完整的、干净的。

---

## **工作流程示例**

假设你修改了一些文件，并希望推送到远程仓库，以下是完整的步骤：

### **步骤 1：查看修改状态**

```bash
git status
```

### **步骤 2：添加到暂存区**

```bash
git add 文件名
```

如果需要添加所有修改：

```bash
git add .
```

### **步骤 3：提交到本地仓库**

```bash
git commit -m "描述你的修改"
```

### **步骤 4：推送到远程仓库**

推送到 **GitHub**：

```bash
git push origin main
```

推送到 **Gitee**：

```bash
git push gitee main
```

---
