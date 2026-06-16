# Conference Hall Reservation System

A desktop application for managing conference hall bookings, built with Python and PySide6 (Qt for Python). This was a university project for a Data Engineering course.

## What It Does

The application lets users sign up, log in, browse available halls, and make reservations. Admin users can manage halls, view all reservations across users, and check payment transactions. The interface is a multi-window desktop GUI built with Qt Designer `.ui` files.

## Features

- User registration and login (with admin role support)
- Hall browsing with capacity and hourly pricing
- Make a reservation by picking a hall, date, and duration
- Automatic price calculation based on duration and hall rate
- Payment confirmation flow with transaction logging
- View and manage your own reservations (edit date, delete)
- Admin panel for managing halls (add, edit, delete)
- Admin panel for viewing and canceling any reservation
- Admin panel for viewing all payment transactions
- SQLite database for local data persistence

## Technologies

- Python 3.13
- PySide6 (Qt 6.9)
- SQLite3
- Qt Designer (for UI layout files)

## How It Works

The application uses a simple layered structure:

- `main.py` is the entry point. It creates the main window and contains all the business logic for authentication, reservations, payments, and table population.
- `window_manager.py` handles creating and showing/hiding the different windows. It imports the auto-generated UI classes from the `gui/` folder.
- `db_manegar.py` is the database layer. It manages four tables: accounts, halls, reservations, and transactions. All SQL queries are in this file.
- `gui/` contains the auto-generated Python files from Qt Designer `.ui` files. Each file defines the layout for one window.
- `UI/` contains the original `.ui` XML files edited in Qt Designer.

The flow is straightforward: a user logs in, the app checks if they are an admin or regular user, and shows the appropriate main page. From there they navigate to sub-pages for reservations, hall management, etc. Each sub-page is a separate `QDialog` window.

## Setup

1. Make sure you have Python 3.10 or newer installed.
2. Install the required package:

   ```
   pip install PySide6
   ```

3. From the project root, run:

   ```
   python src/main.py
   ```

   The database file (`database.db`) will be created automatically on first run.

## How to Test

There is no automated test suite. To test manually:

1. Run the application.
2. Sign up as a regular user.
3. Log in and try making a reservation.
4. Sign up with the admin radio button checked to create an admin account.
5. Log in as admin and test hall management and reservation oversight.

## Project Structure

```
.
├── src/
│   ├── main.py              # Application entry point and business logic
│   ├── window_manager.py    # Window creation and navigation
│   ├── db_manegar.py        # Database manager (SQLite)
│   ├── gui/                 # Auto-generated UI classes from Qt Designer
│   │   ├── Login.py
│   │   ├── Signup.py
│   │   ├── MainPage.py
│   │   ├── AdminLogin.py
│   │   ├── AdminMainPage.py
│   │   ├── MakeReservation.py
│   │   ├── ViewReservations.py
│   │   ├── ManageHall.py
│   │   ├── ManageReservations.py
│   │   ├── PaymentPage.py
│   │   └── PaymentTransactions.py
│   └── UI/                  # Qt Designer .ui files (source layouts)
├── docs/                    # Documentation and diagrams
├── .gitignore
└── README.md
```

## Screenshots

The following screenshots would be useful for understanding the UI:

1. **Login screen** -- shows the main login form with username/password fields and buttons for admin login and signup
2. **Signup screen** -- shows the registration form with the admin radio button option
3. **User main page** -- shows the two options: Make Reservation and View Reservations
4. **Make Reservation page** -- shows the hall dropdown, date picker, and duration spinner
5. **Payment page** -- shows the reservation summary and pay button
6. **Admin main page** -- shows the three admin options: Manage Halls, View All Reservations, View Transactions
7. **Manage Halls page** -- shows the halls table with add/edit/delete buttons

## Future Improvements

- Add input validation (e.g., prevent past dates, check for overlapping reservations)
- Add a search or filter option for reservations
- Improve the database class to use context managers for connections
- Add proper password hashing instead of storing plaintext
- Add a "forgot password" flow
- Support editing more reservation fields (not just the date)
- Add export to CSV for transactions
