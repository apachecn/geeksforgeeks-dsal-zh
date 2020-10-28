# 计算频率等于其值的元素| 设置 2

给定一个大小为 **N** 的整数 **arr []** 数组，任务是对频率等于其值的频率的所有元素进行计数。

**范例**：

> **输入**：arr [] = {3，2，2，3，4，3}
> **输出**：2
> **说明**：
> 元素 2 的频率为 2
> 元素 3 的频率为 3
> 元素 4 的频率为 1
> 2 和 3 是具有与其值相同频率的元素
> 
> **输入**：arr [] = {1、2、3、4、5、6}
> **输出**：1

**方法**：遵循以下步骤解决问题：

1.  将每个值小于等于给定数组大小的每个数组元素的频率存储在 **freq []** 数组中。

2.  进行上述步骤的原因是，一个元素的频率最多可以等于给定数组的大小。 因此，无需存储其值大于给定数组大小的元素的频率。

3.  计算频率等于其值的整数。

4.  打印最终计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program of the 
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the integer
// which has a frequency in the
// array equal to its value.
void solve(int arr[], int n)
{
    // Store frequency of array
    // elements
    int freq[n+1] ={0};

    for (int i = 0; i < n; i++) {

        // Store the frequency
        // only if arr[i]<=n
        if (arr[i] <= n)
            freq[arr[i]]++;
    }

    // Initially the count is zero
    int count = 0;

    for (int i = 1; i <= n; i++) {
        // If the freq[i] is equal
        // to i, then increment
        // the count by 1
        if (i == freq[i]) {
            count++;
        }
    }

    // Print the final count
    cout << count << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 1, 3, 2, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    solve(arr, N);
    return 0;
}

```

## Java

```java

// Java program of the 
// above approach
class GFG{

// Function to find the integer
// which has a frequency in the
// array equal to its value.
static void solve(int arr[], 
                  int n)
{
  // Store frequency of array
  // elements
  int []freq = new int[n + 1];

  for (int i = 0; i < n; i++) 
  {
    // Store the frequency
    // only if arr[i]<=n
    if (arr[i] <= n)
      freq[arr[i]]++;
  }

  // Initially the count is zero
  int count = 0;

  for (int i = 1; i <= n; i++) 
  {
    // If the freq[i] is equal
    // to i, then increment
    // the count by 1
    if (i == freq[i]) 
    {
      count++;
    }
  }

  // Print the final count
  System.out.print(count + "\n");
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {3, 1, 1, 3, 2, 2, 3};
  int N = arr.length;
  solve(arr, N);
}
}

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program of the
# above approach

# Function to find the integer
# which has a frequency in the
# array equal to its value.
def solve(arr, n):

    # Store frequency of array
    # elements
    freq = [0] * (n + 1);

    for i in range(n):

        # Store the frequency
        # only if arr[i]<=n
        if (arr[i] <= n):
            freq[arr[i]] += 1;

    # Initially the count is zero
    count = 0;

    for i in range(1, n + 1):

        # If the freq[i] is equal
        # to i, then increment
        # the count by 1
        if (i == freq[i]):
            count += 1;

    # Print final count
    print(count , "");

# Driver Code
if __name__ == '__main__':

    arr = [3, 1, 1, 3, 
           2, 2, 3];
    N = len(arr);
    solve(arr, N);

# This code is contributed by shikhasingrajput

```

## C#

```cs

// C# program of the 
// above approach
using System;
class GFG{

// Function to find the integer
// which has a frequency in the
// array equal to its value.
static void solve(int []arr, 
                  int n)
{
  // Store frequency of array
  // elements
  int []freq = new int[n + 1];

  for (int i = 0; i < n; i++) 
  {
    // Store the frequency
    // only if arr[i]<=n
    if (arr[i] <= n)
      freq[arr[i]]++;
  }

  // Initially the count is zero
  int count = 0;

  for (int i = 1; i <= n; i++) 
  {
    // If the freq[i] is equal
    // to i, then increment
    // the count by 1
    if (i == freq[i]) 
    {
      count++;
    }
  }

  // Print the readonly count
  Console.Write(count + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {3, 1, 1, 3, 2, 2, 3};
  int N = arr.Length;
  solve(arr, N);
}
}

// This code is contributed by shikhasingrajput

```

**Output**

```
2

```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*

有关 **O（N * log（N））**方法，请参阅[先前的文章](https://www.geeksforgeeks.org/count-the-elements-having-frequency-equals-to-its-value/)。



* * *

* * *



