# Split Payment App – Backend

A Node.js/Express backend for managing group expenses, splitting payments, and enforcing group budgets. This API powers the Split Payment App, allowing users to track shared expenses, upload receipts, and receive notifications.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Setup & Installation](#setup--installation)
- [Environment Variables](#environment-variables)
- [Database Setup](#database-setup)
- [Running the Server](#running-the-server)
- [API Endpoints](#api-endpoints)
- [Testing](#testing)
- [Error Handling](#error-handling)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Features

- **User and Group Management:** Create users and groups, add/remove members.
- **Expense Tracking:** Add, view, and filter expenses by group, category, or date.
- **Expense Splitting:** Automatically split expenses among group members.
- **Receipt Uploads:** Attach image receipts to expenses.
- **Budget Enforcement:** Set monthly group budgets and block or warn on overspending.
- **Webhook Notifications:** Trigger webhooks on key events (e.g., expense created).
- **RESTful API:** Well-structured endpoints for easy integration.

---

## Tech Stack

- **Node.js** (runtime)
- **Express.js** (web framework)
- **PostgreSQL** (database)
- **pg** (PostgreSQL client)
- **Multer** (file uploads)
- **dotenv** (environment variables)
- **Jest** (testing, if configured)

---

## Project Structure

```
split-payment-backend/
├── config/           # Database and app configuration
├── controllers/      # Route handler logic
├── models/           # Database models and queries
├── routes/           # Express route definitions
├── utils/            # Utility functions (e.g., webhook triggers)
├── uploads/          # Uploaded receipt images (gitignored)
├── .env              # Environment variables (gitignored)
├── .gitignore
├── package.json
├── README.md
```

---

## Setup & Installation

### Prerequisites

- [Node.js](https://nodejs.org/)
- [npm](https://www.npmjs.com/)
- [PostgreSQL](https://www.postgresql.org/)
- [Git](https://git-scm.com/)

### Installation Steps

1. **Clone the repository**
   ```sh
   git clone https://github.com/your-username/split-payment-app.git
   cd split-payment-app/split-payment-backend
   ```

2. **Install dependencies**
   ```sh
   npm install
   ```

3. **Configure environment variables**  
   See [Environment Variables](#environment-variables).

4. **Set up the database**  
   See [Database Setup](#database-setup).

---

## Environment Variables

Create a `.env` file in the root of `split-payment-backend`:

```
DATABASE_URL=postgres://username:password@localhost:5432/your_db
PORT=5000
WEBHOOK_URL=https://your-webhook-url.com
```

- `DATABASE_URL`: PostgreSQL connection string.
- `PORT`: Port for the Express server.
- `WEBHOOK_URL`: (Optional) URL to send webhook notifications.

---

## Database Setup

1. **Create a PostgreSQL database**  
   Example:
   ```sql
   CREATE DATABASE split_payment_db;
   ```

2. **Create tables**  
   Example schema (simplified):

   ```sql
   CREATE TABLE users (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100) NOT NULL,
     email VARCHAR(100) UNIQUE NOT NULL
   );

   CREATE TABLE groups (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100) NOT NULL
   );

   CREATE TABLE group_members (
     group_id INT REFERENCES groups(id),
     user_id INT REFERENCES users(id),
     PRIMARY KEY (group_id, user_id)
   );

   CREATE TABLE expenses (
     id SERIAL PRIMARY KEY,
     group_id INT REFERENCES groups(id),
     paid_by INT REFERENCES users(id),
     amount NUMERIC(10,2) NOT NULL,
     category VARCHAR(50),
     description TEXT,
     receipt_url VARCHAR(255),
     created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );

   CREATE TABLE expense_shares (
     expense_id INT REFERENCES expenses(id),
     user_id INT REFERENCES users(id),
     amount NUMERIC(10,2) NOT NULL,
     PRIMARY KEY (expense_id, user_id)
   );

   CREATE TABLE group_budgets (
     id SERIAL PRIMARY KEY,
     group_id INT REFERENCES groups(id),
     monthly_limit NUMERIC(10,2) NOT NULL,
     active BOOLEAN DEFAULT TRUE
   );
   ```

   *(Adjust as per your actual schema.)*

---

## Running the Server

```sh
npm start
```
Server runs at `http://localhost:5000` by default.

---

## API Endpoints

### Groups

- `POST /groups`  
  Create a new group.

- `GET /groups/:groupId`  
  Get group details.

- `POST /groups/:groupId/budget`  
  Set or update a group’s monthly budget.

### Users

- `POST /users`  
  Create a new user.

- `POST /groups/:groupId/members`  
  Add a user to a group.

### Expenses

- `POST /expenses`  
  Add a new expense (supports file upload for receipts).

  **Request Example:**
  ```json
  {
    "groupId": 1,
    "paidBy": 2,
    "amount": 500,
    "category": "Food",
    "description": "Dinner at restaurant",
    "splits": [
      { "userId": 2, "amount": 250 },
      { "userId": 3, "amount": 250 }
    ]
  }
  ```

- `GET /groups/:groupId/expenses`  
  Get all expenses for a group (supports filters).

### Webhooks

- Webhook is triggered on expense creation (see `utils/webhook.js`).

---

## Testing

If tests are configured (e.g., with Jest):

```sh
npm test
```

---

## Error Handling

- All endpoints return appropriate HTTP status codes.
- Errors are logged and returned in JSON format.

---

## Security

- **Secrets:** `.env` and sensitive files are excluded via `.gitignore`.
- **Validation:** Input is validated in controllers.
- **Uploads:** Only image files are allowed for receipts.
- **Do not commit secrets or node_modules.**

---

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Create a new Pull Request

---

## License

MIT

---

## Contact

For questions or support, open an issue or
