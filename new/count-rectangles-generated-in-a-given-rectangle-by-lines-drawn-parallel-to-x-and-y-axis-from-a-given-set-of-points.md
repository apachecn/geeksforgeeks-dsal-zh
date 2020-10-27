# 计算从给定点集中平行于 X 和 Y 轴绘制的线在给定矩形中生成的矩形

给定 [2D 数组](https://www.geeksforgeeks.org/dynamically-allocate-2d-array-c/) [矩形[] []](https://www.geeksforgeeks.org/check-given-four-integers-sides-make-rectangle/) 表示矩形{（0，0），（L，0），（0，B），（L，B）的顶点 }的尺寸为 **L * B** ，而另一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)的大小为 **N** ，的大小为，在直角坐标系中 。 从给定数组的每个点绘制平行于 **X 轴**的水平线和平行于 **Y 轴**的垂直线。 任务是计算给定矩形内存在的所有可能的矩形。

**范例**：

> **输入**：矩形[] [] = {{0，0}，{5，0}，{0，5}，{5，5}}，points [] [] = {{1， 2}，{3，4}}
> **输出**：9
> **说明**：
> 在点{1、2}上绘制一条水平线和一条垂直线 和点{3,4}。
> 
> ```
>   _ _ _ _ _ 
> 5|_|_ _|_ _|
> 4| |   |3,4|
> 3|_|_ _|_ _| 
> 2| |1,2|   |
> 1|_|_ _|_ _|
>  0 1 2 3 4 5
> 
> ```
> 
> 因此，所需的输出为 9。
> 
> **输入**：矩形[] [] = {{0，0}，{4，0}，{0，5}，{4，5}}，points [] [] = {{1， 3}，{2、3}，{3、3}}。
> **输出**：12

**方法**：想法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并计算通过给定点[] []数组的所有不同水平和垂直线。 最后，返回**的乘积值（不同水平线的数量– 1）*（垂直线的数量– 1）**。 请按照以下步骤解决问题：

*   创建两个[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)，例如 **cntHor** ， **cntVer** ，以存储通过**点[] [] []** 数组的所有不同的水平线和垂直线 。
*   遍历 points [] []数组。
*   使用 **cntHor** 中的元素计数来计数所有不同的水平线。
*   使用 **cntVer** 中的元素计数来计数所有不同的垂直线。
*   最后，打印**的值（cntHor – 1 中的元素数）*（cntVer – 1 中的元素数）**。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the count 
// of ractangles 
int cntRect(int points[][2], int N,
             int rectangle[][2])
{
    // Store distinct
    // horizontal lines
    unordered_set<int> cntHor;   

    // Store distinct
    // Vertical lines
    unordered_set<int> cntVer;   

    // Insert horizontal line
    // passing through 0
    cntHor.insert(0);

    // Insert vertical line
    // passing through 0.
    cntVer.insert(0);

    // Insert horizontal line
    // passing through rectangle[3][0]
    cntHor.insert(rectangle[3][0]);

    // Insert vertical line
    // passing through rectangle[3][1]
    cntVer.insert(rectangle[3][1]);

    // Insert all horizontal and 
    // vertical lines passing through
    // the given array
    for (int i = 0; i < N; i++) {

        // Insert all horizontal lines
        cntHor.insert(points[i][0]);

        // Insert all vertical lines
        cntVer.insert(points[i][1]);
    }

    return (cntHor.size() - 1) * 
              (cntVer.size() - 1);
}

// Driver Code
int main()
{
    int rectangle[][2] = {{0, 0}, {0, 5},
                          {5, 0}, {5, 5}};
    int points[][2] = {{1, 2}, {3, 4}};

    int N = sizeof(points) / sizeof(points[0]);
    cout<<cntRect(points, N, rectangle);
}

```

## Java

```java

// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to get the count
// of ractangles
public static int cntRect(int points[][], int N,
                          int rectangle[][])
{

    // Store distinct
    // horizontal lines
    HashSet<Integer> cntHor = new HashSet<>();

    // Store distinct
    // Vertical lines
    HashSet<Integer> cntVer = new HashSet<>();

    // Insert horizontal line
    // passing through 0
    cntHor.add(0);

    // Insert vertical line
    // passing through 0.
    cntVer.add(0);

    // Insert horizontal line
    // passing through rectangle[3][0]
    cntHor.add(rectangle[3][0]);

    // Insert vertical line
    // passing through rectangle[3][1]
    cntVer.add(rectangle[3][1]);

    // Insert all horizontal and
    // vertical lines passing through
    // the given array
    for(int i = 0; i < N; i++)
    {

        // Insert all horizontal lines
        cntHor.add(points[i][0]);

        // Insert all vertical lines
        cntVer.add(points[i][1]);
    }
    return (cntHor.size() - 1) *
           (cntVer.size() - 1);
}

// Driver Code
public static void main(String args[])
{
    int rectangle[][] = { { 0, 0 }, { 0, 5 },
                          { 5, 0 }, { 5, 5 } };
    int points[][] = { { 1, 2 }, { 3, 4 } };

    int N = points.length;

    System.out.println(cntRect(points, N, 
                               rectangle));
}
}

// This code is contributed by hemanth gadarla

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to get the count 
# of ractangles 
def cntRect(points, N,
            rectangle):

    # Store distinct
    # horizontal lines
    cntHor = set([])  

    # Store distinct
    # Vertical lines
    cntVer = set([])

    # Insert horizontal line
    # passing through 0
    cntHor.add(0)

    # Insert vertical line
    # passing through 0.
    cntVer.add(0)

    # Insert horizontal line
    # passing through rectangle[3][0]
    cntHor.add(rectangle[3][0])

    # Insert vertical line
    # passing through rectangle[3][1]
    cntVer.add(rectangle[3][1])

    # Insert all horizontal and 
    # vertical lines passing through
    # the given array
    for i in range (N):

        # Insert all horizontal lines
        cntHor.add(points[i][0])

        # Insert all vertical lines
        cntVer.add(points[i][1])

    return ((len(cntHor) - 1) *
            (len(cntVer) - 1))

# Driver Code
if __name__ == "__main__":

    rectangle = [[0, 0], [0, 5],
                 [5, 0], [5, 5]]
    points = [[1, 2], [3, 4]]    
    N = len(points)
    print (cntRect(points, N, rectangle))

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to get the count
// of ractangles
public static int cntRect(int [,]points, 
                          int N, int [,]rectangle)
{
  // Store distinct
  // horizontal lines
  HashSet<int> cntHor = new HashSet<int>();

  // Store distinct
  // Vertical lines
  HashSet<int> cntVer = new HashSet<int>();

  // Insert horizontal line
  // passing through 0
  cntHor.Add(0);

  // Insert vertical line
  // passing through 0.
  cntVer.Add(0);

  // Insert horizontal line
  // passing through rectangle[3,0]
  cntHor.Add(rectangle[3, 0]);

  // Insert vertical line
  // passing through rectangle[3,1]
  cntVer.Add(rectangle[3, 1]);

  // Insert all horizontal and
  // vertical lines passing through
  // the given array
  for(int i = 0; i < N; i++)
  {
    // Insert all horizontal lines
    cntHor.Add(points[i, 0]);

    // Insert all vertical lines
    cntVer.Add(points[i, 1]);
  }
  return (cntHor.Count - 1) *
         (cntVer.Count - 1);
}

// Driver Code
public static void Main(String []args)
{
  int [,]rectangle = {{0, 0}, {0, 5},
                      {5, 0}, {5, 5}};
  int [,]points = {{1, 2}, {3, 4}};
  int N = points.GetLength(0);
  Console.WriteLine(cntRect(points, N, 
                            rectangle));
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
9

```

***时间复杂度**：O（N）*
***辅助空间**：O（N）*



* * *

* * *



