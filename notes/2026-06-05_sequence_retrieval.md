\# Lab Notes - KbpA Homologue Sequence Retrieval

\# BM954 MSc Project - MM3



\## What I did today (05-06-26)



1\. Located the query protein KbpA on UniProt using accession P0ADE6

2\. Ran BLAST search from the UniProt entry page using blastp

3\. Got 250 hits back from UniProtKB

4\. Downloaded the accession list as kbp\_blast\_accessions.txt

5\. Removed the "TR:" prefix from accessions using Notepad Find \& Replace

6\. Used UniProt ID Mapping tool to map 250 accessions to UniProtKB

7\. 248 out of 250 accessions mapped successfully

8\. Downloaded 248 sequences in FASTA format as kbp\_homologues.fasta

9\. Copied kbp\_homologues.fasta into the sequences/ folder in the repository



\## Issues encountered

\- BLAST download didn't have FASTA format directly

\- Accessions had "TR:" prefix that needed removing before ID mapping worked

\- 2 accessions failed to map (reason unknown)



\## Next steps

\- Search InterPro for more homologues

\- Find 3D structures on RCSB/PDB

\- Align sequences with MAFFT



\## Next



10\. Searched InterPro using P0ADE6

11\. Found family IPR052196 - Bacterial Potassium Binding (19k proteins, 8 reviewed)

12\. Downloaded 8 reviewed sequences as kbp\_interpro\_reviewed.fasta

13\. Copied kbp\_interpro\_reviewed.fasta into the sequences/ folder



\## Issues encountered

\- Downloaded files had double .fasta extension, renamed manually



14\. Searched RCSB/PDB using P0ADE6

15\. Found 3 experimental structures:

&#x20;   - 7PVC: Kbp.K with potassium bound, NMR, E. coli K-12 (2022)

&#x20;   - 7VCM: GINKO1 crystal structure, X-ray 1.85A, E. coli K-12 (2022)

&#x20;   - 8ZEX: HaloKbp1a biosensor, X-ray 1.66A, E. coli (2024)

16\. Downloaded all 3 as .cif files and saved to structures/ folder



\## Next



17\. Installed MAFFT (v7.526) for Windows

18\. Ran MAFFT alignment on 248 KbpA homologue sequences

&#x20;   - Command: mafft --auto --reorder kbp\_homologues.fasta

&#x20;   - Strategy: FFT-NS-i (iterative refinement)

&#x20;   - Output saved as: results/alignments/kbp\_homologues\_aligned.fasta



\## Next steps



\- Visualise alignment in JalView

\- Run MAFFT on InterPro sequences too

