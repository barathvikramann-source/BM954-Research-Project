 Analysis pipeline - run order

1. 01_alignment.sh - MAFFT alignment (Section 2.2)
2. 02_trimming.sh - trimAl trimming (Section 2.3)
3. 03_phylogeny.sh - IQ-TREE model selection + inference (Section 2.4)
4. 04_structural_comparison.cxc - ChimeraX superposition (Section 2.8)

Tools were installed via conda (conda-forge and bioconda channels):
conda install iqtree
conda install trimal
conda install figtree

 Manual (GUI-based) steps not scripted above

- 2.1 Dataset retrieval: sequences retrieved manually from UniProt
  (UniRef50_P0ADE6 cluster), downloaded 29 June 2026.
- 2.2 Fragment removal: three fragment sequences (A0A4Z0QFG9, Q9F2D1,
  A0ABX2V4C1) manually removed in Jalview v2.11.5.1 before alignment.
- 2.5 - 2.5 Tree visualisation: launched with
  `figtree uniprot_aligneddd.trimal.fasta.treefile`
  Midpoint rooting, bootstrap support display, and tip relabeling
  (organism name, UniProt accession, genotype) were performed
  manually within FigTree's GUI.
- 2.6 Conservation mapping: conservation calculated in Jalview and mapped
  onto PDB 7PVC in ChimeraX v1.11.1 (GUI-based, not scripted).
- 2.7 Structure retrieval: AlphaFold models downloaded manually by UniProt
  accession from the AlphaFold Protein Structure Database (v6), 15 July 2026.

 Raw terminal log

full_terminal_log.txt contains the complete, unedited command history
from this analysis, including troubleshooting steps.
