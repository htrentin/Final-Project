# Alignment or Mapping #

After the quality control procedure we proceed to do the alignment to the 726 maize genome ([AGPv3, INSEC Assembly GCA_000005005.5, release 23, 727](ftp://ftp.ensemblgenomes.org/pub/plants/)). To do the alignment the authors of tge paper work with [STAR package](http://labshare.cshl.edu/shares/gingeraslab/www-data/dobin/STAR/STAR.sandbox/doc/STARmanual.pdf). The [command](http://homer.ucsd.edu/homer/basicTutorial/mapping.html) to do the alignment is:
	
> Build genome index:
> 
	$ STAR  --runMode genomeGenerate --runThreadN <# cpus> --genomeDir <genome output directory> --genomeFastaFiles <input Genome FASTA file>
>Align RNA-Seq Reads to the genome:
>
	$ STAR --genomeDir <Directory with the Genome Index>  --runThreadN <# cpus> --readFilesIn <FASTQ file> --outFileNamePrefix <OutputPrefix>

The package STAR will create several output files from which the "*.Aligned.out.sam" is the most importan, since this one was the file used to make the Differential expression analysis using the featureCounts() function in R.
