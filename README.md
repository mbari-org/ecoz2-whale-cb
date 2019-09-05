# LPC Based K-Means Clustering on Whale Vocalizations

> Note: all generated data and plots are committed to this repository.
> See the setup section below if you want to reproduce the exercises.

The exercises described here follow Juang et al (1982) for the implementation 
of the algorithm for codebook generation as well as in terms of corresponding
evaluation based on distortion performance. 
A general overview of LPC can be found on [wikipedia](https://en.wikipedia.org/wiki/Linear_predictive_coding).
In our case, we are exploring this technique for clustering of whale sounds.

In short, the steps followed in each exercise below are:

- LPC analysis to generate training vectors for clustering from a given
  whale sound file. This generates a single "predictor" file containing
  all the LPC vectors for codebook training.
  
- Codebook generation, inspection, and evaluation.
  This includes plots of distortion, σ-ratio, and inertia as functions
  of codebook size; cell cardinality and distortion; and visualization of
  the clusters and centroids based on the first couple of
  reflection coefficients associated with the prediction coefficients.

### Exercises

- [HBSe_20161221T010133](HBSe_20161221T010133/README.md)
- [HBSe_20170128T231621](HBSe_20170128T231621/README.md)

## Setup

To facilitate reproducibility this repository has [ecoz2](https://github.com/ecoz2/ecoz2)
as a submodule (to point to a particular version).

    $ git clone --recursive https://github.com/ecoz2/ecoz2-whale-cb.git
    $ cd ecoz2-whale-cb
    # Build ecoz2 executables:
    $ cd ecoz2/
    $ make
    $ export PATH=`pwd`/_out/bin:$PATH
    $ export PATH=`pwd`/src/py:$PATH
    $ pip install pandas matplotlib 
    $ cd ..
    

----

Juang, B-H., Wong, D.Y., Gray, A.H.,
"Distortion Performance of Vector Quantization for LPC Voice Coding,"
IEEE Trans. ASSP, Vol. 30, No. 2, April, 1982.
DOI: [10.1109/TASSP.1982.1163866](https://doi.org/10.1109/TASSP.1982.1163866)
