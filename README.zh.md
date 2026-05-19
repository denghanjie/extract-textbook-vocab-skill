# 📚 教材词汇提取技能 — Extract Textbook Vocab

一个用于从教材/练习册图片中提取圈画、高亮或标注词汇，并生成结构化 CSV 文件的 Kimi 技能。

---

## ✨ 功能介绍

当你提供带有标注（圈画、高亮、下划线等）的教材页面图片时，本技能将自动：

1. **读取图片** — 识别所有被标记的词汇或短语
2. **还原词形** — 将单词转换为原始形式（复数→单数、过去式→原形等）
3. **标注词性与翻译** — 根据上下文确定词性，并提供简洁的中文翻译
4. **生成 CSV 文件** — 输出整洁的 `vocabulary.csv` 文件

---

## 📥 安装方法

### 方式一：下载 `.skill` 文件（推荐）

1. 从 [Releases](../../releases) 页面下载 `extract-textbook-vocab.skill`
2. 解压到对应客户端的技能目录：

```bash
# Kimi Code CLI
unzip extract-textbook-vocab.skill -d ~/.kimi/skills/

# WorkBuddy
unzip extract-textbook-vocab.skill -d ~/.workbuddy/skills/

# Claude Code
unzip extract-textbook-vocab.skill -d ~/.claude/skills/

# 其他 Agent 客户端
unzip extract-textbook-vocab.skill -d ~/.config/agents/skills/
```

### 方式二：克隆源码

```bash
git clone https://github.com/denghanjie/extract-textbook-vocab-skill.git

# Kimi Code CLI
cp -r extract-textbook-vocab-skill/extract-textbook-vocab ~/.kimi/skills/

# WorkBuddy
cp -r extract-textbook-vocab-skill/extract-textbook-vocab ~/.workbuddy/skills/

# Claude Code
cp -r extract-textbook-vocab-skill/extract-textbook-vocab ~/.claude/skills/
```

### 技能扫描路径

Kimi 及相关客户端会按以下顺序扫描技能：
- `~/.config/agents/skills/`
- `~/.kimi/skills/`
- `~/.claude/skills/`

> 💡 **WorkBuddy 用户**：WorkBuddy 支持标准 Kimi 技能格式，将技能文件夹放入 `~/.workbuddy/skills/` 即可自动识别。

---

## 🚀 使用方式

### Kimi Code CLI

安装后，直接在对话中使用：

```
/skill:extract-textbook-vocab
```

或直接描述你的需求：

> "从这些教材图片中提取圈画的词汇，生成 CSV 文件。"

> "这些是练习册页面，高亮的单词是词汇，请提取并做成单词表。"

### WorkBuddy

在 WorkBuddy 对话中：

1. 上传教材图片
2. 输入：
   > "使用 extract-textbook-vocab 技能，提取图片中圈画的词汇"
   
   或直接说：
   > "提取这些教材中标注的单词，生成带词性和中文翻译的 CSV"

### Claude Code / 其他客户端

将技能放入对应目录后，Claude 会根据技能描述自动匹配使用场景。你也可以明确调用：

> "请使用 extract-textbook-vocab 技能处理这些图片，提取高亮词汇。"

---

## 📋 处理规则

| 类型 | 处理方式 | 示例 |
|------|---------|------|
| 复数名词 | → 单数形式 | stems → stem, tulips → tulip |
| 过去式/过去分词动词 | → 动词原形 | purchased → purchase, exported → export |
| 第三人称单数动词 | → 动词原形 | claims → claim, handles → handle |
| 形容词（含分词形容词） | → 保持原样 | globalized, appealing, fresh-cut |
| 专有名词 | → 保持原样 | The Netherlands |
| 复数中心名词短语 | → 单数中心词 | employment opportunities → employment opportunity |

⚠️ **重要规则**：如果过去分词（如 *globalized*）或现在分词（如 *appealing*）在句中作形容词使用，**保留该形式**，不要转换为动词原形。

---

## 📝 输出示例

生成的 `vocabulary.csv` 格式如下：

```csv
Word/Phrase,Chinese
stem,n. 花茎；茎
purchase,v. 购买
globalized,adj. 全球化的
responsible for,adj. 对……负责；归因于
employment opportunity,n. 就业机会
```

- 两列结构：**Word/Phrase**（单词/短语）和 **Chinese**（中文翻译）
- 词性前缀：**n.**（名词）、**v.**（动词）、**adj.**（形容词）、**adv.**（副词）
- 逗号后无空格（除非翻译内容本身包含）

---

## ✅ 质量检查清单

在最终输出前，系统会交叉验证每个条目：

1. 基础词形是否与句中用法一致？
2. 复数名词后缀是否已去除？
3. 动词变形（-ed, -s）是否已还原为原形？
4. 形容词（包括分词形容词）是否保持未变？
5. 词性标签是否准确且已标注？

如有歧义，会重新读取图片上下文进行判断。

---

## 🔧 环境要求

- Kimi Code CLI / WorkBuddy / Claude Code 或其他支持 Kimi 技能的 Agent 客户端
- 包含圈画、高亮或标注词汇的教材图片（支持 JPG、PNG 等常见格式）

---

## 📄 许可证

MIT License
