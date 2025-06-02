# Global Business & Compliance

> A detailed but concise **revision summary** of the **"Global Business & Compliance"** section for the **Stripe Associate Architect Certification**:

---

## 🌍 Global Business & Compliance — 5% of Exam

This section focuses on **how Stripe supports international operations**, ensures compliance with **financial regulations**, and helps platforms handle **cross-border complexities** like FX, KYC, and payment method localization.

---

### 🌐 1. **Challenges for Global Businesses**

When operating globally with Stripe, businesses face several key challenges:

| Challenge                    | Description                                                                                                      |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Currency handling**        | Customers pay in one currency, businesses may want to settle in another (requires FX and multi-currency support) |
| **Regulatory compliance**    | Local laws (e.g. PSD2 in EU) require 3D Secure, verification, tax handling (VAT, GST), etc.                      |
| **Cross-border fees**        | Higher fees may apply for international cards and FX conversions                                                 |
| **Payment method diversity** | Preferred payment methods vary by region (e.g. SEPA in EU, ACH in US, Konbini in Japan)                          |
| **Identity verification**    | KYC/AML rules differ per country; more data is required as volume increases                                      |

---

### 💱 2. **Foreign Exchange (FX) & Currency Support**

Stripe supports **over 135 currencies**. You can:

* **Charge customers in their local currency** for better conversion.
* **Settle in your own currency** (Stripe will handle the conversion).

**FX fee:** Typically \~2% is applied on top of base processing fees when currency conversion occurs.

🔹 APIs like `balance_transaction`, `charge`, and `payout` return both original and converted amounts.

---

### 🔄 3. **Cross-Border Transactions**

Cross-border payments occur when:

* The **card is issued in a different country** from the business.
* **Platform and connected accounts** are in different jurisdictions.

Risks/concerns:

* Higher decline rates.
* Need for **3D Secure (Strong Customer Authentication)**.
* Delays in **fund availability** due to AML checks.
* **Extra documentation** may be required for high-risk regions.

---

### 💳 4. **Common Regional Payment Methods**

| Region        | Common Methods                       |
| ------------- | ------------------------------------ |
| Europe        | SEPA Direct Debit, iDEAL, Bancontact |
| North America | ACH, cards                           |
| Asia          | Konbini, Alipay, WeChat Pay          |
| Latin America | OXXO, Boleto, Pix                    |

Use the **[Stripe Payment Method Guide](https://stripe.com/docs/payments/payment-methods/overview)** to determine which methods are supported **per country**.

✅ Choose **payment methods** based on customer preference, not just availability.

---

### 🛡️ 5. **Integration Security Guide**

Stripe provides a comprehensive **[Integration Security Guide](https://stripe.com/docs/security/guide)** which covers:

* **PCI compliance**: Use [Stripe Elements or Checkout](https://stripe.com/docs/payments/payment-element) to stay SAQ-A compliant.
* **Tokenization**: Never store raw card numbers; use `token` or `payment_method` objects.
* **Webhook verification**: Always validate Stripe webhook signatures.
* **Authentication (OAuth)**: Secure third-party integrations via Stripe Connect.

Best Practices:

* Use HTTPS
* Rotate API keys
* Use client and server-side validation
* Monitor suspicious activity using **Radar**

---

### 🏦 6. **Multiple Bank Accounts**

Stripe allows you to:

* Add **multiple external bank accounts** to a single Stripe account.
* Define **default payout accounts** per **currency** (e.g. USD payouts to US bank, EUR to EU bank).
* For **Connect platforms**, you can configure separate payout destinations for each **connected account**.

Key Benefits:

* Optimize **currency exchange**
* Reduce FX fees
* Meet **local compliance** (e.g. Japan may require domestic settlement)

ℹ️ Configuration via API (`external_accounts`) or Dashboard.

---

## 🧠 Summary Table

| Topic                    | Key Takeaway                                           |
| ------------------------ | ------------------------------------------------------ |
| Currency Handling        | Accept in local, settle in preferred currency with FX  |
| Regional Compliance      | Stripe adapts to local laws (e.g., SCA, KYC)           |
| Payment Method Diversity | Tailor to customer’s location and behavior             |
| Cross-border Fees        | Be aware of higher FX/processing fees                  |
| Integration Security     | Follow Stripe’s best practices to remain PCI compliant |
| Multi-Bank Setup         | Route funds based on currency or region                |

---