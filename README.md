# 🌿 AAB-E-HAYAT™ Botanical Juice — Official Storefront & Cloudflare Worker

A high-converting, mobile-first single-product e-commerce application for **AAB-E-HAYAT™ Natural Botanical Juice (500ml)** by Empire Global Herbal Science, backed by **Firebase Realtime Database** and a fast **Cloudflare Worker** serverless backend.

All environment variables and secrets are managed directly inside the **Cloudflare Dashboard**. There is **no separate `.env` file, no `package.json`, and no `wrangler.toml`** required.

---

## 📂 Repository Structure

```
aabe-hayyat/
├── index.html              # Single-product landing page (Aab-E-Hayat Botanical Juice 500ml)
├── admin.html              # Store admin management portal
├── image/                  # Product gallery images (1.png, 2.png, 3.png, 4.png)
├── worker.js               # Cloudflare Worker code (paste directly into Cloudflare)
├── DEPLOY_GUIDE.md         # Deployment & Cloudflare settings guide
├── database.rules.json     # Firebase Realtime Database security rules
└── README.md               # Project overview
```

---

## 🚀 Quick Deployment

1. **Frontend (GitHub Pages / Vercel)**: Push to GitHub and deploy statically for free.
2. **Backend (Cloudflare Worker)**: Copy `worker.js` and paste it into a Cloudflare Worker at [dash.cloudflare.com](https://dash.cloudflare.com/).
3. **Environment Variables**: Add your live `CASHFREE_APP_ID`, `CASHFREE_SECRET_KEY`, `SHIPROCKET_EMAIL`, `SHIPROCKET_PASSWORD` in Cloudflare Worker **Settings → Variables and Secrets**.
# tara
