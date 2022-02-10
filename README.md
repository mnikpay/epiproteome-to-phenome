# Connecting epiproteome biomarkers to phenome
The aim of this unix package is to invetigate the contribution of epigenome-proteome pairs listed in our manuscript to a phenotype. Below, we describe each script and it's application:

## Getting Started

The entire package can be obtained from [here](https://zenodo.org/record/5979701)

then access it as:
```
unzip locus_annotator.zip

chmod -R 700 ./locus_annotator

cd ./locus_annotator
```
To conduct a search, the locus coordinate and the phenotype name must be passed to the wrapper script.

Example1 with genomic position:
```
bash wrapper.sh chr5:95734724 BMI_PMID30239722
```


Example2 with genomic range:
```
bash wrapper.sh chr19:45409039-45412650 LDL_PMID24097068
```
