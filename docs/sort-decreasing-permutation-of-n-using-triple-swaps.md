# 使用三重交换对 N 的递减排列进行排序

> 原文:[https://www . geeksforgeeks . org/sort-渐减-置换-n-use-triple-swaps/](https://www.geeksforgeeks.org/sort-decreasing-permutation-of-n-using-triple-swaps/)

给定一个由递减排列的 **N** 个数字组成的**数组 A[]** ，任务是使用三重交换对数组进行排序。如果无法对数组进行排序，则打印-1。

> 三重互换指的是选定指数的周期性右移。循环右移:x–> y–> z–> x。

**示例:**

> **输入:** A[] = {4，3，2，1}
> **输出:** 1 2 3 4
> **解释:**
> 对于给定数组，第一步是选择索引:x = 0，y = 2，z = 3
> 因此，A[3]= A[2]；A[2]= A[0]；A[0] = A[3]。
> 交换前:4 3 2 1，交换后:1 3 4 2。
> 对于给定的数组，第二步是选择索引:x = 1，y = 2，z = 3 因此，A[3]= A[2]；A[2]= A[1]；A[1] = A[3]。
> 交换前:1 3 4 2，交换后:1 2 3 4。
> **输入:** A[] = {5，4，3，2，1}
> **输出:** 1 2 3 4 5
> **解释:**
> 对于给定的数组，第一步是选择索引:x = 0，y = 3，z = 4 因此，
> A[4]= A[3]；A[3]= A[0]；A[0] = A[4]，交换前:5 4 3 2 1 和交换后:1 4 3 5 2
> 对于给定的数组，第二步是选择索引:x = 1，y = 3，z = 4 因此，
> A[4]= A[3]；A[3]= A[1]；A[1] = A[4]，交换前:1 4 3 5 2，交换后:1 2 3 4 5

**方法:**
要解决上面提到的问题，我们必须选择三个指标，这样我们才能在正确的位置带上**至少一个元素。我们的意思是，我们必须在索引 0 处引入 1，在索引 1 处引入 2，以此类推。**

1.  选择 x 作为当前索引号 I，
2.  z 被选为 x + 1 的索引，它总是 N–I–1，并且
3.  相应地选择 y。

然后，我们必须使用这些索引通过元素的循环右移来执行元素交换。

下面是上述方法的实现:

## C++

```
// C++ implementation to sort
// decreasing permutation of N
// using triple swaps

#include <bits/stdc++.h>
using namespace std;

// Function to sort Array
void sortArray(int A[], int N)
{

    // The three indices that
    // has to be chosen
    int x, y, z;

    // Check if possible to sort array
    if (N % 4 == 0 || N % 4 == 1) {

        // Swapping to bring element
        // at required position
        // Bringing at least one
        // element at correct position
        for (int i = 0; i < N / 2; i++) {

            x = i;
            if (i % 2 == 0) {

                y = N - i - 2;
                z = N - i - 1;
            }

            // Tracing changes in Array
            A[z] = A[y];
            A[y] = A[x];
            A[x] = x + 1;
        }

        // Print the sorted array
        cout << "Sorted Array: ";

        for (int i = 0; i < N; i++)

            cout << A[i] << " ";
    }

    // If not possible to sort
    else

        cout << "-1";
}

// Driver code
int main()
{

    int A[] = { 5, 4, 3, 2, 1 };

    int N = sizeof(A) / sizeof(A[0]);

    sortArray(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort
// decreasing permutation of N
// using triple swaps

class GFG{

// Function to sort array
static void sortArray(int A[], int N)
{

    // The three indices that
    // has to be chosen
    int x = 0, y = 0, z = 0;

    // Check if possible to sort array
    if (N % 4 == 0 || N % 4 == 1)
    {

        // Swapping to bring element
        // at required position
        // Bringing at least one
        // element at correct position
        for(int i = 0; i < N / 2; i++)
        {
           x = i;

           if (i % 2 == 0)
           {
               y = N - i - 2;
               z = N - i - 1;
           }

           // Tracing changes in array
           A[z] = A[y];
           A[y] = A[x];
           A[x] = x + 1;
        }

        // Print the sorted array
        System.out.print("Sorted Array: ");

        for(int i = 0; i < N; i++)
           System.out.print(A[i] + " ");
    }

    // If not possible to sort
    else
    {
        System.out.print("-1");
    }
}

// Driver code
public static void main(String[] args)
{

    int A[] = { 5, 4, 3, 2, 1 };
    int N = A.length;

    sortArray(A, N);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to sort
# decreasing permutation of N
# using triple swaps

# Function to sort array
def sortArray(A, N):

    # Check if possible to sort array
    if (N % 4 == 0 or N % 4 == 1):

        # Swapping to bring element
        # at required position
        # Bringing at least one
        # element at correct position
        for i in range(N // 2):
            x = i
            if (i % 2 == 0):
                y = N - i - 2
                z = N - i - 1

            # Tracing changes in Array
            A[z] = A[y]
            A[y] = A[x]
            A[x] = x + 1

        # Print the sorted array
        print("Sorted Array: ", end = "")

        for i in range(N):
            print(A[i], end = " ")

    # If not possible to sort
    else:
        print("-1")

# Driver code
A = [ 5, 4, 3, 2, 1 ]
N = len(A)

sortArray(A, N)

# This code is contributed by yatinagg
```

## C#

```
// C# implementation to sort
// decreasing permutation of N
// using triple swaps
using System;
class GFG{

// Function to sort array
static void sortArray(int []A, int N)
{

    // The three indices that
    // has to be chosen
    int x = 0, y = 0, z = 0;

    // Check if possible to sort array
    if (N % 4 == 0 || N % 4 == 1)
    {

        // Swapping to bring element
        // at required position
        // Bringing at least one
        // element at correct position
        for(int i = 0; i < N / 2; i++)
        {
            x = i;

            if (i % 2 == 0)
            {
                y = N - i - 2;
                z = N - i - 1;
            }

            // Tracing changes in array
            A[z] = A[y];
            A[y] = A[x];
            A[x] = x + 1;
        }

        // Print the sorted array
        Console.Write("Sorted Array: ");

        for(int i = 0; i < N; i++)
        Console.Write(A[i] + " ");
    }

    // If not possible to sort
    else
    {
        Console.Write("-1");
    }
}

// Driver code
public static void Main(String[] args)
{
    int []A = { 5, 4, 3, 2, 1 };
    int N = A.Length;

    sortArray(A, N);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to sort
// decreasing permutation of N
// using triple swaps

// Function to sort array
function sortArray(A, N)
{

    // The three indices that
    // has to be chosen
    let x = 0, y = 0, z = 0;

    // Check if possible to sort array
    if (N % 4 == 0 || N % 4 == 1)
    {

        // Swapping to bring element
        // at required position
        // Bringing at least one
        // element at correct position
        for(let i = 0; i < N / 2; i++)
        {
           x = i;

           if (i % 2 == 0)
           {
               y = N - i - 2;
               z = N - i - 1;
           }

           // Tracing changes in array
           A[z] = A[y];
           A[y] = A[x];
           A[x] = x + 1;
        }

        // Print the sorted array
        document.write("Sorted Array: ");

        for(let i = 0; i < N; i++)
           document.write(A[i] + " ");
    }

    // If not possible to sort
    else
    {
        document.write("-1");
    }
}

// Driver Code

    let A = [ 5, 4, 3, 2, 1 ];
    let N = A.length;

    sortArray(A, N);

</script>
```

**Output:** 

```
Sorted Array: 1 2 3 4 5
```