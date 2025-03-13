# VSCode 入门指南

Visual Studio Code（简称 VSCode）是一款由微软开发的免费、开源的代码编辑器。它支持多种编程语言，拥有丰富的插件生态系统，并且可以在 Windows、macOS 和 Linux 上运行。无论你是初学者还是经验丰富的开发者，VSCode 都能帮助你更高效地编写代码。

本指南将带你了解 VSCode 的基本功能和使用方法，帮助你快速上手。

## 1. 安装 VSCode

### Windows/macOS/Linux

1. 访问 [VSCode 官方网站](https://code.visualstudio.com/)。
2. 根据你的操作系统下载对应的安装包。
3. 运行安装包并按照提示完成安装。

## 2. 首次启动

安装完成后，启动 VSCode。你将看到一个简洁的界面，包含以下主要区域：

- **侧边栏**：包含文件资源管理器、搜索、源代码管理等功能。
- **编辑区域**：用于编写和编辑代码。
- **状态栏**：显示当前文件的状态、编码格式、行号等信息。
- **活动栏**：位于最左侧，用于切换不同的功能视图。

## 3. 基本操作

### 3.1 打开文件夹

1. 点击左上角的“文件”菜单，选择“打开文件夹”。
2. 选择你存放代码的文件夹，点击“选择文件夹”。

### 3.2 创建新文件

1. 在侧边栏的文件资源管理器中，右键点击文件夹或空白区域，选择“新建文件”。
2. 输入文件名并按下回车。

### 3.3 保存文件

1. 按下 `Ctrl + S`（Windows/Linux）或 `Cmd + S`（macOS）。
2. 如果是首次保存，VSCode 会提示你选择保存位置和文件名。

### 3.4 打开终端

1. 按下 ``Ctrl + ` ``（Windows/Linux）或 ``Cmd + ` ``（macOS）。
2. 终端会在编辑区域底部打开，你可以在这里运行命令行工具。

## 4. 常用快捷键

| 功能                   | 快捷键 (Windows/Linux) | 快捷键 (macOS)       |
|------------------------|------------------------|----------------------|
| 新建文件               | `Ctrl + N`             | `Cmd + N`            |
| 打开文件               | `Ctrl + O`             | `Cmd + O`            |
| 保存文件               | `Ctrl + S`             | `Cmd + S`            |
| 保存所有文件           | `Ctrl + K S`           | `Cmd + K S`          |
| 查找                   | `Ctrl + F`             | `Cmd + F`            |
| 替换                   | `Ctrl + H`             | `Cmd + H`            |
| 打开命令面板           | `Ctrl + Shift + P`     | `Cmd + Shift + P`    |
| 切换侧边栏             | `Ctrl + B`             | `Cmd + B`            |
| 打开终端               | `Ctrl + ```           | `Cmd + ```           |
| 关闭当前标签页         | `Ctrl + W`             | `Cmd + W`            |
| 重开最近关闭的标签页   | `Ctrl + Shift + T`     | `Cmd + Shift + T`    |
| 格式化代码             | `Shift + Alt + F`      | `Shift + Option + F` |

## 5. 扩展插件

VSCode 的扩展插件极大地增强了其功能。以下是安装和使用插件的基本步骤：

1. 点击侧边栏中的“扩展”图标（或按下 `Ctrl + Shift + X` / `Cmd + Shift + X`）。
2. 在搜索框中输入你需要的插件名称，例如“Python”。
3. 点击“安装”按钮。
4. 安装完成后，VSCode 会自动启用插件。

### 推荐插件

(this is just an example, you can modify it)

- **Python**：Python 语言支持。
- **Prettier**：代码格式化工具。
- **ESLint**：JavaScript 代码检查工具。
- **GitLens**：增强 Git 功能。
- **Bracket Pair Colorizer**：给括号加上不同的颜色，方便阅读。

## 6. 配置文件

VSCode 的许多设置可以通过配置文件进行自定义。

1. 按下 `Ctrl + Shift + P` / `Cmd + Shift + P`，输入“Preferences: Open Settings (JSON)”。
2. 你将看到一个 `settings.json` 文件，在这里可以添加或修改配置。

### 示例配置

```json
{
  "editor.fontSize": 14,
  "editor.tabSize": 2,
  "files.autoSave": "onFocusChange",
  "workbench.colorTheme": "One Dark Pro"
}
```

## 7. 版本控制

VSCode 内置了 Git 支持，可以方便地进行版本控制。

1. 点击侧边栏中的“源代码管理”图标（或按下 `Ctrl + Shift + G` / `Cmd + Shift + G`）。
2. 你可以在这里查看文件的改动、提交更改、推送代码等。

## 8. 调试功能

VSCode 提供了强大的调试功能，支持多种编程语言。

1. 点击侧边栏中的“调试”图标（或按下 `Ctrl + Shift + D` / `Cmd + Shift + D`）。
2. 点击“创建一个 launch.json 文件”，选择你的调试环境。
3. 配置好调试设置后，点击“开始调试”按钮。

## 9. 自定义主题

你可以根据自己的喜好更改 VSCode 的外观。

1. 按下 `Ctrl + Shift + P` / `Cmd + Shift + P`，输入“Preferences: Color Theme”。
2. 选择一个你喜欢的主题，VSCode 会立即应用。

## 10. 社区与支持

VSCode 拥有活跃的社区和丰富的文档资源，遇到问题时可以参考以下资源：

- [官方文档](https://code.visualstudio.com/docs)
- [GitHub 仓库](https://github.com/microsoft/vscode)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/vscode)
