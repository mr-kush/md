# 📝 Stripe Associate Architect Certification – Mock Exam

**Total Questions**: 50
**Duration**: 90 minutes
**Passing Score**: \~80%
**Instructions**: Each question has one correct answer unless stated otherwise.

---

### **Section 1: Payments (20%)**

1. **What is the primary use of the Payment Intents API?**
   A) Generate customer tokens
   B) Manage payouts
   C) Track and handle full payment lifecycle
   D) Manage subscriptions

2. **Which Stripe product simplifies embedding a pre-built checkout UI for cards, wallets, and more?**
   A) Elements
   B) Checkout
   C) Payment Element
   D) Radar

3. **What must be done after a successful PaymentIntent requires 3D Secure authentication?**
   A) Restart the payment
   B) Call the `confirm` method
   C) Redirect the user to the Stripe Dashboard
   D) Retry with another card

4. **What does a charge represent in Stripe?**
   A) A refund
   B) A customer
   C) An attempt to move money from a customer’s payment method
   D) A transfer between two bank accounts

5. **When working with multiple currencies, which object helps determine the right currency to use at checkout?**
   A) ExchangeObject
   B) CurrencyAPI
   C) PaymentIntent
   D) Prices

---

### **Section 2: Billing (10%)**

6. **Which object is central to recurring billing in Stripe?**
   A) Invoice
   B) Subscription
   C) PaymentIntent
   D) Mandate

7. **Which of the following best describes a metered billing model?**
   A) Fixed recurring charges
   B) Customers are billed based on usage
   C) Pay only for setup
   D) Monthly discount-based pricing

8. **What Stripe feature allows modifying billing cycle mid-subscription?**
   A) Webhooks
   B) Invoices
   C) Subscription Schedules
   D) Price IDs

9. **Which of the following helps reduce failed payments in recurring billing?**
   A) Retry rules & Smart Retries
   B) Chargeback rules
   C) Radar rules
   D) Mandate rules

10. **What’s a key step when migrating from manual invoicing to Stripe Billing?**
    A) Cancel all existing subscriptions
    B) Import customers and pricing into Stripe
    C) Rebuild entire backend
    D) Switch to Custom accounts

---

### **Section 3: Connect (15%)**

11. **Which Stripe account type offers the highest platform control?**
    A) Standard
    B) Express
    C) Custom
    D) OAuth

12. **In a platform using direct charges, who is the merchant of record?**
    A) Platform
    B) Connected Account
    C) Stripe
    D) The customer

13. **What is the purpose of a destination charge?**
    A) Charge the platform
    B) Send charge funds to a connected account
    C) Send payout to cardholder
    D) Redirect funds to Radar

14. **When would you use `separate charges and transfers`?**
    A) To simplify reconciliation
    B) To delay fund routing decisions
    C) When needing instant payouts
    D) With bank transfers only

15. **Which Connect account type provides a lightweight dashboard with tax info and payouts?**
    A) Custom
    B) Express
    C) Standard
    D) Direct

16. **What object tracks funds movement in Stripe Connect?**
    A) Invoice
    B) Charge
    C) Transfer
    D) BankTransaction

17. **What information is required when onboarding Express accounts?**
    A) Full KYC
    B) Social media login
    C) Name, Email, Bank Account
    D) Tax filings

18. **How does a platform handle chargebacks in Connect with direct charges?**
    A) Stripe pays
    B) Platform pays
    C) Connected account handles it
    D) Refunded automatically

---

### **Section 4: API Patterns (5%)**

19. **What does idempotency help prevent in API requests?**
    A) Rate limiting
    B) Duplicate charges
    C) Payment failures
    D) Incorrect authentication

20. **Which header must be used for idempotent requests?**
    A) `Authorization`
    B) `X-Retry`
    C) `Idempotency-Key`
    D) `Retry-Token`

21. **When should you expand nested objects in the API response?**
    A) To save bandwidth
    B) To reduce errors
    C) To access related object details in one call
    D) To throttle request size

22. **What is the purpose of webhooks in Stripe?**
    A) To create customers
    B) To notify your system of asynchronous events
    C) To generate payments
    D) To handle subscriptions

23. **Which key type should never be exposed on the frontend?**
    A) Publishable
    B) Test
    C) Secret
    D) OAuth Token

---

### **Section 5: Disputes, Declines & Refunds (10%)**

24. **Which is a common cause of a card decline?**
    A) Radar block
    B) Issuer rules
    C) API misuse
    D) Test mode usage

25. **What tool helps manage fraud risk in Stripe?**
    A) Radar
    B) Billing
    C) Webhooks
    D) Connect

26. **What’s the first step in the dispute process?**
    A) Stripe refunds money
    B) Issuing bank files a chargeback
    C) Platform notifies merchant
    D) API responds with 402

27. **Which of the following helps reduce disputes?**
    A) Better invoices
    B) Issuing bank contact
    C) Radar rules, clear descriptors, and customer communication
    D) Smart retries

28. **What object is used to refund a charge?**
    A) RefundIntent
    B) CreditNote
    C) Refund
    D) Dispute

---

### **Section 6: Reporting & Reconciliation (5%)**

29. **Which report provides line-item level payout details?**
    A) Balance report
    B) Reconciliation report
    C) Payment report
    D) Monthly summary

30. **What object shows a financial transaction affecting the Stripe balance?**
    A) Charge
    B) Refund
    C) Balance Transaction
    D) Invoice

31. **When reconciling payouts, what’s the first step?**
    A) Call refund endpoint
    B) Download payout reconciliation report
    C) Sync your database
    D) Create a new PaymentIntent

32. **What field is used to match a payout to its transactions?**
    A) ID
    B) Transaction code
    C) Balance transaction ID
    D) Reconciliation tag

33. **What info does Stripe collect to verify accounts for payouts?**
    A) GitHub profile
    B) Business URL
    C) Tax IDs and Government ID
    D) Customer support number

---

### **Section 7: Global Business & Compliance (5%)**

34. **What is a primary challenge of global payment acceptance?**
    A) OAuth limits
    B) Different authentication methods and currencies
    C) Expired API keys
    D) Checkout load time

35. **Which method helps Stripe handle FX for cross-border transactions?**
    A) ExchangeRateObject
    B) FX Handler
    C) Real-time currency conversion
    D) PaymentIntent.currency

36. **What’s a benefit of adding multiple bank accounts per region?**
    A) Easier UI
    B) Regulatory reporting
    C) Reduce FX conversion fees
    D) Duplicate payments

---

### **Section 8: Payment Methods (10%)**

37. **Which of these is not a commonly supported payment method in Europe via Stripe?**
    A) SEPA Debit
    B) iDEAL
    C) UPI
    D) Bancontact

38. **What Stripe tool can generate a hosted link to accept payments?**
    A) Checkout
    B) Payment Link
    C) Billing Portal
    D) Stripe JS

39. **What’s a benefit of bank transfer payment methods?**
    A) Instant settlement
    B) Lower fraud risk
    C) Card reward points
    D) Faster refunds

40. **Which Stripe product can hold funds before capturing?**
    A) SetupIntent
    B) Transfer
    C) Authorization Hold
    D) Chargeback object

41. **What object is used to create a Payment Link?**
    A) Session
    B) Link
    C) PaymentIntent
    D) Product

---

### **Section 9: Radar & Fraud (10%)**

42. **Which Stripe product helps evaluate payment risk in real time?**
    A) Elements
    B) Radar
    C) Checkout
    D) Link

43. **What feature allows platforms to add custom logic to Radar rules?**
    A) Radar Extensions
    B) Radar for Fraud Teams
    C) Fraud Guard
    D) Logic Builder

44. **What is a `risk_level` returned by Stripe?**
    A) A 3DS version
    B) A fraud score for a transaction
    C) API performance stat
    D) Card CVV status

45. **Which is a best practice for minimizing fraud?**
    A) Allow all payments
    B) Retry failed transactions aggressively
    C) Enable 3D Secure, use Radar, and validate customer info
    D) Use manual payments only

---

### **Bonus Questions**

46. **What event should be listened to for successful subscription payments?**
    A) `invoice.payment_succeeded`
    B) `payment_intent.created`
    C) `subscription.created`
    D) `payment_intent.failed`

47. **Which payment method mandates SCA (Strong Customer Authentication) in EU?**
    A) Credit Card (without 3DS)
    B) SEPA
    C) iDEAL
    D) Card with 3D Secure

48. **How are chargebacks handled on direct charges?**
    A) Platform pays the fee
    B) Connected account bears the responsibility
    C) Stripe absorbs the loss
    D) Customer pays it

49. **Which Stripe feature helps automate upgrades and downgrades of subscriptions?**
    A) Coupons
    B) Subscription Schedule
    C) Mandates
    D) Transfers

50. **Which object allows storing a payment method for future use?**
    A) SetupIntent
    B) Authorization
    C) Balance
    D) Refund
