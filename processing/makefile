.SECONDEXPANSION:
.SECONDARY:
.DELETE_ON_ERROR:

### OPTIONS
SECOND_PASS = 0

### SYSTEM TOOLS
LN = /bin/ln
MV = /bin/mv
CAT = /bin/cat
MKDIR = /bin/mkdir
ECHO = /bin/echo
CP = /bin/cp
CD = cd
GREP = /bin/grep
CUT = /bin/cut
ZCAT = /bin/zcat

### USER TOOLS
TRIM_GALORE = /zenodotus/abc/scratch/paz2005/bin/trim_galore
FASTQC = /home/paz2005/zeno/bin/src/fastqc_v0.11.3/FastQC/fastqc
BEDTOOLS = /zenodotus/abc/scratch/paz2005/bin/src/bedtools2-2.26-1/bin/bedtools
BWA = /zenodotus/abc/scratch/paz2005/bin/src/bwa-0.7.15/bwa
SAMTOOLS = /zenodotus/abc/scratch/paz2005/bin/src/samtools-1.3.1/samtools
BCFTOOLS = /zenodotus/abc/scratch/paz2005/bin/src/bcftools-1.3.1/bcftools
PLOT_BAMSTATS = /zenodotus/abc/scratch/paz2005/bin/src/samtools-1.3.1/misc/plot-bamstats
JAVA = /zenodotus/abc/scratch/paz2005/bin/src/gatk/jdk1.8.0_102/bin/java
GATK = /zenodotus/abc/scratch/paz2005/bin/src/gatk/gatk-protected/target/GenomeAnalysisTK.jar
TABIX = /zenodotus/abc/scratch/paz2005/bin/src/samtools-1.3.1/htslib-1.3.1/tabix
BGZIP = /zenodotus/abc/scratch/paz2005/bin/src/samtools-1.3.1/htslib-1.3.1/bgzip
PICARD = /zenodotus/abc/scratch/paz2005/bin/src/picard-tools-2.5.0/picard.jar
RSCRIPT = /home/paz2005/zeno/bin/src/R-3.2.1/pzR3.2.1/bin/Rscript
R = /home/paz2005/zeno/bin/src/R-3.2.1/pzR3.2.1/bin/R
STAR = /home/paz2005/zeno/bin/src/STAR-STAR_2.4.2a/source/STAR
QORTS = /home/paz2005/zeno/bin/src/hartleys-QoRTs-200b950/QoRTs_0.3.5/QoRTs.jar
FEATURE_COUNTS = /home/paz2005/zeno/bin/src/subread-1.4.6-p4-source/bin/featureCounts
FREEBAYES = /zenodotus/abc/scratch/paz2005/bin/src/freebayes/bin/freebayes
VARSCAN = /zenodotus/abc/scratch/paz2005/bin/src/VarScan.v2.3.9.jar
SNPSIFT = /zenodotus/abc/scratch/paz2005/bin/SnpSift.jar
SNPEFF = /zenodotus/abc/scratch/paz2005/bin/snpEff.jar
VCF_COMPARE = /zenodotus/abc/scratch/paz2005/bin/vcf-compare
VCF_ISEC  = /zenodotus/abc/scratch/paz2005/bin/vcf-isec
VCF_MERGE =  /zenodotus/abc/scratch/paz2005/bin/vcf-merge
VCF_TO_TAB = /zenodotus/abc/scratch/paz2005/bin/vcf-to-tab
VCF_TO_BED = /zenodotus/abc/scratch/paz2005/bin/vcf2bed
QORTS = /zenodotus/abc/scratch/paz2005/bin/src/QoRTs_1.1.8/QoRTs.jar

### SCRIPTS
PREPARE_CMP_FOR_VENN = /scratchLocal/paz2005/hajjar-annexinA2/scripts/prepareCmpForVenn.sh
PLOT_VCF_COMPARE = /scratchLocal/paz2005/hajjar-annexinA2/scripts/plotVcfCmp.R
PLOT_INDIVIDUAL_QC = /scratchLocal/paz2005/hajjar-annexinA2/scripts/plotIndividualQC.R
PLOT_SUMMARY_QC = /scratchLocal/paz2005/hajjar-annexinA2/scripts/plotSummaryQC.R

### REFERENCES
REFERENCE_FASTA = /scratchLocal/paz2005/hajjar-annexinA2/ref/hg38p3.ANXA2.masked.fa
REFERENCE = /scratchLocal/paz2005/hajjar-annexinA2/ref/hg38p3.ANXA2.masked.fa
ANNOTATION = /scratchLocal/paz2005/hajjar-annexinA2/ref/gencode.v23.comprehensive.annotation.gtf
DB_SNP = /scratchLocal/paz2005/hajjar-annexinA2/ref/hg38bundle/Homo_sapiens_assembly38.dbsnp.vcf.gz
SAMPLE_INFO = /scratchLocal/paz2005/hajjar-annexinA2/hajjar_mapping.txt

### PARAMETERS
NUM_THREADS = 8
BWA_OPTIONS = -M -h 100 -L 50,50 -O 7
GATK_OPTIONS = -drf DuplicateRead
FREEBAYES_OPTIONS = --use-duplicate-reads
READ_LENGTH_MAX = 151
QORTS_OPTIONS = --runFunctions NVC,GCDistribution,QualityScoreDistribution,chromCounts,writeGenewiseGeneBody,writeGeneBody --maxReadLength $(READ_LENGTH_MAX) --minMAPQ 0 --keepMultiMapped --maxPhredScore 45

lc = $(subst A,a,$(subst B,b,$(subst C,c,$(subst D,d,$(subst E,e,$(subst F,f,$(subst G,g,$(subst H,h,$(subst I,i,$(subst J,j,$(subst K,k,$(subst L,l,$(subst M,m,$(subst N,n,$(subst O,o,$(subst P,p,$(subst Q,q,$(subst R,r,$(subst S,s,$(subst T,t,$(subst U,u,$(subst V,v,$(subst W,w,$(subst X,x,$(subst Y,y,$(subst Z,z,$1))))))))))))))))))))))))))


### DO NOT EDIT BELOW THIS LINE UNLESS YOU KNOW WHAT YOU ARE DOING
### TEXT TRANSFORMATION HELPERS
COMMA = ,
UNDERSCORE = _
EMPTY :=
SPACE := $(empty) $(empty)
define \n


endef

### VARIABLES
FASTQFILES := $(wildcard *_R1*.fastq.gz)
TRIMMED_FASTQFILES := $(patsubst %.fastq.gz,%_trimmed.fq.gz,$(wildcard *_R1.fastq.gz))
SAMPLES := $(sort $(foreach a,$(FASTQFILES), $(subst $(SPACE),$(UNDERSCORE),$(wordlist 1,3, $(subst _, ,$a)))))
SAMPLE_GROUPS := $(shell cat $(SAMPLE_INFO)| sed 1d | cut -f 4  | sort | uniq )
NUMBER_SAMPLES := $(shell cat $(SAMPLE_INFO) | sed 1d | wc -l )


all: haplotypecaller freebayes varscan vcf_compare
fastqc: $(patsubst %.fastq.gz,%_fastqc.zip,$(wildcard *_R1.fastq.gz))
trim: $(patsubst %.fastq.gz,%_trimmed.fq.gz,$(wildcard *_R1.fastq.gz))
align: $(TRIMMED_FASTQFILES:_trimmed.fq.gz=.sam) $(patsubst %.fastq.gz,%_trimmed.fq.gz,$(wildcard *_R1.fastq.gz))
sorted_bam: $(FASTQFILES:.fastq.gz=.sorted.bam)
merged_bam: $(addsuffix .merged.bam, $(SAMPLES))
qc_data: $(addprefix ./qc/, $(addsuffix /QC.summary.txt, $(SAMPLES)))
qc_plots: ./qc/individualPDFs/summary.table.txt ./qc/summaryPDFs/summary.table.txt
deduped_bam: $(addsuffix .merged.dedup.bam, $(SAMPLES)) $(addsuffix .merged.dedup.bam.bai, $(SAMPLES))
realn_bam: $(addsuffix .merged.dedup.realn.bam, $(SAMPLES)) $(addsuffix .merged.dedup.realn.bam.bai, $(SAMPLES))
recal_bam: $(addsuffix .merged.dedup.realn.recal.bam, $(SAMPLES)) $(addsuffix .merged.dedup.realn.recal.bam.bai, $(SAMPLES))
haplotypecaller: haplotypecaller.all_samples.vcf.gz.tbi $(addsuffix .haplotypecaller.vcf.gz, $(SAMPLES)) $(addsuffix .haplotypecaller.ann.vcf.gz, $(SAMPLES)) $(addsuffix .haplotypecaller.ann.vcf.gz.tbi, $(SAMPLES)) 
freebayes: freebayes.all_samples.vcf.gz.tbi $(addsuffix .freebayes.vcf.gz, $(SAMPLES)) $(addsuffix .freebayes.ann.vcf.gz, $(SAMPLES)) $(addsuffix .freebayes.ann.vcf.gz.tbi, $(SAMPLES))
mpileup: samtools.all_samples.mpileup
varscan: varscan.all_samples.vcf.gz.tbi $(addsuffix .varscan.vcf.gz, $(SAMPLES)) $(addsuffix .varscan.ann.vcf.gz, $(SAMPLES)) $(addsuffix .varscan.ann.vcf.gz.tbi, $(SAMPLES))
vcf_compare: $(addsuffix .vcf-compare.txt, $(SAMPLES)) $(addsuffix .vcf-compare.venn.pdf, $(SAMPLES))
vcf_intersection: $(addsuffix .vcf-intersection.vcf.gz, $(SAMPLES)) $(addsuffix .vcf-intersection.vcf.gz.tbi, $(SAMPLES)) $(addsuffix .vcf-intersection.snpeff.vcf.gz, $(SAMPLES)) $(addsuffix .vcf-intersection.snpeff.bed, $(SAMPLES)) $(addsuffix .intersect.vcf.gz.tbi,$(SAMPLE_GROUPS)) $(addsuffix $1.intersect.unique.vcf.gz.tbi, $(SAMPLE_GROUPS))  $(addsuffix .union.vcf.gz.tbi,$(SAMPLE_GROUPS)) $(addsuffix $1.union.unique.vcf.gz.tbi, $(SAMPLE_GROUPS)) per_sample_variant_table_from_intersections.txt


### FASTQC 
%_fastqc.zip: %.fastq.gz $$(subst R1,R2,%.fastq.gz)
	$(FASTQC) $^

%_fastqc.zip: %.fastq.gz
	$(FASTQC) $<

### TRIM GALORE
%_trimmed.fq.gz: %.fastq.gz
	$(TRIM_GALORE) --phred64 --quality 3 --stringency 10 --length 20 -fastqc $<

### ALIGNMENT
%.sam: %_trimmed.fq.gz
	$(BWA) mem $(BWA_OPTIONS) -R '@RG\tID:$(subst $(SPACE),$(UNDERSCORE),$(wordlist 1,3, $(subst _, ,$@)))\tSM:$(subst $(SPACE),$(UNDERSCORE),$(wordlist 1,3, $(subst _, ,$@)))\tLB:$(subst $(SPACE),$(UNDERSCORE),$(wordlist 1,3, $(subst _, ,$@)))\tPL:illumina\tPU:$(word 4, $(subst _, ,$@))' $(REFERENCE) $< >$@

### CONVERT SAM TO BAM
%.bam: %.sam
	$(SAMTOOLS) view -bS -q1 $< > $@

### SORT BAM FILES
%.sorted.bam: %.bam
	$(SAMTOOLS) sort -O bam -T $<.tmp $< > $@

### MERGE BAM FILES BY SAMPLE NAME
find-bam-files = $(sort $(filter $1_% , $(FASTQFILES:.fastq.gz=.sorted.bam)))

define merge-bam-files
$1.merged.bam: $(call find-bam-files,$1)
	$$(if $$(findstring 1, $$(words $$^)),$$(LN) -fs $$^ $$@,$(SAMTOOLS) merge -f $$@ $$^)
endef

$(foreach s,$(SAMPLES),$(eval $(call merge-bam-files,$s)))

### MARK DUPLICATES	
%.merged.dedup.bam: %.merged.bam
	$(JAVA) -Xmx4g -jar $(PICARD) MarkDuplicates VALIDATION_STRINGENCY=SILENT INPUT=$< OUTPUT=$@ METRICS_FILE=$(basename $@).metrics REMOVE_DUPLICATES=false

### INDEX DE-DUPLICATED BAM FILE	
%.merged.dedup.bam.bai: %.merged.dedup.bam
	$(SAMTOOLS) index $< 

### DEFINE INTERVALS TO TARGET FOR LOCAL REALIGNMENT
%.merged.dedup.intervals: %.merged.dedup.bam %.merged.dedup.bam.bai
	$(JAVA) -Xmx4g -jar $(GATK) -T RealignerTargetCreator -R $(REFERENCE_FASTA) -I $< -o $@ $(GATK_OPTIONS)

### PERFORM LOCAL REALIGNMENT AROUND INDELS
%.merged.dedup.realn.bam: %.merged.dedup.bam %.merged.dedup.intervals
	$(JAVA) -Xmx4g -jar $(GATK) -T IndelRealigner -R $(REFERENCE_FASTA) -I $< -targetIntervals $(word 2,$^) -o $@ $(GATK_OPTIONS)
	
### INDEX DE-DUPLICATED REALIGNED BAM FILE
%.merged.dedup.realn.bam.bai: %.merged.dedup.realn.bam
	$(SAMTOOLS) index $< 
	
### DETECT ERRORS IN BASE QUALITY SCORES
%.merged.dedup.realn.recal.table: %.merged.dedup.realn.bam %.merged.dedup.realn.bam.bai
	$(JAVA) -Xmx4g -jar $(GATK) -T BaseRecalibrator -R $(REFERENCE_FASTA) -I $< -knownSites $(DB_SNP) -o $@ $(GATK_OPTIONS)
	
### RECALIBRATE BASE QUALITY SCORES
%.merged.dedup.realn.recal.bam: %.merged.dedup.realn.bam %.merged.dedup.realn.recal.table %.merged.dedup.realn.bam.bai
	$(JAVA) -Xmx4g -jar $(GATK) -T PrintReads -R $(REFERENCE_FASTA) -I $< -BQSR $(word 2,$^) -o $@ $(GATK_OPTIONS)

### INDEX RECALIBRATED BAM FILE
%.merged.dedup.realn.recal.bam.bai: %.merged.dedup.realn.recal.bam
	$(SAMTOOLS) index $< 

### QC
./qc/%/QC.summary.txt: %.merged.dedup.realn.recal.bam %.merged.dedup.realn.recal.bam.bai
	$(MKDIR) -p ./qc/$* && raw=$$(echo $$(zcat $**_R1*.fq.gz | wc -l)/4 | bc) && if [ -f $**R2*.fq.gz  ] ; then $(JAVA) -Xmx20G -jar $(QORTS) QC $(QORTS_OPTIONS) --seqReadCt $$(echo $$raw) $< $(ANNOTATION) ./qc/$* ; else $(JAVA) -Xmx20G -jar $(QORTS) QC $(QORTS_OPTIONS) --singleEnded --seqReadCt $$(echo $$raw) $< $(ANNOTATION) ./qc/$* ; fi

### PLOT SUMMARY QC
./qc/summaryPDFs/summary.table.txt: decoder.txt
	$(MKDIR) -p ./qc/summaryPDFs && $(RSCRIPT) $(PLOT_SUMMARY_QC) $<

### PLOT INDIVIDUAL QC
./qc/individualPDFs/summary.table.txt: decoder.txt
	$(MKDIR) -p ./qc/individualPDFs && $(RSCRIPT) $(PLOT_INDIVIDUAL_QC) $<

### CALL VARIANTS GATK HAPLOTYPE CALLER
haplotypecaller.all_samples.vcf: $(addsuffix .merged.dedup.realn.recal.bam, $(SAMPLES))
	$(JAVA) -Xmx8g -jar $(GATK) -T HaplotypeCaller -R $(REFERENCE_FASTA) -nct $(NUM_THREADS) --dbsnp $(DB_SNP) --sample_ploidy 2 --genotyping_mode DISCOVERY --read_filter BadCigar --downsampling_type NONE --annotation AlleleBalanceBySample --annotation ClippingRankSumTest --output_mode EMIT_VARIANTS_ONLY $(addprefix -I , $^) -o $@ $(GATK_OPTIONS)

haplotypecaller.all_samples.vcf.gz: haplotypecaller.all_samples.vcf
	$(BGZIP) $<

haplotypecaller.all_samples.vcf.gz.tbi: haplotypecaller.all_samples.vcf.gz
	$(TABIX) $<

define split-gatk-vcf-files
$1.haplotypecaller.vcf.gz: haplotypecaller.all_samples.vcf.gz haplotypecaller.all_samples.vcf.gz.tbi
	$(JAVA) -Xmx2g -jar $(GATK) -T SelectVariants -R $(REFERENCE_FASTA) --downsampling_type NONE  --variant $$< -o $$@ -sn $1 -env -ef $(GATK_OPTIONS)

$1.haplotypecaller.ann.vcf.gz: $1.haplotypecaller.vcf.gz
	$(JAVA) -Xmx2g -jar $(SNPSIFT) annotate $(DB_SNP) $$< | $(BGZIP) -c > $$@
	
$1.haplotypecaller.ann.vcf.gz.tbi: $1.haplotypecaller.ann.vcf.gz
	$(TABIX) $$<
endef

$(foreach s,$(SAMPLES),$(eval $(call split-gatk-vcf-files,$s)))

### CALL VARIANTS WITH FREEBAYES
freebayes.all_samples.vcf: $(addsuffix .merged.dedup.realn.recal.bam, $(SAMPLES))
	$(FREEBAYES) $(FREEBAYES_OPTIONS) --fasta-reference $(REFERENCE_FASTA) $(addprefix -b , $^) > $@

freebayes.all_samples.vcf.gz: freebayes.all_samples.vcf
	$(BGZIP) $<

freebayes.all_samples.vcf.gz.tbi: freebayes.all_samples.vcf.gz
	$(TABIX) $<

define split-freebayes-vcf-files
$1.freebayes.vcf.gz: freebayes.all_samples.vcf.gz freebayes.all_samples.vcf.gz.tbi
	$(JAVA) -Xmx2g -jar $(GATK) -T SelectVariants -R $(REFERENCE_FASTA) --downsampling_type NONE  --variant $$< -o $$@ -sn $1 -env -ef $(GATK_OPTIONS)

$1.freebayes.ann.vcf.gz: $1.freebayes.vcf.gz
	$(JAVA) -Xmx2g -jar $(SNPSIFT) annotate $(DB_SNP) $$< | $(BGZIP) -c > $$@

$1.freebayes.ann.vcf.gz.tbi: $1.freebayes.ann.vcf.gz
	$(TABIX) $$<
endef

$(foreach s,$(SAMPLES),$(eval $(call split-freebayes-vcf-files,$s)))


### CALL VARIANTS WITH VARSCAN
samtools.all_samples.mpileup: $(addsuffix .merged.dedup.realn.recal.bam, $(SAMPLES)) $(addsuffix .merged.dedup.realn.recal.bam.bai, $(SAMPLES))
	$(SAMTOOLS) mpileup --excl-flags UNMAP,SECONDARY,QCFAIL -d 500000 --min-MQ 1 --no-BAQ --fasta-ref $(REFERENCE_FASTA) $(filter %.bam , $^) > $@

samples.list:
	echo -e $(subst $(SPACE),,$(foreach sample,$(SAMPLES),$(subst $(SPACE),$(UNDERSCORE),$(wordlist 1,3,$(subst _, ,$(sample))))"\n")) > $@ && sed -i '$$ d' $@

varscan.all_samples.vcf: samtools.all_samples.mpileup samples.list
	$(JAVA) -Xmx8g -jar $(VARSCAN) mpileup2cns $(word 1,$^) --vcf-sample-list $(word 2,$^) --output-vcf 1 --variants 1 > $@

varscan.all_samples.vcf.gz: varscan.all_samples.vcf
	$(BGZIP) $<

varscan.all_samples.vcf.gz.tbi: varscan.all_samples.vcf.gz
	$(TABIX) $<

define split-varscan-vcf-files
$1.varscan.vcf.gz: varscan.all_samples.vcf.gz varscan.all_samples.vcf.gz.tbi
	$(JAVA) -Xmx2g -jar $(GATK) -T SelectVariants -R $(REFERENCE_FASTA) --downsampling_type NONE  --variant $$< -o $$@ -sn $1 -env -ef $(GATK_OPTIONS)

$1.varscan.ann.vcf.gz: $1.varscan.vcf.gz
	$(JAVA) -Xmx2g -jar $(SNPSIFT) annotate $(DB_SNP) $$< | $(BGZIP) -c > $$@

$1.varscan.ann.vcf.gz.tbi: $1.varscan.ann.vcf.gz
	$(TABIX) $$<
endef

$(foreach s,$(SAMPLES),$(eval $(call split-varscan-vcf-files,$s)))


### CREATE VENN FROM ALL THREE VARIANT CALLERS PER SAMPLE
define vcf-compare
$1.vcf-compare.txt: $1.varscan.ann.vcf.gz $1.freebayes.ann.vcf.gz $1.haplotypecaller.ann.vcf.gz $1.varscan.ann.vcf.gz.tbi $1.freebayes.ann.vcf.gz.tbi $1.haplotypecaller.ann.vcf.gz.tbi
	$(VCF_COMPARE) -g $$(wordlist 1, 3, $$^) | $(GREP) ^VN | $(CUT) -f 2- > $$@

$1.vcf-compare.venn.pdf: $1.vcf-compare.txt
	$(PLOT_VCF_COMPARE) `$(PREPARE_CMP_FOR_VENN) $$<`
endef

$(foreach s,$(SAMPLES),$(eval $(call vcf-compare,$s)))


### PRINT INTERSECTION BETWEEN ALL THREE VARIANT CALLERS PER SAMPLE
define vcf-intersection
$1.vcf-intersection.vcf: $1.varscan.ann.vcf.gz $1.freebayes.ann.vcf.gz $1.haplotypecaller.ann.vcf.gz $1.varscan.ann.vcf.gz.tbi $1.freebayes.ann.vcf.gz.tbi $1.haplotypecaller.ann.vcf.gz.tbi
	$(VCF_ISEC) -n +3  $$(wordlist 1, 3, $$^) > $$@

$1.vcf-intersection.vcf.gz: $1.vcf-intersection.vcf
	$(BGZIP) $$<

$1.vcf-intersection.vcf.gz.tbi: $1.vcf-intersection.vcf.gz
	$(TABIX) $$<	

$1.vcf-intersection.snpeff.vcf.gz: $1.vcf-intersection.vcf.gz $1.vcf-intersection.vcf.gz.tbi
	$(JAVA) -Xmx8g -jar $(SNPEFF) eff -v GRCh38.82 $$< | $(BGZIP) -c > $$@ && $(TABIX) $$@

$1.vcf-intersection.snpeff.bed: $1.vcf-intersection.snpeff.vcf.gz
	$(ZCAT) $$< | $(VCF_TO_BED) --keep-header > $$@
endef

$(foreach s,$(SAMPLES),$(eval $(call vcf-intersection,$s)))

per_sample_variant_table_from_intersections.txt: $(addsuffix .vcf-intersection.vcf.gz, $(SAMPLES))
	$(VCF_MERGE) --collapse none $^ | $(VCF_TO_TAB) > $@


### PRINT COMPLEMENTS BETWEEN THE GROUPS OF SAMPLES
find-vcf-files = $(addsuffix .vcf-intersection.vcf.gz,$(shell cat $(SAMPLE_INFO) | grep $1 | cut -f 1))

define vcf-group-intersection
$1.intersect.vcf: $(call find-vcf-files,$1)
	$(VCF_ISEC) --force  -n +6 $$^ > $$@

$1.intersect.vcf.gz: $1.intersect.vcf
	$(BGZIP) $$<

$1.intersect.vcf.gz.tbi: $1.intersect.vcf.gz
	$(TABIX) $$<
endef

$(foreach g,$(SAMPLE_GROUPS),$(eval $(call vcf-group-intersection,$g)))


define vcf-complement
$1.intersect.unique.vcf: $(addsuffix .intersect.vcf.gz.tbi,$(SAMPLE_GROUPS))
	$(VCF_ISEC) --force --complement $1.intersect.vcf.gz $$(addsuffix .intersect.vcf.gz, $$(filter-out $1, $(SAMPLE_GROUPS))) > $$@

$1.intersect.unique.vcf.gz: $1.intersect.unique.vcf
	$(BGZIP) $$<

$1.intersect.unique.vcf.gz.tbi: $1.intersect.unique.vcf.gz
	$(TABIX) $$<
endef

$(foreach g,$(SAMPLE_GROUPS),$(eval $(call vcf-complement,$g)))


define vcf-group-union
$1.union.vcf: $(call find-vcf-files,$1)
	$(VCF_ISEC) --force  -n +0 $$^ > $$@

$1.union.vcf.gz: $1.union.vcf
	$(BGZIP) $$<

$1.union.vcf.gz.tbi: $1.union.vcf.gz
	$(TABIX) $$<
endef

$(foreach g,$(SAMPLE_GROUPS),$(eval $(call vcf-group-union,$g)))


define vcf-complement-union
$1.union.unique.vcf: $(addsuffix .union.vcf.gz.tbi,$(SAMPLE_GROUPS))
	$(VCF_ISEC) --force --complement $1.union.vcf.gz $$(addsuffix .union.vcf.gz, $$(filter-out $1, $(SAMPLE_GROUPS))) > $$@

$1.union.unique.vcf.gz: $1.union.unique.vcf
	$(BGZIP) $$<

$1.union.unique.vcf.gz.tbi: $1.union.unique.vcf.gz
	$(TABIX) $$<
endef

$(foreach g,$(SAMPLE_GROUPS),$(eval $(call vcf-complement-union,$g)))


#  /scratchLocal/paz2005/hajjar-annexinA2/hajjar_mapping.txt


### MERGE BAM FILES BY SAMPLE NAME

#define merge-bam-files
#$1.merged.bam: $(call find-bam-files,$1)
#	$$(if $$(findstring 1, $$(words $$^)),$$(LN) -fs $$^ $$@,$(SAMTOOLS) merge -f $$@ $$^)
#endef

#$(foreach s,$(SAMPLES),$(eval $(call merge-bam-files,$s)))


#############

### CALL VARIANTS WITH VARSCAN
#%.varscan.vcf: %.merged.dedup.realn.recal.bam %.merged.dedup.realn.recal.bam.bai
#	$(SAMTOOLS) mpileup --excl-flags UNMAP,SECONDARY,QCFAIL --min-MQ 1 --no-BAQ --fasta-ref $(REFERENCE_FASTA) $< | $(JAVA) -Xmx8g -jar $(VARSCAN) mpileup2snp --output-vcf  > $@

#%.varscan.vcf.gz: %.varscan.vcf
#	$(BGZIP) $<

#%.varscan.vcf.gz.tbi: %.varscan.vcf.gz
#	$(TABIX) $^
#varscan.all_samples.vcf: mpileup.all_samples.vcf
#	$(JAVA) -Xmx8g -jar $(VARSCAN) mpileup2snp $< --output-vcf --variants
#	$(FREEBAYES) $(FREEBAYES_OPTIONS) --fasta-reference $(REFERENCE_FASTA) $(addprefix -b , $^) > $@

#	 $(FREEBAYES_OPTIONS) --fasta-reference $(REFERENCE_FASTA) $(addprefix -b , $^) > $@


## VARIABLES
#$(subst $(SPACE),$(UNDERSCORE),$(wordlist 1,3, $(subst _, ,$@)))
#SAMPLES := $(sort $(foreach a,$(FASTQFILES),$(word 3, $(subst _, ,$a))))
#FLOWCELLS := $(sort $(join $(foreach a,$(FASTQFILES),$(firstword $(subst _, ,$a))), $(addprefix _, $(foreach a,$(FASTQFILES),$(word 2, $(subst _, ,$a))))))
#BARCODES :=  $(sort $(join $(join $(foreach a,$(FASTQFILES),$(firstword $(subst _, ,$a))), $(addprefix _, $(foreach a,$(FASTQFILES),$(word 2, $(subst _, ,$a))))), $(addprefix _, $(foreach a,$(FASTQFILES),$(word 3, $(subst _, ,$a))))))
#LANES := $(sort $(join $(join $(join $(foreach a,$(FASTQFILES),$(firstword $(subst _, ,$a))), $(addprefix _, $(foreach a,$(FASTQFILES),$(word 2, $(subst _, ,$a))))), $(addprefix _, $(foreach a,$(FASTQFILES),$(word 3, $(subst _, ,$a))))), $(addprefix _, $(foreach a,$(FASTQFILES),$(word 4, $(subst _, ,$a))))))

