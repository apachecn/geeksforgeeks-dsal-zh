# 在圆形数组中找到下一个更大的元素

> 原文:[https://www . geesforgeks . org/find-下一个更大的圆形数组元素/](https://www.geeksforgeeks.org/find-the-next-greater-element-in-a-circular-array/)

给定一个圆形的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]****N**整数，使得给定数组的最后一个元素与该数组的第一个元素相邻，任务是打印该圆形数组中的[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。不存在更大元素的元素，考虑下一个更大的元素为**-1”**。

**示例:**

> **输入:** arr[] = {5，6，7}
> **输出:** {6，7，-1}
> **解释:**
> 5 的下一个更大的元素是 6，6 的是 7，7 的是-1，因为我们没有任何元素大于它本身，所以它的-1。
> 
> **输入:** arr[] = {4，-2，5，8}
> **输出:** {5，5，8，-1}
> **解释:**
> 下一个更大的元素为 4 是 5，为-2 它的 5，为 5 它的 5 是 8，为 8 它是-1 因为我们没有任何元素大于它本身所以它的-1，为 3 它的 4。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

*   为了使循环数组的属性有效，再次将给定的数组元素追加到同一个数组中。

**例如:**

> 让 arr[] = {1，4，3}
> 在追加了相同的元素集之后，arr[]变成了
> arr[] = {1，4，3，1，4，3}

*   找到下一个更大的元素，直到形成上述数组中的 **N** 个元素。
*   如果找到更大的元素，则打印该元素，否则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the NGE
void printNGE(int A[], int n)
{

    // Formation of circular array
    int arr[2 * n];

    // Append the given array element twice
    for (int i = 0; i < 2 * n; i++)
        arr[i] = A[i % n];

    int next, i, j;

    // Iterate for all the
    // elements of the array
    for (i = 0; i < n; i++) {

        // Initialise NGE as -1
        next = -1;

        for (j = i + 1; j < 2 * n; j++) {

            // Checking for next
            // greater element
            if (arr[i] < arr[j]) {
                next = arr[j];
                break;
            }
        }

        // Print the updated NGE
        cout << next << ", ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    printNGE(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the NGE
static void printNGE(int []A, int n)
{

    // Formation of circular array
    int []arr = new int[2 * n];

    // Append the given array element twice
    for(int i = 0; i < 2 * n; i++)
        arr[i] = A[i % n];

    int next;

    // Iterate for all the
    // elements of the array
    for(int i = 0; i < n; i++)
    {

        // Initialise NGE as -1
        next = -1;

        for(int j = i + 1; j < 2 * n; j++)
        {

            // Checking for next
            // greater element
            if (arr[i] < arr[j])
            {
                next = arr[j];
                break;
            }
        }

        // Print the updated NGE
        System.out.print(next + ", ");
    }
}

// Driver Code
public static void main(String args[])
{

    // Given array arr[]
    int []arr = { 1, 2, 1 };

    int N = arr.length;

    // Function call
    printNGE(arr, N);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the NGE
def printNGE(A, n):

    # Formation of circular array
    arr = [0] * (2 * n)

    # Append the given array
    # element twice
    for i in range(2 * n):
        arr[i] = A[i % n]

    # Iterate for all the
    # elements of the array
    for i in range(n):

        # Initialise NGE as -1
        next = -1

        for j in range(i + 1, 2 * n):

            # Checking for next
            # greater element
            if(arr[i] < arr[j]):
                next = arr[j]
                break

        # Print the updated NGE
        print(next, end = ", ")

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 1 ]

    N = len(arr)

    # Function call
    printNGE(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the NGE
static void printNGE(int []A, int n)
{

    // Formation of circular array
    int []arr = new int[2 * n];

    // Append the given array element twice
    for(int i = 0; i < 2 * n; i++)
       arr[i] = A[i % n];

    int next;

    // Iterate for all the
    // elements of the array
    for(int i = 0; i < n; i++)
    {

       // Initialise NGE as -1
       next = -1;

       for(int j = i + 1; j < 2 * n; j++)
       {

          // Checking for next
          // greater element
          if (arr[i] < arr[j])
          {
              next = arr[j];
              break;
          }
       }

       // Print the updated NGE
       Console.Write(next + ", ");
    }
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int []arr = { 1, 2, 1 };

    int N = arr.Length;

    // Function call
    printNGE(arr, N);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the NGE
function printNGE(A, n)
{

    // Formation of circular array
    let arr = Array.from({length: 2 * n}, (_, i) => 0);

    // Append the given array element twice
    for(let i = 0; i < 2 * n; i++)
        arr[i] = A[i % n];

    let next;

    // Iterate for all the
    // elements of the array
    for(let i = 0; i < n; i++)
    {

        // Initialise NGE as -1
        next = -1;

        for(let j = i + 1; j < 2 * n; j++)
        {

            // Checking for next
            // greater element
            if (arr[i] < arr[j])
            {
                next = arr[j];
                break;
            }
        }

        // Print the updated NGE
        document.write(next + ", ");
    }
}

// Driver Code

    // Given array arr[]
    let arr = [ 1, 2, 1 ];

    let N = arr.length;

    // Function call
    printNGE(arr, N);

</script>
```

**Output**

```
2, -1, 2, 
```

这种方法需要 0(n)2 的时间，但需要 0(n)数量级的**额外空间**

一种节省空间的解决方案是使用相同的阵列来处理圆形阵列。如果仔细观察整个数组，那么在第 n 个索引之后，下一个索引总是从 0 开始，所以使用 **mod 运算符**，我们可以很容易地访问循环列表的元素，如果我们使用(i)%n 并运行从第 I 个索引到第 n+i 个索引的循环，并应用 mod，我们可以在给定数组内的循环数组中进行遍历，而无需使用任何额外的空间。

下面是上述方法的实现:

## C++

```
// C++ program to demonstrate the use of circular
// array without using extra memory space
#include <bits/stdc++.h>
using namespace std;

// Function to find the Next Greater Element(NGE)
void printNGE(int A[], int n)
{
    int k;
    for(int i = 0; i < n; i++)
    {

        // Initialise k as -1 which is printed
        // when no NGE found
        k = -1;

        for(int j = i + 1; j < n + i; j++)
        {
            if (A[i] < A[j % n])
            {
                cout <<" "<< A[j % n];
                k = 1;
                break;
            }
        }

        // Gets executed when no NGE found
        if (k == -1)
            cout << "-1 ";
    }
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 8, 6, 7 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    printNGE(arr, N);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to demonstrate the use of circular
// array without using extra memory space

#include <stdio.h>

// Function to find the Next Greater Element(NGE)
void printNGE(int A[], int n)
{
    int k;
    for (int i = 0; i < n; i++) {
        // Initialise k as -1 which is printed when no NGE
        // found
        k = -1; //
        for (int j = i + 1; j < n + i; j++) {
            if (A[i] < A[j % n]) {
                printf("%d ", A[j % n]);
                k = 1;
                break;
            }
        }
        if (k == -1) // Gets executed when no NGE found
            printf("-1 ");
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 8, 6, 7 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    printNGE(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate the
// use of circular array without
// using extra memory space
import java.io.*;

class GFG{

// Function to find the Next
// Greater Element(NGE)
static void printNGE(int A[], int n)
{
    int k;
    for(int i = 0; i < n; i++)
    {

        // Initialise k as -1 which is
        // printed when no NGE found
        k = -1;
        for(int j = i + 1; j < n + i; j++)
        {
            if (A[i] < A[j % n])
            {
                System.out.print(A[j % n] + " ");
                k = 1;
                break;
            }
        }

        // Gets executed when no NGE found
        if (k == -1)
            System.out.print("-1 ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int[] arr = { 8, 6, 7 };

    int N = arr.length;

    // Function call
    printNGE(arr, N);
}
}

// This code is contributed by yashbeersingh42
```

## 蟒蛇 3

```
# Python3 program to demonstrate the use of circular
# array without using extra memory space

# Function to find the Next Greater Element(NGE)
def printNGE(A, n) :

    for i in range(n) :

        # Initialise k as -1 which is printed when no NGE
        # found
        k = -1
        for j in range(i + 1, n + i) :
            if (A[i] < A[j % n]) :
                print(A[j % n], end = " ")
                k = 1
                break

        if (k == -1) : # Gets executed when no NGE found
            print("-1 ", end = "")

# Given array arr[]
arr = [ 8, 6, 7 ]

N = len(arr)

# Function call
printNGE(arr, N)

# This code is contributed by divyeshrabadia07
```

## C#

```
// C# program to demonstrate the
// use of circular array without
// using extra memory space
using System;
class GFG {

    // Function to find the Next
    // Greater Element(NGE)
    static void printNGE(int[] A, int n)
    {
        int k;
        for(int i = 0; i < n; i++)
        {

            // Initialise k as -1 which is
            // printed when no NGE found
            k = -1;
            for(int j = i + 1; j < n + i; j++)
            {
                if (A[i] < A[j % n])
                {
                    Console.Write(A[j % n] + " ");
                    k = 1;
                    break;
                }
            }

            // Gets executed when no NGE found
            if (k == -1)
                Console.Write("-1 ");
        }
    }

  static void Main()
  {

    // Given array arr[]
    int[] arr = { 8, 6, 7 };

    int N = arr.Length;

    // Function call
    printNGE(arr, N);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // JavaScript program to demonstrate the
    // use of circular array without
    // using extra memory space

    // Function to find the Next
    // Greater Element(NGE)
    function printNGE(A, n)
    {
        let k;
        for(let i = 0; i < n; i++)
        {

            // Initialise k as -1 which is
            // printed when no NGE found
            k = -1;
            for(let j = i + 1; j < n + i; j++)
            {
                if (A[i] < A[j % n])
                {
                    document.write(A[j % n] + " ");
                    k = 1;
                    break;
                }
            }

            // Gets executed when no NGE found
            if (k == -1)
                document.write("-1 ");
        }
    }

    // Given array arr[]
    let arr = [ 8, 6, 7 ];

    let N = arr.length;

    // Function call
    printNGE(arr, N);

</script>
```

**Output**

```
-1 7 8 
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)

**方法 3 次:**该方法使用方法 2 中用于循环数组的相同概念，但使用 Stack 找出 O(n)时间复杂度中下一个较大的元素，其中 n 是数组的大小。为了更好的理解，你可以看到[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find the Next Greater Element(NGE)
void printNGE(int a[], int n)
{
    stack <int> s;
      vector<int> ans(n);
        for(int i=2*n-1;i>=0;i--)
        {
            while(!s.empty() && a[i%n]>=s.top())
                s.pop();
            if(i<n){
            if(!s.empty())
            {
                ans[i]=s.top();
            }
            else
            {
                ans[i]=-1;               
            }
            }
            s.push(a[i%n]);
         }

    for (int i = 0; i < n; i++) {
          cout<<ans[i]<<" ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 8, 6, 7 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    printNGE(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.util.*;
class GFG {

  public static void printNGE(int[] arr)
  {
        Stack<Integer> stack = new Stack<>();
        int n = arr.length;
        int[] result = new int[n];

        for(int i = 2*n - 1; i >= 0; i--)
        {

            // Remove all the elements in Stack that are less than arr[i%n]
            while(!stack.isEmpty() && arr[i % n] >= stack.peek()){
                stack.pop();
            }
            if(i < n)
            {
                if(!stack.isEmpty())
                    result[i] = stack.peek();
                else
                    result[i] = -1; // When none of elements in Stack are greater than arr[i%n]
            }
            stack.push(arr[i % n]);
        }
        for(int i:result)
        {
          System.out.print(i + " ");
        }
    }

  // Driver code
  public static void main (String[] args) {
      int[] arr = {8, 6 , 7};

      printNGE(arr);

    }
}

// This code is contributed by vaibhavpatel1904.
```

**Output**

```
-1 7 8 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)