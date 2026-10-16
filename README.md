# 泡泡课表 · Release 分发仓库

本仓库**只用于分发已签名的正式版 APK**，不含任何源码。应用源码在私有仓库中维护。

## 为什么单独开一个仓库

App 内置的「检查更新」用 GitHub API 匿名查询 `releases/latest`。
GitHub 的匿名 API **查不到私有仓库**（一律返回 404），所以必须有一个公开仓库来承载 Release。
而把源码仓库直接设为 public，会连带公开它的完整提交历史，因此拆成两个仓库。

## ⚠️ 硬规则：本仓库永远不要提交源码或敏感文件

Release 页面上那两个 `Source code (zip)` / `Source code (tar.gz)` **是 GitHub 为每个
Release 自动生成的，不在 assets 列表里，也无法删除或关闭**。它们的内容就是
**本仓库在该 tag 时的状态**。

本仓库目前只有一个 README，所以那两个压缩包解开来也就只有 `README.md`（约 1 KB），
不含任何源码 —— 已实测确认。

**但这意味着：往本仓库提交任何文件，都会立刻出现在这些压缩包里，而且和 git 历史一样难以收回。**
源码留在私有仓库，这里只放发布产物。

## 安装

到 [Releases](../../releases) 下载最新的 `.apk`，传到手机安装即可。

- 要求 Android 8.0（API 26）及以上
- 包名 `com.linan.coursetable`
- 自 v1.2 起使用正式 release 签名；v1.0 / v1.1 为 debug 签名，
  因此**从 v1.0 / v1.1 升级到 v1.2 必须先卸载旧版本**

## 发布流程（维护者）

在源码仓库打 tag、构建出签名 APK 后：

```bash
gh release create v1.2 dist/paopao-schedule-v1.2.apk \
  --repo cedarln/paopao_schedule_releases \
  --title "v1.2" \
  --notes "本次改动……" \
  --latest
```

约定：

- **只上传 release 正式签名的 APK**，不要上传 debug 包
- tag 用 `vX.Y` 格式（App 里的版本比较依赖 tag 里的数字）
- 资产文件名以 `.apk` 结尾（App 取 assets 里第一个 `.apk`）
