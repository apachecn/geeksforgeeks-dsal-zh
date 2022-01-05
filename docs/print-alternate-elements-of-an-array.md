# 打印阵列的替代元素

> 原文:[https://www . geesforgeks . org/print-alternate-elements of-a-array/](https://www.geeksforgeeks.org/print-alternate-elements-of-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，任务是打印给定数组中出现在奇数索引处的元素(基于 *1 的索引*)。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 1 3 5
> **解释:**
> 出现在奇数位置的数组元素为:{1，3，5}。
> 因此，需要的输出是 1 3 5。
> 
> **输入:** arr[] = {-5，1，4，2，12 }
> T3】输出: -5 4 12

**天真法:**解决这个问题最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查当前元素的位置是否为奇数。如果发现为真，则打印当前元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print
// Alternate elements
// of the given array
void printAlter(int arr[], int N)
{
    // Print elements
    // at odd positions
    for (int currIndex = 0;
         currIndex < N; currIndex++) {

        // If currIndex stores even index
        // or odd position
        if (currIndex % 2 == 0) {
            cout << arr[currIndex] << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    printAlter(arr, N);
}
```

## C

```
// C program to implement
// the above approach

#include <stdio.h>

// Function to print
// Alternate elements
// of the given array
void printAlter(int arr[], int N)
{
    // Print elements
    // at odd positions
    for (int currIndex = 0;
         currIndex < N; currIndex++) {

        // If currIndex stores even index
        // or odd position
        if (currIndex % 2 == 0) {
            printf("%d ", arr[currIndex]);
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    printAlter(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to print
// Alternate elements
// of the given array
static void printAlter(int[] arr, int N)
{

    // Print elements
    // at odd positions
    for(int currIndex = 0;
            currIndex < N;
            currIndex++)
    {

        // If currIndex stores even index
        // or odd position
        if (currIndex % 2 == 0)
        {
            System.out.print(arr[currIndex] + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    printAlter(arr, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print
# Alternate elements
# of the given array
def printAlter(arr, N):

    # Print elements
    # at odd positions
    for currIndex in range(0, N):

        # If currIndex stores even index
        # or odd position
        if (currIndex % 2 == 0):
            print(arr[currIndex], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5 ]
    N = len(arr)

    printAlter(arr, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print
// Alternate elements
// of the given array
static void printAlter(int[] arr, int N)
{

    // Print elements
    // at odd positions
    for(int currIndex = 0;
            currIndex < N;
            currIndex++)
    {

        // If currIndex stores even index
        // or odd position
        if (currIndex % 2 == 0)
        {
            Console.Write(arr[currIndex] + " ");
        }
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    printAlter(arr, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
// javascript program to implement
// the above approach

// Function to print
// Alternate elements
// of the given array
function printAlter(arr, N)
{

    // Print elements
    // at odd positions
    for(var currIndex = 0; currIndex < N; currIndex++)
    {

        // If currIndex stores even index
        // or odd position
        if (currIndex % 2 == 0)
        {
            document.write(arr[currIndex] + " ");
        }
    }
}

// Driver Code

    var arr = [ 1, 2, 3, 4, 5 ]
    var N = arr.length;

    printAlter(arr, N);

 // This code is contributed by bunnyram19.
```

**Output:** 

```
1 3 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**为了优化上述方法，其思想是只遍历给定数组中出现在奇数位置的那些元素。按照以下步骤解决问题:

*   用循环变量**迭代一个从 **0** 到 **N** 的循环。**
*   打印**arr【currIndex】**的值，并将 **currIndex** 的值增加 **2** 直到 **currIndex** 超过 n

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print
// Alternate elements
// of the given array
void printAlter(int arr[], int N)
{
    // Print elements
    // at odd positions
    for (int currIndex = 0;
         currIndex < N; currIndex += 2) {

        // Print elements of array
        cout << arr[currIndex] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    printAlter(arr, N);
}
```

## C

```
// C program to implement
// the above approach

#include <stdio.h>

// Function to print
// Alternate elements
// of the given array
void printAlter(int arr[], int N)
{
    // Print elements
    // at odd positions
    for (int currIndex = 0;
         currIndex < N; currIndex += 2) {

        // Print elements of array
        printf("%d ", arr[currIndex]);
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    printAlter(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to print
// Alternate elements
// of the given array
static void printAlter(int[] arr, int N)
{

    // Print elements
    // at odd positions
    for(int currIndex = 0;
            currIndex < N;
            currIndex += 2)
    {

        // Print elements of array
        System.out.print(arr[currIndex] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    printAlter(arr, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print
# Alternate elements
# of the given array
def printAlter(arr, N):

    # Print elements
    # at odd positions
    for currIndex in range(0, N, 2):

        # Print elements of array
        print(arr[currIndex], end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5 ]
    N = len(arr)

    printAlter(arr, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print
// Alternate elements
// of the given array
static void printAlter(int[] arr, int N)
{

    // Print elements
    // at odd positions
    for(int currIndex = 0;
            currIndex < N;
            currIndex += 2)
    {

        // Print elements of array
        Console.Write(arr[currIndex] + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    printAlter(arr, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Function to print
// Alternate elements
// of the given array
function printAlter(arr, N)
{
    // Print elements
    // at odd positions
    for (var currIndex = 0;
        currIndex < N; currIndex += 2)
        {

        // Print elements of array
        document.write( arr[currIndex] + " ");
    }
}

var arr= [ 1, 2, 3, 4, 5 ];
    var N = 5;
    printAlter(arr, N);

</script>
```

**Output:** 

```
1 3 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

#### 方法 3:在 Python 中使用切片:

通过设置步长值为 2，使用 [**python 列表切片**](https://www.geeksforgeeks.org/python-list-slicing/) 进行切片。

下面是实现:

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print
# Alternate elements
# of the given array
def printAlter(arr, N):

    # Print elements
    # at odd positions by using slicing
    # we use * to print with spaces
    print(*arr[::2])

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4, 5]
    N = len(arr)

    printAlter(arr, N)

# This code is contributed by vikkycirus
```

#### 输出:

```
1 3 5
```

**时间复杂度:** O(N)

**空间复杂度:** O(1)