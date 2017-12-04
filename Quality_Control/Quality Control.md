# FINAL PROJECT #
## Quality Control ##

The RNA sequencing used in the analysis was a paired end sequencing using Sanger/Illumina 1.9, meaning we have two files per each sample. The original files are found in NCBI under the accession [GSE98379](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE98379). For the purpose of quality control we will work only with one of the samples under the code [SRR5488449.sra](ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByStudy/sra/SRP/SRP105/SRP105764/SRR5488449/).

1. In order to work with the data we have to convert the file from 
".sra" to ".fastq" format. This is done by using in Unix the tool called [toolkit](https://www.ncbi.nlm.nih.gov/books/NBK158899/). 

The steps are:

**i**. Dowload the package [sratoolkit](http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-win64.zip)
   
**ii.** In the shell of Unix type cmd.exe and then cd to the local directory where we have downloaded "sratoolkit".

**iii.** once we are inside the the folder we "cd" to the folder "bin" and then type *fastq-dump <Name of the project>*, in our case:

      $ fastq-dump SRR5488449
Once we type ls we can appreciate that the file was downloaded and it is now with the new format **.fastq**

      $ ls
		>> SRR5488449.fastq

The quality of the sequencies was done according to the paper with the program [FASTQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/). We download the program and unzip the files into a folder in a local directory. Once it is unzip, we run the "**run_fastqc.bat**", which is an interactive graphical application. Inside the application, we load manually the file "SRR5488449.fastq".

The [output](**PUT THE LINK OF THE GITHUB .HTML FOR THE OUTPUT**) of the program is shown below.

## Per Base Sequence Quality ##

According to the graph we can appreciate that we have some skewness towards the right since the median value is close to the third interquantile (the yellow boxes represents the Interquantile range, 25 and 75%). The mean quality (blue line) and the interquantile range are in the portion of very good quality calls (green section) even for long runs (195-199). However, a warning could be noticed for one read from 94 to 104, and two reads between 195-199 in which the lower quartile (10%) is below 10 in the quality scores (y-axis). More information is found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/2%20Per%20Base%20Sequence%20Quality.html).

## **Per Tile Sequence Quality** ##

This graph is only display for analysis in which an illumina library was used, due to they retains the original sequence identifier. This graph allow us to associate the quality to a portion of the flowcell. We can appreciate that the graph is practically blue indicating that the quality was very good with just a few spots where the quality decays (yellow-green points in the graph). This is an evidence that the quality was at or above the average quality for each tile. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/12%20Per%20Tile%20Sequence%20Quality.html)

## **Per Sequence Quality Scores** ##

This graph help us to see if a subset of the sequences has low quality values. The most frequently observed mean quality is above 27, meaning we are above a 0.2% error rate. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/3%20Per%20Sequence%20Quality%20Scores.html) 

## **Per Base Sequence Content** ##

This plots the proportion of each of the DNA bases in the position for which the bases has been called. When lookin at the graph we will expect the lines to be parallel to each others, however, we can appreciate a little bias in the analysis. This bias could be due to the use of random hexamers, introducing a number of different k-mers at the 5' end. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/4%20Per%20Base%20Sequence%20Content.html).


## **Per Sequence GC Content** ##

We can appreciate a fairly normal distribution with a little skew to the right. The graph shows the theoretical GC content in the genome as around 45%. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/5%20Per%20Sequence%20GC%20Content.html)

## **Per Base N Content** ##

According to the graph, the sequencing was able to call all the bases with sufficient confidence and for that the line is in the point of 0 for the y-axis. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/6%20Per%20Base%20N%20Content.html)

## **Sequence Length Distribution** ##
We can appreciate here the distribution of fragment sizes in the file. Heving only one peak means that we have uniform length of the sequence fragments 199 and 201bp. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/7%20Sequence%20Length%20Distribution.html)

## **Sequence Duplication Levels** ##

The low values duplication indicate a very high level of coverage of the target sequence, with some enrichment bias. The second peak in the blue line is indicating a number of different highly duplicated sequences. Thus, they have to pay attention to this in order to clarify if this is due to contaminant sets or a severe technical duplication. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/8%20Duplicate%20Sequences.html)

## **Overrepresented Sequences** ##

This represent those sequences in the first 100.000 sequences of the file that are overrepresented in the whole sequence data. When looking at the possible source of hits, we find that these 5 sequences do not have any other match suggesting that they are not adapters. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/9%20Overrepresented%20Sequences.html)

## **Adapter Content** ##

According to the cumulative graph we can appreciate that the count of adapters start at position 45 bp, with the maximum at 89bp, but the frequency is below 5% indicating that there is not warning. The [nextera transposase sequence](https://support.illumina.com/content/dam/illumina-support/documents/documentation/chemistry_documentation/experiment-design/illumina-adapter-sequences-1000000002694-03.pdf) is a type of adapter used by Illumina.More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/10%20Adapter%20Content.html)

## **Kmer Content** ##

This graph is shwing us the top 6 kmer of 7 bp with a significant deviation from an even coverage at all positions. More information can be found [here](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/11%20Kmer%20Content.html)

The above analysis shows a little concern about the quality of the sequences forcing the authors to make a trimming process. Thus, the author removes primer contamination and adaptors using the program **cutadapt_v.1.13** and **Trimmomatic**. 

**# CutAdapt version 1.14 #**
The latest version of program is downloaded in [here](http://cutadapt.readthedocs.io/en/stable/installation.html) or by using the following command in Linux:

	$ pip install --user --upgrade cutadapt 

We have problems in the use of this program since apparently this one is not able to run in a Windows environment. However, The command that should be used is the following 

	$ cutadapt -q 20 -u 10 -m 20 -o <Output file.fatq> <Input <file.fastq>
Where the options q is the threshold qphred set up to 20; the option u is to remove kmers localized at the beginning of the sequences (we can use a length of 10 bp to remove them); and the option m is to remove the empty and/or short reads using a length of 20 bp.

After that the file should be analyzed again using the program FASTQC. Usually the overrepresented sequences are kept and thus a step to remove them from the analysis id required. To do so, we should run the following command:

	$ cutadapt -a <overrepresented sequence provided by FASTQC> -o <output file.fastq> <input file.fastq>
 
After this the files should be in shape to be used in Alignment or mapping analysis.


**#TRIMMOMATIC#**

The program should be download to our local machines following this link [TRIMMOMATIC](http://www.usadellab.org/cms/?page=trimmomatic). After installing the program we run it using GIT BASH as follows:

	$ java -Xmx2g -classpath ~/trimmomatic.jar org.usadellab.trimmomatic.TrimmomaticSE -phred33 SRR5488449.fastq SRR5488449_trimmed.fastq ILLUMINACLIP:contaminants.fasta:2:40:12 LEADING:10 TRAILING:10 SLIDINGWINDOW:4:18 MINLEN:20

The program trimmomatic requires java in order to run. The option xmx indicates the maximum size of memory allocation. The ~/trimmomatic is invoking the executable of the program. We have to indicate the path of the folder in which the executable is located. At the same time we clarify to the program the type of phred we have in our sequences. 

In order remove contaminants in Illumina analysis we indicate to the program the option "ILLUMNACLIP:contaminants.fasta:2:40:12". The option LEADING is used here to Cut bases off the start of a read (Kmers), if below a threshold of 10bp specified here. The remotion of empty reads or short reads we use the option MINLEN:20. 

After this we have to run again the command specifing to the program how to remove over represented sequences and nextera adapters. The following command should be used:

	$ java -Xmx2g -classpath ~/trimmomatic.jar org.usadellab.trimmomatic.TrimmomaticSE -phred33 SRR5488449_trimmed.fastq SRR5488449_trimmed_adapters.fastq ILLUMINACLIP:NexteraPE-PE.fa:2:30:10 LEADING:5 TRAILING:10 SLIDINGWINDOW:4:18 MINLEN:20

After this analysis we proceed to run the files in the FASTQC program. We have some problems in the remotion of overrepresented sequences and thus our FASTQC program output does not show this problems as fixed.
Finally, after this the files should be in shape to be used in Alignment or mapping analysis.

