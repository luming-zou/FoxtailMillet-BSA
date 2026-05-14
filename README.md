# FoxtailMillet-BSA
Scripts for identifying QTL in foxtail millets  

# Dependencies for the scripts  
+ python3  
+ R 3.6
+ samtools 1.11  
+ ggplot2 3.4.2
+ vcftools 0.1.16

# Produce fasta index for the reference genome  
Note: This fasta index file is required for subsequent delta-index analysis and manhattan plot. The reference genome was downloaded from setaria-db (http://111.203.21.71:8000/download.html).   
  
	samtools faidx REFERENCE.fa  

# Sample list and order  
+ S01, bulk of reistant larvae   
+ S02, bulk of susceptible larvae   
+ S03, Wild type  
+ S04, Mutant type  

# Extract gt info into GT format from the vcf  
	vcftools --vcf 01.SNP_biallele.recode.vcf \
		--extract-FORMAT-info GT \
		--out gt

# vcf was filtered to keep only biallel sites  
	vcftools \
	    --vcf SNP.final.vcf \
	    --min-alleles 2 \
	    --max-alleles 2 \
	    --recode \
	    --out SNP_biallele  

# Extract allele depth for each sample  
extract\_depth.py  

	python3 extract_depth.py > depth.txt

# Filter depth  
filter\_depth.r  

	Rscript filter_depth.r  

# Calculate Delta(SNP-index)  
delta\_snp\_index.r  
  
  
	Rscript delta_snp_index.r  

# Manhattan plot  
mahattan.r  
  
	Rscript manhattan.r  

