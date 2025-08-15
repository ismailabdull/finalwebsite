# Jubayr Learning Center - Donation System

A complete donation system built with Stripe integration for Jubayr Learning Center. This system supports both one-time and monthly donations with secure payment processing.

## Features

- ✅ **One-Time Donations**: Custom amount input with validation
- ✅ **Monthly Donations**: Preset options ($20, $40, $60) + custom amount
- ✅ **Stripe Elements Integration**: Secure payment processing
- ✅ **Apple Pay & Google Pay Support**: Modern payment methods
- ✅ **Responsive Design**: Works on all devices
- ✅ **Form Validation**: Client-side and server-side validation
- ✅ **Success/Error Handling**: Clear user feedback
- ✅ **Test Mode**: Uses Stripe test keys for development

## Project Structure

```
website/
├── server.js                 # Express server with Stripe integration
├── package.json             # Node.js dependencies
├── .env                     # Environment variables (create this)
├── (donate.html removed)    # Donation functionality removed
├── css/
│   ├── style.css           # Main styles
│   └── (donation.css removed) # Donation functionality removed
├── js/
│   ├── script.js           # Main site JavaScript
│   └── donation.js         # Donation system JavaScript
└── README.md               # This file
```

## Setup Instructions

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure Stripe Keys

Create a `.env` file in the root directory:

```env
# Stripe Configuration
STRIPE_SECRET_KEY=your_stripe_secret_key_here
STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key_here

# Server Configuration
PORT=4242
NODE_ENV=development
```

**To get your Stripe test keys:**

1. Sign up for a free Stripe account at [stripe.com](https://stripe.com)
2. Go to the Stripe Dashboard
3. Navigate to Developers → API Keys
4. Copy your **Publishable key** and **Secret key** (test mode)
5. Replace the placeholder keys in the `.env` file

### 3. Update Frontend Stripe Key

In `js/donation.js`, replace the placeholder publishable key:

```javascript
const stripe = Stripe('YOUR_STRIPE_PUBLISHABLE_KEY');
```

### 4. Start the Server

```bash
# Development mode (with auto-restart)
npm run dev

# Production mode
npm start
```

The server will start on `http://localhost:4242`

### 5. Test the Donation System

1. (Donation functionality removed)
2. Test with Stripe's test card numbers:
   - **Success**: `4242 4242 4242 4242`
   - **Decline**: `4000 0000 0000 0002`
   - **Requires Authentication**: `4000 0025 0000 3155`

## API Endpoints

### POST `/create-payment-intent`

Creates a Stripe PaymentIntent for processing donations.

**Request Body:**
```json
{
  "amount": 25.00,
  "currency": "usd",
  "donationType": "one-time",
  "email": "donor@example.com"
}
```

**Response:**
```json
{
  "clientSecret": "pi_xxx_secret_xxx",
  "paymentIntentId": "pi_xxx"
}
```

### POST `/payment-success`

Handles successful payment confirmations.

**Request Body:**
```json
{
  "paymentIntentId": "pi_xxx",
  "donationType": "one-time",
  "amount": 25.00,
  "email": "donor@example.com"
}
```

## Testing

### Test Card Numbers

Use these test card numbers to simulate different scenarios:

| Card Number | Description | Result |
|-------------|-------------|---------|
| `4242 4242 4242 4242` | Visa | ✅ Success |
| `4000 0000 0000 0002` | Visa | ❌ Declined |
| `4000 0025 0000 3155` | Visa | 🔐 Requires Authentication |
| `5555 5555 5555 4444` | Mastercard | ✅ Success |
| `3782 822463 10005` | American Express | ✅ Success |

### Test CVC and Expiry

- **CVC**: Any 3 digits (e.g., `123`)
- **Expiry**: Any future date (e.g., `12/25`)

## Security Features

- ✅ **HTTPS Required**: Stripe Elements require HTTPS in production
- ✅ **Server-side Validation**: All amounts validated on server
- ✅ **Client-side Validation**: Form validation before submission
- ✅ **Secure Payment Processing**: Stripe handles all sensitive data
- ✅ **CORS Protection**: Configured for local development

## Customization

### Changing Donation Amounts

(Donation functionality removed - donate.html no longer exists)

```html
<button type="button" class="amount-option" data-amount="20">$20</button>
<button type="button" class="amount-option" data-amount="40">$40</button>
<button type="button" class="amount-option" data-amount="60">$60</button>
```

### Styling

(Donation functionality removed - donation.css no longer exists)

### Adding New Payment Methods

Stripe Elements automatically supports new payment methods. To prioritize specific methods, edit the `paymentMethodOrder` in `js/donation.js`:

```javascript
paymentElement = elements.create("payment", {
    layout: "tabs",
    paymentMethodOrder: ["card", "apple_pay", "google_pay", "link"],
});
```

## Troubleshooting

### Common Issues

1. **"Invalid API key" error**
   - Check that your Stripe keys are correct in `.env`
   - Ensure you're using test keys, not live keys

2. **"CORS error" in browser**
   - Make sure the server is running on `http://localhost:4242`
   - Check that CORS is properly configured in `server.js`

3. **Payment form not loading**
   - Check browser console for JavaScript errors
   - Verify Stripe.js is loaded correctly
   - Ensure the publishable key is correct

4. **"Amount must be at least $1.00" error**
   - Check that the amount input contains a valid number
   - Ensure the amount is being sent correctly to the server

### Debug Mode

Enable debug logging by adding this to `server.js`:

```javascript
// Add before app.listen()
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`, req.body);
  next();
});
```

## Production Deployment

For production deployment:

1. **Use Live Stripe Keys**: Replace test keys with live keys
2. **Enable HTTPS**: Stripe requires HTTPS in production
3. **Set Environment Variables**: Configure production environment
4. **Database Integration**: Add database to store donation records
5. **Email Notifications**: Implement email confirmations
6. **Analytics**: Add donation tracking and reporting

## Support

For issues or questions:

1. Check the [Stripe Documentation](https://stripe.com/docs)
2. Review the browser console for JavaScript errors
3. Check the server logs for backend errors
4. Verify all environment variables are set correctly

## License

This project is licensed under the MIT License. 