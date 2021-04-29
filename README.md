# ITDetect


## Introduction

ITDetect (Internal Tandem Duplication Detector) is a sensitive ITD variant caller for next-generation sequencing data.

It detects candidate ITD position from soft-clipped reads and determines if actual ITD may exist based on the reads whose alignment pattern supports presumed ITD. 

Its performance was validated using whole exome sequencing data of AML patient samples with FLT3-ITD.

ITD in FLT3 gene is well known as an indication for poor prognosis and >25% of AML patients are positive for FLT3-ITD.

Even though some ITD can be detected by popular variant callers such as Pindel as insertion, researchers can expect to find ITD with better sensitivity using ITDetect which is specifically designed for ITD detection.


## BAM files used in the paper

BAM files that were used in the paper are located in BAM directory.


## Installation

ITDetect is released in a precompiled binary package. For installation, download the package ([ITDetect.tar.gz](https://github.com/cpmsnuh/ITDetect/blob/main/ITDetect.tar.gz)) and unzip/untar it.

```bash
tar -xzf ITDetect.tar.gz
```

When you finish installation, under the installation directory (i.e. YOURPATH),

you can see three sub-directories such as /bin with ITDetect executable file, /lib with library files and /data with the sample data files for your test.

You can test ITDetect simply by running the executable ITDetect.jar file in YOURPATH/bin directory.

If you want to move the installation directory, just copy the whole directory including /bin and /lib directories.

ITDetect needs `Java Runtime Environment (> ver 1.8.0)` and `Python (> ver 3.7.0)`.

If you want a reference genome such as hs37d5, download the genome sequences and unzip/untar it. (recommended: hg19)


## Commands

To run ITDetect, you call ITDetect.py with mandatory parameters set as follows:

```bash
python ITDetect.py \
	-p [path to ITDetect] \
	-b [input BAM file] \
	-o [output VCF file] \
	-r [reference genome file] \
	-t [target gene region file]
```

•	The following parameters are mandatory.
```
-p (--path)	path to ITDetect
```

> path where you unzip ITDetect.tar.gz.

```
-b (--bam)	input BAM file
```

> For initial detection of candidate ITDs, ITDetect uses reads aligned as soft-clipped by aligner.

> BWA-mem is well known aligner allowing reads aligned soft-clipped.

> ITDetect has been only tested with BWA-mem generated BAM files so we highly recommend BWA-mem as your aligner for you to generate BAM file for ITDetect.

> Along with input BAM file, BAM index file (.bai) should be exist.

```
-o (--output)	output VCF file
```
> For each ITD called by ITDetect, additional information for the ITD (e.g. read count) is given in INFO column.

> The description for the information is in below.

```
-r (--reference)	reference genome file
```
> For reference genome file, both of fasta (.fa) and fasta index (.fai) files are required.

> To generate .fai file from .fa file, you can use samtools 
(e.g., samtools faidx hg19.fa)

•	The followings parameters are optional.

```
-c (--rcnt)     minimum number of support reads for the ITD called (default: 3)
```

```
-p (--repeat)   minimum number of repeats in the region where ITD is called (default: 10)
```

> In repeat regions, false positive insertion/deletion (including ITD) is often called.

> You can avoid it by filtering out candidate ITD in repeat regions.


```
-t (--target)	target gene file (default: FLT3.exon.14.15.hg19.txt)
```

> If this file is not given, ITDetect scan all regions where all reads in input BAM file are aligned.

> You can limit the search space with this target gene file. Each line of the file should be as follows:

> `[GeneName] [Chromosome] [StartPosition] [EndPosition]`

> Please refer the files `YOURPATH/data`

```
-m (--tmp)      temporary directory (default: output directory)
```

> While calling ITDs, ITDetect generates temporary files.

> You may not want to delete the files while ITD is running.

```
-v(--verbose)  Run ITDetect in verbose mode (default: disabled)
```

```
-h (--help)     Print help message
```

•	The description of TXT output:

```
INFO			Description
TotalReadCount	  	Total number of reads mapped to the variant position
RefReadCount		Total number of reference allele support reads
AltReadCount		Total number of alternative allele (ITD) support reads
VAF			Alternative allele fraction; AltReadCount/(RefReadCount+AltReadCount)
AR			Allelic Ratio; AltReadCount/RefReadCount
DupSize		     	ITD size (without inserted bases)
Insertion		Inserted bases between duplication
Gene			Gene name (as in target gene file (-t))
```

##Example

•	Command Example: S01_FLT3.bam

```bash
python $PATH/ITDetect.py \
	-p $PATH \
	-b $INPUT/"S01_FLT3.bam" \
	-o $OUTPUT/"S01.Panel.ITDetect.vcf" \
	-r $REFERENCE/hg19/hg19_1-22-X-Y-M.fa \
	-t $PATH/data/FLT3.exon.hg19.txt
```

•	Final Result Example: S01.Panel.ITDetect.vcf.filtered.result.txt
```

Chrom   StartPos        Ref     Alt     TotalReadCount  RefReadCount    AltReadCount    VAF     AR      DupSize Insertion       Gene
chr13   28608253        G       GAGATCATATTCATATTCTCTGAAATCAACGTAGAAGTACTCATTATCTGAGGAGCCGGTCACCCCT     352     337     15      0.0426  0.0445  63      CCT     FLT3

```

## Contact

If you have any questions, bugs to report, or suggestions, please send us an email.

[Heejun Jang](mailto:starz77@snu.ac.kr)

[Hongseok Yun](mailto:entropy.yun@gmail.com)


## Download

**Last Updated: 2021-04-12**

•	Entire Package: [ITDetect.tar.gz](https://github.com/cpmsnuh/ITDetect/blob/main/ITDetect.tar.gz)

•	README

**JAVA Runtime Environment**

•	JRE: [download site](https://java.com/download/)
	(Recommended version: v.1.8.0)

**Python**

•	Python: [download site](https://www.python.org/downloads/)
	(Recommended version: v.3.7.5)

**Reference Genome Sequence**

•	hg19, GRCh37 FASTA: [download site](https://gatk.broadinstitute.org/hc/en-us/articles/360035890711-GRCh37-hg19-b37-humanG1Kv37-Human-Reference-Discrepancies)

**Example Input Data**

• 	Download WES example Data (FLT3 region BAM): [download site](https://github.com/cpmsnuh/ITDetect/tree/example_WES)
	
	
	git clone https://github.com/cpmsnuh/ITDetect/ -b example_WES --single-branch <~/your_directory/example_WES>
	

• 	Download Panel-sequencing example Data (FLT3 region BAM): [download site](https://github.com/cpmsnuh/ITDetect/tree/example_Panel) 
	
	
	git clone https://github.com/cpmsnuh/ITDetect/ -b example_Panel --single-branch <~/your_directory/example_Panel>
	
