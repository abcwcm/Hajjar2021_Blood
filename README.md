# Methods and VCF files related to Fassel, Chen, Ruise, Kumar, DeSancho and Hajjar (2021). Blood

The Applied Bioinformatics Core analyzed DNA sequencing data generated after long-range PCR of the AnnexinA2 (ANXA2) gene.
There were samples from three different groups of patients: 1) healthy patients, 2) patients withthrombosis and normal levels of ANXA2, and 3) patients with thrombosis and low or undetectable levels of ANXA2. Following the Broad Institute’s/GATK best practices, variants were identified, annotated, and manually explored.

DNA  samples  were  collected  from  18  patients:

* 6  healthy  patients
* 6  patients  with  thrombosis  and  normal  levels of  ANXA2,  and  
* 6  patients  with  thrombosis  and  low  or  undetectable  levels  of  ANXA2.

The  ANXA2  gene  is  approximately  60  kb  long,  and  was  isolated  via  long  range  PCR  (with  10  kb  5’  and  1  kb  3’  flanking  regions).
The resultant isolates were fragmented and subsequently sequenced (single-end, 150 bp) on an Illumina MiSeq Sequencerat Cornell's Genomics Facility in Ithaca, NY.

The goal of the analysis was to determine whether there are genetic variants that are unique to the patients with thrombosis and low ANXA2 levels.

For variant calling, the following tools were used: FreeBayesv1.0.2-33, VarScan v2.3.9, and HaplotypeCaller v3.6-0.

## Results


![](figures/heatmap_homohetero_noclust.png)

Heatmap of genotypes where columns represent single variants, and rows represent the individual samples.
Light cyan indicates homozygosity for the reference allele, medium cyan heterozygosity, and dark cyan homozygosity for the alternative allele.
The boxes on the left side mark healthy (green), TL (red) and TN (blue) as well as male (brown) and female (off-white) samples.
