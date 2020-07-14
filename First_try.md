# IlPhaBuce1 filtering of PacBio CCS reads

This is a first try to identify co-bionts PacBio HiFi reads prior to assembly.

## Step 1: GC content - Producing a lavalamp plot
One of the first ideas is to plot the GC% of the reads. Lava lamp plots can show different GC content of symbiont species in the sample, for example. Bellow you find a 3D lavalamp plot for all IlPhaBuCe1 HiFi reads kmer=31. For more information on Lavalamp plots: https://github.com/wrf/lavaLampPlot


![Screenshot](image.png)


## GC% only for wolbachia reads
As the GC content of the wolbachia reads (indentifed after assembly) do not deviate much of the species reads we don't see them in the lavalamp plot.

![Screenshot](output_file.png)


# Step 2: Identifying co-bionts possible reads: 
## Wolbachia
I've downloaded 54 sequences of 16S wolbachia endosymbionts of various organisms from ENA, created an aligment from them with clustalw and have input it to a nhmmer search against all IlPhaBuce1 PacBio reads.

`hmmbuild --dna wolbachia.ena.some.hmm  wolbachia.ena.fasta.aln`
`nhmmer --cpu 30 --tblout <output.tbl> wolbachia.ena.some.hmm <all.HiFi.fasta>`

> This has identified 9271 reads. 

### Step 2.2: Clustering
So the next idea was to take these first identified reads cluster them and inquire if it would be worth to search more deeply for reads of this organism to do genome assembly. I have used PacBio tool pbampliconclustering for such https://github.com/PacificBiosciences/pbampliconclustering 

`python /software/team311/mu2/pbampliconclustering/ClusterAmplicons.py cluster -j 20 -g 2 -X -p <out.file> -F -Q <fastq_file_to_cluster.fasq>`

