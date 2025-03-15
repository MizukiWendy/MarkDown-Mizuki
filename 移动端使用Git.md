# 移动端克隆 GitHub 仓库指南

> 以下操作均在有魔法的情况下进行否则访问不到GitHub
---

## 目录

1. [准备工作](#准备工作)  
2. [生成并配置 SSH 密钥](#生成并配置-ssh-密钥)  
3. [克隆 GitHub 仓库](#克隆-github-仓库)  
4. [日常同步操作](#日常同步操作)  
5. [常见问题解决](#常见问题解决)  
6. [注意事项](#注意事项)  

---

## 准备工作

### 1. 安装 Termux（Android）

- **下载地址**：
  - [Google Play](https://play.google.com/store/apps/details?id=com.termux)

### 2. 安装 Git 和基础工具

```bash
pkg update && pkg upgrade  # 更新软件包列表
pkg install git openssh    # 安装 Git 和 SSH
```

### 3. 授予 Termux 存储权限

```bash
termux-setup-storage
```

- 允许 Termux 访问手机存储（弹出权限请求时点击允许）。

---

## 生成并配置 SSH 密钥

> 因为 GitHub 从 2021 年 8 月 13 日 开始移除了对密码认证的支持。现在，使用 HTTPS 克隆 GitHub 仓库时，必须使用 Personal Access Token (PAT) 或 SSH 进行认证。

### 1. 生成 SSH 密钥对

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

- **参数说明**
  - -t ed25519：指定密钥类型为 ED25519（推荐）。
  - -C "<your_email@example.com>"：添加注释（通常为邮箱）。
  - -f /path/to/custom_key_name：指定密钥文件的路径和名称。

- **操作说明**：
  - 输入路径回车选择密钥文件保存的路径（`/storage/emulated/0/SSH/ssh`）。
  - **特别强调！这个路径的文件在指令执行之前应该是不存在的，系统会自动创建这个目录来放置SSH密钥文件**
  - 设置密码（可选）：输入密码或直接回车留空。
  - 确认密码（如设置）。

如果之前你已经创建了文件夹来放置就会出现以下对话

```bash
.../0/Obsidian $ ssh-keygen -t ed25519 -C "your_email@example.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/data/data/com.termux/files/home/.ssh/id_ed25519): /storage/emulated/0/SSH
/storage/emulated/0/SSH already exists.
Overwrite (y/n)? y
Enter passphrase for "/storage/emulated/0/SSH" (empty for no passphrase):回车不设密码
```

这个错误表明你尝试将 SSH 密钥保存到一个已经存在的目录（`/storage/emulated/0/SSH`），而不是一个文件。`ssh-keygen` 期望的是一个文件路径，而不是目录路径。

#### **在 `/storage/emulated/0/SSH` 目录的子目录生成密钥**

1. 重新在指定目录 /storage/emulated/0/SSH/ssh 生成名称为 ssh 的密钥：

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com" -f /storage/emulated/0/SSH
   ```

 按照提示输入密码（或直接按回车留空不设密码）。

---

### 2. 查看并复制公钥

```bash
cat /storage/emulated/0/SSH/ssh.pub
```

- 复制输出的内容（以 `ssh-ed25519` 开头备注邮箱为结尾）。

### 3. 将公钥添加到 GitHub

1. 登录 GitHub，进入 [SSH Keys 设置页面](https://github.com/settings/keys)。
2. 点击 **New SSH Key**。
3. 输入标题（如 `Termux-Mobile`），粘贴复制的公钥。
4. 点击 **Add SSH Key**。

### 4. 配置 SSH 代理

```bash
eval $(ssh-agent)          # 启动 SSH 代理
ssh-add /storage/emulated/0/SSH/ssh  # 添加私钥到代理
```

- 如果设置了密码，需输入密码。

---

## 克隆 GitHub 仓库

### 1. 切换至目标目录

一般安卓手机的内部存储设备都是这个路径，可以根据需要添加文件路径后缀

```bash
cd /storage/emulated/0/   # 进入手机内部存储根目录
```

### 2. 执行克隆命令

```bash
git clone git@github.com:用户名/仓库名.git
```

- **示例**：

  ```bash
  git clone git@github.com:MizukiWendy/MyProject.git
  ```

### 3. 首次连接确认

```text
The authenticity of host 'github.com (IP)' can't be established.
ED25519 key fingerprint is SHA256:xxx...
Are you sure you want to continue (yes/no)?
```

- 输入 `yes` 并回车以信任 GitHub 服务器。

---

## 日常同步操作

### 1. 拉取远程更新

```bash
cd /path/to/repo     # 进入仓库目录
git pull origin main # 拉取最新内容（分支名需与远程一致）
```

### 2. 提交本地更改

```bash
git add .                        # 添加所有修改到暂存区
git commit -m "提交描述"         # 提交更改
git push origin main             # 推送至远程仓库
```

### 3. 处理冲突

```bash
git pull origin main             # 先拉取最新内容
# 手动解决冲突后提交
git add .
git commit -m "解决冲突"
git push origin main
```

---

## 常见问题解决

### 1. 错误：`Permission denied (publickey)`

- **检查项**：
  - 公钥是否完整添加到 GitHub。
  - 私钥是否加载到 SSH 代理（`ssh-add -l` 查看）。
  - 测试连接：`ssh -T git@github.com`。

### 2. 错误：`src refspec main does not match any`

- **原因**：本地分支名与远程不一致（如远程为 `master`）。
- **解决**：

  ```bash
  git push origin master  # 推送至 master 分支
  ```

### 3. 克隆卡顿或无响应

- **尝试浅克隆**：

  ```bash
  git clone --depth 1 git@github.com:用户/仓库.git
  ```

- **检查网络**：

  ```bash
  ping github.com  # 确保网络连通
  ```

### 4. 文件换行符警告

```text
warning: LF will be replaced by CRLF
```

- **禁用自动转换**：

  ```bash
  git config --global core.autocrlf false
  ```

---

## 注意事项

1. **文件权限管理**  
   - 私钥权限设为 `600`：

     ```bash
     chmod 600 ~/.ssh/id_ed25519
     ```

   - 避免系统应用误修改仓库文件。

2. **冲突处理策略**  
   - 拉取前优先提交本地更改：

     ```bash
     git stash        # 暂存本地修改
     git pull         # 拉取远程更新
     git stash pop    # 恢复暂存内容
     ```

3. **备份建议**  
   - 定期压缩仓库备份：

     ```bash
     tar -czvf repo-backup-$(date +%Y%m%d).tar.gz /path/to/repo
     ```

4. **大文件处理**  
   - 超过 100MB 的文件建议使用 [Git LFS](https://git-lfs.com/)。

5. **安全提示**  
   - 私钥文件（`ssh`）禁止外泄。
   - 敏感数据勿提交至公开仓库。

---
