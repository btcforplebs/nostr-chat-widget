# Nostr Web Chat Plugin Demo

This repository contains a lightweight demo that shows how to embed a Nostr chat widget into your own website.  The goal is to let visitors start a conversation with no setup – simply paste the snippet below into your site.

## Quick‑Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/nostr-web-chat-plugin.git
   ```

2. **Start the demo server** (works on macOS, Linux, Windows – Node 18+ is required)
   ```bash
   cd nostr-web-chat-plugin
   npm install
   npm run dev
   ```
   The server will start at [http://localhost:5173](http://localhost:5173).

3. **Copy the widget snippet** – add this to the place in your HTML where you want the chat box to appear:

   ```html
   <div id="nostr-chat"></div>
   <script type="module" src="https://cdn.jsdelivr.net/npm/@nostrweb/chat-plugin@1.0.0/lib/index.js"></script>
   <script>
     const chat = new NostrChat({ target: '#nostr-chat', relay: 'wss://nostr.oxal.org' });
   </script>
   ```

   - `#nostr-chat` is the DOM element that will contain the widget.
   - Replace `relay` with your preferred Nostr relay if you wish.

4. **Open your page** in any browser.  The chat widget should load automatically and allow users to send/receive messages.

## How It Works

- The demo runs a lightweight Vite development server that bundles the widget.
- The widget itself is distributed via CDN in the example snippet.
- No additional build steps are required for using the widget – just drop the HTML snippet in.

## Common Issues

| Issue | Fix |
|---|---|
| Browser blocks mixed‑content (HTTP vs HTTPS) | Serve your page over HTTPS or host the widget on HTTP only while in dev. |
| Relay is unreachable | Ensure the relay URL is correct and that it supports WebSocket connections. |
| Styling conflict | The widget uses scoped CSS; if you override global styles that affect form elements, the widget may break. |

## Contributing

Feel free to open issues or pull requests.  If you add a new relay or feature, remember to update the example snippet accordingly.

## License

MIT LICENSE.  See [LICENSE](LICENSE) for details.
