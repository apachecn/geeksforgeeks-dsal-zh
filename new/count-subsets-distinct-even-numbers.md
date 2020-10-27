# 对具有不同偶数的子集进行计数

给定 n 个数字的序列。 任务是对给定集合的所有子集进行计数，这些子集只有偶数，并且所有子集都是不同的。
**注意**：根据集合的属性，如果两个子集具有相同的元素集，则将它们视为一个元素。 例如：[2，4，8]和[4，2，8]被认为是相同的。

例子：

```
Input : {4, 2, 1, 9, 2, 6, 5, 3} 
Output : 7
The subsets are:
[4], [2], [6], [4, 2], 
[2, 6], [4, 6], [4, 2, 6]

Input : {10, 3, 4, 2, 4, 20, 10, 6, 8, 14, 2, 6, 9}
Output : 127

```

**简单方法**是考虑所有子集并检查它们是否满足给定条件。 时间复杂度将成倍增长。

**有效方法**是对不同的偶数进行计数。 使其为**等于**。 然后应用公式：

**2 <sup>ceven</sup> – 1**

这类似于计算 n 个给定元素集中的子集数。 **1** 被减去，因为未考虑空集。

## C++

```cpp

// C++ implementation to count subsets having 
// even numbers only and all are distinct 
#include <bits/stdc++.h> 
using namespace std; 

// function to count the 
// required subsets 
int countSubsets(int arr[], int n) 
{ 
    unordered_set<int> us; 
    int even_count = 0; 

    // inserting even numbers in the set 'us' 
    // single copy of each number is retained 
    for (int i=0; i<n; i++) 
        if (arr[i] % 2 == 0) 
            us.insert(arr[i]); 

    unordered_set<int>:: iterator itr; 

    // distinct even numbers 
    even_count = us.size(); 

    // total count of required subsets 
    return (pow(2, even_count) - 1); 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = {4, 2, 1, 9, 2, 6, 5, 3}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << "Number of subsets = "
         << countSubsets(arr, n); 
    return 0;      
}   

```

## Java

```java

// Java implementation to count subsets having 
// even numbers only and all are distinct 
import java.util.*; 

class GFG  
{ 

// function to count the 
// required subsets 
static int countSubsets(int arr[], int n) 
{ 
    HashSet<Integer> us = new HashSet<>(); 
    int even_count = 0; 

    // inserting even numbers in the set 'us' 
    // single copy of each number is retained 
    for (int i = 0; i < n; i++) 
        if (arr[i] % 2 == 0) 
            us.add(arr[i]); 

    // counting distinct even numbers 
    even_count=us.size(); 

    // total count of required subsets 
    return (int) (Math.pow(2, even_count) - 1); 
} 

// Driver code 
public static void main(String[] args)  
{ 
    int arr[] = {4, 2, 1, 9, 2, 6, 5, 3}; 
    int n = arr.length; 
    System.out.println("Number of subsets = "
        + countSubsets(arr, n)); 
} 
} 

// This code contributed by Rajput-Ji 

```

## Python3

```py

# python implementation to count subsets having  
# even numbers only and all are distinct  

#function to count the required subsets  
def countSubSets(arr, n): 
    us = set() 
    even_count = 0

    # inserting even numbers in the set 'us'  
    # single copy of each number is retained  
    for i in range(n): 
        if arr[i] % 2 == 0: 
            us.add(arr[i]) 

    # counting distinct even numbers  
    even_count = len(us) 

    # total count of required subsets  
    return pow(2, even_count)-  1

# Driver program 
arr = [4, 2, 1, 9, 2, 6, 5, 3] 
n = len(arr) 
print("Numbers of subset=", countSubSets(arr,n)) 

# This code is contributed by Shrikant13 

```

## C#

```cs

// C# implementation to count subsets having 
// even numbers only and all are distinct  
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// function to count the 
// required subsets 
static int countSubsets(int []arr, int n) 
{ 
    HashSet<int> us = new HashSet<int>(); 
    int even_count = 0; 

    // inserting even numbers in the set 'us' 
    // single copy of each number is retained 
    for (int i = 0; i < n; i++) 
        if (arr[i] % 2 == 0) 
            us.Add(arr[i]); 

    // counting distinct even numbers 
    even_count = us.Count; 

    // total count of required subsets 
    return (int) (Math.Pow(2, even_count) - 1); 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    int[] arr = {4, 2, 1, 9, 2, 6, 5, 3}; 
    int n = arr.Length; 
    Console.WriteLine("Number of subsets = "
        + countSubsets(arr, n)); 
} 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
Number of subsets = 7

```

**时间复杂度**：O（n）

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

