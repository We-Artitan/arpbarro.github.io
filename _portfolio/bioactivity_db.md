---
title: "Plant Bioactivity & Molecules DB"
excerpt: "A PySide6 desktop app to compile, cross-reference and explore plant bioactivity data from the scientific literature.<br/><img src='/images/bioactivity_db.png'>"
collection: portfolio
---

![Plant Bioactivity & Molecules DB — dashboard](/images/bioactivity_db.png)

## What it is

**Plant Bioactivity Database** (codename: plant_bioactivity_project) is a desktop application I built in PySide6 to support my PhD research on natural products. It lets me compile, organize and explore bioactivity data on medicinal plants from the scientific literature, with full traceability back to the original references.

At the time of writing, the database holds **133 studies** (115 fully encoded), 9 experiments and 1 molecule — and is growing as my literature review progresses.

## Why I built it

Reviewing the literature on plant bioactivity quickly becomes overwhelming: each article reports multiple experiments (different extracts, solvents, bioactivities, organisms tested, IC50 values...), with cross-references between plants, molecules and biological targets. Spreadsheets stop scaling fast, and existing tools either flatten this complexity or hide it behind a generic CRUD interface.
The app encodes a simple workflow I needed:

> **Étude → Mesures** — one study (the article header) carries *N* measurements (one per activity / target / parameter / result row).

The goal was simple: entering six measurements across six bacterial strains for one article should take roughly **three minutes**, not thirty.

## How it works

The app is organized around five sections, navigable from a collapsible sidebar:

- **Accueil** : a dashboard with key statistics and quick shortcuts
- **Saisie** : structured data entry across multiple linked tabs (study, source, extracts, experiments, molecules)
- **Consultation** : a pivot-table-style explorer where I check the columns I want to see, apply value filters (categorical or numeric thresholds), and export to Excel
- **Analyse** : visualizations and computed statistics across studies
-  **Administration** : controlled vocabularies, integrity checks, backups
Under the hood it uses a relational schema (around 30 entities: studies, plants, extracts, targets, mechanisms, methods, parameters…), with custom fields available for the dimensions I didn't anticipate.

![Plant Bioactivity & Molecules DB — study entry view](/images/bioactivity_db-saisie.png)

Each study row also carries a **reliability score** (built on a fiability checker), so I can tell at a glance which references are robust enough to base conclusions on.

## Status

Currently a personal research tool, local-only, no public repository yet. I'm using it to build the structured dataset that backs my thesis. This was partly vibe-coded to save time. A Streamlit web-based cleaned-up release may follow once the schema stabilises.