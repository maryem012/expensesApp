# ExpensesApp

A personal finance management web application built with **ASP.NET Core 8.0 MVC** and **SQL Server**. It allows users to track income and expenses by category, visualize spending trends, and maintain a clear picture of their financial balance.

## Features

- **Dashboard** – Overview of the last 7 days including:
  - Total Income
  - Total Expense
  - Current Balance (displayed in Tunisian Dinar – DT)
  - Doughnut chart: expenses broken down by category
  - Spline chart: income vs. expense trend over the last 7 days
  - Recent transactions list (last 5)
- **Transaction Management** – Add, edit, and delete financial transactions linked to a category
- **Category Management** – Create and manage income/expense categories with custom icons

## Tech Stack

| Layer        | Technology                                 |
|-------------|---------------------------------------------|
| Framework   | ASP.NET Core 8.0 MVC                        |
| ORM         | Entity Framework Core 8.0                   |
| Database    | Microsoft SQL Server                        |
| UI Charts   | Syncfusion EJ2 for ASP.NET Core             |
| Language    | C# / Razor Views                            |

## Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (local or remote instance)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) (recommended) or VS Code with C# extension

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/maryem012/expensesApp.git
cd expensesApp
```

### 2. Configure the database connection

Open `projetNet/appsettings.json` and update the `DevConnection` connection string to match your SQL Server instance:

```json
"ConnectionStrings": {
  "DevConnection": "Server=YOUR_SERVER;Database=TransactionDB;Trusted_Connection=True;MultipleActiveResultSets=True;TrustServerCertificate=True;"
}
```

### 3. Apply database migrations

```bash
cd projetNet
dotnet ef database update
```

### 4. Run the application

```bash
dotnet run
```

The app will be available at `https://localhost:5001` (or the port shown in your terminal).

## Project Structure

```
expensesApp/
├── projetNet/
│   ├── Controllers/
│   │   ├── DashboardController.cs   # Dashboard summary & charts
│   │   ├── TransactionController.cs # Transaction CRUD
│   │   ├── CategoryController.cs    # Category CRUD
│   │   └── HomeController.cs
│   ├── Models/
│   │   ├── AppDbContext.cs          # EF Core DbContext
│   │   ├── Transaction.cs           # Transaction entity
│   │   └── Category.cs             # Category entity
│   ├── Views/
│   │   ├── Dashboard/
│   │   ├── Transaction/
│   │   ├── Category/
│   │   └── Shared/
│   ├── wwwroot/                     # Static assets
│   ├── appsettings.json
│   └── Program.cs
└── projetNet.sln
```

## Data Models

### Category
| Field      | Type          | Description                    |
|-----------|---------------|--------------------------------|
| CategoryId | int          | Primary key                    |
| Title      | nvarchar(50) | Category name (required)       |
| Icon       | nvarchar(5)  | Emoji or icon for the category |
| Type       | nvarchar(10) | `"Income"` or `"Expense"`      |

### Transaction
| Field         | Type          | Description                          |
|--------------|---------------|--------------------------------------|
| TransactionId | int          | Primary key                          |
| CategoryId    | int          | Foreign key to Category              |
| Amount        | int          | Transaction amount (must be > 0)     |
| Note          | nvarchar(75) | Optional note                        |
| Date          | DateTime     | Transaction date (defaults to today) |

## License

This project is open source and available under the [MIT License](LICENSE).
