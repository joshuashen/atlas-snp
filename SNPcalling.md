Note: this is a version before atlas-snp-evaluate.rb was written. Please keep in mind that this is not the optimal way to do SNP filtering anymore.

This program outputs raw SNP calling result. In order to improve the accuracy, we need to set up a series of filters to discard potential false positives. Here is a list of factors that are useful:

  1. number of SNP reads: the more reads agree upon a SNP, the less likely that the SNP is caused by sequencing errors
  1. coverage of the base: ignore the base if the coverage is larger than certain cutoff value -- analogous to repeats cutoff in genome assembly.
  1. adjusted quality score: quality score is an estimate of the probability that this base-substitution is caused by sequencing errors. It is not independent of number of SNP reads, but contains new information
  1. strand: a substitution is less likely to be caused by 454 sequencing errors if the SNP reads are from both strands.
  1. homopolymer-run size: in 454 sequencing, both substitution and indel errors are closely related to homopolymer runs.
  1. base-swapping: about 20% of 454 substitution errors appear to be swapped sequences between two consecutive bases.
  1. ratio of SNP reads vs coverage: for a diploid genome, the number of SNPs reads should follow binomial distribution, given the coverage and the SNP is heterozygous.


### Quality assessment of the SNP calling. ###

Ideally we should do independent experiments to validate the SNPs. Computationally we can rely on the chemistry of DNA mutation: the transition / transversion ratio. Assuming the true SNPs are results of naturally occurred DNA mutation, the transition/transverion ratio should be close to 2/1 for human (Please note this number might be different to other species). The substitutions from 454 sequencing errors are assumed to be random nucleotide changes, so the ratio is 1:2. Thus we could use a set of two equations based on the base-change spectrum to estimate the false positive rate of SNP calling. Let x, y be the proportion of true SNPs and false SNPs respectively, and m be the ratio of transition/transversion observed in the SNPs called, then

```
  x + y = 1
  2/3 * x + 1/3 *y  = m
```

We get x and y by solve this equation.

Appendix:
Transitions       C:G 

&lt;-&gt;

 T:A
Transversion    C:G 

&lt;-&gt;

 G:C, T:A 

&lt;-&gt;

 G:C, T:A 

&lt;-&gt;

 A:T