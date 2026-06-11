\# BM954 MSc Project - MM3: KbpA Genome Mining

\# Lab Notebook



Student: Barathvikramann

Supervisors: Morgan Feeney, Leighton Pritchard



\---



\# 05-06-2026 - Sequence Retrieval



\## What I was trying to do today



My goal today was to collect as many KbpA homologue sequences as possible from different databases. I need a good diverse set of sequences before I can do any alignment or phylogenetic analysis.



\## Background - what is KbpA?



Before starting I read about the protein so I understood what I was looking for:



\- KbpA (also called YgaU) is a small 149 amino acid protein from E. coli

\- UniProt accession: P0ADE6

\- It binds potassium ions (K+) with high selectivity over sodium

\- It has two domains:

&#x20;   - BON domain (residues 1-89): this is where K+ actually binds

&#x20;   - LysM domain (residues 92-149): this stabilises the protein when K+ is bound

\- When K+ binds, the whole protein changes shape from a loose open structure to a compact globular shape

\- This conformational change is what makes it useful as a biosensor

\- It has been used in several fluorescent K+ biosensors: GINKO1, GINKO2, KRaION1, HaloKbp1



\---



\## Step 1: UniProt BLAST



Why I did this:

\- UniProt BLAST searches the UniProtKB database which has well-annotated sequences

\- Good starting point for finding close homologues



What I did:

1\. Went to https://www.uniprot.org/uniprotkb/P0ADE6

2\. Clicked the BLAST button on the entry page

3\. Used default blastp parameters

4\. Got 250 hits back

5\. Downloaded the accession list



Problem I ran into:

\- Every accession had a "TR:" prefix (e.g. TR:A0A061SSL7 instead of A0A061SSL7)

\- This broke the ID Mapping tool

\- Fixed it using Find and Replace in Notepad to remove all "TR:" prefixes



ID Mapping:

\- Used https://www.uniprot.org/id-mapping to convert accessions to sequences

\- 248 out of 250 mapped successfully (2 failed, reason unknown)

\- Downloaded 248 sequences in FASTA format



Output: sequences/kbp\_homologues.fasta (248 sequences)



Note: UniProtKB has lots of redundant sequences so I expected these 248 to be mostly E. coli and close relatives. Still useful as a starting point.



\---



\## Step 2: InterPro Search



Why I did this:

\- InterPro has pre-curated protein families so I can find the Kbp family directly

\- The reviewed (Swiss-Prot) entries are manually curated and very reliable



What I did:

1\. Searched InterPro using P0ADE6

2\. Found family IPR052196 - Bacterial Potassium Binding

3\. Family has about 19,000 proteins total, 8 are reviewed (Swiss-Prot)

4\. Downloaded the 8 reviewed sequences



Problem I ran into:

\- Downloaded file had a double extension: kbp\_interpro\_reviewed.fasta.fasta

\- Renamed it manually



Output: sequences/kbp\_interpro\_reviewed.fasta (8 sequences)



\---



\## Step 3: NCBI ClusteredNR BLAST



Why I did this:

\- NCBI ClusteredNR groups similar sequences and gives one representative per cluster

\- This should give more diverse hits than UniProtKB which has lots of redundant sequences



What I did:

1\. Went to https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastp

2\. Used P0ADE6 as query

3\. Selected ClusteredNR database

4\. Set max target sequences to 500

5\. Downloaded all results



Output: sequences/kbp\_ncbi\_blast.fasta (500 sequences)



\---



\## Step 4: PDB Structures



Why I did this:

\- Having 3D structures lets me map conserved residues onto the protein structure later

\- Important for understanding which parts of the sequence are functionally critical



What I found:

Searched RCSB PDB using P0ADE6 and found 3 experimental structures



7PVC (2022, NMR, E. coli K-12)

\- Refined NMR structure of Kbp with K+ ion included

\- From Torres Caban et al. 2022

\- Key structure for the K+ binding site - identifies coordinating residues V7, A10, G75, I77, I80



7VCM (2022, X-ray 1.85 Angstrom, E. coli K-12)

\- Crystal structure of GINKO1 (Kbp inserted into EGFP)

\- From Wu et al. 2022

\- Confirms 6 backbone carbonyls coordinate K+: V7, K8, A10, G75, I77, I80 in Kbp numbering

\- Best resolution structure available



8ZEX (2024, X-ray 1.66 Angstrom, E. coli)

\- Structure of HaloKbp1a (Kbp inserted into HaloTag7)

\- From Cheng et al. 2024

\- Most recent structure, shows Kbp still being actively used in biosensor engineering



Downloaded all 3 as .cif files and saved to structures/ folder



\---



\## Summary of what I collected today



\- sequences/kbp\_homologues.fasta: 248 sequences (UniProt BLAST)

\- sequences/kbp\_interpro\_reviewed.fasta: 8 reviewed sequences (InterPro)

\- sequences/kbp\_ncbi\_blast.fasta: 500 sequences (NCBI ClusteredNR)

\- structures/: 7PVC.cif, 7VCM.cif, 8ZEX.cif



\## Issues today



\- UniProt accession list had "TR:" prefix that needed removing

\- 2 accessions failed to map in UniProt ID Mapping, reason unknown

\- InterPro download had double .fasta extension, renamed manually



\## Next steps



\- Align sequences with MAFFT

\- Visualise in JalView

\- Find 3D structures on RCSB/PDB (done above)



\---



\# 07-06-2026 - MAFFT Alignments and JalView Visualisation



\## What I was trying to do today



Run MAFFT alignments on both sequence sets and visualise them in JalView to check quality and identify any problematic sequences.



\---



\## Step 5: MAFFT Alignment - 248 UniProt sequences



Command I used:

\& "C:\\Users\\Barath Vikraman\\Downloads\\mafft-7.526-win64-signed\\mafft-win\\mafft.bat" --auto --reorder sequences\\kbp\_homologues.fasta > results\\alignments\\kbp\_homologues\_aligned.fasta



Why these flags:

\- --auto: lets MAFFT pick the best strategy for my dataset size automatically

\- --reorder: sorts output sequences by similarity, makes it easier to spot clusters in JalView



What MAFFT chose: FFT-NS-i (iterative refinement) - this is a more accurate method, good for 248 sequences



Output: results/alignments/kbp\_homologues\_aligned.fasta

File size: 152,366 bytes



\---



\## Step 6: MAFFT Alignment - 500 NCBI sequences



Command I used:

\& "C:\\Users\\Barath Vikraman\\Downloads\\mafft-7.526-win64-signed\\mafft-win\\mafft.bat" --auto --reorder sequences\\kbp\_ncbi\_blast.fasta > results\\alignments\\kbp\_ncbi\_blast\_aligned.fasta



What MAFFT chose: FFT-NS-2 (fast progressive method, guide trees built twice)

\- MAFFT picked this because the dataset is larger and more diverse

\- FFT-NS-2 is faster than FFT-NS-i but slightly less accurate

\- Fine for a first pass alignment - can use a more accurate method on a refined subset later



Alignment length: 1974 residues

Output: results/alignments/kbp\_ncbi\_blast\_aligned.fasta

File size: approximately 990 KB



Issues:

\- A bash.exe.stackdump file appeared after the run - this is a known Windows artefact from MAFFT and does not mean the alignment failed or is wrong. Did not commit this file.

\- LF to CRLF warning during git add - expected on Windows, no action needed



\---



\## Step 7: JalView Visualisation



Tool: JalView v2.11.5.1

Loaded: results/alignments/kbp\_homologues\_aligned.fasta

Colour scheme applied: Clustal



What I observed:

\- Clear conserved core region at approximately positions 60 to 140 - shows up as solid colour blocks under Clustal colouring

\- The Fe contact residues in the secondary structure annotation at the bottom line up exactly with this conserved region - makes sense as these are the K+ binding residues

\- Most columns in the core show very strong conservation



Sequences that looked problematic:

\- Several WP\_ accessions in the lower part of the alignment are almost entirely gaps - these are probably partial or fragment sequences from NCBI, may need removing before phylogenetics

\- AGR60002 from Salmonella bongori (annotated as hypothetical protein) looks misaligned - its residues are scattered across the full width of the alignment instead of lining up with the core

\- F4T3US\_ECOLX has about 9 extra amino acids before the conserved Met start site - could be a real leader sequence or a wrong start site prediction in the annotation



Important limitation Dr Pritchard pointed out:

\- When he removed all 100% identical sequences, only about 30 unique sequences remained

\- The dataset is almost entirely E. coli and Salmonella

\- I need to get sequences from much more distantly related organisms to make the analysis meaningful



\---



\# 09-06-2026 - Fixing Encoding and Getting More Diverse Sequences



\## What I was trying to do today



Fix the encoding problem Dr Pritchard reported. Get a more diverse set of Kbp sequences. Start reading the literature.



\---



\## Step 8: Fix UTF-16 Encoding



The problem:

\- Dr Pritchard reported he got the error "utf-8 codec can not decode byte 0xff in position 0" when opening my alignment files in Python

\- He ran chardet on the files and found they were saved as UTF-16 instead of UTF-8

\- UTF-16 is not standard for bioinformatics tools and causes errors in Python, command line tools etc.



Why this happened:

\- A Windows text editor (probably Notepad) re-saved the file and switched the encoding

\- MAFFT itself does not produce UTF-16 output



How I fixed it:

\- Ran these PowerShell commands to convert both files to UTF-8:



$content = Get-Content "results\\alignments\\kbp\_ncbi\_blast\_aligned.fasta" -Encoding Unicode

$content | Set-Content "results\\alignments\\kbp\_ncbi\_blast\_aligned.fasta" -Encoding UTF8



$content = Get-Content "results\\alignments\\kbp\_homologues\_aligned.fasta" -Encoding Unicode

$content | Set-Content "results\\alignments\\kbp\_homologues\_aligned.fasta" -Encoding UTF8



\- Also fixed Git line endings globally so this does not happen again:



git config --global core.autocrlf false

git config --global core.eol lf



Committed: both files recommitted as UTF-8, commit a091c1e



Lesson learned: always check file encoding when saving on Windows. From now on all data files must be UTF-8.



\---



\## Step 9: InterPro Similar Proteins - Filtering



Why I did this:

\- Dr Pritchard pointed me to the InterPro similar proteins page as a good source of diverse Kbp sequences

\- Downloaded all proteins with the same BON + LysM domain architecture as P0ADE6



What I downloaded:

\- URL: https://www.ebi.ac.uk/interpro/protein/UniProt/P0ADE6/similar\_proteins/#table

\- Total downloaded: 3,233 sequences

\- Saved as: sequences/kbp\_interpro\_similar.fasta (had double extension issue again, renamed)



Why I needed to filter:

\- Looking at the headers I could see the 3,233 sequences included proteins that are NOT genuine Kbp

\- Examples: Peptidase M23B, Peptidoglycan-binding LysM proteins

\- These share the LysM domain with Kbp but do not have the BON domain where K+ binds

\- I only want true Kbp homologues



How I filtered:

\- Wrote a PowerShell script to keep only sequences with "Potassium binding protein Kbp" in the header

\- The logic: loop through every line, if it is a header line check if it contains that text, if yes keep that sequence, if no skip it



$in = Get-Content "sequences\\kbp\_interpro\_similar.fasta"

$out = @()

$keep = $false

foreach ($line in $in) {

&#x20;   if ($line.StartsWith(">")) {

&#x20;       $keep = $line -match "Potassium binding protein Kbp"

&#x20;   }

&#x20;   if ($keep) { $out += $line }

}

$out | Set-Content "sequences\\kbp\_interpro\_kbp\_only.fasta" -Encoding UTF8



Result: 1,960 sequences kept out of 3,233

Output: sequences/kbp\_interpro\_kbp\_only.fasta



Note: 1,960 is still too many to align directly. Will need to subsample for diversity later.



\---



\## Step 10: New NCBI BLASTp Search for Diverse Homologues



Why I did this:

\- My existing sequences are still too dominated by E. coli and Salmonella

\- Need sequences from completely different bacteria like Pseudomonas, Bacillus, Vibrio

\- Searching the full nr database instead of ClusteredNR should help



Search details:

\- Query: P0ADE6 (149 aa)

\- Database: non-redundant protein sequences (nr)

\- Max target sequences: 5000

\- Search strategy file saved: 2NMTWZA2014\_search\_strategy.asn

\- RID: 2NMUHP9J016 (expires 06-12-2026 23:25)



What I got back (first 100 sequences downloaded):

\- Still mostly Enterobacteriaceae: E. coli, Salmonella, Klebsiella, Serratia, Pantoea, Erwinia, Yersinia, Citrobacter

\- Need to rerun with BLOSUM45 matrix and higher E-value threshold to get more distant hits



\---



\# 10-06-2026 - Literature Review



\## What I read today



I read all 4 key papers on KbpA so I can understand the protein well enough to interpret my alignments and decide which sequences to keep.



\---



\## Paper 1: Ashraf et al. 2016 (Structure) - PDB: 5FIM



This is the foundational paper that first properly characterised Kbp.



Key findings:

\- Kbp binds a single K+ ion with Kd approximately 160 uM

\- High selectivity for K+ over Na+

\- The BON domain alone binds K+ but weakly (Kd about 20 mM)

\- The LysM domain is needed to stabilise the K+-bound state and achieve the tight 160 uM affinity

\- When K+ binds the protein shrinks dramatically: from 12.5 nm (open, no K+) to 6.5 nm (compact, K+ bound) - measured by SAXS

\- Bacteria without Kbp grow fine at low K+ but show a 2-5 hour growth delay at high K+ - confirms it has a real physiological role

\- NMR structure deposited as 5FIM but the exact K+ binding residues were not identified in this paper



Why it matters for my project:

\- Gives me the domain boundaries: BON is residues 1-89, LysM is 92-149

\- Tells me both domains must be present for the protein to work properly

\- This means I should exclude any sequences that are missing either domain



\---



\## Paper 2: Torres Caban et al. 2022 (ACS Sensors) - PDB: 7PVC



This paper finally identified the exact K+ binding residues.



Key findings:

\- Used thallium (Tl+) as a K+ mimic in NMR - thallium produces scalar couplings that identify exactly which atoms touch the ion

\- K+ is coordinated by the backbone carbonyls of: V7, A10, G75, I77, I80 in a distorted square pyramid

\- K8 is a possible 6th ligand

\- G75 and G11 must remain glycine - any other amino acid at these positions breaks the binding site

\- Also did genome mining: searched a metagenomic database and found 4 homologues at 45-72% identity from P. aeruginosa, compost, hydrothermal vent, and Defluviicoccus sp.

\- All 4 homologues retained K+ binding function despite sequence differences



Why it matters for my project:

\- Gives me the exact residues to check are conserved in my alignment: V7, A10, G75, I77, I80

\- G75 and G11 conservation is a key filter criterion - if a sequence does not have glycine at these positions it probably cannot bind K+

\- The genome mining part is very similar to what I am doing - good to know it has been done before and found functional homologues at \~50% identity



\---



\## Paper 3: Wu et al. 2022 (PLOS Biology) - PDB: 7VCM



This paper solved the crystal structure of GINKO1.



Key findings:

\- Crystal structure of GINKO1 (Kbp inserted into EGFP) at 1.85 Angstrom resolution

\- Confirms K+ is coordinated by 6 backbone carbonyls: V154, K155, A157, G222, I224, I227 in GINKO1 numbering

\- These correspond to V7, K8, A10, G75, I77, I80 in Kbp numbering

\- Binding site is in the BON domain right at the interface with the LysM domain

\- Used the structure to engineer GINKO2 with higher K+ sensitivity

\- GINKO2 works in vivo in bacteria, plants and mice



Why it matters for my project:

\- The crystal structure gives the best structural evidence for the binding site

\- The Fe markers I see in JalView secondary structure annotation correspond directly to these residues

\- Confirms the residues I need to check in my alignment



\---



\## Paper 4: Cheng et al. 2024 (JACS) - PDB: 8ZEX



The most recent paper on Kbp-based sensors.



Key findings:

\- Made HaloKbp1 series by inserting Kbp into HaloTag7 (a self-labelling protein tag)

\- Labelled with rhodamine dyes to get red/far-red fluorescence - better for imaging in cells than green sensors

\- Range of Kd values covering physiological K+ concentrations

\- Suitable for detecting K+ changes caused by BK channel activation

\- Crystal structure deposited as 8ZEX



Why it matters for my project:

\- Shows Kbp is still being actively used and engineered

\- Having a third crystal structure (8ZEX) alongside 7PVC and 7VCM is useful for structural comparison

\- Demonstrates that diverse homologues with different binding affinities are valuable for sensor engineering - which is exactly why genome mining is worth doing



\---



\## Key residues summary - what to look for in my alignment



K+ coordinating residues (backbone carbonyls, must be conserved):

\- V7: loop 1, BON domain

\- A10: loop 1, BON domain

\- G75: loop 5, BON domain - MUST be glycine

\- I77: loop 5, BON domain

\- I80: loop 5, BON domain

\- K8: possible 6th ligand



Structurally critical glycines:

\- G11: must be glycine, allows loops 1 and 5 to come close together

\- G75: must be glycine, any side chain would break the F6 packing nearby

\- G79: tight turn, hydrogen bonds with K8



Interdomain contact:

\- N76: hydrogen bonds with V143 in LysM domain - important for domain communication



\---



\## Criteria for excluding sequences from my dataset



A sequence should be removed if:

1\. Missing the BON domain (roughly residues 1-89) - cannot bind K+

2\. Missing the LysM domain (roughly residues 92-149) - cannot stabilise K+ binding

3\. Much shorter than 149 aa - probably a fragment, not a complete protein

4\. G75 is not conserved - binding site geometry would be broken

5\. Signs of a fusion protein or extra domains that are not part of Kbp

6\. 100% identical to another sequence already in the dataset - adds no new information



\---



\## Issues today



\- NCBI BLAST results page hung and took very long to load - results saved under RID 2NMUHP9J016



\---



\## Next steps



\- Rerun BLAST with BLOSUM45 matrix to get sequences from outside Enterobacteriaceae

\- Apply the filtering criteria above to the full sequence dataset

\- Subsample to approximately 150-200 diverse sequences for alignment

\- Run MAFFT on the filtered diverse set

\- Map K+ binding residues V7, A10, G75, I77, I80 onto the JalView alignment

\- Structural comparison of 7PVC, 7VCM, 8ZEX in PyMOL or ChimeraX

\- Phylogenetic analysis with IQ-TREE once alignment is finalised

