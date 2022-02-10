## Getting Started

The aim of this unix package is to invetigate the contribution of epigenome-proteome pairs listed in our manuscript to a phenotype. Below, we describe each script and it's application:

The entire package can be obtained from [here](https://zenodo.org/record/5979701)

then access it as:
```
unzip locus_annotator.zip

chmod -R 700 ./locus_annotator

cd ./locus_annotator
```
To conduct an analysis, first, you need to pass the phenotype ID (based on OpenGWAS db) to the first script. e.g.

This script downloads the GWAS data for your phenotype of interest from the OpenGWAS db and prepare it in a format that is required by the second scripts. The script assumes op is accessible through your path.

The second script examines the association of the identified biomakers with the phenotype of interest using Mendelian randomization, you can conduct a comprehensive search as:


Example1 with genomic position:
```
while read line; do echo $line;sbatch generate_output_p3.sh $line phenotype_name; done < probe.pairs
```
or subset the probe.list file to test a number of probes.

```
bash wrapper.sh chr5:95734724 BMI_PMID30239722
```

The final script combines the findings and prepare the result file which describe the nature of association between biomarkers and the phenotype

```
while read line; do echo $line;sbatch generate_output_p3.sh $line phenotype_name; done < probe.pairs
```
