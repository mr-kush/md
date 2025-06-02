# Radar & Reducing Fraud

> A concise yet detailed **revision summary** of the **"Radar & Reducing Fraud"** section for your **Stripe Associate Architect Certification**:

---

## 🛡️ Radar & Reducing Fraud — 10% of Exam

**Stripe Radar** is Stripe’s machine learning–powered fraud prevention tool, deeply integrated into its payments infrastructure. It helps you **detect, prevent, and respond** to fraudulent activity across card payments.

---

### 1. ⚠️ Types of Fraud Stripe Users May Encounter

Stripe users typically face:

| Fraud Type            | Description                                                             |
| --------------------- | ----------------------------------------------------------------------- |
| **Stolen card fraud** | Fraudster uses compromised card details to make unauthorized payments.  |
| **Card testing**      | Fraudster tests a list of card numbers by making small payments.        |
| **Friendly fraud**    | Real customer denies a valid charge, leading to disputes.               |
| **Chargeback fraud**  | Charge is challenged via the card network; funds are forcibly reversed. |

---

### 2. 🧠 How Stripe Radar Works

Radar uses **machine learning** trained on billions of global Stripe transactions to assign a **risk score** to every payment.

| Layer                   | Description                                                                |
| ----------------------- | -------------------------------------------------------------------------- |
| 🔍 **ML Risk Score**    | Evaluates transactions on features like IP, card fingerprint, device, etc. |
| 📏 **Rules Engine**     | Users can define custom logic using if/then rules.                         |
| 🛠️ **Radar for Teams** | Gives advanced controls, review queues, log exports, and more.             |

---

### 3. 🎯 Risk Evaluation in Practice

Each `PaymentIntent` or `Charge` object may include:

```json
"fraud_details": {
  "stripe_report": "fraudulent" | "safe"
}
```

You can also use:

* `risk_level` (`normal`, `elevated`, `highest`)
* `risk_score` (0–100)
* Radar dashboard filters to review flagged charges

📊 These scores help decide:

* Auto-decline
* Review queue
* Allow and monitor

---

### 4. 🧰 Key Radar Features

| Feature                     | Description                                               |
| --------------------------- | --------------------------------------------------------- |
| **Custom Rules**            | Build rule like: `risk_level = elevated → block`          |
| **Velocity checks**         | Limit attempts per card/IP/email in a time window         |
| **Blocklists / Allowlists** | Prevent or allow specific email domains, cards, countries |
| **SCA Enforcement**         | Dynamically trigger 3DS for risky payments                |
| **Radar for Fraud Teams**   | Offers more detailed event log access, metrics, and rules |
| **Review Queues**           | Hold payments for manual decisioning                      |

---

### 5. 💡 Reducing Fraud: Best Practices

| Goal                      | Best Practice                               |
| ------------------------- | ------------------------------------------- |
| Stop card testing         | Use Radar velocity rules & CAPTCHA          |
| Reduce chargebacks        | Combine Radar + 3D Secure + good descriptor |
| Handle high-risk payments | Route to manual review                      |
| Build trust               | Use clear refund policies, legit receipts   |

---

## ✅ Summary Table

| Concept         | Key Idea                                 |
| --------------- | ---------------------------------------- |
| Stripe Radar    | ML-powered fraud prevention              |
| Radar for Teams | Advanced fraud tools for large merchants |
| Risk Scores     | Evaluates how risky a payment is         |
| Custom Rules    | Define logic to block, allow, or review  |
| Common Threats  | Stolen cards, chargebacks, card testing  |

---