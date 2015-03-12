I will describe some analytical techniques that are essential to any projects along side running the streamlined programs.

The first one is estimate the running time of mapping by BLAT and cross\_match and set appropriate parameters for each step. The atlas-mapper-format-ref.rb takes the reference sequence and make ooc file for blat. The ooc file stores the over-represented 11-mers so that BLAT can ignore them during seeding stage of reads mapping. The default value for ooc cutoff is 1024, which is optimized for human genome. It would be wise to decrease this value for smaller genomes. Higher than optimal value of ooc cutoff would decrease the mapping speed.

The choice of reference is another important issue. Usually the complete and un-redundant genome is the best.