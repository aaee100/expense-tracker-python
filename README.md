# Expense Tracker (Python + Tkinter)

![Python](https://img.shields.io/badge/Python-3-blue)
![GUI](https://img.shields.io/badge/GUI-Tkinter-green)
![Data](https://img.shields.io/badge/Data-Pandas-orange)

## About the Project

Expense Tracker is a desktop application built with **Python**, **Tkinter**, and **Pandas** for recording and organizing personal expenses.

Users can add expenses, manage categories and descriptions, view all recorded transactions, and analyze spending through detailed summaries. The application stores its data locally in CSV and JSON files, so it works completely offline.

## Screenshots

### Main Window

![Main Window](screenshots/main-window.png)

### Expense List

![Expense List](screenshots/expenses-table.png)

### Expense Summary

![Expense Summary](screenshots/totals-window.png)

## Features

- Add expenses with a date, category, description, and amount.
- Select categories and descriptions from editable dropdown menus.
- Add, rename, delete, and move categories and descriptions.
- Automatically sort expense records chronologically.
- View all saved expenses in a scrollable table.
- View spending totals by month, year, category, and description.
- View category totals by month and year.
- Sort category and description summaries alphabetically or by amount.
- Store expense records and category settings locally.
- Automatically create the application's `data/` directory when needed.

## Technologies Used

- Python
- Tkinter and ttk
- Pandas
- JSON
- Pathlib

## Requirements

- Python
- pandas

Install the required package:

```bash
pip install -r requirements.txt
```

Tkinter is included with most standard Python installations.

## Installation

1. Clone this repository.

2. Open the project directory.

3. Install the required dependency:

   ```bash
   pip install -r requirements.txt
   ```

4. Run the application:

   ```bash
   python expense_tracker.py
   ```

The application automatically creates a `data/` directory beside the Python script if it does not already exist.

## Project Structure

```text
expense-tracker-python/
├── expense_tracker.py
├── data/
│   ├── expenses.csv
│   └── categories.json
├── screenshots/
│   ├── main-window.png
│   ├── expenses-table.png
│   └── totals-window.png
├── requirements.txt
├── .gitignore
├── README.md
└── article.md
```

The two files inside `data/` are created automatically when the application runs. They contain the user's expense records and category configuration.

## Data Storage

The application uses two local files:

- **expenses.csv** — stores expense dates, categories, descriptions, and amounts.
- **categories.json** — stores categories and their associated descriptions.

The CSV file is sorted chronologically when expenses are saved. Category changes are stored in the JSON file and remain available when the application is restarted.

For a public repository, use fictional sample data rather than personal financial records.

## Future Improvements

- Add charts for monthly and category-based spending.
- Introduce monthly budgets and remaining-balance tracking.
- Add search and filtering by date, category, or description.
- Export expense summaries to Excel or PDF.
- Add backup and restore functionality.
- Support different currencies.

## License

This project is open source and available under the MIT License.
