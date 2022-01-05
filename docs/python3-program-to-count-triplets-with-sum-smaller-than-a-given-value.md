# Python3 编程计算总和小于给定值的三元组

> 原文:[https://www . geeksforgeeks . org/python 3-程序到计数的三胞胎的总和小于给定值/](https://www.geeksforgeeks.org/python3-program-to-count-triplets-with-sum-smaller-than-a-given-value/)

给定一组不同的整数和一个和值。查找总和小于给定总和值的三元组的计数。预期时间复杂度为 0(n<sup>2</sup>)。
**例:**

```
Input : arr[] = {-2, 0, 1, 3}
        sum = 2.
Output : 2
Explanation :  Below are triplets with sum less than 2
               (-2, 0, 1) and (-2, 0, 3) 

Input : arr[] = {5, 1, 3, 4, 7}
        sum = 12.
Output : 4
Explanation :  Below are triplets with sum less than 12
               (1, 3, 4), (1, 3, 5), (1, 3, 7) and 
               (1, 4, 5)
```

一个**简单的解决方案**是运行三个循环来逐个考虑所有的三元组。对于每个三元组，如果三元组总和小于给定总和，则比较总和并增加计数。

## 蟒蛇 3

```
# A Simple Python 3 program to count triplets with sum smaller
# than a given value

def countTriplets(arr, n, sum):

    # Initialize result
    ans = 0

    # Fix the first element as A[i]
    for i in range( 0 ,n-2):

        # Fix the second element as A[j]
        for j in range( i+1 ,n-1):

            # Now look for the third number
            for k in range( j+1, n):
                if (arr[i] + arr[j] + arr[k] < sum):
                    ans+=1

    return ans

# Driver program
arr = [5, 1, 3, 4, 7]
n = len(arr)
sum = 12
print(countTriplets(arr, n, sum))

#Contributed by Smitha
```

输出:

```
4
```

上述解的时间复杂度为 O(n <sup>3</sup> )。一个**高效解决方案**可以先对数组进行排序，然后循环使用[这个](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)帖子的方法 1，来计数 O(n)<sup>2</sup>中的三胞胎。

```
1) Sort the input array in increasing order.
2) Initialize result as 0.
3) Run a loop from i = 0 to n-2\.  An iteration of this loop finds all
   triplets with arr[i] as first element.
     a) Initialize other two elements as corner elements of subarray
        arr[i+1..n-1], i.e., j = i+1 and k = n-1
     b) Move j and k toward each other until they meet, i.e., while (j= sum
                then k--
            // Else for current i and j, there can (k-j) possible third elements
            // that satisfy the constraint.
            (ii) Else Do ans += (k - j) followed by j++ 
```

以下是上述想法的实现。

## 蟒蛇 3

```
# Python3 program to count triplets with 
# sum smaller than a given value 

# Function to count triplets with sum smaller
# than a given value         
def countTriplets(arr,n,sum):

    # Sort input array
    arr.sort()

    # Initialize result 
    ans = 0

    # Every iteration of loop counts triplet with 
    # first element as arr[i].
    for i in range(0,n-2):

        # Initialize other two elements as corner elements 
        # of subarray arr[j+1..k] 
        j = i + 1
        k = n-1

        # Use Meet in the Middle concept 
        while(j < k):

            # If sum of current triplet is more or equal, 
            # move right corner to look for smaller values
            if (arr[i]+arr[j]+arr[k] >=sum):
                k = k-1

            # Else move left corner 
            else:

                # This is important. For current i and j, there 
                # can be total k-j third elements. 
                ans += (k - j)
                j = j+1

    return ans

# Driver program 
if __name__=='__main__':
    arr = [5, 1, 3, 4, 7] 
    n = len(arr) 
    sum = 12
    print(countTriplets(arr, n, sum)) 

# This code is contributed by 
# Yatin Gupta 
```

**输出:**

```
4
```

更多详情请参考[计数总和小于给定值](https://www.geeksforgeeks.org/count-triplets-with-sum-smaller-that-a-given-value/)的三胞胎整篇文章！