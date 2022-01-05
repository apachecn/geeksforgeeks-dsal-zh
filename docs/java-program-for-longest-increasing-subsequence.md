# 最长递增子序列的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序最长递增子序列/](https://www.geeksforgeeks.org/java-program-for-longest-increasing-subsequence/)

最长递增子序列(LIS)问题是求给定序列的最长子序列的长度，使子序列的所有元素按递增顺序排序。例如，{10，22，9，33，21，50，41，60，80}的 LIS 长度为 6，LIS 长度为{10，22，33，50，60，80}。
![longest-increasing-subsequence](img/f735f577a7c1ecb67090d0d1959dfc2a.png)

更多示例:

```
Input  : arr[] = {3, 10, 2, 1, 20}
Output : Length of LIS = 3
The longest increasing subsequence is 3, 10, 20

Input  : arr[] = {3, 2}
Output : Length of LIS = 1
The longest increasing subsequences are {3} and {2}

Input : arr[] = {50, 3, 10, 7, 40, 80}
Output : Length of LIS = 4
The longest increasing subsequence is {3, 7, 40, 80}

```

**最优子结构:**
让 arr[0..n-1]是输入数组，L(i)是以索引 I 结束的 LIS 的长度，因此 arr[i]是 LIS 的最后一个元素。
然后，L(i)可以递归地写成:
L(i) = 1 + max( L(j))，其中 0 < j < i 和 arr[j]<arr[I]；或者
L(i) = 1，如果不存在这样的 j。
为了找到给定数组的 LIS，我们需要返回 max(L(i))，其中 0 < i < n.
因此，我们看到 LIS 问题满足最优子结构性质，因为主问题可以使用子问题的解来解决。

下面是 LIS 问题的简单递归实现。它遵循上面讨论的递归结构。

```
/* A Naive Java Program for LIS Implementation */
class LIS {
    static int max_ref; // stores the LIS

    /* To make use of recursive calls, this function must return
   two things:
   1) Length of LIS ending with element arr[n-1]. We use
      max_ending_here for this purpose
   2) Overall maximum as the LIS may end with an element
      before arr[n-1] max_ref is used this purpose.
   The value of LIS of full array of size n is stored in
   *max_ref which is our final result */
    static int _lis(int arr[], int n)
    {
        // base case
        if (n == 1)
            return 1;

        // 'max_ending_here' is length of LIS ending with arr[n-1]
        int res, max_ending_here = 1;

        /* Recursively get all LIS ending with arr[0], arr[1] ...
           arr[n-2]. If   arr[i-1] is smaller than arr[n-1], and
           max ending with arr[n-1] needs to be updated, then
           update it */
        for (int i = 1; i < n; i++) {
            res = _lis(arr, i);
            if (arr[i - 1] < arr[n - 1] && res + 1 > max_ending_here)
                max_ending_here = res + 1;
        }

        // Compare max_ending_here with the overall max. And
        // update the overall max if needed
        if (max_ref < max_ending_here)
            max_ref = max_ending_here;

        // Return length of LIS ending with arr[n-1]
        return max_ending_here;
    }

    // The wrapper function for _lis()
    static int lis(int arr[], int n)
    {
        // The max variable holds the result
        max_ref = 1;

        // The function _lis() stores its result in max
        _lis(arr, n);

        // returns max
        return max_ref;
    }

    // driver program to test above functions
    public static void main(String args[])
    {
        int arr[] = { 10, 22, 9, 33, 21, 50, 41, 60 };
        int n = arr.length;
        System.out.println("Length of lis is "
                           + lis(arr, n) + "\n");
    }
}
/*This code is contributed by Rajat Mishra*/
```

**Output:**

```
Length of lis is 5

```

**重叠子问题:**
考虑到上面的实现，下面是大小为 4 的数组的递归树。lis(n)给出了 arr[]的 lis 长度。

```
              lis(4)
        /        |     
      lis(3)    lis(2)   lis(1)
     /           /
   lis(2) lis(1) lis(1)
   /
lis(1)

```

我们可以看到有很多子问题被一次又一次地解决。因此，该问题具有重叠子结构性质，用记忆法或制表法都可以避免同一子问题的重新计算。下面是 LIS 问题的一个列表实现。

```
/* Dynamic Programming Java implementation of LIS problem */

class LIS {
    /* lis() returns the length of the longest increasing
       subsequence in arr[] of size n */
    static int lis(int arr[], int n)
    {
        int lis[] = new int[n];
        int i, j, max = 0;

        /* Initialize LIS values for all indexes */
        for (i = 0; i < n; i++)
            lis[i] = 1;

        /* Compute optimized LIS values in bottom up manner */
        for (i = 1; i < n; i++)
            for (j = 0; j < i; j++)
                if (arr[i] > arr[j] && lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;

        /* Pick maximum of all LIS values */
        for (i = 0; i < n; i++)
            if (max < lis[i])
                max = lis[i];

        return max;
    }

    public static void main(String args[])
    {
        int arr[] = { 10, 22, 9, 33, 21, 50, 41, 60 };
        int n = arr.length;
        System.out.println("Length of lis is " + lis(arr, n) + "\n");
    }
}
/*This code is contributed by Rajat Mishra*/
```

**Output:**

```
Length of lis is 5

```

详情请参考[动态规划|集合 3(最长递增子序列)](https://www.geeksforgeeks.org/longest-increasing-subsequence/)整篇文章！