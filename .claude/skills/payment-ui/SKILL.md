---
name: payment-ui
description: Implement client-side payment UI and checkout flows. Use this skill when the user needs to build payment forms, checkout pages, pricing displays, embedded payment widgets, or any user-facing payment interface that integrates with backend payment APIs.
---

This skill guides frontend payment UI implementation. Read `requirements.md` and the backend API to understand which payment providers are integrated and what checkout flows to support. Derive all implementation from actual requirements.

## UI Components

### Pricing Display
- Clear price with currency symbol and formatting
- Original price with strikethrough if discounted
- Savings amount or percentage shown
- Package/tier comparison when multiple options exist
- Recommended/popular badge on preferred option

### Checkout Flow
- Product summary with image, name, price
- Customer information form (email, name, etc.)
- Payment method selection
- Provider's embedded payment form or redirect
- Order confirmation / success page
- Error handling with recovery options

### Payment Method Selection
- Clear icons/logos for each payment method
- Brief description of each option
- Disabled state for unavailable methods
- Remember last used method (optional)

## Provider Integration Patterns

### Stripe Elements
- Load Stripe.js from `js.stripe.com`
- Mount card element or payment element
- Handle `confirmPayment()` with client secret from backend
- Show loading state during confirmation
- Handle success redirect or error display

### PayPal Buttons
- Load PayPal SDK with client ID
- Render PayPal buttons in container
- Handle `createOrder` → call backend for order ID
- Handle `onApprove` → call backend to capture
- Handle `onError` → show error message

### Redirect-Based (MoMo, VNPay, ZaloPay)
- Call backend to create payment and get redirect URL
- Show loading/redirect message
- Redirect user to provider's payment page
- Handle return URL with success/failure state
- Poll or wait for webhook confirmation before showing success

### Hosted Checkout (Stripe Checkout, Paddle)
- Call backend to create checkout session
- Redirect to hosted checkout URL
- Handle success/cancel return URLs
- Show appropriate message on return

## UX Principles

### Trust & Security
- Show security badges and trust indicators
- Display accepted payment methods clearly
- Use HTTPS indicators in messaging
- Never ask for full card details in custom forms (use provider's secure elements)

### Loading States
- Disable submit button during processing
- Show spinner or progress indicator
- Display "Processing payment..." message
- Prevent double submission

### Error Handling
- Clear, human-readable error messages
- Specific guidance for common errors (card declined, insufficient funds)
- Retry option without re-entering all data
- Fallback to alternative payment method suggestion

### Mobile Optimization
- Large touch targets for payment buttons
- Appropriate keyboard types for inputs (numeric for card numbers)
- Wallet payment options (Apple Pay, Google Pay) when available
- Minimal form fields — only ask what's necessary

## Checkout Form Guidelines

### Required Fields
- Email (for receipt and order lookup)
- Payment method selection
- Provider-specific payment details (via their secure elements)

### Optional Fields (Only If Needed)
- Name (if fulfillment requires it)
- Phone (if SMS notification needed)
- Address (only for physical products)

### Validation
- Real-time validation as user types
- Clear error states on invalid fields
- Validate before enabling submit button
- Don't validate too aggressively (allow corrections)

## State Management

### Checkout State
```
idle → loading → ready → submitting → success | error
```

- **idle** — Initial load, fetching product data
- **loading** — Initializing payment provider SDK
- **ready** — Form ready for input
- **submitting** — Payment in progress
- **success** — Payment confirmed, show confirmation
- **error** — Payment failed, show error with retry

### Persistence
- Save cart/selection in localStorage for recovery
- Clear sensitive data on completion
- Handle page refresh during checkout gracefully

## Success & Confirmation

### Success Page
- Clear confirmation message
- Order number / reference
- Summary of what was purchased
- Next steps (download link, access instructions, email confirmation notice)
- Contact support link

### Email Confirmation
- Mention that confirmation email is sent
- Provide order lookup option if email doesn't arrive
- Show support contact for issues

## Accessibility

- All form fields have proper labels
- Error messages announced to screen readers
- Focus management during checkout flow
- Keyboard navigation through payment options
- Sufficient color contrast on buttons and text

## Testing Checklist

- [ ] Test with provider's test card numbers
- [ ] Test successful payment end-to-end
- [ ] Test declined card scenarios
- [ ] Test network failure during payment
- [ ] Test page refresh during checkout
- [ ] Test on mobile devices
- [ ] Test keyboard navigation
- [ ] Test screen reader experience
- [ ] Test loading states display correctly
- [ ] Test error messages are helpful
