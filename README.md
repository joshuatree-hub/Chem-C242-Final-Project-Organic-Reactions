# Chem C242 Final Project — Organic Reaction Modeling with GNNs + Transformers

## Overview

This project develops a **two-stage machine learning pipeline** for modeling chemical reactions:

- **Stage 1 (GNN):** Learn molecular representations from structure using quantum chemistry targets  
- **Stage 2 (Transformer):** Classify reaction types from SMILES, optionally augmented with GNN-derived features  

The central question is whether **structure-informed embeddings improve reaction classification** beyond SMILES alone.

---

## Repository Structure

- **Collected Data Processed/**
  - uspto_50k_processed.csv

- **gnn_and_transformer_development/**
  - gnn_and_transformer_final_draft.ipynb

- **README.md**

- **.gitignore**

---

## Datasets

### USPTO-50K (Reactions)
- Reaction dataset used for classification
- Processed into structured reactant → product format

### Alchemy Dataset (Molecules)
- Quantum chemistry dataset used to train GNN
- Targets include:
  - HOMO/LUMO energies
  - Dipole moment
  - Polarizability
  - Heat capacity and thermodynamic quantities

---

## Methodology

### 1. Graph Neural Network (GNN)

- Built with PyTorch Geometric  
- Uses atom- and bond-level features (RDKit-based)  
- Message passing (GINEConv) → global pooling → regression head  
- Outputs **fixed-length molecular embeddings**

---

### 2. Transformer Classifier

- Custom SMILES tokenizer with special tokens:
  - `[RMOL]`, `[PMOL]`, `[RGNN]`, `[PGNN]`, `[SEP]`

- Two configurations:
  - **SMILES-only**
  - **SMILES + injected GNN embeddings**

- Architecture:
  - Token embedding + positional encoding  
  - Transformer encoder  
  - Mean pooling + MLP classifier  

---

## Reaction Classes (Consolidated into 5)

- **Class 1:** Heteroatom alkylation & arylation  
- **Class 2:** Acylation  
- **Class 3:** C–C bond formation  
- **Class 4:** Heterocycles + Protection/Deprotection  
- **Class 5:** Redox + Functional Group Interconversion/Additions  

---

## Key Idea

Evaluate whether:

> Learned molecular properties (GNN) improve reaction classification (Transformer)

---

## Repository Design Choices

Large intermediate files were intentionally excluded:

- *.pt  
- *.pkl  
- cached_data/  
- checkpoints/  

**Reason:**
- GitHub enforces a 100 MB file limit  
- Raw datasets and model checkpoints can exceed 1 GB  

---

## Reproducibility

To reproduce results:

1. Construct molecular graphs (RDKit featurization)  
2. Train GNN on Alchemy dataset  
3. Generate molecular embeddings  
4. Train Transformer (with and without GNN features)  
5. Evaluate classification performance  

---

## Dependencies

- PyTorch  
- PyTorch Geometric  
- RDKit  
- scikit-learn  

---

## Data Access

Full datasets and intermediate artifacts are not included due to size constraints.

To request access, email:

**joshua_tree@berkley.edu**

---

## Author

Chemical Engineering & Applied Mathematics  
University of California, Berkeley  

Focus:
- Machine learning for chemistry  
- Molecular representation learning  
- Reaction modeling  