# 💸 Stripe Funds Flow Models

Stripe provides three main **funds flow models** that determine how payments are routed between the platform and connected accounts when using [Stripe Connect](https://stripe.com/docs/connect).

These are:
- ✅ Direct Charges
- ✅ Destination Charges
- ✅ Separate Charges and Transfers

Each model offers flexibility depending on your business use case, compliance responsibility, and how you want to control payment flows.

---

## 1️⃣ Direct Charges

In this model, **connected accounts** are the _merchant of record_.

### 🔹 Characteristics:
- The **connected account** is responsible for the charge.
- The charge appears on their statement.
- The platform is **not liable** for chargebacks or disputes.
- The **connected account's Stripe key** is used to create the charge.

### 🧠 When to use:
- Your platform acts as a SaaS or provides tools, but you don’t want to be in the payment flow.
- You want the seller to own their compliance and relationship with Stripe.

### 📦 Flow:
```

Customer → Charge → Connected Account

````

### 🧾 Example:
```js
const stripe = require('stripe')('CONNECTED_ACCOUNT_SECRET');

const charge = await stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
});
````

---

## 2️⃣ Destination Charges

In this model, the **platform** creates the charge and **routes** the funds to a **connected account** as the destination.

### 🔹 Characteristics:

* The **platform** is the *merchant of record*.
* The platform handles the **customer relationship**, charge, and dispute resolution.
* The funds are **automatically transferred** to the connected account.
* Good for **marketplaces and platforms** that are aggregating sellers.

### 🧠 When to use:

* Your platform wants to handle customer support and own the full payment experience.
* You want to programmatically control who receives the funds.

### 📦 Flow:

```
Customer → Charge → Platform → Connected Account
```

### 🧾 Example:

```js
const charge = await stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
  transfer_data: {
    destination: '{{CONNECTED_ACCOUNT_ID}}',
  },
});
```

---

## 3️⃣ Separate Charges and Transfers

This model separates **charging the customer** from **transferring funds** to connected accounts.

### 🔹 Characteristics:

* The platform creates a charge and **retains the funds** initially.
* It then makes a **manual transfer** to the connected account(s).
* Allows splitting between multiple recipients (e.g., revenue shares, platform fees).
* Requires the platform to manage more logic and **handle compliance**.

### 🧠 When to use:

* You need **maximum control** over fund distribution.
* You want to **split revenue** or delay transfers.

### 📦 Flow:

```
Customer → Charge → Platform → Transfer(s) → Connected Account(s)
```

### 🧾 Example:

```js
// Create the charge (funds stay with platform initially)
const charge = await stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
});

// Later, send part to the connected account
const transfer = await stripe.transfers.create({
  amount: 1500,
  currency: 'usd',
  destination: '{{CONNECTED_ACCOUNT_ID}}',
});
```

---

## 🧮 Summary Table

| Feature                     | Direct Charges    | Destination Charges | Separate Charges & Transfers |
| --------------------------- | ----------------- | ------------------- | ---------------------------- |
| Merchant of Record          | Connected Account | Platform            | Platform                     |
| Charge Created By           | Connected Account | Platform            | Platform                     |
| Funds Automatically Routed  | ✅ Yes             | ✅ Yes               | ❌ Manual                     |
| Platform Takes Platform Fee | ❌ No              | ✅ Yes               | ✅ Yes                        |
| Platform Handles Disputes   | ❌ No              | ✅ Yes               | ✅ Yes                        |
| Multi-party Splitting       | ❌ No              | ❌ No                | ✅ Yes                        |

---

## 📚 Resources

* [Stripe Docs: Connect Charges Overview](https://stripe.com/docs/connect/charges)
* [Destination Charges](https://stripe.com/docs/connect/destination-charges)
* [Separate Charges & Transfers](https://stripe.com/docs/connect/separate-charges-and-transfers)
