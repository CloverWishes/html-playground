# HTML Playground

[**English**](#english) | [**中文**](#chinese)

---

## <a id="english"></a>English

> A lightweight PWA for creating, editing, and previewing HTML/CSS/JS pages on iOS / browser — fully offline, zero dependencies.

### Features

- **Create** pages with any HTML/CSS/JS code (title + source)
- **Persist** all data in IndexedDB (falls back to localStorage) — survives browser close / offline
- **Preview** via Blob → objectURL rendered in an iframe
- **Edit** saved pages with preview/edit switching; `Ctrl+S` / `⌘+S` to save
- **Manage** page list sorted by update time (open / edit / delete)
- **PWA** — add to iOS home screen, works offline

### Tech Stack

- Pure **HTML5 + CSS3 + JavaScript (ES6+)**
- **PWA**: `manifest.json` + `sw.js` (ServiceWorker for offline cache)
- **IndexedDB** as primary storage, **localStorage** as fallback
- Zero dependencies — no frameworks, no CDN, no third-party libraries

### File Structure

```
html-playground/
├── index.html       # Main app (UI + logic)
├── manifest.json    # PWA manifest (icons, start URL)
├── sw.js            # Service Worker (offline cache rules)
└── README.md        # This file
```

### Usage

Open `https://cloverwishes.github.io/html-playground` in any browser.

| Action | How |
|---|---|
| **Create** | Enter title + HTML → click **💾 保存** |
| **Preview** | Click **打开** on a page item |
| **Edit** | Click **编辑** → edit code → click **💾 保存并预览** or `Ctrl+S` / `⌘+S` |
| **Delete** | Click **删除** on a page item |
| **Back** | Click **← 返回** in the navbar |

#### Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Enter` (in title field) | Focus the code editor |
| `Ctrl+Enter` / `⌘+Enter` (in editor) | Create new page |
| `Ctrl+S` / `⌘+S` (in edit mode) | Save and switch to preview |

### Data Model

All data is stored under a single key `html_playground_pages`:

```javascript
// IndexedDB store 'pages' → key 'html_playground_pages'
// localStorage fallback → key 'html_playground_pages'
[
  {
    id: 'timestamp-random',     // Unique ID
    title: 'My Page',           // Page title
    content: '<html>...</html>', // Full HTML source
    updatedAt: 1700000000000    // Timestamp (ms)
  }
]
```

#### Storage Priority

1. **IndexedDB** (`html-playground` database, `pages` object store)
2. **localStorage** (automatic fallback if IndexedDB unavailable)

### Deployment (GitHub Pages)

This project lives in a subdirectory `/html-playground/`, so all resource paths use absolute sub-paths:

```html
<!-- index.html -->
<link rel="manifest" href="/html-playground/manifest.json">
navigator.serviceWorker.register('/html-playground/sw.js')
```

```json
// manifest.json
"start_url": "/html-playground/"
```

```javascript
// sw.js
const urlsToCache = [
  '/html-playground/',
  '/html-playground/index.html',
  '/html-playground/manifest.json'
];
```

To deploy:
1. Push to the `html-playground` folder in your GitHub Pages repo
2. Enable GitHub Pages on the branch where this folder lives
3. Visit `https://cloverwishes.github.io/html-playground`

### iOS Home Screen Setup

1. Open `https://cloverwishes.github.io/html-playground` in **Safari** (trailing slash required)
2. Tap **Share** → **Add to Home Screen**
3. The icon launches in fullscreen mode (`display: standalone`)

### Browser Compatibility

| Feature | Support |
|---|---|
| IndexedDB | iOS 8+, all modern browsers |
| localStorage | All browsers (fallback) |
| Service Worker | iOS 11.3+, all modern browsers |
| `backdrop-filter` | iOS 9+, all modern browsers |
| PWA `display: standalone` | iOS 12.1+ (Safari) |

On iOS 26+ all features are fully supported. IndexedDB works correctly in both normal and private browsing since iOS 17+.

### Notes

- No external dependencies — everything is self-contained in 3 files
- All data is stored locally — there is no server
- Clearing browser data will delete all saved pages
---

## <a id="chinese"></a>中文

> 一个轻量级 PWA 应用，在 iOS / 浏览器端创建、编辑和预览 HTML/CSS/JS 页面，完全离线可用，零依赖。

### 功能

- **创建**包含任意 HTML/CSS/JS 代码的子页面（标题 + 源码）
- **持久化**存储到 IndexedDB（回退到 localStorage）— 关闭浏览器或离线数据不丢失
- **预览**通过 Blob 生成 objectURL 放入 iframe 渲染
- **编辑**已保存页面（支持预览/编辑切换，`Ctrl+S` / `⌘+S` 快捷键保存）
- **管理**页面列表按更新时间倒序排列（打开 / 编辑 / 删除）
- **PWA** — 可添加至 iOS 主屏幕，离线可用

### 技术栈

- 纯原生 **HTML5 + CSS3 + JavaScript (ES6+)**
- **PWA**：`manifest.json` + `sw.js`（ServiceWorker 离线缓存）
- **IndexedDB** 为主存储，**localStorage** 为回退方案
- **零依赖** — 无框架、无 CDN、无第三方库

### 文件结构

```
html-playground/
├── index.html       # 主应用（所有 UI 和逻辑）
├── manifest.json    # PWA 清单（图标、启动地址等）
├── sw.js            # Service Worker（离线缓存规则）
└── README.md        # 本文件
```

### 使用方法

用浏览器打开 `https://cloverwishes.github.io/html-playground`。

| 操作 | 方法 |
|---|---|
| **创建** | 输入标题 + HTML → 点击 **💾 保存** |
| **预览** | 点击页面条目的 **打开** |
| **编辑** | 点击 **编辑** → 修改代码 → 点击 **💾 保存并预览** 或按 `Ctrl+S` / `⌘+S` |
| **删除** | 点击页面条目的 **删除** |
| **返回** | 点击导航栏的 **← 返回** |

#### 快捷键

| 快捷键 | 操作 |
|---|---|
| `Enter`（标题输入框） | 聚焦到代码编辑器 |
| `Ctrl+Enter` / `⌘+Enter`（编辑器中） | 创建新页面 |
| `Ctrl+S` / `⌘+S`（编辑模式） | 保存并切换到预览 |

### 数据模型

所有数据存储在单一键 `html_playground_pages` 下：

```javascript
// IndexedDB 存储空间 'pages' → 键 'html_playground_pages'
// localStorage 回退 → 键 'html_playground_pages'
[
  {
    id: 'timestamp-random',      // 唯一标识
    title: '我的页面',            // 页面标题
    content: '<html>...</html>', // 完整 HTML 源码
    updatedAt: 1700000000000     // 更新时间戳（毫秒）
  }
]
```

#### 存储优先级

1. **IndexedDB**（`html-playground` 数据库，`pages` 对象存储）
2. **localStorage**（IndexedDB 不可用时自动回退）

### 部署（GitHub Pages）

项目位于子目录 `/html-playground/`，所有资源引用使用绝对子路径：

```html
<!-- index.html -->
<link rel="manifest" href="/html-playground/manifest.json">
navigator.serviceWorker.register('/html-playground/sw.js')
```

```json
// manifest.json
"start_url": "/html-playground/"
```

```javascript
// sw.js
const urlsToCache = [
  '/html-playground/',
  '/html-playground/index.html',
  '/html-playground/manifest.json'
];
```

部署步骤：
1. 将文件推送至 GitHub Pages 仓库的 `html-playground` 文件夹
2. 在该分支上启用 GitHub Pages
3. 访问 `https://cloverwishes.github.io/html-playground`

### iOS 主屏幕添加

1. 用 **Safari** 打开 `https://cloverwishes.github.io/html-playground`（末尾带斜杠）
2. 点击 **分享** → **添加到主屏幕**
3. 图标将以全屏模式启动（`display: standalone`）

### 浏览器兼容性

| 特性 | 支持范围 |
|---|---|
| IndexedDB | iOS 8+，所有现代浏览器 |
| localStorage | 所有浏览器（回退方案） |
| Service Worker | iOS 11.3+，所有现代浏览器 |
| `backdrop-filter` | iOS 9+，所有现代浏览器 |
| PWA `display: standalone` | iOS 12.1+（Safari） |

iOS 26+ 全面支持所有特性。IndexedDB 自 iOS 17+ 起在普通浏览和无痕模式下均正常工作。

### 注意事项

- 无外部依赖 — 3 个文件完全自包含
- 所有数据存储在浏览器本地 — 无需服务器
- 清除浏览器数据将删除所有已保存的页面

