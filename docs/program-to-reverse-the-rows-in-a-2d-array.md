# 编程反转 2d 阵列中的行

> 原文:[https://www . geesforgeks . org/program-to-reverse-in-a-2d-array/](https://www.geeksforgeeks.org/program-to-reverse-the-rows-in-a-2d-array/)

给定一个大小为 **M x N** 整数的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **arr[][]** ，其中 **M** 是行数， **N** 是列数。任务是反转给定 2D 数组的每一行。
**例:**

```
Input: arr[][] = 
{ {1, 2, 3},
  {4, 5, 6},
  {7, 8, 9} }
Output:
3 2 1
6 5 4
9 8 7

Input: arr[][] = 
{ {1, 2}, 
  {4, 5}, 
  {7, 8}, 
  {9, 10} }
Output:
2 1
5 4
8 7
10 9
```

**进场:**

1.  对于给定 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中的每一行，执行以下操作:
    *   将**起始**索引初始化为 0，**结束**索引初始化为 N-1。
    *   迭代循环，直到开始索引小于结束索引，交换这些索引处的值，并将索引更新为:

```
swap(arr[i][start], arr[i][end])
start++;
end--;
```

1.  对 2D 数组中的所有行执行上述操作。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

const int M = 3;
const int N = 3;

// A utility function
// to swap the two element
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to reverse
// the given 2D arr[][]
void reverseArray(int arr[M][N])
{

    // Traverse each row of arr[][]
    for (int i = 0; i < M; i++) {

        // Initialise start and end index
        int start = 0;
        int end = N - 1;

        // Till start < end, swap the element
        // at start and end index
        while (start < end) {

            // Swap the element
            swap(&arr[i][start],
                 &arr[i][end]);

            // Increment start and decrement
            // end for next pair of swapping
            start++;
            end--;
        }
    }

    // Print the arr[][] after
    // reversing every row
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            cout << arr[i][j] << ' ';
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int arr[][3] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };

    // Function call
    reverseArray(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

static int M = 3;
static int N = 3;

// Function to reverse
// the given 2D arr[][]
static void reverseArray(int arr[][])
{

    // Traverse each row of arr[][]
    for (int i = 0; i < M; i++) {

        // Initialise start and end index
        int start = 0;
        int end = N - 1;

        // Till start < end, swap the element
        // at start and end index
        while (start < end) {

            // Swap the element
            int temp = arr[i][start];
            arr[i][start] = arr[i][end];
            arr[i][end] = temp;

            // Increment start and decrement
            // end for next pair of swapping
            start++;
            end--;
        }
    }

    // Print the arr[][] after
    // reversing every row
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            System.out.print(arr[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[][] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };

    // Function call
    reverseArray(arr);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
M = 3;N = 3;

# Function to reverse
# the given 2D arr[][]
def reverseArray(arr) :

    # Traverse each row of arr[][]
    for i in range(M) :

        # Initialise start and end index
        start = 0;
        end = N - 1;

        # Till start < end, swap the element
        # at start and end index
        while (start < end) :

            # Swap the element
            arr[i][start], arr[i][end] = arr[i][end], arr[i][start];

            # Increment start and decrement
            # end for next pair of swapping
            start += 1;
            end -= 1;

    # Print the arr[][] after
    # reversing every row
    for i in  range(M) :
        for j in range(N) :
            print(arr[i][j],end= ' ');

        print();

# Driver Code
if __name__ ==  "__main__" :

    arr = [ [ 1, 2, 3 ],
            [ 4, 5, 6 ],
            [ 7, 8, 9 ] ];

    # Function call
    reverseArray(arr);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

static int M = 3;
static int N = 3;

// Function to reverse
// the given 2D [,]arr
static void reverseArray(int [,]arr)
{

    // Traverse each row of [,]arr
    for (int i = 0; i < M; i++) {

        // Initialise start and end index
        int start = 0;
        int end = N - 1;

        // Till start < end, swap the element
        // at start and end index
        while (start < end) {

            // Swap the element
            int temp = arr[i,start];
            arr[i, start] = arr[i, end];
            arr[i, end] = temp;

            // Increment start and decrement
            // end for next pair of swapping
            start++;
            end--;
        }
    }

    // Print the [,]arr after
    // reversing every row
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {
            Console.Write(arr[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{
    int [,]arr = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };

    // Function call
    reverseArray(arr);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach   
const M = 3;
    const N = 3;

    // Function to reverse
    // the given 2D arr
    function reverseArray(arr) {

        // Traverse each row of arr
        for (i = 0; i < M; i++) {

            // Initialise start and end index
            var start = 0;
            var end = N - 1;

            // Till start < end, swap the element
            // at start and end index
            while (start < end) {

                // Swap the element
                var temp = arr[i][start];
                arr[i][start] = arr[i][end];
                arr[i][end] = temp;

                // Increment start and decrement
                // end for next pair of swapping
                start++;
                end--;
            }
        }

        // Print the arr after
        // reversing every row
        for (i = 0; i < M; i++) {
            for (j = 0; j < N; j++) {
                document.write(arr[i][j] + " ");
            }
            document.write("<br/>");
        }
    }

    // Driver Code

        var arr = [ [ 1, 2, 3 ],
        [ 4, 5, 6 ],
        [ 7, 8, 9 ] ];

        // Function call
        reverseArray(arr);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
3 2 1 
6 5 4 
9 8 7
```