---
name: extract-textbook-vocab-zh
description: 从教材或练习册图片中提取被圈画、高亮或标记的词汇，并生成结构化的 CSV 文件。当用户提供了带有圈画/高亮/下划线词汇的教材页面图片，并要求提取词汇、建立单词表、从标记词汇创建 CSV，或类似需要将图片中的标注文本转换为表格/列表格式的任务时使用。
---

# 教材词汇提取

从教材/练习册图片中提取被圈画、高亮、下划线或以其他方式标记为词汇的单词或短语，然后生成一份整洁的 CSV 文件。

## 工作流程

### 1. 读取图片

读取所有提供的图片。识别每一个被圈画、高亮、下划线或以其他视觉方式标记为词汇的单词或短语。

### 2. 确定基础形式

在尊重上下文用法的前提下，将每个提取出的单词/短语转换为其**原始/基础形式**：

| 规则 | 原文示例 | 基础形式 |
|------|---------|---------|
| 复数名词 → 单数 | stems, tulips, auction houses | stem, tulip, auction house |
| 过去式 / 过去分词动词 → 动词原形 | purchased, exported, dominated | purchase, export, dominate |
| 第三人称单数动词 → 动词原形 | claims, handles, processes | claim, handle, process |
| 形容词（包括用作形容词的分词）→ 保持原样 | globalized, appealing, fresh-cut, predictable | globalized, appealing, fresh-cut, predictable |
| 专有名词 → 保持原样 | The Netherlands | The Netherlands |
| 中心词为复数的名词短语 → 单数中心词 | employment opportunities, high-tech cooling systems | employment opportunity, high-tech cooling system |

**关键规则：** 如果过去分词（如 *globalized*）或现在分词（如 *appealing*）在句中充当形容词，请保留该形式。**不要**将其转换为动词原形。

### 3. 标注词性并翻译

对每个条目，根据其**在上下文中的实际用法**确定词性，并在中文翻译前加上前缀：

- **n.** 表示名词
- **v.** 表示动词
- **adj.** 表示形容词
- **adv.** 表示副词

提供简洁、符合上下文的中文翻译。

示例：
- `stem` → n. 花茎；茎
- `purchase` → v. 购买
- `globalized` → adj. 全球化的
- `responsible for` → adj. 对……负责；归因于

### 4. 构建 CSV

创建一个名为 `vocabulary.csv`（或用户指定的名称）的 CSV 文件，严格包含两列：

```csv
Word/Phrase,Chinese
stem,n. 花茎；茎
purchase,v. 购买
globalized,adj. 全球化的
```

- 逗号后不加空格，除非是翻译内容本身包含空格。
- 每个被标记的单词/短语占一行。

### 5. 校验

在最终定稿前，逐行交叉检查：

1. 基础形式是否与单词在句中的用法一致？
2. 复数名词后缀是否已去除？
3. 动词变形（-ed、-s）是否已还原为原形？
4. 形容词（包括分词形容词）是否保持未变？
5. 词性标签是否准确且已标注？

如有任何条目存在歧义，请重新读取图片上下文以作出判断。
