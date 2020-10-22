# 搜索元素的数组范围查询

> 原文： [https://www.geeksforgeeks.org/array-range-queries-for-searching-an-element/](https://www.geeksforgeeks.org/array-range-queries-for-searching-an-element/)

给定一个由`N`个元素组成的数组和形式为`L R X`的`Q`个查询。对于每个查询，必须输出元素`X`是否存在于索引`L`和`R`（包括）之间的数组中。

**先决条件**： [Mo 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)

**示例**：

```
Input : N = 5
        arr = [1, 1, 5, 4, 5]
        Q = 3
        1 3 2
        2 5 1
        3 5 5         
Output : No
         Yes
         Yes
Explanation :
For the first query, 2 does not exist between the indices 1 and 3.
For the second query, 1 exists between the indices 2 and 5.
For the third query, 5 exists between the indices 3 and 5.

```

**朴素方法**：

朴素方法是针对每个查询遍历从`L`到`R`的元素，线性搜索`X`。在最坏的情况下，从`L`到`R`可以有`N`个元素，因此每个查询的最差情况时间复杂度为`O(n)`。 因此，对于所有`Q`查询，时间复​​杂度将变为`O(Q * N)`。

**使用联合查找方法**：

此方法仅检查所有连续相等值中的一个元素。 如果`X`不等于这些值，则算法会跳过所有其他相等的元素，并继续遍历下一个不同的元素。 该算法显然仅在连续存在大量相等元素时才有用。

**算法**：

1.  将所有连续的相等元素合并为一组。

2.  处理查询时，从`R`开始。让`index = R`。

3.  将`a[index]`与`X`进行比较。如果它们相等，则打印`"Yes"`，然后遍历其余范围。 否则，跳过所有属于`a[index]`组的连续元素。 索引等于该组的根索引的 1。

4.  继续上述步骤，直到找到`X`或直到索引小于`L`。

5.  如果索引小于`L`，则打印`"No"`。

以下是上述想法的实现。

## C++ 

```cpp

// Program to determine if the element 
// exists for different range queries 
#include <bits/stdc++.h> 
using namespace std; 

// Structure to represent a query range 
struct Query 
{ 
    int L, R, X; 
}; 

const int maxn = 100; 

int root[maxn]; 

// Find the root of the group containing 
// the element at index x 
int find(int x) 
{ 
    return x == root[x] ? x : root[x] = 
                find(root[x]); 
} 

// merge the two groups containing elements 
// at indices x and y into one group 
int uni(int x, int y) 
{ 
    int p = find(x), q = find(y); 
    if (p != q) { 
        root[p] = root[q]; 
    } 
} 

void initialize(int a[], int n, Query q[], int m) 
{ 
    // make n subsets with every 
    // element as its root 
    for (int i = 0; i < n; i++) 
        root[i] = i; 

    // consecutive elements equal in value are 
    // merged into one single group 
    for (int i = 1; i < n; i++) 
        if (a[i] == a[i - 1]) 
            uni(i, i - 1); 
} 

// Driver code 
int main() 
{ 
    int a[] = { 1, 1, 5, 4, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    Query q[] = { { 0, 2, 2 }, { 1, 4, 1 }, 
                  { 2, 4, 5 } }; 
    int m = sizeof(q) / sizeof(q[0]); 
    initialize(a, n, q, m); 

    for (int i = 0; i < m; i++) 
    { 
        int flag = 0; 
        int l = q[i].L, r = q[i].R, x = q[i].X; 
        int p = r; 

        while (p >= l) 
        { 

            // check if the current element in 
            // consideration is equal to x or not 
            // if it is equal, then x exists in the range 
            if (a[p] == x) 
            { 
                flag = 1; 
                break; 
            } 
            p = find(p) - 1; 
        } 

        // Print if x exists or not 
        if (flag != 0) 
            cout << x << " exists between [" << l  
                 << ", " << r << "] " << endl; 
        else
            cout << x << " does not exist between [" 
                << l << ", " << r  << "] " << endl; 
    } 
} 

```

## Java

```java
// Java program to determine if the element 
// exists for different range queries 
import java.util.*; 
  
class GFG  
{ 
  
// Structure to represent a query range 
static class Query 
{ 
    int L, R, X; 
  
    public Query(int L, int R, int X)  
    { 
        this.L = L; 
        this.R = R; 
        this.X = X; 
    } 
}; 
  
static int maxn = 100; 
  
static int []root = new int[maxn]; 
  
// Find the root of the group containing 
// the element at index x 
static int find(int x) 
{ 
    if(x == root[x]) 
        return x; 
    else
        return root[x] = find(root[x]); 
} 
  
// merge the two groups containing elements 
// at indices x and y into one group 
static void uni(int x, int y) 
{ 
    int p = find(x), q = find(y); 
    if (p != q)  
    { 
        root[p] = root[q]; 
    } 
} 
  
static void initialize(int a[], int n,  
                       Query q[], int m) 
{ 
    // make n subsets with every 
    // element as its root 
    for (int i = 0; i < n; i++) 
        root[i] = i; 
  
    // consecutive elements equal in value are 
    // merged into one single group 
    for (int i = 1; i < n; i++) 
        if (a[i] == a[i - 1]) 
            uni(i, i - 1); 
} 
  
// Driver code 
public static void main(String args[]) 
{ 
    int a[] = { 1, 1, 5, 4, 5 }; 
    int n = a.length; 
    Query q[] = { new Query(0, 2, 2 ),  
                  new Query( 1, 4, 1 ), 
                  new Query( 2, 4, 5 ) }; 
    int m = q.length; 
    initialize(a, n, q, m); 
  
    for (int i = 0; i < m; i++) 
    { 
        int flag = 0; 
        int l = q[i].L, r = q[i].R, x = q[i].X; 
        int p = r; 
  
        while (p >= l) 
        { 
  
            // check if the current element in 
            // consideration is equal to x or not 
            // if it is equal, then x exists in the range 
            if (a[p] == x) 
            { 
                flag = 1; 
                break; 
            } 
            p = find(p) - 1; 
        } 
  
        // Print if x exists or not 
        if (flag != 0) 
            System.out.println(x + " exists between [" +  
                               l + ", " + r + "] "); 
        else
            System.out.println(x + " does not exist between [" +  
                               l + ", " + r + "] "); 
    } 
} 
} 
  
// This code is contributed by 29AjayKumar 
```

## Python3

```py
# Python3 program to determine if the element 
# exists for different range queries 
  
# Structure to represent a query range 
class Query: 
    def __init__(self, L, R, X): 
        self.L = L 
        self.R = R 
        self.X = X 
  
maxn = 100
root = [0] * maxn 
  
# Find the root of the group containing 
# the element at index x 
def find(x): 
    if x == root[x]: 
        return x 
    else: 
        root[x] = find(root[x]) 
        return root[x] 
  
# merge the two groups containing elements 
# at indices x and y into one group 
def uni(x, y): 
    p = find(x) 
    q = find(y) 
    if p != q: 
        root[p] = root[q] 
  
def initialize(a, n, q, m): 
  
    # make n subsets with every 
    # element as its root 
    for i in range(n): 
        root[i] = i 
  
    # consecutive elements equal in value are 
    # merged into one single group 
    for i in range(1, n): 
        if a[i] == a[i - 1]: 
            uni(i, i - 1) 
  
# Driver Code 
if __name__ == "__main__": 
    a = [1, 1, 5, 4, 5] 
    n = len(a) 
  
    q = [Query(0, 2, 2), 
         Query(1, 4, 1),  
         Query(2, 4, 5)] 
           
    m = len(q) 
    initialize(a, n, q, m) 
    for i in range(m): 
        flag = False
        l = q[i].L 
        r = q[i].R 
        x = q[i].X 
        p = r 
  
        while p >= l: 
  
            # check if the current element in 
            # consideration is equal to x or not 
            # if it is equal, then x exists in the range 
            if a[p] == x: 
                flag = True
                break
            p = find(p) - 1
  
        # Print if x exists or not 
        if flag: 
            print("%d exists between [%d, %d]" % (x, l, r)) 
        else: 
            print("%d does not exists between [%d, %d]" % (x, l, r)) 
  
# This code is contributed by 
# sanjeev2552 
```

## C#

```cs
// C# program to determine if the element 
// exists for different range queries 
using System; 
      
class GFG  
{ 
  
// Structure to represent a query range 
public class Query 
{ 
    public int L, R, X; 
  
    public Query(int L, int R, int X)  
    { 
        this.L = L; 
        this.R = R; 
        this.X = X; 
    } 
}; 
  
static int maxn = 100; 
  
static int []root = new int[maxn]; 
  
// Find the root of the group containing 
// the element at index x 
static int find(int x) 
{ 
    if(x == root[x]) 
        return x; 
    else
        return root[x] = find(root[x]); 
} 
  
// merge the two groups containing elements 
// at indices x and y into one group 
static void uni(int x, int y) 
{ 
    int p = find(x), q = find(y); 
    if (p != q)  
    { 
        root[p] = root[q]; 
    } 
} 
  
static void initialize(int []a, int n,  
                     Query []q, int m) 
{ 
    // make n subsets with every 
    // element as its root 
    for (int i = 0; i < n; i++) 
        root[i] = i; 
  
    // consecutive elements equal in value are 
    // merged into one single group 
    for (int i = 1; i < n; i++) 
        if (a[i] == a[i - 1]) 
            uni(i, i - 1); 
} 
  
// Driver code 
public static void Main(String []args) 
{ 
    int []a = { 1, 1, 5, 4, 5 }; 
    int n = a.Length; 
    Query []q = {new Query(0, 2, 2),  
                 new Query(1, 4, 1), 
                 new Query(2, 4, 5)}; 
    int m = q.Length; 
    initialize(a, n, q, m); 
  
    for (int i = 0; i < m; i++) 
    { 
        int flag = 0; 
        int l = q[i].L, r = q[i].R, x = q[i].X; 
        int p = r; 
  
        while (p >= l) 
        { 
  
            // check if the current element in 
            // consideration is equal to x or not 
            // if it is equal, then x exists in the range 
            if (a[p] == x) 
            { 
                flag = 1; 
                break; 
            } 
            p = find(p) - 1; 
        } 
  
        // Print if x exists or not 
        if (flag != 0) 
            Console.WriteLine(x + " exists between [" +  
                                l + ", " + r + "] "); 
        else
            Console.WriteLine(x + " does not exist between [" +  
                              l + ", " + r + "] "); 
    } 
} 
} 
  
// This code is contributed by PrinciRaj1992 
```

输出：

```
2 does not exist between [0, 2] 
1 exists between [1, 4] 
5 exists between [2, 4]
```

高效的方法（使用 Mo 的算法）：

Mo 的算法是平方根分解的最佳应用之一。

它基于使用上一个查询的答案来计算当前查询的答案的基本思想。之所以这样，是因为Mo算法的构造方式是，如果已知`F([L, R])`，则`F([L + 1, R])`，`F([L – 1, R])`， `F([L, R + 1])`和`F([L, R – 1])`可以很容易地计算出来，每个时间都是`O(F)`时间。

按照查询的顺序回答查询，那么时间复杂度并没有提高到所需的水平。为了显着降低时间复杂度，将查询分为多个块，然后进行排序。对查询进行排序的确切算法如下：

+   定义`BLOCK_SIZE = sqrt(N)`
+   具有相同`L / BLOCK_SIZE`的所有查询都放在同一块中
+   在一个块内，查询基于其`R`值进行排序
+   因此，排序功能按以下方式比较两个查询`Q1`和`Q2`：
+   如果满足以下条件，则`Q1`必须早于`Q2`
    1. `L1 / BLOCK_SIZE <L2 / BLOCK_SIZE`
    2. `L1 / BLOCK_SIZE = L2 / BLOCK_SIZE`并且`R1 < R2`

在对查询进行排序之后，下一步是计算第一个查询的答案，并因此回答其余查询。要确定某个特定元素是否存在，请检查该范围内该元素的频率。非零频率确认该范围内元素的存在。

为了存储元素的频率，在以下代码中使用了STL映射。

在给定的示例中，对查询数组进行排序后的第一个查询为`{0, 2, 2}`。散列`[0, 2]`中元素的频率，然后从图中检查元素 2 的频率。由于 2 出现 0 次，因此打印`No`。

在处理下一个查询（在这种情况下为`{1, 4, 1}`）时，递减范围`[0, 1)`中的元素的频率，并递增范围`[3, 4]`中的元素的频率。此步骤给出了`[1, 4]`中元素的频率，并且可以很容易地从图中看出1在该范围内。

时间复杂度：

预处理部分，即对查询进行排序需要`O(m Log m)`时间。

在整个运行过程中，`R`的索引变量最多更改`O(n * sqrt(n))`次，而`L`的索引变量最多更改其值`O(m * sqrt(n))`次。因此，处理所有查询需要`O(n * sqrt(n))+ O(m * sqrt(n))= O((m + n) * sqrt(n))`时间。

以下是上述想法的 C++ 实现：

```cpp

edit
play_arrow

brightness_4
// CPP code to determine if the element 
// exists for different range queries 
#include <bits/stdc++.h> 
  
using namespace std; 
  
// Variable to represent block size. 
// This is made global, so compare()  
// of sort can use it. 
int block; 
  
// Structure to represent a query range 
struct Query  
{ 
    int L, R, X; 
}; 
  
// Function used to sort all queries so 
// that all queries of same block are 
// arranged together and within a block, 
// queries are sorted in increasing order  
// of R values. 
bool compare(Query x, Query y) 
{ 
    // Different blocks, sort by block. 
    if (x.L / block != y.L / block) 
        return x.L / block < y.L / block; 
  
    // Same block, sort by R value 
    return x.R < y.R; 
} 
  
// Determines if the element is present for all 
// query ranges. m is number of queries 
// n is size of array a[]. 
void queryResults(int a[], int n, Query q[], int m) 
{ 
    // Find block size 
    block = (int)sqrt(n); 
  
    // Sort all queries so that queries of same 
    // blocks are arranged together. 
    sort(q, q + m, compare); 
  
    // Initialize current L, current R 
    int currL = 0, currR = 0; 
  
    // To store the frequencies of  
    // elements of the given range 
    map<int, int> mp; 
  
    // Traverse through all queries 
    for (int i = 0; i < m; i++) { 
          
        // L and R values of current range 
        int L = q[i].L, R = q[i].R, X = q[i].X; 
  
        // Decrement frequencies of extra elements 
        // of previous range. For example if previous 
        // range is [0, 3] and current range is [2, 5], 
        // then the frequencies of a[0] and a[1] are decremented 
        while (currL < L)  
        { 
            mp[a[currL]]--; 
            currL++; 
        } 
  
        // Increment frequencies of elements of current Range 
        while (currL > L)  
        { 
            mp[a[currL - 1]]++; 
            currL--; 
        } 
        while (currR <= R)  
        { 
            mp[a[currR]]++; 
            currR++; 
        } 
  
        // Decrement frequencies of elements of previous 
        // range.  For example when previous range is [0, 10]  
        // and current range is [3, 8], then frequencies of  
        // a[9] and a[10] are decremented 
        while (currR > R + 1)  
        { 
            mp[a[currR - 1]]--; 
            currR--; 
        } 
  
        // Print if X exists or not 
        if (mp[X] != 0) 
            cout << X << " exists between [" << L 
                 << ", " << R << "] " << endl; 
        else
            cout << X << " does not exist between [" 
                 << L << ", " << R << "] " << endl; 
    } 
} 
  
// Driver program 
int main() 
{ 
    int a[] = { 1, 1, 5, 4, 5 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    Query q[] = { { 0, 2, 2 }, { 1, 4, 1 }, { 2, 4, 5 } }; 
    int m = sizeof(q) / sizeof(q[0]); 
    queryResults(a, n, q, m); 
    return 0; 
} 
```

输出：

```
2 does not exist between [0, 2] 
1 exists between [1, 4] 
5 exists between [2, 4]
```
