# Semi Design- AI Friendly

一个本地复用的 Semi Design 主题样式包。这个包只提供一份可直接引入的全局主题 CSS，直接接入 AI IDE 工具中使用，不包含组件、不需要 TypeScript 构建，也不依赖 Rollup 或 Vite 打包流程。

## 目录

```text
my-theme-package/
├── .gitignore
├── package.json
├── README.md
└── styles/
    └── globals.css
```

## 本地安装

在另一个项目里，通过本地路径安装：

```bash
npm install ../my-theme-package
```

也可以显式使用 `file:`：

```bash
npm install file:../my-theme-package
```

路径请按你的实际目录调整。

## 使用方式

推荐在目标项目的全局样式入口文件中引入：

- React / Vite: `src/index.css` 或 `src/styles/globals.css`
- Next.js App Router: `src/app/globals.css` 或 `app/globals.css`
- 其他项目：应用级全局 CSS 入口文件

引入示例：

```css
@import "my-theme-package/globals.css";
```

如果你的项目是从 JS/TS 入口引全局样式，也可以这样写：

```ts
import "my-theme-package/globals.css";
```

## 接入示例

### React / Vite

1. 安装本地包：

```bash
npm install file:../my-theme-package
```

2. 在 `src/main.tsx` 中保留全局样式入口：

```ts
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

3. 在 `src/index.css` 中引入主题包：

```css
@import "my-theme-package/globals.css";
```

### Next.js App Router

1. 安装本地包：

```bash
npm install file:../my-theme-package
```

2. 在 `src/app/globals.css` 或 `app/globals.css` 中引入：

```css
@import "my-theme-package/globals.css";
```

3. 在 `src/app/layout.tsx` 或 `app/layout.tsx` 中继续加载全局样式：

```tsx
import "./globals.css";

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="zh-CN">
      <body>{children}</body>
    </html>
  );
}
```

### 纯 JS / TS 入口

如果项目没有单独的 CSS 入口文件，也可以直接在应用入口引入：

```ts
import "my-theme-package/globals.css";
```

## 维护方式

直接修改 `styles/globals.css` 即可。因为这是本地路径安装，修改后通常重新启动目标项目，或重新执行一次安装，就能同步最新内容。

## 注意

当前 `styles/globals.css` 使用了 Tailwind CSS v4 的 `@theme inline` 语法。

这意味着：

1. 目标项目需要能处理 Tailwind v4 的 CSS
2. 如果目标项目不是 Tailwind v4 环境，`@theme inline` 这部分不会按预期工作

如果你后面要把它改成“纯 CSS Variables 版本”，可以再拆出一个不依赖 Tailwind v4 的兼容版。
