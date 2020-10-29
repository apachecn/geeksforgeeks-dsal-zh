# 在给定的嵌套数组

> 原文：[https://www.geeksforgeeks.org/find-element-with-highest-frequency-in-given-nested-array/](https://www.geeksforgeeks.org/find-element-with-highest-frequency-in-given-nested-array/)

中查找频率最高的元素

给定 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** 。 任务是创建给定阵列 **arr []** 的频率阵列 **freq []** ，并找到频率阵列的最大元素。 如果数组 **freq []** 中两个元素的频率相同，则返回值较小的元素。

**示例**：

> **输入**：arr [] = {1，1，1，2，3，2，2，3，5，5，5，5，4，4，4，4，4};
> **输出**：3
> **说明**：
> 元素的频率由以下公式给出：
> val-> freq []
> 1-> 3
> 2-> 3
> 3-> 2
> 4-> 5
> 5-> 4
> 元素 3 在 频率阵列。
> 
> **输入**：arr [] = {3、5、15、51、15、14、14、14、14、4}；
> **输出**：1
> **说明**：
> 元素的频率由以下公式给出：
> val-> freq []
> 3-> 1
> 4-> 1
> 5-> 1
> 14-> 4
> 15-> 2
> 51-> 1
> 元素 1 在频率阵列中具有最大频率。

**方法**：

1.  将 **arr []** 的元素的频率存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)说 **map1** 中，并以 **arr []** 的元素作为它们的频率 频率作为值。

2.  现在，将 **map1** 的元素频率存储在其他地图中，例如 **map2** 。

3.  遍历 **map2** 获得最高元素。

4.  如果存在多个最高元素，则打印出具有较低值的元素。

下面是上述方法的实现：

## C++ 14

```

// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the highest
// frequency of frequency array
int findElement(int a[], int n)
{
    // To find the maximum frequency
    // initialize it with INT_MIN
    int mx = INT_MIN;
    int ans = 0;

    // Initialize maps to store the
    // count of element in array
    map<int, int> map1, map2;

    // Store the frequency of
    // element of array in map1
    for (int i = 0; i < n; i++) {
        map1[a[i]]++;
    }

    // Storing the frequency i.e.,
    // (x.second) which is count of
    // element in array
    for (auto x : map1) {
        map2[x.second]++;
    }

    for (auto x : map2) {

        // Check if the fequency of
        // element is greater than mx
        if (x.second > mx) {
            mx = x.second;

            // Store the value to check
            // when frequency is same
            ans = x.first;
        }

        // If frequency of 2 element is
        // same than storing minimum value
        else if (x.second == mx) {
            ans = min(ans, x.first);
        }
    }

    // Return the highest frequency
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 1, 1, 2, 3, 2, 2, 3, 5,
                  5, 5, 5, 4, 4, 4, 4, 4 };

    // Size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findElement(arr, n) << endl;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;

class GFG{

// Function to get the highest
// frequency of frequency array
static int findElement(int a[], int n)
{

    // To find the maximum frequency
    // initialize it with INT_MIN
    int mx = Integer.MIN_VALUE;
    int ans = 0;

    // Initialize maps to store the
    // count of element in array
    Map<Integer, Integer> map1 = new HashMap<>(),
                          map2 = new HashMap<>();

    // Store the frequency of
    // element of array in map1
    for(int i = 0; i < n; i++)
    {
        map1.put(a[i], map1.getOrDefault(a[i], 0) + 1);
    }

    // Storing the frequency i.e.,
    // (x.second) which is count of
    // element in array
    for(Integer x : map1.values()) 
    {
        map2.put(x, map2.getOrDefault(x, 0) + 1);
    }

    for(Map.Entry<Integer, Integer> x : map2.entrySet())
    {

        // Check if the fequency of
        // element is greater than mx
        if (x.getValue() > mx)
        {
            mx = x.getValue();

            // Store the value to check
            // when frequency is same
            ans = x.getKey();
        }

        // If frequency of 2 element is
        // same than storing minimum value
        else if (x.getValue() == mx)
        {
            ans = Math.min(ans, x.getKey());
        }
    }

    // Return the highest frequency
    return ans;
}

// Driver code
public static void main (String[] args) 
{

    // Given array arr[]
    int arr[] = { 1, 1, 1, 2, 3, 2, 2, 3, 5,
                  5, 5, 5, 4, 4, 4, 4, 4 };

    // Size of the array
    int n = arr.length;

    // Function call
    System.out.println(findElement(arr, n));
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program for the above approach
import sys

# Function to get the highest
# frequency of frequency array
def findElement(a, n):

    # To find the maximum frequency
    # initialize it with INT_MIN
    mx = -sys.maxsize - 1
    ans = 0

    # Initialize maps to store the
    # count of element in array
    map1 = {}
    map2 = {}

    # Store the frequency of
    # element of array in map1
    for i in a:
        map1[i] = map1.get(i, 0) + 1

    # Storing the frequency i.e.,
    # (x.second) which is count of
    # element in array
    for x in map1:
        map2[map1[x]] = map2.get(map1[x], 0) + 1

    for x in map2:

        # Check if the fequency of
        # element is greater than mx
        if (map2[x] > mx):
            mx = map2[x]

            # Store the value to check
            # when frequency is same
            ans = x

        # If frequency of 2 element is
        # same than storing minimum value
        elif (map2[x] == mx):
            ans = min(ans, x)

    # Return the highest frequency
    return ans

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 1, 1, 2, 3, 2, 2, 3, 
            5, 5, 5, 5, 4, 4, 4, 4, 4]

    # Size of the array
    n = len(arr)

    # Function call
    print(findElement(arr, n))

# This code is contributed by mohit kumar 29

```

**Output:** 

```
3

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



