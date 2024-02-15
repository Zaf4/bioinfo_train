
# Mapping 

find the best possible loci to which a sequence could be aligned 
(quickly)

# Alignment

for each locus determine the optimal base-by-base alignment of the query sequence to the reference sequence.


## Hash-based mapping

Step 1:
hash/index the genome
for example find each k-mers on a ref.

| k-mer | Genome Position |
| ---- | ---- |
| CAT | 1,7 |
| ATG | 2 |
| TGG | 3,10 |
| ...  | ... |
Step 2:
Use the index to map reads

Read = TGGTCA
**TGG**TCA

### Optimal size for k-mers for Human genome

Above 90% of 50mers appears only once.

The trade-off is that k=50 uses too much memory

20=< k <35 is preferred.

## Mapping Quality (MAPQ)

Probability of mapping only that sequence. 

$$
 MAPQ = -10\times log_{10}(P_{map-loc-wrong})
$$

| $P_{map-loc-wrong}$ | MAPQ |
| ---- | ---- |
| 1 | 0 |
| 0.1 | 10 |
| 0.01 | 20 |
| 0.001 | 30 |
| 0.0001 | 40 |

### Alignment Algorithms

Smith-Waterman: **LOCAL**
Needleman-Wunsch: **GLOBAL**

