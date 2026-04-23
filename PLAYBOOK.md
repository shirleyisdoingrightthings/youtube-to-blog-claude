# YouTube → Blog | 操作手册 (PLAYBOOK)

> 本文档为实操指南，说明如何配置、运行以及自定义你的 YouTube 抓取与总结工作流。
> 系统架构及设计思想说明见 → [README.md](README.md)

---

## 一、环境配置 (Setup)

### 1. 前置要求

- Python 3.11+
- [Claude Code](https://claude.ai/code)（CLI 命令行或桌面应用）

### 2. 安装依赖项

```bash
pip install -r requirements.txt
```

### 3. 配置 API Keys

```bash
cp .env.example .env
```

编辑 `.env` 文件并填入你的凭证：

| 变量 | 获取方式 |
|---|---|
| `YOUTUBE_TRANSCRIPT_API_KEY` | [youtube-transcript.io](https://www.youtube-transcript.io) → 注册 → 复制 token（不含 "Basic "）|
| `NOTION_API_KEY` | [notion.so/profile/integrations](https://www.notion.so/profile/integrations) → New integration → 复制 secret |
| `NOTION_DATABASE_ID` | 在 Notion 中打开你的目标数据库 → 从 URL 中复制 32 位 ID |

> **Notion 数据库设置：** 创建 Integration 后，在 Notion 中打开目标数据库，点击 **Share（分享）**，并赋予你的 Integration 访问权限。该数据库需要包含以下属性：`Name` (Title), `URL` (URL), `Type` (Select), `Category` (Multi-select), `Created Date` (Date), `Status` (Status)。

### 4. 创建输出目录

```bash
mkdir output
```

---

## 二、使用方法 (Usage)

在 Claude Code 会话中打开此文件夹：

```bash
cd "/Users/shirleywu/Desktop/YouTube Transcript Scraper and Summary"
claude
```

然后只需粘贴任意 YouTube 链接：

```
https://youtu.be/am_oeAoUhew
```

Claude 将会自动处理接下来的所有步骤（字幕抓取、分段解读、本地归档、Notion 上传）——无需提供额外的指令。

---

## 三、自定义修改 (Customization)

工作流的高度解耦设计允许你轻松进行客制化：

- **更改输出语言：** 编辑 `skills/article_generation.md` 中的「输出语言与风格」部分。
- **更改文章结构：** 编辑 `skills/article_generation.md` 中的 6 段式模板——Claude 会严格遵守。
- **跳过 Notion 上传：** 从主控台 `CLAUDE.md` 中删除 Step 4，并保留 `.env` 中的 `NOTION_*` 环境变量为空。
- **修改 Notion 映射属性：** 修改 `notion_upload.py` 中的 `create_page()` 函数，使其与你自己的数据库结构字段严格匹配。

---

## 四、API 限制说明

遇到调用失败时，请优先检查以下额度是否耗尽：

| 服务 | 免费额度 / 计费 |
|---|---|
| youtube-transcript.io | 20 个视频 / 月（免费版） |
| Notion API | 无限制（配合 Integration 使用） |
| Claude Code | 基于你的 Anthropic 订阅计划产生 Token 费用 |
