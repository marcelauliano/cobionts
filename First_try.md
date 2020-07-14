# IlPhaBuce1 filtering of PacBio CCS reads

This is a first try to identify co-bionts PacBio HiFi reads prior to assembly.

## Step 1: GC content - Producing a lavalamp plot
One of the first ideas is to plot the GC% of the reads. Lava lamp plots can show different GC content of symbiont species in the sample, for example. Bellow you find a 3D lavalamp plot for all IlPhaBuCe1 HiFi reads kmer=31. For more information on Lavalamp plots: https://github.com/wrf/lavaLampPlot


![Screenshot](image.png)


## GC% only for wolbachia reads
As the GC content of the wolbachia reads do not deviate much of the species reads we don't see them in the lavalamp plot.

![Screenshot](output_file.png)


# Step 2: Identifying co-bionts possible reads: 
# Wolbachia
I've downloaded 54 sequences of 16S wolbachia endosymbionts of various organisms from ENA, created an aligment from them with clustalw and have input it to a nhmmer search against all IlPhaBuce1 PacBio reads.

`nhmmer --cpu 30 --tblout <output.tbl> <all.HiFi.fasta>`

