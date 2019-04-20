# nygc-short-alignment-marking

###Tool to mark short alignments in a bam file.

* Version: 2.1
* Author: Minita Shah, Anne-Katrin Emde, Andre Corvelo
* Contact: mshah@nygenome.org

# Manual

**Description:**
This tool parses the bam file and marks as unmapped a read with alignment length below a user-defined threshold. Reads are not filtered from the bam file but kept as unmapped.

**Installation:**
* Ubuntu
```
export LD_LIBRARY_PATH=/path/to/lib:$LD_LIBRARY_PATH
filter_bam --help
```

* CentOS/RedHat 
```
filter_bam --help
```


**Usage:** 
```
./filter_bam --help
filter_bam - Filters bam file based on alignment length (with potential to add other filters).
Created by Minita Shah (mshah@nygenome.org)
==========================================================================================================================================

SYNOPSIS
    filter_bam [options]

DESCRIPTION
    -h, --help
          Displays this help message.
    --version
          Display version information.

  Options:
    -I, --BAM BAM
          Input bam file Valid filetypes are: bam and sam.
    -A1, --ALN_LEN_PRIM ALN_LEN_PRIM
          Primary (loose) alignment length
    -A2, --ALN_LEN_SECOND ALN_LEN_SECOND
          Supplementary (strict) alignment length
    -o, --OUT_PREFIX OUT_PREFIX
          Output file prefix

VERSION
    filter_bam version: 2.1
    Last update March 2019
```

**Example usage:**
```
Input bam - BWA mem aligned bam
filter_bam -I <bam_file> -A1 30 -A2 30 -o <out_prefix>.bam | samtools view -b -o <out_prefix>.bam -
```

**Output files:**
* Short alignment marked bam file
* Summary stats
```
E.g.
Total Reads: 113850215
Total Primary Reads: 113458066
Total Supplementary Reads: 392149
Total Primary Reads Filtered: 130714
Total Supplementary Reads Filtered: 0

Samples with known bacterial contamination:
Total Reads: 115894178
Total Primary Reads: 114818564
Total Supplementary Reads: 1075614
Total Primary Reads Filtered: 4089355
Total Supplementary Reads Filtered: 4952
```

**Tags being added:**
* FT:Z:short_alignment - read marked as unaligned because of short alignment
* e.g. ZA:Z:chrUn_KN707964v1_decoy,511,-,80S71M,0,7 - user-defined tag; supplementary alignment information. Occurs along with "FT" tag
