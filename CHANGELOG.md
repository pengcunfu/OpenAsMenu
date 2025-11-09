# 更新日志

所有重要的项目变更都将记录在此文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)，
并且本项目遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [Unreleased]

### 新增
- GitHub Actions 自动构建和发布工作流

## [1.0.0] - YYYY-MM-DD

### 新增
- ✨ 右键菜单管理功能
  - 添加、删除、修改自定义右键菜单项
  - 支持文件和目录分别配置
  - 实时状态检测和刷新
  
- ✨ Win11 菜单样式切换
  - 在 Win11 简化菜单和完整菜单之间切换
  - 自动重启资源管理器应用更改
  - 系统兼容性自动检测
  
- ✨ 配置管理
  - JSON 格式配置文件
  - 预设常用 IDE 和编辑器配置
  - 配置导入导出支持
  
- ✨ 用户界面
  - 现代化 WPF 界面设计
  - 响应式布局
  - 完整的错误处理和用户提示
  
- 🔒 安全特性
  - 管理员权限自动检测和提升
  - 路径验证和文件存在性检查
  - 注册表访问权限测试

### 技术栈
- .NET 8.0 + WPF
- Microsoft.Win32.Registry 5.0.0
- Newtonsoft.Json 13.0.3

### 系统要求
- Windows 7 或更高版本
- .NET 8.0 运行时（Framework-Dependent 版本）
- 管理员权限

---

## 版本说明

### Self-Contained（独立版本）
- 包含完整的 .NET 运行时
- 无需安装 .NET
- 文件体积较大（约 100MB+）
- 推荐给普通用户使用

### Framework-Dependent（依赖版本）
- 需要安装 .NET 8.0 运行时
- 文件体积较小（约 1-2MB）
- 推荐给开发者或已安装 .NET 的用户

---

## 贡献指南

欢迎提交 Issue 和 Pull Request！

### 提交 Issue
- 请详细描述问题和复现步骤
- 提供系统版本和错误信息
- 如有可能，附上截图

### 提交 Pull Request
- Fork 本仓库
- 创建特性分支 (`git checkout -b feature/AmazingFeature`)
- 提交更改 (`git commit -m 'Add some AmazingFeature'`)
- 推送到分支 (`git push origin feature/AmazingFeature`)
- 开启 Pull Request

---

[Unreleased]: https://github.com/yourusername/OpenAsMenu/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/yourusername/OpenAsMenu/releases/tag/v1.0.0
