# 100 Days of Data Engineering

![GitHub last commit](https://img.shields.io/github/last-commit/ali-hegazy-ai/100-days-of-data-engineering)
![GitHub repo size](https://img.shields.io/github/repo-size/ali-hegazy-ai/100-days-of-data-engineering)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![SQL](https://img.shields.io/badge/SQL-PostgreSQL-blue.svg)

This repository documents my 100 day learning journey into Data Engineering. It is both a personal study log and a public learning resource for anyone who wants to follow the same path or explore core data engineering concepts in a structured way. The material follows three DataCamp career tracks and includes daily notes, exercises, code samples, and small projects.

---

## Table of Contents

- [DataCamp Tracks Used](#datacamp-tracks-used)
- [Purpose](#purpose)
- [What is in This Repository](#what-is-in-this-repository)
- [Suggested Directory Structure](#suggested-directory-structure)
- [Progress Tracker](#progress-tracker)
- [How to Use This Repository](#how-to-use-this-repository)
- [Cloning This Repository](#cloning-this-repository)
- [Contributing](#contributing)
- [License](#license)

---

## DataCamp Tracks Used

| Track | Link |
|-------|------|
| Associate Data Engineer in SQL | [View on DataCamp](https://app.datacamp.com/learn/career-tracks/associate-data-engineer-in-sql) |
| Data Engineer in Python | [View on DataCamp](https://app.datacamp.com/learn/career-tracks/data-engineer-in-python) |
| Professional Data Engineer | [View on DataCamp](https://app.datacamp.com/learn/career-tracks/professional-data-engineer) |

---

## Purpose

- Record what I learn each day with notes and examples.
- Convert course material into reusable reference notes and small projects.
- Provide a public, transparent resource that other learners can read, clone, or adapt.

> **Note:** This is not a polished tutorial. It is a working log that records definitions, code, experiments, mistakes, and corrections as I move from fundamentals to more advanced workflows.

---

## What is in This Repository

- Daily notes and study summaries in markdown
- Concept explanations and terminology lists
- SQL and Python practice files and snippets
- Small project folders and example pipelines
- References, links, and external resources
- A progress tracker for the three DataCamp tracks

---

## Suggested Directory Structure

```
100-days-of-data-engineering/
├── README.md
├── progress_tracker.md
├── associate-data-engineer-sql/
│   ├── 01-understanding-data-engineering.md
│   ├── 02-introduction-to-sql.md
│   ├── 03-intermediate-sql.md
│   ├── 04-joining-data.md
│   ├── 05-database-design.md
│   └── notes/
├── data-engineer-python/
│   ├── 01-python-foundations.md
│   ├── 02-data-ingestion.md
│   ├── 03-etl-workflows.md
│   ├── 04-automation.md
│   └── notes/
├── professional-data-engineer/
│   ├── 01-advanced-pipelines.md
│   ├── 02-orchestration.md
│   ├── 03-nosql-and-storage.md
│   ├── 04-dbt-transformations.md
│   └── notes/
├── projects/
│   ├── pipeline-project-1/
│   └── warehouse-model-project/
└── resources/
    ├── references.md
    └── links.md
```

---

## Progress Tracker

### Associate Data Engineer in SQL

- [ ] Understanding Data Engineering
- [ ] Introduction to SQL
- [ ] Intermediate SQL
- [ ] Joining Data in SQL
- [ ] Database Design
- [ ] Data Warehousing Concepts
- [ ] Additional practice and notes

### Data Engineer in Python

- [ ] Python foundations for data engineering
- [ ] Data ingestion and cleaning with Python
- [ ] Building ETL workflows
- [ ] Automation and scheduling basics
- [ ] Introduction to orchestration tools
- [ ] Additional practice and notes

### Professional Data Engineer

- [ ] Advanced pipeline patterns and design
- [ ] Scheduling and monitoring
- [ ] Distributed processing concepts
- [ ] Cloud data warehouses and storage
- [ ] dbt and transformation workflows
- [ ] DevOps, containerization, and CI/CD basics
- [ ] Performance, testing, and observability
- [ ] Capstone project work or final review

---

## How to Use This Repository

1. Open the folder that matches the track you are working on.
2. Add a daily note for the current date.
3. Update the progress tracker regularly.
4. Commit and push your changes to GitHub if you are tracking progress.
5. Add supporting project files in the `projects` directory as needed.

---

## Cloning This Repository

Anyone can clone this repository and use it locally. You will need Git installed and a terminal such as Command Prompt, PowerShell, Terminal, or bash.

### Step 1: Check if Git is installed

```bash
git --version
```

### Step 2: Install Git if needed

**Windows:**
- Download installer from: https://git-scm.com/download/win

**macOS:**
```bash
xcode-select --install
```
or
```bash
brew install git
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt install git
```

**Linux (Fedora):**
```bash
sudo dnf install git
```

**Linux (Arch):**
```bash
sudo pacman -S git
```

### Step 3: Clone the repository

```bash
git clone https://github.com/ali-hegazy-ai/100-days-of-data-engineering.git

cd 100-days-of-data-engineering
```

### Step 4: Pull updates later if needed

```bash
git pull origin main
```
or
```bash
git pull origin master
```

---

## Contributing

Contributions are welcome! If you would like to improve this repository:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/improvement`)
3. Make your changes
4. Commit your changes (`git commit -m 'Add some improvement'`)
5. Push to the branch (`git push origin feature/improvement`)
6. Open a Pull Request

---

## Suggested Additional Content

Here are some topics and resources to consider adding as you progress:

### Associate Data Engineer in SQL Track
- **Data Warehousing Concepts** - Star schema, snowflake schema, fact and dimension tables
- **SQL Performance Optimization** - Query optimization, indexing strategies, EXPLAIN plans
- **Window Functions** - RANK, ROW_NUMBER, LAG, LEAD, partitioning

### Data Engineer in Python Track
- **Pandas Deep Dive** - Advanced data manipulation techniques
- **Apache Spark with PySpark** - Distributed data processing
- **Testing Data Pipelines** - pytest, data validation, unit testing

### Professional Data Engineer Track
- **Streaming Data** - Apache Kafka, real-time processing patterns
- **Data Quality Frameworks** - Great Expectations, data contracts
- **Infrastructure as Code** - Terraform, Docker for data engineering
- **CI/CD for Data Pipelines** - GitHub Actions, dbt Cloud, automated testing

### Projects to Consider
- **Real-time Dashboard Pipeline** - Kafka → Spark → PostgreSQL → Dashboard
- **Data Lake Implementation** - S3/GCS with Delta Lake or Apache Iceberg
- **ML Feature Store** - Building a feature engineering pipeline
- **Log Analytics Pipeline** - ELK stack or similar for log processing

### Certifications to Pursue
- Google Cloud Professional Data Engineer
- AWS Certified Data Analytics Specialty
- Databricks Certified Data Engineer Associate

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <strong>Happy Learning!</strong><br>
  Made with dedication by <a href="https://github.com/ali-hegazy-ai">Ali Hegazy</a>
</p>
