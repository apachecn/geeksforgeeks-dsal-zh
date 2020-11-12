# 使两个数组元素相等的最小按位与运算

> 原文：[https://www.geeksforgeeks.org/minimum-bitwise-and-operations-to-make-any-two-array-elements-equal/](https://www.geeksforgeeks.org/minimum-bitwise-and-operations-to-make-any-two-array-elements-equal/)

给定一个大小为`n`的整数数组和一个整数`k`，

我们可以在任意数组元素和`k`之间执行任意次的按位 AND 运算。

该任务是打印使数组中任何两个元素相等所需的最小数量此类操作。

如果执行上述操作后无法使数组的任何两个元素相等，则打印 -1。

**示例**：

> 输入：`k = 6`; 数组：`1, 2, 1, 2`
>
> 输出：0
>
> 说明：数组中已经有两个相等的元素，因此答案为 0。
> 
> 输入：`k = 2`; 数组：`5, 6, 2, 4`
>
> 输出：1
>
> 说明：如果对元素 6 应用 AND 操作，它将变为`6 & 2 = 2`
>
> 且数组将变为`5 2 2 4`
>
> 现在，数组有两个相等的元素，因此答案为 1。
> 
> 输入：`k = 15`; 数组：`1, 2, 3`
>
> 输出：-1
>
> 说明：无论我们执行上述操作多少次，
>
> 该数组永远不会有相等的元素对。 所以答案是 -1

**方法**：

关键观察是，如果可以制作所需的数组，则答案将为 0，1 或 2。 它永远不会超过 2。

> 因为，如果`x & k = y`，那么，无论您执行了多少次`y & k`，它始终会给出`y`。

*   如果数组中已经有相等的元素，则答案将为 0。

*   对于答案为 1，我们将创建一个新数组`b`，其中包含`b[i] = a[i] & K`，

    现在，对于每个`a[i]`，我们将检查是否存在任何索引`j`，即`i != j`和`a[i] = b[j]`。

    如果是，则答案为 1。

*   对于答案为 2，我们将在新数组`b`

    中检查索引`i`是否存在索引`j`，使得`i != j`和`b[i] = b[j]`。

    如果是，则答案为 2。

*   如果不满足上述任何条件，则答案为 -1。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to count the 
// minimum operations required. 
int minOperations(int a[], int n, int K) 
{ 
    unordered_map<int, bool> map; 
    for (int i = 0; i < n; i++) { 

        // check if the initial array 
        // already contains an equal pair 
        if (map[a[i]])  
            return 0; 
        map[a[i]] = true; 
    } 

    // create new array with AND operations 
    int b[n]; 
    for (int i = 0; i < n; i++)  
        b[i] = a[i] & K;     

    // clear the map 
    map.clear(); 

    // Check if the solution 
    // is a single operation 
    for (int i = 0; i < n; i++) { 

        // If Bitwise operation between 
        //'k' and a[i] gives 
        // a number other than a[i] 
        if (a[i] != b[i]) 
            map[b[i]] = true; 
    } 

    // Check if any of the a[i] 
    // gets equal to any other element 
    // of the array after the operation. 
    for (int i = 0; i < n; i++)  

        // Single operation 
        // will be enough 
        if (map[a[i]])  
           return 1; 

    // clear the map 
    map.clear(); 

    // Check if the solution 
    // is two operations 
    for (int i = 0; i < n; i++) { 

        // Check if the array 'b' 
        // contains duplicates 
        if (map[b[i]])  
           return 2; 

        map[b[i]] = true; 
    } 

    // otherwise it is impossible to 
    // create such an array with 
    // Bitwise AND operations 
    return -1; 
} 

// Driver code 
int main() 
{ 

    int K = 3; 
    int a[] = { 1, 2, 3, 7 }; 
    int n = sizeof(a)/sizeof(a[0]); 

    // Function call to compute the result 
    cout << minOperations(a, n, K); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 

class geeks 
{ 

    // Function to count the 
    // minimum operations required. 
    public static int minOperations(int[] a, int n, int K) 
    { 
        HashMap<Integer, Boolean> map = new HashMap<>(); 

        for (int i = 0; i < n; i++) 
        { 

            // check if the initial array 
            // already contains an equal pair 
            // try-catch is used so that 
            // nullpointer exception can be handeled 
            try 
            { 
                if (map.get(a[i])) 
                    return 1; 
            }  
            catch (Exception e)  
            { 
                //TODO: handle exception 
            } 

            try 
            { 
                map.put(a[i], true); 
            } catch (Exception e) {} 
        } 

        // create new array with AND operations 
        int[] b = new int[n]; 
        for (int i = 0; i < n; i++) 
            b[i] = a[i] & K; 

        // clear the map 
        map.clear(); 

        // Check if the solution 
        // is a single operation 
        for (int i = 0; i < n; i++) 
        { 

            // If Bitwise operation between 
            // 'k' and a[i] gives 
            // a number other than a[i] 
            if (a[i] != b[i]) 
            { 
                try 
                { 
                    map.put(b[i], true); 
                } 
                catch (Exception e) {} 
            } 
        } 

        // Check if any of the a[i] 
        // gets equal to any other element 
        // of the array after the operation. 
        for (int i = 0; i < n; i++) 
        { 

            // Single operation 
            // will be enough 
            try 
            { 
                if (map.get(a[i])) 
                    return 1; 
            } 
            catch (Exception e)  
            { 
                //TODO: handle exception 
            } 
        } 

        // clear the map 
        map.clear(); 

        // Check if the solution 
        // is two operations 
        for (int i = 0; i < n; i++) 
        { 

            // Check if the array 'b' 
            // contains duplicates 
            try
            { 
                if (map.get(b[i])) 
                    return 2; 
            }  
            catch (Exception e)  
            { 
                //TODO: handle exception 
            } 

            try
            { 
                map.put(b[i], true); 
            }  
            catch (Exception e)  
            { 
                //TODO: handle exception 
            } 
        } 

        // otherwise it is impossible to 
        // create such an array with 
        // Bitwise AND operations 
        return -1; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        int K = 3; 
        int[] a = { 1, 2, 3, 7 }; 
        int n = a.length; 

        // Function call to compute the result 
        System.out.println(minOperations(a, n, K)); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python3 implementation of the approach  
from collections import defaultdict 

# Function to count the minimum  
# operations required.  
def minOperations(a, n, K):  

    Map = defaultdict(lambda:False) 
    for i in range(0, n):  

        # check if the initial array  
        # already contains an equal pair  
        if Map[a[i]] == True:  
            return 0
        Map[a[i]] = True

    # create new array with AND operations  
    b = []  
    for i in range(0, n):  
        b.append(a[i] & K)  

    # clear the map  
    Map.clear()  

    # Check if the solution  
    # is a single operation  
    for i in range(0, n):  

        # If Bitwise operation between  
        #'k' and a[i] gives  
        # a number other than a[i]  
        if a[i] != b[i]: 
            Map[b[i]] = True

    # Check if any of the a[i]  
    # gets equal to any other element  
    # of the array after the operation.  
    for i in range(0, n):  

        # Single operation  
        # will be enough  
        if Map[a[i]] == True: 
            return 1

    # clear the map  
    Map.clear()  

    # Check if the solution  
    # is two operations  
    for i in range(0, n):  

        # Check if the array 'b'  
        # contains duplicates  
        if Map[b[i]] == True:  
            return 2

        Map[b[i]] = True

    # otherwise it is impossible to  
    # create such an array with  
    # Bitwise AND operations  
    return -1

# Driver code  
if __name__ == "__main__":  

    K = 3
    a = [1, 2, 3, 7]  
    n = len(a)  

    # Function call to compute the result  
    print(minOperations(a, n, K))  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation of the approach  
using System;  
using System.Collections.Generic;  

class GFG  
{  

    // Function to return the count of  
    // minimum operations required  
    public static int minOperations(int[] a,  
                                    int n, int K)  
    {  

        Dictionary<int, Boolean> map =  
                new Dictionary<int, Boolean>();  

        for (int i = 0; i < n; i++)  
        {  

            // Check if the initial array  
            // already contains an equal pair  
            if (map.ContainsKey(a[i]))  
                return 0;  

            map.Add(a[i], true);  
        }  

        // Create new array with AND operations  
        int[] b = new int[n];  
        for (int i = 0; i < n; i++)  
            b[i] = a[i] & K;  

        // Clear the map  
        map.Clear();  

        // Check if the solution  
        // is a single operation  
        for (int i = 0; i < n; i++)  
        {  

            // If Bitwise OR operation between  
            // 'k' and a[i] gives  
            // a number other than a[i]  
            if (a[i] != b[i])  
                map.Add(b[i], true);  
        }  

        // Check if any of the a[i]  
        // gets equal to any other element  
        // of the array after the operation  
        for (int i = 0; i < n; i++)  
        {  

            // Single operation  
            // will be enough  
            if (map.ContainsKey(a[i]))  
                return 1;  
        }  

        // Clear the map  
        map.Clear();  

        // Check if the solution  
        // is two operations  
        for (int i = 0; i < n; i++)  
        {  

            // Check if the array 'b'  
            // contains duplicates  
            if (map.ContainsKey(b[i]))  
                return 2;  
            map.Add(b[i], true);  
        }  

        // Otherwise it is impossible to  
        // create such an array with  
        // Bitwise OR operations  
        return -1;  
    }  

    // Driver code  
    public static void Main(String[] args)  
    {  
        int K = 3;  
        int[] a = { 1, 2, 3, 7 };  
        int n = a.Length;  
        Console.WriteLine(minOperations(a, n, K));  
    }  
}  

// This code is contributed by Rajput-Ji  

```

**输出**：

```
1

```

**复杂度**：`O(n)`



* * *

* * *



