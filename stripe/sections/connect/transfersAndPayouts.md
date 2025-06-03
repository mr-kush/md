# 💸 Transfers and Payouts in Stripe Connect

Stripe Connect allows platforms to move funds to connected accounts and help them access those funds via payouts.

---

## 🔁 What's the Difference?

| Concept   | Transfers | Payouts |
|-----------|-----------|---------|
| **Purpose** | Move funds from Platform → Connected Account | Move funds from Stripe balance → Bank account (or debit card) |
| **Who triggers it** | Platform | Stripe (auto or manual) |
| **Where funds go** | To connected account’s Stripe balance | To external bank/debit account |
| **API Object** | `Transfer` | `Payout` |
| **Used in** | Separate Charges & Transfers flow | After charge is settled in connected account |

---

## 1️⃣ Transfers (Platform → Connected Account)

Transfers move funds from your **platform's Stripe balance** to a **connected account's Stripe balance**.

### 📦 Use Case
- Used when using **Separate Charges and Transfers** model.
- Useful for delayed or conditional fund distribution.

### 🧾 Code Example

```js
const transfer = await stripe.transfers.create({
  amount: 1000,
  currency: 'usd',
  destination: 'acct_connectedAccountId',
});
````

### ✅ Tips:

* The `destination` is the connected account ID.
* Funds must already be in the **platform’s balance** in the correct currency.

---

## 2️⃣ Payouts (Stripe → Bank)

Payouts move funds from a **connected account's Stripe balance** to their **external bank account** or debit card.

### 📦 Use Case

* After funds are in the connected account’s balance (via charge or transfer), payouts settle the funds externally.

### 🧾 Code Example (Manual Payout)

```js
const payout = await stripe.payouts.create({
  amount: 5000,
  currency: 'usd',
}, {
  stripeAccount: 'acct_connectedAccountId',
});
```

### 🔁 Automatic Payouts

By default, Stripe automatically pays out connected accounts on a **daily, weekly, or monthly** schedule.

You can configure this using the [Dashboard](https://dashboard.stripe.com) or API:

```js
await stripe.accounts.update('acct_connectedAccountId', {
  settings: {
    payouts: {
      schedule: {
        interval: 'manual', // or 'daily', 'weekly', 'monthly'
      },
    },
  },
});
```

---

## 3️⃣ Workflow Diagram

```
+------------+         +----------------+         +---------------+
|  Customer  |  --->   |  Platform      |  --->   | Connected Acct|
|   pays     |         | (Stripe Balance)|        | (Stripe Balance)|
+------------+         +----------------+         +---------------+
                                                 |
                                                 v
                                        +--------------------+
                                        |  Payout (to bank)  |
                                        +--------------------+
```

---

## 🧮 Summary Table

| Action     | Platform Balance | Connected Account Balance | Bank Account |
| ---------- | ---------------- | ------------------------- | ------------ |
| `charge`   | ✅ Increases      | ❌                         | ❌            |
| `transfer` | ⬇️ Decreases     | ✅ Increases               | ❌            |
| `payout`   | ❌                | ⬇️ Decreases              | ✅ Appears    |

---

## 🛑 Things to Watch Out For

* Transfers **can only be made in the same currency** as the source balance.
* Payouts **require external account setup** (`external_account` or `default_for_currency`).
* Funds from a charge may be **subject to delay or reserve** before eligible for transfer or payout.
* Manual payouts **must be explicitly triggered**.

---

## 📚 Resources

* [Stripe Docs: Transfers](https://stripe.com/docs/connect/separate-charges-and-transfers#transfers)
* [Stripe Docs: Payouts](https://stripe.com/docs/connect/payouts)
* [Account Capabilities & Balances](https://stripe.com/docs/connect/balance)