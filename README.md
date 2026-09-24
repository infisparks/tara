# 💧 TARA Collegrade / Aqua Solutions — Official Storefront & Cloudflare Worker

A high-converting, mobile-first single-product e-commerce application for **Powerful Submersible Water Pump (Tara Collegrade 280W)**, backed by **Firebase Realtime Database**, **Shiprocket Logistics Auto-Push**, and **Razorpay & Cashfree Multi-Gateway Support** with a fast **Cloudflare Worker** serverless backend.

---

## ⚡ Active Configuration

- **Active Payment Gateway**: `razorpay` (Easily switchable to `cashfree` anytime)
- **Firebase Project ID**: `taraecommerce-bd665`
- **Firebase Realtime Database**: `https://taraecommerce-bd665-default-rtdb.firebaseio.com`
- **Shiprocket Account**: `tara472@gmail.com`
- **Razorpay Key ID**: `rzp_live_TftfltJkKZaBIx`

---

## 🔄 Multi-Gateway Architecture (Switching between Razorpay & Cashfree)

Both payment gateways are fully coded and preserved in the codebase. To switch gateways for different clients or environments:

### Option 1: Inside `worker.js`
Update the `PAYMENT_GATEWAY` field in `DEFAULT_CONFIG`:
```javascript
// Set to 'razorpay' or 'cashfree'
PAYMENT_GATEWAY: 'razorpay'
```

### Option 2: In Cloudflare Worker Dashboard
Set an Environment Variable:
- **Variable Name**: `PAYMENT_GATEWAY`
- **Value**: `razorpay` or `cashfree`

The frontend and backend automatically adapt and open the correct modal (Razorpay Checkout Modal or Cashfree Checkout Modal) without requiring code rewrites.

---

## 🔔 Razorpay Webhook Setup Guide

To ensure orders are automatically confirmed, saved to Firebase RTDB, and pushed to Shiprocket when a customer pays online via Razorpay:

### 1. Log in to Razorpay Dashboard
Go to [Razorpay Dashboard](https://dashboard.razorpay.com/) and navigate to **Settings (or Account & Settings)** → **Webhooks**.

### 2. Click "Add New Webhook"
Fill in the following fields:

- **Webhook URL**:
  ```
  https://<YOUR_WORKER_SUBDOMAIN>.workers.dev/api/webhooks/razorpay
  ```
  *(Replace `<YOUR_WORKER_SUBDOMAIN>` with your Cloudflare Worker URL, e.g., `https://tara.infisparks.workers.dev/api/webhooks/razorpay`)*

- **Secret**:
  ```
  rzp_tara_webhook_secret_2026
  ```
  *(Or enter your custom secret and update `RAZORPAY_WEBHOOK_SECRET` in `worker.js` / Cloudflare env)*

- **Active Events (Select these checkboxes)**:
  - `payment.captured`
  - `payment.authorized`
  - `payment.failed`
  - `order.paid`

### 3. Save Webhook
Click **Create Webhook**. Now, whenever an online payment is captured, Razorpay will automatically notify your Cloudflare Worker, confirm the order in Firebase Realtime Database, create a shipment on Shiprocket, and dispatch WhatsApp notifications!

---

## 🚚 Shiprocket Logistics Webhook Setup

In your [Shiprocket Dashboard](https://app.shiprocket.in/) under **Settings** → **API** → **Webhooks**:
- **Webhook URL**:
  ```
  https://<YOUR_WORKER_SUBDOMAIN>.workers.dev/api/webhooks/shiprocket
  ```
- **Events**: Order Status Updates, Tracking Updates (In Transit, Out For Delivery, Delivered, Cancelled).

---

## 📂 Repository Structure

```
tara/
├── index.html              # Customer storefront & responsive checkout (Razorpay + Cashfree + COD OTP)
├── admin.html              # Admin dashboard for orders, tracking, statuses, and Shiprocket sync
├── image/                  # Product image gallery
├── worker.js               # Cloudflare Worker serverless backend (APIs, RTDB REST, Gateways, Shiprocket)
├── database.rules.json     # Firebase Realtime Database security rules
└── README.md               # Setup & webhook configuration guide
```

---

## 🚀 Cloudflare Worker Deployment

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/) → **Workers & Pages**.
2. Create or select your Worker (e.g., `tara`).
3. Copy all code from [worker.js](file:///Volumes/CrucialX9/infispark_project/tara/worker.js) and paste it into the Cloudflare Worker Quick Edit editor.
4. Click **Deploy / Save and Deploy**.
