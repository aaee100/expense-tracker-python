# Building a Personal Expense Tracker with Python, Tkinter, and Pandas

## Introduction

Keeping track of personal expenses can help people understand their spending habits and organize their finances. I built this Expense Tracker as a desktop application using Python, Tkinter, and Pandas.

The application allows users to record expenses, organize them into categories, manage descriptions, and review spending summaries across different periods. It stores information locally in CSV and JSON files, so it works without an online account or database server.

The project began as a relatively simple programming exercise. During development, I gradually expanded its functionality, improved the interface, and fixed several problems discovered through testing. It became an opportunity to practice desktop GUI development, file handling, data validation, data organization, and data analysis.

## How the Project Developed

### 1. Starting with a simple CSV expense tracker

The original assignment was to build a small desktop application that could record daily expenses.

The first version had four input fields:

- **Date** — when the expense occurred.
- **Category** — the general type of expense.
- **Description** — a more specific explanation.
- **Amount** — how much was spent.

Users could add an expense, save it to a CSV file, and see the overall amount spent.

Initially, the CSV file was stored in the user's Downloads folder. The application was then extended with a separate window containing a scrollable table, allowing users to view their saved expense records.

### 2. Improving categories and chronological sorting

After testing the first version, I identified several improvements that would make the application more practical.

I wanted users to select common categories and descriptions from dropdown menus without being restricted to predefined options. The solution was to use editable comboboxes: users could select an existing entry or type something new.

Another improvement concerned the order of expense records. The original application appended every new expense to the end of the CSV file. This was inconvenient when entering an expense from an earlier date.

I changed the saving process so that records are sorted chronologically. An older expense is therefore placed in its correct position rather than appearing after newer entries.

### 3. Expanding the spending summaries

The next major improvement was the analysis functionality.

Instead of displaying only the overall amount spent, I wanted users to understand how their expenses were distributed.

The summary window was expanded with separate tabs:

- **By Month** — total spending for each month.
- **By Year** — total spending for each year.
- **By Category** — total spending for each category.
- **By Description** — total spending for each description.
- **By Category & Year** — spending for each category in each year.
- **By Category & Month** — spending for each category in each month.

Pandas made these calculations easier through grouping and aggregation operations.

I also added sorting options to the category and description summaries, allowing users to organize the results alphabetically or by spending amount.

### 4. Debugging the summary calculations

The summary functionality required several rounds of testing and debugging.

One issue involved floating-point precision. Some totals appeared with unnecessary decimal digits, such as `126.10000000000001`, instead of `126.10`. I addressed the display problem by rounding monetary values and formatting amounts to two decimal places.

Another challenge appeared when implementing the sorting options for the category and description tabs. The initial code did not consistently handle the different structures returned by Pandas. Some attempts produced incorrect values or caused errors when the program tried to convert summary data into numbers.

The solution was to introduce helper functions that normalize summary data into simple label-and-value pairs before displaying or sorting it.

These problems showed me that calculating a total is only part of data analysis. The program must also handle the resulting data structure correctly and present the results in a form that users can understand.

### 5. Creating a category management window

As the application became more flexible, I wanted users to manage their categories without editing files manually.

I added a dedicated **Manage Categories** window with the ability to:

- Add new categories.
- Rename existing categories.
- Delete categories.
- Add and delete descriptions.
- Rename descriptions.
- Move descriptions between categories.

This also introduced a more organized relationship between categories and descriptions. For example, a description such as "Restaurant" belongs to "Food", while "Bus Ticket" belongs to "Transport".

During testing, I encountered problems with dialog windows appearing behind the main application and selections disappearing from the description list. I refined the window's dialog handling and list-selection logic so that the management operations behaved more consistently.

### 6. Organizing local data storage

The original application stored its files in the Downloads folder. This worked, but it was not ideal for a project intended to be maintained in a GitHub repository.

I changed the file setup to use `pathlib` and the location of the Python script:

```python
BASE_DIR = Path(__file__).parent
DATA_DIR = BASE_DIR / "data"
DATA_DIR.mkdir(exist_ok=True)

csv_file = DATA_DIR / "expenses.csv"
categories_file = DATA_DIR / "categories.json"
```

The application now creates a `data/` directory beside the program automatically.

This keeps the expense records and category settings together with the application, rather than relying on a fixed location in the user's home directory.

## Main Features

The finished application includes:

- Adding expenses with dates, categories, descriptions, and amounts.
- Editable category and description dropdown menus.
- Automatic saving and chronological sorting of expense records.
- A table displaying all recorded expenses.
- Detailed summaries by month, year, category, and description.
- Combined summaries by category and month or year.
- Sorting options for category and description totals.
- A category management window for editing categories and descriptions.
- Local CSV and JSON storage.

## Technologies Used

**Python** — the main programming language used for the application's logic.

**Tkinter and ttk** — used to create the desktop interface, input fields, dropdown menus, tables, tabs, dialogs, and additional windows.

**Pandas** — used to load and save expense records, process dates and amounts, sort records, and calculate grouped spending totals.

**JSON** — used to store customizable categories and their associated descriptions.

**Pathlib** — used to manage file paths and create the application's local data directory.

## How the Application Works

### Loading and saving expenses

The `load_expenses()` function reads the CSV file into a Pandas DataFrame. It converts the date column into datetime values and the amount column into numeric values.

The `save_expenses()` function prepares the data, rounds monetary amounts to two decimal places, sorts records by date, and writes the updated DataFrame back to CSV.

When a user adds an expense, the application creates a new row, combines it with the existing records, and saves the updated data.

### Managing categories

The application uses a dictionary to represent the relationship between categories and descriptions.

The `load_categories()` function reads this information from `categories.json`. If the file does not exist, the application creates it using the default categories.

The `save_categories()` function writes changes back to JSON, allowing customized categories and descriptions to remain available between sessions.

### Calculating summaries

Pandas grouping operations calculate totals across different dimensions.

For example, grouping records by month produces monthly totals, while grouping by category shows how much was spent in each category.

The application uses these results to populate tables in the summary window. Separate functions prepare the category and description summaries so that their values can be displayed and sorted correctly.

### Building the interface

Tkinter handles the application's windows and user interactions. Functions connected to buttons, dropdown events, and dialogs perform the different operations.

The main window is used to enter expenses and access the application's features. Additional windows display expense records, detailed summaries, and category management tools.

## Project Structure

The repository is organized as follows:

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

The application creates the `data/` directory and its files when needed. For a public portfolio, fictional sample expenses are preferable to personal financial records.

## Challenges and Lessons Learned

This project taught me that developing a useful application involves much more than implementing its initial requirements.

The development process included improving the user interface, organizing related data, handling dates and monetary values, debugging Pandas operations, and refining interactions between multiple Tkinter windows.

I also learned the importance of separating different types of information. CSV provides a straightforward way to store expense records, while JSON is suitable for the category and description configuration.

Testing was an important part of the process. Some features worked individually but needed further adjustments when combined with the rest of the application. Debugging the summary tabs and category management window helped me understand the importance of checking how data and GUI events interact.

## Limitations and Future Improvements

Although the application covers the main functions of a basic expense tracker, several improvements are possible:

- Add charts showing spending patterns over time and by category.
- Introduce monthly budgets and remaining-balance tracking.
- Add filtering by date range, category, or description.
- Export summaries to Excel or PDF.
- Make the currency configurable.
- Improve validation and error handling for damaged or unexpected data files.
- Add backup and restore functionality.

These improvements could make the application more convenient and reliable.

## AI-Assisted Development

AI tools were used during parts of the development process to explore implementation approaches, understand unfamiliar functions, troubleshoot errors, and improve the documentation.

The suggestions were reviewed and tested rather than treated as automatically correct. The debugging process was particularly useful for learning how to investigate errors, understand Pandas data structures, and refine Tkinter interactions.

Being able to explain the code, verify its behavior, and recognize its limitations remains an important part of developing programming skills.

## Conclusion

The Expense Tracker evolved from a simple CSV-based exercise into a more complete desktop application.

It combines Tkinter for the graphical interface, Pandas for data processing and analysis, CSV for expense records, and JSON for customizable categories.

The most valuable part of the project was the iterative development process: starting with a small working program, identifying practical limitations, adding features, testing them, and correcting problems along the way.

It provided practical experience in turning a simple programming task into a structured application that can be maintained and improved over time.
