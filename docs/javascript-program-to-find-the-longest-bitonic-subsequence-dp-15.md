# 寻找最长双音素子序列的 Javascript 程序| DP-15

> 原文:[https://www . geesforgeks . org/JavaScript-program-to-find-最长的双音素子序列-dp-15/](https://www.geeksforgeeks.org/javascript-program-to-find-the-longest-bitonic-subsequence-dp-15/)

给定一个包含 n 个正整数的数组 arr[0 … n-1]，arr[]的一个[子序列](http://en.wikipedia.org/wiki/Subsequence)如果先递增后递减，则称为 Bitonic。编写一个函数，以数组为参数，返回最长的双音素子序列的长度。
按递增顺序排序的序列被认为是双音素的，递减部分为空。类似地，递减顺序被认为是 Bitonic，递增部分为空。
**示例:**

```
Input arr[] = {1, 11, 2, 10, 4, 5, 2, 1};
Output: 6 (A Longest Bitonic Subsequence of length 6 is 1, 2, 10, 4, 2, 1)

Input arr[] = {12, 11, 40, 5, 3, 1}
Output: 5 (A Longest Bitonic Subsequence of length 5 is 12, 11, 5, 3, 1)

Input arr[] = {80, 60, 30, 40, 20, 10}
Output: 5 (A Longest Bitonic Subsequence of length 5 is 80, 60, 30, 20, 10)
```

来源:微软面试问题

**解**
这个问题是标准[最长递增子序列(LIS)问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的变种。假设输入数组是长度为 n 的 arr[]，我们需要使用 [LIS 问题](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的动态规划解来构造两个数组 lis[]和 lds[]。lis[i]存储以 arr[i]结尾的最长递增子序列的长度。lds[i]存储从 arr[i]开始的最长递减子序列的长度。最后，我们需要返回 lis[I]+LDS[I]–1 的最大值，其中 I 是从 0 到 n-1。
以下是上述动态规划解决方案的实现。

## java 描述语言

```
<script>

/* Dynamic Programming implementation in JavaScript for longest bitonic 
   subsequence problem */    

    /* lbs() returns the length of the Longest Bitonic Subsequence in 
    arr[] of size n. The function mainly creates two temporary arrays 
    lis[] and lds[] and returns the maximum lis[i] + lds[i] - 1. 

    lis[i] ==> Longest Increasing subsequence ending with arr[i] 
    lds[i] ==> Longest decreasing subsequence starting with arr[i] 
    */
    function lbs(arr,n)
    {
        let i, j; 
        /* Allocate memory for LIS[] and initialize LIS values as 1 for 
            all indexes */
        let lis = new Array(n)
        for (i = 0; i < n; i++) 
            lis[i] = 1;

        /* Compute LIS values from left to right */
        for (i = 1; i < n; i++) 
            for (j = 0; j < i; j++) 
                if (arr[i] > arr[j] && lis[i] < lis[j] + 1) 
                    lis[i] = lis[j] + 1; 

        /* Allocate memory for lds and initialize LDS values for 
            all indexes */
        let lds = new Array(n); 
        for (i = 0; i < n; i++) 
            lds[i] = 1; 

        /* Compute LDS values from right to left */
        for (i = n-2; i >= 0; i--) 
            for (j = n-1; j > i; j--) 
                if (arr[i] > arr[j] && lds[i] < lds[j] + 1) 
                    lds[i] = lds[j] + 1; 

        /* Return the maximum value of lis[i] + lds[i] - 1*/
        let max = lis[0] + lds[0] - 1; 
        for (i = 1; i < n; i++) 
            if (lis[i] + lds[i] - 1 > max) 
                max = lis[i] + lds[i] - 1; 

        return max; 
    }
    let arr=[0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15]
    let n = arr.length;
    document.write("Length of LBS is "+ lbs( arr, n )); 

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
 Length of LBS is 7
```

时间复杂度:O(n^2)
辅助空间:O(n)

详情请参考[最长双音素子序列| DP-15](https://www.geeksforgeeks.org/longest-bitonic-subsequence-dp-15/) 的完整文章！