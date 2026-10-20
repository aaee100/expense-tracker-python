
# Building a Personal Expense Tracker with Python and Tkinter

## Introduction

Keeping track of personal expenses can help people understand their spending habits and organize their finances. I built this Expense Tracker as a desktop application using Python, Tkinter, and Pandas.

The application allows users to record expenses, organize them into categories, manage expense descriptions, and review spending summaries across different periods and categories. It stores data locally in CSV and JSON files, so it can work offline without requiring an online account or database server.

This project gave me an opportunity to work with Python functions, desktop GUI development, file handling, data validation, and data analysis.

## Features

### 1. Recording expenses

Users can enter four pieces of information for each expense:

- **Date** — when the expense occurred.
- **Category** — the general type of expense, such as Food or Transport.
- **Description** — a more specific detail, such as Groceries or Bus Ticket.
- **Amount** — the cost of the expense.

The application checks that all fields are filled in, validates the date and amount, and saves the new expense when the input is accepted.

### 2. Managing categories and descriptions

The application includes default categories such as Food, Transport, Entertainment, Utilities, Shopping, Health, Education, and Other.

Users can also customize their categories by adding, renaming, deleting, and moving categories or descriptions. This makes the application more flexible than a tracker with a fixed list of expense types.

Category information is stored in a JSON file, allowing custom categories and descriptions to persist between sessions.

### 3. Viewing recorded expenses

The application provides a separate window displaying saved expenses in a table.

The table includes the date, category, description, and amount. Scrollbars make it easier to navigate the displayed records.

### 4. Analyzing spending

The Expense Tracker calculates totals across several dimensions:

- By month
- By year
- By category
- By description
- By category and year
- By category and month

The category and description summaries can also be sorted by amount or alphabetically. These views help users understand where their money is going and identify their largest expense categories.

### 5. Local data storage

The application uses two files:

- `expenses.csv` stores the recorded expenses.
- `categories.json` stores categories and their associated descriptions.

The files are saved in a `data/` directory next to the Python program. The application creates this directory automatically if it does not already exist.

Using local files keeps the project relatively simple and avoids the need to configure a separate database.

## Technologies Used

**Python** — the main programming language used to implement the application's logic.

**Tkinter and ttk** — used to create the desktop interface, input fields, dropdown menus, tables, tabs, and additional windows.

**Pandas** — used to load expense records, process dates and amounts, combine new records with existing data, and calculate grouped spending totals.

**JSON** — used to save and load customizable categories and descriptions.

**Pathlib** — used to define file paths and manage the application's data directory.

## How the Application Works

### 1. Setting up files and directories

The program uses `Path(__file__).parent` to identify the directory containing the Python script. It then defines the data directory and the paths for the expense and category files.

This keeps the storage locations organized relative to the application instead of relying on a particular user's Downloads folder or another fixed location.

### 2. Loading and saving categories

The `load_categories()` function loads the category mapping from `categories.json`. If the file does not exist, the application creates one using the default categories.

The `save_categories()` function organizes the category data and writes it back to JSON. This allows changes made through the category management window to be saved for future sessions.

### 3. Loading and saving expenses

The `load_expenses()` function reads saved records from the CSV file and converts the date and amount columns into appropriate data types.

The `save_expenses()` function prepares the data, rounds amounts to two decimal places, sorts records by date, and writes the results back to CSV.

When a user adds an expense, the application creates a new row and combines it with the existing records before saving the updated data.

### 4. Calculating spending summaries

Pandas makes it possible to group expense records and calculate totals without manually processing every record.

For example, grouping by month makes it possible to calculate monthly spending, while grouping by category shows how much was spent in each expense category.

The application uses these grouped results to populate tables in a separate summary window. Multiple tabs organize the results so that users can explore different views of their spending.

### 5. Building the graphical interface

Tkinter provides the main application window, where users enter expense details and access the application's features.

Separate windows display the expense table, detailed summaries, and category management tools. Functions connected to buttons and dropdown events handle user interactions.

This structure separates many of the application's actions into individual functions, making the code easier to follow and maintain.

## Project Structure

The repository can be organized as follows:

```text
expense-tracker-python/
├── expense_tracker.py
├── README.md
├── article.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── expenses.csv
│   └── categories.json
└── screenshots/
    ├── main-window.png
    ├── expenses-table.png
    └── totals-window.png
```

The `data/` files may be created by the application when it runs, so they do not necessarily need to be committed to the repository. For a public portfolio, fictional sample data is preferable to real personal financial records.

## Challenges and Lessons Learned

One of the main challenges in this project was organizing expense information so that it could be used both for individual records and for summaries.

Working with Pandas helped me understand how to convert data types, sort records, group rows, and calculate totals. Tkinter introduced me to event-driven programming, where functions respond to button clicks and other user interactions.

Another important part was keeping category information separate from expense records. Using JSON for categories and CSV for expenses gave each file a clear purpose.

I also learned that input validation and file handling are important in desktop applications. Dates and amounts need to be checked, and saved data must be loaded consistently so that the application can continue working across sessions.

## Limitations and Future Improvements

Although the application covers the main functions of a basic expense tracker, there are several areas where it could be improved:

- **More robust validation:** enforce a consistent date format and validate amounts more thoroughly, including whether negative amounts should be allowed.
- **Safer file handling:** provide clearer messages for corrupted CSV or JSON files and unexpected file access errors.
- **Improved table interaction:** add sorting by clicking column headings and filtering expenses by date or category.
- **Visual reports:** add charts showing spending patterns over time and spending by category.
- **Budget tracking:** allow users to set monthly budgets and compare spending against them.
- **Export options:** generate Excel or PDF reports.
- **Currency settings:** make the currency symbol configurable instead of always displaying dollars.
- **Dependency documentation:** specify compatible Python and Pandas versions so that installation is reproducible.

These improvements could make the application more convenient and reliable for everyday use.

## AI-Assisted Development

AI tools can be useful during software development for exploring implementation approaches, understanding unfamiliar functions, debugging issues, and improving documentation.

Where AI assistance was used during this project, I treat the generated suggestions as material to review and test rather than assuming that they are automatically correct. Being able to explain the code, verify its behavior, and recognize its limitations is an important part of developing programming skills.

*Adjust this section to accurately describe the assistance you actually used.*

## Conclusion

The Expense Tracker is a practical Python project that combines desktop GUI development, file handling, data management, and basic financial analysis.

It demonstrates how Tkinter can provide a simple interface while Pandas handles data processing and JSON supports customizable application settings. The project also provides a foundation for future improvements, such as charts, budgets, filtering, and report generation.

Building this application helped me practice turning a real-world problem into a working software project while identifying areas where validation, usability, and maintainability could be improved.
