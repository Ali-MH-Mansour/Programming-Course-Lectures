# Quarto Setup — Programming Course Site

## What this is

A Quarto Book project that publishes all 18 lectures to a GitHub Pages website.  
Each lecture is a `.qmd` file (Quarto Markdown — compatible with plain `.md`).

---

## Prerequisites

- [Quarto](https://quarto.org/docs/get-started/) installed locally
- GitHub account
- Git installed

---

## Steps to publish

### 1. Create a GitHub repository

The repository is already set up at:
**https://github.com/Ali-MH-Mansour/Programming-Course-Lectures**

If it does not yet exist on GitHub, create a new repository with that exact name.

### 2. `_quarto.yml` is already configured

The `author:` and `repo-url:` fields are filled in:
```yaml
author: "Ali-MH-Mansour"
repo-url: "https://github.com/Ali-MH-Mansour/Programming-Course-Lectures"
```

### 3. Convert existing lecture files

The existing student handouts in `../lectures/` are plain Markdown — they work in Quarto as-is.  
Copy or symlink them into `lectures/en/` with `.qmd` extension:

```bash
mkdir -p lectures/en
# Example for L06:
cp ../lectures/L06-student-handout.md lectures/en/L06-arrays-pointers.qmd
```

Or rename them in bulk:
```bash
for f in ../lectures/L*-student-handout.md; do
    base=$(basename "$f" -student-handout.md)
    cp "$f" "lectures/en/${base}.qmd"
done
```

### 4. Preview locally

```bash
quarto preview
```

This opens a browser with the live site. Edit any `.qmd` and the browser auto-refreshes.

### 5. Publish to GitHub Pages

```bash
git init
git remote add origin https://github.com/Ali-MH-Mansour/Programming-Course-Lectures.git
git add .
git commit -m "initial commit"
git push -u origin main
```

After the first push, GitHub Actions (`.github/workflows/publish.yml`) will:
1. Install Quarto
2. Render the book
3. Deploy it to `https://Ali-MH-Mansour.github.io/Programming-Course-Lectures/`

Enable GitHub Pages in your repo settings:  
**Settings → Pages → Source → GitHub Actions**

---

## Adding Arabic (or Russian) pages

Option A — **separate language folders** (simplest):
```
lectures/
  en/   ← English student handouts
  ar/   ← Arabic versions
```
Add a second `_quarto.yml` `chapters:` block under a language part, or maintain two separate Quarto projects.

Option B — **Quarto multilingual** (`lang:` per file):
Add `lang: ar` to the YAML front matter of Arabic `.qmd` files. Quarto will apply RTL text direction automatically.

---

## File naming convention

| Source file | Quarto file |
|-------------|-------------|
| `L06-student-handout.md` | `lectures/en/L06-arrays-pointers.qmd` |
| `L06-arabic.md` | `lectures/ar/L06-arrays-pointers.qmd` |
