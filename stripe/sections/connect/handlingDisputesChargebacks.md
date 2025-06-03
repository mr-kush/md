# **Handling Disputes & Chargebacks in Stripe Connect**

It includes:

* What a dispute is
* Who is responsible in different charge models
* Steps to respond to disputes
* Best practices for platforms and connected accounts
* Code examples and flow

---

## ⚖️ Handling Disputes & Chargebacks in Stripe Connect

A **dispute** (or **chargeback**) occurs when a cardholder questions a charge and contacts their card issuer. Stripe removes the funds from the account and notifies you or the connected account.

---

### 🧾 What is a Dispute?

- Issued by a **cardholder’s bank**.
- The payment is **automatically reversed** by Stripe.
- Stripe charges a **$15 dispute fee** (for standard accounts in the US).

---

### 🤝 Responsibility Depends on Charge Model

| Charge Model                    | Who is Responsible for Disputes? | Who Gets Notified? |
|--------------------------------|----------------------------------|---------------------|
| Direct Charges                 | Connected Account                | Connected Account   |
| Destination Charges            | Platform                         | Platform            |
| Separate Charges & Transfers   | Platform                         | Platform            |

> 🧠 Platforms using `destination` or `separate` models **must handle disputes themselves**.

---

### 🔁 Dispute Lifecycle

```

+------------+     +------------+     +-------------------+
\| Cardholder | --> | Issuer     | --> | Stripe             |
+------------+     +------------+     +-------------------+
|
v
+-------------------------+      +---------------------+
\| Funds Removed from      | <--  | Dispute Created     |
\| Stripe Account Balance  |      +---------------------+
+-------------------------+

````

---

### 🧑‍⚖️ Responding to Disputes

You have ~7-21 days to **submit evidence** depending on the card network.

#### ✅ Common Evidence Types:
- Proof of delivery (tracking ID)
- Signed receipts
- Customer communications
- Refund policy
- Service terms accepted by the customer

#### 📦 Example: Submitting Dispute Evidence

```js
const evidence = await stripe.disputes.update(
  'dp_123',
  {
    evidence: {
      customer_email_address: 'user@example.com',
      customer_name: 'John Doe',
      product_description: 'Monthly Subscription',
    },
  },
  {
    stripeAccount: 'acct_connectedAccountId',
  }
);
````

---

### 🛡️ Best Practices to Prevent Disputes

* Use **Radar** to detect fraud.
* Collect **explicit consent** before billing.
* Provide clear descriptors for charges.
* Use **real-time email or SMS** confirmations.
* Clearly explain **refund & cancellation policies**.

---

### 📌 Tips for Connect Platforms

* Always notify connected accounts about disputes (if you're handling them).
* Use `balance.transaction` metadata to trace the original payment.
* For **Express or Custom** accounts, use `stripeAccount` header to access/manage disputes.

---

### 📊 Webhook Monitoring

Listen to the following webhooks:

* `charge.dispute.created`
* `charge.dispute.closed`
* `charge.dispute.funds_reinstated`

> Stripe sends these to both the platform and connected account depending on the charge model.

---

### 📚 Resources

* [Disputes & Fraud](https://stripe.com/docs/disputes)
* [Disputes in Connect](https://stripe.com/docs/connect/disputes)
* [Submit Dispute Evidence](https://stripe.com/docs/api/disputes/update)
* [Handling Disputes Programmatically](https://stripe.com/docs/disputes/mechanics)