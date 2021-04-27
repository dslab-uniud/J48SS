# J48SS

This repository contains the JAR file of WEKA 3.9.1, modified to contain J48SS decision tree classifier.
The decision tree is capable of handling categorical, numerical, time series and sequential (e.g., text) data in a seamless way, during the same execution cycle in order to establish a prediction.

ARFF files used by the algorithm are structured as usual.
For what concerns sequential and time series features, they are encoded as string attributes, following the conventions:
 - sequences:
   - the name of the attribute should begin with "SEQ_"
   - as for the sequence, it should be encoded as, for instance: ‘A,B,C>B,A>D>…’, that represents a sequence with itemset {A,B,C} followed by itemset {B,A}, followed by {D}. For instance, for textual data the string "this is a string" should be encoded as 'this>is>a>string'
 - time series:
   - the name of the attribute should begin with "TS_"
   - as for the time series, it should be encoded as, for instance: ‘1.53,-2.5,3.6, …’. Currently, no multivariate time series are supported. Please encode them using different attributes.

Of course, multiple sequential and time series attributes may be present in the dataset.

J48SS is based on J48, thus it inherits all its parameters. In addition, it also has some specific ones:
  - for sequential attributes:
    - maxGap: the max gap between two itemsets of a pattern. If set to 1, only patterns of contiguous itemsets will be found (no gap). If "max gap" is set to N, a gap of N-1 itemsets is allowed between two consecutive itemsets of a pattern. The larger the gap, the (considerably) slower the algorithm
    - maxPatternLength: maximum pattern length in terms of itemset count
    - minimumSupport: minimum support that the extracted sequential patterns must have (between 0 and 1)
  - for time series attributes:
    - crossoverP: crossover probability of the genetic algorithm  
    - mutationP: mutation probability of the genetic algorithm 
    - numEvals: number of evaluations performed by the genetic algorithm
    - popSize: population size of the genetic algorithm  
    - seed: seed used by the genetic algorithm
  - common attributes:
    - patternWeight: weight to use to evaluate the patterns (simplicity vs accuracy)
    - maxTime: used to cut-off the search of the patterns after a certain amount of time, in seconds
    - useIGPruning: whether to use the IG scoring of the best non-sequential attribute found to guide the pruning of pattern search space (should be leaved to True)

All attributes already come with their default values, although some tuning should be performed. This is especially true for patternWeight.

More information can be found at:

Andrea Brunello, Enrico Marzano, Angelo Montanari, and Guido Sciavicco - J48SS: A Novel Decision Tree Approach for the Handling of Sequential and Time Series Data. MDPI, 2019

Please cite the work as:
```
@article{brunello2019j48ss,
  title={J48SS: A novel decision tree approach for the handling of sequential and time series data},
  author={Brunello, Andrea and Marzano, Enrico and Montanari, Angelo and Sciavicco, Guido},
  journal={Computers},
  volume={8},
  number={1},
  pages={21},
  year={2019},
  publisher={Multidisciplinary Digital Publishing Institute}
}
```
