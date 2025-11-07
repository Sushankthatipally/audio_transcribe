# GitHub Push Instructions

## Step 1: Configure Git (First Time Only)

If you haven't configured Git before:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Step 2: Check Current Status

```bash
cd c:\Users\nani\Desktop\sonar\repo
git status
```

## Step 3: Add Files to Git

```bash
# Add all files (respecting .gitignore)
git add .

# Check what will be committed
git status
```

## Step 4: Commit Changes

```bash
git commit -m "Initial commit: Telugu-English translation evaluation project

- SeamlessM4T-v2-large model integration
- 2,665 audio files translated and evaluated
- 8 evaluation metrics (BLEU, ChrF++, TER, WER, CER, ROUGE, METEOR, BERTScore)
- Results: 90.5% BERTScore F1 achieved
- Progress tracking and caching implemented
- Comprehensive documentation and visualizations"
```

## Step 5: Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `telugu-english-translation` (or your preferred name)
3. Description: "Telugu to English speech translation evaluation using SeamlessM4T"
4. Choose: Public or Private
5. **DO NOT** initialize with README (we already have one)
6. Click "Create repository"

## Step 6: Add Remote and Push

GitHub will show you commands. Use these:

```bash
# Add the remote (replace 'yourusername' with your GitHub username)
git remote add origin https://github.com/yourusername/telugu-english-translation.git

# Check remote is added
git remote -v

# Push to GitHub (main branch)
git branch -M main
git push -u origin main
```

## Step 7: Verify

Go to your GitHub repository URL to verify all files are uploaded.

---

## Troubleshooting

### Authentication Error

If you get authentication errors, you'll need a Personal Access Token:

1. Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Select scopes: `repo` (full control of private repositories)
4. Generate and copy the token
5. When pushing, use the token as your password

### Large File Error

If you get "file too large" errors:

```bash
# Check .gitignore is working
git ls-files --others --ignored --exclude-standard

# Remove large files from git cache
git rm --cached -r TG/
git commit -m "Remove large audio files"
```

### Already Exists Error

If remote already exists:

```bash
# Remove old remote
git remote remove origin

# Add new one
git remote add origin https://github.com/yourusername/telugu-english-translation.git
```

---

## Future Updates

To push future changes:

```bash
git add .
git commit -m "Description of changes"
git push
```

---

## What Gets Uploaded

✅ **Included:**

- Jupyter notebook
- README.md
- requirements.txt
- .gitignore
- results/ (JSON, CSV files)
- Documentation

❌ **Excluded (via .gitignore):**

- TG/ folder (audio files - too large)
- .seamless_cache/ (cache files)
- .venv311/ (Python environment)
- seamless_translations.txt (large output file)
- Model checkpoints (auto-downloaded)

---

## Repository Size

Expected size: ~5-10 MB (without audio/cache/models)

**Note**: Keep audio files and large outputs locally. Users can download the model automatically when they run the notebook.
