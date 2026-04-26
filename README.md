# Behind-the-Drop-Revenue-Customer-Analytics-for-a-Corporate-Travel-Platform
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

Workflow

Scaffold: Had Claude Code structure the full analysis (6 sections: Data Overview, Booking Trend, Cancellation, Deep Dive, Revenue, Customer Behavior) and generate initial charts.
Stress-test: Cross-checked every output against the raw data instead of accepting it.
Correct: Fixed filter logic, reframed sections, added missing breakdowns.
Extend: Built a deeper July-anomaly investigation Claude didn't surface.

Division of Labor

| Claude Code did | I did |
|---|---|
| Generated analysis scaffold | Defined what success/loss means for the business |
| Wrote SQL/pandas filters | Validated filters against raw data |
| Produced initial charts | Caught silent data drops (Car missing) |
| Drafted recommendations | Reframed weak insights, added Product and Decline month deep dive |


# 5. Analysis Structure

# 6. Key Findings 

# 7. How to Run

# 8. What I'd Do Next
