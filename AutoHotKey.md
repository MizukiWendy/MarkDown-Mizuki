# AutoHotKey 使用文档

>*From Mizuki*
---

## 官方网站

**[AutoHotKey](https://www.autohotkey.com/)** ：<https://www.autohotkey.com>

## 使用流程

1. 官网下载安装 AutoHotkey
2. 打开AutoHotKey Dash
3. 点击New Script新建脚本文件
4. 编写代码
5. 双击运行

注：~~懒得写代码的直接问AI~~

## 使用示例

### 一、符号替换

#### 1、基础符号替换

**语法：**

```ahk
Hotstring(":*:被替换的字符", "替换成的字符")  ; 即时触发  
Hotstring("::被替换的字符", "替换成的字符")   ; 需按空格/Tab/回车触发  
```

**示例：**

```ahk
; 即时触发  
Hotstring(":*:;;r", "→")      ; →  
Hotstring(":*:;;eq", "＝")     ; 双等号  
Hotstring(":*:;;c", "℃")      ; 摄氏度  

; 手动触发  
Hotstring("::;;ok", "✓")      ; 输入;;ok后按空格生效  
Hotstring("::;;sig", "Best Regards{Enter}John")  ; 多行签名  
```

### 二、快捷键操作

#### 1. 打开程序/文件

```ahk
组合键::Run("可执行文件路径")  
```

**示例：**

```ahk
#n::Run("notepad.exe")                  ; Win+N打开记事本  
^!t::Run("wt.exe")                      ; Ctrl+Alt+T打开终端  
#g::Run("C:\Program Files\Google\...")  ; 带空格的路径需引号包裹  
```

#### 2. 管理员权限启动

```ahk
^!m::RunAs("taskmgr.exe")  ; Ctrl+Alt+M以管理员身份打开任务管理器  
```

### 三、窗口管理

#### 1. 窗口位置/大小调整

```ahk
热键::WinMove(X坐标, Y坐标, 宽度, 高度, "窗口标题")  
热键::WinMaximize("窗口标题")  ; 最大化  
热键::WinMinimize("窗口标题")  ; 最小化  
```

**示例：**

```ahk
^!#m::WinMove(0, 0, 800, 600, "A")   ; Ctrl+Alt+Win+M移动并缩放窗口  
^!Up::WinMaximize("A")               ; 最大化当前窗口  
^!Down::WinMinimize("A")             ; 最小化当前窗口  
```

#### 2. 窗口置顶/透明化

```ahk
^#t::WinSetAlwaysOnTop(-1, "A")     ; Ctrl+Win+T切换置顶  
^#7::WinSetTransparent(200, "A")    ; 设置半透明（200为透明度值）  
```

#### 3. 窗口切换与激活

```ahk
#q::Send("!{Tab}")                  ; Win+Q模拟Alt+Tab  
#c::WinActivate("ahk_exe chrome.exe")  ; Win+C激活Chrome窗口  
```

### 四、其他常用功能

#### 1. 文本快速输入

```ahk
:*:触发字符::  
{
    代码块（支持多行操作）  
}  
```

**示例：**

```ahk
:*:;;vdate::
{
    Send(FormatTime(, "yyyy-MM-dd HH:mm:ss"))  ; 输入当前日期和时间
}

:*:;;hr::  
{
    Send("------------------------------")  ; 插入分隔线  
}  
```

#### 2. 剪贴板增强

```ahk
#v::Send("{Ctrl down}v{Ctrl up}")   ; Win+V粘贴纯文本（需预先处理剪贴板）  
^+V::Send "#v"              ; Ctrl+Shift+V打开剪贴板历史工具
```

#### 3. 鼠标操作

```ahk
~MButton::  ; 双击中键打开计算器
{  
    if (A_PriorHotkey = "~MButton" && A_TimeSincePriorHotkey < 300)  
        Run("calc.exe")  
}  

RButton & LButton::WinClose("A")  ; 右键+左键关闭当前窗口  
```

### 五、注意事项

#### 开机自动执行

如果想要脚本开机自动执行只需把脚本文件的快捷方式拖动至

```shell
C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
```

目录下的文件夹即可

如果会按键盘

1. 找到启动文件夹：
2. 按下 Win + R，打开运行对话框。
3. 输入以下路径并回车：

```shell
shell:startup
```

这将直接打开当前用户的启动文件夹。

#### 符号替换

:`*`:表示即时触发，::需手动触发
输入原始分号需转义：Hotstring(":`*`:`;", ";")

#### 路径与权限

路径含空格需用双引号包裹
操作系统级操作（如任务管理器）需脚本以管理员身份运行

#### 窗口标题匹配

"A"表示当前活动窗口
精准匹配使用ahk_exe 进程名.exe

#### 调试技巧

右键托盘图标选择「Reload This Script」重新加载脚本
使用MsgBox("变量值：" Var)输出调试信息

#### 多显示器支持

```ahk
^+Left::{
    ; 检查是否有活动窗口
    if !WinExist("A") {
        MsgBox("未找到活动窗口！")
        return
    }
    ; 获取活动窗口的当前位置和大小
    try WinGetPos(&X, &Y, &Width, &Height, "A")
    ; 判断窗口当前所在显示器
    if (X >= 0 && X < 1920) {
        ; 窗口在主屏幕，移动到副屏幕
        ; 副屏是竖屏，假设位于主屏幕左侧，坐标为 (-1440, 0)
        ; 调整窗口大小以适应副屏分辨率（1440x2560）
        NewWidth := 900  ; 副屏宽度
        NewHeight := 2560 ; 副屏高度
        WinMove(-2000, 0, NewWidth, NewHeight, "A")
    } else {
        ; 窗口在副屏幕，移回主屏幕
        ; 调整窗口大小以适应主屏分辨率（1920x1080）
        NewWidth := 1000  ; 主屏宽度
        NewHeight := 1000 ; 主屏高度
        WinMove(960, 200, NewWidth, NewHeight, "A")
    }
}
```

保存为 .ahk 文件后双击运行，建议配合 AutoHotkey v2 官方文档 进一步扩展功能。

## 附件

### 常用按键

| 指向键盘按键 | 符号 |
| :-----| :----: |
| Ctrl | ^ |
| Shift | + |
| Alt | ! |
| Shift | # |
| 其余功能键 | 使用大括号 |
| 数字或字母 | 直接输入 |
