# ETL Script: Countries by GDP

This Python script performs a simple ETL (Extract, Transform, Load) process on a list of countries and their GDP values. It pulls data from a **Wikipedia** page (via the [Wayback Machine](https://web.archive.org)), processes that data, and saves it into both a **CSV file** and a **SQLite database**. Finally, the script executes a sample SQL query on the loaded table and logs the entire process to a log file.

## Table of Contents

- [Overview](#overview)
- [Data Source](#data-source)
- [Functions](#functions)
  - [extract()](#extract)
  - [transforms()](#transforms)
  - [load_to_csv()](#load_to_csv)
  - [load_to_database()](#load_to_database)
  - [run_query()](#run_query)
  - [log_progress()](#log_progress)
- [Requirements](#requirements)
- [Usage](#usage)
- [File Descriptions](#file-descriptions)
- [Customization](#customization)
- [License](#license)
- [Contact](#contact)

---

## Overview

1. **Extract**: Scrapes the Wikipedia page (archived version) for the “List of countries by GDP (nominal)” table.  
2. **Transform**: Converts GDP values from millions to billions of USD, renaming the column accordingly.  
3. **Load**:  
   - Saves the processed data to a CSV file (`Countries_by_GDP.csv`).  
   - Stores the data in a local SQLite database (`World_Economies.db`) as a table (`Countries_by_GDP`).  
4. **Log**: Writes progress messages and timestamps to a log file (`etl_project_log.txt`).  
5. **Query**: Executes an example SQL query to fetch countries with a GDP >= 100 billion USD, printing the results.

---

## Data Source

- **URL**:  
  [Archived Wikipedia Page](https://web.archive.org/web/20230902185326/https://en.wikipedia.org/wiki/List_of_countries_by_GDP_%28nominal%29)

- **Table Content**: The script specifically extracts data from the third `<tbody>` element, which contains the relevant country names and GDP (in millions of USD).

---

## Functions

### `extract(url, table_attributes)`
- **Purpose**:  
  - Sends a GET request to the specified `url`, parses the HTML, and extracts rows containing valid country names and GDP data.
  - Returns a Pandas DataFrame with columns defined in `table_attributes` (e.g., `["Country", "GDP_USD_millions"]`).

### `transforms(df)`
- **Purpose**:  
  - Converts GDP values from strings (with commas) to floating-point numbers.
  - Transforms GDP from millions of USD to billions of USD (rounding to 2 decimal places).
  - Renames the GDP column from `GDP_USD_millions` to `GDP_USD_billions`.
  - Returns the transformed DataFrame.

### `load_to_csv(df, csv_path)`
- **Purpose**:  
  - Saves the DataFrame `df` to a CSV file at `csv_path`.

### `load_to_database(df, sql_connection, table_name)`
- **Purpose**:  
  - Saves the DataFrame `df` into the SQLite database using the provided connection.
  - If the table already exists, it is replaced.

### `run_query(query_statement, sql_connection)`
- **Purpose**:  
  - Runs the given SQL query (`query_statement`) on the open SQLite connection.
  - Prints the SQL command and the resulting query output to the terminal.

### `log_progress(message)`
- **Purpose**:  
  - Writes a timestamped message to the log file `etl_project_log.txt`.
  - Useful for tracking progress and debugging issues in the ETL pipeline.

---

## Requirements

- **Python 3.7+**
- **Libraries**:
  - [requests](https://pypi.org/project/requests/)
  - [beautifulsoup4](https://pypi.org/project/beautifulsoup4/)
  - [pandas](https://pypi.org/project/pandas/)
  - [numpy](https://pypi.org/project/numpy/)
  - [sqlite3](https://docs.python.org/3/library/sqlite3.html) (built-in with Python 3)
- **Optional** (for datetime formatting):
  - [datetime](https://docs.python.org/3/library/datetime.html) (also standard library)

A sample `requirements.txt` could look like this:

```txt
beautifulsoup4>=4.9.3
requests>=2.25.1
pandas>=1.1.5
numpy>=1.19.5
```

---

## Usage

1. **Clone or Download the Script**:

   ```bash
   git clone https://github.com/YourGitHubName/YourRepo.git
   cd YourRepo
   ```

2. **(Optional) Create a Virtual Environment**:

   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   venv\Scripts\activate     # Windows
   ```

3. **Install Required Dependencies**:

   ```bash
   pip install beautifulsoup4 requests pandas numpy
   ```

4. **Run the Script**:

   ```bash
   python etl_script.py
   ```

5. **Check Outputs**:
   - **CSV File**: `./Countries_by_GDP.csv`
   - **SQLite DB**: `World_Economies.db` (table: `Countries_by_GDP`)
   - **Log File**: `etl_project_log.txt`
   - **Terminal/Console Output**: Shows query results (countries with GDP >= 100 billion USD).

---

## File Descriptions

- **`etl_script.py`**: Main script containing all ETL functions and the workflow.  
- **`etl_project_log.txt`**: Generated/updated by the script; logs process events with timestamps.  
- **`Countries_by_GDP.csv`**: Output CSV file with the final, transformed data.  
- **`World_Economies.db`**: SQLite database containing the table `Countries_by_GDP`.

---

## Customization

1. **Changing the Source URL**:  
   - Update the `url` variable to target a different page or data source.
2. **Modifying Table Columns**:  
   - Change `table_attributes` if you want to capture additional columns (e.g., `Population`).
3. **Query Adjustments**:  
   - Edit `query_statement` to run different queries against the database (e.g., filtering by regions).
4. **Logging Details**:  
   - Adjust the `log_progress` function or its usage to log more/less detail.

---

## License

```
MIT License
...
```

---

## Contact

- **Author**: Your Name / Organization  
- **Email**: [joseph74790@gmail.com](mailto:joseph74790@gmail.com)  
- **GitHub**: [Frank Kendemah](https://github.com/YourGitHubName)

Feel free to reach out if you have questions, suggestions, or feedback regarding this ETL script.

---

*Happy Data Extraction and Analysis!*
