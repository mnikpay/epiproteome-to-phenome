### Description
The aim of this unix package is to investigate the contribution of epigenome-proteome biomarker pairs listed in our manuscript to a phenotype. Below, we describe each script and their use. Users can edit the scripts to meet their requirements.

The entire package can be obtained from [here](https://zenodo.org/record/6047689)

It can be accessed as:
```
unzip epiproteomics_package.zip

chmod -R 700 ./epiproteomics_package

cd ./epiproteomics_package
```
The first step is to obtain GWAS data for the phenotype of interest from the OpenGWAS db. This can be done by passing its phenotype ID (from OpenGWAS db) to the first script. e.g.
```
bash obtain_gwas_data_p1.sh ebi-a-GCST010780
```
In the above example, the script downloads the GWAS data for SARS-COV-2 and prepares it in a format that is required by the second script. 

The second script examines the association of the identified biomarkers (probes) with the phenotype of interest using Mendelian randomization, you can conduct a comprehensive search as:

```
while read line; do echo $line;bash mr_analysis_p2.sh $line phenotype_ID; done < probe.list
```
or subset the probe.list file to test a number of probes.

If you are using a computing cluster, you can replace the bash command with an equivalent command (e.g. sbatch) to submit jobs to the cluster.


The final script examines the results from the MR analysis (stored in phenotype ID.table file) and prepares the output file (named as phenotype ID.biomarker.pairs) which describes the nature of associations between biomarkers and the phenotype. 

```
while read line; do echo $line;bash generate_output_p3.sh $line phenotype_name; done < probe.pairs
```
Example of an output file that points higher methylation at ABO locus (measured by cg21160290 probe) contributes to severity of SARS-COV-2 infection by increasting the level of ABO protein (measured by ABO.9253.52.3 probe).

|Methylation_probe|Trait           |B        |SE       |P       |NSNP|Protein_probe|Trait           |B       |SE        |P       |NSNP|
|-----------------|----------------|---------|---------|--------|----|-------------|----------------|--------|----------|--------|----|
|cg22535403       |ebi-a-GCST010780|0.07|0.01|6.03E-09|9   |ABO.9253.52.3|ebi-a-GCST010780|0.07|0.01|4.5E-11|22  |

In the above table, the first six columns describe the nature of association between the methylation probe and the phenotype. The remaining columns describe the association between the protein probe and the phenotype. The sign of effect size (B) indicates the direction of association (i.e. a positive beta indicates higher level of the probe is associated with higher level/risk of the phenotype), SE indicates standard error, P indicates p-value, NSNP indicates the number of SNPs in the instrument used to examine the association between the probe and the phenotype.
