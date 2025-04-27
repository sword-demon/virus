---
title: electron uninstall question
date: 2025-03-16 01:14:08
tags: [electron, React]
categories: [electron]
---

## 前言

使用`electron-vite`创建一个项目

```bash
pnpm create @quick-start/electron
```

```bash
$ pnpm create @quick-start/electron
.../1959aa47c0c-3bae                     | Progress: resolved 1, reused 0, downl.../1959aa47c0c-3bae                     | Progress: resolved 4, reused 1, downl.../1959aa47c0c-3bae                     |   +8 +
.../1959aa47c0c-3bae                     | Progress: resolved 4, reused 1, downl.../1959aa47c0c-3bae                     | Progress: resolved 8, reused 2, downl.../1959aa47c0c-3bae                     | Progress: resolved 8, reused 2, downloaded 6, added 8, done
✔ Project name: … snippets
✔ Select a framework: › react
✔ Add TypeScript? … No / Yes
✔ Add Electron updater plugin? … No / Yes
✔ Enable Electron download mirror proxy? … No / Yes

Scaffolding project in /Users/wxvirus/WebStormProjects/snippets...

Done. Now run:

  cd snippets
  pnpm install
  pnpm dev

```

## 然后启动报错

> 错误内容

```bash
dev server running for the electron renderer process at:

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
error during start dev server and electron app:
Error: Electron uninstall
    at getElectronPath
```

## 解决办法

```bash
sudo npm install -g electron-fix
electron-fix start
```

> 效果如下

```bash
$ electron-fix start
Electron version: 34.2.0
✔ Download Electron successful!
✔ Write configuration succeeded!
✔ Unzip Electron successful!
✔ Success!

```

## 常用快捷键配置

```bash
vim ~/.zshrc

# pnpm
alias p="pnpm "
alias pd="pnpm dev"
alias pb="pnpm build"
alias pp="pnpm preview"

# git
alias gb="git branch"
alias ga="git add -A"
alias go="git checkout"
alias gp="git push;git push gitee"
alias gl="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
