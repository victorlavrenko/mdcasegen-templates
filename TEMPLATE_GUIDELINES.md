# TEMPLATE GUIDELINES

These templates are written in Markdown and used by the **mdcasegen** engine to generate multiple clinical case variants.

The syntax is designed to:

* Stay readable when rendered
* Be easy to edit in GitHub
* Allow structured variation
* Avoid technical-looking markup

---

# 1. Required Structure

Each template must contain:

```
## Metadata
...
## Question
...
## Gold Answer
...
```

Order matters.

---

# 2. Metadata Section

The metadata block starts with:

```
## Metadata
```

Inside metadata, use subsection headers and bullet lists.

Example:

```md
## Metadata
Case ID: orl-ssnhl-acute

### Protocol
- Sudden sensorineural hearing loss (SSNHL)

### Question category
- Urgent treatment, no missing data

### Variations
- Age: 18–80
- Affected ear: left or right
- Time since onset: 24–72 hours

### Noise
- allergies
- nasal congestion
- appears calm
```

### Rules

* `Case ID:` must be present.
* Subsections use `###`.
* Bullet lists use `-`.
* Do not rename subsection titles unless coordinated.

---

# 3. Sections

After metadata, you may include sections such as:

```
## Question
## Answer
## Gold Answer
```

The generator recognizes section headers that begin with `##`.

---

# 4. Inline Alternatives

Inline alternatives allow multiple wording options.

Syntax:

```md
**option1 | option2 | option3**
```

Example:

```md
A **35**-year-old patient presents with **sudden | abrupt** onset hearing loss.
```

### Rules

* Options are separated by `|`
* Spaces around `|` are recommended
* Empty options are not allowed
* The entire alternative must be inside `**`

Correct:

```
**normal | unchanged | at baseline**
```

Incorrect:

```
**normal| |baseline**
```

---

# 5. Block Alternatives (A), B), C) …)

Block alternatives allow large structured variants.

Syntax:

```
A) ...
B) ...
```

The generator:

* Groups consecutive A)/B)/C) blocks
* Randomly selects one block
* Removes the others

---

## 5.1 One-Line Block Alternative

Example:

```md
A) Weber lateralizes to the left ear
B) Weber lateralizes to the right ear
```

Each line is a full alternative.

---

## 5.2 Multi-Line Block Alternative

You may write:

```md
A):
- Weber lateralizes to the left ear
- Rinne is positive on the right

B):
- Weber lateralizes to the right ear
- Rinne is negative on the right
```

Everything indented or listed after the label belongs to that variant,
until:

* A blank line
* A new variant label (e.g., C))
* A new section (`##`)

---

## 5.3 Colon Splicing Behavior (Important)

If you write:

```md
Tuning fork testing shows

A):
- Weber lateralizes to the left
```

The engine will attach the colon `:` to the previous line:

Output:

```
Tuning fork testing shows:
- Weber lateralizes to the left
```

This allows natural English formatting.

You may also write:

```md
A) that sound is heard louder in the left ear
```

In that case, the text after `A)` is appended to the previous line.

---

## 5.4 Label Rules

* Labels must be single capital letters followed by `)`
* Examples: `A)`, `B)`, `C)`
* No spaces before the letter
* No lowercase letters

Correct:

```
A)
B)
```

Incorrect:

```
a)
Option A)
```

---

# 6. Noise Lines (Optional Information)

Noise lines are entire lines wrapped in bold:

```md
**The patient reports mild nasal congestion.**
```

If the metadata includes that noise keyword,
the engine may remove that entire line randomly.

### Rules

* The entire line must be bold.
* No extra text before or after the bold.
* Noise must also appear in `### Noise` metadata.

---

# 7. Numeric Values

Numeric values may be varied based on metadata ranges.

Example metadata:

```
### Variations
- Age: 18–80
```

In the question:

```
A **35**-year-old patient...
```

The number inside `**` may be replaced within the allowed range.

---

# 8. Best Practices

### Keep templates clean and readable

If the rendered Markdown looks awkward, fix it.

### Keep variants parallel

If A) is 2 bullet points, B) should usually also be 2.

### Avoid deeply nested alternatives

Inline `**a | b | c**` is preferred over complex block logic when possible.

### Avoid mixing unrelated A)/B) groups without spacing

Separate groups clearly.

---

# 9. Common Mistakes

❌ Leaving an empty option:

```
**normal | | baseline**
```

❌ Forgetting closing `**`

❌ Using lowercase labels:

```
a)
```

❌ Adding blank line inside a block unintentionally

---

# 10. Minimal Valid Template Example

```md
## Metadata
Case ID: example-template

### Variations
- Age: 18–80

## Question

A **35**-year-old patient presents with **sudden | abrupt** hearing loss.

Tuning fork testing shows

A):
- Weber lateralizes to the left
- Rinne is positive

B):
- Weber lateralizes to the right
- Rinne is negative

What is the best management?

## Gold Answer

- steroid
```

---

# Summary

The template language supports:

* Markdown sections
* Metadata blocks
* Inline alternatives with `|`
* Block alternatives with `A)`, `B)`
* Optional noise lines
* Natural English formatting

The goal is:

> Human-readable first. Structured variation second.