In UNIX,

If you add `&` to the end of command, it will run on the background and prompt will be free

```shell
paste 1.fq 2.fq | sort | uniq -c &
```
this gives you a kind of job id...
and command prompt will be free...

use `nohup` (not hang up) on the beginning, if you want cluster to continue even when you close your pc.
```shell
nohup paste 1.fq 2.fq | sort | uniq -c &
```


| Alinger | Approach | Applications | Availability |
| ---- | ---- | ---- | ---- |
| BWA-mem | Burrow-Wheeler | DNA, SE, PE, SV | open-source |
| Bowtie2 | Burrow-Wheeler | DNA, SE, PE, SV | open-source |
| Novoalign | hash-based | DNA, SE, PE | free for academic use |
| TopHat | Burrow-Wheeler | RNA-seq | open-source |
| STAR | hash-based (reads) | RNA-seq | open-source |
| GSNAP | hash-based (reads) | RNA-seq | open-source |

### BWA-MEM workflow

|                       *Reference Genome (FASTA)*  
|                                            |
|                                           \\/
*FASTQ (Unaligned)* -->  **BWA - MEM** --> SAM File (Aligned)

`bwa` requires index files from the reference genome

* Create BWT of reference genome
```shell
bwa index grch38.fa
```
Slow but, only needs to be done **once** for a genome...


* Align paired-end FASTQ to BWT index.
```shell
bwa mem grch38.fa 1.fq 2.fq > sample.sam
```
output is in SAM format...

**SAM is simply an alignment file**


## SAM format

Sequence Alignment/Map (SAM) format

Strength of the SAM and BAM formats
- Compressed
- Indexed: Fast viewing, slicing 
- Single-end and paired end
- Simple to produce
- **Good toolkits available**

SAM format overview
11 columns (12th optional)

| Col Number | Name | Meaning | Example |
| ---- | ---- | ---- | ---- |
| 1 | QNAME | Read name or query name |  |
| 2 | FLAG | bitwise flag |  |
| 3 | RNAME | reference seq | chr1 |
| 4 | POS | 1-based alignment start coordinate | 8,753,245 |
| 5 | MAPQ | mapping quality | 60 |
| 6 | CIGAR | extended CIGAR string |  |
| 7 | MRNM | If paired, the mate's ref. seq | chr1 |
| 8 | MPOS | If paired, the mate's align. seq | 8,753,795 |
| 9 | ISIZE | If paired, the insert size | 560 |
| 10 | SEQ | Sequence of the query | ACTAT.. |
| 11 | QUAL | quality of string for the query | HHH.. |
| 12  | OPT | optional tags |  |

Show the first line (column names) of a sam or bam file 
```shell
samtools view some.bam | head -1
```

### Converting SAM to BAM

#### SAM 
- Text-based 
- Human readable 
- Requires More Memory
#### BAM
- Binary format 
- Less memory
- Around 10%

**CRAM**
- Even more compression
- Around 1-5%


```shell
samtools view -Sb sample.sam > sample.bam
```
> -Sb:
> 	From SAM to bam