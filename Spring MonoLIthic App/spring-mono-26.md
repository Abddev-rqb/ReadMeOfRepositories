# Stripe Payment Integration in Spring Boot Monolithic Architecture

## Table of Contents

- [Introduction](#introduction)
- [How Payments and Stripe Work](#how-payments-and-stripe-work)
  - [Client-Side Workflow](#client-side-workflow)
  - [Server-Side Workflow](#server-side-workflow)
- [Setting Up a Stripe Account](#setting-up-a-stripe-account)
- [Overview of the `StripePayment` Component](#overview-of-the-stripepayment-component)
- [Preparing Backend for Stripe Payment Integration](#preparing-backend-for-stripe-payment-integration)
  - [PaymentIntents with Stripe](#paymentintents-with-stripe)
  - [Setting Up API for Generating Stripe Client Secret](#setting-up-api-for-generating-stripe-client-secret)
- [Frontend Integration with React](#frontend-integration-with-react)
  - [Setting Up Stripe in React](#setting-up-stripe-in-react)
  - [Understanding Redux Integration in Stripe Payment](#understanding-redux-integration-in-stripe-payment)
  - [Creating Payment Form](#creating-payment-form)
  - [Creating Stripe Payment Flow](#creating-stripe-payment-flow)
  - [Creating Order Confirmation Page](#creating-order-confirmation-page)
- [Managing Loose Ends in Payment Flow](#managing-loose-ends-in-payment-flow)
- [Conclusion](#conclusion)

---

## Introduction
Stripe is a powerful payment processing platform that enables seamless and secure transactions in web applications. This guide provides a comprehensive overview of integrating Stripe into a Spring Boot monolithic architecture, covering both backend and frontend implementation with React.

## How Payments and Stripe Work

### Client-Side Workflow
1. The user enters payment details in the React frontend.
2. The frontend sends a request to the backend to generate a **client secret**.
3. The client secret is returned and used to confirm the payment.
4. The payment confirmation triggers order processing.

### Server-Side Workflow
1. The backend receives a payment request from the frontend.
2. A **PaymentIntent** is created using the Stripe API.
3. The **client secret** is returned to the frontend.
4. The frontend confirms the payment, and the backend validates it.

## Setting Up a Stripe Account
1. Go to [Stripe](https://stripe.com/) and sign up.
2. Retrieve API keys from the developer dashboard.
3. Configure webhook endpoints to handle events.

## Overview of the `StripePayment` Component
The `StripePayment` component in React is responsible for capturing payment details, sending payment requests, and handling the response.

## Preparing Backend for Stripe Payment Integration

### PaymentIntents with Stripe
**PaymentIntents** are used to handle various states of a payment (e.g., requires authentication, succeeded, or failed).

### Setting Up API for Generating Stripe Client Secret
```java
@RestController
@RequestMapping("/api/payment")
public class PaymentController {
    
    @Value("${stripe.secret.key}")
    private String stripeSecretKey;
    
    @PostMapping("/create-payment-intent")
    public ResponseEntity<Map<String, String>> createPaymentIntent(@RequestBody PaymentRequest request) {
        Stripe.apiKey = stripeSecretKey;
        
        try {
            PaymentIntentCreateParams params =
                PaymentIntentCreateParams.builder()
                    .setAmount(request.getAmount())
                    .setCurrency("usd")
                    .build();
            
            PaymentIntent intent = PaymentIntent.create(params);
            
            Map<String, String> response = new HashMap<>();
            response.put("clientSecret", intent.getClientSecret());
            return ResponseEntity.ok(response);
        } catch (StripeException e) {
            return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).build();
        }
    }
}
```

## Frontend Integration with React

### Setting Up Stripe in React
1. Install dependencies:
   ```sh
   npm install @stripe/react-stripe-js @stripe/stripe-js
   ```
2. Initialize Stripe in `App.js`:
   ```js
   import { Elements } from '@stripe/react-stripe-js';
   import { loadStripe } from '@stripe/stripe-js';
   
   const stripePromise = loadStripe("YOUR_PUBLISHABLE_KEY");
   
   function App() {
       return (
           <Elements stripe={stripePromise}>
               <PaymentForm />
           </Elements>
       );
   }
   ```

### Understanding Redux Integration in Stripe Payment
- Use Redux to manage payment state and update the UI dynamically based on success or failure.

### Creating Payment Form
```js
import { useStripe, useElements, CardElement } from '@stripe/react-stripe-js';

const PaymentForm = () => {
    const stripe = useStripe();
    const elements = useElements();
    
    const handleSubmit = async (event) => {
        event.preventDefault();
        
        const { paymentIntent, error } = await stripe.confirmCardPayment(clientSecret, {
            payment_method: { card: elements.getElement(CardElement) }
        });
        
        if (error) console.log(error);
        else console.log("Payment successful: ", paymentIntent);
    };
    
    return (
        <form onSubmit={handleSubmit}>
            <CardElement />
            <button type="submit">Pay</button>
        </form>
    );
};
```

### Creating Stripe Payment Flow
1. Capture payment details in the frontend.
2. Process the payment using Stripe.
3. Update order status in the backend.

### Creating Order Confirmation Page
After a successful payment, navigate to an order confirmation page displaying transaction details.

## Managing Loose Ends in Payment Flow
- Handle errors gracefully.
- Implement retry logic for failed payments.
- Secure API endpoints.

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)