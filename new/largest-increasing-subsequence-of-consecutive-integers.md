# 连续整数

的最大递增子序列

给定 n 个正整数数组。 我们需要找到连续正整数的最大递增序列。

**示例：**

```
Input : arr[] = {5, 7, 6, 7, 8} 
Output : Size of LIS = 4
         LIS = 5, 6, 7, 8

Input : arr[] = {5, 7, 8, 7, 5} 
Output : Size of LIS = 2
         LIS = 7, 8

```

通过 [LIS](https://www.geeksforgeeks.org/longest-increasing-subsequence/) 的概念可以轻松解决此问题，其中每个下一个更大的元素与以前的元素之间的差为 1。但这将花费 O（n ^ 2）的时间复杂度。

通过使用散列，我们可以找到时间连续性为 O（n）且具有连续整数的最长递增序列的大小。

我们创建一个哈希表。现在，对于每个元素 arr [i]，我们执行 hash [arr [i]] = hash [arr [i] – 1] +1。因此，对于每个元素，我们知道最长的连续递增子序列结尾 用它。 最后，我们从哈希表中返回最大值。

## C ++

```

// C++ implementation of longest continuous increasing 
// subsequence 
#include <bits/stdc++.h> 
using namespace std; 

// Function for LIS 
int findLIS(int A[], int n) 
{ 
    unordered_map<int, int> hash; 

    // Initialize result 
    int LIS_size = 1; 
    int LIS_index = 0; 

    hash[A[0]] = 1; 

    // iterate through array and find 
    // end index of LIS and its Size 
    for (int i = 1; i < n; i++) { 
        hash[A[i]] = hash[A[i] - 1] + 1; 
        if (LIS_size < hash[A[i]]) { 
            LIS_size = hash[A[i]]; 
            LIS_index = A[i]; 
        } 
    } 

    // print LIS size 
    cout << "LIS_size = " << LIS_size << "\n"; 

    // print LIS after setting start element 
    cout << "LIS : "; 
    int start = LIS_index - LIS_size + 1; 
    while (start <= LIS_index) { 
        cout << start << " "; 
        start++; 
    } 
} 

// driver 
int main() 
{ 
    int A[] = { 2, 5, 3, 7, 4, 8, 5, 13, 6 }; 
    int n = sizeof(A) / sizeof(A[0]); 
    findLIS(A, n); 
    return 0; 
} 

```

## 爪哇

```

// Java implementation of longest continuous increasing 
// subsequence 
import java.util.*; 

class GFG  
{ 

// Function for LIS 
static void findLIS(int A[], int n) 
{ 
    Map<Integer, Integer> hash = new HashMap<Integer, Integer>(); 

    // Initialize result 
    int LIS_size = 1; 
    int LIS_index = 0; 

    hash.put(A[0], 1); 
    // iterate through array and find 
    // end index of LIS and its Size 
    for (int i = 1; i < n; i++)  
    { 
        hash.put(A[i], hash.get(A[i] - 1)==null? 1:hash.get(A[i] - 1)+1); 
        if (LIS_size < hash.get(A[i]))  
        { 
            LIS_size = hash.get(A[i]); 
            LIS_index = A[i]; 
        } 
    } 

    // print LIS size 
    System.out.println("LIS_size = " + LIS_size); 

    // print LIS after setting start element 
    System.out.print("LIS : "); 
    int start = LIS_index - LIS_size + 1; 
    while (start <= LIS_index) 
    { 
        System.out.print(start + " "); 
        start++; 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int A[] = { 2, 5, 3, 7, 4, 8, 5, 13, 6 }; 
    int n = A.length; 
    findLIS(A, n); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python3

```

# Python3 implementation of longest  
# continuous increasing subsequence 

# Function for LIS 
def findLIS(A, n): 
    hash = dict() 

    # Initialize result 
    LIS_size, LIS_index = 1, 0

    hash[A[0]] = 1

    # iterate through array and find 
    # end index of LIS and its Size 
    for i in range(1, n): 

        # If the desired key is not present  
        # in dictionary, it will throw key error,  
        # to avoid this error this is necessary 
        if A[i] - 1 not in hash: 
            hash[A[i] - 1] = 0

        hash[A[i]] = hash[A[i] - 1] + 1
        if LIS_size < hash[A[i]]: 
            LIS_size = hash[A[i]] 
            LIS_index = A[i] 

    # print LIS size 
    print("LIS_size =", LIS_size) 

    # print LIS after setting start element 
    print("LIS : ", end = "") 

    start = LIS_index - LIS_size + 1
    while start <= LIS_index: 
        print(start, end = " ") 
        start += 1

# Driver Code 
if __name__ == "__main__": 
    A = [ 2, 5, 3, 7, 4, 8, 5, 13, 6 ] 
    n = len(A) 
    findLIS(A, n) 

# This code is contributed by sanjeev2552 

```

## C＃

```

// C# implementation of longest continuous increasing 
// subsequence 
using System; 
using System.Collections.Generic;  

class GFG  
{ 

// Function for LIS 
static void findLIS(int []A, int n) 
{ 
    Dictionary<int,int> hash = new Dictionary<int,int>(); 

    // Initialize result 
    int LIS_size = 1; 
    int LIS_index = 0; 

    hash.Add(A[0], 1); 

    // iterate through array and find 
    // end index of LIS and its Size 
    for (int i = 1; i < n; i++)  
    { 
        if(hash.ContainsKey(A[i]-1)) 
        { 
            var val = hash[A[i]-1]; 
            hash.Remove(A[i]); 
            hash.Add(A[i], val + 1);  
        } 
        else
        { 
            hash.Add(A[i], 1); 
        } 
        if (LIS_size < hash[A[i]])  
        { 
            LIS_size = hash[A[i]]; 
            LIS_index = A[i]; 
        } 
    } 

    // print LIS size 
    Console.WriteLine("LIS_size = " + LIS_size); 

    // print LIS after setting start element 
    Console.Write("LIS : "); 
    int start = LIS_index - LIS_size + 1; 
    while (start <= LIS_index) 
    { 
        Console.Write(start + " "); 
        start++; 
    } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []A = { 2, 5, 3, 7, 4, 8, 5, 13, 6 }; 
    int n = A.Length; 
    findLIS(A, n); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
LIS_size = 5
LIS : 2 3 4 5 6 

```

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。