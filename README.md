# Frequent-Itemsets-by-Apriori-SON-Algorithm-from-Scratch

# Task Details

For this exercise, you will need to rst study the Section 6.4 (up to 6.4.3) of the text-book, Mining Massive Datasets, Leskovec, Rajaraman, Ullman (third edition, 2020), and then follow the instructions below:

1. Implement the simple, randomized algorithm (Apriori) given in Section 6.4.1 of the text-book. 

2. Implement the algorithm of Savasere, Omiecinski, and Navathe (SON algorithm), as explained in Section 6.4.3.

3. Compare the two algorithms implemented above on ALL the following datasets: T10I4D100K, T40I10D100K, chess, connect, mushroom, pumsb, pumsb star; those datasets are available at: http://fimi.ua.ac.be/data/  Report the observed outcomes and comparisons on individual datasets and in overall.

4. Perform different experiments on the simple randomized algorithm, using the following sample sizes: 1%, 2%, 5% and 10%. Compare your experimental results. Additionally compare the results of the above experiments with the results produced by the SON algorithm. Your approach should be as efficient as possible in terms of runtime and memory requirements. Report on challenges that you might have come across during the imple- mentation and running the experiments.

# Implementation of simple, randomized algorithm (Apriori)

1) Imported basic libraries random and numpy

2) Define a global variable for threshold percentage, which determine whether the itemset is frequent or not. For example, if the threshold percentage I set is 1% (0.01), and the data size is 30000, that means when the itemset exist 300 times or more, than it will be classified as frequent

3) Read lines for 7 datasets (T10I4D100K, T40I10D100K, chess, connect, mushroom, pumsb, pumsb_star), lines in each dataset will be stored in a list

4) Write the function of the simple, randomized algorithm with A-priori algorithm inside
  
     i) The function contains 2 parameters – list of data and the sample size (1%/2%/5%/10%)
  
  ii) At the beginning, the function will choose random sample from the whole dataset, say like if the whole dataset is 30000 rows and the sample size is 1%, then it will choose 300 rows randomly and form a new list (sample).
  
  iii) Calculate the threshold by (whole_set_size * threshold_percent * sample_size) Using above example, which means 30000*1%*1% = 3 that means if the itemset exist 3 times or above In this sample (300 rows), then it is classified as frequent.
  
  iv) 1st pass of A-priori algorithm: - Count the occurrence/support of each singleton - filter for frequent singletons (if the support of each singleton >= threshold, then it is frequent)
  
  v) 2nd pass of A-priori algorithm: - Count the occurrence/support of each doubleton. However, if the doubleton contains an element which is not in the list of frequent singletons, then the whole doubleton will not consider as frequent doubleton. - filter for frequent doubletons (if the support of each doubleton >= threshold, then it is frequent)
 
 vi) List out all association rules for the frequent doubletons and calculate its confidence

5) Use above function to find the frequent itemset for 7 datasets (T10I4D100K, T40I10D100K, chess, connect, mushroom, pumsb, pumsb_star) with sample size (1%/2%/5%/10%)

6) Get the size of above frequent itemsets and compare
