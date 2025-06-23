# Split Payment App – Backend

This is the backend API for the Split Payment App, a Node.js/Express application that helps groups track shared expenses, split bills, and manage group budgets.

## Features

- **Create and manage groups**
- **Add expenses with receipts**
- **Split expenses among group members**
- **Set and enforce monthly group budgets**
- **Expense filtering by category, amount, and date**
- **Webhook support for notifications**

## Tech Stack

- Node.js
- Express.js
- PostgreSQL
- Multer (for file uploads)
- dotenv (for environment variables)

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/)
- [PostgreSQL](https://www.postgresql.org/)
- [Git](https://git-scm.com/)

### Installation

1. **Clone the repository**
   ```sh
   git clone https://github.com/your-username/split-payment-app.git
   cd split-payment-app/split-payment-backend
   ```

2. **Install dependencies**
   ```sh
   npm install
   ```

3. **Set up environment variables**

   Create a `.env` file in the root of `split-payment-backend`:

   ```
   DATABASE_URL=postgres://username:password@localhost:5432/your_db
   PORT=5000
   ```

4. **Set up the database**

   - Create a PostgreSQL database.
   - Run the SQL scripts in the `models` or `migrations` folder to create tables.

5. **Start the server**
   ```sh
   npm start
   ```

   The server will run on `http://localhost:5000` by default.

## API Endpoints

### Expenses

- `POST /expenses`  
  Add a new expense (with optional receipt upload).

- `GET /groups/:groupId/expenses`  
  Get all expenses for a group (with filters).

### Groups

- `POST /groups`  
  Create a new group.

- `GET /groups/:groupId`  
  Get group details.

### Budgets

- `POST /groups/:groupId/budget`  
  Set or update a group’s monthly budget.

## Folder Structure

```
split-payment-backend/
├── controllers/
├── config/
├── models/
├── routes/
├── utils/
├── uploads/
├── .env
├── .gitignore
├── package.json
└── README.md
```

## Security

- **Do not commit your `.env` file or secrets.**
- All secrets and sensitive files are excluded via `.gitignore`.

## License

MIT
