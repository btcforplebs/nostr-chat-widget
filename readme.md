# Nostr Web Chat Plugin Demo

This repository contains a lightweight demo that shows how to embed a Nostr chat widget into your own website.  The goal is to let visitors start a conversation with no setup – simply paste the snippet below into your site.

## Quick‑Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/btcforplebs/nostr-web-chat-plugin.git
   ```

2. **Start the demo server** (works on macOS, Linux, Windows – Node 18+ is required)
   ```bash
   cd nostr-web-chat-plugin
   npm install
   npm run dev
   ```
   The server will start the demo at [http://localhost:4000](http://localhost:4000/demo).

   ## Website Embed (Node.js)

1. **copy chat.JS to nodeJS project** 

      /src/chat.js move to website /src folder

2. **Copy the widget snippet** – add this to the place in your HTML where you want the chat box to appear:

   ```html
   <!-- Add the chat widget node-->
        <script type="module" src="../src/chat.js"></script>

   <!-- Add chat widget container -->
         <div id="chat-widget-root"></div>
   ```


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
