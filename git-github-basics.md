# Git & GitHub Basics for Beginners

## Part 1: Set Up Your GitHub Profile

### Step 1: Create GitHub Account
1. Go to **github.com**
2. Sign up with username (example: `safa_sb`)
3. Verify email

### Step 2: Configure Git on Your Computer
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Step 3: Create Your Profile README
1. Click **"+"** → **New repository**
2. Name it **EXACTLY** your username (example: `safa_sb`)
3. Check **Add a README file**
4. Click **Create repository**

### Step 4: Edit Your Profile
Edit the README.md with something simple like:
```markdown
# Hi, I'm Safa!

## About Me
- Learning Git and GitHub
- New to coding
- Student

## My Projects
- My first repository
- Learning everyday!
```

---

## Part 2: Basic Git Commands

### Create Your First Repository

#### Method 1: Start on GitHub (Easier)
1. Create new repository on GitHub
2. Clone it:
```bash
git clone https://github.com/username/my-first-repo.git
cd my-first-repo
```

#### Method 2: Start Locally
```bash
mkdir my-project
cd my-project
git init
```

### The Main Git Commands You Need

#### 1. Check Status
See what's changed:
```bash
git status
```

#### 2. Add Files
Add a specific file:
```bash
git add filename.txt
```

Add everything:
```bash
git add .
```

#### 3. Commit (Save)
Save your changes:
```bash
git commit -m "Your message here"
```

#### 4. Push (Upload)
Send to GitHub:
```bash
git push
```

#### 5. Pull (Download)
Get latest changes:
```bash
git pull
```

---

## Part 3: Simple Practice Exercise

### Exercise 1: Create and Push a File
```bash
# 1. Create a new file
echo "Hello World" > hello.txt

# 2. Add it
git add hello.txt

# 3. Commit it
git commit -m "Add hello file"

# 4. Push it
git push
```

### Exercise 2: Update a File
```bash
# 1. Edit the file
echo "Hello GitHub" >> hello.txt

# 2. Add the changes
git add hello.txt

# 3. Commit
git commit -m "Update hello file"

# 4. Push
git push
```

---

## Part 4: Common Workflow

This is what you'll do most of the time:

### Daily Workflow
```bash
# 1. Make changes to your files

# 2. Check what changed
git status

# 3. Add your changes
git add .

# 4. Commit with a message
git commit -m "What you did"

# 5. Push to GitHub
git push
```

---

## Quick Reference

| Command | What it does | Example |
|---------|-------------|---------|
| `git status` | Check changes | `git status` |
| `git add` | Stage changes | `git add file.txt` |
| `git commit` | Save changes | `git commit -m "message"` |
| `git push` | Upload to GitHub | `git push` |
| `git pull` | Download from GitHub | `git pull` |
| `git clone` | Copy repo | `git clone [url]` |

---

## Tips for Students

### Good Commit Messages
- Good: "Add login page"
- Good: "Fix spelling error"
- Good: "Update README"
- Bad: "stuff"
- Bad: "asdfgh"
- Bad: "changes"

### When to Commit?
- After completing a small task
- Before taking a break
- When something works

### Remember
1. **Add → Commit → Push** (this is the pattern!)
2. Commit often
3. Write clear messages
4. Don't be afraid to make mistakes

---

## Troubleshooting

### "Nothing to commit"
- You forgot to `git add` your files

### "Failed to push"
- Try `git pull` first, then push again

### "Not a git repository"
- You're in the wrong folder or forgot `git init`

---

## Next Steps
Once comfortable with these basics:
- Learn about branches
- Try pull requests
- Collaborate with others

---

## Part 5: Markdown Formatting for README Files

Markdown is the language used to format README.md files on GitHub.

### Headers (Titles)
```markdown
# Main Title (H1)
## Subtitle (H2)
### Section Title (H3)
#### Subsection (H4)
##### Small Header (H5)
###### Smallest Header (H6)
```

### Text Formatting
```markdown
**This text is bold**
*This text is italic*
***This text is bold and italic***
~~This text is strikethrough~~
```

### Lists

#### Unordered List (Bullets)
```markdown
- First item
- Second item
- Third item
  - Nested item
  - Another nested item
```

#### Ordered List (Numbers)
```markdown
1. First item
2. Second item
3. Third item
   1. Nested item
   2. Another nested item
```

### Links
```markdown
[Click here to visit Google](https://www.google.com)
[Link to my repository](https://github.com/username/repo-name)
```

### Images
```markdown
![Image description](image-url.png)
![GitHub Logo](https://github.com/logo.png)
```

### Code

#### Inline Code
```markdown
Use `git status` to check changes.
```

#### Code Block
````markdown
```python
print("Hello World")
```

```bash
git add .
git commit -m "message"
```
````

### Line Breaks and Paragraphs
```markdown
First paragraph.

Second paragraph (empty line between).

Line break without paragraph  
(two spaces at the end of line)
```

### Horizontal Line
```markdown
---
or
***
```

### Tables
```markdown
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Data 1   | Data 2   | Data 3   |
| Data 4   | Data 5   | Data 6   |
```

### Blockquotes
```markdown
> This is a quote
> It can span multiple lines
```

### Task Lists
```markdown
- [x] Completed task
- [ ] Uncompleted task
- [ ] Another task to do
```

### Example README Using These Formats

```markdown
# Project Title

## Description
This is my **first project** using *Git and GitHub*.

## Features
- Feature one
- Feature two
- Feature three

## Installation
1. Clone the repository
2. Run `npm install`
3. Start the project

## Code Example
```python
def hello():
    print("Hello GitHub!")
```

## Links
- [My GitHub Profile](https://github.com/username)
- [Documentation](https://docs.github.com)

## Status
- [x] Basic setup complete
- [ ] Add more features
- [ ] Write tests

---
**Note**: This project is under development.
```

### Quick Reference

| What You Want | How to Write It | Result |
|--------------|-----------------|--------|
| Big title | `# Title` | # Title |
| Subtitle | `## Subtitle` | ## Subtitle |
| Bold | `**bold**` | **bold** |
| Italic | `*italic*` | *italic* |
| Code | `` `code` `` | `code` |
| Link | `[text](url)` | [text](url) |
| Bullet | `- item` | - item |
| Number | `1. item` | 1. item |

---

**Remember**: Git is like saving your game - do it often!

*Keep practicing these commands and they'll become second nature!*