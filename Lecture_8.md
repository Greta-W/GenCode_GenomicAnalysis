# Input Code: call all variants in the file, give likelihood of each .bam file having each specific genotype:
```
bcftools mpileup -Ou -f bbc.fasta SRR10729165.sorted.bam SRR10729166.sorted.bam SRR10729566.sorted.bam SRR10733526.sorted.bam SRR31835375.sorted.bam SRR31835473.sorted.bam SRR31835482.sorted.bam SRR31835573.sorted.bam | bcftools call -mv -Ov -o body_size.vcf
```

# Output: 
```
Note: none of --samples-file, --ploidy or --ploidy-file given, assuming all sites are diploid
[mpileup] 8 samples in 8 input files
[mpileup] maximum number of reads per input file set to -d 250
```

# Input Code: Open and view file
```
nano body_size.vcf
```

# Output:
```
##bcftools_callCommand=call -mv -Ov -o body_size.vcf; Date=Mon Sep 28 14:35:54 2026
#CHROM  POS     ID      REF     ALT     QUAL    FILTER  INFO    FORMAT  SRR10729165.sorted.bam  SRR10729166.sorted.bam  SRR10729566.sorted.bam  SRR1073352>
bbc     157     .       C       T       666.844 .       DP=118;VDB=0.536151;SGB=23.8296;RPBZ=2.50294;MQBZ=0;MQSBZ=0;BQBZ=2.1436;SCBZ=0;MQ0F=0;AC=7;AN=16;D>
bbc     177     .       G       A       98.3539 .       DP=114;VDB=0.824688;SGB=9.43672;RPBZ=-0.857602;MQBZ=0;MQSBZ=0;BQBZ=-2.86974;SCBZ=0;MQ0F=0;AC=2;AN=>
bbc     214     .       A       T       204.532 .       DP=120;VDB=0.529691;SGB=26.0651;RPBZ=1.25793;MQBZ=0;MQSBZ=0;BQBZ=1.05434;SCBZ=-0.385922;MQ0F=0;AC=>
bbc     220     .       G       A       204.535 .       DP=119;VDB=0.424341;SGB=23.9858;RPBZ=1.38836;MQBZ=0;MQSBZ=0;BQBZ=1.28104;SCBZ=-0.369922;MQ0F=0;AC=>
bbc     223     .       T       TG      118.427 .       INDEL;IDV=6;IMF=0.461538;DP=119;VDB=0.358309;SGB=9.43672;RPBZ=0.176134;MQBZ=0;MQSBZ=0;BQBZ=1.28104>
bbc     224     .       T       G       217.318 .       DP=121;VDB=0.194617;SGB=-21.98;RPBZ=1.79035;MQBZ=0;MQSBZ=0;BQBZ=-0.142979;SCBZ=0;MQ0F=0;AC=5;AN=16>
bbc     248     .       G       C       205.957 .       DP=126;VDB=0.280929;SGB=14.4151;RPBZ=-2.20118;MQBZ=0;MQSBZ=0;BQBZ=1.40758;SCBZ=-0.710343;MQ0F=0;AC>
bbc     386     .       G       A       205.187 .       DP=93;VDB=0.285429;SGB=29.7446;RPBZ=-0.00535344;MQBZ=0;MQSBZ=0;BQBZ=3.2344;SCBZ=0;MQ0F=0;AC=2;AN=1>
bbc     470     .       C       G       205.081 .       DP=98;VDB=0.017972;SGB=31.7139;RPBZ=-0.958796;MQBZ=0;MQSBZ=0;BQBZ=1.02853;SCBZ=0.675557;MQ0F=0;AC=>

^G Help          ^O Write Out     ^F Where Is      ^K Cut           ^T Execute       ^C Location      M-U Undo         M-A Set Mark     M-] To Bracket
^X Exit          ^R Read File     ^\ Replace       ^U Paste         ^J Justify       ^/ Go To Line    M-E Redo         M-6 Copy         ^B Where Was
```
