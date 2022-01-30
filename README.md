# DNA Project

Find proximity between species using DNA database

## Resources

* [Find a species](https://www.ncbi.nlm.nih.gov/search/all/?term=bee)
* [Species info](https://www.ncbi.nlm.nih.gov/data-hub/taxonomy/7460/)
* [Kaggle algo](https://www.kaggle.com/cdeotte/rapids-genetic-algorithm-knn-cv-0-01840) to compare
* [Cross-Species Sequence comparisons](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC430969/)
* [Multiple sequence aligment](https://en.wikipedia.org/wiki/Multiple_sequence_alignment)
* [Supported languages](https://www.ncbi.nlm.nih.gov/datasets/docs/v1/languages/python/)


## Solutions

### Solution 1 - Compare genes

1. Recognize genes
2. compare genes between species (how many similar nucleotides?)

Seems good because ncbi also gives genome with all separated genes of a species:
* how much of the all DNA does the genome represent?
* do gene comparison between species "work" ? (sequences similarities to check)

Example:

```
cat bee-genome/ncbi_dataset/data/GCF_003254395.2/cds_from_genomic.fna | grep ">lcl|" | awk '/gene/{ print $2 }' > bee.genes
cat fly-genome/ncbi_dataset/data/GCA_005959815.1/cds_from_genomic.fna | grep ">lcl|" | awk '/gene/{ print $2 }' > fly.genes
```

### Solution 2 - Compare words

1. Small enough slices to belong to a single gene, but large enough to be significant
2. Compare slices with a tolerance (to allow alleles match)
  * slices of same size with offset can make same gene mismatch
  * first "find a zone", then compare (mismatch should be visible after few nucleotides, e.g. 100)
3. Appliquer un ratio pour "exclure" les cas des slices cross-genes

This basic alg could be ok, but we should before make a test telling, among a single species, if the gene is well recognized and no confusion is made with other similar genes.

Then try to find a gene common with another species and see if it is correctly found

### Solution 3 - Use a Phylogenetic tree

[Wikipedia](https://en.wikipedia.org/wiki/Phylogenetic_tree)



