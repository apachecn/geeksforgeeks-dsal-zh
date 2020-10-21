# 查找二进制矩阵中是否有一个角为 1 的矩形

> 原文： [https://www.geeksforgeeks.org/find-rectangle-binary-matrix-corners-1/](https://www.geeksforgeeks.org/find-rectangle-binary-matrix-corners-1/)

有给定的二进制矩阵，我们需要查找给定矩阵中是否存在所有四个角均等于 1 的矩形或正方形。

**示例**：

```
Input :
mat[][] = { 1 0 0 1 0
            0 0 1 0 1
            0 0 0 1 0
            1 0 1 0 1}
Output : Yes
as there exists-
1 0 1
0 1 0
1 0 1

```



**暴力方法**：

每当我们在任意索引处找到 1 时，我们便开始扫描矩阵，然后尝试寻找所有可以形成矩形的索引组合。

算法-

```
for i = 1 to rows
  for j = 1 to columns
   if matrix[i][j] == 1
     for k=i+1 to rows
       for l=j+1 to columns
         if (matrix[i][k]==1 &&
             matrix[l][i]==1 &&
             m[l][k]==1)
                return true
return false

```

**时间复杂度**：`O(m ^ 2 * n ^ 2)`。

## C++ 

```cpp

// A brute force approach based CPP program to 
// find if there is a rectangle with 1 as corners. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns true if there is a rectangle with 
// 1 as corners. 
bool isRectangle(const vector<vector<int> >& m) 
{ 
    // finding row and column size 
    int rows = m.size(); 
    if (rows == 0) 
        return false; 
    int columns = m[0].size(); 

    // scanning the matrix 
    for (int y1 = 0; y1 < rows; y1++) 
        for (int x1 = 0; x1 < columns; x1++) 

            // if any index found 1 then try 
            // for all rectangles 
            if (m[y1][x1] == 1) 
                for (int y2 = y1 + 1; y2 < rows; y2++) 
                    for (int x2 = x1 + 1; x2 < columns; x2++) 
                        if (m[y1][x2] == 1 && m[y2][x1] == 1 && m[y2][x2] == 1) 
                            return true; 
    return false; 
} 

// Driver code 
int main() 
{ 
    vector<vector<int> > mat = { { 1, 0, 0, 1, 0 }, 
                                 { 0, 0, 1, 0, 1 }, 
                                 { 0, 0, 0, 1, 0 }, 
                                 { 1, 0, 1, 0, 1 } }; 
    if (isRectangle(mat)) 
        cout << "Yes"; 
    else
        cout << "No"; 
} 

```

## Java

```java

// A brute force approach based CPP program to 
// find if there is a rectangle with 1 as corners. 
public class FindRectangle { 
    // Returns true if there is a rectangle with 
    // 1 as corners. 
    static boolean isRectangle(int m[][]) 
    { 
        // finding row and column size 
        int rows = m.length; 
        if (rows == 0) 
            return false; 
        int columns = m[0].length; 

        // scanning the matrix 
        for (int y1 = 0; y1 < rows; y1++) 
            for (int x1 = 0; x1 < columns; x1++) 
                // if any index found 1 then try 
                // for all rectangles 
                if (m[y1][x1] == 1) 
                    for (int y2 = y1 + 1; y2 < rows; y2++) 
                        for (int x2 = x1 + 1; x2 < columns; x2++) 
                            if (m[y1][x2] == 1 && m[y2][x1] == 1 && m[y2][x2] == 1) 
                                return true; 
        return false; 
    } 

    public static void main(String args[]) 
    { 
        int mat[][] = { { 1, 0, 0, 1, 0 }, 
                        { 0, 0, 1, 0, 1 }, 
                        { 0, 0, 0, 1, 0 }, 
                        { 1, 0, 1, 0, 1 } }; 
        if (isRectangle(mat)) 
            System.out.print("Yes"); 
        else
            System.out.print("No"); 
    } 
} 
// This code is contributed by Gaurav Tiwari 

```

## Python3

```py

# A brute force approach based Python3 program to 
# find if there is a rectangle with 1 as corners. 

# Returns true if there is a rectangle  
# with 1 as corners. 
def isRectangle(m): 

    # finding row and column size 
    rows = len(m) 
    if (rows == 0): 
        return False
    columns = len(m[0]) 

    # scanning the matrix 
    for y1 in range(rows): 

        for x1 in range(columns): 

            # if any index found 1 then  
            # try for all rectangles 
            if (m[y1][x1] == 1): 
                for y2 in range(y1 + 1, rows): 
                    for x2 in range(x1 + 1, columns): 
                        if (m[y1][x2] == 1 and 
                            m[y2][x1] == 1 and 
                            m[y2][x2] == 1): 
                            return True
    return False

# Driver code 
mat = [[1, 0, 0, 1, 0], 
       [0, 0, 1, 0, 1], 
       [0, 0, 0, 1, 0], 
       [1, 0, 1, 0, 1]] 

if (isRectangle(mat)): 
    print("Yes") 
else: 
    print("No") 

# This code is conteibuted 
# by mohit kumar 29 

```

## C# 

```cs

// A brute force approach based C# program to 
// find if there is a rectangle with 1 as corners. 
using System; 

public class FindRectangle { 
    // Returns true if there is a rectangle with 
    // 1 as corners. 
    static Boolean isRectangle(int[, ] m) 
    { 
        // finding row and column size 
        int rows = m.GetLength(0); 
        if (rows == 0) 
            return false; 
        int columns = m.GetLength(1); 

        // scanning the matrix 
        for (int y1 = 0; y1 < rows; y1++) 
            for (int x1 = 0; x1 < columns; x1++) 

                // if any index found 1 then try 
                // for all rectangles 
                if (m[y1, x1] == 1) 
                    for (int y2 = y1 + 1; y2 < rows; y2++) 
                        for (int x2 = x1 + 1; x2 < columns; x2++) 
                            if (m[y1, x2] == 1 && m[y2, x1] == 1 && m[y2, x2] == 1) 
                                return true; 
        return false; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int[, ] mat = { { 1, 0, 0, 1, 0 }, 
                        { 0, 0, 1, 0, 1 }, 
                        { 0, 0, 0, 1, 0 }, 
                        { 1, 0, 1, 0, 1 } }; 
        if (isRectangle(mat)) 
            Console.Write("Yes"); 
        else
            Console.Write("No"); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Yes

```

**有效方法**：

+ 从上到下，逐行扫描

+ 对于每一行，请记住 01 的每种组合并将其推入哈希集

+ 如果我们在下一行中再次找到该组合，我们得到矩形

**时间复杂度**：`O(n * m ^ 2)`。

## C++

```

// An efficient approach based CPP program to 
// find if there is a rectangle with 1 as 
// corners. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns true if there is a rectangle with 
// 1 as corners. 
bool isRectangle(const vector<vector<int> >& matrix) 
{ 
    // finding row and column size 
    int rows = matrix.size(); 
    if (rows == 0) 
        return false; 

    int columns = matrix[0].size(); 

    // map for storing the index of combination of 2 1's 
    unordered_map<int, unordered_set<int> > table; 

    // scanning from top to bottom line by line 
    for (int i = 0; i < rows; ++i) { 

        for (int j = 0; j < columns - 1; ++j) { 
            for (int k = j + 1; k < columns; ++k) { 

                // if found two 1's in a column 
                if (matrix[i][j] == 1 && matrix[i][k] == 1) { 

                    // check if there exists 1's in same 
                    // row previously then return true 
                    // we don't need to check (j, k) pair 
                    // and again (k, j) pair because we always 
                    // store pair in ascending order and similarly 
                    // check in ascending order, i.e. j always less 
                    // than k. 
                    if (table.find(j) != table.end() 
                        && table[j].find(k) != table[j].end()) 
                        return true; 

                    // store the indexes in hashset 
                    table[j].insert(k); 
                } 
            } 
        } 
    } 
    return false; 
} 

// Driver code 
int main() 
{ 
    vector<vector<int> > mat = { { 1, 0, 0, 1, 0 }, 
                                 { 0, 1, 1, 1, 1 }, 
                                 { 0, 0, 0, 1, 0 }, 
                                 { 1, 1, 1, 1, 0 } }; 
    if (isRectangle(mat)) 
        cout << "Yes"; 
    else
        cout << "No"; 
} 
// This code is improved by Gautam Agrawal 

```

## Java

```
// An efficient approach based Java program to
// find if there is a rectangle with 1 as
// corners.
import java.util.HashMap;
import java.util.HashSet;
public class FindRectangle {
    // Returns true if there is a rectangle with
    // 1 as corners.
    static boolean isRectangle(int matrix[][])
    {
        // finding row and column size
        int rows = matrix.length;
        if (rows == 0)
            return false;
        int columns = matrix[0].length;
 
        // map for storing the index of combination of 2 1's
        HashMap<Integer, HashSet<Integer> > table = new HashMap<>();
 
        // scanning from top to bottom line by line
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns - 1; j++) {
                for (int k = j + 1; k < columns; k++) {
                    // if found two 1's in a column
                    if (matrix[i][j] == 1 && matrix[i][k] == 1) {
                        // check if there exists 1's in same
                        // row previously then return true
                        if (table.containsKey(j) && table.get(j).contains(k)) {
                            return true;
                        }
                        if (table.containsKey(k) && table.get(k).contains(j)) {
                            return true;
                        }
 
                        // store the indexes in hashset
                        if (!table.containsKey(j)) {
                            HashSet<Integer> x = new HashSet<>();
                            x.add(k);
                            table.put(j, x);
                        }
                        else {
                            table.get(j).add(k);
                        }
                        if (!table.containsKey(k)) {
                            HashSet<Integer> x = new HashSet<>();
                            x.add(j);
                            table.put(k, x);
                        }
                        else {
                            table.get(k).add(j);
                        }
                    }
                }
            }
        }
        return false;
    }
 
    public static void main(String args[])
    {
        int mat[][] = { { 1, 0, 0, 1, 0 },
                        { 0, 0, 1, 0, 1 },
                        { 0, 0, 0, 1, 0 },
                        { 1, 0, 1, 0, 1 } };
        if (isRectangle(mat))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
// This code is contributed by Gaurav Tiwari
```

## Python3

```
# An efficient approach based Python program 
# to find if there is a rectangle with 1 as 
# corners. 
 
# Returns true if there is a rectangle
# with 1 as corners. 
def isRectangle(matrix):
 
    # finding row and column size 
    rows = len(matrix)
    if (rows == 0):
        return False
 
    columns = len(matrix[0])
 
    # map for storing the index of 
    # combination of 2 1's 
    table = {}
 
    # scanning from top to bottom 
    # line by line 
    for i in range(rows): 
        for j in range(columns - 1):
            for k in range(j + 1, columns): 
 
                # if found two 1's in a column 
                if (matrix[i][j] == 1 and
                    matrix[i][k] == 1):
 
                    # check if there exists 1's in same 
                    # row previously then return true 
                    if (j in table and k in table[j]):
                        return True
 
                    if (k in table and j in table[k]):
                        return True
 
                    # store the indexes in hashset 
                    if j not in table:
                        table[j] = set()
                    if k not in table:
                        table[k] = set()
                    table[j].add(k) 
                    table[k].add(j)
    return False
 
# Driver Code
if __name__ == '__main__':
    mat = [[ 1, 0, 0, 1, 0 ],
           [ 0, 0, 1, 0, 1 ],
           [ 0, 0, 0, 1, 0 ],
           [ 1, 0, 1, 0, 1 ]] 
    if (isRectangle(mat)):
        print("Yes")
    else:
        print("No")
     
# This code is contributed 
# by SHUBHAMSINGH10
```

## C#

```
// An efficient approach based C# program to
// find if there is a rectangle with 1 as
// corners.
using System;
using System.Collections.Generic;
 
public class FindRectangle {
    // Returns true if there is a rectangle with
    // 1 as corners.
    static bool isRectangle(int[, ] matrix)
    {
        // finding row and column size
        int rows = matrix.GetLength(0);
        if (rows == 0)
            return false;
        int columns = matrix.GetLength(1);
 
        // map for storing the index of combination of 2 1's
        Dictionary<int, HashSet<int> > table = new Dictionary<int, HashSet<int> >();
 
        // scanning from top to bottom line by line
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns - 1; j++) {
                for (int k = j + 1; k < columns; k++) {
                    // if found two 1's in a column
                    if (matrix[i, j] == 1 && matrix[i, k] == 1) {
                        // check if there exists 1's in same
                        // row previously then return true
                        if (table.ContainsKey(j) && table[j].Contains(k)) {
                            return true;
                        }
                        if (table.ContainsKey(k) && table[k].Contains(j)) {
                            return true;
                        }
 
                        // store the indexes in hashset
                        if (!table.ContainsKey(j)) {
                            HashSet<int> x = new HashSet<int>();
                            x.Add(k);
                            table.Add(j, x);
                        }
                        else {
                            table[j].Add(k);
                        }
                        if (!table.ContainsKey(k)) {
                            HashSet<int> x = new HashSet<int>();
                            x.Add(j);
                            table.Add(k, x);
                        }
                        else {
                            table[k].Add(j);
                        }
                    }
                }
            }
        }
        return false;
    }
 
    public static void Main(String[] args)
    {
        int[, ] mat = { { 1, 0, 0, 1, 0 },
                        { 0, 0, 1, 0, 1 },
                        { 0, 0, 0, 1, 0 },
                        { 1, 0, 1, 0, 1 } };
        if (isRectangle(mat))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}
 
// This code is contributed by PrinciRaj1992
```

输出：

```
Yes
```

