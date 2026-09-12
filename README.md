# JSON Image Viewer

一个轻量、现代、纯前端的 JSON 图片浏览器。

输入一个可访问的 JSON URL，项目会自动识别其中的图片地址，并以响应式画廊展示。支持搜索、历史记录、深色模式、图片大图预览、缩放、键盘切换、复制图片 URL 等功能。

**无需后端、无需数据库、无需 Node.js。** 直接部署到 GitHub Pages、Cloudflare Pages、Nginx 或任意静态网站托管即可。

[![Live Demo](https://img.shields.io/badge/Demo-GitHub%20Pages-4f46e5?style=flat-square)](https://cloudsonly.github.io/JSON-Image-Viewer/)
[![License](https://img.shields.io/badge/license-MIT-22c55e?style=flat-square)](#license)

## ✨ 特性

- 🔗 **JSON URL 加载**：输入远程 JSON 地址即可加载。
- 🧠 **智能识别图片数据**：支持数组、对象数组、嵌套对象，以及常见的 `url`、`src`、`image`、`icon`、`thumbnail`、`preview` 等字段。
- 🖼️ **响应式画廊**：桌面、平板、手机自动适配。
- 🔎 **实时搜索**：按图片名称或 URL 过滤。
- 🔍 **大图预览**：支持上一张 / 下一张、放大、缩小、重置和新窗口打开。
- ⌨️ **键盘操作**：预览时支持 `←` / `→`、`Esc`、`+` / `-`、`0`。
- 📋 **复制图片地址**：一键复制图片 URL。
- 🕘 **访问历史**：自动保存最近访问的 JSON 地址，数据存储在浏览器 `localStorage`。
- 🌙 **深色模式**：支持手动切换，并记住用户选择。
- ⚡ **纯原生实现**：无框架、无 npm、无构建步骤、无后端依赖。
- 🔒 **前端处理**：项目本身没有后端接口，不会把 JSON 数据上传到第三方服务。
- 🧩 **静态部署友好**：适合 GitHub Pages、Cloudflare Pages、Vercel、Netlify、Nginx 等环境。

## 🚀 在线使用

直接打开：

**https://cloudsonly.github.io/JSON-Image-Viewer/**

## 📦 部署

### GitHub Pages

1. Fork 或直接使用本仓库。
2. 保证 `index.html` 位于仓库根目录。
3. 在 GitHub 的 `Settings → Pages` 中选择 `Deploy from a branch`。
4. 选择 `main` 分支和 `/ (root)`。
5. 保存后等待 GitHub Pages 完成部署。

### 其他静态托管

项目没有构建流程，直接上传 `index.html` 即可：

```text
JSON-Image-Viewer/
└── index.html
```

适用于：

- Cloudflare Pages
- Vercel
- Netlify
- Nginx / Apache
- 任意静态文件服务器

## 🧪 支持的 JSON 格式

项目不会要求 JSON 必须严格使用某一种结构，会递归查找常见图片字段。

### 1. 字符串数组

```json
[
  "https://example.com/a.png",
  "https://example.com/b.jpg"
]
```

### 2. 对象数组

```json
[
  {
    "name": "GitHub",
    "url": "https://example.com/github.png"
  },
  {
    "name": "Example",
    "url": "https://example.com/example.png"
  }
]
```

### 3. 常见容器字段

```json
{
  "name": "My Icons",
  "images": [
    { "name": "One", "url": "https://example.com/1.png" },
    { "name": "Two", "url": "https://example.com/2.png" }
  ]
}
```

也支持 `data`、`items`、`list`、`results`、`photos`、`icons` 等常见字段，以及更深层的嵌套结构。

## 🔧 图片字段识别

对象中的以下字段会被优先作为图片地址：

```text
url
imageUrl
src
image
icon
thumbnail
preview
cover
logo
```

名称字段会优先读取：

```text
name
title
filename
label
displayName
alt
```

如果没有名称，会自动生成 `图片 1`、`图片 2` 等名称。

## ⚠️ CORS 注意事项

这是一个纯浏览器端项目，因此加载远程 JSON 时，**目标服务器必须允许跨域请求（CORS）**。

例如目标服务器需要返回类似：

```http
Access-Control-Allow-Origin: *
```

如果浏览器提示 `Failed to fetch`，即使 URL 在浏览器地址栏里能够正常打开，也可能是 CORS 限制。

### GitHub Raw

GitHub Raw 是比较适合此项目的 JSON 数据来源，例如：

```text
https://raw.githubusercontent.com/<user>/<repo>/main/images.json
```

## 🛡️ 隐私说明

项目本身没有服务器端代码，也没有数据库。

JSON 请求由你的浏览器直接发送到你输入的 URL；访问历史和主题设置仅保存在当前浏览器的 `localStorage` 中。

因此：

- 不需要登录。
- 不需要账号系统。
- 不需要后端 API。
- 不会由本项目代为上传你的 JSON。

但需要注意：**你的浏览器仍然会直接请求你输入的第三方 URL**，因此具体数据如何处理取决于目标站点和浏览器本身。

## ⌨️ 快捷键

图片大图预览时：

| 快捷键 | 功能 |
| --- | --- |
| `←` | 上一张 |
| `→` | 下一张 |
| `Esc` | 关闭预览 |
| `+` / `=` | 放大 |
| `-` | 缩小 |
| `0` | 重置缩放 |

鼠标滚轮也可以在大图预览中调整缩放。

## 🛠️ 技术栈

项目采用浏览器原生能力实现：

- HTML5
- CSS3
- Vanilla JavaScript
- Fetch API
- LocalStorage
- GitHub Pages

不依赖：

- React / Vue / Angular
- jQuery
- Bootstrap / Tailwind
- npm / pnpm / yarn
- Node.js 构建工具
- 后端服务

## 🧹 本次优化重点

相比早期版本，本项目重点做了以下调整：

### 性能

- 使用 `DocumentFragment` 批量渲染图片卡片，减少重复 DOM 操作。
- 图片启用 `loading="lazy"` 与异步解码。
- 搜索直接过滤内存中的数据，而不是反复查询整个 DOM。
- 加载新 URL 时自动取消上一个未完成请求。
- 增加请求超时控制，避免页面长期停留在加载状态。
- 对图片 URL 做去重，减少重复渲染。

### 稳定性

- 对 URL、JSON、网络请求分别进行错误处理。
- 对损坏的 `localStorage` 历史数据自动恢复。
- 图片加载失败时显示占位状态，不影响其他图片。
- 支持递归扫描更深层 JSON 结构。
- 避免将用户提供的名称和 URL 直接拼进 HTML，降低 DOM 注入风险。

### 用户体验

- 增加深色模式。
- 增加真正的图片大图查看器。
- 支持键盘切图和缩放。
- 搜索结果实时显示。
- 历史记录操作更清晰。
- 移动端布局重新适配。
- 减少对第三方图标 CDN 的依赖，核心界面可以离线运行。

## 📁 项目结构

```text
JSON-Image-Viewer/
├── index.html
└── README.md
```

目前项目特意保持为单文件结构，方便个人使用、Fork 和直接部署。

## 💡 后续可以继续加入

如果项目继续扩展，可以考虑：

- 支持直接上传本地 JSON 文件。
- 支持粘贴 JSON 文本。
- 支持从 JSON 中选择指定数组路径。
- 支持瀑布流 / 网格大小切换。
- 支持收藏图片。
- 支持批量复制 URL。
- 支持导出图片列表为 JSON / TXT。
- 支持自定义图片字段映射。
- 支持从 URL 查询参数直接打开指定 JSON。

## 📄 License

本项目采用 **MIT License**。

