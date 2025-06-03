# 💸 Payouts and Receiving Them – Stripe Overview

---

## 📥 What Are Payouts?

**Payouts** refer to the transfer of funds from **Stripe's balance to your external bank account** (for platforms and connected accounts).

There are **two types of recipients**:

* **Standard Stripe accounts (your own account)** – Stripe handles payouts automatically.
* **Connected accounts (via Stripe Connect)** – You control **when and how** funds are paid out.

---

## 🧠 Key Concepts

| Term                  | Description                                                           |
| --------------------- | --------------------------------------------------------------------- |
| **Balance**           | Funds held within Stripe; not yet transferred to your bank.           |
| **Available balance** | Funds ready to be paid out.                                           |
| **Pending balance**   | Funds in transit (e.g., processing period) before becoming available. |
| **Payout**            | Movement of available funds to your (or connected account's) bank.    |
| **Instant Payout**    | A faster method to send money instantly (with a fee).                 |

---

## 📤 Payout Flow (Your Own Account)

1. Customer pays via Stripe (funds go to **Stripe balance**).
2. Stripe deducts fees → funds become **available**.
3. Stripe schedules payout to your bank account (based on country, bank, and schedule).
4. You receive the payout in your bank.

🗓️ **Default payout schedule:** Daily, weekly, or monthly (customizable in Dashboard).

---

## 🧮 Example Timeline (US Card Payment)

| Step              | Date    | Notes                       |
| ----------------- | ------- | --------------------------- |
| Payment received  | Jan 1   | Appears as "pending"        |
| Becomes available | Jan 2–3 | Processing delay (1–2 days) |
| Payout initiated  | Jan 3   | Based on schedule           |
| Funds in bank     | Jan 4   | Depends on bank speed       |

---

## 📦 Payouts in **Connect Platforms**

For platforms using **Stripe Connect**, you control **how and when** funds are paid to connected accounts.

### Types of Charges Affecting Payouts

| Charge Type                    | Who Gets the Payout   | Platform Control | Notes                                  |
| ------------------------------ | --------------------- | ---------------- | -------------------------------------- |
| **Direct charges**             | Connected account     | Limited          | You don't see the funds.               |
| **Destination charges**        | Connected account     | Full control     | You receive payment and route to them. |
| **Separate charge & transfer** | You and then transfer | Full control     | Max flexibility.                       |

---

## 🧾 Triggering Payouts for Connect Accounts

You can manually or programmatically control payouts.

```ts
await stripe.payouts.create({
  amount: 10000,
  currency: 'usd',
}, {
  stripeAccount: 'acct_connected123',
});
```

Or use `automatic_payout_schedule`:

```ts
await stripe.accounts.update('acct_...', {
  settings: {
    payouts: {
      schedule: {
        interval: 'weekly',
        weekly_anchor: 'friday',
      },
    },
  },
});
```

---

## 🚀 Instant Payouts

* Available in the US and some countries.
* Works with **eligible debit cards or bank accounts**.
* Used for **Express or Custom accounts** and your own platform account.
* Faster but incurs an additional fee (e.g., **1%**).

```ts
await stripe.payouts.create({
  amount: 10000,
  currency: 'usd',
  method: 'instant',
});
```

---

## 🛑 Payout Failures – Common Causes

| Reason                    | Resolution                               |
| ------------------------- | ---------------------------------------- |
| Invalid bank account      | Ensure routing/account number is correct |
| Insufficient funds        | Ensure enough **available** balance      |
| Verification issues (KYC) | Complete identity verification           |
| Currency mismatch         | Ensure bank supports payout currency     |

---

## 📊 Reconciling Payouts

To match your bank statement with Stripe:

1. Use **Payout Reconciliation Report**.
2. Each payout links to related balance transactions.
3. Track gross and net totals + fees.

---

## 📋 Best Practices

* Use **webhooks** to track:

  * `payout.paid`
  * `payout.failed`
  * `balance.available`
* Always verify `available` balance before triggering manual payouts.
* Enable **automatic retries** for failed payouts.
* Monitor using **Dashboard → Balance → Payouts**.

---

## 🔐 Security Considerations

* Limit who can access payout settings.
* Use **Connect’s capabilities** to sandbox restricted access to balances.
* Never hardcode account numbers or keys.

---

## 🌍 Global Payout Considerations

| Factor               | Variation Example                                 |
| -------------------- | ------------------------------------------------- |
| Payout timing        | Longer in some countries (e.g., 7 days in Brazil) |
| Supported currencies | USD, EUR, GBP, INR, etc. (varies per country)     |
| Supported banks      | Some countries require local banks                |
| FX fees              | Applied when converting currencies                |

---

## 🧠 Summary

* **Payouts** move funds from Stripe balance to a bank.
* Platform accounts get payouts automatically.
* Connect accounts can receive payouts via several models.
* Always monitor available balances and webhook events.
* Use **Payout reports** for accurate reconciliation.

