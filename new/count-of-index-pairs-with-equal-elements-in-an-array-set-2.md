# 数组中具有相等元素的索引对的计数 | 系列 2

> 原文：[https://www.geeksforgeeks.org/count-of-index-pairs-with-equal-elements-in-an-array-set-2/](https://www.geeksforgeeks.org/count-of-index-pairs-with-equal-elements-in-an-array-set-2/)

给定`N`个元素的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`。 任务是计算索引`(i, j)`的总数，以使`arr[i] = arr[j]`和`i != j`。

**示例**：

> **输入**：`arr[] = {1, 2, 1, 1} `​​
>
> **输出**：3
>
> **说明**：
>
> 在数组中 `arr[0] = arr[2] = arr [3]`
>
> 有效对为`（0, 2)`, `(0, 3)`和`(2, 3)`
> 
> **输入**：`arr[] = {2, 2, 3, 2, 3}`
>
> **输出**：4
>
> **说明**：
>
> 在数组中`arr[0] = arr[1] = arr[3]`和`arr[2] = arr[4]`
>
> 所以有效对是`(0, 1)`，`(0, 3)`，`(1, 3)`，`(2, 4)`

对于朴素和有效的方法，请参阅本文的[先前文章](https://www.geeksforgeeks.org/count-index-pairs-equal-elements-array/)。

**更好的方法-使用两个指针**：这个想法是[对给定的数组和具有相同元素的索引差进行](https://www.geeksforgeeks.org/sorting-algorithms/)排序。 步骤如下：

1.  排序给定的数组。

2.  将两个指针**左侧**和**右侧**分别初始化为 0 和 1。

3.  现在直到右边小于 **N** ，执行以下操作：

    *   如果元素索引的左侧和右侧相同，则增加右侧指针并将右侧指针和左侧指针的**差加到最终计数中。**

    *   否则更新从左到右的值。

4.  完成上述步骤后，打印计数值。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the pair in
// the array arr[]
int countPairs(int arr[], int n)
{
    int ans = 0;

    // Sort the array
    sort(arr, arr + n);

    // Initialize two pointers
    int left = 0, right = 1;
    while (right < n) {

        if (arr[left] == arr[right])

            // Add all valid pairs to answer
            ans += right - left;
        else
            left = right;
        right++;
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 2, 3, 2, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << countPairs(arr, N);
    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
class GFG{

// Function that counts the pair in
// the array arr[]
static int countPairs(int arr[], int n)
{
    int ans = 0;

    // Sort the array
    Arrays.sort(arr);

    // Initialize two pointers
    int left = 0, right = 1;
    while (right < n) 
    {
        if (arr[left] == arr[right])

            // Add all valid pairs to answer
            ans += right - left;
        else
            left = right;
        right++;
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 2, 2, 3, 2, 3 };

    int N = arr.length;

    // Function call
    System.out.print(countPairs(arr, N));
}
}

// This code is contributed by Rohit_ranjan

```

## Python3

```py

# Python3 program for the above approach

# Function that counts the pair in
# the array arr[]
def countPairs(arr, n):

    ans = 0

    # Sort the array
    arr.sort()

    # Initialize two pointers
    left = 0
    right = 1;
    while (right < n):

        if (arr[left] == arr[right]):

            # Add all valid pairs to answer
            ans += right - left;
        else:
            left = right;
        right += 1

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [2, 2, 3, 2, 3]

    N = len(arr)

    # Function call
    print (countPairs(arr, N))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program for the above approach
using System;
class GFG{

// Function that counts the pair in
// the array []arr
static int countPairs(int []arr, int n)
{
    int ans = 0;

    // Sort the array
    Array.Sort(arr);

    // Initialize two pointers
    int left = 0, right = 1;
    while (right < n) 
    {
        if (arr[left] == arr[right])

            // Add all valid pairs to answer
            ans += right - left;
        else
            left = right;
        right++;
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int []arr = { 2, 2, 3, 2, 3 };

    int N = arr.Length;

    // Function call
    Console.Write(countPairs(arr, N));
}
}

// This code is contributed by sapnasingh4991

```

**Output:** 

```
4

```

**时间复杂度**：`O(N * log N)`

**辅助空间**：`O(1)`

**高效方法–使用单个遍历**：的想法是使用 [**散列**](https://www.geeksforgeeks.org/hashing-data-structure/) 并更新频率大于 1 的每对的计数。以下是步骤：

1.  创建一个 [unordered_map](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) **M** ，以将每个元素的[频率存储在数组](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)中。

2.  遍历给定的数组，并继续更新 **M** 中每个元素的频率。

3.  在上述步骤中更新频率时，如果任何元素的频率大于 0，则将该频率计数为最终计数。

4.  完成上述步骤后，打印对数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that count the pairs having
// same elements in the array arr[]
int countPairs(int arr[], int n)
{
    int ans = 0;

    // Hash map to keep track of
    // occurences of elements
    unordered_map<int, int> count;

    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Check if occurence of arr[i] > 0
        // add count[arr[i]] to answer
        if (count[arr[i]] != 0)
            ans += count[arr[i]];

        // Increase count of arr[i]
        count[arr[i]]++;
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 1, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << countPairs(arr, N);
    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
class GFG{

// Function that count the pairs having
// same elements in the array arr[]
static int countPairs(int arr[], int n)
{
    int ans = 0;

    // Hash map to keep track of
    // occurences of elements
    HashMap<Integer, 
            Integer> count = new HashMap<>();

    // Traverse the array arr[]
    for (int i = 0; i < n; i++)
    {

        // Check if occurence of arr[i] > 0
        // add count[arr[i]] to answer
        if(count.containsKey(arr[i]))
        {
            ans += count.get(arr[i]);
            count.put(arr[i], count.get(arr[i]) + 1);
        }
        else
        {
            count.put(arr[i], 1);
        }
    }

    // Return the result
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 1, 2, 1, 1 };
    int N = arr.length;

    // Function call
    System.out.print(countPairs(arr, N));
}
}

// This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that count the pairs having
// same elements in the array []arr
static int countPairs(int []arr, int n)
{
    int ans = 0;

    // Hash map to keep track of
    // occurences of elements
    Dictionary<int,
                 int> count = new Dictionary<int,
                                             int>();

    // Traverse the array []arr
    for (int i = 0; i < n; i++)
    {

        // Check if occurence of arr[i] > 0
        // add count[arr[i]] to answer
        if(count.ContainsKey(arr[i]))
        {
            ans += count[arr[i]];
            count[arr[i]] = count[arr[i]] + 1;
        }
        else
        {
            count.Add(arr[i], 1);
        }
    }

    // Return the result
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    // Given array []arr
    int []arr = { 1, 2, 1, 1 };
    int N = arr.Length;

    // Function call
    Console.Write(countPairs(arr, N));
}
}

// This code is contributed by PrinciRaj1992

```

**Output:** 

```
3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



