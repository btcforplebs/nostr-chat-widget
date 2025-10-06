# Nostr Chat Widget

A lightweight, client‑only Nostr chat widget that can be dropped into any website. The widget is built using **nostr-tools** and **Tailwind CSS** for styling.

---

## 🚀 Quick Start

```bash
# clone and open the demo page
git clone https://github.com/yourusername/nostr-web-chat-plugin.git
cd nostr-web-chat-plugin
open demo/index.html  # use your preferred browser
```

Once the demo page is open you can immediately play with the widget:
1. **Add the public key** – see *Configuring the Public Key* section below.
2. Hit the orange button in the bottom‑right corner and start chatting!

---

## 🔑 Configuring the Public Key (npub) on the Demo Page

We added an easy‑to‑use input bar at the top‑center of the demo page that lets you quickly test the widget with any Nostr npub. The JS code reads the key from **localStorage** under the key `cs_pubkey`. When you set a new npub it temporarily overwrites the hard‑coded `csPubkey` value in `src/chat.js`. This makes testing live chats a breeze without touching the source.

### How It Works
1. **Add the input bar** – The demo page already contains a small form (see `demo/index.html`).
2. **Enter an npub** – Click *Set Npub* to store the value in localStorage.
3. **Reload the page** – The widget automatically loads the new key from localStorage and uses it for all DM interactions.
4. **Clear** – Delete `cs_pubkey` from localStorage or set it back to the original value to revert.

Below is a quick snippet of the relevant part of `demo/index.html` for reference:

```html
<div id="npub-config" class="fixed top-4 left-1/2 transform -translate-x-1/2 z-50"
     style="background: rgba(255,255,255,0.9); padding:.5rem 1rem; border-radius:.5rem;"
>
  <input type="text" id="npub-input" placeholder="Enter your npub..." class="p-1 border rounded" style="width:220px;"/>
  <button id="set-npub" class="p-1 bg-blue-500 text-white rounded ml-2">Set Npub</button>
</div>
<script type="module">
  const setBtn = document.getElementById('set-npub');
  setBtn.addEventListener('click', () => {
    const npub = document.getElementById('npub-input').value.trim();
    if (!npub) return;
    localStorage.setItem('cs_pubkey', npub);
    alert('NPUB set! Refresh the page to use it.');
  });
</script>
```

The source file `src/chat.js` then checks localStorage on initialization:

```js
// At runtime, override the hard‑coded key if present in localStorage
const stored = localStorage.getItem('cs_pubkey');
if (stored) {
  CONFIG.csPubkey = stored;
}
```

You can keep the original placeholder in `src/chat.js` for production releases. For development or demo purposes, this pattern is the recommended way.

---

## 📖 Getting Your Public Key

1. Create a Nostr identity using any Nostr client.
2. Export your public key in hex format (not npub).
3. Add it to the `csPubkey` field in `src/chat.js`.

**Tip:** You can convert npub to hex at [nostr.band/tools](https://nostr.band/tools).

---

## 🎨 Customization

### Styling

The widget uses Tailwind CSS utility classes. To customize colors, search for these classes in `chat.js`:
- Primary color: `from-[#fdad01] to-[#ff8c00]` (orange gradient)
- Change it to your brand colors.

### Mobile Behavior

On mobile devices, the chat expands to fullscreen automatically. Customize this in the CSS:

```css
@media (max-width: 600px) {
  /* Adjust mobile styles here */
}
```

---

## 🔒 How It Works

1. **Session Creation**: Generates an in‑memory keypair stored locally for the session.
2. **Message Encryption**: All messages are encrypted using NIP‑04 (end‑to‑end encryption).
3. **Relay Publishing**: Encrypted messages are published to multiple Nostr relays.
4. **Real‑time Updates**: Subscribes to replies from your team's public key.
5. **Local Storage**: Messages persist locally for 24 hours per session.

---

## 📦 Dependencies
- **[nostr-tools](https://github.com/nbd-wtf/nostr-tools)** – Nostr protocol implementation
- **[Tailwind CSS](https://tailwindcss.com/)** – Styling framework

---

## 🛠️ Development

### Local Testing

```bash
# Clone and test the demo
git clone https://github.com/yourusername/nostr-web-chat-plugin.git
cd nostr-web-chat-plugin
open demo/index.html  # or serve with a static server
```

1. Open `demo/index.html` in a browser.
2. Use the npub input bar to test with any key.

---

## 📱 Receiving Messages

To receive and respond to chat messages, use any Nostr client:
- **Desktop**: [Nostr.band](https://nostr.band), [Snort](https://snort.social)
- **Mobile**: [Damus](https://damus.io), [Amethyst](https://github.com/vitorpamplona/amethyst)

---

## 🔐 Security Considerations

- **Ephemeral Keys**: New keypair per session (24‑hr expiration).
- **No User Data**: No cookies or tracking.
- **E2E Encryption**: Messages are encrypted before being sent.
- **Relay Privacy**: Distributed across multiple relays.

---

## 📄 License
MIT License – see [LICENSE](LICENSE).

---

## 🤝 Contributing

Pull requests welcome! Please open an issue first if you plan a large change.

---

## 💬 Support
- **Issues**: [GitHub Issues](https://github.com/yourusername/nostr-web-chat-plugin/issues)
- **Nostr DM**: Use any DM to contact the maintainer.

---

**Made with ⚡ by Loge Media**
