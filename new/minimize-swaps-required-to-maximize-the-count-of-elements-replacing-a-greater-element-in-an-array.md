# 最小化交换以最大化替换数组中较大元素的元素数

> 原文：[https://www.geeksforgeeks.org/minimize-swaps-required-to-maximize-the-count-of-elements-replacing-a-greater-element-in-an-array/](https://www.geeksforgeeks.org/minimize-swaps-required-to-maximize-the-count-of-elements-replacing-a-greater-element-in-an-array/)

给定一个数组 **A []** ，该数组由 **N** 个元素组成，任务是查找所需交换的最小数量，以便在原始数组中交换数组元素以替换更高的元素 ，已最大化。

**示例**：

> **输入**：A [] = {4、3、3、2、5}
> **输出**：3
> **说明**：
> 交换 1：{ **4** ，3、3、2， **5** }-> { **5** ，3、3、2， **4** }
> 交换 2：{ **5** ，3， **3** ，2，4}-> { **3** ，3， **5** ，2、4}。
> 交换 3：{3、3， **5** ， **2** ，4}-> {3、3， **2** ， **5** ，4}
> 因此，元素{4，3，2}在交换
> **输入后占据较高元素的原始位置。 A [] = {6，5，4，3，2，1}
> **输出 L** 5**

**天真的方法**：解决问题的最简单方法可以实现如下：

*   **以升序对**数组进行排序。

*   初始化两个变量，即*结果*，和*索引*，以分别存储计数和在原始数组中已考虑的索引。

*   遍历数组元素。 对于任何元素 **A [i]** ，转到数组中大于 <sub>i</sub> 的值，并相应地增加*索引*变量。

*   找到大于 **A [i]** 的元素后，将*结果*和*索引*递增。

*   如果*索引*已到达数组的末尾，则没有元素可以与先前检查的元素交换。

*   因此，打印**计数**。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of swaps required
int countSwaps(int A[], int n)
{
    // Sort the array in ascending order
    sort(A, A + n);

    int ind = 1, res = 0;

    for (int i = 0; i < n; i++) {

        // Iterate until a greater element
        // is found
        while (ind < n and A[ind] == A[i])

            // Keep incrementing ind
            ind++;

        // If a greater element is found
        if (ind < n and A[ind] > A[i]) {

            // Increase count of swap
            res++;

            // Increment ind
            ind++;
        }

        // If end of array is reached
        if (ind >= n)
            break;
    }

    // Return the answer
    return res;
}

// Driver Code
int main()
{

    int A[] = { 4, 3, 3, 2, 5 };
    cout << countSwaps(A, 5);

    return 0;
}

```

## Java

```java

// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the minimum
// number of swaps required
static int countSwaps(int A[], int n)
{
    // Sort the array in ascending order
    Arrays.sort(A);
    int ind = 1, res = 0;

    for (int i = 0; i < n; i++)
    {

        // Iterate until a greater element
        // is found
        while (ind < n && A[ind] == A[i])

            // Keep incrementing ind
            ind++;

        // If a greater element is found
        if (ind < n && A[ind] > A[i]) 
        {

            // Increase count of swap
            res++;

            // Increment ind
            ind++;
        }

        // If end of array is reached
        if (ind >= n)
            break;
    }

    // Return the answer
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 4, 3, 3, 2, 5 };
    System.out.print(countSwaps(A, 5));
}
}

// This code is contributed by gauravrajput1

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to find the minimum
# number of swaps required
def countSwaps(A, n):

    # Sort the array in ascending order
    A.sort()

    ind, res = 1, 0

    for i in range(n):

        # Iterate until a greater element
        # is found
        while (ind < n and A[ind] == A[i]):

            # Keep incrementing ind
            ind += 1

        # If a greater element is found
        if (ind < n and A[ind] > A[i]):

            # Increase count of swap
            res += 1

            # Increment ind
            ind += 1

        # If end of array is reached
        if (ind >= n):
            break

    # Return the answer
    return res

# Driver Code
A = [ 4, 3, 3, 2, 5 ]

print (countSwaps(A, 5))

# This code is contributed by chitranayal

```

## C#

```cs

// C# Program to implement
// the above approach
using System;
class GFG{

// Function to find the minimum
// number of swaps required
static int countSwaps(int []A, int n)
{
    // Sort the array in ascending order
    Array.Sort(A);
    int ind = 1, res = 0;

    for (int i = 0; i < n; i++)
    {

        // Iterate until a greater element
        // is found
        while (ind < n && A[ind] == A[i])

            // Keep incrementing ind
            ind++;

        // If a greater element is found
        if (ind < n && A[ind] > A[i]) 
        {

            // Increase count of swap
            res++;

            // Increment ind
            ind++;
        }

        // If end of array is reached
        if (ind >= n)
            break;
    }

    // Return the answer
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 4, 3, 3, 2, 5 };
    Console.Write(countSwaps(A, 5));
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
3

```

**时间复杂度**：O（N * log N）

**辅助空间**：`O(1)`

**高效方法**：

由于两个不相等元素之间的任何交换都会导致元素替换较高的元素，因此可以看出，所需的最小交换数为 ***N –（最大交换频率 数组元素）*** 。 因此，使用 [**HashMap**](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 找到数组中最频繁的元素，然后打印结果。

以下是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of swaps required
int countSwaps(int A[], int n)
{
    // Stores the frequency of the
    // array elements
    map<int, int> mp;

    // Stores maximum frequency
    int max_frequency = 0;

    // Find the max frequency
    for (int i = 0; i < n; i++) {

        // Update frequency
        mp[A[i]]++;

        // Update maximum frequency
        max_frequency
            = max(max_frequency, mp[A[i]]);
    }

    return n - max_frequency;
}

// Driver Code
int main()
{

    int A[] = { 6, 5, 4, 3, 2, 1 };

    // function call
    cout << countSwaps(A, 6);

    return 0;
}

```

## Java

```java

// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the minimum
// number of swaps required
static int countSwaps(int arr[], int n)
{
    // Stores the frequency of the
    // array elements
    HashMap<Integer,
              Integer> mp = new HashMap<Integer,
                                        Integer>();

    // Stores maximum frequency
    int max_frequency = 0;

    // Find the max frequency
    for (int i = 0; i < n; i++)
    {

        // Update frequency
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }

        // Update maximum frequency
        max_frequency = Math.max(max_frequency, 
                                 mp.get(arr[i]));
    }
    return n - max_frequency;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 6, 5, 4, 3, 2, 1 };

    // function call
    System.out.print(countSwaps(A, 6));
}
}

// This code is contributed by Rohit_ranjan

```

## Python3

```py

# Python3 Program to implement 
# the above approach 

# Function to find the minimum 
# number of swaps required 
def countSwaps(A, n): 

    # Stores the frequency of the 
    # array elements 
    mp = {} 

    # Stores maximum frequency 
    max_frequency = 0

    # Find the max frequency 
    for i in range(n):

        # Update frequency 
        if A[i] in mp:
            mp[A[i]] += 1
        else:
            mp[A[i]] = 1

        # Update maximum frequency 
        max_frequency = max(max_frequency, 
                            mp[A[i]]) 

    return n - max_frequency

# Driver code
if __name__ == "__main__":    

      A = [6, 5, 4, 3, 2, 1] 

    # function call 
    print(countSwaps(A, 6))

# This code is contributed by divyeshrabadiya07

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum
// number of swaps required
static int countSwaps(int []arr, int n)
{

    // Stores the frequency of the
    // array elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Stores maximum frequency
    int max_frequency = 0;

    // Find the max frequency
    for(int i = 0; i < n; i++)
    {

        // Update frequency
        if(mp.ContainsKey(arr[i]))
        {
            mp[arr[i]] = mp[arr[i]] + 1;
        }
        else
        {
            mp.Add(arr[i], 1);
        }

        // Update maximum frequency
        max_frequency = Math.Max(max_frequency, 
                                 mp[arr[i]]);
    }
    return n - max_frequency;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 6, 5, 4, 3, 2, 1 };

    // Function call
    Console.Write(countSwaps(A, 6));
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
5

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



