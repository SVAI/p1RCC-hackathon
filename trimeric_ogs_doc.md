# Team name: trimericOGs
## Main project focus: Classifying Tumor Stages based on Structural Variants in Patient Data

***Our initial goal was to make a phylogenetic tree of all the patients based on the structural variants from their sequencing data in order to see if we could identify the progression of mutants in prcc as the cancer progresses into later stages.***

**Data Pipeline** 
We acquired structural variant data from [NIH Cancer Genome Atlas (TCGA)](https://portal.gdc.cancer.gov/exploration?filters=%7B%22op%22%3A%22and%22%2C%22content%22%3A%5B%7B%22op%22%3A%22in%22%2C%22content%22%3A%7B%22field%22%3A%22cases.disease_type%22%2C%22value%22%3A%5B%22Kidney%20Renal%20Papillary%20Cell%20Carcinoma%22%5D%7D%7D%2C%7B%22op%22%3A%22in%22%2C%22content%22%3A%7B%22field%22%3A%22cases.primary_site%22%2C%22value%22%3A%5B%22Kidney%22%5D%7D%7D%5D%7D&searchTableTab=cases) and transformed the data into a matrix where columns refered to gene corresponding to the structural vairant location and rows correspond to each patient (value of 1 means that patient has that structural variant, value of 0 means the patient does not). 

**Downstream Analysis**
The data matrix was then pipelined into [perfect phylogeny algorithm](https://github.com/mcmero/perfect_phylogeny). Tentatively, the algorithm failed to create a phylogenetic tree. (more comprehensive attempt tbd)

As a result, we proceeded to classify tumor stages by implementing a T-SNE and a decision tree separately.

**T-SNE implementaton:** T-SNE: a non-linear dimensionality reduction algorithm to explore our sparse high-dimensional data. In the plot, the color represents the stage of the patient, and 0 means the stage data was not available. From the plot we mostly see stochastic patterns across all stages. However, under closer observation, we see an interesting cluster right in the center.
![alt text](https://github.com/wugwhisperer/p1rcc-hackathon/blob/master/T-SNE%20Implementation/image.png)

At the center of the plot, we see a cluster of orange, which refers to stage 1 patients. However, we have 5 times as much stage 1 patient data than any other patients at later stages. Thus our alternative interpretation is that because we have more stage 1 patient data, we were able to observe a cluster. Thus, if we were given more data about patients of later stage carcinoma, then we would have been able to observe meaning clusters per later stage carcinomas.

Aa an improvement to this T-SNE classification, we would have done additional feature selection, and see if we can replicate the TSNE result on subsets of data. We would want to identify the most discriminating features to improve the clustering behavior. From there, we would add Bill’s structural variant data to see if his structural variant data clusters with other patients of the same stage and narrow down relevant structural variants unique to his stage.

**Decision Tree implementation:** Trees are constructed greedily. Thus, initial divisions have greatest ability to discriminate between stages of pRCC. The decision tree was used as an exploratory tool to identify potential genes mutated in late stage tumors.
![alt text](https://github.com/wugwhisperer/p1rcc-hackathon/blob/master/tree.png)


**More details can be found in following the presentation:**
[Final Presentation](https://docs.google.com/presentation/d/1osi2q12_nNaGA8KWcEz_bnAeZe2A7tEbwa1I5buVe4k/edit?usp=sharing)
