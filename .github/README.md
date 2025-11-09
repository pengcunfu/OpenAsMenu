# GitHub 工作流说明

本目录包含 OpenAsMenu 项目的 GitHub Actions 工作流配置和相关文档。

## 📁 文件结构

```
.github/
├── workflows/
│   ├── build-and-release.yml  # 自动构建和发布工作流
│   └── ci.yml                 # 持续集成工作流
├── RELEASE.md                 # 发布指南
├── USAGE.md                   # 使用指南
└── README.md                  # 本文件
```

## 🚀 工作流说明

### 1. Build and Release (build-and-release.yml)

**触发条件**：
- 推送版本标签（如 `v1.0.0`）
- 手动触发

**功能**：
- ✅ 编译 .NET 8.0 WPF 项目
- ✅ 生成两个版本：
  - Self-Contained（独立版本，包含运行时）
  - Framework-Dependent（依赖版本，需要 .NET 8.0）
- ✅ 创建 GitHub Release
- ✅ 上传编译好的 ZIP 文件
- ✅ 保留构建产物 30 天

**输出文件**：
- `OpenAsMenu-{version}-win-x64-self-contained.zip`
- `OpenAsMenu-{version}-win-x64-framework-dependent.zip`

### 2. CI Build (ci.yml)

**触发条件**：
- 推送到 main/master/develop 分支
- 提交 Pull Request

**功能**：
- ✅ 验证代码可以成功编译
- ✅ 测试构建输出
- ✅ 不创建 Release（仅用于测试）

## 📝 如何发布新版本

### 快速发布

```bash
# 1. 提交所有更改
git add .
git commit -m "准备发布 v1.0.0"
git push origin main

# 2. 创建并推送标签
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0

# 3. 等待 GitHub Actions 自动构建和发布
```

### 详细步骤

查看 [RELEASE.md](RELEASE.md) 获取完整的发布指南。

## 📖 文档

- **[RELEASE.md](RELEASE.md)** - 详细的发布流程和故障排查
- **[USAGE.md](USAGE.md)** - 用户使用指南
- **[../CHANGELOG.md](../CHANGELOG.md)** - 版本更新日志

## 🔧 配置说明

### 必需的 Secrets

工作流使用 GitHub 自动提供的 `GITHUB_TOKEN`，无需额外配置。

### 权限要求

确保仓库设置中启用了以下权限：
1. Settings → Actions → General
2. Workflow permissions → Read and write permissions
3. 勾选 "Allow GitHub Actions to create and approve pull requests"

## 🎯 版本号规范

使用语义化版本号：

- `v1.0.0` - 正式版本
- `v1.0.0-beta.1` - Beta 版本
- `v1.0.0-rc.1` - Release Candidate 版本

格式：`v{major}.{minor}.{patch}[-{prerelease}]`

## 🛠️ 本地测试

### 测试编译

```bash
# 恢复依赖
dotnet restore OpenAsMenu/OpenAsMenu.csproj

# 编译
dotnet build OpenAsMenu/OpenAsMenu.csproj --configuration Release

# 发布（独立版本）
dotnet publish OpenAsMenu/OpenAsMenu.csproj `
  --configuration Release `
  --runtime win-x64 `
  --self-contained true `
  --output ./publish/win-x64 `
  -p:PublishSingleFile=true
```

### 测试工作流

使用 [act](https://github.com/nektos/act) 在本地运行 GitHub Actions：

```bash
# 安装 act
choco install act-cli

# 测试 CI 工作流
act push -W .github/workflows/ci.yml

# 测试发布工作流（需要标签）
act push -W .github/workflows/build-and-release.yml
```

## 📊 构建状态

查看构建状态：
- 访问仓库的 [Actions](../../actions) 页面
- 查看最近的工作流运行记录
- 点击具体运行查看详细日志

## ❓ 常见问题

### Q: 为什么工作流没有触发？
A: 
- 检查标签格式是否为 `v*`（如 `v1.0.0`）
- 确认已推送标签到远程仓库
- 查看 Actions 页面是否有错误

### Q: 构建失败怎么办？
A:
1. 查看 Actions 日志
2. 检查 .NET SDK 版本
3. 验证项目文件路径
4. 确认依赖包版本

### Q: 如何修改发布说明？
A: 编辑 `build-and-release.yml` 中的 `body` 部分。

### Q: 如何添加更多平台支持？
A: 在工作流中添加新的 `dotnet publish` 步骤，指定不同的 `--runtime`。

## 🤝 贡献

欢迎改进工作流配置！

提交 PR 前请：
1. 测试工作流是否正常运行
2. 更新相关文档
3. 说明修改原因

## 📞 支持

遇到问题？
- 查看 [GitHub Actions 文档](https://docs.github.com/cn/actions)
- 提交 [Issue](../../issues)
- 参与 [Discussions](../../discussions)

---

**注意**：首次使用前，请将 README.md 中的 `yourusername` 替换为实际的 GitHub 用户名或组织名。
