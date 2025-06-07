Absolutely! Here's **Sample Paper #2** for the **Stripe Associate Architect Certification** exam – carefully designed to match the actual exam structure and scope.

---

# 📝 Stripe Associate Architect Certification – **Mock Exam #2**

**Total Questions**: 50
**Duration**: 90 minutes
**Format**: Multiple Choice (1 correct unless stated)
**Passing Score**: \~80%

---

### 🔹 **Section 1: Payments (20%)**

1. **Which Stripe object manages the lifecycle of a customer payment?**
   A) Invoice
   B) PaymentIntent
   C) PaymentMethod
   D) SetupIntent

2. **When using the Payment Element, what must be created server-side first?**
   A) Invoice
   B) PaymentMethod
   C) PaymentIntent
   D) Customer

3. **What is the role of the `confirm` method on a PaymentIntent?**
   A) Save card data
   B) Issue a refund
   C) Trigger payment collection
   D) Register a webhook

4. **What is the default status of a PaymentIntent just after creation?**
   A) `processing`
   B) `succeeded`
   C) `requires_payment_method`
   D) `requires_action`

5. **Which PaymentIntent field ensures the same operation isn’t repeated on retries?**
   A) idempotency\_key
   B) transaction\_key
   C) payment\_token
   D) correlation\_id

---

### 🔹 **Section 2: Billing (10%)**

6. **What object represents a recurring subscription in Stripe?**
   A) PaymentIntent
   B) Schedule
   C) Subscription
   D) Invoice

7. **Which of the following best supports usage-based billing?**
   A) Plan
   B) Product
   C) Metered Pricing
   D) Fixed Pricing

8. **How can Stripe help recover failed recurring payments?**
   A) Radar Rules
   B) Automatic Retries + Smart Retries
   C) API Retry Loop
   D) Mandate Rules

9. **How do you programmatically change a subscription plan?**
   A) Cancel and recreate
   B) Call the `update` endpoint with a new `price`
   C) Archive the product
   D) Migrate the customer to a new dashboard

10. **Which Stripe object helps structure complex changes like upgrades or downgrades?**
    A) BillingGroup
    B) PriceFlow
    C) Subscription Schedule
    D) Smart Invoicing

---

### 🔹 **Section 3: Connect (15%)**

11. **What’s the most hands-off account type for Connect platforms?**
    A) Standard
    B) Express
    C) Custom
    D) Direct

12. **Who handles KYC for Express accounts?**
    A) The platform
    B) Stripe
    C) Connected user
    D) Third-party compliance provider

13. **When using separate charges and transfers, which object must be created explicitly?**
    A) Transfer
    B) Charge
    C) Top-up
    D) AccountLink

14. **What type of charge makes the platform the merchant of record?**
    A) Direct Charge
    B) Separate Charge
    C) Destination Charge
    D) Platform Charge

15. **What Connect feature controls how often funds are sent to connected accounts?**
    A) Invoice Schedule
    B) Transfer Delay
    C) Payout Schedule
    D) Settlement Period

16. **Which report provides a breakdown of fees for a platform’s connected accounts?**
    A) Balance Report
    B) Connect Financial Report
    C) Issuing Statement
    D) Disbursement Log

17. **Which method supports onboarding Express accounts via web redirect?**
    A) OAuth Authorization
    B) Account Links
    C) Embedded JS SDK
    D) Dashboard Invite

18. **Which object links a platform charge to a connected account in destination charging?**
    A) ConnectedAccount
    B) Transfer
    C) Charge.destination
    D) PaymentLink

---

### 🔹 **Section 4: API Patterns (5%)**

19. **What is the role of `expand[]` in Stripe API calls?**
    A) Add query filters
    B) Limit response size
    C) Include related object details inline
    D) Trigger updates

20. **What’s the recommended way to test webhook handling locally?**
    A) Deploy to prod
    B) Use `ngrok` or Stripe CLI
    C) Log response from test webhook event
    D) Skip testing

21. **What’s the risk of not using idempotency keys on retries?**
    A) 404 errors
    B) Event delays
    C) Duplicate charges
    D) API version mismatch

22. **Where should Stripe secret keys be stored in a production system?**
    A) Frontend JavaScript
    B) Environment variables or a secrets vault
    C) Console log
    D) HTML meta tags

23. **What webhook event indicates a card payment succeeded?**
    A) `customer.created`
    B) `payment_intent.succeeded`
    C) `charge.failed`
    D) `invoice.upcoming`

---

### 🔹 **Section 5: Disputes, Declines, Refunds (10%)**

24. **How long after a charge can a customer initiate a dispute?**
    A) 1 week
    B) 30 days
    C) Varies by card network
    D) Never

25. **Which practice helps reduce fraud-related disputes?**
    A) Force card storage
    B) Use generic statement descriptors
    C) Enable 3D Secure + Radar
    D) Refund all customers by default

26. **Which object is created when a dispute occurs?**
    A) Dispute
    B) Refund
    C) DisputeIntent
    D) Violation

27. **What is one reason for a `card_declined` error?**
    A) Incorrect webhook
    B) API version conflict
    C) Card blocked by issuer
    D) Insufficient rate limit

28. **Where can a platform respond to disputes?**
    A) Through the API or Dashboard
    B) Only via webhook
    C) Email to Stripe
    D) Via card issuer

---

### 🔹 **Section 6: Reporting & Reconciliation (5%)**

29. **What Stripe object tracks every financial movement?**
    A) BalanceTransaction
    B) PaymentIntent
    C) InvoiceItem
    D) Fee

30. **Which of the following helps merchants reconcile payouts with internal accounting?**
    A) SetupIntent list
    B) Payout Reconciliation Report
    C) API Explorer
    D) Event Logs

31. **Which report should you download for fee-level details by connected account?**
    A) Issuing statement
    B) Stripe Sigma
    C) Connect Financial Report
    D) Smart Reconciliation

32. **Currency conversions are recorded in which field of a BalanceTransaction?**
    A) `converted_amount`
    B) `fx`
    C) `net`
    D) `exchange_rate`

33. **Why might a payout not match total charge amount?**
    A) API error
    B) FX fluctuation
    C) Stripe fees and refunds
    D) Insufficient retries

---

### 🔹 **Section 7: Global Business & Compliance (5%)**

34. **Which of the following is a challenge of accepting global payments?**
    A) Language support
    B) Multiple time zones
    C) Payment method preference and currency issues
    D) Stripe CLI limitations

35. **What is one way to reduce FX conversion fees when operating globally?**
    A) Use test keys
    B) Charge only in USD
    C) Use local bank accounts
    D) Disable Stripe Radar

36. **Which of the following helps Stripe handle compliance across countries?**
    A) Mandate API
    B) Global Tax Engine
    C) Know Your Customer (KYC) processes
    D) Dashboard Roles

---

### 🔹 **Section 8: Payment Methods (10%)**

37. **What payment method is popular in Germany and supported by Stripe?**
    A) iDEAL
    B) SEPA Direct Debit
    C) OXXO
    D) UPI

38. **Which Stripe feature allows hosting a secure payment page without backend coding?**
    A) Hosted Checkout
    B) Payment Links
    C) Connect Redirect
    D) PaymentIntent

39. **How can a business accept offline bank transfer payments?**
    A) SetupIntent
    B) PaymentMethod.create
    C) Using `customer_balance` or `bank_transfer` type
    D) Apple Pay

40. **What object allows placing a temporary hold on funds?**
    A) Refund
    B) SetupIntent
    C) Uncaptured Charge
    D) Transfer

41. **Which card brands support 3D Secure by default in Stripe?**
    A) Visa & Mastercard
    B) AMEX only
    C) Discover & Diners
    D) All cards from Stripe Issuing

---

### 🔹 **Section 9: Radar & Reducing Fraud (10%)**

42. **What feature lets you set custom rules in Stripe to block suspicious transactions?**
    A) Custom Auth Rules
    B) Stripe CLI
    C) Radar Rules
    D) Invoice Fraud Guard

43. **What is `risk_score` in Stripe Radar?**
    A) API speed metric
    B) Estimated chance of fraud
    C) Payout delay timer
    D) Fee prediction

44. **Which option is NOT a good fraud prevention measure?**
    A) Manual capture
    B) 3D Secure
    C) Clear billing descriptors
    D) Allow anonymous payments

45. **Radar for Fraud Teams offers which advantage?**
    A) AI-based transaction scoring
    B) More countries
    C) PCI exemption
    D) Faster payouts

---

### 🔹 **Bonus / Integrations**

46. **What type of account is used to manage Stripe API credentials?**
    A) Developer Portal
    B) API Dashboard
    C) Stripe Account
    D) Key Vault

47. **Which field in PaymentIntent can hold extra metadata?**
    A) `notes`
    B) `context`
    C) `metadata`
    D) `payment_info`

48. **What is the purpose of a SetupIntent?**
    A) Pay now
    B) Initiate subscription
    C) Save payment method for future use
    D) Set up webhooks

49. **How do you test authentication flows with 3D Secure in test mode?**
    A) Use special card numbers
    B) Enable test webhook
    C) Use live key
    D) Request real payment

50. **What Stripe product lets you build a white-label payment experience?**
    A) Checkout
    B) Connect with Custom accounts
    C) Radar
    D) Payment Links