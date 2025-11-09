# 发布指南

本文档说明如何使用 GitHub Actions 自动发布 OpenAsMenu 项目。

## 自动发布流程

### 方式一：通过 Git 标签触发（推荐）

1. **确保代码已提交并推送到主分支**
   ```bash
   git add .
   git commit -m "准备发布 v1.0.0"
   git push origin main
   ```

2. **创建版本标签**
   ```bash
   # 创建标签（使用语义化版本号）
   git tag -a v1.0.0 -m "Release version 1.0.0"
   
   # 推送标签到远程仓库
   git push origin v1.0.0
   ```

3. **自动构建和发布**
   - GitHub Actions 会自动检测到标签推送
   - 开始构建 Windows x64 版本（独立版和依赖版）
   - 创建 GitHub Release
   - 上传编译好的 ZIP 文件

### 方式二：手动触发

1. 访问 GitHub 仓库页面
2. 点击 **Actions** 标签
3. 选择 **Build and Release** 工作流
4. 点击 **Run workflow** 按钮
5. 选择分支并点击 **Run workflow**

## 版本号规范

使用 [语义化版本](https://semver.org/lang/zh-CN/) 规范：

- **主版本号（Major）**: 不兼容的 API 修改
- **次版本号（Minor）**: 向下兼容的功能性新增
- **修订号（Patch）**: 向下兼容的问题修正

示例：
- `v1.0.0` - 首个正式版本
- `v1.1.0` - 添加新功能
- `v1.1.1` - 修复 Bug
- `v2.0.0` - 重大更新，可能不兼容旧版本

## 发布前检查清单

- [ ] 代码已通过 CI 测试
- [ ] 更新 `CHANGELOG.md` 文件
- [ ] 更新 `README.md` 中的版本信息（如需要）
- [ ] 检查项目文件中的版本号
- [ ] 测试编译是否成功
- [ ] 确认所有依赖包版本正确

## 发布内容

每次发布会生成以下文件：

### 1. Self-Contained（独立版本）
- **文件名**: `OpenAsMenu-{version}-win-x64-self-contained.zip`
- **特点**: 
  - 包含 .NET 8.0 运行时
  - 单文件可执行程序
  - 无需安装 .NET
  - 文件较大（约 100MB+）

### 2. Framework-Dependent（依赖版本）
- **文件名**: `OpenAsMenu-{version}-win-x64-framework-dependent.zip`
- **特点**:
  - 需要安装 .NET 8.0 运行时
  - 文件较小（约 1-2MB）
  - 适合已安装 .NET 的用户

## 发布后操作

1. **验证 Release**
   - 检查 Release 页面是否正确创建
   - 下载并测试两个版本的 ZIP 文件
   - 确认程序可以正常运行

2. **更新文档**
   - 在 README.md 中添加下载链接
   - 更新版本徽章（如有）

3. **通知用户**
   - 在 Discussions 或 Issues 中发布更新公告
   - 社交媒体分享（如需要）

## 回滚发布

如果发现发布有问题：

1. **删除 Release**
   ```bash
   # 在 GitHub Release 页面删除发布
   ```

2. **删除标签**
   ```bash
   # 删除本地标签
   git tag -d v1.0.0
   
   # 删除远程标签
   git push origin :refs/tags/v1.0.0
   ```

3. **修复问题后重新发布**

## 预发布版本

创建预发布版本（Beta、RC 等）：

```bash
# 创建预发布标签
git tag -a v1.0.0-beta.1 -m "Beta release 1"
git push origin v1.0.0-beta.1
```

在 GitHub Release 中勾选 "This is a pre-release" 选项。

## 故障排查

### 构建失败
1. 检查 Actions 日志
2. 确认 .NET SDK 版本正确
3. 验证项目文件路径

### Release 创建失败
1. 检查 `GITHUB_TOKEN` 权限
2. 确认标签格式正确（v*）
3. 查看 Actions 日志中的错误信息

### 文件上传失败
1. 检查文件是否正确生成
2. 确认文件路径正确
3. 验证 ZIP 文件完整性

## 持续集成

- **CI 工作流**: 每次推送到主分支或 PR 时自动运行
- **构建测试**: 验证代码可以成功编译
- **不创建 Release**: 仅用于测试构建

## 相关链接

- [GitHub Actions 文档](https://docs.github.com/cn/actions)
- [语义化版本规范](https://semver.org/lang/zh-CN/)
- [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)
