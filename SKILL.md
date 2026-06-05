# LaTeX 简历编译指南

## 环境依赖

| 工具 | 说明 |
|------|------|
| **TeX Live** | LaTeX 发行版，提供 `xelatex` 编译器 |
| **XeLaTeX** | 支持 Unicode 和系统字体，用于中文渲染 |
| **xeCJK** | LaTeX 宏包，处理中日韩文字排版 |
| **fontawesome5** | LaTeX 宏包，提供图标支持 |

---

## macOS 安装

1. 下载安装 [TeX Live](https://tug.org/texlive/) 或使用 Homebrew：
   ```bash
   brew install --cask mactex-no-gui
   ```
2. 安装后重启终端，验证：
   ```bash
   xelatex --version
   ```
3. 字体使用 macOS 内置的 `PingFang SC`，无需额外安装。

---

## Windows 安装

1. 下载安装 [TeX Live for Windows](https://tug.org/texlive/)（`install-tl-windows.exe`）
2. 安装后重启终端，验证：
   ```bash
   xelatex --version
   ```
3. **修改字体**：`resume.tex` 第12行改为 Windows 内置字体：
   ```latex
   \setCJKmainfont{Microsoft YaHei}
   ```
   或使用跨平台字体（需另行下载 [Noto CJK](https://github.com/notofonts/noto-cjk)）：
   ```latex
   \setCJKmainfont{Noto Serif CJK SC}
   ```

---

## 编译命令

```bash
xelatex resume.tex
```

编译两次可确保目录/引用正确：
```bash
xelatex resume.tex && xelatex resume.tex
```

生成的文件说明：

| 文件 | 说明 |
|------|------|
| `resume.pdf` | 最终输出的 PDF |
| `resume.aux` | 辅助文件，可删除 |
| `resume.log` | 编译日志，报错时查看 |
| `resume.out` | 书签信息，可删除 |
| `resume.synctex.gz` | 编辑器跳转用，可删除 |

---

## VS Code / Windsurf 配置（推荐）

安装扩展 **LaTeX Workshop**（`james-yu.latex-workshop`），支持：
- 保存时自动编译
- 内置 PDF 预览
- 正向/反向跳转（SyncTeX）

在 `.vscode/settings.json` 中添加：
```json
{
  "latex-workshop.latex.recipe.default": "lastUsed",
  "latex-workshop.latex.tools": [
    {
      "name": "xelatex",
      "command": "xelatex",
      "args": ["-synctex=1", "-interaction=nonstopmode", "%DOC%"]
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "xelatex",
      "tools": ["xelatex"]
    }
  ]
}
```

---

## 清理编译产物

```bash
rm -f resume.aux resume.log resume.out resume.synctex.gz
```
