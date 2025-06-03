# 🛩️ jetcue-client

**jetcue-client** is the tiny embeddable widget for the **JetCue** platform.
Drop a single React component—or a one-liner `<script>`—into any site or mobile‑web view and start collecting tickets / contact requests that flow straight into your JetCue dashboard for manual or AI‑powered replies.

* **Plug‑and‑play** – one import, one `<JetCueForm id="…"/>`, done.
* **Framework‑agnostic** – ships ESM, CJS **and** a minified UMD build for vanilla JS.
* **Type‑safe** – written in TypeScript with complete `.d.ts` typings.
* **Featherweight** – < 25 kB gzip (JS only, no external CSS).

---

## Installation

```bash
# with pnpm
pnpm add jetcue-client

# or yarn
yarn add jetcue-client

# or npm
npm install jetcue-client
```

*React 18+ is a peer dependency and must already exist in the host project.*

---

## Quick start (React / Next JS)

```tsx
import { JetCueForm } from "jetcue-client";

export default function Contact() {
  return (
    <section className="max-w-md mx-auto">
      {/* form_… is generated in the JetCue dashboard */}
      <JetCueForm id="form_01HR6MZ2G1MZ4X9T4XR8F8YQZD" />
    </section>
  );
}
```

That’s it!
Submissions instantly appear in your **JetCue** Inbox under the associated Project.

### Props

| Prop        | Type         | Default                 | Description                                   |
| ----------- | ------------ | ----------------------- | --------------------------------------------- |
| `id` (req.) | string       | —                       | The ULID you copy from the JetCue dashboard.  |
| `endpoint`  | string       | `https://api.jetcue.ai` | Override for staging / self‑host.             |
| `onSuccess` | `() => void` | `undefined`             | Callback fired after a successful submission. |

---

## Quick start (no React)

1. Add the script from a CDN (unpkg here, but Skypack/jsDelivr work too):

   ```html
   <script src="https://unpkg.com/jetcue-client@0.1.0/dist/index.iife.js" crossorigin></script>
   ```

2. Render it wherever you like:

   ```html
   <div id="jetcue-contact"></div>

   <script>
     const { JetCueForm } = window.JetCueClient; // global from the UMD build
     ReactDOM.createRoot(document.getElementById("jetcue-contact")).render(
       React.createElement(JetCueForm, { id: "form_01HR6MZ2G1MZ4X9T4XR8F8YQZD" })
     );
   </script>
   ```

> Need a **non‑React** host? Wrap the UMD build in a Web Component (coming soon).

---

## Styling

The component ships with minimal inline styles so it inherits your site’s fonts & colours.
If you need stronger isolation you can:

1. Wrap it in a Shadow DOM by setting `window.JETCUE_USE_SHADOW = true` before the script;
2. Add your own classes via an upcoming `classNameMap` prop (road‑map).

---

## FAQ

* **Where do I get the `form_…` ID?**
  Create a Project in the JetCue dashboard → **Forms** → **Copy embed ID**.

* **Can I add extra fields or validation?**
  Yes – use the no‑code Form Builder in JetCue; the widget will auto‑render whatever schema you save.

* **Is it GDPR / PIPA compliant?**
  JetCue stores submissions in region‑segregated PostgreSQL clusters and supports data‑export & deletion APIs. See [https://jetcue.ai/legal](https://jetcue.ai/legal).

---

## Development / Contributing

```bash
pnpm i
pnpm --filter jetcue-client dev     # Storybook playground
pnpm --filter jetcue-client build   # tsup → dist/
```

We welcome PRs for new field types, accessibility tweaks, and bundle‑size wins 🙏

---

## License

MIT © 2025 JetCue, Inc.
