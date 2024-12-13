# BLAST (Basic Local Alignment Search Tool)
This is a basic tutorial on how to set up Blast on the Fred Hutch computing clusters. To run the graphical interface, visit the NCBI website here: "https://blast.ncbi.nlm.nih.gov/Blast.cgi".

# Accessing FHCC computing cluster
Make sure you can access rhino03 (or equivalent) cluster on the FHCC servers, including ssh (https://sciwiki.fredhutch.org/scicomputing/access_methods), and for ease of transferring larger files, an ftp client such as filezilla.

# Install BLAST
Blast is already installed on the FHCC servers.  To upload the module, log into rhino03 and type 
```
module load BLAST+/2.14.0-gompi-2022b
```

# Construct BLAST Database
