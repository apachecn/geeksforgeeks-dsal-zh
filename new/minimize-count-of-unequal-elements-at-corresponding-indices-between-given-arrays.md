# 最小化给定数组之间相应索引处不等元素的数量

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A []** 和 **B []** ，它们由 **N** 个正整数和一个矩阵 **List [] []组成** 由 **M** 对索引组成，任务是最大程度地减少不相等的相同索引元素的数量（ **A <sub>i</sub> ！= B <sub>i</sub>** ），方法是在数组 A []中的任意一对给定索引之间交换。

**示例**：

> **输入**：N = 5，M = 4，A [] = {1，5，9，2，3}，B [] = {2，4，5，1，3}，列表[ ] [] = {{1，4}，{2，3}，{3，5}，{2，5}}}
> **输出**：1
> **HTG7]
> 初始数组 A [] = {1、5、9、2、3}
> A []中的交换索引（1、4）= {2、5、9、1、3}
> 在 A [] = {2，9，5，1，1，3}中交换索引（2，3）
> 因此，在比较最终数组 A []（= {2，9，5，1，3} ）与数组 B []（= {2，4，5，1，3}），唯一不相等的相同索引元素对是 A [2]！= B [2]（基于 1 的索引）**
> 
> **输入**：N = 5，M = 4，A [] = {1，10，19，6，2}，B [] = {1，6，10，2，19}，列表[ ] [] = {{1，4}，{2，3}，{3，5}，{2，5}}
> **输出**：2

**方法**：由于可以在对对列表中指定的数组 A []的元素进行任意次数的交换，因此可以将这些元素视为已连接的[集](https://www.geeksforgeeks.org/union-find/)，并且在其内部进行交换 允许的元素。 以下是实现此方法的步骤：

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) A []并创建一组[连接的组件](http://www.geeksforgeeks.org/strongly-connected-components/)，可以使用[不交集](https://www.geeksforgeeks.org/disjoint-set-data-structures/)轻松完成。
2.  对于 **B []** 中的每个元素，查找 **A []** **（A [i]，B [i]）**中的相应元素是否属于同一连接 组件与否。
3.  如果是，则使 A [i] = B [i]并继续。 否则，增加不匹配对的数量。
4.  完成上述所有步骤后，打印不匹配对的计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h>  
using namespace std;  

int find(int par[],int x); 
void unionn(int par[], int a, int b); 

// Function that count of the mismatched 
// pairs in bot the array 
int countPairs(int A[], int B[], int N, 
               int M, int List[][2]) 
{ 
    int count = 0; 

    // Create a parent array 
    // and initialize it 
    int par[N + 1]; 
    for(int i = 0; i <= N; i++) 
        par[i] = i; 

    // Preprocessing of the given 
    // pairs of indices 
    for(int i = 0; i < M; i++) 
    { 

        // 1-based indexing 
        int index1 = find(par, List[i][0] - 1); 
        int index2 = find(par, List[i][1] - 1); 

        // If both indices doesn't belong 
        // to same component 
        if (index1 != index2) 
        { 

            // Insert the indices in 
            // same component 
            unionn(par, index1, index2); 
        } 
    } 

    // Map to get the indices 
    // of array A 
    map<int, int> mp; 

    for(int i = 0; i < N; i++) 
    { 
        mp[A[i]] = i; 
    } 

    for(int i = 0; i < N; i++) 
    { 
        if (A[i] != B[i]) 
        { 

            // If current element is not 
            // present in array B then 
            // count this as mismatched 
            if(mp.find(B[i]) == mp.end()) 
            { 
                count++; 
                continue; 
            } 

            // Get the index of the element 
            // in array B 
            int j = mp[B[i]]; 

            // Check if both indices belong 
            // to same connected component 
            // if not increment the count 
            if (find(par, i) != find(par, j)) 
                count++; 
        } 
    } 

    // Return answer 
    return count; 
} 

// Function that gives the connected 
// component of each index 
int find(int par[],int x) 
{ 
    if (par[x] == x) 
        return x; 
    else
        return par[x] = find(par, par[x]); 
} 

// Function that creates the 
// connected componenets 
void unionn(int par[], int a, int b) 
{ 

    // Find parent of a and b 
    // recursively 
    a = find(par, a); 
    b = find(par, b); 

    if (a == b) 
        return; 

    // Update the parent of a 
    par[a] = b; 
}  

// Driver Code 
int main() 
{ 
    int N = 5; 
    int M = 4; 

    // Given arrays A[], B[] 
    int A[] = { 1, 5, 9, 2, 3 }; 
    int B[] = { 2, 4, 5, 1, 3 }; 

    // List of indices 
    int List[][2] = { { 1, 4 }, { 2, 3 }, 
                      { 3, 5 }, { 2, 5 } }; 

    // Function call 
    cout << countPairs(A, B, N, M, List); 

    return 0; 
}  

// This code is contributed by rutvik_56 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG { 

    // Function that count of the mismatched 
    // pairs in bot the array 
    public static int countPairs(int A[], int B[], 
                                int N, int M, 
                                int[][] List) 
    { 
        int count = 0; 

        // Create a parent array 
        // and initialize it 
        int par[] = new int[N + 1]; 
        for (int i = 0; i <= N; i++) 
            par[i] = i; 

        // Preprocessing of the given 
        // pairs of indices 
        for (int i = 0; i < M; i++) { 

            // 1-based indexing 
            int index1 
                = find(par, List[i][0] - 1); 
            int index2 
                = find(par, List[i][1] - 1); 

            // If both indices doesn't belong 
            // to same component 
            if (index1 != index2) { 

                // Insert the indices in 
                // same component 
                union(par, index1, index2); 
            } 
        } 

        // HashMap to get the indices 
        // of array A 
        HashMap<Integer, Integer> map 
            = new HashMap<>(); 

        for (int i = 0; i < N; i++) { 
            map.put(A[i], i); 
        } 

        for (int i = 0; i < N; i++) { 
            if (A[i] != B[i]) { 

                // If current element is not 
                // present in array B then 
                // count this as mismatched 
                if (!map.containsKey(B[i])) { 
                    count++; 

                    continue; 
                } 

                // Get the index of the element 
                // in array B 
                int j = map.get(B[i]); 

                // Check if both indices belong 
                // to same connected component 
                // if not increment the count 
                if (find(par, i) != find(par, j)) 
                    count++; 
            } 
        } 

        // Return answer 
        return count; 
    } 

    // Function that gives the connected 
    // component of each index 
    public static int find(int par[], 
                        int x) 
    { 
        if (par[x] == x) 
            return x; 
        else
            return par[x] 
                = find(par, par[x]); 
    } 

    // Function that creates the 
    // connected componenets 
    public static void
    union(int par[], int a, int b) 
    { 
        // Find parent of a and b 
        // recursively 
        a = find(par, a); 
        b = find(par, b); 
        if (a == b) 
            return; 

        // Update the parent of a 
        par[a] = b; 
    } 

    // Driver Code 
    public static void
        main(String[] args) 
    { 
        int N = 5; 
        int M = 4; 

        // Given arrays A[], B[] 
        int A[] = { 1, 5, 9, 2, 3 }; 
        int B[] = { 2, 4, 5, 1, 3 }; 

        // List of indices 
        int List[][] 
            = { { 1, 4 }, { 2, 3 },  
                { 3, 5 }, { 2, 5 } }; 

        // Function Call 
        System.out.println( 
            countPairs(A, B, N, M, List)); 
    } 
} 

```

## Python3

```py

# Python3 program for the above approach  

# Function that count of the mismatched 
# pairs in bot the array  
def countPairs(A, B, N, M, List): 

    count = 0

    # Create a parent array 
    # and initialize it 
    par = [0] * (N + 1) 
    for i in range(N + 1): 
        par[i] = i 

    # Preprocessing of the given 
    # pairs of indices 
    for i in range(M): 

        # 1-based indexing 
        index1 = find(par, List[i][0] - 1) 
        index2 = find(par, List[i][1] - 1) 

        # If both indices doesn't belong 
        # to same component 
        if(index1 != index2): 

            # Insert the indices in 
            # same component 
            union(par, index1, index2) 

    # HashMap to get the indices 
    # of array A 
    map = {} 

    for i in range(N): 
        map[A[i]] = i 

    for i in range(N): 
        if(A[i] != B[i]): 

            # If current element is not 
            # present in array B then 
            # count this as mismatched 
            if(B[i] not in map.keys()): 
                count += 1
                continue

            # Get the index of the element 
            # in array B 
            j = map[B[i]] 

            # Check if both indices belong 
            # to same connected component 
            # if not increment the count 
            if(find(par, i) != find(par, j)): 
                count += 1

    # Return answer 
    return count 

# Function that gives the connected 
# component of each index 
def find(par, x): 

    if(par[x] == x): 
        return x 
    else: 
        par[x] = find(par, par[x]) 
        return par[x] 

# Function that creates the 
# connected componenets 
def union(par, a, b): 

    # Find parent of a and b 
    # recursively 
    a = find(par, a) 
    b = find(par, b) 

    if(a == b): 
        return

    # Update the parent of a 
    par[a] = b 

# Driver Code 
N = 5
M = 4

# Given arrays A[], B[] 
A = [ 1, 5, 9, 2, 3 ] 
B = [ 2, 4, 5, 1, 3 ] 

# List of indices 
List = [ [ 1, 4 ], [ 2, 3 ], 
        [ 3, 5 ], [ 2, 5 ] ] 

# Function call 
print(countPairs(A, B, N, M, List)) 

# This code is contributed by Shivam Singh 

```

## C#

```cs

// C# program for the above approach 
using System; 
using System.Collections.Generic; 
class GFG{ 

    // Function that count of the mismatched 
    // pairs in bot the array 
    public static int countPairs(int[] A, int[] B, int N, 
                                int M, int[, ] List) 
    { 
        int count = 0; 

        // Create a parent array 
        // and initialize it 
        int[] par = new int[N + 1]; 
        for (int i = 0; i <= N; i++) 
            par[i] = i; 

        // Preprocessing of the given 
        // pairs of indices 
        for (int i = 0; i < M; i++)  
        { 

            // 1-based indexing 
            int index1 = find(par, List[i, 0] - 1); 
            int index2 = find(par, List[i, 1] - 1); 

            // If both indices doesn't belong 
            // to same component 
            if (index1 != index2) 
            { 

                // Insert the indices in 
                // same component 
                union(par, index1, index2); 
            } 
        } 

        // Dictionary to get the indices 
        // of array A 
        Dictionary<int, int> map = new Dictionary<int, int>(); 
        for (int i = 0; i < N; i++)  
        { 
            if (map.ContainsKey(A[i])) 
                map[A[i]] = i; 
            else
                map.Add(A[i], i); 
        } 

        for (int i = 0; i < N; i++)  
        { 
            if (A[i] != B[i])  
            { 

                // If current element is not 
                // present in array B then 
                // count this as mismatched 
                if (!map.ContainsKey(B[i]))  
                { 
                    count++; 
                    continue; 
                } 

                // Get the index of the element 
                // in array B 
                int j = map[B[i]]; 

                // Check if both indices belong 
                // to same connected component 
                // if not increment the count 
                if (find(par, i) != find(par, j)) 
                    count++; 
            } 
        } 

        // Return answer 
        return count; 
    } 

    // Function that gives the connected 
    // component of each index 
    public static int find(int[] par, int x) 
    { 
        if (par[x] == x) 
            return x; 
        else
            return par[x] = find(par, par[x]); 
    } 

    // Function that creates the 
    // connected componenets 
    public static void union(int[] par, int a, int b) 
    { 
        // Find parent of a and b 
        // recursively 
        a = find(par, a); 
        b = find(par, b); 
        if (a == b) 
            return; 

        // Update the parent of a 
        par[a] = b; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int N = 5; 
        int M = 4; 

        // Given arrays []A, []B 
        int[] A = {1, 5, 9, 2, 3}; 
        int[] B = {2, 4, 5, 1, 3}; 

        // List of indices 
        int[, ] List = {{1, 4}, {2, 3}, {3, 5}, {2, 5}}; 

        // Function Call 
        Console.WriteLine(countPairs(A, B, N, M, List)); 
    } 
} 

// This code is contributed by shikhasingrajput 

```

**Output:** 

```
1

```

***时间复杂度**：O（N + M）*
***辅助空间**：O（N）*



* * *

* * *



