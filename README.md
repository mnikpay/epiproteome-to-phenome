The aim of this package is to invetigate the contribution of epigenome-proteome pairs listed in our manuscript to a phenotype. Below, we describe each script and it's application:

The entire package can be obtained from [here](https://zenodo.org/record/5979701)

then it can be accessed as:
```
unzip locus_annotator.zip

chmod -R 700 ./locus_annotator

cd ./locus_annotator
```
To conduct an analysis, first, we need to pass a phenotype ID (from OpenGWAS db) to the first script. e.g.
```
bash obtain_gwas_data_p1.sh phenotype_ID
```
This script downloads the GWAS data for your phenotype of interest from the OpenGWAS db and prepares it in a format that is required by the second script. The script assumes access to bcftools is possible through the user PATH.

The second script examines the association of the identified biomakers with the phenotype of interest using Mendelian randomization, you can conduct a comprehensive search as:

```
while read line; do echo $line;bash generate_output_p3.sh $line phenotype_ID; done < probe.pairs
```
or subset the probe.list file to test a number of probes.

If you are using a computing cluster, you can replace the bash command with an equillent command (e.g. sbatch) to submit jobs to cluster.


The final script combines the findings and prepare the result file which describe the nature of association between biomarkers and the phenotype

```
while read line; do echo $line;sbatch generate_output_p3.sh $line phenotype_name; done < probe.pairs
```
