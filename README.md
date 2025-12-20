# 📝 Juleaf
> A free, open-source alternative to Overleaf for Julia developers. Write academic papers with live code execution and instant PDF preview.

![Julia](https://img.shields.io/badge/Julia-1.9+-9558B2?logo=julia)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-stable-brightgreen)

## ✨ Features

-  **Split-pane interface** - Code on left, PDF preview on right
-  **Live compilation** - Auto-compiles 2 seconds after typing
- **Execute Julia code** - Run code blocks and embed plots directly
- **Publication-ready** - LaTeX equations, CairoMakie plots, professional formatting
- **No cloud dependency** - Runs completely offline on your machine
- **Pure Julia** - No Jupyter or Python required
- **100% Free** - No subscriptions, no limits

Perfect for research papers, technical reports, and scientific documentation.

---

## 📋 Prerequisites

### 1. Install Julia

**macOS:**
```bash
# Via Homebrew
brew install julia

# Or download from https://julialang.org/downloads/
```

**Linux:**
```bash
# Ubuntu/Debian
sudo apt-get install julia

# Arch
sudo pacman -S julia

# Or download from https://julialang.org/downloads/
```

**Windows:**
- Download installer from [julialang.org/downloads](https://julialang.org/downloads/)
- Run installer and follow prompts
- Add Julia to PATH when prompted

Verify installation:
```bash
julia --version
# Should show: julia version 1.9 or higher
```

### 2. Install LaTeX Engine

**macOS:**

*Option A: TinyTeX* (Recommended - ~200MB)
```bash
brew install quarto
quarto install tinytex
```

*Option B: MacTeX* (~4GB)
```bash
brew install --cask mactex-no-gui
```

**Linux:**

*Option A: TinyTeX*
```bash
# Install Quarto first
sudo wget https://quarto.org/download/latest/quarto-linux-amd64.deb
sudo dpkg -i quarto-linux-amd64.deb
quarto install tinytex
```

*Option B: TeX Live*
```bash
# Ubuntu/Debian
sudo apt-get install texlive-xetex texlive-latex-extra

# Arch
sudo pacman -S texlive-core texlive-latexextra
```

**Windows:**

*Option A: TinyTeX*
```powershell
# Install Quarto from https://quarto.org/docs/get-started/
# Then in PowerShell/CMD:
quarto install tinytex
```

*Option B: MiKTeX*
- Download from [miktex.org](https://miktex.org/download)
- Run installer

### 3. Configure PATH (TinyTeX only)

**macOS:**
```bash
echo 'export PATH="$HOME/Library/TinyTeX/bin/universal-darwin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**Linux:**
```bash
echo 'export PATH="$HOME/.TinyTeX/bin/x86_64-linux:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

**Windows:**
TinyTeX auto-configures PATH. Restart terminal if needed.

Verify:
```bash
# macOS/Linux
which xelatex

# Windows (PowerShell)
where.exe xelatex
```

---

## 🚀 Installation

### 1. Clone or Download
```bash
git clone https://github.com/yourusername/julia-weave-editor.git
cd julia-weave-editor
```

Or download the three files:
- `server.jl`
- `editor.html`
- `README.md`

### 2. Install Julia Dependencies
Start Julia **in the project directory**:
```bash
cd julia-weave-editor
julia --project=.
```

In the Julia REPL:
```julia
using Pkg
Pkg.activate(".")
Pkg.add(["HTTP", "Weave", "CairoMakie"])
```

Wait for installation to complete (first time may take a few minutes).

---

## 🎯 Usage

### Start the Server

**macOS/Linux:**
```bash
julia --project=. server.jl
```

**Windows (PowerShell/CMD):**
```powershell
julia --project=. server.jl
```

You should see:
```
Starting Overleaf-like server on http://localhost:8080
Press Ctrl+C to stop
```

### Open in Browser
Navigate to: **http://localhost:8080**

### Using the Editor

1. **Edit code** in the left pane
2. **Auto-compile**: Waits 2 seconds after you stop typing
3. **Manual compile**: 
   - Click "Compile" button
   - Mac: `Cmd+S`
   - Windows/Linux: `Ctrl+S`
4. **View PDF** in the right pane

### Example Document Syntax

```julia
---
title: "My Research Paper"
---

## Introduction

This is a scientific document with executable Julia code.

```julia
using CairoMakie

# Generate data
x = range(0, 10, 100)
y = sin.(x) .* exp.(-0.1x)

# Create plot
fig = Figure(size = (600, 400))
ax = Axis(fig[1, 1], 
    xlabel = "Time (s)", 
    ylabel = "Amplitude",
    title = "Damped Oscillation"
)
lines!(ax, x, y, color = :blue, linewidth = 2)
fig
```

## Results

The plot above shows exponential decay with the equation:

$$
y(t) = \sin(t) \cdot e^{-0.1t}
$$
```

---

## 🛠️ Troubleshooting

### "Package HTTP not found"
```bash
cd your-project-directory
julia --project=.
```
Then in Julia:
```julia
using Pkg
Pkg.add(["HTTP", "Weave", "CairoMakie"])
```

### "could not spawn xelatex"

**All platforms:**
```bash
# macOS/Linux
which xelatex

# Windows (PowerShell)
where.exe xelatex
```

If empty:
- **macOS**: Add TinyTeX to PATH (see Prerequisites), restart terminal
- **Linux**: Add TinyTeX to PATH (see Prerequisites), run `source ~/.bashrc`
- **Windows**: Reinstall TinyTeX or MiKTeX, restart terminal
- **All**: Restart Julia after installing LaTeX

### "Compilation failed"
- Check browser console (`F12`) for errors
- View terminal output for detailed messages
- Ensure all Julia packages installed
- Verify LaTeX installation

### Port 8080 already in use
Edit `server.jl`:
```julia
const PORT = 3000  # Change to any available port
```

### Windows-specific: "Permission denied"
Run PowerShell/CMD as Administrator when installing packages.

---

## 📦 What You Get

The app includes:
- Full markdown support
- LaTeX equation rendering
- Julia code execution
- CairoMakie plot generation
- Automatic PDF compilation
- Keyboard shortcuts
- Live preview updates

---

## 🔧 Advanced Usage

### Custom Port
```julia
# In server.jl
const PORT = 3000  # Use any available port
```

### Additional Packages
Install any Julia package for use in documents:
```julia
using Pkg
Pkg.add("DataFrames")  # Example
```

Then use in your `.jmd` files:
```julia
using DataFrames
df = DataFrame(A = 1:4, B = ["M", "F", "F", "M"])
```

---

## 🚀 Future Enhancements

- [ ] Syntax highlighting (CodeMirror integration)
- [ ] Multiple file support
- [ ] Project save/load functionality
- [ ] Export to HTML, Word, Markdown
- [ ] Collaborative editing (WebSockets)
- [ ] Dark mode
- [ ] Custom themes
- [ ] BibTeX support

---

## 📜 Requirements Summary

| Component | Version | Required |
|-----------|---------|----------|
| Julia | ≥ 1.9 | ✅ |
| HTTP.jl | Latest | ✅ |
| Weave.jl | Latest | ✅ |
| CairoMakie.jl | Latest | ✅ |
| TinyTeX or MacTeX | Any | ✅ |

---

## 🤝 Contributing

Contributions welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests
- Improve documentation

---

##  License

MIT License - Free for personal and commercial use.

---

## Why This Exists

Overleaf is great but requires internet and has limitations. This project provides:
- **Complete offline functionality**
- **No usage limits**
- **Full Julia integration**
- **Zero cost**
- **Privacy** (your documents stay on your machine)

Perfect for researchers, students, and anyone writing technical documents with Julia.

---

## 📧 Support

Having issues? 
1. Check the Troubleshooting section
2. Review the Prerequisites
3. Open an issue on GitHub

---

**Built with ❤️ for the Julia community**
