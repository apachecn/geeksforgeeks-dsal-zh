# 生成数组，其每个元素与其左边元素的差产生给定的数组

> 原文:[https://www . geeksforgeeks . org/generate-array-每个元素与其左元素的差产生给定的数组/](https://www.geeksforgeeks.org/generate-array-whose-difference-of-each-element-with-its-left-yields-the-given-array/)

给定一个整数 **N** 和一个(N–1)整数的 **arr1[]** ，任务是在范围**【1，N】**中找到 N 个整数的序列 **arr2[]** ，使得**arr 1[I]= arr 2[I+1]–arr 2[I]**。arr1[]中的整数位于 **[-N，N]** 范围内。
**示例:**

> **输入:** N = 3，arr 1[]=
> **输出:**arr 2[]=【T3，1，2】**解释:**
> 【arr 2[1]–arr 2[0]=(1–3)】 5)
> **解释:**
> arr 2[1]–arr 2[0]=(2–1)= 1 = arr 1[0]【t20]【arr 2]–arr 2[2]–arr 2[1]=(3–2)= 1 = arr 1[1]【t21]【arr 2[3]–arr 2[2]=(4–3)= 1 = arr 1

**进场:**
按照步骤解决问题:

1.  假设 **arr2[]** 的第一个元素为 **X** 。
2.  下一个元素将是 **X + arr1[0]** 。
3.  **arr2[]** 的其余元素可以表示，w.r.t **X** 。
4.  已知序列 **arr2[]** 可以包含范围**【1，N】**内的整数。所以最小可能的整数是 **1** 。
5.  **arr 2【】**的最小个数可以用 **X** 来求，将其与 **1** 等同起来求 **X** 的值。
6.  最后利用 **X** 的值，可以找出**arr 2【】**中的所有其他数字。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sequence
void find_seq(int arr[],
              int m, int n) {
    int b[n];
    int x = 0;

    // initializing 1st element
    b[0] = x;

    // Creating sequence in
    // terms of x
    for (int i = 0;
         i < n - 1; i++) {

        b[i + 1] = x +
                   arr[i] + b[i];
    }

    int mn = n;

    // Finding min element
    for (int i = 0; i < n; i++)
    {
        mn = min(mn, b[i]);
    }

    // Finding value of x
    x = 1 - mn;

    // Creating original sequence
    for (int i = 0; i < n; i++) {
        b[i] += x;
    }

    // Output original sequence
    for (int i = 0; i < n; i++) {
        cout << b[i] << " ";
    }
    cout << endl;
}

// Driver function
int main()
{
    int N = 3;
    int arr[] = { -2, 1 };

    int M = sizeof(arr) / sizeof(int);
    find_seq(arr, M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find the sequence
static void find_seq(int arr[], int m,
                                int n)
{
    int b[] = new int[n];
    int x = 0;

    // Initializing 1st element
    b[0] = x;

    // Creating sequence in
    // terms of x
    for(int i = 0; i < n - 1; i++)
    {
       b[i + 1] = x + arr[i] + b[i];
    }

    int mn = n;

    // Finding min element
    for(int i = 0; i < n; i++)
    {
       mn = Math.min(mn, b[i]);
    }

    // Finding value of x
    x = 1 - mn;

    // Creating original sequence
    for(int i = 0; i < n; i++)
    {
       b[i] += x;
    }

    // Output original sequence
    for(int i = 0; i < n; i++)
    {
        System.out.print(b[i] + " ");
    }
    System.out.println();
}

// Driver code
public static void main (String[] args)
{
    int N = 3;
    int arr[] = new int[]{ -2, 1 };
    int M = arr.length;

    find_seq(arr, M, N);
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sequence
def find_seq(arr, m, n):

    b = []
    x = 0

    # Initializing 1st element
    b.append(x)

    # Creating sequence in
    # terms of x
    for i in range(n - 1):
        b.append(x + arr[i] + b[i])

    mn = n

    # Finding min element
    for i in range(n):
        mn = min(mn, b[i])

    # Finding value of x
    x = 1 - mn

    # Creating original sequence
    for i in range(n):
        b[i] += x

    # Output original sequence
    for i in range(n):
        print(b[i], end = ' ')

    print()

# Driver code
if __name__=='__main__':

    N = 3
    arr = [ -2, 1 ]
    M = len(arr)

    find_seq(arr, M, N)

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find the sequence
static void find_seq(int []arr, int m,
                                int n)
{
    int []b = new int[n];
    int x = 0;

    // Initializing 1st element
    b[0] = x;

    // Creating sequence in
    // terms of x
    for(int i = 0; i < n - 1; i++)
    {
       b[i + 1] = x + arr[i] + b[i];
    }

    int mn = n;

    // Finding min element
    for(int i = 0; i < n; i++)
    {
       mn = Math.Min(mn, b[i]);
    }

    // Finding value of x
    x = 1 - mn;

    // Creating original sequence
    for(int i = 0; i < n; i++)
    {
       b[i] += x;
    }

    // Output original sequence
    for(int i = 0; i < n; i++)
    {
       Console.Write(b[i] + " ");
    }
    Console.WriteLine();
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    int []arr = new int[]{ -2, 1 };
    int M = arr.Length;

    find_seq(arr, M, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the sequence
function find_seq(arr,m, n) {
    let b = new Array(n);
    let x = 0;

    // initializing 1st element
    b[0] = x;

    // Creating sequence in
    // terms of x
    for (let i = 0;
         i < n - 1; i++) {

        b[i + 1] = x +
                   arr[i] + b[i];
    }

    let mn = n;

    // Finding min element
    for (let i = 0; i < n; i++)
    {
        mn = Math.min(mn, b[i]);
    }

    // Finding value of x
    x = 1 - mn;

    // Creating original sequence
    for (let i = 0; i < n; i++) {
        b[i] += x;
    }

    // Output original sequence
    for (let i = 0; i < n; i++) {
        document.write(b[i] + " ");
    }
    document.write("<br>");
}

// Driver function

    let N = 3;
    let arr = [ -2, 1 ];

    let M = arr.length;
    find_seq(arr, M, N);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
3 1 2
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*