# SCIROS — OpenAlex Query & Proximity Filtering Script

## Overview

This repository contains a Python script and an example output dataset developed within the **SCIROS project** (Strategic Collaboration for Interdisciplinary Research on Open Science in SSH).

The purpose of this repository is to support **reproducible retrieval and filtering of bibliographic records from OpenAlex**, in alignment with the methodology described in the SCIROS data paper.

Specifically, the script implements a **workaround for the lack of proximity operators in OpenAlex**, enabling results comparable to queries executed in Scopus and Web of Science.

---

## Repository Contents

The repository consists of:

- `SCIROS_openalex_api.py`  
  Python script used to query OpenAlex and perform proximity-based filtering

- `SCIROS_TOS_openalex_proximity_ALL_2025-05-22.xlsx`  
  Example output dataset generated using the script

- `.gitignore`  
  Excludes local data processing artifacts (e.g. `/data`, `__pycache__`)

No additional modules, configuration files, or documentation are included.

---

## Methodological Context

The script operationalizes a key step in the SCIROS dataset construction pipeline:

> ensuring comparability of bibliographic queries across databases with different search capabilities.

In Scopus and Web of Science, queries use proximity operators such as:

`Set C NEAR/2 (Set A NEAR/0 Set B)`


However, OpenAlex does not support proximity operators. To address this, the SCIROS workflow combines:

1. API-based retrieval (broad query)
2. Post-processing in Python (proximity filtering)

This approach is described in detail in the SCIROS data paper.

---

## What the Script Does

The script performs the following steps:

1. Defines keyword sets (A, B, C) corresponding to:
   - Open Science concepts
   - research domains and infrastructures
   - theoretical / conceptual framing

2. Queries OpenAlex API:
   - retrieves records matching combined keyword expressions
   - filters results to English-language records

3. Processes metadata:
   - extracts titles, abstracts, authors, and keywords
   - reconstructs abstract text where needed

4. Applies proximity filtering:
   - checks whether keywords from different sets occur within a defined word window
   - emulates `NEAR/x` logic used in WoS/Scopus

5. Exports results:
   - saves intermediate data locally
   - exports final dataset to Excel (`.xlsx`)

---

## Key Concept: Proximity Emulation

Instead of relying on database-native operators:

`keyword1 NEAR/2 keyword2`


the script:

- tokenizes text (title + abstract)
- calculates distances between keyword occurrences
- retains only records meeting the proximity condition

This allows OpenAlex results to approximate the precision of controlled database queries.

---

## How to Run

### Requirements

The script uses standard Python libraries (e.g. `requests`, `pandas`).  
No `requirements.txt` is provided.

### Execution

Run the script directly:

```bash
python SCIROS_openalex_api.py
```

All parameters (keywords, query structure, filtering logic) are defined inside the script.

---

## Output Data

The included Excel file:

`SCIROS_TOS_openalex_proximity_ALL_2025-05-22.xlsx`

represents:

- a filtered subset of OpenAlex records  
- aligned with SCIROS query logic  
- suitable for further integration into the full dataset pipeline  

In the broader SCIROS workflow, such data are later:

- deduplicated  
- reconciled with Scopus and Web of Science  
- transformed into composite records  

---

## Reuse Potential

This repository supports several reuse scenarios:

### 1. Reproducing OpenAlex Retrieval

- run the script as-is  
- obtain a comparable OpenAlex dataset  
- integrate results into systematic literature reviews  

---

### 2. Updating the Dataset

- rerun the script (OpenAlex is continuously updated)  
- optionally adjust query parameters in the code  

This enables longitudinal analyses.

---

### 3. Adapting to New Research Topics

To reuse the script:

- modify keyword sets (A, B, C) in the code  
- keep proximity logic unchanged  

This preserves methodological consistency across domains.

---

### 4. Supporting Bibliometric Analysis

The output dataset can be used for:

- co-authorship analysis  
- co-citation analysis  
- topic modeling  
- scientometric studies  

---

### 5. Corpus Construction

When combined with full-text collections (e.g. Zotero):

- enables corpus building  
- supports discourse and semantic analysis  

---

## Limitations

- OpenAlex abstracts may be incomplete or reconstructed  
- Proximity filtering is an approximation of database-native operators  

The script does not include:

- deduplication  
- metadata reconciliation  
- multi-database integration  

These steps belong to the broader SCIROS workflow.

---

## Relation to the SCIROS Dataset

This repository implements one stage of the full pipeline:

**OpenAlex data retrieval + proximity filtering**

The complete dataset:

- combines OpenAlex, Scopus, and Web of Science  
- includes composite records  
- is available via Zenodo (see data paper)  

---

## License

CC BY 4.0

---

## Authors

Developed within the SCIROS project by:

- Cezary Rosiński  
- Piotr Wciślik  
- Magdalena Wnuk  
- Maciej Maryl  

[Digital Humanities Centre, Institute of Literary Research, Polish Academy of Sciences](https://chc.ibl.waw.pl/)
