
To get count of A, T, G, C on a fasta file.


```shell
sort dna.txt | uniq -c 
```
`sort` the file first,
pipes into `uniq -c `
to count each of their numbers.