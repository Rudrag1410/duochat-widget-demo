# @duochat/chat-widget

[![npm version](https://img.shields.io/npm/v/@duochat/chat-widget?color=2563EB&label=npm)](https://www.npmjs.com/package/@duochat/chat-widget)
[![license](https://img.shields.io/npm/l/@duochat/chat-widget)](./LICENSE)
[![bundle size](https://img.shields.io/bundlephobia/minzip/@duochat/chat-widget?color=22c55e)](https://bundlephobia.com/package/@duochat/chat-widget)
[![types](https://img.shields.io/npm/types/@duochat/chat-widget)](https://www.npmjs.com/package/@duochat/chat-widget)
[![node](https://img.shields.io/node/v/@duochat/chat-widget)](https://nodejs.org)

> 💬 Drop a full-featured live-chat messenger onto **any website** in one line of JavaScript.

No backend wiring. No iframe juggling. No CSS wars. Just one script tag — and your customers are chatting.

---

## ✨ What's inside

- 🚀 **Zero-config embed** — one `<script>` tag and you're live
- 🧩 **npm + CDN** — works with any bundler or plain HTML
- 🎨 **Fully themeable** — match your brand with fine-grained design tokens
- 🔒 **Privacy-first** — visitor PII travels via `postMessage`, never in URLs
- 📦 **Tiny SDK** — the loader is kilobytes; the full UI streams from the CDN
- 🔌 **Framework-ready** — React, Next.js, Vue, Svelte, vanilla JS — all work
- 🌗 **Dark mode support** — out of the box

---

## 📦 Installation

```bash
npm install @duochat/chat-widget
# or
yarn add @duochat/chat-widget
# or
pnpm add @duochat/chat-widget
```

---

## 🚀 Quick start

### Via npm / bundler

```ts
import Duochat from '@duochat/chat-widget';

Duochat({
  widget_id: 'YOUR_APP_ID',
  name: 'Jane Doe',
  email: 'jane@example.com',
});
```

### Via CDN script tag

Drop this before `</body>` on every page — that's all:

```html
<script src="https://cdn.jsdelivr.net/npm/@duochat/chat-widget@1.0.3/dist/sdk/index.umd.js"></script>
<script>
  Duochat({
    widget_id: 'YOUR_APP_ID',
    name: 'Jane Doe',
    email: 'jane@example.com',
  });
</script>
```

### ⚡ Async CDN (non-blocking)

Load the script without blocking page render. The stub queues your call and replays it once the SDK arrives:

```html
<script>
  window.Duochat = window.Duochat || function () {
    (window.Duochat.q = window.Duochat.q || []).push(arguments);
  };
  Duochat({ widget_id: 'YOUR_APP_ID' });
</script>
<script async src="https://cdn.jsdelivr.net/npm/@duochat/chat-widget@1.0.3/dist/sdk/index.umd.js"></script>
```

---

## 🎮 JavaScript API

```js
// 🟢 Boot the widget (or reconfigure a running one)
Duochat.boot({ widget_id: 'YOUR_APP_ID', name: 'Alice', email: 'alice@co.com' });

// 👁️ Show the launcher bubble
Duochat.show();

// 🙈 Hide launcher + messenger
Duochat.hide();

// 🔄 Update visitor identity on-the-fly — no reload
Duochat.update({ name: 'Bob', email: 'bob@co.com' });

// 💥 Tear down completely — removes all DOM nodes
Duochat.shutdown();
```

| Method | What it does |
|--------|--------------|
| `boot(config)` | Inject iframes and start the widget. Calling it twice updates config. |
| `show()` | Reveal the launcher after it was hidden. |
| `hide()` | Collapse the messenger and hide the launcher. |
| `update(partial)` | Merge new attributes without reloading anything. |
| `shutdown()` | Remove all widget DOM and reset internal state. |

---

## ⚙️ Configuration

All fields are optional except `widget_id`.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `widget_id` | `string` | **required** | Your Duochat app ID |
| `app_id` | `string` | — | Alias for `widget_id` |
| `name` | `string` | — | Visitor display name |
| `email` | `string` | — | Visitor email |
| `phone` | `string` | — | Visitor phone number |
| `user_id` | `string` | — | Your own user identifier |
| `custom_attributes` | `Record<string, string \| number \| boolean>` | — | Extra metadata on the conversation |
| `alignment` | `'left' \| 'right'` | `'right'` | Which corner the widget anchors to |
| `horizontal_padding` | `number` | `24` | Edge offset in px |
| `vertical_padding` | `number` | `24` | Bottom offset in px |
| `background_color` | `string` | `'#2563EB'` | Launcher bubble accent color (hex) |
| `appearance` | `WidgetAppearanceConfig` | — | Fine-grained theme tokens |
| `show_launcher` | `boolean` | `true` | Toggle the launcher bubble |
| `launch_directly` | `boolean` | `false` | Open the messenger immediately on boot |
| `sound_enabled` | `boolean` | `true` | Play notification sounds |
| `collect_visitor_email` | `boolean` | — | Prompt for email before first message |

---

## 🎨 Appearance theming

Make it yours — override any design token:

```ts
Duochat.boot({
  widget_id: 'YOUR_APP_ID',
  background_color: '#7C3AED',
  appearance: {
    theme_mode: 'dark',
    accent_color: '#7C3AED',
    messenger_background: '#18181b',
    messenger_text: '#f4f4f5',
    messenger_text_secondary: '#a1a1aa',
    bubble_agent_background: '#27272a',
    bubble_user_background: '#7C3AED',
    bubble_user_text: '#ffffff',
    composer_border: '#3f3f46',
    composer_background: '#27272a',
    composer_placeholder: '#71717a',
    privacy_policy_url: 'https://yoursite.com/privacy',
    privacy_policy_label: 'Privacy policy',
  },
});
```

| Token | Description |
|-------|-------------|
| `theme_mode` | `'light'` or `'dark'` |
| `accent_color` | Buttons, links, highlights |
| `messenger_background` | Panel background color |
| `messenger_text` | Primary text color |
| `messenger_text_secondary` | Timestamps and labels |
| `bubble_agent_background` | Incoming message bubble |
| `bubble_user_background` | Outgoing message bubble |
| `bubble_user_text` | Outgoing message text |
| `composer_border` | Input border color |
| `composer_background` | Input area background |
| `composer_placeholder` | Placeholder text color |
| `privacy_policy_url` | Footer link URL |
| `privacy_policy_label` | Footer link text |

---

## 📄 License

MIT © [Duochat](https://duochat.in)
