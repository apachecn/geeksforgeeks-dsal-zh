# 检查任意一对半圆是否相交

> 原文:[https://www . geesforgeks . org/check-if-any-pair-of-半圆-intersect-or-not/](https://www.geeksforgeeks.org/check-if-any-pair-of-semicircles-intersect-or-not/)

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，使得每对点 **(x，y)** 将半圆的端点表示为 **(x，0)** 和 **(y，0)** ，任务是检查是否有任何一对半圆相交。如果发现**为真**，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {0，15，5，10}
> **输出:**否
> 
> **输入:** arr[] = {0，10，5，15 }
> T3】输出:是

**方法:**给定的问题可以通过检查任意一对半圆是否相交，然后相应地打印元素来解决。按照以下步骤解决问题:

*   将所有可能的半圆存储在一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，它们对应的是 **x 坐标**和 **y 坐标**。
*   现在，[生成所有可能的上述向量对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并执行以下步骤:
    *   让这对坐标为 **X** 和 **Y** ，使用以下条件检查圆是否相交:
        *   如果 **(X[0] < Y[0]** 、 **X[1] < Y[1]** 、 **Y[0] < X[2])** 或 **(Y[0] < X[0]** 、 **Y[1] < X[1]** 、 **X[0] < Y[1])** 否则，不会相交。
        *   如果以上两个圆相交，则打印**“是”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成以上步骤后，如果任意一对圆不相交，则打印**“否”**。

## C++

```
// C++ program for the above approach

#include <iostream>
#include <vector>
using namespace std;

// Function to check if any pairs of
// the semicircles intersects or not
bool checkIntersection(int arr[], int N)
{

    // Stores the coordinates of all
    // the semicircles
    vector<pair<int, int> > vec;

    for (int i = 0; i < N - 1; i++) {

        // x and y are coordinates
        int x = arr[i], y = arr[i + 1];

        // Store the minimum and maximum
        // value of the pair
        int minn = min(x, y);
        int maxx = max(x, y);

        // Push the pair in vector
        vec.push_back({ minn, maxx });
    }

    // Compare one pair with other pairs
    for (int i = 0; i < vec.size(); i++) {

        pair<int, int> x = vec[i];

        // Generating the second pair
        for (int j = 0;
             j < vec.size(); j++) {

            // Extract all the second
            // pairs one by one
            pair<int, int> y = vec[j];

            // 1st condition
            bool cond1
                = (x.first < y.first
                   and x.second < y.second
                   and y.first < x.second);

            // 2nd condition
            bool cond2
                = (y.first < x.first
                   and y.second < x.second
                   and x.first < y.second);

            // If any one condition
            // is true
            if (cond1 or cond2) {
                return true;
            }
        }
    }

    // If any pair of semicircles
    // doesn't exists
    return false;
}

// Driver Code
int main()
{
    int arr[] = { 0, 15, 5, 10 };
    int N = sizeof(arr) / sizeof(int);

    if (checkIntersection(arr, N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to check if any pairs of
// the semicircles intersects or not
static boolean checkIntersection(int arr[], int N)
{

    // Stores the coordinates of all
    // the semicircles
    Vector<pair > vec = new Vector<>();

    for(int i = 0; i < N - 1; i++)
    {

        // x and y are coordinates
        int x = arr[i], y = arr[i + 1];

        // Store the minimum and maximum
        // value of the pair
        int minn = Math.min(x, y);
        int maxx = Math.max(x, y);

        // Push the pair in vector
        vec.add(new pair( minn, maxx ));
    }

    // Compare one pair with other pairs
    for(int i = 0; i < vec.size(); i++)
    {
        pair x = vec.elementAt(i);

        // Generating the second pair
        for(int j = 0;
                j < vec.size(); j++)
        {

            // Extract all the second
            // pairs one by one
            pair y = vec.elementAt(j);

            // 1st condition
            boolean cond1 = (x.first < y.first &&
                            x.second < y.second &&
                             y.first < x.second);

            // 2nd condition
            boolean cond2 = (y.first < x.first &&
                            y.second < x.second &&
                             x.first < y.second);

            // If any one condition
            // is true
            if (cond1 || cond2)
            {
                return true;
            }
        }
    }

    // If any pair of semicircles
    // doesn't exists
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 0, 15, 5, 10 };
    int N = arr.length;

    if (checkIntersection(arr, N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if any pairs of
# the semicircles intersects or not
def checkIntersection(arr, N):

    # Stores the coordinates of all
    # the semicircles
    vec = []

    for i in range(N - 1):

        # x and y are coordinates
        x = arr[i]
        y = arr[i + 1]

        # Store the minimum and maximum
        # value of the pair
        minn = min(x, y)
        maxx = max(x, y)

        # Push the pair in vector
        vec.append([minn, maxx])

    # Compare one pair with other pairs
    for i in range(len(vec)):
        x = vec[i]

        # Generating the second pair
        for j in range(len(vec)):

            # Extract all the second
            # pairs one by one
            y = vec[j]

            # 1st condition
            cond1 = (x[0] < y[0] and
                     x[1] < y[1] and
                     y[0] < x[1])

            # 2nd condition
            cond2 = (y[0] < x[0] and
                     y[1] < x[1] and
                     x[0] < y[1])

            # If any one condition
            # is true
            if (cond1 or cond2):
                return True

    # If any pair of semicircles
    # doesn't exists
    return False

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 15, 5, 10 ]
    N = len(arr)

    if (checkIntersection(arr, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

class pair
{
    public int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to check if any pairs of
// the semicircles intersects or not
static bool checkIntersection(int []arr, int N)
{

    // Stores the coordinates of all
    // the semicircles
    List<pair > vec = new List<pair>();

    for(int i = 0; i < N - 1; i++)
    {

        // x and y are coordinates
        int x = arr[i], y = arr[i + 1];

        // Store the minimum and maximum
        // value of the pair
        int minn = Math.Min(x, y);
        int maxx = Math.Max(x, y);

        // Push the pair in vector
        vec.Add(new pair( minn, maxx ));
    }

    // Compare one pair with other pairs
    for(int i = 0; i < vec.Count; i++)
    {
        pair x = vec[i];

        // Generating the second pair
        for(int j = 0;
                j < vec.Count; j++)
        {

            // Extract all the second
            // pairs one by one
            pair y = vec[j];

            // 1st condition
            bool cond1 = (x.first < y.first &&
                         x.second < y.second &&
                          y.first < x.second);

            // 2nd condition
            bool cond2 = (y.first < x.first &&
                         y.second < x.second &&
                          x.first < y.second);

            // If any one condition
            // is true
            if (cond1 || cond2)
            {
                return true;
            }
        }
    }

    // If any pair of semicircles
    // doesn't exists
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 0, 15, 5, 10 };
    int N = arr.Length;

    if (checkIntersection(arr, N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
No
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*