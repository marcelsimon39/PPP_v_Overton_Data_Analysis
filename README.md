## Comparison of the PPP and Overton's Peatland Policy Coverage

This repository contains the analysis of the [Peatland Policy Portal](https://peatlandpolicyportal.eu)'s coverage of peatland policies against that of [Overton](https://overton.io).

These analyses were conducted as part of the paper: [The European Peatland Policy Portal: Demonstrating Machine Learning and Analytics Tools for Evidence-based Land Use Policymaking](https://doi.org/10.12688/openreseurope.23501.1).

### Python Script Explanation
A Python script designed to perform a high-confidence, quantitative comparison between the Peatland Policy Portal (PPP) and the Overton policy databases. The primary goal is to determine the percentage of overlap and analyze the nature of that overlap across different policy levels (National, Regional, Local).

- Project Objective
- Core Features
- System Requirements
- Installation
- Usage
- Code Structure
- Output Description
- License

#### Project Objective

This script automates the process of cross-referencing two distinct policy datasets to identify matching documents. It was engineered to overcome common data quality issues such as inconsistent naming conventions, language barriers, and formatting errors, ensuring the final analysis is both accurate and defensible.

#### Core Features

- High-Precision Matching: Implements a reciprocal best match algorithm. A match is only confirmed if two policy titles are mutually each other's best match, virtually eliminating false positives from asymmetrical comparisons.
- Fuzzy String Comparison: Uses thefuzz with a calibrated 95% similarity threshold to account for minor variations in titles while maintaining high precision.
- Multilingual Support: Employs a two-pass matching strategy, first attempting to match using a policy's English title and then its native-language title, maximizing coverage for non-English speaking countries.
- Data Normalization: Includes a robust function to consolidate country subdivisions (e.g., mapping Germany: Bavaria to Germany), ensuring accurate country-level aggregation.
- Flexible Search Scope: Intelligently searches for matches within a policy's specific country and within a broader EU category in the Overton dataset.
- Clear & Actionable Output: Generates two distinct, easy-to-interpret CSV files summarizing the results by policy level and by country.

#### System Requirements
- Python 3.7+
- pandas
- thefuzz
- python-Levenshtein (recommended for performance)
- tqdm

#### Installation

1. Clone the repository:

bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

2. Install the required Python libraries:

bash

pip install pandas thefuzz python-Levenshtein tqdm
Note: The python-Levenshtein library is not strictly required by thefuzz but provides a significant C-based performance boost for string distance calculations.

#### Usage

1. Configure Paths: Open the script and update the file path constants at the top to point to your local datasets.

python

# --- V9 FINAL CONFIGURATION ---
ODOO_NEW_PATH = '/path/to/your/Odoo data NEW.csv'
OVERTON_NEW_PATH = '/path/to/your/Overton data NEW.csv'
FINAL_OUTPUT_PATH_SUMMARY = '/path/to/your/output/ppp_overton_level_summary.csv'
FINAL_OUTPUT_PATH_DETAILS = '/path/to/your/output/ppp_overton_level_details.csv'

2. Execute the Script: Run the script from your terminal.

bash

python your_script_name.py
The script will display a progress bar and print the final summary tables to the console upon completion.

#### Code Structure
The script is organized into modular functions for clarity and maintainability.

Function	Description
consolidate_overton_country()	Takes a string from the Overton Source country column and returns a standardized parent country name (e.g., "UK: Scotland" -> "United Kingdom").
attempt_reciprocal_match()	The core matching engine. Takes a PPP title and a list of Overton titles and returns a confirmed match only if the reciprocal best-match condition is met at the required threshold.
main()	The main orchestrator function. It handles data loading, preparation, iterates through the PPP dataset, calls the matching functions, aggregates the results, and saves the final output files.

#### Output Description

The analysis generates two primary CSV files:

ppp_overton_level_summary.csv: Provides a high-level overview of the match results, aggregated by the policy's territorial level. | ppp_level | Match | No Match | Total | Match_Percentage | | :--- | :--- | :--- | :--- | :--- | | National | 53 | 344 | 397 | 13.35 | | Regional | 12 | 98 | 110 | 10.91 | | Local | 1 | 32 | 33 | 3.03 |

ppp_overton_level_details.csv: Provides a granular breakdown of match results for each country. | ppp_country | Match | No Match | Total | Match_Percentage | | :--- | :--- | :--- | :--- | :--- | | United Kingdom | 14 | 15 | 29 | 48.28 | | Germany | 8 | 58 | 66 | 12.12 | | Ireland | 12 | 23 | 35 | 34.29 |

#### License

This project is licensed under the MIT License. See the LICENSE file for details.