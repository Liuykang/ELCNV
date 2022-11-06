# IhybCNV

IhybCNV: An intra-hybrid approach for CNV detection from next-generation sequencing data </br>

# Usage

1. API for the entire process

(1) open the file `run.py`, and modify the variables `bam_path` and `fa_path` inside;

```python
if __name__ == '__main__':
    # Local path of the *.bam file
    bam_path = r"/real_data/NA19238.chrom21.SLX.maq.SRP000032.2009_07.bam"
    
    # Local path of the *.fasta file or the *.fa file
    fa_path = r"./data/chr21.fa"
    
    # Local path of the ground truth of the sequenced sample.
    gt_path = r"./data/NA19238.gt"
    
    # parameter setting of the preprocessing
    bin_size = 1000  # the bin size ('1000' by default)

    main(bam_path, fa_path, gt_path=gt_path, bin_size=bin_size, cbs_imp='python')
```

   (2) run the `run.py`;

   (3) check the `main` function in the file `run.py` for more information.

2. API only for the core module of the IhybCNV

```python
from ihybcnv import IhybCNV

ihybcnv = IhybCNV()

# 0 stands for inliers and 1 for outliers(CNVs).
# labels with different merging strategies are obtained by the IhybCNV and the BCM method
labels = ihybcnv.fit_predict(X) 

# If you only need anomaly score vectors with different merging strategies.
scores = ihybcnv.decision_function(X)
```

3. API only for the BCM method

```python
'''
    A new non-parametric adaptive threshold without an assumption of any distributions.
    This method first employs the kernel density estimation (KDE) method
    with default parameters to estimate the probability density function
    of the outlier score vector, then leverages the 2-means method to
    bi-cluster its probability density. 
    
    This model can convert anomaly scores into a collective of binary labels that can 		
    indicate whether each point is outliers or not.
'''
from bcm import BCM

clf = BCM()
clf.fit(X)

# 0 stands for inliers and 1 for outliers(CNVs).
labels = clf.labels_

```

# Real Datasets

The real datasets can be obtained in the following 2 ways.

- clink this link：https://pan.baidu.com/s/1Ja4XH2wZupeAcwc9qhZn8A extraction code：29to
- [1000 Genomes Project](https://www.internationalgenome.org/)

# Required Dependencies

1. Python 3.8            
   - biopython     1.78
   - combo         0.1.1
   - numpy         1.18.5
   - pandas        1.0.5
   - pysam         0.16.0.1
   - pyod          0.8.4
   - rpy2          3.4.2
   - scikit-learn  0.23.1
   - scipy         1.5.0
2. R 3.4.4
   - DNAcopy

# Citing IhybCNV

[IhybCNV](https://www.sciencedirect.com/science/article/pii/S1051200421003432?via%3Dihub) is published in [Digital Signal Processing](https://www.journals.elsevier.com/digital-signal-processing). If you use this code in your work, we would like to cite the following paper.

```
@article{XIE2022103304,
	title = {IhybCNV: An intra-hybrid approach for CNV detection from next-generation sequencing data},
	journal = {Digital Signal Processing},
	volume = {121},
	pages = {103304},
	year = {2022},
	issn = {1051-2004},
	doi = {https://doi.org/10.1016/j.dsp.2021.103304},
	url = {https://www.sciencedirect.com/science/article/pii/S1051200421003432},
	author = {Kun Xie and Kang Liu and Haque A.K. Alvi and Wenyue Ji and Shuzhen Wang and Liang Chang and Xiguo Yuan},
}
```

