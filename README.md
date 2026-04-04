# aipic

Flutter 跨端 **AI 相机** 应用（iOS / Android），主打成片「高级感」与端侧 **AI 构图辅助**。

- 开发计划：[docs/Flutter_AI_相机_开发计划.md](docs/Flutter_AI_相机_开发计划.md)

首次在本机提交前，请将 Git 用户名与邮箱设为你自己的（若未配置全局身份）：

```bash
git config user.name "你的名字"
git config user.email "你的邮箱"
```

## 环境要求

- [Flutter](https://docs.flutter.dev/get-started/install)（稳定版）
- Xcode（macOS，用于 iOS）
- Android Studio / Android SDK（用于 Android）

## 克隆与运行

```bash
git clone <你的仓库 URL>
cd aipic
flutter pub get
flutter run
```

> 仓库初始化后若尚未执行 `flutter create`，请先按开发计划完成脚手架，再补充依赖与运行命令。

## 推送到 GitHub（维护者）

若本地已 `git init` 并完成首次提交，在 GitHub 新建空仓库后执行：

```bash
git remote add origin https://github.com/<用户或组织>/<仓库名>.git
git branch -M main
git push -u origin main
```

若已安装 [GitHub CLI](https://cli.github.com/)，也可：`gh repo create <仓库名> --private --source=. --remote=origin --push`
