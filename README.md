# SENTINEL – Data Processing

## Project Overview

This project covers loading and analysing SENTINEL data, performing data quality checks and generating six derived transaction features using historical data to prevent future leakage. It also includes assigning fraud reason codes, velocity and high-risk MCC flags and comparing locally calculated features with the provided Supabase features table to evaluate match rates and investigate discrepancies.

## Project Structure

```text
SENTINEL/
│
├── .env
├── .gitignore
├── requirements.txt
├── sentinel_data_processing.ipynb
└── README.md
```

## Setup Steps

### 1. Clone the Repository

```bash
git clone <repository-url>
cd <repository-folder>
```

### 2. Create a Virtual Environment

Create a separate Python virtual environment for this project.

```bash
python -m venv sentinelenv
```

### 3. Activate the Environment

**Windows (Command Prompt):**

```bash
sentinelenv\Scripts\activate
```

### 4. Install Dependencies

Install all required Python packages using the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

### 5. Configure Environment Variables

Create a `.env` file in the project root directory and add the required Supabase credentials.

```env
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key
```

Replace the placeholder values with your actual credentials.

**Note:** Keep your `.env` file private. Do not upload database credentials or secrets to GitHub.

### 6. Start Jupyter Notebook

Launch Jupyter Notebook:
Alternatively, open the project folder in VS Code and select the `sentinelenv` Python interpreter.

## How to Run

1. Activate the virtual environment.
2. Ensure all dependencies are installed.
3. Verify that the `.env` file contains valid Supabase credentials.
4. Open `sentinel_data_processing.ipynb`.
5. Select the `sentinelenv` kernel in Jupyter Notebook.
6. Run the notebook cells sequentially from top to bottom.

## Data Quality Check and Feature Engineering

Performed data quality checks covers checking dataset dimensions, column names and data types. Validates actual versus expected data types, generates null-value reports, checks duplicate IDs and complete duplicate rows, identifies numerical outliers and verifies dataset splits (warmup, train, validation and holdout) with corresponding row counts.

The notebook calculates the following six derived features:

1. `amount_to_avg_ratio_derived` – Transaction amount compared with the customer's previous 90-day average.
2. `is_new_device_derived` – Identifies devices not previously used by the customer within 90 days.
3. `customer_merchant_distance_km_derived` – Calculates the geographical distance between customer and merchant using the Haversine formula.
4. `is_night_derived` – Identifies transactions occurring between midnight and 5 AM (IST).
5. `transaction_count_last_1_hour_derived` – Counts previous transactions made by the customer within one hour.
6. `transaction_amount_last_24_hours_derived` – Calculates the customer's previous transaction amount over 24 hours.

All features are calculated using information available before each transaction to prevent future data leakage.

## Important Notes

- The original transaction data is kept unchanged.
- Derived features are stored separately.
- Database credentials are managed through environment variables.
- The virtual environment should not be committed to GitHub.
- The `.gitignore` file excludes sensitive and unnecessary files.

