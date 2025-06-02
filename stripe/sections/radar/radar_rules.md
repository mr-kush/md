# **Radar Rule Cheat Sheet** and **visual flow of how Radar handles a payment**

---

## 🎯 Radar Rule Cheat Sheet

Radar rules use a simple DSL (Domain Specific Language) to **evaluate payment attributes** and decide whether to allow, block, or review a payment.

### 📌 Basic Rule Actions

```txt
block    → Prevent the payment
allow    → Always allow the payment
review   → Flag the payment for manual review
```

### 📌 Common Rule Fields

| Field          | Description                         | Example                      |
| -------------- | ----------------------------------- | ---------------------------- |
| `amount`       | Payment amount in cents             | `amount > 10000`             |
| `currency`     | Payment currency code               | `currency:"usd"`             |
| `ip_country`   | Country of customer's IP address    | `ip_country:"NG"`            |
| `card_country` | Country of the card issuer          | `card_country:"US"`          |
| `risk_level`   | Stripe-assigned risk label          | `risk_level:"elevated"`      |
| `risk_score`   | Stripe risk score (0.0 to 1.0)      | `risk_score > 0.8`           |
| `email`        | Customer's email                    | `email:"fraud@example.com"`  |
| `email_domain` | Domain part of the email            | `email_domain:"gmail.com"`   |
| `metadata.*`   | Any metadata key set on the payment | `metadata.user_type:"guest"` |

### 📌 Rule Examples

```txt
# Block high-risk payments
block if: risk_level = "highest"

# Review payments from specific country
review if: ip_country = "RU"

# Allow staff emails
allow if: email_domain = "company.com"

# Block test cards
block if: card_country = "ZZ"

# Allow low-risk small payments
allow if: risk_score < 0.3 and amount < 2000
```

### 📌 Advanced Tips

* Use `or`, `and`, and parentheses for logic grouping.
* Use `in` for lists: `ip_country in ["CN", "RU", "NG"]`
* Wildcard match on emails: `email:"*@tempmail.com"`

---

## 🔄 Visual Flow: How Radar Handles a Payment

Here’s a simplified logical flow diagram of how **Stripe Radar processes a payment**:

```
1️⃣ Payment Attempted
       ↓
2️⃣ Stripe Applies Core Fraud Detection
       ↓
3️⃣ Radar Machine Learning Scores Payment
       ↓
4️⃣ Radar Rules Evaluated (Your Custom Rules)
       ↓
5️⃣ Decision Made:
    ├─ ✅ Allow → Payment proceeds
    ├─ 🚫 Block → Payment declined
    └─ 🕵️ Review → Payment placed in manual review queue
       ↓
6️⃣ Manual Review (if enabled)
       ↓
7️⃣ Final Action:
    ├─ Accept Payment
    └─ Cancel Payment
```

---

### 🧠 Quick Notes

* **Default rules** apply if no custom rules are set.
* Radar models are trained on global Stripe data.
* Custom rules override default behavior **only** if matched.
* **Radar for Fraud Teams** allows custom rules, block/allow lists, and manual review tools.

---
