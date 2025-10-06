# Configuration Guide

This guide walks you through configuring the Nostr Chat Widget for your website.

## Table of Contents
- [Basic Setup](#basic-setup)
- [Getting Your Nostr Keys](#getting-your-nostr-keys)
- [Relay Configuration](#relay-configuration)
- [Customization](#customization)
- [Receiving Messages](#receiving-messages)

## Basic Setup

### Step 1: Include Dependencies

Add these to your HTML `<head>`:

```html
<!-- Tailwind CSS for styling -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Import map for nostr-tools -->
<script type="importmap">
{
  "imports": {
    "nostr-tools": "https://esm.sh/nostr-tools@1.17.0"
  }
}
</script>
```

### Step 2: Add the Widget

Before your closing `</body>` tag:

```html
<!-- Chat widget script -->
<script type="module" src="path/to/chat.js"></script>

<!-- Chat widget container -->
<div id="chat-widget-root"></div>
```

### Step 3: Configure Your Public Key

Open `chat.js` and locate the `CONFIG` object:

```javascript
const CONFIG = {
  relays: [
    'wss://relay.damus.io',
    'wss://relay.primal.net',
    'wss://nos.lol',
    'wss://relay.btcforplebs.com',
    'wss://relay.logemedia.com'
  ],
  csPubkey: 'YOUR_PUBLIC_KEY_HERE' // Replace with your hex public key
};
```

## Getting Your Nostr Keys

### Option 1: Using an Existing Nostr Client

If you already use Nostr:

1. Open your Nostr client (Damus, Amethyst, Snort, etc.)
2. Go to Settings → Keys/Security
3. Copy your **public key** (NOT your private key)
4. If it starts with `npub1`, convert it to hex format (see below)

### Option 2: Generate New Keys

For a fresh customer support identity:

1. Install a Nostr client:
   - Desktop: [Nostr.band](https://nostr.band), [Nostrudel](https://nostrudel.ninja)
   - Mobile: [Damus (iOS)](https://damus.io), [Amethyst (Android)](https://github.com/vitorpamplona/amethyst)

2. Create a new account
3. **IMPORTANT**: Securely save your private key (nsec)
4. Copy your public key for the config

### Converting npub to Hex

If your public key starts with `npub1`:

**Online Tool:**
- Visit [nostr.band/tools](https://nostr.band/tools)
- Paste your npub
- Copy the hex version

**Using JavaScript:**
```javascript
import { nip19 } from 'nostr-tools';
const hex = nip19.decode('npub1...').data;
console.log(hex);
```

## Relay Configuration

### Default Relays

The widget connects to multiple relays for reliability:

```javascript
relays: [
  'wss://relay.damus.io',      // General purpose, reliable
  'wss://relay.primal.net',    // Popular, good uptime
  'wss://nos.lol',             // Community favorite
  'wss://relay.btcforplebs.com', // Bitcoin-focused
  'wss://relay.logemedia.com'  // Custom relay
]
```

### Choosing Relays

**Good relays have:**
- High uptime (99%+)
- Good geographic distribution
- Support for kind 4 events (DMs)
- Read/write permissions

**Popular Relay Lists:**
- [nostr.watch](https://nostr.watch) - Relay monitoring
- [relay.tools](https://relay.tools) - Relay explorer

### Running Your Own Relay

For maximum control, run your own Nostr relay:

**Quick Setup:**
```bash
# Using nostr-rs-relay (Rust)
docker run -d -p 8080:8080 scsibug/nostr-rs-relay

# Using strfry (C++)
# See: https://github.com/hoytech/strfry
```

Then add to your config:
```javascript
relays: [
  'wss://your-relay.example.com',
  // ... plus backup public relays
]
```

## Customization

### Colors

The widget uses Tailwind classes. Change colors by replacing:

**Primary gradient** (orange):
```javascript
// Find in chat.js:
from-[#fdad01] to-[#ff8c00]

// Replace with your brand colors:
from-[#4F46E5] to-[#7C3AED]  // Purple
from-[#10B981] to-[#059669]  // Green
from-[#EF4444] to-[#DC2626]  // Red
```

**Connection indicator**:
```javascript
// Green dot when connected:
bg-green-400

// Change to match your theme:
bg-blue-400
bg-purple-400
```

### Position

Change the widget position in `chat.js`:

```javascript
// Bottom-right (default)
className="fixed bottom-4 right-4 sm:bottom-6 sm:right-6"

// Bottom-left
className="fixed bottom-4 left-4 sm:bottom-6 sm:left-6"

// Top-right
className="fixed top-4 right-4 sm:top-6 sm:right-6"
```

### Branding

**Team Name:**
```javascript
// Find in chat.js render function:
<div class="text-xs font-semibold text-[#fdad01] mb-1">Loge Media Team</div>

// Replace with:
<div class="text-xs font-semibold text-[#fdad01] mb-1">Your Team Name</div>
```

**Header Title:**
```javascript
<h3 class="font-bold text-base sm:text-lg">Instant Chat</h3>

// Change to:
<h3 class="font-bold text-base sm:text-lg">Need Help?</h3>
```

## Receiving Messages

### Setting Up Your Client

1. **Import Your Private Key**
   - Open your Nostr client
   - Go to Settings → Import Key
   - Paste your private key (nsec or hex)
   - **NEVER share your private key**

2. **Enable DM Notifications**
   - Settings → Notifications
   - Enable "Direct Messages"
   - Enable push notifications (mobile)

3. **Monitor for Messages**
   - New chat sessions will appear as DMs
   - Each session has a unique temporary public key
   - Reply directly - users see responses instantly

### Recommended Clients

**Desktop/Web:**
- [Nostr.band](https://nostr.band) - Comprehensive web client
- [Nostrudel](https://nostrudel.ninja) - Feature-rich
- [Snort.social](https://snort.social) - Clean interface

**Mobile:**
- [Damus (iOS)](https://damus.io) - Native iOS app
- [Amethyst (Android)](https://github.com/vitorpamplona/amethyst) - Powerful Android client

**Multi-device Tips:**
- Use the same private key across devices
- Messages sync automatically via relays
- Consider a dedicated device/account for support

## Advanced Configuration

### Session Duration

Change the 24-hour session expiry:

```javascript
// In getSessionKey() function:
if (Date.now() - session.created < 24 * 60 * 60 * 1000) {
  // Change to 48 hours:
  if (Date.now() - session.created < 48 * 60 * 60 * 1000) {
  // Change to 12 hours:
  if (Date.now() - session.created < 12 * 60 * 60 * 1000) {
```

### Multiple Support Accounts

Support multiple team members:

```javascript
const CONFIG = {
  relays: [...],
  csPubkeys: [
    'team-member-1-hex-pubkey',
    'team-member-2-hex-pubkey',
    'team-member-3-hex-pubkey'
  ]
};

// Then update subscribeToReplies():
authors: CONFIG.csPubkeys
```

### Custom Welcome Message

Add an automatic welcome message:

```javascript
// In init() function, after subscribeToReplies():
setTimeout(() => {
  addMessage('cs', 'Hi! How can we help you today?');
}, 500);
```

## Troubleshooting

### Widget Not Appearing
- Check browser console for errors
- Verify Tailwind CSS is loaded
- Ensure import map is correct
- Check `#chat-widget-root` div exists

### Messages Not Sending
- Verify relay connections in console
- Check public key is in hex format
- Ensure relays support kind 4 (DMs)
- Try different relays

### Not Receiving Replies
- Confirm correct private key in client
- Check relay overlap (client and widget)
- Verify DM notifications enabled
- Check client is connected to relays

### Mobile Issues
- Clear browser cache
- Check responsive CSS is applied
- Test on actual device, not just emulator
- Verify safe-area-inset for notched devices

## Security Best Practices

1. **Never expose private keys**
   - Only use public keys in client code
   - Store private keys securely (password manager)
   - Never commit keys to version control

2. **Use HTTPS**
   - Serve widget over secure connection
   - Some relays require wss:// (secure websockets)

3. **Rate limiting**
   - Consider implementing rate limits
   - Monitor for spam/abuse
   - Block abusive session keys if needed

4. **Session management**
   - Sessions expire automatically
   - No persistent user tracking
   - Messages stored only in localStorage

## Support

Need help? Issues? Contributions?

- **GitHub Issues**: [Report a bug](https://github.com/yourusername/nostr-chat-widget/issues)
- **Documentation**: [Full docs](https://github.com/yourusername/nostr-chat-widget)
- **Nostr**: DM us on Nostr for support