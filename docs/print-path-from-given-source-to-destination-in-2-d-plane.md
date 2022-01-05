# 在二维平面中打印从给定源到目的地的路径

> 原文:[https://www . geesforgeks . org/print-path-从给定源到目标的二维平面/](https://www.geeksforgeeks.org/print-path-from-given-source-to-destination-in-2-d-plane/)

给定源点 **(src <sub>x</sub> 、src <sub>y</sub> )** 和目的点 **(dst <sub>x</sub> 、dst <sub>y</sub> )** 的坐标，任务是确定从源点到达目的点的可能路径。从任何一点来看 **(x，y)** 只有两种有效招式: **(2 * x + y，y)** 或 **(x，2 * y + x)** 。如果路径不存在，则打印 **-1** 。
**例:**

> **输入:【src <sub>x</sub> 、src <sub>和</sub>= { 5.8 }，(dst <sub>x</sub> 、dst <sub>和</sub>= { 83.21 }**

**方法:**想法是使用从每个点
进行两次[递归](https://www.geeksforgeeks.org/recursion/)调用

1.  在第一次递归调用中，通过 **(2 * x + y)** 更新**‘x’**，并且不改变 **y** 坐标。
2.  在第二次递归调用中，通过 **(2 * y + x)** 更新**‘y’**，并且不改变 **x** 坐标。

如果当前坐标 **x** 或 **y** 超过目的地坐标，我们终止递归调用。将路径存储在[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)中，到达堆栈
的目的打印元素后，执行上述方法:

## C++

```
// C++ program for printing a path from
// given source to destination
#include <bits/stdc++.h>
using namespace std;

// Function to print the path
void printExistPath(stack<int> sx, stack<int> sy, int last)
{
    // Base condition
    if (sx.empty() || sy.empty()) {
        return;
    }
    int x = sx.top();
    int y = sy.top();

    // Pop stores elements
    sx.pop();
    sy.pop();

    // Recursive call for printing stack
    // In reverse order
    printExistPath(sx, sy, last);
    if (sx.size() == last - 1) {

        cout << "(" << x << ", " << y << ")";
    }
    else {
        cout << "(" << x << ", " << y << ") -> ";
    }
}

// Function to store the path into
// The stack, if path exist
bool storePath(int srcX, int srcY, int destX, int destY,
            stack<int>& sx, stack<int>& sy)
{
    // Base condition
    if (srcX > destX || srcY > destY) {
        return false;
    }

    // Push current elements
    sx.push(srcX);
    sy.push(srcY);

    // Condition to check whether reach to the
    // Destination or not
    if (srcX == destX && srcY == destY) {
        printExistPath(sx, sy, sx.size());
        return true;
    }

    // Increment 'x' ordinate of source by (2*x+y)
    // Keeping 'y' constant
    if (storePath((2 * srcX) + srcY, srcY, destX, destY, sx, sy)) {
        return true;
    }

    // Increment 'y' ordinate of source by (2*y+x)
    // Keeping 'x' constant
    if (storePath(srcX, (2 * srcY) + srcX, destX, destY, sx, sy)) {
        return true;
    }

    // Pop current elements form stack
    sx.pop();
    sy.pop();

    // If no path exists
    return false;
}

// Utility function to check whether path exist or not
bool isPathExist(int srcX, int srcY, int destX, int destY)
{
    // To store x co-ordinate
    stack<int> sx;

    // To store y co-ordinate
    stack<int> sy;

    return storePath(srcX, srcY, destX, destY, sx, sy);
}

// Function to find the path
void printPath(int srcX, int srcY, int destX, int destY)
{
    if (!isPathExist(srcX, srcY, destX, destY))
    {
        // Print -1, if path doesn't exist
        cout << "-1";
    }
}

// Driver code
int main()
{
    int srcX = 5, srcY = 8;

    int destX = 83, destY = 21;

    // Function call
    printPath(srcX, srcY, destX, destY);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for printing a path from
// given source to destination
import java.util.*;

class GFG{

// Function to print the path
static void printExistPath(Stack<Integer> sx,
                Stack<Integer> sy, int last)
{
    // Base condition
    if (sx.isEmpty() || sy.isEmpty()) {
        return;
    }
    int x = sx.peek();
    int y = sy.peek();

    // Pop stores elements
    sx.pop();
    sy.pop();

    // Recursive call for printing stack
    // In reverse order
    printExistPath(sx, sy, last);
    if (sx.size() == last - 1) {

        System.out.print("(" + x+ ", " + y+ ")");
    }
    else {
        System.out.print("(" + x+ ", " + y+ ")->");
    }
}

// Function to store the path into
// The stack, if path exist
static boolean storePath(int srcX, int srcY,
                        int destX, int destY,
            Stack<Integer> sx, Stack<Integer> sy)
{
    // Base condition
    if (srcX > destX || srcY > destY) {
        return false;
    }

    // Push current elements
    sx.add(srcX);
    sy.add(srcY);

    // Condition to check whether reach to the
    // Destination or not
    if (srcX == destX && srcY == destY) {
        printExistPath(sx, sy, sx.size());
        return true;
    }

    // Increment 'x' ordinate of source by (2*x+y)
    // Keeping 'y' constant
    if (storePath((2 * srcX) + srcY, srcY,
                    destX, destY, sx, sy))
    {
        return true;
    }

    // Increment 'y' ordinate of source by (2*y+x)
    // Keeping 'x' constant
    if (storePath(srcX, (2 * srcY) + srcX,
                    destX, destY, sx, sy))
    {
        return true;
    }

    // Pop current elements form stack
    sx.pop();
    sy.pop();

    // If no path exists
    return false;
}

// Utility function to check whether path exist or not
static boolean isPathExist(int srcX, int srcY,
                        int destX, int destY)
{
    // To store x co-ordinate
    Stack<Integer> sx = new Stack<Integer>();

    // To store y co-ordinate
    Stack<Integer> sy = new Stack<Integer>();

    return storePath(srcX, srcY, destX,
                    destY, sx, sy);
}

// Function to find the path
static void printPath(int srcX, int srcY,
                    int destX, int destY)
{
    if (!isPathExist(srcX, srcY, destX, destY))
    {
        // Print -1, if path doesn't exist
        System.out.print("-1");
    }
}

// Driver code
public static void main(String[] args)
{
    int srcX = 5, srcY = 8;

    int destX = 83, destY = 21;

    // Function call
    printPath(srcX, srcY, destX, destY);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for printing a path from
# given source to destination

# Function to print the path
def printExistPath( sx,  sy, last):

    # Base condition
    if (len(sx) == 0 or len(sy) == 0):
        return

    x = sx[-1];
    y = sy[-1]

    # Pop stores elements
    sx.pop();
    sy.pop();

    # Recursive call for printing stack
    # In reverse order
    printExistPath(sx, sy, last);

    if (len(sx) == last - 1):
        print("(" + str(x) + ", " + str(y) + ")", end='')

    else:
        print("(" + str(x) + ", " + str(y) + ") -> ", end='')

# Function to store the path into
# The stack, if path exist
def storePath(srcX, srcY, destX, destY, sx,  sy):

    # Base condition
    if (srcX > destX or srcY > destY):
        return False;

    # Push current elements
    sx.append(srcX);
    sy.append(srcY);

    # Condition to check whether reach to the
    # Destination or not
    if (srcX == destX and srcY == destY):
        printExistPath(sx, sy, len(sx));
        return True;

    # Increment 'x' ordinate of source by (2*x+y)
    # Keeping 'y' constant
    if (storePath((2 * srcX) + srcY, srcY, destX, destY, sx, sy)):
        return True;

    # Increment 'y' ordinate of source by (2*y+x)
    # Keeping 'x' constant
    if (storePath(srcX, (2 * srcY) + srcX, destX, destY, sx, sy)):
        return True;

    # Pop current elements form stack
    sx.pop();
    sy.pop();

    # If no path exists
    return False;

# Utility function to check whether path exist or not
def isPathExist(srcX, srcY, destX, destY):

    # To store x co-ordinate
    sx = []

    # To store y co-ordinate
    sy = []

    return storePath(srcX, srcY, destX, destY, sx, sy);

# Function to find the path
def printPath(srcX, srcY, destX, destY):

    if (not isPathExist(srcX, srcY, destX, destY)):

        # Print -1, if path doesn't exist
        print("-1");

# Driver code
if __name__=='__main__':

    srcX = 5
    srcY = 8;

    destX = 83
    destY = 21;

    # Function call
    printPath(srcX, srcY, destX, destY);

    # This code is contributed by rutvik_56
```

## C#

```
// C# program for printing a path from
// given source to destination
using System;
using System.Collections.Generic;

class GFG{

// Function to print the path
static void printExistPath(Stack<int> sx,
                Stack<int> sy, int last)
{
    // Base condition
    if (sx.Count == 0 || sy.Count == 0) {
        return;
    }
    int x = sx.Peek();
    int y = sy.Peek();

    // Pop stores elements
    sx.Pop();
    sy.Pop();

    // Recursive call for printing stack
    // In reverse order
    printExistPath(sx, sy, last);
    if (sx.Count == last - 1) {

        Console.Write("(" + x + ", " + y + ")");
    }
    else {
        Console.Write("(" + x + ", " + y + ")->");
    }
}

// Function to store the path into
// The stack, if path exist
static bool storePath(int srcX, int srcY,
                        int destX, int destY,
            Stack<int> sx, Stack<int> sy)
{
    // Base condition
    if (srcX > destX || srcY > destY) {
        return false;
    }

    // Push current elements
    sx.Push(srcX);
    sy.Push(srcY);

    // Condition to check whether reach to the
    // Destination or not
    if (srcX == destX && srcY == destY) {
        printExistPath(sx, sy, sx.Count);
        return true;
    }

    // Increment 'x' ordinate of source by (2*x+y)
    // Keeping 'y' constant
    if (storePath((2 * srcX) + srcY, srcY,
                    destX, destY, sx, sy))
    {
        return true;
    }

    // Increment 'y' ordinate of source by (2*y+x)
    // Keeping 'x' constant
    if (storePath(srcX, (2 * srcY) + srcX,
                    destX, destY, sx, sy))
    {
        return true;
    }

    // Pop current elements form stack
    sx.Pop();
    sy.Pop();

    // If no path exists
    return false;
}

// Utility function to check whether path exist or not
static bool isPathExist(int srcX, int srcY,
                        int destX, int destY)
{
    // To store x co-ordinate
    Stack<int> sx = new Stack<int>();

    // To store y co-ordinate
    Stack<int> sy = new Stack<int>();

    return storePath(srcX, srcY, destX,
                    destY, sx, sy);
}

// Function to find the path
static void printPath(int srcX, int srcY,
                    int destX, int destY)
{
    if (!isPathExist(srcX, srcY, destX, destY))
    {
        // Print -1, if path doesn't exist
        Console.Write("-1");
    }
}

// Driver code
public static void Main(String[] args)
{
    int srcX = 5, srcY = 8;

    int destX = 83, destY = 21;

    // Function call
    printPath(srcX, srcY, destX, destY);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for printing a path from
    // given source to destination

    // Function to print the path
    function printExistPath(sx, sy, last)
    {
        // Base condition
        if (sx.length == 0 || sy.length == 0) {
            return;
        }
        let x = sx[sx.length - 1];
        let y = sy[sy.length - 1];

        // Pop stores elements
        sx.pop();
        sy.pop();

        // Recursive call for printing stack
        // In reverse order
        printExistPath(sx, sy, last);
        if (x==83) {

            document.write("(" + x + ", " + y + ")");
        }
        else {
            document.write("(" + x + ", " + y + ") -> ");
        }
    }

    // Function to store the path into
    // The stack, if path exist
    function storePath(srcX, srcY, destX, destY, sx, sy)
    {
        // Base condition
        if (srcX > destX || srcY > destY) {
            return false;
        }

        // Push current elements
        sx.push(srcX);
        sy.push(srcY);

        // Condition to check whether reach to the
        // Destination or not
        if (srcX == destX && srcY == destY) {
            printExistPath(sx, sy, sx.length);
            return true;
        }

        // Increment 'x' ordinate of source by (2*x+y)
        // Keeping 'y' constant
        if (storePath((2 * srcX) + srcY, srcY,
                        destX, destY, sx, sy))
        {
            return true;
        }

        // Increment 'y' ordinate of source by (2*y+x)
        // Keeping 'x' constant
        if (storePath(srcX, (2 * srcY) + srcX,
                        destX, destY, sx, sy))
        {
            return true;
        }

        // Pop current elements form stack
        sx.pop();
        sy.pop();

        // If no path exists
        return false;
    }

    // Utility function to check whether path exist or not
    function isPathExist(srcX, srcY, destX, destY)
    {
        // To store x co-ordinate
        let sx = [];

        // To store y co-ordinate
        let sy = [];

        return storePath(srcX, srcY, destX, destY, sx, sy);
    }

    // Function to find the path
    function printPath(srcX, srcY, destX, destY)
    {
        if (!isPathExist(srcX, srcY, destX, destY))
        {
            // Print -1, if path doesn't exist
            document.write("-1");
        }
    }

    let srcX = 5, srcY = 8;

    let destX = 83, destY = 21;

    // Function call
    printPath(srcX, srcY, destX, destY);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
(5, 8) -> (5, 21) -> (31, 21) -> (83, 21)
```