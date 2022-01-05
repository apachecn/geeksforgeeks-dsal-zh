# 找出数组左侧最近的较小数字

> 原文:[https://www . geesforgeks . org/在数组左侧查找最近的较小数字/](https://www.geeksforgeeks.org/find-the-nearest-smaller-numbers-on-left-side-in-an-array/)

给定一个整数数组，为每个元素找到最近的较小的数字，使较小的元素位于左侧。

**示例:**

```
Input:  arr[] = {1, 6, 4, 10, 2, 5}
Output:         {_, 1, 1,  4, 1, 2}
First element ('1') has no element on left side. For 6, 
there is only one smaller element on left side '1'. 
For 10, there are three smaller elements on left side (1,
6 and 4), nearest among the three elements is 4.

Input: arr[] = {1, 3, 0, 2, 5}
Output:        {_, 1, _, 0, 2}
```

预期时间复杂度为 0(n)。

一个**简单的解决方案**是使用两个嵌套循环。外部循环从第二个元素开始，内部循环到达外部循环拾取的元素左侧的所有元素，并在找到较小的元素后立即停止。

## C++

```
// C++ implementation of simple algorithm to find
// smaller element on left side
#include <iostream>
using namespace std;

// Prints smaller elements on left side of every element
void printPrevSmaller(int arr[], int n)
{
    // Always print empty or '_' for first element
    cout << "_, ";

    // Start from second element
    for (int i=1; i<n; i++)
    {
        // look for smaller element on left of 'i'
        int j;
        for (j=i-1; j>=0; j--)
        {
            if (arr[j] < arr[i])
            {
                cout << arr[j] << ", ";
                break;
            }
        }

        // If there is no smaller element on left of 'i'
        if (j == -1)
           cout << "_, " ;
    }
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = {1, 3, 0, 2, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    printPrevSmaller(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of simple
// algorithm to find smaller
// element on left side
import java.io.*;
class GFG {

// Prints smaller elements on
// left side of every element
static void printPrevSmaller(int []arr, int n)
{

    // Always print empty or '_'
    // for first element
    System.out.print( "_, ");

    // Start from second element
    for (int i = 1; i < n; i++)
    {
        // look for smaller
        // element on left of 'i'
        int j;
        for(j = i - 1; j >= 0; j--)
        {
            if (arr[j] < arr[i])
            {
                System.out.print(arr[j] + ", ");
                break;
            }
        }

        // If there is no smaller
        // element on left of 'i'
        if (j == -1)
        System.out.print( "_, ") ;
    }
}

    // Driver Code
    public static void main (String[] args)
    {
        int []arr = {1, 3, 0, 2, 5};
        int n = arr.length;
        printPrevSmaller(arr, n);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 implementation of simple
# algorithm to find smaller element
# on left side

# Prints smaller elements on left
# side of every element
def printPrevSmaller(arr, n):

    # Always print empty or '_' for
    # first element
    print("_, ", end="")

    # Start from second element
    for i in range(1, n ):

        # look for smaller element
        # on left of 'i'
        for j in range(i-1 ,-2 ,-1):

            if (arr[j] < arr[i]):

                print(arr[j] ,", ",
                            end="")
                break

        # If there is no smaller
        # element on left of 'i'
        if (j == -1):
            print("_, ", end="")

# Driver program to test insertion
# sort
arr = [1, 3, 0, 2, 5]
n = len(arr)
printPrevSmaller(arr, n)

# This code is contributed by
# Smitha
```

## C#

```
// C# implementation of simple
// algorithm to find smaller
// element on left side
using System;

class GFG {

    // Prints smaller elements on
    // left side of every element
    static void printPrevSmaller(int []arr,
                                    int n)
    {

        // Always print empty or '_'
        // for first element
        Console.Write( "_, ");

        // Start from second element
        for (int i = 1; i < n; i++)
        {
            // look for smaller
            // element on left of 'i'
            int j;
            for(j = i - 1; j >= 0; j--)
            {
                if (arr[j] < arr[i])
                {
                    Console.Write(arr[j]
                                + ", ");
                    break;
                }
            }

            // If there is no smaller
            // element on left of 'i'
            if (j == -1)
            Console.Write( "_, ") ;
        }
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {1, 3, 0, 2, 5};
        int n = arr.Length;
        printPrevSmaller(arr, n);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of simple
// algorithm to find smaller
// element on left side

// Prints smaller elements on
// left side of every element
function printPrevSmaller( $arr, $n)
{

    // Always print empty or
    // '_' for first element
    echo "_, ";

    // Start from second element
    for($i = 1; $i < $n; $i++)
    {

        // look for smaller
        // element on left of 'i'
        $j;
        for($j = $i - 1; $j >= 0; $j--)
        {
            if ($arr[$j] < $arr[$i])
            {
                echo $arr[$j] , ", ";
                break;
            }
        }

        // If there is no smaller
        // element on left of 'i'
        if ($j == -1)
        echo "_, " ;
    }
}

    // Driver Code
    $arr = array(1, 3, 0, 2, 5);
    $n = count($arr);
    printPrevSmaller($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript implementation
// of simple algorithm to find
// smaller element on left side

// Prints smaller elements on
// left side of every element
function printPrevSmaller( arr, n)
{
    // Always print empty or '_' for first element
    document.write("_, ");

    // Start from second element
    for (let i=1; i<n; i++)
    {
        // look for smaller element on left of 'i'
        let j;
        for (j=i-1; j>=0; j--)
        {
            if (arr[j] < arr[i])
            {
                 document.write(arr[j] + ", ");
                break;
            }
        }

        // If there is no smaller element on left of 'i'
        if (j == -1)
           document.write("_, ");
    }
}

    // Driver program

    let arr = [ 1, 3, 0, 2, 5 ];
    let n = arr.length;
    printPrevSmaller(arr, n);

</script>
```

**输出:**

```
_, 1, _, 0, 2, ,
```

上述解的时间复杂度为 O(n <sup>2</sup> )。

可以有一个在 O(n)时间内有效的**高效解决方案**。想法是使用堆栈。堆栈用于维护到目前为止已经处理过的值的子序列，该子序列小于已经处理过的任何后续值。
下面是基于堆栈的算法

```
Let input sequence be 'arr[]' and size of array be 'n'

1) Create a new empty stack S

2) For every element 'arr[i]' in the input sequence 'arr[]',
   where 'i' goes from 0 to n-1.
    a) while S is nonempty and the top element of 
       S is greater than or equal to 'arr[i]':
           pop S

    b) if S is empty:
           'arr[i]' has no preceding smaller value
    c) else:
           the nearest smaller value to 'arr[i]' is 
           the top element of S

    d) push 'arr[i]' onto S
```

下面是上述算法的实现。

## C++

```
// C++ implementation of efficient algorithm to find
// smaller element on left side
#include <iostream>
#include <stack>
using namespace std;

// Prints smaller elements on left side of every element
void printPrevSmaller(int arr[], int n)
{
    // Create an empty stack
    stack<int> S;

    // Traverse all array elements
    for (int i=0; i<n; i++)
    {
        // Keep removing top element from S while the top
        // element is greater than or equal to arr[i]
        while (!S.empty() && S.top() >= arr[i])
            S.pop();

        // If all elements in S were greater than arr[i]
        if (S.empty())
            cout << "_, ";
        else  //Else print the nearest smaller element
            cout << S.top() << ", ";

        // Push this element
        S.push(arr[i]);
    }
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = {1, 3, 0, 2, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    printPrevSmaller(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Stack;

//Java implementation of efficient algorithm to find
// smaller element on left side
class GFG {

// Prints smaller elements on left side of every element
    static void printPrevSmaller(int arr[], int n) {
        // Create an empty stack
        Stack<Integer> S = new Stack<>();

        // Traverse all array elements
        for (int i = 0; i < n; i++) {
            // Keep removing top element from S while the top
            // element is greater than or equal to arr[i]
            while (!S.empty() && S.peek() >= arr[i]) {
                S.pop();
            }

            // If all elements in S were greater than arr[i]
            if (S.empty()) {
                System.out.print("_, ");
            } else //Else print the nearest smaller element
            {
                System.out.print(S.peek() + ", ");
            }

            // Push this element
            S.push(arr[i]);
        }
    }

    /* Driver program to test insertion sort */
    public static void main(String[] args) {
        int arr[] = {1, 3, 0, 2, 5};
        int n = arr.length;
        printPrevSmaller(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of efficient
# algorithm to find smaller element
# on left side
import math as mt

# Prints smaller elements on left
# side of every element
def printPrevSmaller(arr, n):

    # Create an empty stack
    S = list()

    # Traverse all array elements
    for i in range(n):

        # Keep removing top element from S
        # while the top element is greater
        # than or equal to arr[i]
        while (len(S) > 0 and S[-1] >= arr[i]):
            S.pop()

        # If all elements in S were greater
        # than arr[i]
        if (len(S) == 0):
            print("_, ", end = "")
        else: # Else print the nearest
              # smaller element
            print(S[-1], end = ", ")

        # Push this element
        S.append(arr[i])

# Driver Code
arr = [ 1, 3, 0, 2, 5]
n = len(arr)
printPrevSmaller(arr, n)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of efficient algorithm to find
// smaller element on left side
using System;
using System.Collections.Generic;

public class GFG
{

    // Prints smaller elements on left side of every element
    static void printPrevSmaller(int []arr, int n)
    {
        // Create an empty stack
        Stack<int> S = new Stack<int>();

        // Traverse all array elements
        for (int i = 0; i < n; i++)
        {
            // Keep removing top element from S while the top
            // element is greater than or equal to arr[i]
            while (S.Count != 0 && S.Peek() >= arr[i])
            {
                S.Pop();
            }

            // If all elements in S were greater than arr[i]
            if (S.Count == 0)
            {
                Console.Write("_, ");
            }
            else //Else print the nearest smaller element
            {
                Console.Write(S.Peek() + ", ");
            }

            // Push this element
            S.Push(arr[i]);
        }
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        int []arr = {1, 3, 0, 2, 5};
        int n = arr.Length;
        printPrevSmaller(arr, n);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of efficient
// algorithm to find smaller element on left side

// Prints smaller elements on left
// side of every element
function printPrevSmaller(arr, n)
{

    // Create an empty stack
    let S = [];

    // Traverse all array elements
    for(let i = 0; i < n; i++)
    {

        // Keep removing top element from S
        // while the top element is greater
        // than or equal to arr[i]
        while ((S.length != 0) &&
             (S[S.length - 1] >= arr[i]))
        {
            S.pop();
        }

        // If all elements in S were
        // greater than arr[i]
        if (S.length == 0)
        {
            document.write("_, ");
        }

        // Else print the nearest smaller element
        else
        {
            document.write(S[S.length - 1] + ", ");
        }

        // Push this element
        S.push(arr[i]);
    }
}

// Driver code
let arr = [ 1, 3, 0, 2, 5 ];
let n = arr.length;

printPrevSmaller(arr, n);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
_, 1, _, 0, 2,
```

上述程序的时间复杂度为 0(n)，因为每个元素最多被推入和弹出一次到堆栈。所以每个元素执行的操作总数是恒定的。
本文由阿希什·库马尔·辛格供稿。如果您发现上述代码/算法不正确，请写评论，或者找到其他方法解决相同的问题。