## Genomic File Formats

These are the formats you will encounter regularly while handling genetic data. Spend some time thinking about and understanding what they contain, how these are generated, and how you can view them. Some example files for each format are contained in the examplefiles folder.

Many of these formats contain simple text, and can be viewed using the Linux 'cat'/'more'/'less' commands (.fastq, .bed, .vcf). A file that has the suffix .gz is a zipped file. It can be viewed using 'zcat'/'zmore'/'zless' instead of 'cat'/'more'/'less'.

Some of these files can be quite large, and running operations/analyses on the whole human genome can be quite long. One trick while working with these files is to split them up by chromosome. The same operation is then run independently on each chromosome file. It is important for bioinformaticians to know when this is okay and when this won't work.

1. .fa/.fasta: Contains sequence data. Contains simple text. Each sequence contained in the fasta file has a header line (which started with a '>')
Example: 
>Chr1_GrCH37
AATACCCGNNTCAAAAACCCCTTGGGGGGGGGGGGGGGGGCAAT
AATTCAACTGATCNATCATGGSTAGCTAGGTCAAAAAAAAAAAA

2. .fastq: This is the raw sequence data you get from a sequencing run. This contains read information unaligned to the reference genome. Each read you get from the sequencing machine has four lines: 
    
    A sequence identifier with information about the sequencing run and the cluster. The exact contents of this line vary by based on the BCL to FASTQ conversion software used.
    The sequence (the base calls; A, C, T, G and N).
    A separator, which is simply a plus (+) sign.
    The basecall quality scores. These are Phred scores, using ASCII characters to encode the numerical quality scores.

3. .sam: A fastq file only contains sequence reads. Now these have to be aligned to the reference genome. The output of this alignment is stored in sam files. To view a sam file, you use a program called *samtools*. 

Each line in a sam file contains information about a particular read, its sequence, its quality (how much you can trust it), and where it aligns to in the genome. 

4. .bam: Sam files are large! A .bam file is a compressed sam file, stored in binary format. That means if you try to view a bam file with 'more' or 'less' you will see gibberish.

6. .bed: This is a tab-delimited text file containing information about genetic regions of interest. For example, you might have a bed file where each line represents the regions covered by each gene. 
Each line represents a given region. It has at least three columns:
chromosome
start
end
more columns may represent more columns, like gene name etc.

7. .vcf. VCF is the standard file format for storing genetic variation data. A VCF file is a tab-delimited text file. The first few lines (which begin with '##') are comment lines that describe the contents of the file. These are followed by a header line (starting with a single '#') that contains the names of the columns. Then all following lines contain genetic variation data for each genetic variant that is tested. One variant per line. 
These are the column names:
#CHROM chromosome
POS position
ID variant ID (sometimes blank, not all variants have an ID)
REF reference allele
ALT alternative allele
QUAL quality score 
FILTER pass/fail (did this variant pass quality filters)
INFO any more information. If there is information here, the keys in this column have to be described in the comment lines above
FORMAT Information about the following columns, and what format it is presented in
GENOTYPE_SAMPLE1 Genotype of sample 1.
GENOTYPE_SAMPLE2 Genotype of sample2
...
The above is a vey brief description. This [link](https://samtools.github.io/hts-specs/VCFv4.2.pdf) has more detailed information on the VCF format.

8. GTF. The GTF, like a bed file, is a tab-delimited text file, usually containing genomic annotations. Each line corresponds to a region of the genome. The following are the columns.
chromosome name
annotation source	{ENSEMBL,HAVANA}
feature type 	{gene,transcript,exon,CDS,UTR,start_codon,stop_codon,Selenocysteine}
genomic start location 	integer-value (1-based)
genomic end location 	integer-value
score (may be empty) 
genomic strand 	{+,-}
genomic phase (may not be used)
additional information as key-value pairs
