# Split Payment App – Group Expense & Settlement Platform

A full-featured backend API built with **Node.js**, **Express**, and **PostgreSQL** for managing shared group expenses, calculating balances, optimizing settlements, and generating reports.

---

## 📅 Features

### ✅ Core Modules

* **User Auth**: JWT login/register, password hashing with bcrypt
* **Groups**: Create groups, add/remove members, assign roles (Admin, Member, Viewer)
* **Expenses**:

  * Add expenses (equal/unequal splits, exact amounts)
  * Receipt upload (Multer)
  * Comments + Emoji reactions
  * Expense locking after 7 days
* **Balances**:

  * Real-time net balances
  * Smart debt optimization (like Splitwise)
* **Settlements**:

  * Manual payments
  * UPI link and QR code generation
  * Recurring contribution scheduler (cron-based)
* **Reports**:

  * Monthly summary & top contributors
  * Budget limit alerts
  * Export to CSV / PDF
* **Notifications**:

  * Console/email reminders for dues
  * Webhook and push-style alerts (demo only)

---

## 🌐 Tech Stack

* **Backend**: Node.js, Express.js
* **Database**: PostgreSQL
* **Auth**: JWT, bcrypt
* **Uploads**: Multer
* **Email**: Nodemailer
* **PDF/CSV**: pdfkit, json2csv
* **Scheduler**: node-cron

---

## 🚀 Getting Started

### 1. Clone the Repo

```bash
git clone https://github.com/your-username/split-payment-backend.git
cd split-payment-backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Setup Environment Variables

Create `.env` file:

```env
PORT=5000
DB_NAME=splitpaydb
DB_USER=youruser
DB_PASSWORD=yourpass
DB_HOST=localhost
JWT_SECRET=your_jwt_secret
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
```

### 4. Run the App

```bash
npm run dev
```

---

## 📒 API Endpoints

### ✨ Auth

* `POST /api/auth/register`  → Register new user
* `POST /api/auth/login`     → Login user

### 🪢 Groups

* `POST /api/groups/create`  → Create group
* `POST /api/groups/add-member` → Add member
* `GET /api/groups/my-groups`   → View my groups
* `GET /api/groups/:groupId/members`

### 📅 Expenses

* `POST /api/expenses/add` (Form-data with receipt + JSON)
* `GET /api/expenses/:groupId`
* `POST /api/expenses/:expenseId/comment`
* `GET /api/expenses/:expenseId/comments`

### ♻️ Balances

* `GET /api/balances/:groupId`

### 💳 Settlements

* `POST /api/settlements/add`
* `GET /api/settlements/:groupId`
* `GET /api/settlements/upi-link`
* `GET /api/settlements/upi-qr`
* `POST /api/settlements/recurring`

### 📊 Reports

* `GET /api/reports/summary?groupId=1&month=6&year=2025`
* `GET /api/reports/export/:groupId/csv`
* `GET /api/reports/export/:groupId/pdf`

---

## 📄 Testing With Postman

1. Use `/api/auth/login` to get a JWT token
2. Use `Bearer Token` auth in Postman for secured routes
3. Upload receipts using form-data:

   * Key: `receipt` (file)
   * Key: `data` (text, JSON string)

---

## 📅 Scheduler

* **Auto monthly contributions**: via `node-cron`
* **Daily due reminders**: email or console alerts at 8AM

---

## 📃 License

MIT

---

## ✨ Author

https://github.com/KrishTanna28
