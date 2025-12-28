# LaTeX Setup Tutorial

> Imagine a world where you can collaborate with fellow researchers and students without paying a single cent. This repository makes it possible, a free, local LaTeX workspace that replaces Overleaf.

A comprehensive guide to setting up a local LaTeX workspace with VS Code and Git (your personal Overleaf alternative).

This repository includes:
- **A&A (Astronomy & Astrophysics) Template** - Professional journal template for astronomy papers from A&A
- **Exercise Sheet Template** - Clean layout for university assignments and problem sets
- **Cheat Sheet Template** - Compact multi-column format for quick reference guides
- **Complete setup instructions** - Everything you need to get started locally

## Setup Guide

### 1. Install Prerequisites

#### macOS

```bash
# Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install LaTeX
brew install --cask mactex
```

#### Linux (Ubuntu/Debian)

```bash
sudo apt-get update
sudo apt-get install texlive-full
```

#### Windows

Download and install [MiKTeX](https://miktex.org/download) or [TeX Live](https://tug.org/texlive/windows.html)

### 2. Install VS Code Extensions

- **LaTeX Workshop** (James Yu) - ID: `james-yu.latex-workshop`
  - Automatic compilation
  - Real-time preview while editing
  - Syntax highlighting

- **PDF Viewer** (tomoki1207) - ID: `tomoki1207.pdf`
  - View PDF files directly in VS Code
  - Synced scrolling with your LaTeX source code

```bash
# Via Command Line:
code --install-extension james-yu.latex-workshop
code --install-extension tomoki1207.pdf
```

### 3. Install Additional LaTeX Packages

This is an **important step**! Your LaTeX projects use specific packages via `\usepackage{...}` in your `.tex` files. These packages must be installed on your system for compilation to work.

**Different projects need different packages.** Check the `requirements.txt` file in this repository for a comprehensive list of commonly used packages.

#### Option A: Install all packages at once (Recommended for simplicity)

Install the complete TeX Live scheme with all packages. This ensures compatibility with any LaTeX project:

```bash
sudo tlmgr install scheme-full
```

**Note:** This installation:
- Takes approximately **30 minutes**
- Requires about **8 GB of disk space**
- Covers all standard and many specialized LaTeX packages

#### Option B: Install essential packages only

If you prefer a smaller installation, install just the essential packages:

```bash
# macOS/Linux
sudo tlmgr update --self
sudo tlmgr install amsmath amssymb graphicx fancyhdr hyperref booktabs siunitx mhchem
```

#### Option C: Install packages as needed

Start with a minimal setup and add packages as your projects require them. If your project fails to compile, look for error messages like `! LaTeX Error: File 'package-name.sty' not found`. Then install it:

```bash
sudo tlmgr install package-name
```

See `requirements.txt` for a list of optional packages and what they do.

### 4. Clone Repository Locally

Replace `<your-username>` with your actual GitHub username (example: `git clone git@github.com:john-doe/Underleaf.git`):

```bash
git clone git@github.com:<your-username>/Underleaf.git
cd Underleaf
```

**If SSH doesn't work**, use HTTPS instead:
```bash
git clone https://github.com/<your-username>/Underleaf.git
cd Underleaf
```

### 5. Configure VS Code

In VS Code: `Cmd/Ctrl + Shift + P` → "Preferences: Open Settings (JSON)"

Add the following settings:

```json
{
  "[latex]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "James-Yu.latex-workshop"
  },
  "latex-workshop.latex.autoBuild.run": "onFileChange",
  "latex-workshop.latex.tools": [
    {
      "name": "latexmk",
      "command": "latexmk",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-pdf",
        "-outdir=%OUTDIR%",
        "%DOC%"
      ]
    }
  ]
}
```

## Project Structure

```
.
├── README.md
├── .gitignore
├── requirements.txt
├── template_astronomy/        # A&A journal template for astronomy papers
│   ├── aa_example.tex
│   └── aa.cls
├── template_exercise/         # Exercise sheet template
│   └── main.tex
└── template_cheat_sheet/      # Cheat sheet template
    └── cheat_sheet.tex
```

## Quick Start

If you want to get started immediately:

1. **Complete Steps 1-3** of the Setup Guide above
2. **Pick a template**: 
   - Exercise sheets? → Open `template_exercise/main.tex`
   - Cheat sheet? → Open `template_cheat_sheet/cheat_sheet.tex`
   - Research paper? → Open `template_astronomy/aa_example.tex`
3. **Generate PDF**: Click the **Run** button (▶ icon) in the top-right corner of VS Code, or press `Cmd/Ctrl + Shift + B`
4. **View PDF** - Press `Cmd/Ctrl + Alt + V` to preview, or check the folder for `main.pdf`

**Note:** LaTeX Workshop will compile automatically when you save your file (if configured). You can also manually click **Run** anytime to recompile.

## Useful Git Commands

```bash
# Add changes
git add .

# Create commit
git commit -m "Description of changes"

# Push to repository
git push origin main

# Update local copy
git pull origin main
```

## Tips & Tricks

- **Auto-build on save**: LaTeX Workshop compiles automatically
- **PDF Preview**: Press `Cmd/Ctrl + Alt + V` to open preview
- **Quick new projects**: Use the template folder and duplicate it
- **Git ignore**: Compiled files (.pdf, .aux, .log) are already ignored in .gitignore

## Troubleshooting

### Package not found error

**Error:** `! LaTeX Error: File 'package-name.sty' not found`

**Solution:** Install the missing package:
```bash
sudo tlmgr install package-name
```

### PDF not showing up

**Problem:** LaTeX Workshop isn't creating a PDF

**Solutions:**
1. Check the **Problems** panel in VS Code (Cmd/Ctrl + Shift + M) for error messages
2. Open the `.log` file to see what went wrong
3. Try running `latexmk -pdf` manually in terminal:
   ```bash
   cd your-project-folder
   latexmk -pdf main.tex
   ```

### Permission denied when installing packages

**Error:** `sudo tlmgr install` requires password

**Solution:** Enter your computer password when prompted. You won't see the text, just type and press Enter.

### PDF Viewer not working

**Problem:** PDF preview doesn't open in VS Code

**Solutions:**
1. Make sure you installed the PDF Viewer extension (see Step 2)
2. Restart VS Code
3. Press `Cmd/Ctrl + Alt + V` while viewing a `.pdf` file

## Resources

- [LaTeX Workshop Documentation](https://github.com/James-Yu/LaTeX-Workshop)
- [TeX Live Package Manager](https://www.tug.org/texlive/tlmgr.html)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
