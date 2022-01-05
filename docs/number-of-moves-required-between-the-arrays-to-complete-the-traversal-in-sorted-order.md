# 按排序顺序完成遍历所需的数组间移动次数

> 原文:[https://www . geeksforgeeks . org/需要在数组之间移动多少次才能按排序顺序完成遍历/](https://www.geeksforgeeks.org/number-of-moves-required-between-the-arrays-to-complete-the-traversal-in-sorted-order/)

给定大小为 **N** 的两个排序的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **X[]** 和大小为 **M** 的 **Y[]** 具有唯一值。任务是计算数组之间以升序遍历两个数组中的所有元素所需的移动总数。如果最初，遍历从 **X[]** 数组开始。

**示例:**

> ***输入:** X[] = {1}，Y[] = {2，3，4}*
> ***输出:** 1*
> ***说明:**遍历 X 数组后只需移动 1 次，然后移动到**Y 数组的 *0* 索引*并遍历其剩余的值。**
> 
> **输入** ***:** X[] = {1，3，4}，Y[] = {2，5，6}*
> ***输出:** 3*

**方法:**给定的问题可以使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。按照以下步骤解决问题:

*   初始化两个指针，说 **i** 为 **0** 和 **j** 为 **0** 分别指向 **X[]** 和 **Y[]** 数组。
*   将另一个变量 **total_moves** 初始化为 **0** ，以存储所需的移动次数。
*   由于[遍历](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)总是从 **X[]** 数组开始，所以首先比较当前索引处的值。出现了两种情况:
*   如果当前存在于 **X[]** 阵列:
    *   如果**X【I】<Y【j】**，只需增加指数 **i** 。
    *   如果**X【I】>Y【j】**，增加 **total_moves** 和索引 **j** 。
*   如果当前出现在 **Y[]** 阵列:
    *   如果**Y【j】<X【I】**，增量指数 **j** 。
    *   如果**Y【j】>X【I】**，增加**总 _ 移动**和索引 **i** 。
*   重复以上步骤，直到任何一个数组遍历完成。
*   一旦上述[循环](https://www.geeksforgeeks.org/range-based-loop-c/)结束，**总移动量**将在以下两种情况下递增:
    *   如果遍历在 **X** 数组和 **j < M** 结束，那么将 **total_moves** 增加 **1** 。
    *   如果遍历在 **Y** 数组和 **i < N** 结束，那么将 **total_moves** 增加 **1** 。
*   打印 **total_moves** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of moves
// required between the arrays to complete
// the traversal in sorted order
int numberofMoves(int X[], int Y[], int n, int m)
{

    // Variable to check if present
    // at X array or not
    bool present_at_X = true;

    // Store total number of moves
    int total_moves = 0;

    // Initialize i and j pointing to X and
    // Y array respectively
    int i = 0, j = 0;

    // Loop until one array is
    // completely traversed
    while (i < n && j < m) {

        // If currently present at X array,
        // and X[i]<Y[j], increment index i
        if (present_at_X == true && X[i] < Y[j]) {
            i++;
        }

        // If present at X array and Y[j]<X[i]
        else if (present_at_X == true && Y[j] < X[i]) {

            // Increment total_moves and update
            // present at X variable and index j
            total_moves++;
            present_at_X = false;
            j++;
        }

        // If present at Y array and
        // Y[j] < X[i], increment j
        else if (present_at_X == false && Y[j] < X[i]) {
            j++;
        }

        // If present at Y array and
        // X[i] < Y[j]
        else if (present_at_X == false && X[i] < Y[j]) {

            // Increment total_moves and index i
            // and update present at X variable
            total_moves++;
            present_at_X = true;
            i++;
        }
    }

    // Check if present at X array and j < m,
    // so increment total_moves by 1
    if (present_at_X == true && j < m) {
        total_moves++;
        present_at_X = false;
    }

    // If finished traversal at Y array
    // and X's array traversal is left,
    // increment total_moves by 1
    if (present_at_X == false && i < n) {
        total_moves++;
        present_at_X = true;
    }

    // Return the result
    return total_moves;
}

// Driver Code
int main()
{

    // Given Input
    int X[] = { 1, 3, 4 };
    int n = sizeof(X) / sizeof(X[0]);
    int Y[] = { 2, 5, 6 };
    int m = sizeof(Y) / sizeof(Y[0]);

    // Function Call
    cout << numberofMoves(X, Y, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the number of moves
// required between the arrays to complete
// the traversal in sorted order
static int numberofMoves(int[] X, int Y[], int n, int m)
{

    // Variable to check if present
    // at X array or not
    boolean present_at_X = true;

    // Store total number of moves
    int total_moves = 0;

    // Initialize i and j pointing to X and
    // Y array respectively
    int i = 0, j = 0;

    // Loop until one array is
    // completely traversed
    while (i < n && j < m) {

        // If currently present at X array,
        // and X[i]<Y[j], increment index i
        if (present_at_X == true && X[i] < Y[j]) {
            i++;
        }

        // If present at X array and Y[j]<X[i]
        else if (present_at_X == true && Y[j] < X[i]) {

            // Increment total_moves and update
            // present at X variable and index j
            total_moves++;
            present_at_X = false;
            j++;
        }

        // If present at Y array and
        // Y[j] < X[i], increment j
        else if (present_at_X == false && Y[j] < X[i]) {
            j++;
        }

        // If present at Y array and
        // X[i] < Y[j]
        else if (present_at_X == false && X[i] < Y[j]) {

            // Increment total_moves and index i
            // and update present at X variable
            total_moves++;
            present_at_X = true;
            i++;
        }
    }

    // Check if present at X array and j < m,
    // so increment total_moves by 1
    if (present_at_X == true && j < m) {
        total_moves++;
        present_at_X = false;
    }

    // If finished traversal at Y array
    // and X's array traversal is left,
    // increment total_moves by 1
    if (present_at_X == false && i < n) {
        total_moves++;
        present_at_X = true;
    }

    // Return the result
    return total_moves;
}

// Driver Code
public static void main(String[] args)
{
    // Given Input
    int X[] = { 1, 3, 4 };
    int n = X.length;
    int Y[] = { 2, 5, 6 };
    int m = Y.length;

    // Function Call
    System.out.print(numberofMoves(X, Y, n, m));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of moves
# required between the arrays to complete
# the traversal in sorted order
def numberofMoves(X, Y, n, m):

    # Variable to check if present
    # at X array or not
    present_at_X = True

    # Store total number of moves
    total_moves = 0

    # Initialize i and j pointing to X and
    # Y array respectively
    i, j = 0, 0

    # Loop until one array is
    # completely traversed
    while (i < n and j < m):

        # If currently present at X array,
        # and X[i]<Y[j], increment index i
        if (present_at_X == True and X[i] < Y[j]):
            i += 1

        # If present at X array and Y[j]<X[i]
        elif (present_at_X == True and Y[j] < X[i]):

            # Increment total_moves and update
            # present at X variable and index j
            total_moves += 1
            present_at_X = False
            j += 1

        # If present at Y array and
        # Y[j] < X[i], increment j
        elif (present_at_X == False and Y[j] < X[i]):
            j += 1

        # If present at Y array and
        # X[i] < Y[j]
        elif (present_at_X == False and X[i] < Y[j]):

            # Increment total_moves and index i
            # and update present at X variable
            total_moves += 1
            present_at_X = True
            i += 1

    # Check if present at X array and j < m,
    # so increment total_moves by 1
    if (present_at_X == True and j < m):
        total_moves += 1
        present_at_X = False

    # If finished traversal at Y array
    # and X's array traversal is left,
    # increment total_moves by 1
    if (present_at_X == False and i < n):
        total_moves += 1
        present_at_X = True

    # Return the result
    return total_moves

# Driver Code
if __name__ == '__main__':

    # Given Input
    X = [ 1, 3, 4 ]
    n = len(X)
    Y = [ 2, 5, 6 ]
    m = len(Y)

    # Function Call
    print(numberofMoves(X, Y, n, m))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach

using System;

public class GFG{

    // Function to find the number of moves
// required between the arrays to complete
// the traversal in sorted order
static int numberofMoves(int[] X, int[] Y, int n, int m)
{

    // Variable to check if present
    // at X array or not
    bool present_at_X = true;

    // Store total number of moves
    int total_moves = 0;

    // Initialize i and j pointing to X and
    // Y array respectively
    int i = 0, j = 0;

    // Loop until one array is
    // completely traversed
    while (i < n && j < m) {

        // If currently present at X array,
        // and X[i]<Y[j], increment index i
        if (present_at_X == true && X[i] < Y[j]) {
            i++;
        }

        // If present at X array and Y[j]<X[i]
        else if (present_at_X == true && Y[j] < X[i]) {

            // Increment total_moves and update
            // present at X variable and index j
            total_moves++;
            present_at_X = false;
            j++;
        }

        // If present at Y array and
        // Y[j] < X[i], increment j
        else if (present_at_X == false && Y[j] < X[i]) {
            j++;
        }

        // If present at Y array and
        // X[i] < Y[j]
        else if (present_at_X == false && X[i] < Y[j]) {

            // Increment total_moves and index i
            // and update present at X variable
            total_moves++;
            present_at_X = true;
            i++;
        }
    }

    // Check if present at X array and j < m,
    // so increment total_moves by 1
    if (present_at_X == true && j < m) {
        total_moves++;
        present_at_X = false;
    }

    // If finished traversal at Y array
    // and X's array traversal is left,
    // increment total_moves by 1
    if (present_at_X == false && i < n) {
        total_moves++;
        present_at_X = true;
    }

    // Return the result
    return total_moves;
}

// Driver Code
    static public void Main ()
    {

        // Given Input
    int[] X = { 1, 3, 4 };
    int n = X.Length;
    int[] Y = { 2, 5, 6 };
    int m = Y.Length;

    // Function Call
    Console.WriteLine(numberofMoves(X, Y, n, m));
    }
}

// This code is contributed by unknown2108.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the number of moves
// required between the arrays to complete
// the traversal in sorted order
function numberofMoves(X,Y,n,m)
{

    // Variable to check if present
    // at X array or not
    let present_at_X = true;

    // Store total number of moves
    let total_moves = 0;

    // Initialize i and j pointing to X and
    // Y array respectively
    let i = 0, j = 0;

    // Loop until one array is
    // completely traversed
    while (i < n && j < m) {

        // If currently present at X array,
        // and X[i]<Y[j], increment index i
        if (present_at_X == true && X[i] < Y[j]) {
            i++;
        }

        // If present at X array and Y[j]<X[i]
        else if (present_at_X == true && Y[j] < X[i]) {

            // Increment total_moves and update
            // present at X variable and index j
            total_moves++;
            present_at_X = false;
            j++;
        }

        // If present at Y array and
        // Y[j] < X[i], increment j
        else if (present_at_X == false && Y[j] < X[i]) {
            j++;
        }

        // If present at Y array and
        // X[i] < Y[j]
        else if (present_at_X == false && X[i] < Y[j]) {

            // Increment total_moves and index i
            // and update present at X variable
            total_moves++;
            present_at_X = true;
            i++;
        }
    }

    // Check if present at X array and j < m,
    // so increment total_moves by 1
    if (present_at_X == true && j < m) {
        total_moves++;
        present_at_X = false;
    }

    // If finished traversal at Y array
    // and X's array traversal is left,
    // increment total_moves by 1
    if (present_at_X == false && i < n) {
        total_moves++;
        present_at_X = true;
    }

    // Return the result
    return total_moves;
}

// Driver Code

    // Given Input
   var X = [1, 3, 4 ];
   var n =X.length;
   var Y = [2, 5, 6 ];
   var m = Y.length;

    // Function Call
    document.write(numberofMoves(X, Y, n, m));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
3
```

***时间复杂度:** O(N+M)*
***辅助空间:** O(1)*