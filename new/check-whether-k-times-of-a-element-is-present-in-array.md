# 检查数组

中是否存在元素的 K 次

给定数组 **arr []** 和整数 **K** ，任务是检查数组中是否还存在 K 次任何元素。

**范例**：

> **输入**：arr [] = {10，14，8，13，5}，K = 2
> **输出**：是
> **说明**：
> K 的 5 倍也出现在数组中，即 10。
> **输入**：arr [] = {7，8，5，9，11}，K = 3
> **输出**：否
> **说明**：
> 数组中不存在任何元素的 K 次

**天真的方法**：一个简单的解决方案是运行两个嵌套的[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，并检查每个元素在数组中是否也存在该元素的 K 倍。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation to check whether
// K times of a element is present in 
// the array

#include <bits/stdc++.h>

using namespace std;

// Function to find if K times of
// an element exists in array
void checkKTimesElement(int arr[], int n, int k)
{
    bool found = false;

    // Loop to check that K times of 
    // element is present in the array
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (arr[j] == k * arr[i]) {
                found = true;
                break;
            }
        }
    }

    if (found)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver code
int main()
{
    int arr[] = { 10, 14, 8, 13, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    // Function Call
    checkKTimesElement(arr, n, k);
    return 0;
}

```

## Java

```java

// Java implementation to check whether
// K times of a element is present in 
// the array

class GFG{

// Function to find if K times of
// an element exists in array
static void checkKTimesElement(int arr[], 
                               int n, 
                               int k)
{
    boolean found = false;

    // Loop to check that K times of 
    // element is present in the array
    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j < n; j++) 
       {
          if (arr[j] == k * arr[i])
          {
              found = true;
              break;
          }
       }
    }

    if (found)
        System.out.print("Yes" + "\n");
    else
        System.out.print("No" + "\n");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 10, 14, 8, 13, 5 };
    int n = arr.length;
    int k = 2;

    // Function call
    checkKTimesElement(arr, n, k);
}
}

// This code is contributed by sapnasingh4991

```

## Python3

```py

# Python3 implementation to check whether
# K times of a element is present in 
# the array

# Function to find if K times of
# an element exists in array
def checkKTimesElement(arr, n, k):

    found = False

    # Loop to check that K times of 
    # element is present in the array
    for i in range(0, n):
        for j in range(0, n):

            if arr[j] == k * arr[i]:
                found = True
                break
    if found:
        print('Yes')
    else:
        print('No')

# Driver code 
if __name__=='__main__':

    arr = [ 10, 14, 8, 13, 5 ]
    n = len(arr)
    k = 2

    # Function Call
    checkKTimesElement(arr, n, k)

# This code is contributed by rutvik_56

```

## C#

```cs

// C# implementation to check whether
// K times of a element is present in 
// the array
using System;

class GFG{

// Function to find if K times of
// an element exists in array
static void checkKTimesElement(int []arr, 
                               int n, 
                               int k)
{
    bool found = false;

    // Loop to check that K times of 
    // element is present in the array
    for(int i = 0; i < n; i++)
    {
       for(int j = 0; j < n; j++)
       {
          if (arr[j] == k * arr[i])
          {
              found = true;
              break;
          }
       }
    }
    if (found)
        Console.Write("Yes" + "\n");
    else
        Console.Write("No" + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 10, 14, 8, 13, 5 };
    int n = arr.Length;
    int k = 2;

    // Function call
    checkKTimesElement(arr, n, k);
}
}

// This code is contributed by amal kumar choubey

```

**Output:** 

```
Yes

```

**高效方法**：的想法是将所有元素存储在[哈希图中](https://www.geeksforgeeks.org/hashing-data-structure/)，并针对每个元素检查该哈希图中是否存在该元素的 K 次。 如果它存在于哈希图中，则返回 True，否则返回 False。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation to check whether
// K times of a element is present in 
// the array

#include <bits/stdc++.h>

using namespace std;

// Function to check if K times of
// an element exists in array
bool checkKTimesElement(int arr[], int n, int k)
{
    // Create an empty set
    unordered_set<int> s;
    for (int i = 0; i < n; i++){
        s.insert(arr[i]);
    }

    for (int i = 0; i < n; i++) {

        // Check if K times of 
        // element exists in set
        if (s.find(arr[i] * k) != s.end())
            return true;
    }

    return false;
}

// Driven code
int main()
{
    int arr[] = { 5, 14, 8, 13, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    if (checkKTimesElement(arr, n, k))
        cout << "Yes\n";
    else
        cout << "No\n";
    return 0;
}

```

## Java

```java

// Java implementation to check whether
// K times of a element is present in 
// the array
import java.util.*;

class GFG{

// Function to check if K times of
// an element exists in array
static boolean checkKTimesElement(int arr[], int n,
                                             int k)
{

    // Create an empty set
    HashSet<Integer> s = new HashSet<Integer>();

    for(int i = 0; i < n; i++)
    {
       s.add(arr[i]);
    }

    for(int i = 0; i < n; i++)
    {

       // Check if K times of 
       // element exists in set
       if (s.contains(arr[i] * k))
           return true;
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 14, 8, 13, 10 };
    int n = arr.length;
    int k = 2;

    if (checkKTimesElement(arr, n, k))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by amal kumar choubey

```

## Python3

```py

# Python3 implementation to 
# check whether K times of  
# a element is present in the array

# Function to check if K times of
# an element exists in array
def checkKTimesElement(arr, n, k):

  # Create an empty set
  s = set([])
  for i in range (n):
    s.add(arr[i])
  for i in range (n):

    # Check if K times of 
    # element exists in set
    if ((arr[i] * k) in s):
      return True
    return False

# Driver code
if __name__ == "__main__":

  arr = [5, 14, 8, 13, 10]
  n = len(arr)
  k = 2

  if (checkKTimesElement(arr, n, k)):
    print ("Yes")
  else:
    print("No")

# This code is contributed by Chitranayal

```

## C#

```cs

// C# implementation to check whether
// K times of a element is present in 
// the array
using System;
using System.Collections.Generic;

class GFG{

// Function to check if K times of
// an element exists in array
static bool checkKTimesElement(int[] arr, int n,
                                          int k)
{

    // Create an empty set
    HashSet<int> s = new HashSet<int>();

    for(int i = 0; i < n; i++)
    {
       s.Add(arr[i]);
    }

    for(int i = 0; i < n; i++)
    {

       // Check if K times of 
       // element exists in set
       if (s.Contains(arr[i] * k))
           return true;
    }
    return false;
}

// Driver code
static public void Main ()
{
    int[] arr = { 5, 14, 8, 13, 10 };
    int n = arr.Length;
    int k = 2;

    if (checkKTimesElement(arr, n, k))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by ShubhamCoder

```

**Output:** 

```
Yes

```

**时间复杂度**：O（n）



* * *

* * *



