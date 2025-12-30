# subscription-tracker

Lightweight Node.js service to track user subscriptions and send renewal reminders.

Overview
- Tracks subscriptions and renewal dates.
- Sends renewal reminder emails using configured mail transport.
- Includes API routes and a simple workflow for scheduling reminders.

Prerequisites
- Node.js 18+ (or LTS)
- A MongoDB instance (connection string in environment)
- SMTP credentials (for sending email) or a mail testing service like Mailtrap

Quick start
1. Clone the repo and install dependencies:

	```bash
	git clone <repo-url>
	cd subscription-tracker
	npm install
	```

2. Create environment variables. Copy or create a `.env` file and set at least:

	- `PORT` (defaults to 8080)
	- `MONGODB_URI` (MongoDB connection string)
	- SMTP settings used by `config/nodemailer.js` (e.g. `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASS`)
	- `SUPPORT_EMAIL` (optional, used in email templates)
	- QStash / Upstash credentials if you use scheduled jobs (optional)

	See `config/env.js` for more environment usage details.

3. Run in development mode:

	```bash
	npm run dev
	```

4. Start production server:

	```bash
	npm start
	```

Project layout (important files)
- `app.js` — app entrypoint
- `package.json` — npm scripts and dependencies
- `config/` — environment and integrations (see `config/nodemailer.js` and `config/upstash.js`)
- `controllers/` — request handlers and business logic
- `routes/` — API route definitions
- `models/` — Mongoose models for `User` and `Subscription`
- `utils/email-template.js` — email templates (including renewal reminder)

Using the renewal template
- Import the template: `const { renewalReminderTemplate } = require('./utils/email-template')`
- Call it with `{ email, username, planName, renewalDate, amount, currency, billingCycle, paymentMethod, accountUrl, supportEmail, unsubscribeUrl, additionalNotes }` and send using your mailer. It returns `{ subject, text, html }` ready for your transporter.

Development notes
- API routes are defined in the `routes/` folder; adjust or add routes as needed.
- Scheduling of reminders may use QStash / Upstash; check `config/upstash.js` and any CRON/QStash integrations.

Contributing
- Open an issue or PR. Keep changes small and focused.

License
- (Add project license information here)
