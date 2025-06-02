# Declines, Disputes & Refunds
 
> concise yet detailed revision summary for the **"Declines, Disputes & Refunds"** section of Stripe Docs — tailored for the **Stripe Associate Architect Certification**:

---

## 🧾 Declines, Disputes & Refunds — 10% of Exam

This section covers how Stripe handles **failed payments**, **fraud**, and **refunds/disputes**, and what best practices and tools (like Radar) you should use to reduce financial risks and improve customer trust.

---

### ❌ 1. **Understanding Declines & Failed Payments**

#### Types of Declines:

| Type                | Who Triggers It        | Examples                            |
| ------------------- | ---------------------- | ----------------------------------- |
| **Card Declines**   | Card networks / Issuer | Insufficient funds, expired card    |
| **Stripe Declines** | Stripe’s risk engine   | High-risk behavior, blocked country |

#### Response Codes:

* `card_declined`
* `insufficient_funds`
* `do_not_honor`
* `incorrect_cvc`

💡 Use the `PaymentIntent.last_payment_error` to access decline details.

---

### 📉 2. **Reducing Network Declines**

✅ **Best Practices to Minimize Declines:**

* Use **Payment Intents API** (it handles retries, authentication)
* Enable **3D Secure (3DS)** via `payment_method_options[card][request_three_d_secure]`
* Implement **automatic card retries**
* Enable **card updates** via Stripe Link or network updates
* Use **Smart Retries** (in Billing)

---

### 🛡️ 3. **Preventing Fraud with Radar**

Stripe Radar uses **machine learning** to analyze hundreds of signals and block risky transactions.

#### Key Features:

* ✅ **Dynamic 3D Secure** triggering
* ✅ **Custom Rules**: E.g., block a specific country/IP
* ✅ **Blocklists**: For emails, cards, IPs
* ✅ **Radar for Fraud Teams**: Adds advanced logic, rule simulation, and manual reviews

#### Example Custom Rule:

```sql
if :ip_country != 'US' then block
```

---

### 💸 4. **Refunds**

* Refunds can be **full** or **partial**
* Initiated via Dashboard or API:

  ```bash
  POST /v1/refunds
  ```
* Can be **automated** (e.g., cancellation flow)
* Takes 5–10 business days to reflect on card

⚠️ Stripe still charges processing fees (they’re **not returned** in most cases)

---

### ⚖️ 5. **Disputes (Chargebacks)**

#### What is a Dispute?

A **customer challenges a charge** with their bank — Stripe notifies you via:

* `charge.dispute.created` webhook

#### Actions:

* Submit **evidence** within **7 days** (receipts, proof of service, communication logs)
* Use **Dashboard** or API to respond

#### Tips to Prevent Disputes:

* Clear **descriptor** on customer statements
* Accurate product descriptions
* Refund quickly when requested
* Use 3D Secure to shift liability

---

### 🧠 Summary Table

| Topic            | Best Practice                                      |
| ---------------- | -------------------------------------------------- |
| Declines         | Use PaymentIntents + automatic retries             |
| Network Declines | Smart retries, card updater, 3D Secure             |
| Fraud            | Use Radar + Custom Rules                           |
| Refunds          | API/Dashboard; takes up to 10 days                 |
| Disputes         | Submit evidence; use 3DS; clear billing descriptor |

---