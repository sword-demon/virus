---
title: electron-snippets-window
date: 2025-03-16 14:15:35
tags: [electron]
---

## 更改窗口在屏幕里的位置

通过主进程的代码进行控制

`src/main/index.ts`

```typescript
import { app, shell, BrowserWindow, ipcMain, screen } from 'electron'
import { join } from 'path'
import { electronApp, optimizer, is } from '@electron-toolkit/utils'
import icon from '../../resources/icon.png?asset'

function createWindow(): void {
  // 获取主屏幕的高度和宽度
  const { width } = screen.getPrimaryDisplay().workAreaSize
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    width: 600,
    height: 600,
    show: false,
    x: width - 600,
    y: 50,
    autoHideMenuBar: true,
    // 永远保持置顶
    // alwaysOnTop: true,
    ...(process.platform === 'linux' ? { icon } : {}),
    webPreferences: {
      preload: join(__dirname, '../preload/index.js'),
      sandbox: false
    }
  })

  // ... 其他代码
```