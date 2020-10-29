# 检查数组的每个元素是否为另一个数组的任何两个元素的和

> 原文：[https://www.geeksforgeeks.org/check-if-each-element-of-an-array-is-the-sum-of-any-two-elements-of-another-array/](https://www.geeksforgeeks.org/check-if-each-element-of-an-array-is-the-sum-of-any-two-elements-of-another-array/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A []** 和 **B []** ，它们由 **N** 整数组成，任务是检查数组 **B []** 可以通过添加数组 **A []** 的任意两个元素来形成。 如果可能，则打印“ **是”** 。 否则，打印“ **否”** 。

**示例**：

> **输入**：A [] = {3，5，1，4，2}，B [] = {3，4，5，6，7}}
> **输出**：是的
> **说明**：
> B [0] = 3 =（1 + 2）= A [2] + A [4]，
> B [1] = 4 =（1 + 3）= A [2] + A [0]，
> B [2] = 5 =（3 + 2）= A [0] + A [4]，
> B [3] = 6 = （2 + 4）= A [4] + A [3]，
> B [4] = 7 =（3 + 4）= A [0] + A [3]
> **输入**：A [] = {1,2,3,4,5}，B [] = {1,2,3,4,5}
> **输出**：否

**方法**：

请按照以下步骤解决问题：

*   将 **B []** 的每个元素存储在 [Set](https://www.geeksforgeeks.org/set-in-cpp-stl/) 中。

*   对于数组 A []的每对索引**（i，j）**，检查是否存在 **A [i]** + **A [j]** 组。 如果发现是真的，则从**集**中删除 **A [i] + A [j]** 。

*   如果设置为空，则打印“ **是”** 。 否则，打印“ **否”** 。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 
#include  
using namespace std; 

// Function to check if each element 
// of B[] can be formed by adding two 
// elements of array A[] 
string checkPossible(int A[], int B[], int n) 
{ 
    // Store each element of B[] 
    unordered_set values; 

    for (int i = 0; i < n; i++) { 
        values.insert(B[i]); 
    } 

    // Traverse all possible pairs of array 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < n; j++) { 

            // If A[i] + A[j] is present in 
            // the set 
            if (values.find(A[i] + A[j]) 
                != values.end()) { 

                // Remove A[i] + A[j] from the set 
                values.erase(A[i] + A[j]); 

                if (values.empty()) 
                    break; 
            } 
        } 
    } 

    // If set is empty 
    if (values.size() == 0) 
        return "Yes"; 

    // Otherwise 
    else
        return "No"; 
} 

// Driver Code 
int main() 
{ 
    int N = 5; 

    int A[] = { 3, 5, 1, 4, 2 }; 
    int B[] = { 3, 4, 5, 6, 7 }; 

    cout << checkPossible(A, B, N); 
} 

```

## Java

```java

// Java program to implement 
// the above approach 
import java.io.*;
import java.util.*; 

class GFG{

// Function to check if each element 
// of B[] can be formed by adding two 
// elements of array A[] 
static String checkPossible(int A[], int B[],
                            int n) 
{ 

    // Store each element of B[] 
    Set values = new HashSet(); 

    for(int i = 0; i < n; i++) 
    { 
        values.add(B[i]); 
    } 

    // Traverse all possible pairs of array 
    for(int i = 0; i < n; i++) 
    { 
        for(int j = 0; j < n; j++) 
        { 

            // If A[i] + A[j] is present in 
            // the set 
            if (values.contains(A[i] + A[j]))
            { 

                // Remove A[i] + A[j] from the set 
                values.remove(A[i] + A[j]); 

                if (values.size() == 0) 
                    break; 
            } 
        } 
    } 

    // If set is empty 
    if (values.size() == 0) 
        return "Yes"; 

    // Otherwise 
    else
        return "No"; 
} 

// Driver Code 
public static void main(String args[])
{ 
    int N = 5; 
    int A[] = { 3, 5, 1, 4, 2 }; 
    int B[] = { 3, 4, 5, 6, 7 }; 

    System.out.print(checkPossible(A, B, N)); 
} 
} 

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program to implement 
# the above approach 

# Function to check if each element 
# of B[] can be formed by adding two 
# elements of array A[] 
def checkPossible(A, B, n):

    # Store each element of B[] 
    values = set([])

    for i in range (n):
        values.add(B[i])

    # Traverse all possible 
    # pairs of array 
    for i in range (n):
        for j in range (n):

            # If A[i] + A[j] is present in 
            # the set 
            if ((A[i] + A[j]) in values):

                # Remove A[i] + A[j] from the set 
                values.remove(A[i] + A[j])

                if (len(values) == 0):
                    break

    # If set is empty 
    if (len(values) == 0):
        return "Yes"

    # Otherwise 
    else:
        return "No"

# Driver Code 
if __name__ == "__main__":

  N = 5

  A = [3, 5, 1, 4, 2]
  B = [3, 4, 5, 6, 7]

  print (checkPossible(A, B, N))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program to implement 
// the above approach 
using System;
using System.Collections.Generic;
class GFG{

// Function to check if each element 
// of []B can be formed by adding two 
// elements of array []A 
static String checkPossible(int []A, int []B,
                            int n) 
{ 

  // Store each element of []B 
  HashSet values = new HashSet(); 

  for(int i = 0; i < n; i++) 
  { 
    values.Add(B[i]); 
  } 

  // Traverse all possible pairs of array 
  for(int i = 0; i < n; i++) 
  { 
    for(int j = 0; j < n; j++) 
    { 
      // If A[i] + A[j] is present in 
      // the set 
      if (values.Contains(A[i] + A[j]))
      {                 
        // Remove A[i] + A[j] from the set 
        values.Remove(A[i] + A[j]); 

        if (values.Count == 0) 
          break; 
      } 
    } 
  } 

  // If set is empty 
  if (values.Count == 0) 
    return "Yes"; 

  // Otherwise 
  else
    return "No"; 
} 

// Driver Code 
public static void Main(String []args)
{ 
  int N = 5; 
  int []A = {3, 5, 1, 4, 2}; 
  int []B = {3, 4, 5, 6, 7}; 

  Console.Write(checkPossible(A, B, N)); 
} 
} 

// This code is contributed by Amit Katiyar 

```

**Output:** 

```
Yes

```

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：`O(n)`*



* * *

* * *



