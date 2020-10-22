# 稀疏表

> 原文： [https://www.geeksforgeeks.org/sparse-table/](https://www.geeksforgeeks.org/sparse-table/)

我们已经在[范围最小查询（平方根分解和稀疏表）](https://www.geeksforgeeks.org/range-minimum-query-for-static-array/)中简要讨论了稀疏表。

稀疏表概念用于对一组静态数据进行快速查询（元素不变）。 它进行预处理，以便可以有效地回答查询。

示例问题 1：范围最小查询

我们有一个数组`arr[0 ... n-1]`。 我们需要有效地找到从索引`L`（查询开始）到`R`（查询结束）的最小值，其中`0 <= L <= R <= n-1`。 考虑存在许多范围查询的情况。

**示例**：

```
Input:  arr[]   = {7, 2, 3, 0, 5, 10, 3, 12, 18};
        query[] = [0, 4], [4, 7], [7, 8]

Output: Minimum of [0, 4] is 0
        Minimum of [4, 7] is 3
        Minimum of [7, 8] is 12

```

这个想法是预先计算所有大小为`2^j`的子数组的最小值，其中`j`从 0 到`log n`变化。 我们进行表`lookup[i][j]`的查找，使`lookup[i][j]`包含从`i`开始且范围为`2^j`的最小值。 例如，`lookup[0][3]`包含范围为`[0, 7]`的最小值（从 0 开始且大小为`2^3`）

**如何填充此查找表或稀疏表？**

这个想法很简单，使用以前计算的值以自下而上的方式填充。 我们使用 2 的较低乘方的值计算 2 的当前乘方的范围。 例如，要找到范围`[0, 7]`的最小值（范围大小是 3 的幂），我们可以使用以下两个最小值。

1.  范围`[0, 3]`的最小值（范围大小是 2 的幂）

2.  范围`[4, 7]`的最小值（范围大小是 2 的幂）

根据上面的示例，下面是公式，

```
// Minimum of single element subarrays is same
// as the only element.
lookup[i][0] = arr[i]

// If lookup[0][2] <=  lookup[4][2], 
// then lookup[0][3] = lookup[0][2]
If lookup[i][j-1] <= lookup[i+2j-1-1][j-1]
   lookup[i][j] = lookup[i][j-1]

// If lookup[0][2] >  lookup[4][2], 
// then lookup[0][3] = lookup[4][2]
Else 
   lookup[i][j] = lookup[i+2j-1-1][j-1] 
```

![](img/e760c54b1075de94fe0f8d7f96b2cedd.png)

对于任意范围`[L, R]`，我们需要使用 2 的幂的范围。想法是使用 2 的最接近的幂。我们总是需要最多进行一次比较（比较两个是 2 的幂的范围的最小值。 一个范围以`L`开头，以`L +`最近的 2 的幂”结尾。 另一个范围以`R`结束，并以“`R – `最接近的 2 的幂`+ 1`开头。 例如，如果给定范围是`(2, 10)`，我们比较两个范围`(2, 9)`和`(3, 10)`中的最小值。

Based on above example, below is formula,

```
// For (2, 10), j = floor(Log<sub>2</sub>(10-2+1)) = 3
j = floor(Log(R-L+1))

// If lookup[0][3] <=  lookup[3][3], 
// then min(2, 10) = lookup[0][3]
If lookup[L][j] <= lookup[R-(int)pow(2, j)+1][j]
   min(L, R) = lookup[L][j]

// If lookup[0][3] >  arr[lookup[3][3], 
// then min(2, 10) = lookup[3][3]
Else 
   min(L, R) = lookup[i+2j-1-1][j-1]
```

由于我们只进行一次比较，因此查询的时间复杂度为`O(1)`。

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to do range minimum query 
// using sparse table 
#include <bits/stdc++.h> 
using namespace std; 
#define MAX 500 

// lookup[i][j] is going to store minimum 
// value in arr[i..j]. Ideally lookup table 
// size should not be fixed and should be 
// determined using n Log n. It is kept 
// constant to keep code simple. 
int lookup[MAX][MAX]; 

// Fills lookup array lookup[][] in bottom up manner. 
void buildSparseTable(int arr[], int n) 
{ 
    // Initialize M for the intervals with length 1 
    for (int i = 0; i < n; i++) 
        lookup[i][0] = arr[i]; 

    // Compute values from smaller to bigger intervals 
    for (int j = 1; (1 << j) <= n; j++) { 

        // Compute minimum value for all intervals with 
        // size 2^j 
        for (int i = 0; (i + (1 << j) - 1) < n; i++) { 

            // For arr[2][10], we compare arr[lookup[0][7]]  
            // and arr[lookup[3][10]] 
            if (lookup[i][j - 1] <  
                        lookup[i + (1 << (j - 1))][j - 1]) 
                lookup[i][j] = lookup[i][j - 1]; 
            else
                lookup[i][j] =  
                         lookup[i + (1 << (j - 1))][j - 1]; 
        } 
    } 
} 

// Returns minimum of arr[L..R] 
int query(int L, int R) 
{ 
    // Find highest power of 2 that is smaller 
    // than or equal to count of elements in given 
    // range. For [2, 10], j = 3 
    int j = (int)log2(R - L + 1); 

    // Compute minimum of last 2^j elements with first 
    // 2^j elements in range. 
    // For [2, 10], we compare arr[lookup[0][3]] and 
    // arr[lookup[3][3]], 
    if (lookup[L][j] <= lookup[R - (1 << j) + 1][j]) 
        return lookup[L][j]; 

    else
        return lookup[R - (1 << j) + 1][j]; 
} 

// Driver program 
int main() 
{ 
    int a[] = { 7, 2, 3, 0, 5, 10, 3, 12, 18 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    buildSparseTable(a, n); 
    cout << query(0, 4) << endl; 
    cout << query(4, 7) << endl; 
    cout << query(7, 8) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to do range minimum query 
// using sparse table 
import java.io.*; 

class GFG { 

    static int MAX =500; 

    // lookup[i][j] is going to store minimum 
    // value in arr[i..j]. Ideally lookup table 
    // size should not be fixed and should be 
    // determined using n Log n. It is kept 
    // constant to keep code simple. 
    static int [][]lookup = new int[MAX][MAX]; 

    // Fills lookup array lookup[][] in bottom up manner. 
    static void buildSparseTable(int arr[], int n) 
    { 

        // Initialize M for the intervals with length 1 
        for (int i = 0; i < n; i++) 
            lookup[i][0] = arr[i]; 

        // Compute values from smaller to bigger intervals 
        for (int j = 1; (1 << j) <= n; j++) { 

            // Compute minimum value for all intervals with 
            // size 2^j 
            for (int i = 0; (i + (1 << j) - 1) < n; i++) { 

                // For arr[2][10], we compare arr[lookup[0][7]]  
                // and arr[lookup[3][10]] 
                if (lookup[i][j - 1] <  
                            lookup[i + (1 << (j - 1))][j - 1]) 
                    lookup[i][j] = lookup[i][j - 1]; 
                else
                    lookup[i][j] =  
                            lookup[i + (1 << (j - 1))][j - 1]; 
            } 
        } 
    } 

    // Returns minimum of arr[L..R] 
    static int query(int L, int R) 
    { 

        // Find highest power of 2 that is smaller 
        // than or equal to count of elements in given 
        // range. For [2, 10], j = 3 
        int j = (int)Math.log(R - L + 1); 

        // Compute minimum of last 2^j elements with first 
        // 2^j elements in range. 
        // For [2, 10], we compare arr[lookup[0][3]] and 
        // arr[lookup[3][3]], 
        if (lookup[L][j] <= lookup[R - (1 << j) + 1][j]) 
            return lookup[L][j]; 

        else
            return lookup[R - (1 << j) + 1][j]; 
    } 

    // Driver program 
    public static void main (String[] args) 
    { 
        int a[] = { 7, 2, 3, 0, 5, 10, 3, 12, 18 }; 
        int n = a.length; 

        buildSparseTable(a, n); 

        System.out.println(query(0, 4)); 
        System.out.println(query(4, 7)); 
        System.out.println(query(7, 8)); 

    } 
} 

// This code is contributed by vt_m. 

```

## Python3

```py

# Python3 program to do range minimum  
# query using sparse table  
import math 

# Fills lookup array lookup[][] in  
# bottom up manner.  
def buildSparseTable(arr, n): 

    # Initialize M for the intervals 
    # with length 1  
    for i in range(0, n):  
        lookup[i][0] = arr[i]  

    j = 1

    # Compute values from smaller to  
    # bigger intervals  
    while (1 << j) <= n:  

        # Compute minimum value for all  
        # intervals with size 2^j 
        i = 0
        while (i + (1 << j) - 1) < n:  

            # For arr[2][10], we compare arr[lookup[0][7]]  
            # and arr[lookup[3][10]]  
            if (lookup[i][j - 1] <  
                lookup[i + (1 << (j - 1))][j - 1]):  
                lookup[i][j] = lookup[i][j - 1]  
            else: 
                lookup[i][j] = \ 
                        lookup[i + (1 << (j - 1))][j - 1]  

            i += 1
        j += 1        

# Returns minimum of arr[L..R]  
def query(L, R):  

    # Find highest power of 2 that is smaller  
    # than or equal to count of elements in  
    # given range. For [2, 10], j = 3  
    j = int(math.log2(R - L + 1))  

    # Compute minimum of last 2^j elements  
    # with first 2^j elements in range.  
    # For [2, 10], we compare arr[lookup[0][3]]  
    # and arr[lookup[3][3]],  
    if lookup[L][j] <= lookup[R - (1 << j) + 1][j]:  
        return lookup[L][j]  

    else: 
        return lookup[R - (1 << j) + 1][j]  

# Driver Code 
if __name__ == "__main__": 

    a = [7, 2, 3, 0, 5, 10, 3, 12, 18]  
    n = len(a)  
    MAX = 500

    # lookup[i][j] is going to store minimum  
    # value in arr[i..j]. Ideally lookup table  
    # size should not be fixed and should be  
    # determined using n Log n. It is kept  
    # constant to keep code simple.  
    lookup = [[0 for i in range(MAX)] 
                 for j in range(MAX)] 

    buildSparseTable(a, n)  
    print(query(0, 4))  
    print(query(4, 7))  
    print(query(7, 8))  

# This code is contributed by Rituraj Jain 

```

## C# 

```cs

// C# program to do range minimum query 
// using sparse table 
using System; 

public class GFG { 

    static int MAX= 500; 

    // lookup[i][j] is going to store minimum 
    // value in arr[i..j]. Ideally lookup table 
    // size should not be fixed and should be 
    // determined using n Log n. It is kept 
    // constant to keep code simple. 
    static int [,]lookup = new int[MAX, MAX]; 

    // Fills lookup array lookup[][] in bottom up manner. 
    static void buildSparseTable(int []arr, int n) 
    { 
        // Initialize M for the intervals with length 1 
        for (int i = 0; i < n; i++) 
            lookup[i, 0] = arr[i]; 

        // Compute values from smaller to bigger intervals 
        for (int j = 1; (1 << j) <= n; j++) { 

            // Compute minimum value for all intervals with 
            // size 2^j 
            for (int i = 0; (i + (1 << j) - 1) < n; i++) { 

                // For arr[2][10], we compare arr[lookup[0][7]]  
                // and arr[lookup[3][10]] 
                if (lookup[i, j - 1] <  
                            lookup[i + (1 << (j - 1)), j - 1]) 
                    lookup[i, j] = lookup[i, j - 1]; 
                else
                    lookup[i, j] =  
                            lookup[i + (1 << (j - 1)), j - 1]; 
            } 
        } 
    } 

    // Returns minimum of arr[L..R] 
    static int query(int L, int R) 
    { 

        // Find highest power of 2 that is smaller 
        // than or equal to count of elements in given 
        // range. For [2, 10], j = 3 
        int j = (int)Math.Log(R - L + 1); 

        // Compute minimum of last 2^j elements with first 
        // 2^j elements in range. 
        // For [2, 10], we compare arr[lookup[0][3]] and 
        // arr[lookup[3][3]], 
        if (lookup[L, j] <= lookup[R - (1 << j) + 1, j]) 
            return lookup[L, j]; 

        else
            return lookup[R - (1 << j) + 1, j]; 
    } 

    // Driver program 
    static public void Main () 
    { 
        int []a = { 7, 2, 3, 0, 5, 10, 3, 12, 18 }; 
        int n = a.Length; 

        buildSparseTable(a, n); 

        Console.WriteLine(query(0, 4)); 
        Console.WriteLine(query(4, 7)); 
        Console.WriteLine(query(7, 8)); 
    } 
} 

// This code is contributed by vt_m.  

```

Output:

```
Minimum of [0, 4] is 0
Minimum of [4, 7] is 3
Minimum of [7, 8] is 12
```

因此，稀疏表方法支持`O(1)`时间，`O(N log N)`预处理时间和`O(N log N)`空间的查询操作。

示例问题 2：范围 GCD 查询

我们有一个数组`arr[0 ... n-1]`。 我们需要找到`L`和`R`范围内的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)，其中 `0 <= L <= R <= n-1`。 考虑存在许多范围查询的情况，例如：

```
Input : arr[] = {2, 3, 5, 4, 6, 8}
        queries[] = {(0, 2), (3, 5), (2, 3)}
Output : 1
         2
         1

```

**我们使用 GCD 的以下属性**：

*   GCD 函数是关联的，`GCD(a, b, c)= GCD(GCD(a, b), c)= GCD(a, GCD(b, c))`，我们可以使用子范围的 GCD 计算范围的 GCD 。

*   如果我们多次采用重叠范围的 GCD，那么它不会改变答案。 例如，`GCD(a, b, c)= GCD(GCD(a, b), GCD(b, c))`。 因此，像最小范围查询问题一样，我们只需进行一次比较即可找到给定范围的 GCD。

我们使用与上述相同的逻辑构建一个稀疏表。 建立稀疏表后，我们可以通过以 2 的幂打破给定范围来找到所有 GCD，并将每张 GCD 加到当前答案中。

## C++

```cpp

// C++ program to do range minimum query 
// using sparse table 
#include <bits/stdc++.h> 
using namespace std; 
#define MAX 500 

// lookup[i][j] is going to store GCD of 
// arr[i..j]. Ideally lookup table 
// size should not be fixed and should be 
// determined using n Log n. It is kept 
// constant to keep code simple. 
int table[MAX][MAX]; 

// it builds sparse table. 
void buildSparseTable(int arr[], int n) 
{ 
    // GCD of single element is element itself 
    for (int i = 0; i < n; i++) 
        table[i][0] = arr[i]; 

    // Build sparse table 
    for (int j = 1; j <= n; j++) 
        for (int i = 0; i <= n - (1 << j); i++) 
            table[i][j] = __gcd(table[i][j - 1], 
                    table[i + (1 << (j - 1))][j - 1]); 
} 

// Returns GCD of arr[L..R] 
int query(int L, int R) 
{ 
    // Find highest power of 2 that is smaller 
    // than or equal to count of elements in given 
    // range.For [2, 10], j = 3 
    int j = (int)log2(R - L + 1); 

    // Compute GCD of last 2^j elements with first 
    // 2^j elements in range. 
    // For [2, 10], we find GCD of arr[lookup[0][3]] and 
    // arr[lookup[3][3]], 
    return __gcd(table[L][j], table[R - (1 << j) + 1][j]); 
} 

// Driver program 
int main() 
{ 
    int a[] = { 7, 2, 3, 0, 5, 10, 3, 12, 18 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    buildSparseTable(a, n); 
    cout << query(0, 2) << endl; 
    cout << query(1, 3) << endl; 
    cout << query(4, 5) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to do range minimum query  
// using sparse table  
import java.util.*; 

class GFG 
{  
static final int MAX = 500;  

// lookup[i][j] is going to store GCD of  
// arr[i..j]. Ideally lookup table  
// size should not be fixed and should be  
// determined using n Log n. It is kept  
// constant to keep code simple.  
static int [][]table = new int[MAX][MAX];  

// it builds sparse table.  
static void buildSparseTable(int arr[],  
                             int n)  
{  
    // GCD of single element is 
    // element itself  
    for (int i = 0; i < n; i++)  
        table[i][0] = arr[i];  

    // Build sparse table  
    for (int j = 1; j <= n; j++)  
        for (int i = 0; i <= n - (1 << j); i++)  
            table[i][j] = __gcd(table[i][j - 1],  
                                table[i + (1 << (j - 1))][j - 1]);  
}  

// Returns GCD of arr[L..R]  
static int query(int L, int R)  
{  
    // Find highest power of 2 that is  
    // smaller than or equal to count of  
    // elements in given range.For [2, 10], j = 3  
    int j = (int)Math.log(R - L + 1);  

    // Compute GCD of last 2^j elements  
    // with first 2^j elements in range.  
    // For [2, 10], we find GCD of  
    // arr[lookup[0][3]] and arr[lookup[3][3]],  
    return __gcd(table[L][j],  
                 table[R - (1 << j) + 1][j]);  
}  

static int __gcd(int a, int b)  
{  
    return b == 0 ? a : __gcd(b, a % b);      
} 

// Driver Code 
public static void main(String[] args)  
{  
    int a[] = { 7, 2, 3, 0, 5, 10, 3, 12, 18 };  
    int n = a.length;  
    buildSparseTable(a, n);  
    System.out.print(query(0, 2) + "\n");  
    System.out.print(query(1, 3) + "\n");  
    System.out.print(query(4, 5) + "\n");  
}  
}  

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 program to do range minimum  
# query using sparse table  
import math 

# Fills lookup array lookup[][] in  
# bottom up manner.  
def buildSparseTable(arr, n): 

    # GCD of single element is element itself  
    for i in range(0, n):  
        table[i][0] = arr[i]  

    # Build sparse table 
    j = 1
    while (1 << j) <= n:  
        i = 0
        while i <= n - (1 << j):  
            table[i][j] = math.gcd(table[i][j - 1],  
                                   table[i + (1 << (j - 1))][j - 1]) 

            i += 1
        j += 1

# Returns minimum of arr[L..R]  
def query(L, R):  

    # Find highest power of 2 that is smaller  
    # than or equal to count of elements in  
    # given range. For [2, 10], j = 3  
    j = int(math.log2(R - L + 1))  

    # Compute GCD of last 2^j elements with  
    # first 2^j elements in range.  
    # For [2, 10], we find GCD of arr[lookup[0][3]]  
    # and arr[lookup[3][3]],  
    return math.gcd(table[L][j],  
                    table[R - (1 << j) + 1][j]) 

# Driver Code  
if __name__ == "__main__": 

    a = [7, 2, 3, 0, 5, 10, 3, 12, 18]  
    n = len(a)  
    MAX = 500

    # lookup[i][j] is going to store minimum  
    # value in arr[i..j]. Ideally lookup table  
    # size should not be fixed and should be  
    # determined using n Log n. It is kept  
    # constant to keep code simple.  
    table = [[0 for i in range(MAX)]  
                for j in range(MAX)] 

    buildSparseTable(a, n)  
    print(query(0, 2))  
    print(query(1, 3))  
    print(query(4, 5))  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to do range minimum query  
// using sparse table  
using System; 

class GFG 
{  
static readonly int MAX = 500;  

// lookup[i,j] is going to store GCD of  
// arr[i..j]. Ideally lookup table  
// size should not be fixed and should be  
// determined using n Log n. It is kept  
// constant to keep code simple.  
static int [,]table = new int[MAX, MAX];  

// it builds sparse table.  
static void buildSparseTable(int []arr,  
                             int n)  
{  
    // GCD of single element is 
    // element itself  
    for (int i = 0; i < n; i++)  
        table[i, 0] = arr[i];  

    // Build sparse table  
    for (int j = 1; j <= n; j++)  
        for (int i = 0; i <= n - (1 << j); i++)  
            table[i, j] = __gcd(table[i, j - 1],  
                                table[i + (1 << (j - 1)),  
                                                 j - 1]);  
}  

// Returns GCD of arr[L..R]  
static int query(int L, int R)  
{  
    // Find highest power of 2 that is  
    // smaller than or equal to count of  
    // elements in given range. 
    // For [2, 10], j = 3  
    int j = (int)Math.Log(R - L + 1);  

    // Compute GCD of last 2^j elements  
    // with first 2^j elements in range.  
    // For [2, 10], we find GCD of  
    // arr[lookup[0,3]] and arr[lookup[3,3]],  
    return __gcd(table[L, j],  
                 table[R - (1 << j) + 1, j]);  
}  

static int __gcd(int a, int b)  
{  
    return b == 0 ? a : __gcd(b, a % b);      
} 

// Driver Code 
public static void Main(String[] args)  
{  
    int []a = { 7, 2, 3, 0, 5, 10, 3, 12, 18 };  
    int n = a.Length;  
    buildSparseTable(a, n);  
    Console.Write(query(0, 2) + "\n");  
    Console.Write(query(1, 3) + "\n");  
    Console.Write(query(4, 5) + "\n");  
}  
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
1
1
5

```



* * *

* * *



