# 以递增顺序排列的第 k 个丢失元素，在给定序列中不存在

> 原文：[https://www.geeksforgeeks.org/k-th-missing-element-increasing-sequence-not-present-given-sequence/](https://www.geeksforgeeks.org/k-th-missing-element-increasing-sequence-not-present-given-sequence/)

给定两个序列，一个是递增序列 **a []** ，另一个是正常序列 **b []** ，在递增序列中找到第 K 个缺失元素，该元素在给定序列中不存在 顺序。 如果没有第 k 个缺失元素，则输出-1

**示例**：

```
Input:  a[] = {0, 2, 4, 6, 8, 10, 12, 14, 15};
        b[] = {4, 10, 6, 8, 12};
          k = 3
Output: 14
Explanation : The numbers from increasing sequence that
are not present in the given sequence are 0, 2, 14, 15.
The 3rd missing number is 14.

```

**n1** 递增序列 a []上的元素数。

**n2** 给定序列 b []中的元素数。

**天真的方法**会针对递增序列中的每个元素进行迭代，并检查它是否存在于给定序列中，并保留不存在元素的计数器，并打印第 k 个不存在元素 。 这将不够高效，因为它有两个嵌套的 for 循环，这些循环将占用 O（n2）。

时间复杂度：O（n1 * n2）

辅助空间：`O(1)`

**有效方法**是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)。 我们将给定序列的所有元素存储在哈希表中。 然后，我们迭代增加顺序的所有元素。 对于每个元素，我们都在哈希表中对其进行搜索。 如果元素存在于非哈希表中，则我们增加缺少元素的数量。 如果 count 变为 k，则返回缺少的元素。

下面是上述方法的实现

## C++

```cpp

// C++ program to find the k-th missing element 
// in a given sequence 
#include <bits/stdc++.h> 
using namespace std; 

// Returns k-th missing element. It returns -1 if 
// no k is more than number of missing elements. 
int find(int a[], int b[], int k, int n1, int n2) 
{ 
    // Insert all elements of givens sequence b[]. 
    unordered_set<int> s; 
    for (int i = 0; i < n2; i++) 
        s.insert(b[i]); 

    // Traverse through increasing sequence and  
    // keep track of count of missing numbers. 
    int missing = 0; 
    for (int i = 0; i < n1; i++) { 
        if (s.find(a[i]) == s.end()) 
            missing++; 
        if (missing == k) 
            return a[i]; 
    } 

    return -1; 
} 

// driver program to test the above function 
int main() 
{ 
    int a[] = { 0, 2, 4, 6, 8, 10, 12, 14, 15 }; 
    int b[] = { 4, 10, 6, 8, 12 }; 
    int n1 = sizeof(a) / sizeof(a[0]); 
    int n2 = sizeof(b) / sizeof(b[0]); 

    int k = 3; 
    cout << find(a, b, k, n1, n2); 
    return 0; 
} 

```

## Java

```java

// Java program to find the k-th missing element 
// in a given sequence 
import java.util.*; 

class GFG 
{ 

// Returns k-th missing element. It returns -1 if 
// no k is more than number of missing elements. 
static int find(int a[], int b[], int k, int n1, int n2) 
{ 
    // Insert all elements of givens sequence b[]. 
    LinkedHashSet<Integer> s = new LinkedHashSet<>(); 
    for (int i = 0; i < n2; i++) 
        s.add(b[i]); 

    // Traverse through increasing sequence and  
    // keep track of count of missing numbers. 
    int missing = 0; 
    for (int i = 0; i < n1; i++)  
    { 
        if(!s.contains(a[i]) )  
            missing++; 
        if (missing == k) 
            return a[i]; 
    } 

    return -1; 
} 

// Driver code 
public static void main(String[] args)  
{ 
    int a[] = { 0, 2, 4, 6, 8, 10, 12, 14, 15 }; 
    int b[] = { 4, 10, 6, 8, 12 }; 
    int n1 = a.length; 
    int n2 = b.length; 

    int k = 3; 
    System.out.println(find(a, b, k, n1, n2)); 
} 
}  

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to find the k-th  
# missing element in a given sequence  

# Returns k-th missing element. It returns -1 if  
# no k is more than number of missing elements.  
def find(a, b, k, n1, n2): 

    # insert all elements of  
    # given sequence b[]. 
    s = set() 

    for i in range(n2): 
        s.add(b[i]) 

    # Traverse through increasing sequence and  
    # keep track of count of missing numbers.  
    missing = 0
    for i in range(n1): 
        if a[i] not in s: 
            missing += 1
        if missing == k: 
            return a[i] 
    return -1

# Driver code 
a = [0, 2, 4, 6, 8, 10, 12, 14, 15] 
b = [4, 10, 6, 8, 12] 
n1 = len(a) 
n2 = len(b) 
k = 3
print(find(a, b, k, n1, n2)) 

# This code is contributed by Shrikant13 

```

## C#

```cs

// C# program to find the k-th missing element  
// in a given sequence  
using System; 
using System.Collections.Generic; 

class GFG  
{  

// Returns k-th missing element. It returns -1 if  
// no k is more than number of missing elements.  
static int find(int []a, int []b, int k, int n1, int n2)  
{  
    // Insert all elements of givens sequence b[].  
    HashSet<int> s = new HashSet<int>();  
    for (int i = 0; i < n2; i++)  
        s.Add(b[i]);  

    // Traverse through increasing sequence and  
    // keep track of count of missing numbers.  
    int missing = 0;  
    for (int i = 0; i < n1; i++)  
    {  
        if(!s.Contains(a[i]) )  
            missing++;  
        if (missing == k)  
            return a[i];  
    }  

    return -1;  
}  

// Driver code  
public static void Main(String[] args)  
{  
    int []a = { 0, 2, 4, 6, 8, 10, 12, 14, 15 };  
    int []b = { 4, 10, 6, 8, 12 };  
    int n1 = a.Length;  
    int n2 = b.Length;  

    int k = 3;  
    Console.WriteLine(find(a, b, k, n1, n2));  
}  
}  

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
14

```

**时间复杂度**：O（n1 + n2）

**辅助空间**：O（n2）

本文由 [**Raja Vikramaditya**](https://www.facebook.com/raja.vikramaditya.7) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

