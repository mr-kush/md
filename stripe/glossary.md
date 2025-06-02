# **Stripe Glossary** 
Covering important **concepts like Radar, 3D Secure, Bank Transfers**, and more, often referenced in certifications, real-world implementations, and Stripe's architecture.

---

## 🧠 **Extended Stripe Glossary**

**Concepts, Security Terms, Payment Methods**

---

### ✅ **Radar**

> Stripe’s built-in fraud detection and prevention system.

* **Purpose:** Uses machine learning trained on billions of transactions to evaluate risk and block fraudulent charges.
* **Key Features:**

  * Risk scoring per payment (e.g., `risk_level: high`)
  * Rules engine for custom fraud logic
  * Radar for Teams = advanced tooling (blocklists, review queue, manual review)

**Example:**
A suspicious overseas card tries to pay — Stripe flags it with a high risk score and blocks the payment.

---

### 🔐 **3D Secure (3DS & 3DS2)**

> A security protocol that adds an extra layer of customer authentication during card payments.

* **Required for:** PSD2 (Europe), India, and many other regions.
* **Flows:**

  * 3DS1: Redirect to card issuer page
  * 3DS2: Embedded modal or native app challenge
* **Status:**

  * Triggered automatically if required
  * Stripe handles fallback and compliance

**Example:**
A European user sees a popup asking them to verify the transaction via OTP or their bank’s app — this is 3DS in action.

---

### 🏦 **Bank Transfer**

> A payment method where the customer sends money from their bank to a unique virtual account provided by Stripe.

* **Works With:** Japan, Europe (SEPA), Malaysia (FPX), India (Netbanking)
* **Benefits:**

  * Ideal for large transactions
  * No card fees
  * Customer initiated (push-based)

**Example:**
Your SaaS invoices a client for \$2,000 → client pays via **bank transfer** to a virtual Stripe account number. Stripe marks it as paid when funds arrive.

---

### 🌐 **Payment Methods**

> Stripe supports a wide variety of **region-specific** and **global** methods beyond just credit cards.

| Type                   | Examples                              |
| ---------------------- | ------------------------------------- |
| **Cards**              | Visa, Mastercard, AmEx                |
| **Bank Redirects**     | iDEAL (NL), Bancontact (BE), FPX (MY) |
| **Bank Debits**        | ACH, SEPA                             |
| **Wallets**            | Apple Pay, Google Pay                 |
| **Buy Now, Pay Later** | Klarna, Afterpay                      |
| **Bank Transfers**     | JP, EU, UK, India                     |
| **Vouchers**           | OXXO (MX), Boleto (BR)                |

**Example:**
A user in the Netherlands pays via **iDEAL** directly from their bank app.

---

### 🔁 **Recurring Billing**

> Charging customers repeatedly based on a schedule (e.g., monthly, annually).

* Built using:

  * **Products**
  * **Prices**
  * **Subscriptions**
  * **Invoices**
* Handles automatic retries, proration, and metered billing.

**Example:**
A \$29/month SaaS subscription using Stripe Billing automatically charges every 1st of the month.

---

### 🔐 **PCI Compliance**

> Security standard for handling card data. Stripe minimizes your burden.

* Stripe is **PCI-DSS Level 1** compliant.
* If using:

  * **Stripe Checkout / Payment Element** → PCI SAQ-A (least work)
  * **Custom form** (with Stripe.js) → PCI SAQ A-EP (more compliance work)

**Example:**
If you embed Stripe’s hosted **Checkout**, you don’t touch card data, and compliance is easy.

---

### 📬 **Webhooks**

> Server-side events sent by Stripe to your backend when something happens (e.g., `invoice.paid`, `charge.refunded`).

* **Reliable delivery** (retry on failure)
* Must **verify signature**
* Key for async flows: payments, subscriptions, Connect events

**Example:**
When an invoice is paid, Stripe sends a `POST` request to your `/webhooks/stripe` endpoint.

---

### 🪝 **Idempotency Keys**

> Prevents duplicate charges in case of retry (e.g., timeout or crash).

* Every POST (e.g., `PaymentIntent.create`) can include an `Idempotency-Key` header.
* Same key = same result (even if request is re-sent).

**Example:**
Frontend accidentally sends a charge request twice — using an idempotency key, Stripe only charges once.

---

### 🏗️ **Destination vs Separate Charges vs Direct Charges**

> Payment + fund flow strategies in **Connect**

| Model           | Charge goes to    | Fund flow control                    | Good for                     |
| --------------- | ----------------- | ------------------------------------ | ---------------------------- |
| **Destination** | Connected account | Platform triggers charge             | Marketplaces                 |
| **Separate**    | Platform account  | Manual transfer to connected account | Platforms needing hold logic |
| **Direct**      | Connected account | Connected account handles funds      | Full control to seller       |

---

### 💵 **Payout**

> Transfer of funds from a Stripe balance to an external bank account.

* **Scheduled** or **manual**
* Based on payout schedule
* Delay may apply depending on region/compliance

**Example:**
Stripe auto-pays your tutor on Fridays to their bank account.

---

### 🔄 **Proration**

> Automatically adjust billing when a subscription plan changes mid-cycle.

* E.g., upgrade from \$10 → \$20 plan on day 15
* Stripe calculates unused value and charges only the difference

**Example:**
A user upgrades their subscription mid-month → Stripe charges just \$5 more, accounting for **proration**.

---

### 🔍 **Dispute**

> A reversal request by a cardholder with their bank claiming fraud or dissatisfaction.

* Stripe deducts the funds immediately
* You can **submit evidence**
* Decision lies with the bank

**Example:**
User claims “I never authorized this” → you respond with logs, screenshots, and receipt.

---

### 🧾 **Invoice**

> Document and record of a payment attempt—especially in subscriptions.

* Contains line items, tax, customer, payment method
* Used in manual and automatic billing

---
