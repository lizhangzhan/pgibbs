pgibbs - Parallel Gibbs Sampling
================================

by [Graham Neubig](http://www.phontron.com)

This package implements parallel Gibbs sampling using both blocked and multi-sampler methods. The two executables are src/bin/pgibbs-ws for word segmentation and src/bin/pgibbs-hmm for POS tagging.
You can find more details in the following paper:

"[Simple, Correct Parallelization for Blocked Gibbs Sampling](http://www.phontron.com/paper/neubig14pgibbs.pdf)".
Graham Neubig.
Technical Report. 2014.

Data Preparation
----------------

In order to replicate our experiments, you must have the Chinese Treebank 5.0, which can be obtained from the LDC (details [here](http://www.ldc.upenn.edu/Catalog/CatalogEntry.jsp?catalogId=LDC2005T01)).

For HMM-based tagging, the input is divided into words:

上海 浦东 开发 与 法制 建设 同步

And for word-segmentation, the input is divided into characters:

上 海 浦 东 开 发 与 法 制 建 设 同 步

Running Experiments
-------------------

Both programs can be run with

    pgibbs-{ws,hmm} [OPTIONS] INPUTDATA OUTPUTPREFIX

The input data is the previously mentioned files, and the output data is a prefix where the label files will be written. The major options used are as follows:

    -iters 2000             // The number of iterations
    -threads {1,2,4,8}      // The number of threads to use
    -blocksize {1,2,4,10,20,40,100} // The size of a single block for blocked sampling
    -sampmeth {block,parallel} // Whether to perform blocked or parallel sampling
    -skipiters {0,2000}     // Will skip a Metropolis-Hastings rejection for a certain
                            //  number of iterations, when set equal to the number of
                            //  iterations, MH will not be performed

For word segmentation only:

    -n 2                    // The n-gram size of the model

For HMM only:

    -classes 30             // The number of classes in the model