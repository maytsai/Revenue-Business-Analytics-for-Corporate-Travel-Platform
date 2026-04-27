# Behind the Drop: Revenue Customer Analytics for a Corporate Travel Platform
Diagnosing a corporate travel platform's booking decline through demand decomposition, loss analysis, revenue  operations, and customer  segmentation. Built with DuckDB, Python, and Claude Code.

# Table of Content 
  1. [Project Overview](#project-overview)         
  2. [Data Source](#data-source)
  3. [Tech Stack & Environment Set up](#tech-stack-and-environment-set-up)  
  4. [How I Used AI as an Enabler](#how-i-used-ai-as-an-enabler)
  5. [How to run Claude code on the Anaconda environment](#how-to-run-claude-code-on-the-anaconda-environment)      
  6. [Analysis Workflow](#analysis-workflow)
     
                    
# Project Overview
This project is based on a real-world corporate travel transaction dataset. The analysis goes beyond a standard case study to build a structured, end-to-end business investigation into booking volume and revenue decline. It also serves as my first Claude Code project, exploring how AI can augment analytical thinking rather than replace it.

# Data Source
Based on a proprietary corporate travel transaction dataset from a real-world case study. The raw data is not included in this repository for confidentiality reasons. The dataset covers January–December 2018 across three booking products — Air, Hotel, and Car — with approximately 300,000 transactional records.

Data Quality: Excluded 1 revenue outlier ($100M), 20 invalid travel windows, and 23 duplicate IDs before analysis.

# Tech Stack & Environment Set up

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

**Scaffold:**  Worked with Claude Code to brainstorm and structure the full analysis (e.g. Data Overview, Booking Trend,
  Loss Analysis) and generate initial queries and data visualizations.

**Stress-test:** Cross-checked every output against the raw data rather than accepting results at face value.

**Modification:** Fixed filter logic, reframed sections, and added missing breakdowns where the output fell short.

**Extend:** Redirected the analysis independently, building deeper monthly and product-level investigations that Claude didn't surface on its own.

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


# Analysis Workflow:
  1. Data Overview & Quality:
     
     Dataset profile, schema, and the booking-type breakdown by product (Car / Air / Hotel) — the foundation that every later section depends on.
  2. Booking Trend (MoM):
     
     Monthly booking volume and revenue by product. Surfaces the July booking volume decline and the August revenue anomaly.
  3. High-Loss Month Booking Deep Dive: July

     Diagnoses whether July's 32% volume drop was driven by a spike in booking losses or a collapse in new demand: two problems that require different interventions. 
  4. High-Loss Product Deep Dive: Car & Hotel

      Examines loss patterns for the two highest-loss products. 
  5. Revenue Analysis

     Translates monthly booking volume into revenue terms: gross revenue, loss amount, and net revenue to quantify the financial impact of down months and validate whether revenue spikes align with volume gains. 
  6. User Behavior

     Segments travelers by annual booking frequency (Frequent / Occasional / One-time) to understand who drives revenue, which tiers disappeared in July, and whether August's revenue spike reflects a real demand shift or a statistical artifact.
  7. Key Findings & Recommendations   
  
      Consolidates findings into an Act / Investigate / Watch framework, separating what is actionable now from what requires further data
      before intervention.   






