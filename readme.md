# Nostr Chat Widget

A lightweight, client‑only Nostr chat widget that can be dropped into any website. The widget is built using **nostr-tools** and **Tailwind CSS** for styling.

---

## 🚀 Quick Start



Once the demo page is open you can immediately play with the widget:
1. **Add the public key** – see *Configuring the Public Key* section below.
2. Hit the orange button in the bottom‑right corner and start chatting!

---

## 🔑 Configuring the Public Key (npub) on the Demo Page

We added an easy‑to‑use input bar at the top‑center of the demo page that lets you quickly test the widget with any Nostr npub. The JS code reads the key from **localStorage** under the key . When you set a new npub it temporarily overwrites the hard‑coded  value in . This makes testing live chats a breeze without touching the source.

### How It Works
1. **Add the input bar** – The demo page already contains a small form (see ).
2. **Enter an npub** – Click *Set Npub* to store the value in localStorage.
3. **Reload the page** – The widget automatically loads the new key from localStorage and uses it for all DM interactions.
4. **Clear** – Delete  from localStorage or set it back to the original value to revert.

Below is a quick snippet of the relevant part of  for reference:



The source file  then checks localStorage on initialization:



You can keep the original placeholder in  for production releases. For development or demo purposes, this pattern is the recommended way.

---

## 📖 Getting Your Public Key

1. Create a Nostr identity using any Nostr client.
2. Export your public key in hex format (not npub).
3. Add it to the  field in .

**Tip:** You can convert npub to hex at [nostr.band/tools](https://nostr.band/tools).

---

## 🎨 Customization

### Styling

The widget uses Tailwind CSS utility classes. To customize colors, search for these classes in :
- Primary color:  (orange gradient)
- Change it to your brand colors.

### Mobile Behavior

On mobile devices, the chat expands to fullscreen automatically. Customize this in the CSS:


---

## 🔒 How It Works

1. **Session Creation**: Generates an in‑memory keypair stored locally for the session.
2. **Message Encryption**: All messages encrypted using NIP‑04.
3. **Relay Publishing**: Sent to multiple Nostr relays.
4. **Real‑time Updates**: Subscribes to replies from your public key.
5. **Local Storage**: Messages persist for 24 hours.

---

## 📦 Dependencies
- **[nostr-tools](https://github.com/nbd-wtf/nostr-tools)** – Nostr protocol implementation
- **[Tailwind CSS](https://tailwindcss.com/)** – Styling framework

---

## 🛠️ Development

### Local Testing



1. Open  in a browser.
2. Use the npub input bar for testing.

---

## 📱 Receiving Messages

To receive and respond to chat messages, use any Nostr client:
- **Desktop**: [Nostr.band](https://nostr.band), [Snort](https://snort.social)
- **Mobile**: [Damus](https://damus.io), [Amethyst](https://github.com/vitorpamplona/amethyst)

---

## 🔐 Security Considerations
- **Ephemeral Keys**: New keypair per session (24‑hr expiration).
- **No User Data**: No cookies or tracking.
- **E2E Encryption**: Messages encrypted before sending.
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
- **Nostr DM**: Any DM to contact the maintainer.

---

**Made with ⚡ by Loge Media**
