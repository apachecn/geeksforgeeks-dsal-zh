# 用元素后的正负数之和的差代替所有元素

> 原文:[https://www . geeksforgeeks . org/将所有元素替换为元素后的正负数之和的差/](https://www.geeksforgeeks.org/replace-all-elements-by-difference-of-sums-of-positive-and-negative-numbers-after-that-element/)

给定一组正负元素。任务是用范围 **i+1 到 N** 内正负元素绝对和的绝对差来替换数组中的每一个**I**元素。即求 *i+1 到 N* 范围内所有正元素的绝对和以及所有负元素的绝对和。现在求这两个和的绝对差，用第 I 个元素代替。

**注意**:更新后数组的最后一个元素将为零。

**示例:**

```
Input : N = 5,  arr[] = {1, -1, 2, 3, -2}
Output : arr[] = {2, 3, 1, 2, 0}

Input : N = 6,  arr[] = {-3, -4, -2, 5, 1, -2}
Output : arr[] = {2, 2, 4, 1, 2, 0}.
```

**天真法:**天真法是对循环和所有第 I 个元素运行两个，计算索引在 i+1 到 n 范围内的所有正负元素之和的 abs 值，现在求两个和的绝对差，用第 I 个元素替换。
这种方法的时间复杂度为 O(N <sup>2</sup> ，其中 N 是数组中的元素数量。

下面是上述方法的实现:

## C++

```
// C++ program to implement above approach

#include <iostream>
using namespace std;

// Function to print the array elements
void printArray(int N, int arr[])
{
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";

    cout << endl;
}

// Function to replace all elements with absolute
// difference of absolute sums of positive
// and negative elements
void replacedArray(int N, int arr[])
{
    int pos_sum, neg_sum, i, j, diff;

    for (i = 0; i < N; i++) {
        pos_sum = 0;
        neg_sum = 0;

        // Calculate absolute sums of positive
        // and negative elements in range i+1 to N
        for (j = i + 1; j < N; j++) {
            if (arr[j] > 0)
                pos_sum += arr[j];
            else
                neg_sum += arr[j];
        }

        // calculate difference of both sums
        diff = abs(pos_sum) - abs(neg_sum);

        // replace i-th elements with absolute
        // difference
        arr[i] = abs(diff);
    }
}

// Driver code
int main()
{
    int N = 5;
    int arr[] = { 1, -1, 2, 3, -2 };
    replacedArray(N, arr);
    printArray(N, arr);

    N = 6;
    int arr1[] = { -3, -4, -2, 5, 1, -2 };
    replacedArray(N, arr1);
    printArray(N, arr1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement above approach
class GFG
{

// Function to print the array elements
static void printArray(int N, int []arr)
{
    for (int i = 0; i < N; i++)
        System.out.print(arr[i] + " ");

    System.out.println();
}

// Function to replace all elements with
// absolute difference of absolute sums
// of positive and negative elements
static void replacedArray(int N, int []arr)
{
    int pos_sum, neg_sum, i, j, diff;

    for (i = 0; i < N; i++)
    {
        pos_sum = 0;
        neg_sum = 0;

        // Calculate absolute sums of positive
        // and negative elements in range i+1 to N
        for (j = i + 1; j < N; j++)
        {
            if (arr[j] > 0)
                pos_sum += arr[j];
            else
                neg_sum += arr[j];
        }

        // calculate difference of both sums
        diff = Math.abs(pos_sum) - Math.abs(neg_sum);

        // replace i-th elements with absolute
        // difference
        arr[i] = Math.abs(diff);
    }
}

// Driver code
public static void main(String args[])
{
    int N = 5;
    int []arr = { 1, -1, 2, 3, -2 };
    replacedArray(N, arr);
    printArray(N, arr);

    N = 6;
    int []arr1 = { -3, -4, -2, 5, 1, -2 };
    replacedArray(N, arr1);
    printArray(N, arr1);
}
}

// This code is contributed by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 program to implement
# above approach

# Function to print the array elements
def printArray(N, arr):
    for i in range(N):
        print(arr[i], end = " ")

    print("\n", end = "")

# Function to replace all elements with
# absolute difference of absolute sums
# of positive and negative elements
def replacedArray(N, arr):
    for i in range(N):
        pos_sum = 0
        neg_sum = 0

        # Calculate absolute sums of positive
        # and negative elements in range i+1 to N
        for j in range(i + 1, N, 1):
            if (arr[j] > 0):
                pos_sum += arr[j]
            else:
                neg_sum += arr[j]

        # calculate difference of both sums
        diff = abs(pos_sum) - abs(neg_sum)

        # replace i-th elements with absolute
        # difference
        arr[i] = abs(diff)

# Driver code
if __name__ == '__main__':
    N = 5
    arr = [1, -1, 2, 3, -2]
    replacedArray(N, arr)
    printArray(N, arr)

    N = 6
    arr1 = [-3, -4, -2, 5, 1, -2]
    replacedArray(N, arr1)
    printArray(N, arr1)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement above approach
using System;

class GFG
{

// Function to print the array elements
static void printArray(int N, int []arr)
{
    for (int i = 0; i < N; i++)
        Console.Write(arr[i] + " ");

    Console.WriteLine();
}

// Function to replace all elements with
// absolute difference of absolute sums
// of positive and negative elements
static void replacedArray(int N, int []arr)
{
    int pos_sum, neg_sum, i, j, diff;

    for (i = 0; i < N; i++)
    {
        pos_sum = 0;
        neg_sum = 0;

        // Calculate absolute sums of positive
        // and negative elements in range i+1 to N
        for (j = i + 1; j < N; j++)
        {
            if (arr[j] > 0)
                pos_sum += arr[j];
            else
                neg_sum += arr[j];
        }

        // calculate difference of both sums
        diff = Math.Abs(pos_sum) - Math.Abs(neg_sum);

        // replace i-th elements with absolute
        // difference
        arr[i] = Math.Abs(diff);
    }
}

// Driver code
static void Main()
{
    int N = 5;
    int []arr = { 1, -1, 2, 3, -2 };
    replacedArray(N, arr);
    printArray(N, arr);

    N = 6;
    int []arr1 = { -3, -4, -2, 5, 1, -2 };
    replacedArray(N, arr1);
    printArray(N, arr1);
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript program to implement above approach   

// Function to print the array elements
function printArray(N, arr)
{
    for(i = 0; i < N; i++)
        document.write(arr[i] + " ");

    document.write("<br/>");
}

// Function to replace all elements with
// absolute difference of absolute sums
// of positive and negative elements
function replacedArray(N, arr)
{
    var pos_sum, neg_sum, i, j, diff;

    for(i = 0; i < N; i++)
    {
        pos_sum = 0;
        neg_sum = 0;

        // Calculate absolute sums of positive
        // and negative elements in range i+1 to N
        for(j = i + 1; j < N; j++)
        {
            if (arr[j] > 0)
                pos_sum += arr[j];
            else
                neg_sum += arr[j];
        }

        // Calculate difference of both sums
        diff = Math.abs(pos_sum) -
               Math.abs(neg_sum);

        // Replace i-th elements with absolute
        // difference
        arr[i] = Math.abs(diff);
    }
}

// Driver code
var N = 5;
var arr = [ 1, -1, 2, 3, -2 ];
replacedArray(N, arr);
printArray(N, arr);

N = 6;
var arr1 = [ -3, -4, -2, 5, 1, -2 ];
replacedArray(N, arr1);
printArray(N, arr1);

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
2 3 1 2 0 
2 2 4 1 2 0
```

**有效方法:**将正负和初始化为 0。现在从最后一个元素到第一个元素运行一个 for 循环，并计算 diff = ABS(pos _ sum)–ABS(neg _ sum)。
现在，如果第 I 个元素是正的，将其添加到 pos_sum，否则将其添加到 neg_sum。毕竟，用绝对差替换第 I 个元素，即 abs(diff)。

下面是上述方法的实现:

## C++

```
// C++ program to implement above approach

#include <iostream>
using namespace std;

// Function to print the array elements
void printArray(int N, int arr[])
{
    for (int i = 0; i < N; i++)
        cout << arr[i] << " ";

    cout << endl;
}

// Function to replace all elements with absolute
// difference of absolute sums of positive
// and negative elements
void replacedArray(int N, int arr[])
{
    int pos_sum, neg_sum, i, j, diff;

    pos_sum = 0;
    neg_sum = 0;

    for (i = N - 1; i >= 0; i--) {

        // calculate difference of both sums
        diff = abs(pos_sum) - abs(neg_sum);

        // if i-th element is positive,
        // add it to positive sum
        if (arr[i] > 0)
            pos_sum += arr[i];

        // if i-th element is negative,
        // add it to negative sum
        else
            neg_sum += arr[i];

        // replace i-th elements with
        // absolute difference
        arr[i] = abs(diff);
    }
}

// Driver Code
int main()
{
    int N = 5;
    int arr[] = { 1, -1, 2, 3, -2 };
    replacedArray(N, arr);
    printArray(N, arr);

    N = 6;
    int arr1[] = { -3, -4, -2, 5, 1, -2 };
    replacedArray(N, arr1);
    printArray(N, arr1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement above approach
class GFG
{

    // Function to print the array elements
    static void printArray(int N, int arr[])
    {
        for (int i = 0; i < N; i++)
            System.out.print(arr[i] + " ");

        System.out.println();
    }

    // Function to replace all elements with absolute
    // difference of absolute sums of positive
    // and negative elements
    static void replacedArray(int N, int arr[])
    {
        int pos_sum, neg_sum, i, j, diff;

        pos_sum = 0;
        neg_sum = 0;

        for (i = N - 1; i >= 0; i--)
        {

            // calculate difference of both sums
            diff = Math.abs(pos_sum) - Math.abs(neg_sum);

            // if i-th element is positive,
            // add it to positive sum
            if (arr[i] > 0)
                pos_sum += arr[i];

            // if i-th element is negative,
            // add it to negative sum
            else
                neg_sum += arr[i];

            // replace i-th elements with
            // absolute difference
            arr[i] = Math.abs(diff);
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        int N = 5;
        int arr[] = { 1, -1, 2, 3, -2 };
        replacedArray(N, arr);
        printArray(N, arr);

        N = 6;
        int arr1[] = { -3, -4, -2, 5, 1, -2 };
        replacedArray(N, arr1);
        printArray(N, arr1);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python program to implement above approach

# Function to print the array elements
def printArray(N, arr) :

    for i in range (0, N) :
        print(arr[i], end=" ")

    print()

# Function to replace all elements with absolute
# difference of absolute sums of positive
# and negative elements
def replacedArray(N, arr) :

    pos_sum = 0
    neg_sum = 0

    for i in range (N - 1,-1, -1) :

        # calculate difference of both sums
        diff = abs(pos_sum) - abs(neg_sum)

        # if i-th element is positive,
        # add it to positive sum
        if (arr[i] > 0) :
            pos_sum = pos_sum + arr[i]

        # if i-th element is negative,
        # add it to negative sum
        else :
            neg_sum = neg_sum + arr[i]

        # replace i-th elements with
        # absolute difference
        arr[i] = abs(diff)

# Driver Code

N = 5
arr = [ 1, -1, 2, 3, -2 ]
replacedArray(N, arr)
printArray(N, arr)

N = 6
arr1 = [ -3, -4, -2, 5, 1, -2 ]
replacedArray(N, arr1)
printArray(N, arr1)

# This code is contributed by ihritik
```

## C#

```
// C# program to implement above approach
using System;

class GFG
{

    // Function to print the array elements
    static void printArray(int N, int [] arr)
    {
        for (int i = 0; i < N; i++)
            Console.Write(arr[i] + " ");

        Console.WriteLine();
    }

    // Function to replace all elements with absolute
    // difference of absolute sums of positive
    // and negative elements
    static void replacedArray(int N, int [] arr)
    {
        int pos_sum, neg_sum, i, diff;

        pos_sum = 0;
        neg_sum = 0;

        for (i = N - 1; i >= 0; i--)
        {

            // calculate difference of both sums
            diff = Math.Abs(pos_sum) - Math.Abs(neg_sum);

            // if i-th element is positive,
            // add it to positive sum
            if (arr[i] > 0)
                pos_sum += arr[i];

            // if i-th element is negative,
            // add it to negative sum
            else
                neg_sum += arr[i];

            // replace i-th elements with
            // absolute difference
            arr[i] = Math.Abs(diff);
        }
    }

    // Driver Code
    public static void Main ()
    {
        int N = 5;
        int [] arr = { 1, -1, 2, 3, -2 };
        replacedArray(N, arr);
        printArray(N, arr);

        N = 6;
        int [] arr1 = { -3, -4, -2, 5, 1, -2 };
        replacedArray(N, arr1);
        printArray(N, arr1);
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Function to print the array elements
function printArray(N,  arr)
{
    for (var i = 0; i < N; i++)
        document.write( arr[i] +" ");

    document.write("<br>");
}

// Function to replace all elements with absolute
// difference of absolute sums of positive
// and negative elements
function replacedArray( N,  arr)
{
    var pos_sum, neg_sum, i, j, diff;

    pos_sum = 0;
    neg_sum = 0;

    for (i = N - 1; i >= 0; i--) {

        // calculate difference of both sums
        diff = Math.abs(pos_sum) - Math.abs(neg_sum);

        // if i-th element is positive,
        // add it to positive sum
        if (arr[i] > 0)
            pos_sum += arr[i];

        // if i-th element is negative,
        // add it to negative sum
        else
            neg_sum += arr[i];

        // replace i-th elements with
        // absolute difference
        arr[i] = Math.abs(diff);
    }
}

// Driver Code
var N = 5;
    var arr = [ 1, -1, 2, 3, -2 ];
    replacedArray(N, arr);
    printArray(N, arr);
    N=6;
var arr1 = [-3, -4, -2, 5, 1, -2 ];
    replacedArray(N, arr1);
    printArray(N, arr1);

</script>
```

**Output:** 

```
2 3 1 2 0 
2 2 4 1 2 0
```

**时间复杂度:** O(N)，其中 N 为元素个数。