# Data Processing and Analysis Project

This repository hosts a robust data processing and analysis pipeline, designed to transform raw data, validate it, and generate insightful results. The entire workflow is automated using GitHub Actions, ensuring continuous integration, code quality, and automated publication of results.

## Project Overview

The core of this project involves:
*   **Data Conversion**: Converting `.xlsx` files (specifically `data.xlsx`) into `.csv` format (`data.csv`).
*   **Data Processing**: Executing a Python script (`execute.py`) that reads the processed `.csv` data, performs analysis, and outputs structured results.
*   **Result Generation**: Producing a `result.json` file containing the processed insights.
*   **Code Quality**: Ensuring high code quality and consistency using `ruff`.
*   **Continuous Integration/Deployment**: Automating the entire process from code commit to result publication using GitHub Actions and GitHub Pages.

## Getting Started

Follow these instructions to set up the project locally.

### Prerequisites

Ensure you have the following installed:
*   Python 3.11+
*   pip (Python package installer)

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/your-repo.git
    cd your-repo
    ```

2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install dependencies:**
    ```bash
    pip install pandas ruff openpyxl
    ```
    (Note: `openpyxl` is needed for reading `.xlsx` files with pandas).

### Project Structure

```
.
├── .github/              # GitHub Actions workflows
│   └── workflows/
│       └── ci.yml        # CI/CD workflow for testing and publishing
├── data.xlsx             # Original data file (Excel format)
├── data.csv              # Converted CSV data (generated in CI or locally)
├── execute.py            # Python script for data processing
├── index.html            # Single-page responsive HTML app
├── LICENSE               # Project license
└── README.md             # This README file
```

## Usage

### 1. Data Conversion (xlsx to csv)

The `data.xlsx` file needs to be converted to `data.csv` before `execute.py` can process it. This conversion is handled automatically by the CI workflow. If you need to do it manually:

```python
import pandas as pd
df = pd.read_excel('data.xlsx')
df.to_csv('data.csv', index=False)
```

### 2. Running the Data Processor

The `execute.py` script will read `data.csv`, process it, and output `result.json`.

```bash
python execute.py > result.json
```

### 3. Viewing Results

The `result.json` file contains the output of the data processing. In the CI/CD pipeline, this `result.json` is published via GitHub Pages.

## CI/CD Workflow

The `.github/workflows/ci.yml` workflow automatically performs the following steps on every push to the repository:

1.  **Setup Environment**: Installs Python 3.11 and project dependencies.
2.  **Linting**: Runs `ruff` to check code quality and style of `execute.py`.
3.  **Data Conversion**: Converts `data.xlsx` to `data.csv`.
4.  **Execute Script**: Runs `python execute.py > result.json` to generate the `result.json` output.
5.  **Publish Results**: Uses the `actions/upload-pages-artifact` and `actions/deploy-pages` actions to publish `result.json` to GitHub Pages, making the results accessible via a web URL.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---