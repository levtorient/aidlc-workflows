---
name: payment-integration
description: Implement server-side payment integrations with common providers (Stripe, PayPal, MoMo, VNPay, ZaloPay). Use this skill when the user needs to add payment processing, handle webhooks, manage subscriptions, process refunds, or integrate any payment gateway into the backend.
---

This skill guides backend payment integration. Read `requirements.md` and the existing codebase to understand which payment providers are needed and what payment flows to support. Derive all implementation from actual requirements.

## Supported Providers

### International
- **Stripe** — Cards, wallets, subscriptions, invoicing
- **PayPal** — PayPal balance, cards, Pay Later
- **Paddle** — Software/SaaS with tax handling
- **LemonSqueezy** — Digital products with tax compliance

### Vietnam
- **MoMo** — E-wallet, QR payments
- **VNPay** — Bank transfers, QR, cards
- **ZaloPay** — E-wallet, QR payments
- **OnePay** — Cards, bank transfers

## Integration Principles

### Server-Side Only
- Never expose API keys or secrets to the frontend
- Create payment intent/session on server, return only client token or redirect URL
- All sensitive operations happen server-side

### Webhook-First Verification
- Never trust client-side payment confirmation
- Payment is only confirmed when webhook is received and verified
- Webhooks are the source of truth for payment status

### Idempotency
- Store provider's transaction ID to prevent duplicate processing
- Same webhook received twice must not create duplicate orders
- Use idempotency keys when creating payments

### Security
- Verify webhook signatures using raw request body (not parsed JSON)
- Use webhook secrets from environment variables
- Validate all amounts and currencies server-side
- Log payment events for audit trail

## Common Payment Flows

### One-Time Payment
1. Frontend requests checkout → Backend creates payment intent/session
2. Backend returns client secret or redirect URL
3. Customer completes payment on provider's UI or embedded form
4. Provider sends webhook on completion
5. Backend verifies webhook, updates order status, triggers fulfillment

### Subscription
1. Frontend requests subscription → Backend creates subscription with provider
2. Customer enters payment method
3. Provider charges immediately and sends webhook
4. Backend provisions access based on subscription status
5. Provider sends webhooks for renewals, failures, cancellations
6. Backend updates access accordingly

### Refund
1. Admin/system initiates refund → Backend calls provider's refund API
2. Provider processes refund and sends webhook
3. Backend updates order status, adjusts inventory/access if needed

## Provider-Specific Notes

### Stripe
- Use PaymentIntents for one-time, Subscriptions for recurring
- Checkout Sessions for hosted payment page
- Webhook events: `payment_intent.succeeded`, `checkout.session.completed`, `invoice.paid`
- Verify signature with `stripe.webhooks.constructEvent()`

### PayPal
- Use Orders API for one-time payments
- Subscriptions API for recurring
- Webhook events: `CHECKOUT.ORDER.APPROVED`, `PAYMENT.CAPTURE.COMPLETED`
- Verify webhook with PayPal's verification endpoint

### MoMo
- Use Payment API with `requestType` for different flows
- IPN (Instant Payment Notification) for webhook
- Verify signature using HMAC-SHA256 with secret key
- Handle both IPN callback and return URL

### VNPay
- Use Payment URL redirect flow
- IPN for webhook notification
- Verify secure hash using SHA512
- Handle return URL for user redirect

### ZaloPay
- Use Create Order API
- Callback URL for webhook
- Verify MAC using HMAC-SHA256

## Implementation Checklist

### Setup
- [ ] Store API keys/secrets in environment variables
- [ ] Configure webhook endpoint URL in provider dashboard
- [ ] Store webhook secret for signature verification
- [ ] Set up logging for payment events

### Payment Creation
- [ ] Validate order data before creating payment
- [ ] Create order record with `pending` status before calling provider
- [ ] Store provider's payment/session ID on order record
- [ ] Return only safe data to frontend (client secret, redirect URL)

### Webhook Handling
- [ ] Verify signature before processing
- [ ] Return 200 immediately (process async if needed)
- [ ] Check idempotency — skip if already processed
- [ ] Update order status based on event type
- [ ] Trigger post-payment actions (email, fulfillment, access)
- [ ] Log all webhook events

### Error Handling
- [ ] Handle payment failures gracefully
- [ ] Provide clear error messages to frontend
- [ ] Retry logic for transient failures
- [ ] Alert on repeated failures or suspicious activity

## Order Status Flow

```
pending → processing → completed → [refunded]
                   ↘ failed
```

- **pending** — Order created, payment not started
- **processing** — Payment initiated, awaiting confirmation
- **completed** — Payment confirmed via webhook
- **failed** — Payment failed or expired
- **refunded** — Full or partial refund processed

## Testing

- Use provider's test/sandbox mode for development
- Test webhook handling with provider's webhook testing tools
- Verify idempotency by replaying webhooks
- Test failure scenarios (declined cards, insufficient funds)
- Test refund flow end-to-end
