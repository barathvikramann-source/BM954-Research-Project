# BM954 MSc Project - MM3
# Genome mining and evolutionary history of potassium indicators

**Student:** Barath Vikramann Nachinarkiniyan Rajavazhuthi
**Supervisor:** Morgan Feeney
**Institution:** University of Strathclyde
**Module:** BM954 MSc Project

## Project Overview

This project investigates the genome mining and evolutionary history 
of the potassium binding protein Kbp (KbpA) from Escherichia coli. 
KbpA undergoes large conformational changes upon binding potassium 
ions, making it an excellent candidate for potassium biosensor 
development.

The project aims to:
1. Conduct a meta-analysis of potassium binding kinetics from literature
2. Survey public sequence databases for KbpA homologues
3. Investigate relationships between sequence variation, structure and function
4. Use AlphaFold to predict structures for KbpA sequence variants

## Repository Structure

- `sequences/` - KbpA homologue sequences in FASTA format
- `structures/` - 3D structure files from RCSB/PDB
- `papers/` - Reference papers and synopses
- `notes/` - Lab notes documenting all work done
- `results/` - Analysis outputs including alignments
- `scripts/` - Python scripts for data retrieval and analysis
- `data/` - Raw data and kinetics tables
- `notebooks/` - Jupyter notebooks

## Key Protein

- **Protein:** Potassium binding protein Kbp (KbpA)
- **Organism:** Escherichia coli (strain K12)
- **UniProt:** P0ADE6
- **Length:** 149 amino acids

## Progress

- [x] Obtained KbpA homologue sequences from UniProt BLAST (248 sequences)
- [x] Obtained reviewed homologues from InterPro IPR052196 (8 sequences)
- [x] Downloaded 3D structures from RCSB/PDB (7PVC, 7VCM, 8ZEX)
- [ ] Sequence alignment with MAFFT
- [ ] Alignment visualisation with JalView
- [ ] AlphaFold structure prediction
- [ ] Kinetics meta-analysis