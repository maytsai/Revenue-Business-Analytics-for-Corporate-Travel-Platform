# Behind the Drop: Revenue Customer Analytics for a Corporate Travel Platform
Diagnosing a corporate travel platform's booking decline through demand decomposition, loss analysis, revenue  operations, and customer  segmentation. Built with DuckDB, Python, and Claude Code.

# Table of Content
1. [Project Overview](#projectoverview)
2. [Data Source](#data-source)
3. [Data Pipeline Architecture](#data-pipeline-architecture)
4. [Project Structure](#project-structure)
5. [Data Source Overview](#data-source-overview)


# Project Overview
This project is based on a real-world corporate travel transaction dataset. The analysis goes beyond a standard case study to build a structured, end-to-end business investigation into booking volume and revenue decline. It also serves as my first Claude Code project, exploring how AI can augment analytical thinking rather than replace it.

# Data Source
Based on a proprietary corporate travel transaction dataset from a real-world case study. The raw data is not included in this repository for confidentiality reasons. The dataset covers January–December 2018 across three booking products — Air, Hotel, and Car — with approximately 300,000 transactional records.

Data Quality: Excluded 1 revenue outlier ($100M), 20 invalid travel windows, and 23 duplicate IDs before analysis.

# Tech Stack & Environment

#### Data Analysis: DuckDB
- DuckDB is used to run fast, in-process SQL queries directly on the local dataset without needing a database server. It enables efficient aggregation, filtering, and transformation of ~300,000 transactional records, making it well-suited for exploratory analysis in a local environment.  

#### Data Wrangling & Visualization: Python
- Python is used to clean, transform, and visualize the data. Libraries such as Pandas handle data preparation and filtering, while Matplotlib and Seaborn are used to generate charts that support the analysis across booking trends, loss patterns, and customer segmentation. 

#### Environment Management: Anaconda
- Anaconda is an environment management platform that is used to manage the Python environment, ensuring all dependencies and package versions are consistent and reproducible across sessions.

#### AI Thinking Partner: Claude Code
- Claude Code is used throughout the analysis as an AI-powered thinking partner. Rather than generating analysis autonomously, Claude is used to pressure-test analytical framing, refine recommendation logic, and surface potential blind spots — with all analytical decisions driven by independent judgment.


# How I Used AI as an Enabler
Tool: Claude Code (Anaconda environment)

#### Workflow

**Scaffold:** Had Claude Code structure the full analysis (e.g. Data Overview, Booking Trend, Cancellation) and generate initial charts.

**Stress-test:** Cross-checked every output against the raw data instead of accepting it.

**Modification:** Fixed filter logic, reframed sections, and added missing breakdowns.

**Extend:** Built a deeper monthly and product-type investigation that Claude didn't surface.

# How to run Claude code on the Anaconda environment

This project was built inside an Anaconda environment, so Claude Code is installed and launched from the Anaconda Terminal.

#### Prerequisites

- Anaconda / Miniconda installed
- Node.js and `npm` available on your `PATH`
- An Anthropic API key (or active Claude Code login)

#### Setup

**1. Open the Anaconda Terminal** (not your system's default terminal).

**2. Activate your environment:**

```bash
conda activate your_env_name
```

**3. Install Claude Code globally:**

```bash
npm install -g @anthropic-ai/claude-code
```

**4. Navigate to your project folder and launch Claude:**

```bash
cd your_project_folder
claude
```

#### Notes

- Run every command from the **Anaconda Terminal** so Claude Code inherits the active conda environment's Python and packages.
- If `claude` isn't found after install, restart the terminal or check that npm's global `bin` directory is on your `PATH`.

# Project Structure

Analysis Workflow:
  1. Data Overview & Quality:
     
     Dataset profile, schema, and the booking-type breakdown by product (Car / Air / Hotel) — the foundation that every later section depends on.
  3. Booking Trend (MoM):
     
     Monthly booking volume and revenue by product. Surfaces the July booking volume decline and the August revenue anomaly.
  5. High-Loss Month Booking Deep Dive: July
     
  7. High-Loss Product Deep Dive: Car & Hotel
  8. Revenue Analysis        
  9. User Behavior         
  10. Key Findings & Recommendations   

### Data Overview
#### Goal:
Get a high-level understanding of the dataset — record counts, date range, product mix, and booking type breakdown.

#### Analysis:
- Records by product (Air, Hotel, Car)
- Records by booking type
- Booking type breakdown by product






