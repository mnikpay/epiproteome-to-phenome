## Description
The aim of this package is to investigate the contribution of epigenome-proteome biomarker pairs listed in our manuscript to a phenotype. Below, we describe each script and it's application:

The entire package can be obtained from [here](https://zenodo.org/record/5979701)

then it can be accessed as:
```
unzip locus_annotator.zip

chmod -R 700 ./locus_annotator

cd ./locus_annotator
```
The first step is to obtain GWAS data for the phenotype of interest from OpenGWAS db. This can be done by passing its phenotype ID (from OpenGWAS db) to the first script. e.g.
```
bash obtain_gwas_data_p1.sh ebi-a-GCST010780
```
downloads the GWAS data for SARS-COV-2 and prepares it in a format that is required by the second script. This script assumes access to bcftools is possible through the user PATH.

The second script examines the association of the identified biomarkers (probes) with the phenotype of interest using Mendelian randomization, you can conduct a comprehensive search as:

```
while read line; do echo $line;bash mr_analysis_p2.sh $line phenotype_ID; done < probe.list
```
or subset the probe.list file to test a number of probes.

If you are using a computing cluster, you can replace the bash command with an equivalent command (e.g. sbatch) to submit jobs to the cluster.


The final script combines the findings and prepares the output file which describes the nature of association between biomarkers and the phenotype. 

```
while read line; do echo $line;bash generate_output_p3.sh $line phenotype_name; done < probe.pairs
```
Example of an output file that points to the association of ABO locus and severity of SARS-COV-2 infection.

|Methylation_probe|Trait           |B        |SE       |P       |NSNP|Protein_probe|Trait           |B       |SE        |P       |NSNP|
|-----------------|----------------|---------|---------|--------|----|-------------|----------------|--------|----------|--------|----|
|cg21160290       |ebi-a-GCST010780|0.0597921|0.0102896|6.21E-09|7   |ABO.9253.52.3|ebi-a-GCST010780|0.064296|0.00986188|7.05E-11|23  |

Each row in the result file lists the association between a pair of biomarkers and the phenotype. The first column indicates methylation probe, second column is the phenotype ID and columns 3rd to 6th represent summary statistics from the Mendelian randomization test (B, SE, P and NSNPs). The content of remaining columns are similar to the previous columns except they describe the association between the protein probe and the phenotype.
