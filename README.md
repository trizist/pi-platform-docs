# Frontend Javascript SDK for pi-commerce-app

The JS SDK is the frontend SDK, designed to be used in your HTML pages or Single-Page Apps, served in the Pi Browser. This repository, `pi-commerce-app`, leverages the SDK to enable Pi-based commerce transactions.

To enable the SDK, declare your app on the Developer Portal (open `develop.pi` in the Pi Browser).

**Note:** This SDK is **not** for server-side NodeJS apps.

## Installation

Add these `script` tags to your HTML pages:

```html
<script src="https://sdk.minepi.com/pi-sdk.js"></script>
<script>Pi.init({ version: "2.0" })</script>

const scopes = ['payments'];
function onIncompletePaymentFound(payment) { /* Handle incomplete payments */ };

Pi.authenticate(scopes, onIncompletePaymentFound)
  .then(auth => console.log("Hi there! You're ready to make payments!"))
  .catch(error => console.error(error));

Pi.createPayment({
  amount: 3.14,
  memo: "Digital item purchase in pi-commerce-app",
  metadata: { itemId: 1234 }
}, {
  onReadyForServerApproval: paymentId => { /* Server approval */ },
  onReadyForServerCompletion: (paymentId, txid) => { /* Server completion */ },
  onCancel: paymentId => { /* Handle cancel */ },
  onError: (error, payment) => { /* Handle error */ }
});