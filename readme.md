# BLAST (Basic Local Alignment Search Tool)
This is a basic tutorial on how to set up Blast on the Fred Hutch computing clusters. To run the graphical interface, visit the NCBI website here: "https://blast.ncbi.nlm.nih.gov/Blast.cgi".

# Accessing FHCC computing cluster
Make sure you can access rhino03 (or equivalent) cluster on the FHCC servers, including ssh (https://sciwiki.fredhutch.org/scicomputing/access_methods), and for ease of transferring larger files, an ftp client such as filezilla.

# Load BLAST
Blast is already installed on the FHCC servers.  To upload the module, log into rhino03 and run the following command to load the BLAST module (check versions) 
```
module load BLAST+/2.14.0-gompi-2022b
```

# Construct BLAST Database
To construct a BLAST database, one option is to download a FASTA file from Uniprot.  For example, if we want to use the _Mus musculus_ database, visit the Uniprot webpage "https://www.uniprot.org/proteomes/UP000000589", and select the option next to "Gene Count" and "Download one protein sequence per gene (FASTA)".  This should download the file 'UP000000589_10090.fasta.gz'.  

Next, upload this file into a specified directory, for example, "/fh/fast/hill_g/Albert/Genomes_Proteomes/Murine_Sequences/proteomes/UP000000598_10090_Mus_musculus".  To unzip, input the command (while in the directory):
```
gunzip UP000000589_10090.fasta.gz
```
In terminal, run the following command to generate the database:
```
makeblastdb -in UP000000589_10090.fasta -dbtype prot -out UP000000589_10090_db
```
Note the input parameters of makeblastdb
-in: The input FASTA file.  
-dbtype prot: Indicates the database contains protein sequences. Use nucl if it's nucleotide sequences.  
-out: The name of the output database files (e.g., UP000000589_10090_db).  

This will create 8 files, ending in ".pdb", ".phr", ".pin", ".pjs", ",pot", ".psq", ".ptf"., ".pto".  These are different components necessary for the BLAST search.

# BLASTing a peptide
Create a sample file “query.fasta” with the following simple text:
```
>Query1
IIPILGEGLL
```
Now, in the same directory, run the following command:
```
blastp -query query.fasta -db UP000186351_db -out results.txt -outfmt 6
```
Note the input parameters of blastp
-query query.fasta: Specifies the input file containing the query sequence.
-db UP000000589_10090_db: Specifies the BLAST database you created.
-out results.txt: Specifies the output file where results will be written.
-outfmt 6: Outputs the results in tabular format for easier parsing. You can modify this format if needed. 6 is clean; 7 has more information, for example.

A sample query output with "-outfmt 6":
| sequence | database | Uniprot Accesion# | Source (Bac) | %ID |Alignment length | Mismatch | Gap Openings | Query Start | End | Sequence aligned | Match (E-value) | prob(alignment) | Alignment Quality | 
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Query1 | tr|A0A1B1SA89|A0A1B1SA89_9BACT | 100.000 | 10 | 0 | 0 | 1 | 10 | 199 | 208 | 0.43 | 21.2
| Query1 | tr|A0A1B1S6U0|A0A1B1S6U0_9BACT | 62.500 | 8 | 3 | 0 | 2 | 9 | 241 | 248 | 9.8 | 17.3

Note that tr| indicates this is a TrEMBL (unreviewed) UniProt sequence.


