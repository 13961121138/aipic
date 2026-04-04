# GitHub 从零配置与推送（Windows）

> **关于 MCP**：若 Cursor 里的 GitHub MCP 显示异常，无法在 IDE 内一键建库时，请按本文在浏览器与终端完成；修好 MCP 后也只能在**已登录**的前提下辅助部分操作，**账号、令牌、首次推送**仍须你本人确认。

## 一、准备：Git 已安装

在 PowerShell 中执行：

```powershell
git --version
```

若提示找不到命令，请先安装 [Git for Windows](https://git-scm.com/download/win)，安装时勾选 **Git Credential Manager**（便于保存 GitHub 密码/令牌）。

---

## 二、注册并登录 GitHub

1. 打开 [https://github.com](https://github.com)  
2. 注册账号（Sign up）或使用已有账号登录（Sign in）。

---

## 三、在网页上创建空仓库（不要初始化 README）

1. 登录后右上角 **+** → **New repository**。  
2. **Repository name** 填写例如：`aipic`（可自定，全小写无空格较省事）。  
3. 选 **Public** 或 **Private**（私有仅你邀请的人可见）。  
4. **不要**勾选 *Add a README*、*.gitignore*、*license*（避免与本地已有提交冲突）。  
5. 点击 **Create repository**。  
6. 创建成功后页面会显示仓库地址，复制 **HTTPS** 地址，形如：  
   `https://github.com/你的用户名/aipic.git`

---

## 四、身份：在本机设置 Git 用户名与邮箱

在项目目录打开 PowerShell：

```powershell
cd d:\mycode\cursor\aipic
git config user.name "你的 GitHub 显示名或昵称"
git config user.email "你在 GitHub 账号里绑定的邮箱"
```

（与 GitHub 邮箱一致可减少部分提示；也可用 GitHub 提供的 `@users.noreply.github.com` 隐私邮箱。）

---

## 五、用 HTTPS 推送（推荐新手）：个人访问令牌 PAT

从 2021 年起，GitHub **不再接受账户密码** 作为 Git 的 HTTPS 密码，需使用 **Personal Access Token (PAT)**。

1. 浏览器打开：  
   [https://github.com/settings/tokens](https://github.com/settings/tokens)  
2. **Generate new token** → 选 **Generate new token (classic)**。  
3. **Note**：随便填，如 `aipic-laptop`。  
4. **Expiration**：选合适过期时间。  
5. **勾选权限**：至少勾选 **`repo`**（完整仓库权限）。  
6. 生成后 **立刻复制令牌**（只显示一次），粘贴到安全处。

### 关联远程并推送

把下面命令里的 URL 换成你在「三」里复制的仓库地址：

```powershell
cd d:\mycode\cursor\aipic
git remote add origin https://github.com/你的用户名/aipic.git
git push -u origin main
```

- 若提示输入 **Username**：填你的 **GitHub 用户名**。  
- 若提示输入 **Password**：粘贴 **PAT**（不是你的登录密码）。

若已安装 **Git Credential Manager**，成功一次后一般会记住，不必每次粘贴。

---

## 六、可选：SSH 方式（免每次输 PAT，配置稍多）

1. 生成密钥（一路回车即可）：  
   `ssh-keygen -t ed25519 -C "你的邮箱"`  
2. 显示公钥内容并复制：  
   `Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub`  
3. GitHub → **Settings** → **SSH and GPG keys** → **New SSH key**，粘贴保存。  
4. 远程地址使用 SSH：  
   `git remote add origin git@github.com:你的用户名/aipic.git`  
5. `git push -u origin main`

---

## 七、验证

推送成功后，在浏览器打开你的仓库页，应能看到 `README.md`、`docs/` 等文件。

---

## 八、邀请他人协作

仓库页 → **Settings** → **Collaborators**（个人仓库）或组织权限管理 → 添加对方 GitHub 账号，对方 **Accept** 后即可 `git clone` 与推送（对方也需配置 PAT 或 SSH）。

---

## 常见问题

| 现象 | 处理 |
|------|------|
| `remote origin already exists` | 先执行 `git remote remove origin`，再重新 `git remote add origin ...` |
| `failed to push ... rejected` | 若远程先有提交，需先 `git pull origin main --rebase` 再推送；空仓库一般不会 |
| 认证失败 | 确认使用 **PAT** 而非密码；或检查令牌是否过期、是否勾选 `repo` |
