#Input Code: Engaging Conda
```
conda activate bio_env
```

#Output: bcftools activated

#Input Code: Open previously downloaded file through bcftools
```
bcftools query -l body_size.vcf
```

#Output Code: lists contents/opens body_size.vcf file
```
[W::bcf_hdr_check_sanity] MQ should be declared as Type=Float
SRR10729165.sorted.bam
SRR10729166.sorted.bam
SRR10729566.sorted.bam
SRR10733526.sorted.bam
SRR31835375.sorted.bam
SRR31835473.sorted.bam
SRR31835482.sorted.bam
SRR31835573.sorted.bam
```

#Input Code: compress body_size.vcf into an index
```
bgzip body_size.vcf
bcftools index body_size.vcf.gz
```


#Input Code: creates two new text files from body_size.vcf.gz, titled group1.txt (Ethiopian half of the data) and group2.txt (Zambian half of the data)
```
group1.txt
SRR10729165.sorted.bam
SRR10729166.sorted.bam
SRR10729566.sorted.bam
SRR10733526.sorted.bam

group2.txt
SRR31835375.sorted.bam
SRR31835473.sorted.bam
SRR31835482.sorted.bam
SRR31835573.sorted.bam
```

#Input Code: splits body_size.vcf.gz into two files now titled group1.vcf.gz and group2.vcf.gz
```
bcftools view -S group1.txt body_size.vcf.gz -Oz -o group1.vcf.gz
bcftools view -S group2.txt body_size.vcf.gz -Oz -o group2.vcf.gz
```

#Input Code: filters each group's vcf into ”biallelic” SNPs
```
bcftools view -m2 -M2 -v snps group1.vcf.gz -Oz -o group1_biallelic.vcf.gz
bcftools view -m2 -M2 -v snps group2.vcf.gz -Oz -o group2_biallelic.vcf.gz
```

#Input Code: calculates allele frequency within each group
```
bcftools +fill-tags group1_biallelic.vcf.gz -Oz -o group1_af.vcf.gz -- -t AF
bcftools +fill-tags group2_biallelic.vcf.gz -Oz -o group2_af.vcf.gz -- -t AF
```

#Input Code: pulls out just CHROM, POS,and AF (chromosome, position, and allele frequency) from the egg group’s vcf
```
bcftools query -f '%CHROM\t%POS\t%INFO/AF\n' group1_af.vcf.gz > group1_af.tsv
bcftools query -f '%CHROM\t%POS\t%INFO/AF\n' group2_af.vcf.gz > group2_af.tsv
```

#Input Code: starts R Studio program within terminal
```
R
```

#Input Code: assigns the variables g1 and g2 to the columns for chromosome, position, and allele frequency to make it into a table
```
g1 <- read.table("group1_af.tsv", col.names = c("CHROM", "POS", "AF1"))
g2 <- read.table("group2_af.tsv", col.names = c("CHROM", "POS", "AF2"))
```

#Input Code: merges the shared sites only
```
merged <- merge(g1, g2, by = c("CHROM", "POS"))
```

#Input Code: drops any columns where AF couldn't be calculated in one group (places with no called genotypes in that subset)
```
merged <- na.omit(merged)
```
#Input Code: subtracts merged$AF2 from merged$AF1 and puts the totals in their own column titled merged$AF_diff
```
merged$AF_diff <- merged$AF1 - merged$AF2
```

#Input Code: makes a plot of allele frequency differences compared to positions
```
pdf('merged.pdf')
plot(merged$POS, merged$AF_diff,
     pch = 19, col = "steelblue",
     xlab = "Position in gene", ylab = "Allele frequency difference (Group1 - Group2)",
     main = "Allele frequency difference along bbc")
abline(h = 0, lty = 2, col = "grey40")
```

#Input Code: closes the pdf ‘merged.pdf’ that you just made the plot inside of
```
dev.off()
```

# CHANGE SERVER TO LOCAL OR PERSONAL SERVER
#Input Code: to pull up the plot you just made in the merged.pdf
```
scp -r visitor@134.129.113.23:/storehouse/visitor/table_/pigmentation/merged.pdf
```

#Input Code: to open the plot once it has finished downloading
```
open

```
