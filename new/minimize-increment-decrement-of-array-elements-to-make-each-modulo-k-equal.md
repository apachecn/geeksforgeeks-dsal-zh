# 最小化数组元素的增减，以使每个模`K`相等

> 原文：[https://www.geeksforgeeks.org/minimize-increment-decrement-of-array-elements-to-make-each-modulo-k-equal/](https://www.geeksforgeeks.org/minimize-increment-decrement-of-array-elements-to-make-each-modulo-k-equal/)

给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，长度为`N`和整数`K`。 在每个操作中，可以从数组中选择任何元素（例如`arr[i]`），并且可以将其更改为`arr[i] + 1`或`arr[i] – 1`。 任务是找到在数组上执行所需的最少操作数，以使数组以`K`为模的每个值保持相同。

**示例**：

> **输入**：`arr[] = {4, 5, 8, 3, 12}, k = 5`
>
> **输出**：4
>
> **说明**：
>
> 操作 1：`{3, 5, 8, 3, 12}`，将索引 0 处的 4 减少 1。
>
> 操作 2：`{3, 4, 8, 8, 3, 12}`，将索引 1 处的 5 减少 1。
>
> 操作 3：`{3, 3, 8, 3, 12}`，将索引 1 处的 4 减少 1。
>
> 操作 4：`{3, 3, 8, 3, 13}`，将索引 1 处的 12 增加 4 乘 1。
>
> 每个数字的模等于 3，所需的最小步长为 4。
> 
> **输入**：`arr[] = {2, 35, 48, 23, 52}, k = 3`
>
> **输出**：2
>
> **说明**：
>
> 使每个数字的模相等所需的最小步数为 2。

**方法**：想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)来保持已获取的每个模的数量。

*   现在，针对范围`0 <= i`

*   如果小于获得的值小于当前存储的值，则对其进行更新。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
// required to make the modulo of each
// element of the array equal to each other
int Find_min(set<int>& diff_mod,
             map<int, int> count_mod, int k)
{
    // Variable to store minimum
    // operation required
    int min_oprn = INT_MAX;

    // To store operation required to
    // make all modulo equal
    int oprn = 0;

    // Iterating through all
    // possible modulo value
    for (int x = 0; x < k; x++) {
        oprn = 0;

        // Iterating through all different
        // modulo obtained so far
        for (auto w : diff_mod) {

            // Caculating oprn required
            // to make all modulos equal
            // to x
            if (w != x) {

                if (w == 0) {

                    // Checking the operations
                    // that will cost less
                    oprn += min(x, k - x)
                            * count_mod[w];
                }

                else {

                    // Check operation that
                    // will cost less
                    oprn += min(
                                abs(x - w),
                                k + x - w)
                            * count_mod[w];
                }
            }
        }

        // Update the minimum
        // number of operations
        if (oprn < min_oprn)
            min_oprn = oprn;
    }

    // Returing the answer
    return min_oprn;
}

// Function to store different modulos
int Cal_min(int arr[], int n, int k)
{
    // Set to store all
    // different modulo
    set<int> diff_mod;

    // Map to store count
    // of all different  modulo
    // obtained
    map<int, int> count_mod;

    // Storing all different
    // modulo count
    for (int i = 0; i < n; i++) {

        // Insert into the set
        diff_mod.insert(arr[i] % k);

        // Increment count
        count_mod[arr[i] % k]++;
    }

    // Function call to return value of
    // min oprn required
    return Find_min(diff_mod, count_mod, k);
}

// Driver Code
int main()
{
    int arr[] = { 2, 35, 48, 23, 52 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;
    cout << Cal_min(arr, n, k);
    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum operations
// required to make the modulo of each
// element of the array equal to each other
static int Find_min(HashSet<Integer> diff_mod,
                    HashMap<Integer, 
                            Integer> count_mod,
                    int k)
{

    // Variable to store minimum
    // operation required
    int min_oprn = Integer.MAX_VALUE;

    // To store operation required to
    // make all modulo equal
    int oprn = 0;

    // Iterating through all
    // possible modulo value
    for(int x = 0; x < k; x++)
    {
        oprn = 0;

        // Iterating through all different
        // modulo obtained so far
        for(int w : diff_mod) 
        {

            // Caculating oprn required
            // to make all modulos equal
            // to x
            if (w != x) 
            {
                if (w == 0)
                {

                    // Checking the operations
                    // that will cost less
                    oprn += Math.min(x, k - x) *
                            count_mod.get(w);
                }
                else
                {

                    // Check operation that
                    // will cost less
                    oprn += Math.min(Math.abs(x - w), 
                                     k + x - w) * 
                                     count_mod.get(w);
                }
            }
        }

        // Update the minimum
        // number of operations
        if (oprn < min_oprn)
            min_oprn = oprn;
    }

    // Returing the answer
    return min_oprn;
}

// Function to store different modulos
static int Cal_min(int arr[], int n, int k)
{

    // Set to store all
    // different modulo
    HashSet<Integer> diff_mod = new HashSet<>();

    // Map to store count
    // of all different modulo
    // obtained
    HashMap<Integer, 
            Integer> count_mod = new HashMap<>();

    // Storing all different
    // modulo count
    for(int i = 0; i < n; i++) 
    {

        // Insert into the set
        diff_mod.add(arr[i] % k);

        // Increment count
        count_mod.put(arr[i] % k, 
        count_mod.getOrDefault(arr[i] % k, 0) + 1);
    }

    // Function call to return value of
    // min oprn required
    return Find_min(diff_mod, count_mod, k);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 35, 48, 23, 52 };
    int n = arr.length;
    int k = 3;

    System.out.print(Cal_min(arr, n, k));
}
}

// This code is contributed by jrishabh99

```

## Python3

```py

# Python3 program for 
# the above approach
import sys
from collections import defaultdict

# Function to find the minimum operations
# required to make the modulo of each
# element of the array equal to each other
def Find_min(diff_mod,
             count_mod, k):

    # Variable to store minimum
    # operation required
    min_oprn = sys.maxsize

    # To store operation required to
    # make all modulo equal
    oprn = 0

    # Iterating through all
    # possible modulo value
    for x in range (k):
        oprn = 0

        # Iterating through all different
        # modulo obtained so far
        for w in diff_mod:

            # Caculating oprn required
            # to make all modulos equal
            # to x
            if (w != x):

                if (w == 0):

                    # Checking the operations
                    # that will cost less
                    oprn += (min(x, k - x) *
                             count_mod[w])

                else:

                    # Check operation that
                    # will cost less
                    oprn += (min(abs(x - w), 
                                     k + x - w) *
                                     count_mod[w])

        # Update the minimum
        # number of operations
        if (oprn < min_oprn):
            min_oprn = oprn

    # Returing the answer
    return min_oprn

# Function to store different modulos
def Cal_min(arr,  n, k):

    # Set to store all
    # different modulo
    diff_mod = set([])

    # Map to store count
    # of all different  modulo
    # obtained
    count_mod = defaultdict (int)

    # Storing all different
    # modulo count
    for i in range (n):

        # Insert into the set
        diff_mod.add(arr[i] % k)

        # Increment count
        count_mod[arr[i] % k] += 1

    # Function call to return value of
    # min oprn required
    return Find_min(diff_mod, count_mod, k)

# Driver Code
if __name__ == "__main__":  
    arr = [2, 35, 48, 23, 52]
    n = len(arr)
    k = 3
    print( Cal_min(arr, n, k))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum operations
// required to make the modulo of each
// element of the array equal to each other
static int Find_min(HashSet<int> diff_mod,
                    Dictionary<int, 
                               int> count_mod,
                    int k)
{

    // Variable to store minimum
    // operation required
    int min_oprn = int.MaxValue;

    // To store operation required to
    // make all modulo equal
    int oprn = 0;

    // Iterating through all
    // possible modulo value
    for(int x = 0; x < k; x++)
    {
        oprn = 0;

        // Iterating through all different
        // modulo obtained so far
        foreach(int w in diff_mod) 
        {

            // Caculating oprn required
            // to make all modulos equal
            // to x
            if (w != x) 
            {
                if (w == 0)
                {

                    // Checking the operations
                    // that will cost less
                    oprn += Math.Min(x, k - x) *
                            count_mod[w];
                }
                else
                {

                    // Check operation that
                    // will cost less
                    oprn += Math.Min(Math.Abs(x - w), 
                                     k + x - w) * 
                                     count_mod[w];
                }
            }
        }

        // Update the minimum
        // number of operations
        if (oprn < min_oprn)
            min_oprn = oprn;
    }

    // Returing the answer
    return min_oprn;
}

// Function to store different modulos
static int Cal_min(int []arr, int n, int k)
{

    // Set to store all
    // different modulo
    HashSet<int> diff_mod = new HashSet<int>();

    // Map to store count
    // of all different modulo
    // obtained
    Dictionary<int, 
               int> count_mod = new Dictionary<int,
                                               int>();

    // Storing all different
    // modulo count
    for(int i = 0; i < n; i++) 
    {

        // Insert into the set
        diff_mod.Add(arr[i] % k);

        // Increment count
        if(count_mod.ContainsKey((arr[i] % k)))
            count_mod[arr[i] % k] = count_mod[(arr[i] % k)]+1;
        else
            count_mod.Add(arr[i] % k, 1);
    }

    // Function call to return value of
    // min oprn required
    return Find_min(diff_mod, count_mod, k);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 35, 48, 23, 52 };
    int n = arr.Length;
    int k = 3;

    Console.Write(Cal_min(arr, n, k));
}
}

// This code is contributed by Amit Katiyar 

```

**输出**： 

```
2

```

**时间复杂度**：`O(N * K)`



* * *

* * *



