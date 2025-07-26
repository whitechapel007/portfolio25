# EmailJS Setup Guide

## Step 1: Create EmailJS Account

1. Go to [https://www.emailjs.com/](https://www.emailjs.com/)
2. Click "Sign Up" and create a free account
3. Verify your email address

## Step 2: Create Email Service

1. In your EmailJS dashboard, go to "Email Services"
2. Click "Add New Service"
3. Choose your email provider (Gmail, Outlook, etc.)
4. Follow the setup instructions for your provider
5. **Copy the Service ID** - you'll need this later

### For Gmail:

- You'll need to enable 2-factor authentication
- Create an "App Password" in your Google Account settings
- Use this app password, not your regular password

## Step 3: Create Email Template

1. Go to "Email Templates" in your dashboard
2. Click "Create New Template"
3. **Copy the Template ID** - you'll need this later
4. Design your template with these variables:

**Template Settings:**

- **To Email:** `{{to_email}}` (This is crucial - it tells EmailJS where to send the email)

**Template Content:**

```
Subject: New Contact Form Submission - {{subject}}

From: {{from_name}} ({{from_email}})
To: {{to_name}}

Subject: {{subject}}

Message:
{{message}}

---
This email was sent from your portfolio contact form.
```

**Important:** In the EmailJS template editor, make sure to set the "To Email" field to `{{to_email}}` - this is what tells EmailJS where to send the email!

## Step 4: Get Public Key

1. Go to "Account" → "General"
2. Find your **Public Key** - you'll need this later

## Step 5: Update Your Configuration

1. Copy `.env.example` to `.env.local`
2. Update the values in `.env.local`:

```env
VITE_EMAILJS_SERVICE_ID=service_xxxxxxx
VITE_EMAILJS_TEMPLATE_ID=template_xxxxxxx
VITE_EMAILJS_PUBLIC_KEY=xxxxxxxxxxxxxxxx
VITE_RECIPIENT_EMAIL=your-email@gmail.com
```

**Important:** Make sure to use your actual email address for `VITE_RECIPIENT_EMAIL` - this is where the contact form emails will be sent!

## Step 6: Test Your Setup

1. Run your development server: `npm run dev`
2. Go to the Contact page
3. Fill out and submit the form
4. Check your email inbox for the message

## Template Variables

Your EmailJS template can use these variables:

- `{{from_name}}` - Name from the form
- `{{from_email}}` - Email from the form
- `{{subject}}` - Subject from the form
- `{{message}}` - Message from the form
- `{{to_name}}` - Your name (hardcoded as "Ebuka")
- `{{to_email}}` - Your email address (from environment variable)

## Troubleshooting

### Common Issues:

1. **"Service not found"** - Check your Service ID
2. **"Template not found"** - Check your Template ID
3. **"Invalid public key"** - Check your Public Key
4. **Emails not sending** - Check your email service configuration

### Testing:

- Check browser console for error messages
- Verify all IDs are correct
- Make sure your email service is properly configured
- Check spam folder for test emails

## Security Notes

- Public Key is safe to expose in frontend code
- Service ID and Template ID are also safe to expose
- Never expose your private key or email passwords

## Free Tier Limits

EmailJS free tier includes:

- 200 emails per month
- 2 email services
- 1 email template
- Basic support

For production use, consider upgrading to a paid plan for higher limits and better support.
