# Architecture Overview

## System Flow

```mermaid
flowchart TD
    A[main.py] --> B[window_manager.py]
    A --> C[db_manegar.py]
    B --> D[gui/ - UI Classes]
    C --> E[(SQLite database.db)]

    subgraph User Flow
        F[Login/Signup] --> G{Admin?}
        G -->|Yes| H[Admin Main Page]
        G -->|No| I[User Main Page]
        H --> J[Manage Halls]
        H --> K[View All Reservations]
        H --> L[View Transactions]
        I --> M[Make Reservation]
        I --> N[View My Reservations]
        M --> O[Payment Page]
    end
```

## Database Schema

```mermaid
erDiagram
    accounts {
        int id PK
        string username
        string password
        boolean is_admin
    }
    halls {
        int id PK
        string name
        int capacity
        float price_per_hour
    }
    reservations {
        int id PK
        int user_id FK
        int hall_id FK
        string date
        int duration
        string status
    }
    transactions {
        int id PK
        int user_id FK
        int reservation_id FK
        float amount
        string date
    }
    accounts ||--o{ reservations : "makes"
    halls ||--o{ reservations : "booked in"
    accounts ||--o{ transactions : "pays"
    reservations ||--o{ transactions : "recorded in"
```

## File Roles

| File | Purpose |
|---|---|
| `main.py` | Entry point. Contains all business logic: login, signup, reservations, payments, table population. |
| `window_manager.py` | Creates all windows, wires button signals to handlers, manages navigation between pages. |
| `db_manegar.py` | Handles all database operations. Creates tables on init, provides CRUD methods for accounts, halls, reservations, and transactions. |
| `gui/*.py` | Auto-generated from Qt Designer `.ui` files. Each file defines the widget layout for one window. |
| `UI/*.ui` | Qt Designer XML files. These are the source files for the GUI layouts. |
