---
title: "Mol-Intel"
excerpt: "A desktop tool that aggregates phytochemical data from multiple databases for computational drug discovery.<br/><img src='/images/molecular-intel.png'>"
collection: portfolio
---

![Mol-Intel — home view](/images/molecular-intel.png)

## What it is

**Mol-Intel** is a desktop application (PySide6) I'm building for my PhD work on natural products. It aggregates data from ten scientific databases to enrich molecules, protein targets, and producing organisms from a single identifier, then assists with the downstream computational work: ADMET profiling, pocket detection, molecular docking, and dynamics preparation.
At the time of writing, the app connects to PubChem, ChEMBL, ChEBI, COCONUT, NPASS (molecules), UniProt, PDBe, BindingDB (targets), and LOTUS + NPAtlas (organisms), with a local SQLite database that grows as I encode my targets and screening sets.
The goal is to assist the researcher in two things:

1. **Investigating** what is already known about a compound : bioactivities, validated targets, known mechanisms
2. **Preparing and exploiting** computational analyses on those compounds: **ADMET** profiling, **molecular docking**, and **molecular dynamics**

## Why I built it

Working on the anti-quorum sensing activity, I kept rebuilding the same workflow by hand for every new molecule and every new target: search PubChem for descriptors, then ChEMBL for bioactivities, then UniProt for the protein, then PDB for a structure, then prepare a docking grid by hand. Each loop ate an afternoon and the data ended up scattered across spreadsheets and folders.
Mol-Intel turns that loop into a one-click pipeline:

- **Molecule-first**: paste an identifier → the app fans out to PubChem/ChEMBL/ChEBI/COCONUT/NPASS and consolidates everything in one row
- **Target-first**: enter a UniProt accession → sequence, functional sites, PDB structures, and top published inhibitors all come back together
- **Organism-first**: enter a plant or microbe → LOTUS and NPAtlas return every metabolite already published for that species, with bibliographic references


## How it works

The app is organized as six sections in a desktop sidebar: Home, Molecules, Database, Organisms, Analyses, Administration. Under the hood, a relational schema (21 tables: molecules, targets, organisms, pockets, screening sets, identifiers, bioactivities, references...) backs everything, with a connector layer that handles rate limiting, retries, and offline fixtures for testing.
The three useful pipelines stack naturally:

1. **Organisms → Molecules**: pick a plant, populate from LOTUS, get 50–200 published metabolites with DOIs
2. **Targets → Pockets**: pick a protein, fetch the UniProt annotations and a PDB, run FPocket to detect druggable cavities, and let the app classify each pocket as orthosteric or allosteric by cross-referencing the residues with the UniProt binding sites
3. **Both → Docking**: build a screening set from the organism's metabolites, copy a ready-made AutoDock Vina config from the pocket detail panel, and run docking externally

Each detected pocket comes with one-click exports: XYZ coordinates, full Vina config block, PyMOL selection script, and residue list.

## Status

**Working prototype.** 
Personal research tool, local-first. This was partly vibe-coded to save time. I'm currently using it to build the structured dataset that backs my thesis on computational screening. A cleaned-up open-source release will likely follow once the schema stabilizes and the docking workflow is integrated.

