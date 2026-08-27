# SQL-Optimiser  
### Natural-Language SQL Agent for NHS Contract Analytics

SQL-Optimiser is a natural-language agent that converts plain English prompts into validated SQL, safe synthetic-DB test runs, and polished Excel-ready analytical outputs.  
It is purpose-built for NHS contract performance, KPI compliance, turnaround-time analysis, and pricing/costing analytics.

---

## Table of Contents
- [Features](#features)
- [Architecture](#architecture)
- [Memory System](#memory-system)
- [Eval Suite](#eval-suite)
- [Vector Database](#vector-database)
- [MCP Tool Orchestration](#mcp-tool-orchestration)
- [Project Structure](#project-structure)

---

## Features

### Natural-Language -> SQL
The agent interprets prompts such as:

> "Show monthly billable activity and cost for ENHT in Y1."

It generates SQL with:
- mandatory filters  
- correct table selection  
- correct joins  
- correct grouping  
- correct ordering  
- clarifying questions when required  

### Excel-First Reporting
This ensures outputs are immediately usable for operational reporting, contract performance reviews, and senior leadership briefings.  
Every CSV is transformed into a polished Excel workbook containing:
- summary table (always)  
- raw SQL output  
- optional charts  
- optional narrative  
- optional methodology  
- optional assumptions  
- optional key findings  

**Formatting rules:**
- Costs: `£#,##0.00;[Red]-£#,##0.00`  
- Activity: `#,##0`  
- TAT: minutes or hours  
- Header colour: `#A6C9EC`  
- Borders: full borders + thick outer border  

### Synthetic WH_Staging
A safe, realistic test environment including:
- CombinedData  
- BHI_BT_MB_Calc  
- KPI view  
- pricing tables  
- contract year tables  
- location maps  
- test code maps  

---

## Architecture

SQL-Optimiser follows a modular, agent-based architecture designed for clarity, extensibility, and reliable analytical output. Each stage of the pipeline is isolated into a dedicated component, enabling controlled reasoning, deterministic SQL generation, retrieval-augmented behaviour, and structured reporting.

### 1. Natural-Language Processing (NLP)
Interprets user prompts and extracts analytical intent.

Responsibilities:
- tokenisation  
- named-entity recognition (NER)  
- intent classification  
- ambiguity detection  
- extraction of KPI, date ranges, organisations, metrics, filters  

### 2. Semantic Planner
Converts interpreted intent into a formal query plan.

Determines:
- required tables  
- join paths  
- mandatory filters  
- grouping and aggregation rules  
- output schema  

### 3. SQL Generator
Transforms the semantic plan into executable SQL using:
- template-driven generation  
- strict join rules  
- KPI-specific logic  
- deterministic output  

### 4. Synthetic Database Layer
SQL executes against a safe WH_Staging environment mirroring NHS contract datasets:
- CombinedData  
- KPI views  
- pricing tables  
- contract year tables  
- location/test-code maps  

### 5. Report Generator
Converts SQL output into polished analytical artefacts:
- Excel workbooks  
- summary tables  
- charts  
- narrative  
- methodology  
- assumptions  
- key findings  

### 6. Memory System
Three memory types influence agent behaviour:
- structural memory  
- preference memory  
- error memory  

### 7. Eval Suite
Validates the agent across:
- routing  
- SQL correctness  
- clarifications  
- table selection  
- KPI logic  
- report formatting  
- correction behaviour  

### 8. Vector Database
The vector database acts as long-term experiential memory, complementing the structured rule-based memory system. It provides retrieval-augmented reasoning and long-term contextual intelligence.

Stores:
- past prompts  
- past SQL  
- past corrections  
- past clarifications  
- past reports  

Used to:
- improve routing  
- reduce repeated mistakes  
- enhance SQL template selection  
- provide contextual memory for complex queries  

### 9. MCP Tool Orchestration
MCP enables SQL-Optimiser to operate as a multi-tool agent, making it compatible with modern orchestration frameworks and external automation pipelines.

Tools include:
- NLP Tool  
- Planner Tool  
- SQL Tool  
- Report Tool  
- Memory Tool  
- Eval Tool  
- Vector Retrieval Tool  

---

## Memory System
Three memory types ensure consistent, adaptive behaviour:

- **Structural memory** — rules for tables, joins, filters  
- **Preference memory** — formatting, ordering, style  
- **Error memory** — past mistakes + corrections  

Corrections influence future behaviour without overfitting.

---

## Eval Suite
Seven evaluation categories:
- routing  
- SQL correctness  
- clarifications  
- table selection  
- KPI logic  
- report formatting  
- correction behaviour  

---

## Vector Database
The vector database is a core component of SQL-Optimiser, enabling retrieval-augmented reasoning.

It stores:
- past prompts  
- past SQL  
- past corrections  
- past clarifications  
- past reports  

This allows the agent to:
- reuse patterns  
- avoid repeated mistakes  
- improve SQL generation  
- enhance clarifications  
- strengthen domain-specific reasoning  

---

## MCP Tool Orchestration
MCP tools expose each subsystem for external orchestration:

- NLP Tool  
- Planner Tool  
- SQL Tool  
- Report Tool  
- Memory Tool  
- Eval Tool  
- Vector Retrieval Tool  

This enables:
- multi-agent workflows  
- tool-calling architectures  
- integration with external systems  
- modular execution pipelines  

---

## Project Structure

The repository is organised into clear, modular components to support maintainability, extensibility, and production-grade agent behaviour.

```text
sql-optimiser/
│
├── agent/
│   ├── nlp/
│   │   ├── tokenizer.py
│   │   ├── ner.py
│   │   ├── intent_classifier.py
│   │   └── ambiguity_detector.py
│   │
│   ├── planner/
│   │   └── semantic_planner.py
│   │
│   ├── sql_generator/
│   │   ├── templates/
│   │   │   ├── activity.sql.txt
│   │   │   ├── tat.sql.txt
│   │   │   └── kpi.sql.txt
│   │   └── sql_generator.py
│   │
│   ├── report_generator/
│   │   ├── excel_formatter.py
│   │   ├── chart_builder.py
│   │   ├── narrative_builder.py
│   │   └── report_generator.py
│   │
│   ├── memory/
│   │   ├── structural_memory.json
│   │   ├── error_memory.json
│   │   └── preference_memory.json
│   │
│   └── correction_loop.py
│
├── config/
│   ├── schema_metadata.yaml
│   ├── routing_rules.yaml
│   └── domain_values.yaml
│
├── data/
│   ├── synthetic/
│   │   ├── create_dummy_db.sql
│   │   └── seed_values.sql
│   └── examples/
│       └── example_prompts.md
│
├── evals/
│   ├── routing_evals.yaml
│   ├── sql_correctness_evals.yaml
│   ├── clarification_evals.yaml
│   ├── table_selection_evals.yaml
│   ├── kpi_evals.yaml
│   ├── report_evals.yaml
│   ├── correction_evals.yaml
│   └── run_evals.py
│
├── scripts/
│   ├── run_agent.py
│   ├── run_on_csv.py
│   └── demo.ipynb
│
└── docs/
    ├── README.md
    ├── architecture.md
    ├── synthetic_db_schema.md
    ├── evals_overview.md
    ├── memory_design.md
    └── extending_the_agent.md
