# 在只向下或向右移动的矩阵中打印从给定源到目的地的所有唯一路径

> 原文:[https://www . geesforgeks . org/print-all-unique-path-从给定源到矩阵中的目标-仅向下或向右移动/](https://www.geeksforgeeks.org/print-all-unique-paths-from-given-source-to-destination-in-a-matrix-moving-only-down-or-right/)

给定一个[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **mat[][]** 、一个源“ **s** 和一个目的地“ **d** ”，打印从给定的“ **s** ”到“ **d** 的所有唯一路径。从每个单元格中，您可以只向右或向下移动。

**示例:**

> **输入:** mat[][] = {{1，2，3}，{4，5，6}}，s[] = {0，0}，d[]={1，2}
> **输出:**
> 1 4 5 6
> 1 2 5 6
> 1 2 3 6
> 
> **输入** : mat[][] = {{1，2}，{3，4}}，s[] = {0，1}，d[] = {1，1}
> **输出:** 2 4

**方法:**使用[递归](http://www.geeksforgeeks.org/recursion/)从源开始，从矩阵路径中的每个单元格先右后下移动 **mat[][]** ，并将每个值存储在一个向量中。如果到达目的地，打印矢量作为可能的路径之一。按照以下步骤解决问题:

*   如果当前单元格超出边界，则返回。
*   将当前单元格的值推入向量**路径[]。**
*   如果当前单元格是目标，则打印当前路径。
*   对值 **{i+1，j}** 和 **{i，j+1}调用相同的函数。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

vector<vector<int> > mat;
vector<int> s;
vector<int> d;
int m = 2, n = 3;

// Function to print all the  paths
void printVector(vector<int> path)
{
    int cnt = path.size();
    for (int i = 0; i < cnt; i += 2)
        cout << mat[path[i]][path[i + 1]]
             << " ";
    cout << endl;
}

// Function to find all the paths recursively
void countPaths(int i, int j, vector<int> path)
{

    // Base Case
    if (i > d[0] || j > d[1])
        return;
    path.push_back(i);
    path.push_back(j);

    // Destination is reached
    if (i == d[0] && j == d[1]) {
        printVector(path);
        return;
    }

    // Calling the function
    countPaths(i, j + 1, path);
    countPaths(i + 1, j, path);
}

// DriverCode
int main()
{
    mat = { { 1, 2, 3 },
            { 4, 5, 6 } };
    s = { 0, 0 };
    d = { 1, 2 };
    vector<int> path;

    countPaths(s[0], s[1], path);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  static Vector<Integer> s = new Vector<>();
  static Vector<Integer> d = new Vector<>();
  static int m = 2, n = 3;

  // Function to print all the  paths
  static void printVector(Vector<Integer> path, int[][] mat)
  {
    int cnt = path.size();
    for (int i = 0; i < cnt; i += 2)
      System.out.print(mat[path.get(i)][path.get(i + 1)]+ " ");
    System.out.println();
  }

  // Function to find all the paths recursively
  static void countPaths(int i, int j, Vector<Integer> path, int[][]mat)
  {

    // Base Case
    if (i > d.get(0) || j > d.get(1))
      return;
    path.add(i);
    path.add(j);

    // Destination is reached
    if (i == d.get(0) && j == d.get(1)) {
      printVector(path,mat);
      path.remove(path.size()-1);
      path.remove(path.size()-1);
      return;
    }

    // Calling the function
    countPaths(i, j + 1, path,mat);
    countPaths(i + 1, j, path,mat);
    path.remove(path.size()-1);
    path.remove(path.size()-1);
  }

  // DriverCode
  public static void main(String[] args) {
    int[][] mat = {{ 1, 2, 3 },
                   { 4, 5, 6 } };
    s.add(0);
    s.add(0);
    d.add(1);
    d.add(2);
    Vector<Integer> path = new Vector<>();

    countPaths(s.get(0), s.get(1), path, mat);
  }
}

// This code is contributed by Rajput-Ji.
```

## 蟒蛇 3

```
# Python code for the above approach
mat = None
s = None
d = None
m = 2
n = 3

# Function to print all the  paths
def printVector(path):
    cnt = len(path)
    for i in range(0, cnt, 2):
        print(mat[path[i]][path[i + 1]], end=" ")

    print("")

# Function to find all the paths recursively
def countPaths(i, j, path):

    # Base Case
    if (i > d[0] or j > d[1]):
        return
    path.append(i)
    path.append(j)

    # Destination is reached
    if (i == d[0] and j == d[1]):
        printVector(path)
        path.pop()
        path.pop()
        return

    # Calling the function
    countPaths(i, j + 1, path)

    countPaths(i + 1, j, path)
    path.pop()
    path.pop()

# DriverCode
mat = [[1, 2, 3],
       [4, 5, 6]]
s = [0, 0]
d = [1, 2]
path = []

countPaths(s[0], s[1], path)

# This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach
       let mat;
       let s;
       let d;
       let m = 2, n = 3;

       // Function to print all the  paths
       function printVector(path) {
           let cnt = path.length;
           for (let i = 0; i < cnt; i += 2)
               document.write(mat[path[i]][path[i + 1]] + " ")

           document.write("<br>")
       }

       // Function to find all the paths recursively
       function countPaths(i, j, path)
       {

           // Base Case
           if (i > d[0] || j > d[1])
               return;
           path.push(i);
           path.push(j);

           // Destination is reached
           if (i == d[0] && j == d[1]) {
               printVector(path);
               path.pop();
               path.pop();
               return;
           }

           // Calling the function
           countPaths(i, j + 1, path);

           countPaths(i + 1, j, path);
           path.pop();
           path.pop();

       }

       // DriverCode
       mat = [[1, 2, 3],
       [4, 5, 6]];
       s = [0, 0];
       d = [1, 2];
       let path = [];

       countPaths(s[0], s[1], path);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
1 2 3 6 
1 2 5 6 
1 4 5 6
```

***时间复杂度:**O(2<sup>n+m</sup>)*
***辅助空间:** O(1)*