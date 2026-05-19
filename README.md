# Extract Textbook Vocabulary — Kimi Skill

A Kimi Code CLI skill that extracts circled, highlighted, or marked vocabulary words from textbook/workbook images and generates a structured CSV file.

## What It Does

When you provide images of textbook pages with annotated words (circled, highlighted, underlined, etc.), this skill will:

1. Read the images and identify all marked vocabulary
2. Convert words to their base form (plural → singular, past tense → infinitive, etc.)
3. Determine part of speech and provide Chinese translations
4. Output a clean `vocabulary.csv` file

## Installation

### Option 1: Download the `.skill` file

1. Download `extract-textbook-vocab.skill` from the [v1.0.0 release](../../releases/tag/v1.0.0) (or directly from this repo)
2. Extract it to your Kimi skills directory:
   ```bash
   unzip extract-textbook-vocab.skill -d ~/.kimi/skills/
   ```

### Option 2: Clone the source

```bash
git clone https://github.com/YOUR_USERNAME/extract-textbook-vocab-skill.git
cp -r extract-textbook-vocab-skill/extract-textbook-vocab ~/.kimi/skills/
```

### Skill Discovery Paths

Kimi looks for skills in these locations (in order):
- `~/.config/agents/skills/`
- `~/.kimi/skills/`
- `~/.claude/skills/`

## Usage

Once installed, simply ask Kimi:

> "Extract the circled vocabulary from these textbook images and make a CSV."

Or provide images and say:

> "These are pages from my workbook. The highlighted words are vocabulary. Please extract them into a word list."

## Example Output

```csv
Word/Phrase,Chinese
stem,n. 花茎；茎
purchase,v. 购买
globalized,adj. 全球化的
```

## Rules Summary

| Type | Handling |
|------|----------|
| Plural nouns | → Singular (stems → stem) |
| Past tense / participle verbs | → Infinitive (purchased → purchase) |
| 3rd person singular verbs | → Infinitive (claims → claim) |
| Adjectives (including participle adjectives) | → Keep as-is (globalized, appealing) |
| Proper nouns | → Keep as-is |
| Noun phrases with plural head | → Singular head |

## Requirements

- Kimi Code CLI
- Images containing marked/highlighted/circled vocabulary words

## License

MIT
