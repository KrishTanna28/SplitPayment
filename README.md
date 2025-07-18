# Split Payment App - Backend

## Overview

The Split Payment App backend is a Node.js/Express server that enables users to manage group expenses, split bills, track balances, and settle up efficiently. It supports group management, expense tracking, settlements (including UPI QR code generation), reporting, and automated reminders.

---

## Features

- **User Authentication**: Secure registration and login with JWT.
- **Group Management**: Create groups, add/remove members, and manage group roles.
- **Expense Tracking**: Add expenses, split among members, upload receipts, and enforce group budgets.
- **Balance Calculation**: Real-time calculation and optimization of who owes whom.
- **Settlements**: Record payments, generate UPI QR codes, and handle recurring contributions.
- **Reports**: Export expenses as CSV or PDF, and view monthly summaries.
- **Notifications & Reminders**: Email notifications for expenses, reminders for dues, and scheduled recurring contributions.
- **File Uploads**: Upload and store receipts securely.

---

## Project Structure

```
split-payment-backend/
  config/           # Database configuration
  controllers/      # Business logic for each module
  cron/             # Scheduled jobs (reminders, recurring expenses)
  middleware/       # Auth, error handling, file uploads
  routes/           # API endpoints
  utils/            # Helper functions (mailer, optimizer)
  uploads/          # Uploaded receipts
  package.json      # Project metadata and dependencies
  server.js         # Entry point
```

---

## Tech Stack

- **Node.js** (Express)
- **PostgreSQL**
- **JWT** for authentication
- **Multer** for file uploads
- **Nodemailer** for emails
- **node-cron** for scheduled jobs
- **PDFKit**, **json2csv** for reports
- **qrcode** for UPI QR code generation

---

## Getting Started

### Prerequisites

- Node.js (v16+ recommended)
- PostgreSQL database
- Gmail account for sending emails (or configure another SMTP provider)

### Installation

1. **Clone the repository:**
   ```bash
   git clone <repo-url>
   cd split-payment-backend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Set up environment variables:**
   Create a `.env` file in the root with the following:
   ```
   PORT=5000
   DB_USER=your_db_user
   DB_HOST=localhost
   DB_NAME=your_db_name
   DB_PASSWORD=your_db_password
   JWT_SECRET=your_jwt_secret
   EMAIL_USER=your_gmail_address
   EMAIL_PASS=your_gmail_app_password
   ```

4. **Run database migrations** (if any).

5. **Start the server:**
   ```bash
   npm run dev
   ```

---

## API Endpoints

### Auth

- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login and receive JWT

### Groups

- `POST /api/groups/create` - Create a new group
- `GET /api/groups/` - List user's groups
- `POST /api/groups/:groupId/add-member` - Add member to group
- `POST /api/groups/:groupId/remove-member` - Remove member

### Expenses

- `POST /api/expenses/:groupId/add` - Add an expense (with optional receipt upload)
- `GET /api/expenses/:groupId` - List expenses in a group

### Balances

- `GET /api/balances/:groupId` - Get net balances and optimized settlements

### Settlements

- `POST /api/settlements/:groupId/add` - Record a settlement
- `GET /api/settlements/:groupId` - List settlements
- `GET /api/settlements/upi/:userId` - Generate UPI QR code for payment

### Reports

- `GET /api/reports/summary?groupId=&month=&year=` - Monthly summary
- `GET /api/reports/:groupId/csv` - Export expenses as CSV
- `GET /api/reports/:groupId/pdf` - Export expenses as PDF

---

## Scheduled Jobs

- **Daily Reminders**: Sends email reminders for unpaid balances.
- **Recurring Contributions**: Automatically adds recurring expenses (e.g., rent) as per schedule.

---

## File Uploads

- Receipts are uploaded and stored in the `uploads/` directory.
- Only `.png`, `.jpg`, `.jpeg`, and `.pdf` files are allowed.

---

## Error Handling

- Centralized error handler returns JSON error messages.
- Auth middleware protects routes and validates JWT.

---

## Contribution

1. Fork the repo
2. Create your feature branch (`git checkout -b feature/foo`)
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

---

## License

This project is licensed under the ISC License.

---

## Acknowledgements

- Inspired by Splitwise and similar expense-sharing apps.
- Built with Node.js, Express, and PostgreSQL. 
