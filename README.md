# Corporate Data Analyzer

A desktop GUI application that lets non-technical users analyze CSV/Excel data — build grouped reports, generate charts, and export results — without writing any code.

## Overview

Built with Tkinter for the interface and Pandas for data processing, this tool is aimed at users who need quick, repeatable summary reports and visualizations from spreadsheet data but don't want to touch Excel formulas or write scripts. Packaged as a standalone Windows executable using PyInstaller, so it runs without requiring Python to be installed.

## Features

### File Selection & Reading
- Browse and select a CSV or Excel (`.xlsx` / `.xls`) file.
- On clicking **Read**, the app displays the number of rows, number of columns, and all column headings.

### Automatic Column Type Detection
- Detects text columns (object dtype) for use as grouping fields.
- Detects numeric columns, including numeric-looking text (e.g. `"12,000"`) using a comma-stripping conversion check, so values stored as text still register as usable numeric fields.

### Report Builder
- Select a **Group By** column (text), an **Aggregation** method (Sum, Mean, Average, Max, Min, Count, Median), and a **Value** column (numeric).
- Clicking **Preview Report** cleans the group column (trims whitespace, standardizes casing), converts the value column to numeric, drops non-numeric rows, groups and aggregates the data, sorts results in descending order, and displays them in an in-app table.

### Export Report
- Export the generated report as **Excel (.xlsx)** or **CSV (.csv)**.
- The file is saved automatically as `report_output.xlsx` / `report_output.csv` in the same folder as the input file.

### Chart Builder
- Choose from **Bar, Column, Line, or Pie** charts, generated directly from the report data using Matplotlib.
- Charts display the top 10 groups by value (top 6 for pie charts, to keep labels readable).
- Clicking **Export Chart (PNG)** saves the chart as `chart_output.png` in the same folder as the input file.

### Error Handling
- Clear error messages if no file is selected, the file hasn't been read yet, or required dropdown selections are missing.
- Each report/chart generation clears previous results before rendering new ones.

## Tech Stack

- **Python 3**
- **Tkinter** — GUI framework (built into Python)
- **Pandas** — data reading, cleaning, and aggregation
- **Matplotlib** — chart rendering, embedded in the Tkinter window via `FigureCanvasTkAgg`
- **PyInstaller** — packaging into a standalone `.exe`

## Running the App

```bash
pip install -r requirements.txt
python Data_Analyzer.py
```

## Building a Standalone Executable

```bash
pip install pyinstaller
pyinstaller --onefile --windowed Data_Analyzer.py
```

The executable will be created in the `dist/` folder.


## Notes

- Numeric detection for text-stored numbers uses a heuristic: a column is treated as numeric if at least 60% of its values (or a minimum of 3) convert successfully after stripping commas.
- Exported report and chart filenames are fixed (`report_output.*`, `chart_output.png`) and will overwrite previous exports in the same folder if regenerated.
