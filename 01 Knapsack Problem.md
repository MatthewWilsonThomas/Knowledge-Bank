We are given N items where each item has some weight and profit associated with it. We are also given a bag with capacity W, i.e., the bag can hold at most **W** weight in it. The target is to put the items into the bag such that the sum of profits associated with them is the maximum possible. 

**Note:** The constraint here is we can either put an item completely into the bag or cannot put it at all. Note; It is not possible to put a part of an item into the bag.

### Recursion
A simple solution is to consider all subsets of items and calculate the total weight and profit of all subsets. Consider the only subsets whose total weight is smaller than W. From all such subsets, pick the subset with maximum profit.

_**Optimal Substructure**_**:** To consider all subsets of items, there can be two cases for every item. 

-   **Case 1:** The item is included in the optimal subset.
-   **Case 2:** The item is not included in the optimal set.

``` python
# A naive recursive implementation
# of 0-1 Knapsack Problem
 
# Returns the maximum value that
# can be put in a knapsack of
# capacity W
 
 
def knapSack(W, wt, val, n):
 
    # Base Case
    if n == 0 or W == 0:
        return 0
 
    # If weight of the nth item is
    # more than Knapsack of capacity W,
    # then this item cannot be included
    # in the optimal solution
    if (wt[n-1] > W):
        return knapSack(W, wt, val, n-1)
 
    # return the maximum of two cases:
    # (1) nth item included
    # (2) not included
    else:
        return max(
            val[n-1] + knapSack(
                W-wt[n-1], wt, val, n-1),
            knapSack(W, wt, val, n-1))
 
# end of function knapSack
 
 
# Driver Code
if __name__ == '__main__':
    profit = [60, 100, 120]
    weight = [10, 20, 30]
    W = 50
    n = len(profit)
    print knapSack(W, weight, profit, n)
 
# This code is contributed by Nikhil Kumar Singh
```


### Memorization
As there are repetitions of the same subproblem again and again we can implement the following idea to solve the problem.
If we get a subproblem the first time, we can solve this problem by creating a 2-D array that can store a particular state (n, w). Now if we come across the same state (n, w) again instead of calculating it in exponential complexity we can directly return its result stored in the table in constant time.

``` python
# This is the memoization approach of
# 0 / 1 Knapsack in Python in simple
# we can say recursion + memoization = DP
 
def knapsack(wt, val, W, n):
 
    # base conditions
    if n == 0 or W == 0:
        return 0
    if t[n][W] != -1:
        return t[n][W]
 
    # choice diagram code
    if wt[n-1] <= W:
        t[n][W] = max(
            val[n-1] + knapsack(
                wt, val, W-wt[n-1], n-1),
            knapsack(wt, val, W, n-1))
        return t[n][W]
    elif wt[n-1] > W:
        t[n][W] = knapsack(wt, val, W, n-1)
        return t[n][W]
 
# Driver code
if __name__ == '__main__':
    profit = [60, 100, 120]
    weight = [10, 20, 30]
    W = 50
    n = len(profit)
     
    # We initialize the matrix with -1 at first.
    t = [[-1 for i in range(W + 1)] for j in range(n + 1)]
    print(knapsack(weight, profit, W, n))
 
# This code is contributed by Prosun Kumar Sarkar
```

### [[Dynamic Programming]]
Since subproblems are evaluated again, this problem has Overlapping Sub-problems property. So the 0/1 Knapsack problem has both properties of a dynamic programming problem. Like other typical #DynamicProgramming (DP) problems, re-computation of the same subproblems can be avoided by constructing a temporary array $K[]$ in a bottom-up manner.

Follow the below steps to solve the problem:

-   Consider the same cases as mentioned in the recursive approach. 
-   In a DP table let’s consider all the possible weights from ‘1’ to ‘W’ as the columns and the element that can be kept as rows. 
-   The state $DP[i][j]$ will denote the maximum value of ‘j-weight’ considering all values from ‘1 to i-th‘. So if we consider ‘wi‘ (weight in ‘i-th‘ row) we can fill it in all columns which have ‘weight values > wi‘. Now two possibilities can take place: 
    -   Fill ‘wi‘ in the given column.
    -   Do not fill ‘wi‘ in the given column.
-   Now we have to take a maximum of these two possibilities, 
    -   Formally if we do not fill the ‘ith‘ weight in the ‘jth‘ column then the $DP[i][j]$ state will be the same as $DP[i-1][j]$ 
    -   But if we fill the weight, $DP[i][j]$ will be equal to the value of (‘wi‘+ value of the column weighing ‘j-wi’) in the previous row. 
-   So we take the maximum of these two possibilities to fill the current state.

```python
# A Dynamic Programming based Python
# Program for 0-1 Knapsack problem
# Returns the maximum value that can
# be put in a knapsack of capacity W

def knapSack(W, wt, val, n):
    K = [[0 for x in range(W + 1)] for x in range(n + 1)]
 
    # Build table K[][] in bottom up manner
    for i in range(n + 1):
        for w in range(W + 1):
            if i == 0 or w == 0:
                K[i][w] = 0
            elif wt[i-1] <= w:
                K[i][w] = max(val[i-1]
                              + K[i-1][w-wt[i-1]],
                              K[i-1][w])
            else:
                K[i][w] = K[i-1][w]
 
    return K[n][W]
 
# Driver code
if __name__ == '__main__':
    profit = [60, 100, 120]
    weight = [10, 20, 30]
    W = 50
    n = len(profit)
    print(knapSack(W, weight, profit, n))
 
# This code is contributed by Bhavya Jain```