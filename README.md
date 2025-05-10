## 🚀 Chrome Extension Vite Template with TypeScript, TailwindCSS, ShadCN UI

This boilerplate is a modern template to kickstart your Chrome (and Firefox) extension development using:

- ⚡️ Vite
- 🧠 React (with component folder structure)
- ⛑️ TypeScript
- 🎨 TailwindCSS 4
- 🧩 ShadCN UI (optional components with accessibility)
- 🔥 Manifest V3 ready

Built for scalable, component-based development similar to React apps, but structured for browser extension environments.

---

## 🧰 Usage

```bash
npm install           # install dependencies
npm run build         # production build
```

Then:

1. Open `chrome://extensions` in your Chrome browser.
2. Enable **Developer Mode**.
3. Click **Load unpacked**.
4. Select the `dist_chrome` folder.

---

## 📁 Folder Structure

```bash
src/
├── assets/                   # Static icons/images
├── background/               # Service worker logic (background.js)
│   └── index.ts
├── content/                  # Scripts injected into web pages
│   └── index.ts
├── pages/
│   ├── devtools/             # Custom Chrome DevTools panel
│   │   └── index.tsx
│   ├── options/              # Settings or options page
│   │   └── index.tsx
│   ├── popup/                # The popup that appears on extension click
│   │   └── index.tsx
│   └── panel/                # Optional Side Panel (manifest-defined)
│       └── index.tsx
├── components/               # Shared reusable React-style components
│   └── UI/                   # ShadCN-based UI components
├── hooks/                    # Custom hooks (e.g., useChromeStorage)
├── locales/                  # i18n translation files (if enabled)
├── styles/                   # Tailwind config + global styles
├── manifest.json             # Chrome extension manifest (v3)
└── vite.config.base.ts       # Vite config shared across builds
```

---

## 🔍 Explanation of Each Part

| Directory     | Purpose                                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------ |
| `popup/`      | UI shown when clicking the extension icon. Acts like a mini-app.                                 |
| `options/`    | The options/settings page users can open from `chrome://extensions`. Great for user preferences. |
| `devtools/`   | Creates a custom panel in Chrome DevTools. Useful for debugging tools or profiling.              |
| `background/` | Contains the background service worker, handles lifecycle events, alarms, and message passing.   |
| `content/`    | Runs scripts directly in the context of web pages. Useful for DOM access and interaction.        |
| `panel/`      | Optional side panel UI (only available in Chrome, requires `"sidePanel"` permission).            |
| `components/` | Reusable UI elements written in a React-like structure with ShadCN components.                   |
| `hooks/`      | Utility hooks, including Chrome local/sync storage wrappers.                                     |
| `locales/`    | Supports internationalization (i18n). Only enabled if `localize: true` in Vite config.           |

---

## 🧪 Development & Build Scripts

```bash
# Chrome dev build
npm run dev:chrome

# Firefox dev build
npm run dev:firefox

# Production build for Chrome
npm run build:chrome

# Production build for Firefox
npm run build:firefox
```

Output folders: `dist_chrome/` or `dist_firefox/`

---

## ✅ Manifest v3 Config Highlights

```json
{
  "manifest_version": 3,
  "name": "Your Extension Name",
  "description": "A modern Vite + React + TS + TailwindCSS extension.",
  "options_ui": {
    "page": "src/pages/options/index.html"
  },
  "action": {
    "default_popup": "src/pages/popup/index.html",
    "default_icon": {
      "32": "logo.svg"
    }
  },
  "icons": {
    "128": "icon-128.png"
  },
  "background": {
    "service_worker": "src/pages/background/index.ts"
  },
  "permissions": ["storage", "activeTab", "identity", "tabs", "scripting", "cookies", "debugger"],
  "content_scripts": [
    {
      "matches": ["<all_urls>"],
      "js": ["src/pages/content/index.tsx"],
      "css": ["contentStyle.css"],
      "run_at": "document_start"
    }
  ],
  "externally_connectable": {
    "matches": ["http://localhost:3000/*"]
  },
  "devtools_page": "src/pages/devtools/index.html",
  "web_accessible_resources": [
    {
      "resources": ["contentStyle.css", "icon-128.png", "icon-32.png"],
      "matches": ["<all_urls>"]
    }
  ]
}
```

---

## 🌐 Publish to Chrome Web Store

1. Run the GitHub Action: `Build and Zip Chrome Extension`.
2. Download the artifact `vite-web-extension-chrome.zip`.
3. Upload it to [Chrome Developer Dashboard](https://chrome.google.com/webstore/devconsole/).

---

## 📘 References & Credits

- [Vite](https://vitejs.dev/)
- [@crxjs/vite-plugin](https://crxjs.dev/vite-plugin/)
- [Tailwind CSS](https://tailwindcss.com/)
- [ShadCN UI](https://ui.shadcn.dev/)
- [Chrome Extensions Docs](https://developer.chrome.com/docs/extensions/mv3/)
- [webextension-polyfill](https://github.com/mozilla/webextension-polyfill)

---
