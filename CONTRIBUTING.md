# 🤝 Contributing to Windows CMD & PowerShell Cheatsheet

Thank you for your interest in contributing! 🎉  
This cheatsheet is built for cybersecurity learners, SOC analysts, sysadmins, and pentesters.  
Every improvement — big or small — makes it more useful for the community.

---

## 📌 What You Can Contribute

- ✅ **New commands** that are missing from any section
- ✅ **Better descriptions** — clearer, more beginner-friendly explanations
- ✅ **Bug fixes** — typos, wrong syntax, inaccurate descriptions
- ✅ **New sections** — e.g., Active Directory, Windows Firewall Rules, Credential Defense
- ✅ **PowerShell additions** — equivalent or advanced PowerShell versions of CMD commands
- ✅ **Forensic notes** — useful Event IDs, registry keys, forensic tips
- ✅ **Translations** — a version in another language

---

## 🛠️ How to Contribute

### 1. Fork the repository
Click the **Fork** button at the top right of this page.

### 2. Clone your fork
```bash
git clone https://github.com/YOUR-USERNAME/REPO-NAME.git
cd REPO-NAME
```

### 3. Make your changes
Edit `README.md` directly. Follow the existing format:

```cmd
command <argument>          # Short, clear description of what it does
```

For sections with categories, match the comment style:
```cmd
# ── Category Name ─────────────────────────────────────────────────
command                     # What this command does
```

### 4. Commit your changes
```bash
git add README.md
git commit -m "Add: <brief description of what you added>"
git push origin main
```

### 5. Open a Pull Request
Go to the original repo and click **"New Pull Request"**.
Write a short description of what you changed and why.

---

## ✅ Contribution Guidelines

- Keep descriptions **short and clear** — one line per command is the goal
- Use `<angle brackets>` for values the user must replace
- Place the command in the **correct section**
- **Test the command** on a real system before submitting if possible
- Do not add commands that require paid tools (unless clearly marked)
- Mark dangerous/destructive commands with a `⚠️` or `# WARNING` comment

---

## 🏗️ Repo Structure

```
Windows-CMD-Cheatsheet/
├── README.md                           ← Main cheatsheet (auto-renders on GitHub)
├── Windows_Commands_Cheatsheet.pdf     ← Downloadable/printable PDF version
├── LICENSE                             ← MIT License
└── CONTRIBUTING.md                     ← This file
```

---

## 🙋 Questions?

Open an [Issue](https://github.com/Safin313-stack) if unsure about anything. All skill levels welcome!

> Made with ❤️ by [Safin313-stack](https://github.com/Safin313-stack) — Dhaka, Bangladesh 🇧🇩
