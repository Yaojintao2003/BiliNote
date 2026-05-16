# Graphify 知识图谱输出目录

此目录包含 BiliNote 项目的代码知识图谱分析结果，由 [Graphify](https://github.com/safishamsi/graphify) 工具生成。

---

## 目录说明

| 文件 | 说明 |
|------|------|
| `GRAPH_REPORT.md` | 完整的知识图谱分析报告，包含架构概述、实体清单、依赖关系等 |
| `graph.json` | 结构化图谱数据，可用于进一步分析或自定义可视化 |
| `graph.html` | 交互式可视化图谱，在浏览器中打开即可浏览 |

---

## 如何使用图谱工具

### 安装 Graphify

```bash
# 使用 uv (推荐)
uv tool install graphifyy && graphify install

# 或使用 pipx
pipx install graphifyy && graphify install

# 或使用 pip
pip install graphifyy && graphify install
```

> **注意**: PyPI 包名为 `graphifyy`（两个 y），但 CLI 命令是 `graphify`。

### 基本用法

```bash
# 分析当前目录
cd /path/to/your/project
graphify .

# 深度分析模式（更详细的提取）
graphify . --mode deep

# 增量更新（只重新提取变化的文件）
graphify . --update

# 查询知识图谱
graphify query "登录功能是如何实现的？"

# 查找两个实体之间的路径
graphify path "User" "Database"

# 解释概念
graphify explain "Authentication"
```

### 排除文件

创建 `.graphifyignore` 文件来排除不需要分析的文件：

```
node_modules/
*.log
*.min.js
dist/
```

---

## 分析结果说明

### 统计概览

- **总文件数**: ~380 个
- **Python 文件**: 113 个
- **TypeScript/TSX**: 124 个
- **Vue 文件**: 16 个

### 核心架构

```
┌─────────────────────────────────────────────────────────┐
│                      用户界面层                           │
├──────────────┬──────────────┬──────────────────────────┤
│   Web 前端    │  桌面端(Tauri) │      浏览器扩展          │
│   (React)    │   (React)    │      (Vue 3)            │
└──────┬───────┴──────┬───────┴───────────┬──────────────┘
       └──────────────┴───────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────┐
│                    FastAPI 后端                          │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌──────────┐   │
│  │  Note   │  │  Chat   │  │ Provider│  │  Config  │   │
│  │ Router  │  │ Router  │  │ Router  │  │  Router  │   │
│  └────┬────┘  └────┬────┘  └────┬────┘  └────┬─────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │              业务逻辑层 (Services)                │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────┬───────────────────────────────┘
                          │
       ┌──────────────────┼──────────────────┐
       ▼                  ▼                  ▼
┌─────────────┐  ┌──────────────┐  ┌───────────────┐
│  视频下载器   │  │   语音识别    │  │   LLM 服务    │
│  Downloaders│  │ Transcribers │  │   GPT/LLM    │
└─────────────┘  └──────────────┘  └───────────────┘
```

---

## 浏览交互式图谱

直接在浏览器中打开 `graph.html`：

```bash
# macOS
open graph.html

# Linux
xdg-open graph.html

# Windows
start graph.html
```

### 图谱操作

- **缩放**: 鼠标滚轮或右上角按钮
- **移动**: 拖拽画布
- **查看详情**: 点击节点，详情显示在左侧面板
- **搜索**: 使用左上角搜索框过滤节点
- **筛选**: 点击类型按钮按类别筛选

---

## 集成到 Claude Code

在 Claude Code 中加载报告，让 AI 基于图谱回答问题：

```bash
# 查看分析报告
cat graphify-out/GRAPH_REPORT.md

# 然后在对话中询问
"根据知识图谱，解释一下笔记生成的完整流程"
"VideoDownloader 有哪些实现类？"
```

---

## 贡献

此目录由自动化工具生成，不建议手动修改其中的文件。如需更新分析结果，请重新运行 `graphify` 命令。

---

*生成时间: 2026-05-17*  
*工具版本: Graphify v1.0*
