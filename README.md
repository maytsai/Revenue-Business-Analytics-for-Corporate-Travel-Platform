# Behind the Drop: Revenue Customer Analytics for a Corporate Travel Platform
Diagnosing a corporate travel platform's booking decline through demand decomposition, loss analysis, revenue  operations, and customer  segmentation. Built with DuckDB, Python, and Claude Code.

# Table of Content
1. [Project Overview](#projectoverview)
2. [Data Source](#data-source)
3. [Data Pipeline Architecture](#data-pipeline-architecture)
4. [Project Structure](#project-structure)
5. [Data Source Overview](#data-source-overview)


# 1. Project Overview
This project is based on a real-world corporate travel transaction dataset. The analysis goes beyond a standard case study to build a structured, end-to-end business investigation into booking volume and revenue decline. It also serves as my first Claude Code project — exploring how AI can augment analytical thinking rather than replace it.

# 2. Data Source
Based on a proprietary corporate travel transaction dataset from a real-world case study. The raw data is not included in this repository for confidentiality reasons. The dataset covers January–December 2018 across three booking products — Air, Hotel, and Car — with approximately 300,000 transactional records.

Data Quality: Excluded 1 revenue outlier ($100M), 20 invalid travel windows, and 23 duplicate IDs before analysis.

# 3. Tech Stack & Environment
- DuckDB: SQL analytics
- Python: data wrangling and visualization
- Anaconda: environment management
- Claude Code: AI thinking partner


# 4. How I Used AI as an Enabler
Tool: Claude Code (Anaconda environment)
Role: First-pass analyst — I drove framing, validation, and final insight.

#### Workflow

**Scaffold:** Had Claude Code structure the full analysis (e.g. Data Overview, Booking Trend, Cancellation) and generate initial charts.

**Stress-test:** Cross-checked every output against the raw data instead of accepting it.

**Modification:** Fixed filter logic, reframed sections, and added missing breakdowns.

**Extend:** Built a deeper monthly and product-type investigation that Claude didn't surface.


# 5. Analysis Structure
  1. Data Overview & Quality 
  2. Booking Trend (MoM)     
  3. High-Loss Month Booking Deep Dive: July                 
  4. High-Loss Product Deep Dive: Car & Hotel
  5. Revenue Analysis        
  6. User Behavior         
  7. Key Findings & Recommendations   


# 7. How to Run

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


# 8. What I'd Do Next
