# 检查数组是否仅包含一个不同的元素

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr []** ，任务是检查该数组是否仅包含一个不同的元素。 如果仅包含一个不同的元素，则打印“ **是”** ，否则打印“ **否”** 。

**示例**：

> **输入**：arr [] = {3、3、4、3、3}
> **输出**：否
> **说明**：数组{3，4}中存在 2 个不同的元素。
> 因此，输出为 No。
> 
> **输入**：arr [] = {9，9，9，9，9，9，9}
> **输出**：是
> **说明**：
> 数组中唯一不同的元素是 9。
> 因此，输出为 Yes。

**天真的方法**：的想法是[对给定的数组进行](https://www.geeksforgeeks.org/sort-c-stl/)排序，然后针对每个有效索引检查当前元素和下一个元素是否相同。 如果它们不相同，则表示该数组包含多个不同的元素，因此打印“ **否”** ，否则打印“ **是”** 。

***时间复杂度**：O（N * logN）*

***辅助空间**：O（1）*

**更好的方法**：可以通过使用[集](https://www.geeksforgeeks.org/set-in-java/) [数据结构](https://www.geeksforgeeks.org/data-structures/)解决此问题。 自设置以来，不允许重复。 步骤如下：

1.  将数组的元素插入集合。

2.  如果只有一个不同的元素，则步骤 1 之后的集合的大小将为 1，因此打印**为“是”** 。

3.  否则，打印“ **No”** 。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h> 
using namespace std; 

// Function to find if the array 
// contains only one distinct element 
void uniqueElement(int arr[],int n)
{

    // Create a set
    unordered_set<int> set;

    // Traversing the array
    for(int i = 0; i < n; i++)
    {
        set.insert(arr[i]);
    }

    // Compare and print the result
    if(set.size() == 1)
    {
        cout << "YES" << endl;
    }
    else
    {
        cout << "NO" << endl;
    }
} 

// Driver code
int main()
{
    int arr[] = { 9, 9, 9, 9, 9, 9, 9 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    uniqueElement(arr,n);
    return 0;
} 

// This code is contributed by rutvik_56

```

## Java

```java

// Java program for the above approach
import java.util.*;

public class Main {

    // Function to find if the array
    // contains only one distinct element
    public static void
    uniqueElement(int arr[])
    {
        // Create a set
        Set<Integer> set = new HashSet<>();

        // Traversing the array
        for (int i = 0; i < arr.length; i++) {
            set.add(arr[i]);
        }

        // Compare and print the result
        if (set.size() == 1)
            System.out.println("Yes");

        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 9, 9, 9, 9, 9, 9, 9 };

        // Function call
        uniqueElement(arr);
    }
}

```

## Python3

```py

# Python3 program for the above approach

# Function to find if the array 
# contains only one distinct element 
def uniqueElement(arr, n):

    # Create a set
    s = set(arr)

    # Compare and print the result
    if(len(s) == 1):
        print('YES')
    else:
        print('NO')

# Driver code
if __name__=='__main__':

    arr = [ 9, 9, 9, 9, 9, 9, 9 ]
    n = len(arr)

    # Function call
    uniqueElement(arr, n)

# This code is contributed by rutvik_56

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find if the array
// contains only one distinct element
public static void uniqueElement(int []arr)
{

    // Create a set
    HashSet<int> set = new HashSet<int>();

    // Traversing the array
    for(int i = 0; i < arr.Length; i++) 
    {
        set.Add(arr[i]);
    }

    // Compare and print the result
    if (set.Count == 1)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 9, 9, 9, 9, 9, 9, 9 };

    // Function call
    uniqueElement(arr);
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
Yes

```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*

**高效方法**：也可以在不使用任何额外空间的情况下解决此问题。 步骤如下：

1.  假定数组的第一个元素是数组中唯一的[唯一元素，并将其值存储在变量中，例如 **X** 。](https://www.geeksforgeeks.org/count-distinct-elements-in-an-array/)

2.  然后遍历数组，并检查当前元素是否等于 **X** 。

3.  如果发现为真，则继续检查所有数组元素。 如果没有发现元素与 **X** 不同，则打印“是”。

4.  否则，如果任何数组元素不等于 **X** ，则意味着该数组包含多个唯一元素。 因此，打印**为“否”** 。

下面是上述方法的实现：

## C++

```cpp

// C++ program for 
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find if the array
// contains only one distinct element
void uniqueElement(int arr[], int n)
{
  // Assume first element to
  // be the unique element
  int x = arr[0];

  int flag = 1;

  // Traversing the array
  for (int i = 0; i < n; i++) 
  { 
    // If current element is not
    // equal to X then break the
    // loop and print No
    if (arr[i] != x) 
    {
      flag = 0;
      break;
    }
  }

  // Compare and print the result
  if (flag == 1)
    cout << "Yes";
  else
    cout << "No";
}

// Driver Code
int main()
{
  int arr[] = {9, 9, 9, 
               9, 9, 9, 9};
  int n = sizeof(arr) / 
          sizeof(arr[0]);

  // Function call
  uniqueElement(arr, n);
}

// This code is contributed by Chitranayal

```

## Java

```java

// Java program for the above approach

import java.util.*;

public class Main {

    // Function to find if the array
    // contains only one distinct element
    public static void
    uniqueElement(int arr[])
    {
        // Assume first element to
        // be the unique element
        int x = arr[0];

        int flag = 1;

        // Traversing the array
        for (int i = 0; i < arr.length; i++) {

            // If current element is not
            // equal to X then break the
            // loop and print No
            if (arr[i] != x) {
                flag = 0;
                break;
            }
        }

        // Compare and print the result
        if (flag == 1)
            System.out.println("Yes");

        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 9, 9, 9, 9, 9, 9, 9 };

        // Function call
        uniqueElement(arr);
    }
}

```

## Python3

```py

# Python3 program for the above approach 

# Function to find if the array 
# contains only one distinct element
def uniqueElement(arr):

    # Assume first element to
    # be the unique element
    x = arr[0]

    flag = 1

    # Traversing the array
    for i in range(len(arr)):

        # If current element is not
        # equal to X then break the
        # loop and print No
        if(arr[i] != x):
            flag = 0
            break

    # Compare and print the result
    if(flag == 1):
        print("Yes")
    else:
        print("No")

# Driver Code

# Given array arr[]
arr = [ 9, 9, 9, 9, 9, 9, 9 ]

# Function call
uniqueElement(arr)

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# program for the above approach 
using System;

class GFG{

// Function to find if the array
// contains only one distinct element
public static void uniqueElement(int []arr)
{

    // Assume first element to
    // be the unique element
    int x = arr[0];

    int flag = 1;

    // Traversing the array
    for(int i = 0; i < arr.Length; i++)
    {

        // If current element is not
        // equal to X then break the
        // loop and print No
        if (arr[i] != x)
        {
            flag = 0;
            break;
        }
    }

    // Compare and print the result
    if (flag == 1)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
static public void Main ()
{
    int []arr = { 9, 9, 9, 9, 9, 9, 9 };

    // Function call
    uniqueElement(arr);
}
}

// This code is contributed by AnkitRai01

```

**Output:** 

```
Yes

```

***时间复杂度**：O（N）*

***辅助空间**：O（1）*



* * *

* * *



