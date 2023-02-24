#Algorithm 
#DynamicProgramming 

Given a set of n integers, the task is to divide it into two sets s.t. the absolute difference between their sums is minimized. 
Subset 1 has m elements, Subset 2 has n-m elements, then we want to choose Subset 1 and Subset 2 s.t. $$min(abs(sum(Subset1)-sum(Subset2)))$$
There is recursive solution which is to generate all possible sums from all the values of the array and to check which solution is the most optimal one. To generate sums we either include the i’th item in set 1 or don’t include, i.e., include in set 2. The time complexity if O(2^n), with space compelxity O(n). 

We can also solve this using Dynamic Programming. 
![[Pasted image 20230209125504.png]]

This can be implemented in O(n * sum) time and O(sum) space
```python
def minDifference(arr, n):
	sum = 0
	for i in range(n):
		sum += arr[i]
	y = sum // 2 + 1

	# dp[i] gives whether is it possible to get i as
	# sum of elements dd is helper variable we use dd
	# to ignoring duplicates
	dp = [False for i in range(y)]
	dd = [False for i in range(y)]

	# Initialising dp and dd

	# sum = 0 is possible
	dp[0] = True # let dp array is used for storing
	# previous values and dd array is used to
	# store current values
	for i in range(n):

		# updating dd[k] as True if k can be formed
		# using elements from 1 to i+1
		for j in range(y):
			if (j + arr[i] < y and dp[j]):
				dd[j + arr[i]] = True

		# updating dd
		for j in range(y):
			if (dd[j]):
				dp[j] = True
			dd[j] = False # reset dd

	# checking the number from sum/2 to 1 which is
	# possible to get as sum
	for i in range(y-1, 0, -1):
		if (dp[i]):
			return (sum - 2 * i)

		# since i is possible to form then another
		# number is sum-i so mindifference is sum-i-i
	return 0


if __name__ == '__main__':

	arr = [1, 6, 11, 5]
	n = len(arr)
	print("The Minimum difference of 2 sets is ", minDifference(arr, n))
```
