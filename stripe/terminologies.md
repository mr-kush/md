# List of **Stripe terminologies** 
You'll commonly encounter—especially useful for the **Associate Architect Certification**. 

Each term includes:

* A **simple definition**
* A **realistic example** of how it’s used
* Stripe's context (where applicable: API, Dashboard, Connect, etc.)

---

## 🧠 Stripe Key Terminologies (With Examples)

---

### 1. **Platform**

> The business or application that integrates with Stripe to facilitate payments on behalf of others (e.g., a marketplace or SaaS product).

**Example:**
Your app "SkillHub" helps tutors get paid. SkillHub is the **platform** using Stripe Connect to pay tutors.

---

### 2. **Connected Account**

> A Stripe account (Express or Custom) linked to your platform to receive funds.

**Example:**
A tutor signs up on SkillHub and is created as a **connected account** using `accounts.create`.

---

### 3. **Charge**

> A successful payment made by a customer, tied to a PaymentIntent or a standalone `charge` object.

**Example:**
A student pays ₹1,000 for a tutoring session → this becomes a **charge** with `status = succeeded`.

---

### 4. **Customer**

> A Stripe object that stores reusable payment methods, billing info, and subscriptions.

**Example:**
The student is created as a **Customer** object so their card can be reused for future payments.

---

### 5. **PaymentIntent**

> The core object in Stripe’s modern payments API that tracks the entire lifecycle of a payment.

**Example:**
You create a `PaymentIntent` for ₹1,000 when a student checks out, and it tracks 3D Secure, success/failure, and final outcome.

---

### 6. **SetupIntent**

> Used to collect and save a payment method for future use (without charging now).

**Example:**
You save a parent’s card to be used later for auto-pay in the future. You use a **SetupIntent**.

---

### 7. **Payment Method**

> A card, bank account, wallet, or any supported method to make payments.

**Example:**
Visa card, UPI, Klarna, or SEPA Direct Debit—all are **payment methods**.

---

### 8. **Transfer**

> Movement of funds from your Stripe platform balance to a connected account.

**Example:**
You send ₹900 of the ₹1,000 charge to the tutor’s **connected account** via a `transfer`.

---

### 9. **Payout**

> Movement of funds from a Stripe account to an external bank account.

**Example:**
The ₹900 in the tutor’s connected account is sent to their bank—this is a **payout**.

---

### 10. **Balance**

> The pool of available funds in a Stripe account, ready for transfers, payouts, or refunds.

**Example:**
Your platform receives ₹1,000 from a student—Stripe holds this in your **balance** until you transfer it.

---

### 11. **Webhook**

> A real-time notification from Stripe to your server when an event occurs (e.g., `payment_intent.succeeded`).

**Example:**
When a student pays successfully, a **webhook** hits your API to mark the class as confirmed.

---

### 12. **Product**

> A sellable item or service. Each product can have multiple prices.

**Example:**
"Math Tutoring" is a **Product**, with prices like ₹1,000/hour or ₹5,000/month.

---

### 13. **Price**

> The recurring or one-time cost of a product. Tied to billing frequency and amount.

**Example:**
₹5,000/month for Math Tutoring is a **Price** object.

---

### 14. **Subscription**

> A recurring payment relationship between a customer and a product/price.

**Example:**
A parent subscribes to ₹5,000/month for their child’s lessons—this is a **subscription**.

---

### 15. **Invoice**

> A billing document generated for a customer, often used in subscriptions.

**Example:**
On the 1st of each month, Stripe generates an **invoice** for ₹5,000 for that parent.

---

### 16. **Checkout Session**

> A hosted Stripe page to accept payments, subscriptions, or save cards.

**Example:**
You redirect the student to a Stripe-hosted **Checkout Session** to pay ₹1,000.

---

### 17. **Payment Element**

> A customizable UI component to collect payment details securely on your website.

**Example:**
You embed the **Payment Element** into your frontend using React to support cards + UPI + wallets.

---

### 18. **Radar**

> Stripe’s fraud prevention tool that evaluates and blocks risky payments.

**Example:**
A payment from a stolen card is blocked by **Radar**, flagged as `highest_risk_level`.

---

### 19. **Dispute / Chargeback**

> A challenge from a customer claiming a charge was unauthorized or fraudulent.

**Example:**
The student says they didn’t authorize the payment—this creates a **dispute** and Stripe deducts the amount temporarily.

---

### 20. **Refund**

> Return of funds to the customer for a successful charge.

**Example:**
The tutor cancels the class, so you initiate a **refund** on the original ₹1,000 charge.

---

### 21. **Destination Charge**

> A payment where funds go directly to a connected account but are processed by the platform.

**Example:**
You charge ₹1,000 on behalf of a tutor, and the funds go directly to their Stripe **connected account** = **destination charge**.

---

### 22. **Separate Charges and Transfers**

> You accept payment into the platform account, then later **transfer** money to connected accounts manually.

**Example:**
Student pays you ₹1,000 → stays in your account → you later **transfer** ₹900 to the tutor.

---

### 23. **Direct Charges**

> The connected account accepts payments directly. You just help create it via API.

**Example:**
A tutor directly charges the student using their **connected account** credentials.

---

### 24. **Express Account**

> A type of connected account where Stripe handles onboarding, dashboard, and compliance.

**Example:**
The tutor signs up using Stripe’s onboarding link = they get an **Express account**.

---

### 25. **Custom Account**

> A fully white-labeled connected account controlled by your platform.

**Example:**
You collect all tutor info manually and create accounts via API. They never see Stripe UI = **Custom account**.

---
