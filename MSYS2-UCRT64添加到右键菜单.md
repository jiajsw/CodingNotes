# Windows 右键菜单添加 MSYS2 UCRT64 终端

在 Windows 资源管理器中通过右键菜单直接在当前目录打开 **MSYS2 UCRT64** 环境。

使用 MSYS2 官方推荐的 `msys2_shell.cmd` 脚本，配合 `-where` 参数，能够完美处理带有空格或特殊字符的 Windows 路径，是最稳定、最标准的方法。

---

## 注册表脚本 (.reg)

新建一个文本文件，将后缀名改为 `.reg`（例如 `ucrt64_context.reg`），复制以下内容并保存（确保编码为 **UTF-8** 或 **ANSI**），然后双击运行导入注册表。

> ⚠️ **注意**：如果你的 MSYS2 安装路径不是 `D:\dev\msys64`，请自行将脚本中的路径替换为你的实际安装路径（路径中的斜杠在注册表中需要双写转义，即 `\\`）。

```registry
Windows Registry Editor Version 5.00

# 1. 在文件夹空白处右键
[HKEY_CLASSES_ROOT\Directory\Background\shell\UCRT64]
@="UCRT64 终端"
"Icon"="D:\\dev\\msys64\\ucrt64.exe"

[HKEY_CLASSES_ROOT\Directory\Background\shell\UCRT64\command]
@="\"D:\\dev\\msys64\\msys2_shell.cmd\" -ucrt64 -where \"%V\""

# 2. 在文件夹图标上右键
[HKEY_CLASSES_ROOT\Directory\shell\UCRT64]
@="UCRT64 终端"
"Icon"="D:\\dev\\msys64\\ucrt64.exe"

[HKEY_CLASSES_ROOT\Directory\shell\UCRT64\command]
@="\"D:\\dev\\msys64\\msys2_shell.cmd\" -ucrt64 -where \"%1\""
```