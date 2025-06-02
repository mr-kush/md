# Reporting & Reconciliation
> A detailed and streamlined **revision summary** of the **"Reporting & Reconciliation"** section for the **Stripe Associate Architect Certification**:

---

## 📊 Reporting & Reconciliation — 5% of Exam

This section focuses on **how Stripe helps merchants track, verify, and reconcile** their payments, fees, balances, and payouts. Understanding Stripe’s reporting tools is critical for operational accuracy, finance audits, and regulatory compliance.

---

### 🧾 1. **Financial Reports**

Stripe provides **pre-built financial reports** accessible via the **Dashboard** or API:

| Report Name                   | Purpose                                                     |
| ----------------------------- | ----------------------------------------------------------- |
| **Balance Report**            | Breakdown of charges, fees, transfers, and payouts          |
| **Payout Report**             | Shows exact funds in each payout                            |
| **Earnings Report**           | Revenue recognized from successful payments                 |
| **Monthly Financial Reports** | Designed for accounting — includes journal entries and fees |

📥 Downloaded in **CSV** or **PDF** formats; can be automated via Stripe’s **Reporting API** or **Data Pipeline** (for large merchants).

---

### 📘 2. **Report Types Reference**

Each report type has a **specific schema**. Refer to the [Stripe Report Types Documentation](https://stripe.com/docs/reports) for:

* File structure
* Field definitions (e.g., `net`, `fee`, `available_on`, `type`)
* Timing and delivery method

---

### 💰 3. **Payout Reconciliation Report**

This report helps match **Stripe activity** to your **bank deposits**.

Includes:

* Payout ID (e.g., `po_123`)
* Associated transactions (`ch_`, `refund_`, `fee_`)
* Currency breakdowns

✅ Use this to verify **daily or monthly settlements** match what you actually received in your bank account.

---

### 💵 4. **Balance Transaction Types**

Every Stripe movement (charge, refund, payout) generates a **Balance Transaction** with a `type`.

| Type       | Example ID | Description                                |
| ---------- | ---------- | ------------------------------------------ |
| `charge`   | `ch_...`   | Payment from customer                      |
| `refund`   | `re_...`   | Money returned to customer                 |
| `fee`      | `fee_...`  | Stripe’s processing fee                    |
| `payout`   | `po_...`   | Money sent to your bank                    |
| `transfer` | `tr_...`   | Platform-to-account movement (for Connect) |

🔍 Each transaction contains:

* **Net** (amount received after fees)
* **Available on** (date funds are available)
* **Source object** (linked charge, refund, etc.)

---

### 📋 5. **Required Verification Information**

For **compliance and onboarding**, Stripe requires certain documents depending on:

* **Country**
* **Business structure** (individual, LLC, corporation)
* **Volume**

Typically includes:

* Government-issued ID (passport, driver’s license)
* Legal business name and address
* Bank account verification
* Tax identification (e.g., EIN, PAN)

Stripe uses this info to satisfy **KYC (Know Your Customer)** and **AML (Anti-Money Laundering)** regulations.

---

### 💱 6. **Currency Conversions**

Stripe supports **over 135+ currencies**. You can:

* Accept payments in **customer’s currency**
* Settle in **your own currency**

**Conversion Flow:**

1. Customer pays in INR.
2. Stripe converts to USD (your settlement currency).
3. Stripe applies a **FX fee** (\~2%).

Conversion rates are available via:

* Dashboard
* API (`balance_transactions` and `charges` objects)

---

## 🧠 Summary Table

| Feature               | Key Use                                  |
| --------------------- | ---------------------------------------- |
| Financial Reports     | Monthly summaries for accounting         |
| Payout Reconciliation | Match Stripe payouts to bank deposits    |
| Balance Transactions  | Track every fee, refund, and payout      |
| Verification Info     | Satisfies KYC/AML for platform & Connect |
| Currency Conversions  | Cross-border settlement with FX tracking |

---