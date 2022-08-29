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

# Implementation of SON algorithm

1) Imported basic libraries random and numpy

2) Define a global variable for threshold percentage, which determine whether the itemset is frequent or not. For example, if the threshold percentage I set is 1% (0.01), and the data size is 30000, that means when the itemset exist 300 times or more, than it will be classified as frequent

3) Read lines for 7 datasets (T10I4D100K, T40I10D100K, chess, connect, mushroom, pumsb, pumsb_star), lines in each dataset will be stored in a list

4) Write the function of the SON algorithm

      i) The function contains 2 parameters – list of data and the number of chunk (I set 10 chunks)

      ii) At the beginning, the function will divide the whole dataset in to certain number of chunks (let’s say 10).

      iii) Calculate the chunk’s threshold by (whole_set_size * threshold_percent/ number of chunks) Calculate the whole data’s threshold by (whole_set_size * threshold_percent)

      iv) 1st pass of SON algorithm: - Find local frequent doubleton by A-priori algorithm for each chunk (support > = chunk’s threshold) - Union all local frequent doubleton to form a list (candidate itemsets)

      v) 2nd pass of SON algorithm: - count all the candidate itemsets (sum up all the support of that itemset from each chunk) - select those that have support>= whole data’s threshold as the frequent itemsets, in order to remove false positives

5) Use above function to find the frequent itemset for 7 datasets (T10I4D100K, T40I10D100K, chess, connect, mushroom, pumsb, pumsb_star) with number of chunks = 10

6) Get the size of above frequent itemsets and compare with those from the simple, randomized algorithm

# Comparison the above 2 algorithms

Default: For all experiments, I set 1% as threshold, which means if the support of itemset is larger than or equal to 1% times the total number of rows of dataset, then the itemset will be classified as frequent.

I compared the result in 2 perspectives – 1) Jaccard Similarity between list of frequent itemsets & the 2) number of frequent itemsets. The function for simple and random algorithm that I wrote can also list out all the association rules and calculate the confidence for each rule, but it seems there is no good method to compare it with other data, so I don’t list out in here.

I obtained total 5 lists of frequent itemset from each dataset. 4 of them from simple, random algorithm and 1 of them from SON algorithm.

<B>1) Jaccard Similarity<B>

Below is the matrix to show the Jaccard similarity percentage(%) between list of frequent itemsets from simple, random algorithm and SON algorithm. If the number is 100, that means they are 100% equal, it the number close to zero, that means they have no mutual elements.
  
![image](https://user-images.githubusercontent.com/57484350/187123453-ab0e6454-13c3-4ceb-afd4-8b2be69de64b.png)

There are 3 things we can see in this comparison. 
  
1) Among list of frequent itemsets generated by simple, random algorithm (1%/2%/5%/10%), the similarity is getting higher when the sample is getting larger. For example, all similarity between 10% with others is higher than that of similarity between 1%/2% with others. 
  
2) Second, as we know, SON algorithm avoid both false positives and false negatives, so the list of frequent itemset should be more accurate when compare to those only choose a small random sample. Therefore, if the similarity of a frequent itemset is higher when compare to the frequent itemset generated by SON algorithm, the frequent itemset is more representative/accurate. We can see that the similarity increases with the increase in sample size (see below graph). It perfectly make senses, since when the sample size is larger, the representative for whole population is larger also. 
  
3) Third, we can see that the similarity vs itemset from SON algorithm increases at a decreasing rate, with the increase in sample size.

