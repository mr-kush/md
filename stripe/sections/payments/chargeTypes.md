# 💳 Stripe Charges – Types, Fund Flow, and Use Cases

In Stripe, a **charge** is the final object that records the movement of funds from a customer to a merchant or platform. The way charges are created depends on your **platform structure**, **Connect account type**, and **fund flow** model.

---

## 🔑 3 Main Types of Charges in Stripe Connect

| Charge Type                      | Description                                                                      | Use When                                                             | Funds Flow                              |
| -------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------- | --------------------------------------- |
| **Direct Charges**               | Created on the connected account                                                 | Connected account owns payment                                       | Funds go directly to connected account  |
| **Destination Charges**          | Created on platform, but funds go to connected account                           | Platform controls UX & compliance                                    | Platform receives funds, then transfers |
| **Separate Charges & Transfers** | Charge is created on platform, then funds are sent to connected account manually | When you need more control over fund movement (e.g., split payments) | Two-step process: charge then transfer  |

---

## ⚙️ 1. Direct Charges

**Charge is created directly on the connected account** using their credentials.

### ✅ Use Case:

* SaaS platforms where the seller/merchant handles fulfillment, disputes, etc.
* Connected accounts handle liability and compliance.

### 🧱 Example:

```js
const charge = await stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
}, {
  stripeAccount: '{{CONNECTED_ACCOUNT_ID}}'
});
```

### ✅ Key Traits:

* Funds settle **directly to connected account**
* Platform **does not touch the money**
* **Fees**, **disputes**, and **fraud checks** are the responsibility of the **connected account**

---

## ⚙️ 2. Destination Charges

**Platform creates the charge, but funds are routed to the connected account** using the `destination` parameter.

### ✅ Use Case:

* Platform wants to own the payment experience, but **pass most funds** to the seller
* Allows platform to **collect application fees**

### 🧱 Example:

```js
const charge = await stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
  destination: {
    account: '{{CONNECTED_ACCOUNT_ID}}'
  },
  application_fee_amount: 300
});
```

### ✅ Key Traits:

* Platform owns the payment experience and relationship
* Stripe deposits **\$17.00** to connected account, retains **\$3.00** as fee
* Disputes & compliance: **Platform is liable**

---

## ⚙️ 3. Separate Charges and Transfers

**Charge is made to platform**, and later **you programmatically transfer funds** to the connected account using the `Transfers API`.

### ✅ Use Case:

* Need fine-grained control over **fund splitting**
* **Marketplaces**, **multi-vendor orders**, etc.

### 🧱 Charge:

```js
const charge = await stripe.charges.create({
  amount: 5000,
  currency: 'usd',
  source: 'tok_visa'
});
```

### 🧱 Transfer:

```js
await stripe.transfers.create({
  amount: 4000,
  currency: 'usd',
  destination: '{{CONNECTED_ACCOUNT_ID}}',
});
```

### ✅ Key Traits:

* Use `transfer_group` to tie charge & transfer
* Dispute responsibility: **Platform**
* Fully customizable fund distribution

---

## ⚙️ Which One to Use?

| Feature                          | Direct | Destination      | Separate |
| -------------------------------- | ------ | ---------------- | -------- |
| Platform collects fees           | ❌      | ✅                | ✅        |
| Platform handles disputes        | ❌      | ✅                | ✅        |
| Connected account holds payment  | ✅      | ✅ (after payout) | ❌        |
| Use with Custom/Express accounts | ✅      | ✅                | ✅        |
| Flexible payouts                 | ❌      | ⚠️ Manual        | ✅        |

---

## 📈 Other Related Charge Behaviors

### ✅ Capturing a Charge Later

For manual fulfillment flows:

```js
const intent = await stripe.paymentIntents.create({
  amount: 2000,
  currency: 'usd',
  capture_method: 'manual'
});

// Later:
await stripe.paymentIntents.capture(intent.id);
```

---

### 🔁 Refund a Charge

```js
await stripe.refunds.create({
  charge: 'ch_123456789',
  amount: 1500 // optional
});
```

---

### ⚠️ Disputes and Chargebacks

* Linked directly to the `charge.id`
* Webhook: `charge.dispute.created`
* Respond via Stripe Dashboard or API

---

## 🛠️ Charges + PaymentIntents (Modern Workflow)

Today, charges are not created directly — instead:

1. Create a `PaymentIntent`
2. Attach a `payment_method`
3. Confirm it
4. Stripe creates the charge

This provides:

* Better SCA/3DS support
* More fraud mitigation
* Global compatibility

---

## 🧾 Summary Decision Tree

```text
[Do you want to own the payment?]
           |
       Yes |-----------------------------\
           |                              \
     [Do you want instant routing?]        \
         Yes → Use Destination Charges       \
         No  → Use Separate Charge/Transfer   \
                                             \
   No → Use Direct Charges (account owns everything)
```

---

## 📌 Final Notes

* **Use PaymentIntent-based flows** unless you’re maintaining legacy code.
* **Destination charges** are great for **simple split payment logic**
* Use **Separate charges and transfers** for **marketplaces**, **multi-seller orders**, etc.
* Add **metadata** for traceability and reconciliation.
