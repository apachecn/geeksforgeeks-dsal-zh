# 与给定的总和和距末端的最大最短距离配对

> 原文： [https://www.geeksforgeeks.org/print-maximum-shortest-distance/](https://www.geeksforgeeks.org/print-maximum-shortest-distance/)

给定一个由`N`个整数和一个整数`K`组成的数组，请选择两个总和为`K`的不同元素，并找出所选择元素到端点的最大最短距离。

**示例**：

```
Input : a[] = {2, 4, 3, 2, 1}
        k = 5.
Output :  2
Explanation:
Select the pair(4, 1). 
Shortest distance of 4 from ends = 2
Shortest distance of 1 from ends = 1
Hence, answer is max(2, 1) = 2      

Input : a[] = {2, 4, 1, 9, 5}
        k = 3
Output : 3
Explanation:
Select the pair (2, 1)
Shortest distance of 2 from ends = 1
Shortest distance of 1 from ends = 3
Hence, answer is max(1, 3) = 3\. 

```

**注意**：末端元素到末端的距离是 1 而不是 0。



**朴素的方法**：该方法是运行两个循环，并在内部循环中检查两个元素是否与和`k`成对。 如果是，则以两个元素之间最短距离的最大值作为答案，将其与前一对元素的最短距离进行比较，并以这两个元素中的最小值作为答案。 循环结束时，我们将获得所需的输出。

**有效方法**：显然，最短距离是指距左端的距离和距右端的距离，即`min(1+i, N-i)`。 让我们将第 i 个元素的最短距离表示为`Di`。 还有另一种情况，即重复选定对中的一个元素，然后在该元素出现的所有最短距离中选择最小的一个。 循环运行，并将所有数组元素中最短的距离存储在另一个数组中（将其设为`D[]`）。 现在，我们得到了所有元素的最短距离。

运行`for`循环。 如果选取的元素是`x`，则另一个元素应该是`k-x`。 用`max(D[x], D[k-x])`更新`ans`，并在每次更新时，选择先前和当前答案中的最小值。 如果`k-x`不在数组中，则`D[k-x]`将为`INFINITE`，这将已经初始化。

## C++ 

```cpp

// C++ code to find maximum shortest distance  
// from endpoints 
#include <bits/stdc++.h> 
using namespace std; 

// function to find maximum shortest distance 
int find_maximum(int a[], int n, int k) 
{    
    // stores the shortest distance of every  
    // element in original array. 
    unordered_map<int, int> b; 

    for (int i = 0; i < n; i++) { 
        int x = a[i]; 

        // shortest distance from ends 
        int d = min(1 + i, n - i);  
        if (b.find(x) == b.end()) 
            b[x] = d;   

        else

            /* if duplicates are found, b[x]  
            is replaced with minimum of the 
            previous and current position's 
            shortest distance*/
            b[x] = min(d, b[x]);  
    } 

    int ans = INT_MAX; 
    for (int i = 0; i < n; i++) { 
        int x = a[i]; 

        // similar elements ignore them  
        // cause we need distinct elements     
        if (x != k - x && b.find(k - x) != b.end())          
            ans = min(max(b[x], b[k - x]), ans);         
    } 
    return ans; 
} 

// driver code 
int main() 
{ 
    int a[] = { 3, 5, 8, 6, 7 }; 
    int K = 11; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << find_maximum(a, n, K) << endl; 
    return 0; 
} 

```

## Java

```
// Java code to find maximum shortest distance  
// from endpoints 
import java.util.*; 
  
class GFG  
{ 
static void makePermutation(int []a, int n) 
{ 
    // Store counts of all elements. 
    HashMap<Integer,  
            Integer> count = new HashMap<Integer,  
                                         Integer>(); 
    for (int i = 0; i < n; i++) 
    { 
        if(count.containsKey(a[i])) 
        { 
            count.put(a[i], count.get(a[i]) + 1); 
        } 
        else
        { 
            count.put(a[i], 1); 
        } 
    } 
} 
  
// function to find maximum shortest distance 
static int find_maximum(int a[], int n, int k) 
{  
    // stores the shortest distance of every  
    // element in original array. 
    HashMap<Integer, 
            Integer> b = new HashMap<Integer, 
                                     Integer>(); 
      
    for (int i = 0; i < n; i++)  
    { 
        int x = a[i]; 
          
        // shortest distance from ends 
        int d = Math.min(1 + i, n - i);  
        if (!b.containsKey(x)) 
            b.put(x, d);  
  
        else
        { 
  
            /* if duplicates are found, b[x]  
            is replaced with minimum of the 
            previous and current position's 
            shortest distance*/
            b. put(x, Math.min(d, b.get(x)));  
        } 
    } 
      
    int ans = Integer.MAX_VALUE; 
    for (int i = 0; i < n; i++)  
    { 
        int x = a[i]; 
          
        // similar elements ignore them  
        // cause we need distinct elements  
        if (x != k - x && b.containsKey(k - x))          
            ans = Math.min(Math.max(b.get(x),  
                                    b.get(k - x)), ans);      
    } 
    return ans; 
} 
  
// Driver Code 
public static void main(String[] args) 
{ 
    int a[] = { 3, 5, 8, 6, 7 }; 
    int K = 11; 
    int n = a.length; 
    System.out.println(find_maximum(a, n, K)); 
} 
} 
  
// This code is contributed by Rajput-Ji
```

## Python3

```
# Python3 code to find maximum shortest  
# distance from endpoints 
  
# function to find maximum shortest distance 
def find_maximum(a, n, k): 
      
    # stores the shortest distance of every  
    # element in original array. 
    b = dict() 
      
    for i in range(n): 
        x = a[i] 
          
        # shortest distance from ends 
        d = min(1 + i, n - i) 
        if x not in b.keys(): 
            b[x] = d 
        else: 
  
            # if duplicates are found, b[x]  
            # is replaced with minimum of the 
            # previous and current position's 
            # shortest distance*/ 
            b[x] = min(d, b[x]) 
      
    ans = 10**9
    for i in range(n): 
        x = a[i] 
          
        # similar elements ignore them  
        # cause we need distinct elements  
        if (x != (k - x) and (k - x) in b.keys()):          
            ans = min(max(b[x], b[k - x]), ans)  
  
    return ans 
  
# Driver code 
a = [3, 5, 8, 6, 7] 
K = 11
n = len(a) 
print(find_maximum(a, n, K)) 
  
# This code is contributed by mohit kumar
```

## C#

```
// C# code to find maximum shortest distance  
// from endpoints 
using System; 
using System.Collections.Generic; 
      
class GFG  
{ 
static void makePermutation(int []a, int n) 
{ 
    // Store counts of all elements. 
    Dictionary<int, 
               int> count = new Dictionary<int, 
                                           int>(); 
    for (int i = 0; i < n; i++) 
    { 
        if(count.ContainsKey(a[i])) 
        { 
            count[a[i]] = count[a[i]] + 1; 
        } 
        else
        { 
            count.Add(a[i], 1); 
        } 
    } 
} 
  
// function to find maximum shortest distance 
static int find_maximum(int []a, int n, int k) 
{  
    // stores the shortest distance of every  
    // element in original array. 
    Dictionary<int, 
               int> b = new Dictionary<int, 
                                       int>(); 
      
    for (int i = 0; i < n; i++)  
    { 
        int x = a[i]; 
          
        // shortest distance from ends 
        int d = Math.Min(1 + i, n - i);  
        if (!b.ContainsKey(x)) 
            b.Add(x, d);  
  
        else
        { 
  
            /* if duplicates are found, b[x]  
            is replaced with minimum of the 
            previous and current position's 
            shortest distance*/
            b[x] = Math.Min(d, b[x]);  
        } 
    } 
      
    int ans = int.MaxValue; 
    for (int i = 0; i < n; i++)  
    { 
        int x = a[i]; 
          
        // similar elements ignore them  
        // cause we need distinct elements  
        if (x != k - x && b.ContainsKey(k - x))          
            ans = Math.Min(Math.Max(b[x],  
                                    b[k - x]), ans);      
    } 
    return ans; 
} 
  
// Driver Code 
public static void Main(String[] args) 
{ 
    int []a = { 3, 5, 8, 6, 7 }; 
    int K = 11; 
    int n = a.Length; 
    Console.WriteLine(find_maximum(a, n, K)); 
} 
} 
  
// This code is contributed by Princi Singh
```

输出：

```
 2
```

