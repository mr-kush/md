
# 📑 Reporting & Platform Responsibilities in Stripe Connect

As a Stripe Connect platform, you have legal and financial obligations depending on your account type (Standard, Express, Custom). These include **compliance with KYC regulations**, **handling tax forms**, and **financial reporting** for connected accounts.

---

## 🧾 1. Reporting Responsibilities

### 🔸 Financial Reporting

- Platforms can access balance, transfer, and payout information using:
  - `Balance Transactions API`
  - `Reports API`
  - Stripe Dashboard (for internal reporting)

### 📊 Reports Available:

| Report Type                      | Description |
|----------------------------------|-------------|
| **Balance Report**               | Shows all balance-affecting activity |
| **Payout Reconciliation Report** | Matches payouts to related charges, fees |
| **Itemized Financial Reports**   | Breaks down charges, fees, refunds, disputes |

> Download these in the **Dashboard** → **Reports** → **Financial reports** or use [Stripe Reporting API](https://stripe.com/docs/reporting/statements/api).

---

## 🔍 2. KYC (Know Your Customer) & Verification

### ✅ Platform Responsibilities Vary by Account Type:

| Account Type | Who Handles KYC? | Who Owns Customer Relationship? |
|--------------|------------------|-------------------------------|
| Standard     | Stripe           | Connected Account            |
| Express      | Stripe           | Platform (shared)            |
| Custom       | Platform         | Platform                     |

### 🔐 For Express & Custom:
You must collect:
- Business information
- Individual info (e.g., DOB, SSN last 4)
- Bank account details
- Accept Stripe TOS & Privacy Policy

> Stripe enforces these requirements through the `account.requirements` object.

---

## 🛂 3. Platform Compliance Obligations

### 🏛 Key Areas of Responsibility

- **KYC / AML**: Required info for all connected accounts (individual or business)
- **OFAC/Sanctions Checks**: Stripe runs them automatically
- **PCI Compliance**: Stripe helps platforms maintain PCI-DSS using Elements or Checkout
- **TOS Acceptance**: You must present and capture acceptance of Stripe’s TOS on onboarding

---

## 🧾 4. Tax Reporting (1099/Other)

- **For U.S.-based platforms**, Stripe will generate and file **1099-K or 1099-NEC** forms **if thresholds are met**:
  - $600 or more in payouts
- Stripe handles delivery (postal or e-delivery) and IRS submission.
- You can export/download forms via the **Tax Reporting tab** in Stripe.

---

## 📦 Stripe Reports API (Programmatic Access)

```bash
GET /v1/reporting/report_runs
````

Use for:

* Scheduled reports
* Generating downloadable links for finance

```js
const report = await stripe.reporting.reportRuns.create({
  report_type: 'balance.summary.1',
  parameters: {
    interval_start: 1680326400,
    interval_end: 1682918400,
  },
});
```

---

## 🧠 Best Practices for Platforms

* ✅ Track onboarding progress via webhooks (`account.updated`)
* ✅ Automate compliance using `requirements.currently_due` & `future_requirements`
* ✅ Provide connected accounts access to their financial data
* ✅ Configure your own reconciliation reports for payouts, transfers, and disputes
* ✅ Monitor failed verification attempts regularly

---

## 📚 Resources

* [Connect Platform Guide](https://stripe.com/docs/connect)
* [KYC Requirements](https://stripe.com/docs/connect/identity-verification)
* [Financial Reporting](https://stripe.com/docs/reports)
* [Tax Reporting in Stripe](https://stripe.com/docs/connect/tax-reporting)
