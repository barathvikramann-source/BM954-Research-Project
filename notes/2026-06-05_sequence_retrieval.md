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



\# 07-06-2026 - MAFFT Alignments and JalView Visualisation ( Used Claude) for MAFFT



\## What I was trying to do today



Run MAFFT alignments on both sequence sets and visualise them in JalView to check quality and identify any problematic sequences.



\---



\## Step 5: MAFFT Alignment - 248 UniProt sequences ( Used Claude.ai for this command)



Command I used:

\& "C:\\Users\\Barath Vikraman\\Downloads\\mafft-7.526-win64-signed\\mafft-win\\mafft.bat" --auto --reorder sequences\\kbp\_homologues.fasta > results\\alignments\\kbp\_homologues\_aligned.fasta (CLAUDE.AI)



Why these flags:

\- --auto: lets MAFFT pick the best strategy for my dataset size automatically

\- --reorder: sorts output sequences by similarity, makes it easier to spot clusters in JalView



What MAFFT chose: FFT-NS-i (iterative refinement) - this is a more accurate method, good for 248 sequences



Output: results/alignments/kbp\_homologues\_aligned.fasta

File size: 152,366 bytes



\---



\## Step 6: MAFFT Alignment - 500 NCBI sequences ( Used Claude.ai) for allignment



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



How I fixed it: (used claude.ai to fix this issue using a command)

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

$out | Set-Content "sequences\\kbp\_interpro\_kbp\_only.fasta" -Encoding UTF8 (Coded using Claude.AI)



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



\---



\# 11-06-2026 - InterPro Subsampling, MAFFT in JalView, Repository Cleanup



\## What I did today



\- Ran the subsampling script on kbp\_interpro\_kbp\_only.fasta to get a manageable dataset

&#x20;   - Took every 10th sequence from the 1,960 filtered sequences

&#x20;   - Result: 196 sequences saved as sequences/kbp\_interpro\_subsample.fasta



\- Opened kbp\_interpro\_subsample.fasta in JalView

&#x20;   - Ran MAFFT alignment using Web Service > Alignment > MAFFT with Defaults

&#x20;   - 196 sequences, ran successfully via JalView web service

&#x20;   - Applied Clustal colouring

&#x20;   - Two conserved blocks visible corresponding to BON domain (left) and LysM domain (right)

&#x20;   - Conservation and Quality tracks show strongest conservation at K+ binding residue positions

&#x20;   - Saved alignment as results/alignments/kbp\_interpro\_subsample\_aligned.fa



\- Cleaned up repository in response to Issue #2 raised by Dr Pritchard (widdowquinn)

&#x20;   - Removed all template folders not relevant to the project

&#x20;   - Deleted: data/, docs/, notebooks/, scripts/, \_config.yml

&#x20;   - Deleted: results/conservation/, results/positive\_selection/, results/README.md

&#x20;   - Commit fcfbc28 - closes Issue #2



\## Issues today



\- JalView web service MAFFT has a limit of 1000 sequences - could not run on full 1,960 sequence dataset

&#x20;   - Solved by subsampling to 196 sequences first



\## Next steps



\- Run new BLAST search with BLOSUM45 to get sequences from outside Enterobacteriaceae

\- Apply filtering criteria to sequence dataset

\- Map K+ binding residues V7, A10, G75, I77, I80 onto alignment in JalView

\- Structural comparison of 7PVC, 7VCM, 8ZEX in PyMOL or ChimeraX

\- Phylogenetic analysis with IQ-TREE



What I did today (14,15-06-2026)



Step 1 - UniProt 50% identity homologues





Ran BLAST on UniProt against UniProtKB database using query P0ADE6 (Kbp, E. coli K12, 149 aa)

Filtered results to identity range 50-100%

Retrieved 588 filtered hits

Downloaded accession list and performed ID mapping (removed TR:/SP: prefixes)

Result: 1,000 sequences saved as kbp\_uniprot\_50pct.fasta







Step 2 - InterPro domain sequences





Identified Kbp domain architecture: BON domain (PF04972, residues 23-91) + LysM domain (PF01476, residues 92-149)

Visited InterPro PF04972 entry - 26k proteins found (too broad, BON domain alone too common)

Step deferred - will revisit using combined domain architecture filter (PF04972 + PF01476)





Step 3 - NCBI BLAST against ClusteredNR





Ran BLASTP on NCBI using query P0ADE6 against ClusteredNR database

RID: 2ZJEF9F0016

Retrieved 1,000 cluster representative sequences

Downloaded as FASTA (cluster) format

Saved as kbp\_ncbi\_clusternr.fasta

Noted outliers: 28 fragments <100 aa, 8 fusion proteins >300 aa (e.g. 8ZEX\_A at 484 aa)





Step 4 - Combine sequences (JalView)





Opened kbp\_uniprot\_50pct.fasta in JalView (File → Input Alignment → From File)

Loaded kbp\_ncbi\_clusternr.fasta into same window (File → Load Sequences into Alignment)

Combined dataset: 2,000 sequences

Saved as kbp\_combined.fa





Step 5 - Remove redundant sequences and fusion proteins (JalView)





Calculate → Remove Redundancy at 100% threshold → removed 310 exact duplicates → 1,690 sequences

Sorted by length (Calculate → Sort → By Length)

Removed fragments <120 aa and fusion proteins >250 aa → 1,677 sequences

Saved as kbp\_combined\_cleaned.fa





Step 6 - MAFFT alignment





Submitted kbp\_combined\_cleaned.fa to MAFFT online server (https://mafft.cbrc.jp/alignment/server/)

Strategy: --auto

Output: 1,629 sequences (some removed during alignment)

Saved as results/alignments/kbp\_aligned.fasta

Loaded into JalView - two conserved blocks visible (BON domain and LysM domain regions)

Conservation and Quality tracks confirm strong conservation at functional residue positions









Issues today





UniProt BLAST download interface does not support filtered FASTA download directly - had to use accession list + ID mapping workaround

NCBI BLAST downloaded as .txt - had to manually rename to .fasta for JalView compatibility

JalView Remove Redundancy at 90% threshold too aggressive for this protein family (nearly all sequences identical at that level) - kept at 100% for exact duplicate removal only





Next steps





Complete Step 7 - finish removing sequences lacking conserved BON domain residues (Q64, T91, N76)

Step 8 - save final curated alignment with appropriate filename

Step 9 - reduce dataset using CD-HIT or JalView at appropriate identity threshold (suggest 60-70%)

Return to Step 2 - retrieve InterPro sequences using combined domain filter (PF04972 + PF01476)

Map K+ binding residues V7, A10, G75, I77, I80 onto alignment in JalView

Structural comparison of 7PVC, 7VCM, 8ZEX in PyMOL or ChimeraX

Phylogenetic analysis with IQ-TREE





\## What i did today (20,22-06-26)



Structural analysis of 8ZEX (HaloKbp1a)

8ZEX is the engineered potassium biosensor — the Kbp protein inserted into HaloTag7 (Cheng et al. 2024). I wanted to map sequence conservation onto it and see whether the potassium-binding site is conserved, applying the same method my professor showed me on 7PVC.

1\. I opened the structure.

open 8ZEX

I used this to load the 8ZEX structure into ChimeraX so I could work on it.

2\. I loaded my sequence alignment and associated it.



(File → Open → kbp\_interpro\_subsample\_aligned.fa)



I did this so ChimeraX could compare my structure's sequence against 195 related Kbp proteins and work out how conserved each position is. It associated with 13 mismatches (the wild-type 7PVC had 0 — so these 13 are the engineered mutations).

3\. I coloured the structure by conservation.

**color byattribute seq\_conservation**

I used this to colour each residue by how conserved it is — red = conserved, blue = variable. The Log showed the score range was −1.43 to 1.99. I saw the conserved (red) residues clustered around the potassium, and the HaloTag7 part stayed uncoloured because it isn't part of the Kbp family.

4\. I selected the conserved residues.

**select ::seq\_conservation > 0.5**

I used this to pick out only the conserved positions so I could see how many there were and where they sat → 39 residues, clustered at the binding site.

5\. I tightened the cutoff to check the conservation was strong.

**select ::seq\_conservation > 1.0**

I raised the threshold to test whether the conserved residues were borderline or genuinely strong → still 30 residues, barely fewer, still at the site. This showed the conservation is concentrated, not cutoff-dependent.

6\. I selected the variable residues for comparison.

**select ::seq\_conservation < 0.5**

→ 101 residues, mostly on the outer surface. So most of the protein is free to vary; only a minority at the site is conserved.

7\. I looked at how the potassium is held. I drew the contacts/H-bonds around the ion, then cleaned up the view:

**hide solvent**

I used this to hide the water molecules (the red dots) so they didn't clutter the view.

8\. I zoomed in on the potassium.

**view :K**

I used this to centre and zoom on the potassium ion so I could see the pocket up close.

9\. I coloured by element (heteroatom button) so the oxygens showed as red. This let me see that the contacts gripping the potassium come from the backbone of the conserved loops (main-chain carbonyl oxygens), not side chains — the channel-style coordination.

10\. I noted the "8 residues" gap = the disordered loop A162–K169, which couldn't be resolved. It's away from the binding site, so it doesn't affect the coordination analysis.

11\. Observed n and c linker in the structure.



