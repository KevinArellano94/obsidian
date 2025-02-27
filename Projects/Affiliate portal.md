#02-24-2025 #humblefunding #aws #railway #react-typescript-swc #apollo-graphql #neondb #postgress

# Affiliate Portal Development Plan

## Overview

The affiliate portal will function as a standalone system, separate from the main platform, featuring its own registration and login system. Affiliates can sign up to promote products (evaluation accounts and rebills) and earn a 25% recurring commission for every successful sale and rebill attributed to them. The portal will integrate with Rewardful, which is compatible with Stripe, to handle tracking and payouts.

## Core Features

### 1. Registration and Login System

- A standalone registration and login system dedicated to affiliates.
- Fields required during registration: Full Name, Email Address, Password, Tax Information (optional), and Bank Details for payouts.
- Two-Factor Authentication (2FA) for added security.

### 2. Integration with Rewardful

- **Rewardful** will be used to track affiliate links, cookies, and commissions.
- **Tracking Process**:
	- A visitor clicks on an affiliate's unique link.
	- A cookie is placed on the visitor's browser (cookie lifespan to be set to ensure tracking persists).
	- If the visitor completes a purchase, the sale is credited to the affiliate’s account.

### 3. Separate Dashboard

- A modern, user-friendly design showcasing:
	- **Account Balance**: Real-time updates on total earnings and commissions owed.
	- **Link Generator**: Affiliates can generate unique links for promoting products (evaluation accounts). These links will:
		- Redirect users to the payment page (via Stripe).
		- Be embedded with tracking identifiers.
	- **Payment History**: A detailed history of all payouts and commissions earned.
	- **Referral Statistics**: Show data such as clicks, conversions, and earnings from referrals.
- A system to display affiliate names and ID numbers for easy identification.

### 4. Payout System

- **Monthly Payouts**:
	- Commissions will be paid out monthly to affiliates with a balance of $80 or more.
- **Payment Methods**:
	- For U.S.-based affiliates: Direct Deposit to their bank accounts.
	- For international affiliates: Alternative methods such as PayPal or Wise.
- **Payout threshold**:
	- Of $80:
	- Affiliates with balances below $80 will not be eligible for withdrawal.
- **Automation**:
	- The system will automatically calculate payouts at the end of the month.
	- Ensure compliance with financial regulations for both domestic and international payouts.
- **Bank Details Input**:
	- Affiliates can securely input and update their bank or payment details in the dashboard.

### 5 Tracking Mechanism Options

- **Option 1**: Cookie-Based Links (Recommended):
	- Each affiliate is assigned a unique link.
	- Cookies track visitors who click on the link and attribute sales to the affiliate.
	- **Benefits**:
		- Simplified tracking, supports recurring commissions automatically through Rewardful.
- **Option 2**: Stripe Payment Links:
	- Each affiliate is assigned a Stripe-generated payment link.
	- Payment success events are used to attribute sales to the affiliate.
	- **Benefits**:
		- Offers direct Stripe integration but might be less scalable for affiliates compared to cookie-based tracking

### 6. Recurring Commissions

- Affiliates will earn **25%** recurring commissions for the lifetime of customers they refer.

### 7. Withdrawal Requests

- Only affiliates with balances above **$600** can request payouts.
- Affiliates below the threshold will have their commissions rolled over to the next month.

### 8. Admin Features

- A **backend system** for admins to:
	- View affiliate statistics and payout statuses.
	- Manually approve or reject withdrawals (if needed).
	- Add/remove affiliates.
	- Adjust commission rates for specific affiliates

______

# Affiliate Portal Required Implementation

## Core Features

### 1. Registration and Login System

- Two-Factor Authentication (2FA) for added security.

### 3. Separate Dashboard

- **Payment History**: A detailed history of all payouts and commissions earned.

### 4. Payout System

- **Monthly Payouts**:
	- Commissions will be paid out monthly to affiliates with a balance of *$80* **(changed to $600)** or more.
- **Payout threshold**:
	- Of *$80* **(changed to $600)**:
	- Affiliates with balances below *$80* **(changed to $600)** will not be eligible for withdrawal.
- **Automation**:
	- The system will automatically calculate payouts at the end of the month.
	- Ensure compliance with financial regulations for both domestic and international payouts.

### 6. Recurring Commissions

- **Handled by Rewardful**
- Affiliates will earn **25%** recurring commissions for the lifetime of customers they refer.

### 8. Admin Features

- **Handled by Rewardful**
- Adjust commission rates for specific affiliates

______
