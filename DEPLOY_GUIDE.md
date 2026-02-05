# GitHub Actions 部署指南 (Run on GitHub Actions)

本项目已配置 GitHub Actions 工作流，利用 GitHub 免费资源自动运行 `oci-help`。

## 1. 推送代码到 GitHub

你需要拥有自己的 GitHub 仓库。

```bash
# 1. 初始化 Git (如果尚未初始化)
git init

# 2. 关联你的 GitHub 仓库 (请替换 <URL>)
# 如果你是 Fork 的项目，可以忽略这一步，直接 Push
git remote set-url origin <你的仓库SSH或HTTPS地址>

# 3. 提交并推送
git add .
git commit -m "Add GitHub Actions workflow"
git push -u origin main
```

## 2. 配置 Secrets (关键步骤)

为了安全起见，`oci-help.ini` 配置文件（包含 API Key 和敏感信息）不能直接上传到公开仓库。你需要将其作为 Secret 存储。

1. 打开你的 GitHub 仓库页面。
2. 点击顶部导航栏的 **Settings**。
3. 在左侧菜单中找到 **Secrets and variables** -> **Actions**。
4. 点击 **New repository secret** 按钮。
5. 填写以下信息：
    - **Name**: `OCI_CONFIG`
    - **Secret**: (粘贴你本地 `oci-help.ini` 文件的完整内容)
6. 点击 **Add secret** 保存。

## 3. 运行与验证

配置完成后，GitHub Actions 会根据 `.github/workflows/oci-help.yml` 中的设置自动运行。

- **自动运行**: 默认设置为每 6 小时运行一次 (`0 */6 * * *`)。
- **手动触发**:
    1. 点击仓库顶部的 **Actions** 标签。
    2. 在左侧选择 **Run OCI Help** 工作流。
    3. 点击右侧的 **Run workflow** 按钮，选择分支并确认为绿色按钮 **Run workflow**。

## 常见问题

- **日志查看**: 在 Actions 页面点击运行中的 Job，可以查看控制台输出。
- **运行时间限制**: GitHub Actions 单次运行上限为 6 小时。脚本配置了超时保护。
- **封号风险**: 请勿用于极高频或滥用资源的操作。
