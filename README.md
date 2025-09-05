# UploadGate — Glassmorphism File Uploader

A tiny, beautiful, **one-page** uploader that gives you a **direct CDN link** right after upload.
Built with plain **HTML/CSS/JS** and the **Uploadcare Widget SDK** (programmatic only — no web components).

<div align="center">

**Drag & Drop • Paste (Ctrl/Cmd+V) • Click to Select • Progress • Copy Link**

</div>

---

## ✨ Features

* 🪟 Glassmorphism UI (mobile-responsive)
* 🖱️ Drag & drop with visual feedback
* 📋 Paste from clipboard (Ctrl/Cmd + V)
* ⏳ Smooth progress bar + percentage
* 🔗 Instant **CDN URL** + **Copy** + **Open** buttons
* ♿ Keyboard accessible (Enter/Space on the dropzone)
* 🧩 Zero build step — open `index.html` and go

---

## 🗂️ Project Structure

```
uploadgate/
├─ index.html
├─ styles.css
└─ app.js
```

* **index.html** – HTML shell + SDK script tag
* **styles.css** – glass UI, responsive layout
* **app.js** – Uploadcare config, DnD + paste logic, progress, result UI

---

## 🚀 Quick Start

1. **Download / copy** the three files above into one folder.
2. Ensure this SDK tag is in your `<head>` (already present in `index.html`):

```html
<link rel="preconnect" href="https://ucarecdn.com" crossorigin />
<script src="https://ucarecdn.com/libs/widget/3.x/uploadcare.full.min.js"></script>
```

3. Open `index.html` in a modern browser (Chrome, Edge, Firefox, Safari).
4. Drop an image, paste one, or click **Choose image** → get the CDN link → **Copy**.

> ℹ️ Uses your public key from the code: `de9ed09d4ce1948a83c2`.
> Replace it in `app.js` if you have a different key.

```js
// app.js
uploadcare.configure({
  publicKey: "de9ed09d4ce1948a83c2",
  secureDelivery: true,
});
```

---

## 🧠 How it works

* Uses **Uploadcare Widget SDK** *programmatically*:

  * `uploadcare.openDialog(...)` for click-to-select
  * `uploadcare.fileFrom('object', file)` for drag & drop / paste blobs
* **No `<uc-*>` web components** are used (prevents extra buttons & conflicts).
* Progress events update the bar; on completion, we render thumbnail + CDN URL.

---

## 🧪 Usage Tips

* **Drag & drop** anywhere on the dropzone
* **Paste** images from clipboard (screenshots etc.)
* **Keyboard**: focus the dropzone → press **Enter** or **Space** to open dialog
* **Upload another** resets the flow and opens the picker again

---

## 🖼️ CDN URL Tricks (Transformations)

You can transform images on the fly by appending modifiers:

```text
https://ucarecdn.com/<FILE_UUID>/-/scale_crop/1200x630/center/
https://ucarecdn.com/<FILE_UUID>/-/format/webp/
https://ucarecdn.com/<FILE_UUID>/-/quality/smart/
https://ucarecdn.com/<FILE_UUID>/-/resize/800x/
```

Combine them:

```text
https://ucarecdn.com/<FILE_UUID>/-/resize/1200x/-/quality/smart/-/format/webp/
```

---

## 🎛️ Customization

* **Colors & blur**: tweak CSS variables in `styles.css`:

```css
:root{
  --bg1:#0b1020; --bg2:#121a2e;
  --glass:rgba(255,255,255,.08); --glass-2:rgba(255,255,255,.04);
  --border:rgba(255,255,255,.22); --text:#ecf1ff; --muted:rgba(236,241,255,.64);
  --accent:#7aa2ff; --accent-2:#a6ffda;
}
```

* **File types**: currently image-only; to allow any file, remove the `type.startsWith('image/')` checks in `app.js` and the “imagesOnly” option in `openDialog()`.

---

## 🧯 Troubleshooting

**Drag & drop doesn’t work**

* Make sure you’re **not** including any `<uc-*>` web components.
* Keep both listeners that call `e.preventDefault()` on `window` and `document` for `dragover` and `drop`.
* Some mobile browsers have limited DnD support — click or paste instead.

**An extra “Upload Files” button appears**

* That comes from `<uc-file-uploader-regular>` / Web Components. Remove all `<uc-*>` tags and related CSS/JS.

**Paste doesn’t work**

* Browser may block clipboard read; try **Ctrl/Cmd + V** on the page or use the picker.

**403 or “public key invalid”**

* Ensure your **public key** is correct and project allows client uploads.

**Mixed content**

* Serve from **HTTPS** if you embed this inside another site.

---

## 🧩 Roadmap

* [ ] Multi-file uploads with gallery preview
* [ ] Optional cropping UI before upload
* [ ] Non-image file support
* [ ] Theme switcher (light/dark variants)
* [ ] Drag-to-reorder when multi-upload is enabled

---

## 🤝 Contributing

1. Fork & clone
2. Make changes (no build step needed)
3. Open a PR — issues and ideas welcome!

---

## 📜 License

MIT © 2025 UploadGate Authors

---

## 🙏 Credits

* Created as part of **Gatekeepr**
* File storage & CDN by **Uploadcare**
* UI inspired by modern glassmorphism patterns
