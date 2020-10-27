# 数组

的任何其他元素不能除的元素数

给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是确定数组元素的数量，该数量不能被给定数组中的任何其他元素整除。
**范例**：

> **输入**：arr [] = {86，45，18，4，8，28，19，33，2}
> **输出**：4
> **说明 **：
> 元素{2，19，33，45}不能被任何其他数组元素整除。
> 
> **输入**：arr [] = {3，3，3}
> **输出**：0

**朴素的方法**：朴素的方法是遍历整个数组并计算给定数组中任何其他元素不能整除的元素数并打印计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to count the number of
// elements of array which are not
// divisible by any other element
// in the array arr[]
int count(int a[], int n)
{
    int countElements = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        bool flag = true;
        for (int j = 0; j < n; j++) {

            // Check if the element
            // is itself or not
            if (i == j)
                continue;

            // Check for divisibility
            if (a[i] % a[j] == 0) {
                flag = false;
                break;
            }
        }

        if (flag == true)
            ++countElements;
    }

    // Return the final result
    return countElements;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 86, 45, 18, 4, 8,
                  28, 19, 33, 2 };
    int n = sizeof(arr) / sizeof(int);

    // Function Call
    cout << count(arr, n);
    return 0;
}

```

## Java

```java

// Java program for the above approach
class GFG{

// Function to count the number of
// elements of array which are not
// divisible by any other element
// in the array arr[]
static int count(int a[], int n)
{
    int countElements = 0;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        boolean flag = true;
        for(int j = 0; j < n; j++) 
        {

            // Check if the element
            // is itself or not
            if (i == j)
                continue;

            // Check for divisibility
            if (a[i] % a[j] == 0)
            {
                flag = false;
                break;
            }
        }

        if (flag == true)
            ++countElements;
    }

    // Return the final result
    return countElements;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 86, 45, 18, 4, 8,
                  28, 19, 33, 2 };

    int n = arr.length;

    // Function call
    System.out.print(count(arr, n));
}
}

// This code is contributed by Amit Katiyar

```

## Python3

```py

# Python3 program for 
# the above approach

# Function to count the number of
# elements of array which are not
# divisible by any other element
# in the array arr[]
def count(a, n):

    countElements = 0

    # Iterate over the array
    for i in range (n):

        flag = True
        for j in range (n):

            # Check if the element
            # is itself or not
            if (i == j):
                continue

            # Check for divisibility
            if (a[i] % a[j] == 0):
                flag = False
                break

        if (flag == True):
            countElements += 1

    # Return the final result
    return countElements

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [86, 45, 18, 4, 
           8, 28, 19, 33, 2]
    n = len(arr)

    # Function Call
    print( count(arr, n))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program for the 
// above approach
using System;
class GFG{

// Function to count the 
// number of elements of 
// array which are not
// divisible by any other 
// element in the array []arr
static int count(int []a, 
                 int n)
{
  int countElements = 0;

  // Iterate over the array
  for(int i = 0; i < n; i++)
  {
    bool flag = true;
    for(int j = 0; j < n; j++) 
    {
      // Check if the element
      // is itself or not
      if (i == j)
        continue;

      // Check for divisibility
      if (a[i] % a[j] == 0)
      {
        flag = false;
        break;
      }
    }

    if (flag == true)
      ++countElements;
  }

  // Return the readonly result
  return countElements;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int []arr = {86, 45, 18, 4, 8,
               28, 19, 33, 2};

  int n = arr.Length;

  // Function call
  Console.Write(count(arr, n));
}
}

// This code is contributed by Rajput-Ji

```

**Output**

```
4
```

**时间复杂度**：*O（N <sup>2</sup> ）*。
**辅助空间**：*O（1）*

**有效方法**：为优化上述方法，我们将使用[硅酮筛网](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的概念。 步骤如下：

1.  初始化一个布尔数组（例如 **v []** ），其大小等于数组中存在的最大元素+ 1，并且每个索引的**为**。
2.  遍历给定数组 **arr []** ，并将当前元素的多个索引处的值更改为数组 **v []** 中的 **false** 。
3.  创建一个[哈希图](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)，并在其中存储每个元素的频率。
4.  对于数组中的每个元素（例如 **current_element** ），如果 **v [current_element]** 为 true，则该元素不能被给定数组中的任何其他元素整除，并增加该数组的计数 当前元素。
5.  完成上述步骤后，打印**计数**的最终值。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// elements of array which are not
// divisible by any other element
// of same array
int countEle(int a[], int n)
{
    // Length for boolean array
    int len = 0;

    // Hash map for storing the
    // element and it's frequency
    unordered_map<int, int> hmap;
    for (int i = 0; i < n; i++) {

        // Update the maximum element
        len = max(len, a[i]);
        hmap[a[i]]++;
    }

    // Boolean array of size
    // of the max element + 1
    bool v[len + 1];

    for (int i = 0; i <= len; i++) {
        v[i] = true;
    }

    // Marking the multiples as false
    for (int i = 0; i < n; i++) {

        if (v[a[i]] == false)
            continue;

        for (int j = 2 * a[i];
             j <= len; j += a[i]) {
            v[j] = false;
        }
    }

    // To store the final count
    int count = 0;

    // Traverse boolean array
    for (int i = 1; i <= len; i++) {

        // Check if i is not divisible by
        // any other array elements and
        // appears in the array only once
        if (v[i] == true
            && hmap.count(i) == 1
            && hmap[i] == 1) {
            count += 1;
        }
    }

    // Return the final Count
    return count;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 86, 45, 18, 4, 8,
                  28, 19, 33, 2 };
    int n = sizeof(arr) / sizeof(int);

    // Function Call
    cout << countEle(arr, n);

    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
import java.util.*;
class GFG{

// Function to count the 
// number of elements of 
// array which are not 
// divisible by any other 
// element of same array
static int countEle(int a[], 
                    int n)
{
  // Length for boolean array
  int len = 0;

  // Hash map for storing the
  // element and it's frequency
  HashMap<Integer,
          Integer> hmap = new HashMap<>();

  for (int i = 0; i < n; i++) 
  {
    // Update the maximum element
    len = Math.max(len, a[i]);

    if(hmap.containsKey(a[i]))
    {
      hmap.put(a[i], 
      hmap.get(a[i]) + 1);
    }
    else
    {
      hmap.put(a[i], 1);
    }
  }

  // Boolean array of size
  // of the max element + 1
  boolean []v = new boolean[len + 1];

  for (int i = 0; i <= len; i++) 
  {
    v[i] = true;
  }

  // Marking the multiples 
  // as false
  for (int i = 0; i < n; i++) 
  {
    if (v[a[i]] == false)
      continue;

    for (int j = 2 * a[i];
             j <= len; j += a[i]) 
    {
      v[j] = false;
    }
  }

  // To store the 
  // final count
  int count = 0;

  // Traverse boolean array
  for (int i = 1; i <= len; i++) 
  {
    // Check if i is not divisible by
    // any other array elements and
    // appears in the array only once
    if (v[i] == true &&
        hmap.containsKey(i) && 
        hmap.get(i) == 1 && 
        hmap.get(i) == 1) 
    {
      count += 1;
    }
  }

  // Return the final 
  // Count
  return count;
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int arr[] = {86, 45, 18, 4, 8,
               28, 19, 33, 2};
  int n = arr.length;

  // Function Call
  System.out.print(countEle(arr, n));
}
}

// This code is contributed by Princi Singh

```

**Output**

```
4
```

**时间复杂度**：*O（N * log（M））*其中 N 是给定数组中元素的数量，M 是给定数组中的最大元素。
**辅助空间**：*O（M + N）*其中 N 是给定数组中元素的数量，M 是给定数组中的最大元素。



* * *

* * *



