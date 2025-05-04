## Expenses Controller

**Version:** 1.0

A Jupyter‑based Python project to record your expenses into a PostgreSQL database and visualize them through an interactive dashboard.

---

### 🔖 Table of Contents

1. [Description](#description)
2. [Features](#features)
3. [Requirements](#requirements)
4. [Installation](#installation)
5. [Configuration](#configuration)
6. [Usage](#usage)
7. [Database Schema](#database-schema)
8. [Project Structure](#project-structure)
9. [Contributing](#contributing)
10. [License](#license)
11. [Contact](#contact)

---

## Description

This project, **Expenses Controller**, helps you:

* **Record** expenses via a Jupyter Notebook form (using `ipywidgets`).
* **Store** them in a PostgreSQL database.
* **Visualize** summaries and charts of your spending in another notebook acting as a dashboard.

You can run the data‑entry notebook to add new expenses, then open the dashboard notebook to explore totals by category, trends over time, and more.

---

## Features

* Dynamic form for entering expenses with date, category, detail, and amount.
* PostgreSQL integration via `psycopg2`.
* Automated summary and bar charts with `pandas`, `matplotlib`, and `seaborn`.
* Fully contained in Jupyter Notebooks for easy experimentation.

---

## Requirements

* Python **3.1** or higher
* PostgreSQL database

**Python libraries** (add to `requirements.txt` or install via `pip`):

```
psycopg2>=2.9.10
pandas>=2.2.0
matplotlib>=3.8.3
seaborn>=0.13.2
ipywidgets>=8.1.5
```

---

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/your‑username/expenses-controller.git
   cd expenses-controller
   ```
2. (Optional) Create and activate a virtual environment:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

---

## Configuration

1. **Database credentials**: Copy `hidden.py.example` to `hidden.py` and enter your own PostgreSQL host, port, database name, user, and password.

   ```python
   # hidden.py
   secrets = {
       'host': 'YOUR_HOST',
       'port': 5432,
       'database': 'your_db',
       'user': 'your_user',
       'pass': 'your_password'
   }
   ```
2. **Create schema**: Run the provided SQL script `schema.sql` against your PostgreSQL instance.

---

## Usage

Launch Jupyter Notebook or Lab in the project folder:

```bash
jupyter lab
# or
jupyter notebook
```

1. **Data Entry**: Open `data_entry.ipynb`, fill out the expense form, and submit to insert records into the database.
2. **Dashboard**: Open `dashboard.ipynb` to view summaries and charts. You can run this notebook any time to visualize existing expenses.

> **Note**: If you already have expenses in your database, you can skip straight to the dashboard notebook.

---

## Database Schema

Below is the SQL to create the required tables. Save this as `schema.sql` and run it before using the notebooks:

```sql
-- Table for categories
CREATE TABLE category (
    id SERIAL PRIMARY KEY,
    cat_name TEXT NOT NULL
);

-- Table for transactions
CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    cat_id INTEGER REFERENCES category(id),
    tran_date DATE NOT NULL,
    detail TEXT,
    total_amount NUMERIC(12, 2) NOT NULL
);
```

---

## Project Structure

```
expenses-controller/
├── hidden.py.example      # copy to hidden.py with your DB creds
├── schema.sql             # SQL script to create tables
├── data_entry.ipynb       # Notebook with ipywidgets form to add expenses
└── dashboard.ipynb        # Notebook with summaries and charts
```

---

## Contributing

Contributions are welcome! Please:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/YourFeature`).
3. Commit your changes (`git commit -m "Add new feature"`).
4. Push to your branch (`git push origin feature/YourFeature`).
5. Open a Pull Request.

Please ensure code is well-documented and notebooks run without errors.

---

## License

This project is distributed under the **MIT License**. See `LICENSE` for details.

---

## Contact

Created by **Your Name**. For questions or issues, please open an issue on GitHub.
