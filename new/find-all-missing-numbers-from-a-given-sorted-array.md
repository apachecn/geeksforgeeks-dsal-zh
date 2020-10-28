# 从给定的排序数组

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)

中查找所有缺失的数字

给定 **N** 个整数的排序数组 **arr []** ，任务是在范围 **[arr [0]，arr [N]之间找到数组中的多个缺失元素 -1]]** 。

**示例**：

> ***输入**：arr [] = {6，7，10，11，13}*
> ***输出**：8 9 12*
> **解释**：
> 数组的元素存在于最大和最小数组元素[6，13]的范围内。 因此，总值为{6、7、8、9、10、11、12、13}。
> 数组中缺少上述范围的元素是{8，9，12}。
> 
> ***输入**：arr [] = {1、2、4、6}*
> ***输出**：3 5*

**天真的方法**：天真的想法是遍历连续对元素之间的[差异，并打印该范围内的所有数字（如果差异非零）。 步骤如下：](https://www.geeksforgeeks.org/calculate-the-difference-between-consecutive-pair-of-elements-of-a-vector-in-r-programming-diff-function/)

1.  初始化变量 **diff** ，该变量等于 **arr [0] – 0** 。

2.  现在[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，看看 **arr [i] – i** 与 **diff** 之间的差是否为零。

3.  如果上述步骤中的差不等于零，则找到丢失的元素。

4.  要查找多个丢失的元素，请在其中运行一个循环，然后查看 **diff** 是否小于 **arr [i] – i** ，然后打印缺少的元素，即 **i + diff** 。

5.  现在，随着差值的增加，增加 **diff** 。

6.  从步骤 2 重复，直到找不到所有缺少的数字。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the missing elements 
void printMissingElements(int arr[], int N) 
{ 

    // Initialize diff 
    int diff = arr[0] - 0; 

    for (int i = 0; i < N; i++) { 

        // Check if diff and arr[i]-i 
        // both are equal or not 
        if (arr[i] - i != diff) { 

            // Loop for consecutive 
            // missing elements 
            while (diff < arr[i] - i) { 
                cout << i + diff << " "; 
                diff++; 
            } 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    // Given array arr[] 
    int arr[] = { 6, 7, 10, 11, 13 }; 

    int N = sizeof(arr) / sizeof(int); 

    // Function Call 
    printMissingElements(arr, N); 
    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG{ 

// Function to find the missing elements 
static void printMissingElements(int arr[], 
                                 int N) 
{ 

    // Initialize diff 
    int diff = arr[0] - 0; 

    for(int i = 0; i < N; i++) 
    { 

        // Check if diff and arr[i]-i 
        // both are equal or not 
        if (arr[i] - i != diff) 
        { 

            // Loop for consecutive 
            // missing elements 
            while (diff < arr[i] - i) 
            { 
                System.out.print((i + diff) + " "); 
                diff++; 
            } 
        } 
    } 
} 

// Driver Code 
public static void main (String[] args) 
{ 

    // Given array arr[] 
    int arr[] = { 6, 7, 10, 11, 13 }; 

    int N = arr.length; 

    // Function call 
    printMissingElements(arr, N); 
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program for the above approach 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)

# Function to find the missing elements 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)
def printMissingElements(arr, N): 

    # Initialize diff 
    diff = arr[0] 

    for i in range(N): 

        # Check if diff and arr[i]-i 
        # both are equal or not 
        if(arr[i] - i != diff): 

            # Loop for consecutive 
            # missing elements 
            while(diff < arr[i] - i): 
                print(i + diff, end = " ") 
                diff += 1

# Driver Code 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)

# Given array arr[] 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)
arr = [ 6, 7, 10, 11, 13 ] 

N = len(arr) 

# Function call 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)
printMissingElements(arr, N) 

# This code is contributed by Shivam Singh 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)

```

## C#

```cs

// C# program for the above approach
using System;

class GFG{

// Function to find the missing elements 
static void printMissingElements(int[] arr, 
                                 int N) 
{ 

    // Initialize diff 
    int diff = arr[0] - 0; 

    for(int i = 0; i < N; i++)
    { 

        // Check if diff and arr[i]-i 
        // both are equal or not 
        if (arr[i] - i != diff) 
        { 

            // Loop for consecutive 
            // missing elements 
            while (diff < arr[i] - i) 
            { 
                Console.Write(i + diff + " ");
                diff++; 
            } 
        } 
    } 
} 

// Driver code
static void Main()
{

    // Given array arr[] 
    int[] arr = { 6, 7, 10, 11, 13 }; 

    int N = arr.Length; 

    // Function call 
    printMissingElements(arr, N);
}
}

// This code is contributed by divyeshrabadiya07

```

**Output:** 

```
8 9 12

```

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（1）*

**高效方法**：的想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)优化上述方法。 创建一个布尔数组（例如 **b []** ），其大小等于数组中的最大元素，并仅标记数组 b []中存在于给定数组中的那些位置。 打印数组 **b []** 中所有未标记的索引。

以下是步骤：

1.  初始化一个布尔数组 **b []** ，其大小为零，等于数组的[最大元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

2.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并为给定数组中的每个元素标记，将索引在数组 **b []** 中设为 true。

3.  现在从索引 **arr [0]** 中遍历给定数组 **b []** 并打印那些值为假的索引，因为它们是给定数组中缺少的元素。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the missing elements 
void printMissingElements(int arr[], int N) 
{ 
    // Initialize an array with zero 
    // of size equals to the maximum 
    // element in the array 
    int b[arr[N - 1] + 1] = { 0 }; 

    // Make b[i]=1 if i is present 
    // in the array 
    for (int i = 0; i < N; i++) { 

        // If the element is present 
        // make b[arr[i]]=1 
        b[arr[i]] = 1; 
    } 

    // Print the indices where b[i]=0 
    for (int i = arr[0]; i <= arr[N - 1]; i++) { 

        if (b[i] == 0) { 
            cout << i << " "; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    // Given array arr[] 
    int arr[] = { 6, 7, 10, 11, 13 }; 

    int N = sizeof(arr) / sizeof(int); 

    // Function Call 
    printMissingElements(arr, N); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG{ 

// Function to find the missing elements 
static void printMissingElements(int arr[], 
                                int N) 
{ 

    // Initialize an array with zero 
    // of size equals to the maximum 
    // element in the array 
    int[] b = new int[arr[N - 1] + 1]; 

    // Make b[i]=1 if i is present 
    // in the array 
    for(int i = 0; i < N; i++) 
    { 

        // If the element is present 
        // make b[arr[i]]=1 
        b[arr[i]] = 1; 
    } 

    // Print the indices where b[i]=0 
    for(int i = arr[0]; i <= arr[N - 1]; i++) 
    { 
        if (b[i] == 0) 
        { 
            System.out.print(i + " "); 
        } 
    } 
} 

// Driver Code 
public static void main (String[] args) 
{ 

    // Given array arr[] 
    int arr[] = { 6, 7, 10, 11, 13 }; 

    int N = arr.length; 

    // Function call 
    printMissingElements(arr, N); 
} 
} 

// This code is contributed by offbeat 

```

## Python3

```py

# Python3 program to implement 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)
# the above approach 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)

# Function to find the missing elements 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)
def printMissingElements(arr, N): 

    # Initialize an array with zero 
    # of size equals to the maximum 
    # element in the array 
    b = [0] * (arr[N - 1] + 1) 

    # Make b[i]=1 if i is present 
    # in the array 
    for i in range(N): 

        # If the element is present 
        # make b[arr[i]]=1 
        b[arr[i]] = 1

    # Print the indices where b[i]=0 
    for i in range(arr[0], arr[N - 1] + 1): 
        if(b[i] == 0): 
            print(i, end = " ") 

# Driver Code 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)

# Given array arr[] 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)
arr = [ 6, 7, 10, 11, 13 ] 

N = len(arr) 

# Function call 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)
printMissingElements(arr, N) 

# This code is contributed by Shivam Singh 

> 原文：[https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/](https://www.geeksforgeeks.org/find-all-missing-numbers-from-a-given-sorted-array/)

```

## C#

```cs

// C# program for 
// the above approach 
using System;
class GFG{ 

// Function to find the missing elements 
static void printMissingElements(int []arr, 
                                 int N) 
{     
  // Initialize an array with zero 
  // of size equals to the maximum 
  // element in the array 
  int[] b = new int[arr[N - 1] + 1]; 

  // Make b[i]=1 if i is present 
  // in the array 
  for(int i = 0; i < N; i++) 
  { 
    // If the element is present 
    // make b[arr[i]]=1 
    b[arr[i]] = 1; 
  } 

  // Print the indices where b[i]=0 
  for(int i = arr[0]; i <= arr[N - 1]; 
          i++) 
  { 
    if (b[i] == 0) 
    { 
      Console.Write(i + " "); 
    } 
  } 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
  // Given array []arr 
  int []arr = {6, 7, 10, 11, 13}; 

  int N = arr.Length; 

  // Function call 
  printMissingElements(arr, N); 
} 
} 

// This code is contributed by Princi Singh

```

**Output:** 

```
8 9 12

```

***时间复杂度**：O（M），其中 M 是数组的最大元素。*

***辅助空间**：O（M）*



* * *

* * *



