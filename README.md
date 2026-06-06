# Byreal LP Deposit — Setup Notes

> ⚠️ **Before deploying or committing to your project, you must configure the two placeholders below.**

## 1. Backend Server URL (`byreal.html`)

**File:** `byreal.html`  
**Line:** `const BYREAL_API_URL = 'REPLACE_YOUR_VPS_SERVER_HERE';`

Replace `REPLACE_YOUR_VPS_SERVER_HERE` with your actual backend server URL.

**Examples:**
- `https://your-app.onrender.com` just an example.
- `https://your-app.railway.app` just an example. 
- `https://api.yourdomain.com` get a domain or testing area, you'll need it. use cloudflare, vercel, or some equivalent.
- `http://localhost:3000` (for local development only) use vscode live or some equiv.

```javascript
const BYREAL_API_URL = 'https://my-app.onrender.com'; 
```

---

## 2. Fee Wallet Address (`byreal.html`)

**File:** `byreal.html`  
**Line:** `const FEE_WALLET = 'INSERT_FEE_ADDRESS_HERE';`

Replace `INSERT_FEE_ADDRESS_HERE` with your Solana wallet address that will receive the 0.002 SOL platform fee per deposit. 

**Requirements:**
- Must be a valid base58 Solana address (32–44 chars)
- This wallet receives `FEE_LAMPORTS` (2,000,000 lamports = 0.002 SOL) on each deposit

```javascript
const FEE_WALLET = 'YourSolanaWalletAddressHere...';
```

---

## 3. Helius RPC URL (server environment)

**File:** `server.js`  
**Source:** Environment variable `SOLANA_RPC_URL`

This is **not hardcoded** in source — set it in your deployment environment:

```bash
# Render / Railway / VPS
SOLANA_RPC_URL=https://mainnet.helius-rpc.com/?api-key=YOUR_HELIUS_KEY
```

get a helius rpc api link. you'll need it.

**Never commit your Helius API key to GitHub.**

---

## 4. Local Development

For local development, the frontend automatically falls back to `http://localhost:3000`:

```javascript
const SERVER = (location.hostname === 'localhost' || location.hostname === '127.0.0.1')
  ? 'http://localhost:3000'
  : BYREAL_API_URL;
```

Run the server locally:
```bash
npm install
SOLANA_RPC_URL=https://mainnet.helius-rpc.com/?api-key=YOUR_KEY node server.js
```

---

## Files Overview

| File | Purpose | Secrets? |
|------|---------|----------|
| `byreal.html` | Frontend UI | **2 placeholders to fill** |
| `server.js` | Backend proxy / CLI wrapper | Uses env vars only |

---

## Security Checklist Before Pushing to GitHub

- [ ] `BYREAL_API_URL` replaced with your real server URL
- [ ] `FEE_WALLET` replaced with your real Solana address
- [ ] `SOLANA_RPC_URL` set in deployment environment (not in code)
- [ ] No API keys or private keys committed to the repo
