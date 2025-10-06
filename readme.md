# Nostr Chat Widget

A lightweight, privacy-focused chat widget powered by the Nostr protocol. Features end-to-end encryption, decentralized relay connections, and zero server dependencies.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Nostr](https://img.shields.io/badge/protocol-Nostr-purple.svg)

## ✨ Features

- 🔐 **End-to-End Encrypted** - Messages encrypted using NIP-04
- 🌐 **Decentralized** - Connects to multiple Nostr relays
- 🚫 **No Backend Required** - Entirely client-side
- 📱 **Mobile Responsive** - Works seamlessly on all devices
- ⚡ **Lightweight** - Minimal dependencies
- 🔑 **Ephemeral Keys** - Auto-generated session keys (24hr expiry)
- 💾 **Session Persistence** - Messages saved locally per session

## 🚀 Quick Start

### 1. Add Required Files

Include the chat widget files in your HTML:

```html
<!-- Add Tailwind CSS for styling -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Add import map for nostr-tools -->
<script type="importmap">
{
  "imports": {
    "nostr-tools": "https://esm.sh/nostr-tools@1.17.0"
  }
}
</script>

<!-- Add the chat widget -->
<script type="module" src="path/to/chat.js"></script>

<!-- Add chat widget container -->
<div id="chat-widget-root"></div>
```

### 2. Configure Your Public Key

Edit the `CONFIG` object in `chat.js`:

```javascript
const CONFIG = {
  relays: [
    'wss://relay.damus.io',
    'wss://relay.primal.net',
    'wss://nos.lol'
  ],
  csPubkey: 'YOUR_PUBLIC_KEY_HERE' // Your team's Nostr public key (hex format)
};
```

### 3. Done!

The chat widget will appear as a floating button in the bottom-right corner of your page.

## 📋 Configuration Options

| Option | Type | Description |
|--------|------|-------------|
| `relays` | Array | List of Nostr relay URLs to connect to |
| `csPubkey` | String | Your customer support team's public key (hex format) |

### Getting Your Public Key

1. Create a Nostr identity using any Nostr client
2. Export your public key in hex format (not npub)
3. Add it to the `csPubkey` field

**Tip:** You can convert npub to hex at [nostr.band/tools](https://nostr.band/tools)

## 🎨 Customization

### Styling

The widget uses Tailwind CSS utility classes. To customize colors, search for these classes in `chat.js`:

- Primary color: `from-[#fdad01] to-[#ff8c00]` (orange gradient)
- Change to your brand colors

### Mobile Behavior

On mobile devices, the chat expands to fullscreen automatically. Customize this in the CSS:

```css
@media (max-width: 600px) {
  /* Adjust mobile styles here */
}
```

## 🔒 How It Works

1. **Session Creation**: When a user opens the chat, an ephemeral keypair is generated and stored locally
2. **Message Encryption**: All messages are encrypted using NIP-04 (end-to-end encryption)
3. **Relay Publishing**: Encrypted messages are published to multiple Nostr relays
4. **Real-time Updates**: The widget subscribes to replies from your team's public key
5. **Local Storage**: Messages persist locally for 24 hours per session

## 📦 Dependencies

- [nostr-tools](https://github.com/nbd-wtf/nostr-tools) - Nostr protocol implementation
- [Tailwind CSS](https://tailwindcss.com/) - Styling framework

## 🛠️ Development

### Local Testing

1. Clone the repository
2. Open `demo/index.html` in a browser
3. Configure your public key in `chat.js`

### Browser Compatibility

- Chrome/Edge: ✅
- Firefox: ✅
- Safari: ✅
- Mobile browsers: ✅

**Note:** Requires ES6 module support

## 📱 Receiving Messages

To receive and respond to chat messages, you'll need a Nostr client:

### Recommended Clients

- **Desktop**: [Nostr.band](https://nostr.band), [Nostrudel](https://nostrudel.ninja)
- **Mobile**: [Damus (iOS)](https://damus.io), [Amethyst (Android)](https://github.com/vitorpamplona/amethyst)
- **Web**: [Snort.social](https://snort.social), [Iris.to](https://iris.to)

### Setup Instructions

1. Import your private key into a Nostr client
2. Watch for DM notifications from new chat sessions
3. Reply directly from the client - messages appear instantly in the widget

## 🔐 Security Considerations

- **Ephemeral Keys**: Each session generates a new keypair (24hr expiry)
- **No User Data**: No tracking, cookies, or personal data collection
- **E2E Encryption**: All messages encrypted before transmission
- **Relay Privacy**: Messages distributed across multiple relays

## 📄 License

MIT License - See LICENSE file for details

## 🤝 Contributing

Contributions welcome! Please feel free to submit a Pull Request.

## 💬 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/nostr-chat-widget/issues)
- **Nostr**: Contact via Nostr DM

## 🙏 Credits

Built with [Nostr](https://nostr.com) protocol and [nostr-tools](https://github.com/nbd-wtf/nostr-tools)

---

**Made with ⚡ by Loge Media**