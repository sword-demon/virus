---
title: snippets-搜索组件
date: 2025-03-16 14:35:05
tags: [electron]
---

## 搜索组件

### 安装tailwindcss3

```bash
pnpm install -D tailwindcss@3 postcss autoprefixer
npx tailwindcss init -p
```

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./src/**/*.{js,ts,tsx,jsx}', './index.html'],
  theme: {
    extend: {}
  },
  plugins: []
}

```

### vscode react插件

- `ES7+React/Redux/React-Native snippets`
- 快捷键：`rfc`


### 创建搜索组件

`src/renderer/src/components/Search/index.tsx`

```tsx
export default function Search() {
  return (
    <div className="bg-slate-50 p-5">
      <section className="bg-slate-100 p-3">
        <input className="w-full outline-none text-2xl text-slate-600" />
      </section>
    </div>
  )
}
```

然后在`App.tsx`中进行使用

```tsx
import Search from './components/Search'

function App(): JSX.Element {
  return (
    <>
      <Search />
    </>
  )
}

export default App

```

效果图


![搜索组件雏形](https://virusoss.oss-cn-shanghai.aliyuncs.com/2025/03/16/17421077459576.jpg)


## 安装sass使用scss
```bash
pnpm install -D sass
```

`src/renderer/src/assets/global.scss`

```scss
body {
    @apply bg-black;
}
```

## 配置窗口透明

```tsx
const mainWindow = new BrowserWindow({
    width: 600,
    height: 600,
    show: false,
    x: width - 600,
    y: 50,
    autoHideMenuBar: true,
    // 透明
    transparent: true,
    // 永远保持置顶
    // alwaysOnTop: true,
    ...(process.platform === 'linux' ? { icon } : {}),
    webPreferences: {
      preload: join(__dirname, '../preload/index.js'),
      sandbox: false
    }
  })
```

## 调整搜索组件样式

```tsx
export default function Search() {
  return (
    <div className="bg-slate-50 p-3 rounded-lg">
      <section className="bg-slate-200 p-3 rounded-lg">
        <input className="w-full outline-none text-2xl text-slate-500 bg-slate-200" />
      </section>
    </div>
  )
}

```

## 通过css拖动electron窗口

```css
.drag {
    -webkit-app-region: drag;
}

.nodrag,input,select,textarea,option {
    -webkit-app-region: no-drag;
}
```

我们给搜索组件添加上`drag`

```tsx
export default function Search() {
  return (
    <div className="bg-slate-50 p-3 rounded-lg drag">
      <section className="bg-slate-200 p-3 rounded-lg">
        <input className="w-full outline-none text-2xl text-slate-500 bg-slate-200" />
      </section>
    </div>
  )
}
```

>这个时候就可以看到一个透明的无标题框的搜索框，而且可以随意拖动


## 使用vscode插件 lorem 自动生成一段假数据


## 定义假数据
`src/renderer/src/data.ts`
```ts
/**
 * 数据的类型
 */
export interface DataType {
  id: number
  content: string
}

export const data = [
  { id: 1, content: 'sdddsdserge' },
  { id: 2, content: 'sdddsdshe' },
  { id: 3, content: 'sdddsdsgwerg' },
  { id: 4, content: 'sdddsdfewfews' },
  { id: 5, content: 'sdddsdsdwqwqd' },
  { id: 6, content: 'sdddsdsdqwdqw' },
  { id: 7, content: 'sdddsdsdwqdq' }
] as DataType[]

```

## 新建一个结果组件

```tsx
import { useState } from 'react'
import { data as codes } from '@renderer/data'
/**
 * 显示结果组件
 * @returns
 */
export default function Result() {
  // 定义响应式数据
  const [data, setData] = useState(codes)
  return (
    <main className="bg-slate-50 px-3">
      {data.map((item) => (
        <div key={item.id} className="text-slate-700 truncate mb-2">
          {item.content}
        </div>
      ))}
    </main>
  )
}
```

>最后别忘了在`App.tsx`里使用


![添加结果组件后循环遍历假数据](https://virusoss.oss-cn-shanghai.aliyuncs.com/2025/03/16/17421144204597.jpg)


## 优化搜索框圆角样式

结果组件样式调整

```tsx
import { useState } from 'react'
import { data as codes } from '@renderer/data'
/**
 * 显示结果组件
 * @returns
 */
export default function Result() {
  // 定义响应式数据
  const [data, setData] = useState(codes)
  return (
    <main className="bg-slate-50 px-3 rounded-bl-lg rounded-br-lg -mt-[7px] pb-2">
      {data.map((item) => (
        <div key={item.id} className="text-slate-700 truncate mb-2">
          {item.content}
        </div>
      ))}
    </main>
  )
}

```

---

搜索组件样式调整

```tsx
export default function Search() {
  return (
    // 圆角底部的左侧和底部的右侧
    <main className="bg-slate-50 p-3 rounded-lg drag">
      <section className="bg-slate-200 p-3 rounded-lg">
        <input className="w-full outline-none text-2xl text-slate-500 bg-slate-200" />
      </section>
      <section className="text-center text-slate-600 text-xs mt-2">无解的游戏 / wxvirus</section>
    </main>
  )
}

```