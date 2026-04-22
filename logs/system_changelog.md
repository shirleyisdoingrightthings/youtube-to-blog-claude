# System Changelog (Meta-Harness)

> 此日志文件用于记录 `YouTube Transcript Scraper and Summary` 系统框架本身的演进与维护。
> 当触发 Meta-Harness 自检协议（Step 6）时，由 Agent 根据用户的批准在此记录：架构优化、规则重构、脚本升级及目录结构变动。

---

## [2026-04-23]
- **升级模块**：`CLAUDE.md`, `README.md`, `tags.json`, `notion_upload.py`, `skills/article_generation.md`
- **变更详情**：
  1. **(Phase 1) 上下文持久化基建**：引入 `tags.json` 强约束标签发散行为；建立 `logs/` 机制提升系统可观测性；打通 Obsidian `Second Brain` 的 Markdown 双向同步路径。
  2. **(Phase 2) 极简收纳与分类降级**：确立了“本地文件夹不带标签前缀、直接使用完整自然命名”的规则。将标签属性全面转移至标准的 YAML Frontmatter，并同步优化了 `notion_upload.py`，使其能自动跳过 YAML 块。
  3. **(Phase 3) 知识网分层治理**：确立了 **“宏观分类用 YAML Tags 强收敛，微观术语用 Obsidian 双链 `[[ ]]` 自由发散”** 的核心分类准则，并在生成规范中禁用了正文内的 `# 一级标题`。
  4. **(Phase 4) Meta-Harness 自进化协议**：在大纲内新增了触发式的自检 Checklist，允许系统在发生架构改动后主动提出更新 README 等文档的建议并记入本系统日志。
