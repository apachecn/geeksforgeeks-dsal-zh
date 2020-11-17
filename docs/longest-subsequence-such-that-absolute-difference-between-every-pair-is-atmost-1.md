# 最长子序列，其中每对之间的绝对差最大为 1

> 原文：[https://www.geeksforgeeks.org/longest-subsequence-such-that-absolute-difference-between-every-pair-is-atmost-1/](https://www.geeksforgeeks.org/longest-subsequence-such-that-absolute-difference-between-every-pair-is-atmost-1/)

给定大小为`N`的整数数组`arr[]`，任务是找到最长的子序列`S`，以便对每个`a[i], a [j] ∈ S`和`|a[i] – a[j]| ≤ 1`。

**示例**：

> **输入**：`arr[] = {2, 2, 3, 5, 5, 6, 6, 6}`
>
> **输出**：5
> **说明**：
>
> 有 2 个子序列，每对之间的差异最大为 1
>
> `{2, 2, 3}`和`{5, 5, 6, 6, 6}`
>
> 其中最长的一个是`{5, 5, 6, 6, 6}`，长度为 5。
> 
> **输入**：`arr[] = {5, 7, 6, 4, 4, 2}`
>
> **输出**：3


**方法**：

想法是观察到，对于一个子序列，在每个可能的对之间具有差异的情况下，当子序列包含`[X, X + 1]`之间的元素时，最多可能一个子序列。

*   将所需子序列的最大长度初始化为 0。

*   创建一个`HashMap`来存储数组中每个元素的频率。

*   遍历` `，并针对哈希映射中的每个元素`a[i]`：

    *   查找元素`a[i] + 1`，`a[i]`和`a[i] – 1`的出现次数。

    *   找到元素`a[i] + 1`或`a[i] – 1`的最大计数。

    *   如果总出现次数大于找到的最大长度，则更新子序列的最大长度。

下面是上述方法的实现。

## Java

```java

// Java implementation for  
// Longest subsequence such that absolute 
// difference between every pair is atmost 1 

import java.util.*; 
public class GeeksForGeeks { 
    public static int longestAr( 
            int n, int arr[]){ 
        Hashtable<Integer, Integer> count 
            = new Hashtable<Integer, Integer>(); 

        // Storing the frequency of each 
        // element in the hashtable count 
        for (int i = 0; i < n; i++) { 
            if (count.containsKey(arr[i])) 
                count.put(arr[i], count.get( 
                    arr[i]) + 1
                ); 
            else
                count.put(arr[i], 1); 
        } 

        Set<Integer> kset = count.keySet(); 
        Iterator<Integer> it = kset.iterator(); 

        // Max is used to keep a track of 
        // maximum length of the required  
        // subsequence so far. 
        int max = 0; 

        while (it.hasNext()) { 
            int a = (int)it.next(); 
            int cur = 0; 
            int cur1 = 0; 
            int cur2 = 0; 

            // Store frequency of the 
            // given element+1\. 
            if (count.containsKey(a + 1)) 
                cur1 = count.get(a + 1); 

            // Store frequency of the 
            // given element-1\. 
            if (count.containsKey(a - 1)) 
                cur2 = count.get(a - 1); 

            // cur store the longest array  
            // that can be formed using a. 
            cur = count.get(a) + 
                  Math.max(cur1, cur2); 

            // update max if cur>max. 
            if (cur > max) 
                max = cur; 
        } 

        return (max); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int n = 8; 
        int arr[] = { 2, 2, 3, 5, 5, 6, 6, 6 }; 
        int maxLen = longestAr(n, arr); 
        System.out.println(maxLen); 
    } 
} 

```

## Python3

```py

# Python3 implementation for 
# Longest subsequence such that absolute 
# difference between every pair is atmost 1 

def longestAr(n, arr): 
    count = dict() 

    # Storing the frequency of each 
    # element in the hashtable count 
    for i in arr: 
        count[i] = count.get(i, 0) + 1

    kset = count.keys() 

    # Max is used to keep a track of 
    # maximum length of the required 
    # subsequence so far. 
    maxm = 0

    for it in list(kset): 
        a = it 
        cur = 0
        cur1 = 0
        cur2 = 0

        # Store frequency of the 
        # given element+1\. 
        if ((a + 1) in count): 
            cur1 = count[a + 1] 

        # Store frequency of the 
        # given element-1\. 
        if ((a - 1) in count): 
            cur2 = count[a - 1] 

        # cur store the longest array 
        # that can be formed using a. 
        cur = count[a] + max(cur1, cur2) 

        # update maxm if cur>maxm. 
        if (cur > maxm): 
            maxm = cur 

    return maxm 

# Driver Code 
if __name__ == '__main__': 
    n = 8
    arr = [2, 2, 3, 5, 5, 6, 6, 6] 
    maxLen = longestAr(n, arr) 
    print(maxLen) 

# This code is contributed by mohit kumar 29 

```

**输出**：

```
5

```

**时间复杂度**：`O(n)`。

**空间复杂度**：`O(n)`。



* * *

* * *



