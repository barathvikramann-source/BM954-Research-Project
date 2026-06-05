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





