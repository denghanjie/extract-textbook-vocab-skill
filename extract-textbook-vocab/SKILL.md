---
name: extract-textbook-vocab
description: Extract circled, highlighted, or marked vocabulary words from textbook or workbook images and generate a structured CSV file. Use when the user provides images of textbook pages with circled/highlighted/underlined words and asks to extract vocabulary, build a word list, create a CSV from marked words, or similar tasks involving converting annotated text from images into a spreadsheet or list format.
---

# Extract Textbook Vocabulary

Extract vocabulary words that are circled, highlighted, underlined, or otherwise marked in textbook/workbook images, then produce a clean CSV file.

## Workflow

### 1. Read Images

Read all provided images. Identify every word or phrase that is circled, highlighted, underlined, or otherwise visually marked as vocabulary.

### 2. Determine Base Form

Convert each extracted word/phrase to its **original/base form** while respecting its contextual usage:

| Rule | Example in Text | Base Form |
|------|-----------------|-----------|
| Plural nouns → singular | stems, tulips, auction houses | stem, tulip, auction house |
| Past tense / past participle verbs → infinitive | purchased, exported, dominated | purchase, export, dominate |
| 3rd person singular verbs → infinitive | claims, handles, processes | claim, handle, process |
| Adjectives (including participles used as adjectives) → keep as-is | globalized, appealing, fresh-cut, predictable | globalized, appealing, fresh-cut, predictable |
| Proper nouns → keep as-is | The Netherlands | The Netherlands |
| Noun phrases with plural head → singular head | employment opportunities, high-tech cooling systems | employment opportunity, high-tech cooling system |

**Critical rule:** If a past participle (e.g., *globalized*) or present participle (e.g., *appealing*) functions as an adjective in the sentence, preserve that form. Do **not** convert it to the verb infinitive.

### 3. Assign Part-of-Speech & Translate

For each entry, determine its part of speech **as used in context** and prefix the Chinese translation:

- **n.** for nouns
- **v.** for verbs
- **adj.** for adjectives
- **adv.** for adverbs

Provide a concise, context-appropriate Chinese translation.

Examples:
- `stem` → n. 花茎；茎
- `purchase` → v. 购买
- `globalized` → adj. 全球化的
- `responsible for` → adj. 对……负责；归因于

### 4. Build CSV

Create a CSV file named `vocabulary.csv` (or a name the user specifies) with exactly two columns:

```csv
Word/Phrase,Chinese
stem,n. 花茎；茎
purchase,v. 购买
globalized,adj. 全球化的
```

- No spaces after commas unless part of the translation.
- Each marked word/phrase becomes exactly one row.

### 5. Verify

Before finalizing, cross-check every row:

1. Does the base form match how the word is used in the sentence?
2. Have plural noun suffixes been removed?
3. Have verb inflections (-ed, -s) been reverted to infinitive?
4. Are adjectives (including participle adjectives) preserved unchanged?
5. Are POS labels accurate and present?

If any entry is ambiguous, re-read the image context to decide.
