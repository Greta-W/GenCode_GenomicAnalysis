## Trim adaptors and quality check reads
```
for i in *.lite.1_1.fastq
do
OUT=${i%.lite.1_1.fastq}
for i in *.trim.1_1.fastaq
do
OUT=${i%.lite.trim.1_1.fastq}
done
```

## BWA Index the Reference
```
bwa index bbc.fasta
```

## BWA Map the Read
```
for i in *.trim.1_1.fastq
do
OUT=${i%.lite.trim.1_1.fastq}
bwa mem -t 10 bbc.fasta $OUT.lite.trim.1_1.fastq $OUT.lite.trim.1_2.fastq > $OUT.sam
done
```
## Switch .sam files to .bam files
```
for i in *.sam
do
OUT=${i%.sam}
samtools view -b $OUT.sam -o $OUT.bam
done
```

## Sort .bam files
```
for i in *.bam
do
OUT=${i%.bam}
samtools view -b $OUT.bam -o $OUT.sorted.bam
done
```
