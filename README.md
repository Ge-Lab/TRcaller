# TRcaller
Precise and ultrafast tandem repeat variant detection

* High accuracy - 99% accuracy tested with 1000 genomes data

* Ultrafast - Get results in seconds

* Platform independent - Process both short and long reads

* Scalability - Process both whole genome and targeted sequences

## Introduction
TRcaller is a software program to precisely and quickly detect tandem repeats (TR) in DNA sequences. With the targeted TR regions defined, TRcaller is able to call the TR alleles from either short or long read sequences, either whole genome or targeted sequences, in just a few seconds with >99% accuracy.

There is no minimum read depth required for the input BAM file. TRcaller only detects the TR alleles that span the whole TR region and does not connect the multiple broken reads to infer potential long TR alleles. We recommend using long-read sequencing technology to generate sequences to detect TR alleles longer than 250bp.

For loci with uncertain ploidy, such as human X chromosome STR, it is recommended to put the maximum number of ploidy in the loci config file. Therefore, TRcaller may detect multiple alleles than expected. For example, TRcaller will output two alleles for an X-STR locus, as the ploidy of X-STR is set as 2 in the predefined loci config file and the gender of the sample is not a parameter for TRcaller. It would be the user’s discretion to decide whether the minor allele is a true allele or noise.

## Access to TRcaller

Go to TRcaller website, https://trcaller.com/index.aspx

## Preprocessing Tools

### Sort and index BAM
If the input BAM file is not sorted or indexed, please use one of the following methods to sort and index the BAM file, because TRcaller only accepts the sorted and indexed BAM file as input.

Method 1:

Use samtools commands, “samtools sort” and “samtools index”. The details of samtools can be found at https://github.com/samtools/samtools.

    Command:

        samtools sort -o input.sort.bam -O bam input.bam

        samtools index -b input.sort.bam

Method 2:

Download BamAlignSortIndex.jar and run the following command on your local computer. This tool has been tested on Windows, Linux, and MacOS. Please make sure you have the latest version of JAVA installed, https://www.oracle.com/java/technologies/downloads/.

    Command:

        java -jar BamAlignSortIndex.jar input.bam

The command will generate two output files, input.sort.bam and input.sort.bam.bai, which are ready to upload to TRcaller website.


### Reduce the size of BAM input file

Although TRcaller can process sorted and indexed BAM files with any size, the server may not be able to handle large BAM files due to limited resources. If the BAM file size is larger than the current limit, please reduce the BAM file size before uploading the BAM file using one of the following two methods.

Method 1:

Download BamSubset.jar and run the following command on your local computer. This tool has been tested on Windows, Linux, and MacOS. Please make sure you have the latest version of JAVA installed, https://www.oracle.com/java/technologies/downloads/. The output BAM file will be sorted and indexed.

    java -jar BamSubset.jar Bed_file Input.bam reduced_input.bam

For example,

    java -jar BamSubset.jar STR.bed in.bam in.reduced.bam

Method 2:

Use the samtools command view. The details may be found at http://www.htslib.org/doc/samtools-view.html. For example, for samtools version 1.13, and run with two threads

    samtools view --region-file STR.bed --output in.reduced.bam -@ 2 in.bam

where the in.reduced,bam is the reduced bam file.


## Citation

Please cite this work:

Xuewen Wang, Meng Huang, Bruce Budowle, Jianye Ge. 2023. Precise and ultrafast tandem repeat variant detection in massively parallel sequencing reads. bioRxiv 2023.02.15.528687 https://www.biorxiv.org/content/10.1101/2023.02.15.528687v1

## Contact

Please send questions to jianye.ge@unthsc.edu, gejianye@gmail.com, xuewen.wang@unthsc.edu, or xwang.kib@gmail.com
