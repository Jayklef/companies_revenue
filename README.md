# US Companies Data Scraper 🕷️📊

A lightweight Python web scraping project that extracts data on the largest and most profitable companies in the United States directly from Wikipedia. The project handles data extraction, structural parsing, cleaning, and exports the structured data into isolated, analysis-ready CSV files.

## 🚀 Features
* **Automated Data Extraction**: Utilizes `requests` with custom browser headers to safely fetch live Wikipedia tables.
* **HTML Parsing**: Employs `BeautifulSoup` to target and navigate specific tabular data fields (`<tr>`, `<th>`, `<td>`).
* **Data Transformation**: Uses `pandas` to clean whitespace strings, safely parse mismatched tables, and split complex columns (e.g., separating `Headquarters` into clean `City` and `State` fields).
* **Storage Ready**: Saves the formatted results into three isolated, relational `.csv` files.

## 📁 Repository Structure
```text
companies/
│
├── .gitignore                      # Prevents tracking of environments & CSV data
├── README.md                       # Project documentation
├── companies_by_revenue.csv        # Output: Top 100 public companies
├── private_companies_by_revenue.csv # Output: Top 10 private companies
├── companies_by_profit.csv         # Output: Top 10 most profitable companies
└── scraper_notebook.ipynb          # Jupyter Notebook containing the scraper pipeline
```

## 🛠️ Tech Stack & Dependencies
* **Python 3**
* **Requests** (v2.x+) — For managing HTTP network connections
* **BeautifulSoup4** (v4.x+) — For traversing raw web layouts
* **Pandas** (v2.x+) — For tabular engineering and data sanitization
* **lxml / html.parser** — Underlying page markup translation engines

## 💻 Setup & Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com
   cd companies
   ```

2. **Ensure your environment is active (Conda or Venv):**
   ```bash
   # If using Anaconda/Miniconda:
   conda install requests beautifulsoup4 pandas lxml
   
   # Or using standard pip:
   pip install requests beautifulsoup4 pandas lxml
   ```

3. **Launch the environment workspace:**
   ```bash
   # Launch VS Code directly inside the project root
   code .
   ```

## 📊 Pipeline Logic
The code maps out data pipelines over three specific target layouts from the [List of largest companies in the United States by revenue](https://wikipedia.org) Wikipedia entry:

1. **Top Public Corporations:** Pulls the primary 100-row tabular grid.
2. **Top Private Giants:** Targets the secondary list using custom looping logic to handle structure variations safely.
3. **Top Profit Generators:** Isolates high-margin businesses based on financial attributes.

Every target pipeline incorporates an validation gate (`len(row_cells) == len(table_header)`) to prevent cross-contamination from adjacent sidebars or footnotes, ensuring complete data consistency.