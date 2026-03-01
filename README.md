# blendOS v4 Setup Guide - Ready to Go!

## What We Just Did:

### 1. ✅ Updated Dotfiles Repo
- Pushed your current Hyprland config
- Pushed your .zshrc and .p10k.zsh
- Repo: https://github.com/TimothyBear11/Dotfiles

### 2. ✅ Updated blendOS Track
- Added all missing packages (ROCm, Ollama, CLI tools)
- Added automatic dotfiles deployment
- Configured services (ollama, sddm)
- Set up user groups for ROCm
- Repo: https://github.com/TimothyBear11/tracks

---

## Installing blendOS with Your Track:

### 1. Download blendOS v4
- Get the ISO: https://blendos.co/download/

### 2. Boot the Live Environment

### 3. During Installation
When prompted for a track/config:
```
https://github.com/TimothyBear11/tracks/raw/main/hyprland.yaml
```

Or after installation, you can update to your track:
```bash
sudo akshara update https://github.com/TimothyBear11/tracks/raw/main/hyprland.yaml
```

---

## Post-Install Tasks:

### 1. Link Persistent Memory
```bash
ln -s /home/tbear/Games/Steam/openclaw-memory ~/.openclaw/workspace/memory
ln -s /home/tbear/Games/Steam/openclaw-memory/MEMORY.md ~/.openclaw/workspace/MEMORY.md
```

### 2. Verify ROCm
```bash
rocminfo | grep -A 10 "Agent 2"
```
Should show your RX 6700 XT as gfx1030.

### 3. Test Ollama
```bash
systemctl status ollama
ollama pull qwen2.5-coder:7b
ollama run qwen2.5-coder:7b
```

### 4. Verify Services
```bash
systemctl --user status ollama
rocm-smi  # Check GPU
```

---

## What Your Track Includes:

**Desktop Environment:**
- ✅ Hyprland with all tools (grim, slurp, etc.)
- ✅ Noctalia-shell (your current bar)
- ✅ SDDM login manager

**Development:**
- ✅ Zsh with powerlevel10k
- ✅ Neovim
- ✅ Modern CLI tools (eza, bat, fd, fzf, zoxide)
- ✅ GitHub CLI (logged in)

**AI/ML:**
- ✅ ROCm (configured for RX 6700 XT)
- ✅ Ollama with ROCm support
- ✅ User added to render/video groups

**Gaming:**
- ✅ Steam
- ✅ Heroic Games Launcher
- ✅ Wine staging + winetricks
- ✅ ProtonUp-Qt

**Apps:**
- ✅ Kitty terminal
- ✅ Floorp browser
- ✅ Telegram
- ✅ Spotify + Spicetify
- ✅ Vesktop (Discord)
- ✅ KDE Connect

**Your Configs Auto-Deployed:**
- ✅ Hyprland config (with all your keybinds/rules)
- ✅ Kitty config
- ✅ .zshrc with all your aliases
- ✅ .p10k.zsh theme

---

## Updating Your Track Later:

If you want to change something:

1. Edit `~/tracks/hyprland.yaml`
2. Commit and push:
   ```bash
   cd ~/tracks
   git add hyprland.yaml
   git commit -m "Description of changes"
   git push
   ```
3. On blendOS, update:
   ```bash
   sudo akshara update
   ```

---

## Updating Your Dotfiles:

1. Make changes to your local configs
2. Copy to dotfiles repo and push:
   ```bash
   cd ~/dotfiles-temp
   cp ~/.config/hypr/hyprland.conf hypr/
   git add .
   git commit -m "Updated config"
   git push
   ```
3. Rebuild blendOS to pull new dotfiles:
   ```bash
   sudo akshara update
   ```

---

## Rollback if Something Breaks:

blendOS keeps previous deployments. If an update breaks:

1. Reboot
2. At GRUB, you'll see previous deployments
3. Boot into the working one
4. Fix your track YAML
5. Update again

---

## Additional Notes:

- **Default username:** Probably `blend` (check during install)
- **Games drive:** Your nvme1n1 will still be there, no reinstall needed
- **Immutability:** Base system is read-only, all changes via system.yaml
- **Containers:** Use `blend` command or distrobox for additional software

---

You're all set! Ready to try blendOS? 🐻🚀
