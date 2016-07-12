# Genomic Origin Through Taxonomic CHAllenge (GOTTCHA)

GOTTCHA is an application of a novel, gene-independent and signature-based metagenomic
taxonomic profiling method with significantly smaller false discovery rates (FDR) that is 
laptop deployable. Our algorithm was tested and validated on twenty synthetic and mock 
datasets ranging in community composition and complexity, was applied successfully to data
generated from spiked environmental and clinical samples, and robustly demonstrates 
superior performance compared with other available tools.

-------------------------------------------------------------------
## UPDATES

1. No longer uses splitrim. Reports reads directly instead of hits.
2. Allow mismatches by specifying penalty score for a mismatch (still requiring minimal 30bp continuing exact matches)
3. Added “tree” mode to output all nodes in taxonomy lineage. It will be useful to reveal minor but important ranks, e.g. viral subtypes, groups...etc.
4. Added “class” mode to output read classification results.
5. Added “extract” mode to extract mapped reads.
6. User can specify a taxonomy, the profiler will only output/extract results/reads belong to the taxa and it’s descendent.
7. Performance improved. SAM file is processed in parallel.
8. Implemented in Python 3.5, no additional dependency required.

-------------------------------------------------------------------
## DISCLOSURE

GOTTCHA2 is currently under development in BETA stage. Databases for v1 will not be compatible with v2.

-------------------------------------------------------------------
## SYSTEM REQUIREMENT

Python 3.0+ is required. Linux (2.6 kernel or later) or Mac (OSX 10.6 Snow Leopard or later) operating system with minimal 8 GB of RAM is recommended.

-------------------------------------------------------------------
## INSTRUCTIONS

```python
usage: gottcha.py [-h] (-i [FASTQ] [[FASTQ] ...] | -s [SAMFILE])
                  [-d [BWA_INDEX]] [-l [LEVEL]] [-ti [FILE]] [-pm <INT>]
                  [-m {summary,full,tree,class,extract,lineage}] [-x [TAXID]]
                  [-r [FIELD]] [-t <INT>] [-o [DIR]] [-p <STR>] [-mc <FLOAT>]
                  [-mr <INT>] [-ml <INT>] [-nc] [-c] [--silent]
```
Genomic Origin Through Taxonomic CHAllenge (GOTTCHA) is an annotation-
independent and signature-based metagenomic taxonomic profiling tool that has
significantly smaller FDR than other profiling tools. This program is a
wrapper to map input reads to pre-computed signature databases using BWA-MEM
and/or to profile mapped reads in SAM format. (VERSION: 2.0 BETA)

optional arguments:

```
-i [FASTQ] [[FASTQ] ...], --input [FASTQ] [[FASTQ] ...]
```
Input one or multiple FASTQ file(s). Use space to separate multiple input files.
```
-s [SAMFILE], --sam [SAMFILE]
```
Specify the input SAM file. Use '-' for standard input.
```
-d [BWA_INDEX], --database [BWA_INDEX]
```
The path of signature database. The database can be in FASTA format or BWA index (5 files).
```
-l [LEVEL], --dbLevel [LEVEL]
```
Specify the taxonomic level of the input database. You can choose one rank from "superkingdom", "phylum","class", "order", "family", "genus", "species" and "strain". The value will be auto-detected if the input database ended with levels (e.g. GOTTCHA_db.species).
```
-ti [FILE], --taxInfo [FILE]
```
Specify the path of taxonomy information file (taxonomy.tsv). GOTTCHA2 will try to locate this file when user doesn't specify a path. If '--database' option is used, the program will try to find this file in the directory of specified database. If not, the 'database' directory under the location of gottcha.py will be used as default.
```
-pm <INT>, --mismatch <INT>
```
Mismatch penalty for BWA-MEM (pass to option -B while BWA-MEM is running). You can use 99 for not allowing mismatch in alignments (except for extreme cases). [default: 5]
```
-m {summary,full,tree,class,extract,lineage}, --mode {summary,full,tree,class,extract,lineage}
```
You can specify one of the following output modes:

* "summary" : report a summary of profiling result;
* "full" : other than a summary result, this mode will report unfiltered profiling results with more detail;
* "tree" : report results with lineage of taxonomy;
* "class" : output results of classified reads;
* "extract" : extract mapped reads;
* "lineage" : output abundance and lineage in a line

Note that only results/reads belongs to descendants of
TAXID will be reported/extracted if option [--taxonomy TAXID] is specified. [default: summary]
```
-x [TAXID], --taxonomy [TAXID]
```
Specify a NCBI taxonomy ID. The program will only report/extract the taxonomy you specified.
```
-r [FIELD], --relAbu [FIELD]
```
The field will be used to calculate relative abundance. You can specify one of the following fields: "LINEAR_LENGTH", "TOTAL_BP_MAPPED", "READ_COUNT" and "LINEAR_DOC". [default: LINEAR_DOC]
```
-t <INT>, --threads <INT>
```
Number of threads [default: 1]
```
-o [DIR], --outdir [DIR]
```
Output directory [default: .]
```
-p <STR>, --prefix <STR>
```
Prefix of the output file [default:<INPUT_FILE_PREFIX>]
```
-mc <FLOAT>, --minCov <FLOAT>
```
Minimum linear coverage to be considered valid in abundance calculation [default: 0.005]
```
-mr <INT>, --minReads <INT>
```
Minimum number of reads to be considered valid in abundance calculation [default: 3]
```
-ml <INT>, --minLen <INT>
```
Minimum unique length to be considered valid in abundance calculation [default: 60]
```
-nc, --noCutoff
```
Remove all cutoffs. This option is equivalent to use [-mc 0 -mr 0 -ml 0].
```
-c, --stdout
```
Write on standard output.
```
--silent
```
Disable all messages.
```
-h, --help
```
show this help message and exit
