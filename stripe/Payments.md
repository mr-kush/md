# Payments 
> A **detailed yet concise revision summary** of the **"Payments" section** from the Stripe documentation 

---

## 🧾 **Stripe Payments — 20% of Exam Weight**

### ✅ **1. Analyze Business Requirements & Propose the Best Stripe Account Structures**

* **Standard Stripe Account:** Merchant fully controls Stripe integration and dashboard.
* **Connect (Platform) Setup:** Used when building a marketplace, SaaS, or platform; supports Express or Custom connected accounts.
* Choose based on:

  * Who handles onboarding?
  * Who controls payout timing?
  * Who bears chargeback/fraud liability?

---

### ✅ **2. Create a Charge**

* Use the **[Payment Intents API](https://stripe.com/docs/api/payment_intents)** for modern payments.
* A "charge" is created as part of a **PaymentIntent** flow.
* Supports SCA (Strong Customer Authentication), multiple steps (confirmation, capture).

```js
const paymentIntent = await stripe.paymentIntents.create({
  amount: 1099,
  currency: "usd",
  payment_method: "pm_card_visa",
  confirm: true,
});
```

---

### ✅ **3. Stripe Payment Element**

* Frontend UI component for collecting payments.
* Supports cards, wallets (Apple Pay), bank debits, BNPL, etc.
* Reacts dynamically to customer's location and browser.
* Easy drop-in with built-in SCA support and localization.

---

### ✅ **4. Receiving Payouts**

* **Payouts** are transfers of available balance to a user's bank account.
* Occur based on:

  * Standard payout schedule (e.g., T+2 days in U.S.)
  * Can be configured in **Custom/Express accounts**.
* Use `/v1/payouts` endpoint for manual payouts.
* Can view from **Dashboard** → **Balance** → **Payouts**.

---

### ✅ **5. Payment Intents API**

* **Recommended payment flow API** for SCA and multi-step flows.
* Manages payment lifecycle: `requires_payment_method → requires_confirmation → processing → succeeded`.
* Idempotent and supports retries.
* Integrates with **Payment Methods**, 3DS, Radar, webhooks.

---

### ✅ **6. Card Authentication & 3D Secure**

* **3D Secure (3DS):** Adds an extra step for authentication (often mandated by SCA in EU).
* Stripe automatically requests 3DS when required via PaymentIntent.
* Fallback to **3DS2** for better UX.
* Handles challenges via `payment_intent.requires_action`.

---

### ✅ **7. Working with Multiple Currencies**

* Stripe supports over **135+ currencies**.
* Merchant must configure:

  * **Currency-specific pricing**.
  * Bank accounts for receiving payouts in desired currency.
* Can auto-convert to settlement currency.
* Use `currency` field in API requests.
* Understand **presentment currency** (charged to user) vs **settlement currency** (paid to merchant).

---

### 🔁 **Key APIs and Tools in Payments**

| Feature             | API/Tool                                    |
| ------------------- | ------------------------------------------- |
| Payment lifecycle   | `PaymentIntent`, `SetupIntent`              |
| Collecting payments | Stripe.js, Elements, Payment Element        |
| Handling auth & SCA | 3DS integration, `requires_action` handling |
| Multicurrency       | `currency`, FX rates, balance dashboard     |
| Payout tracking     | `payouts`, `balance_transactions`           |

---

### ⚠️ **Best Practices**

* Always use **Payment Intents** over legacy Charges API.
* Implement **webhooks** to handle async events (e.g., `payment_intent.succeeded`, `payment_intent.payment_failed`).
* Ensure **PCI compliance** by using client-side Elements or Payment Element.
* Use **idempotency keys** in your API calls.

---
