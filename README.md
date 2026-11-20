# text-preprocessing-for-ir
**Text Preprocessor for Information Retrieval**

A lightweight Python tool that turns raw English text into a clean list of index terms, the same preprocessing step done before building an inverted index in a Boolean retrieval system. It has no dependencies, and the Porter stemmer is implemented from scratch.

**Pipeline**

Raw text → Tokenization → Normalization → Stop-word removal → Porter stemming → Terms

**Quick Start**

Requirements: Python 3.8 or higher. No packages to install.

Run on the three built-in sample texts:
```bash
python text_preprocessor.py
```

Run on your own file (one text per line, blank lines are ignored):
```bash
python text_preprocessor.py texts.txt
```

**Output**

- Console: the final terms for each text, followed by Precision and Recall against the gold output, plus the extra terms (O − G) and missed terms (G − O) for error analysis.
- `outputs.json`: the processed terms for every text.

Example:
```
text1: ['friend', 'roman', 'countrymen', 'lend', 'ear']

[text1] Precision = 1.00 | Recall = 1.00
   Extra  (O - G): []
   Missed (G - O): []
```

**Evaluating Your Own Texts**

Precision and Recall are computed against the `gold` dictionary in `main()`. To evaluate your own texts, add an entry to it, keyed by `text1`, `text2`, and so on, matching the line order in your file. Write each entry by hand from the project rules rather than by running the program, otherwise the score is meaningless. Texts without a gold entry will score 0.

**Design Decisions**

- Stop words: a fixed custom list of about 70 words, removed before stemming.
- Stemmer: the Porter algorithm (1980), implemented by hand.
- Hyphenated words (e.g. `state-of-the-art`) stay as one token and are not stemmed.
- Abbreviations (e.g. `U.S.A.`) become a single token with the dots removed (`usa`).
- Possessives are stripped (`John's` → `john`).
- Output order and duplicates are preserved.
- Metrics are computed on the sets of distinct terms.

**Known Limitations**

- Only Latin letters are recognized; accented characters and other scripts are not supported.
- Abbreviations without dots, such as `Dr` and `Mr`, are treated as ordinary words.
- Porter stemming can over-stem (`university` and `universe` collapse together) or under-stem related words.
- Stems are not always real words (`quality` → `qualiti`).
