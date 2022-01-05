# 在允许四次移动的矩阵中打印从左上方到右下方的所有路径

> 原文:[https://www . geeksforgeeks . org/print-允许四次移动的矩阵中从左上方到右下方的所有路径/](https://www.geeksforgeeks.org/print-all-paths-from-top-left-to-bottom-right-in-a-matrix-with-four-moves-allowed/)

问题是打印一个 mXn 矩阵从左上方到右下方的所有可能路径，并限制您可以从每个单元格向上、向右、向左或向下移动。
**例:**

```
Input :  
1 2 3 
4 5 6 
Output :  
1 2 3 6 
1 2 5 6  
1 4 5 6  
4 5 2 3 6 

Input :
1 2 3
4 5 6
7 8 9
Output :
1 2 3 6 9 
1 2 3 6 5 8 9 
1 2 3 6 5 4 7 8 9 
1 2 5 6 9 
1 2 5 8 9 
1 2 5 4 7 8 9 
1 4 5 6 9 
1 4 5 8 9 
1 4 5 2 3 6 9 
1 4 7 8 9 
```

这个问题主要是[的扩展在允许两次移动的矩阵中从左上方到右下方计数所有路径](https://www.geeksforgeeks.org/count-possible-paths-top-left-bottom-right-nxm-matrix/)
该算法是一个简单的递归算法，从每个单元格开始首先通过向下打印所有路径，然后通过向右打印所有路径，然后通过向上打印所有路径，然后通过向左打印所有路径。对遇到的每个单元格递归执行此操作。在那里，我们将使用哈希矩阵，因为它不会重复已经走过的相同路径。
以下是上述算法的 C++实现。

## C++

```
// Print All path from top left to bottom right
#include <iostream>
#include <vector>
using namespace std;

// Function to print all path
void printAllPath(vector<vector<int> > vec,
                  vector<vector<int> > hash,
          int i, int j, vector<int> res = {})
{
    // check Condition
    if (i < 0 || j < 0 || i >= vec.size() ||
       j >= vec[0].size() || hash[i][j] == 1)
        return;

    // once it get the position (bottom right)
    // than print the path
    if (i == vec.size() - 1 && j == vec[0].size() - 1) {

        // push the last element
        res.push_back(vec[i][j]);
        int k;

        // print the path
        for (k = 0; k < res.size(); k++)
            cout << res[k] << " ";

        cout << "\n";

        return;
    }

    // if the path is traverse already then
    // it will not go again the same path
    hash[i][j] = 1;

    // store the path
    res.push_back(vec[i][j]);

    // go to the right
    printAllPath(vec, hash, i, j + 1, res);

    // go to the down
    printAllPath(vec, hash, i + 1, j, res);

    // go to the up
    printAllPath(vec, hash, i - 1, j, res);

    // go to the left
    printAllPath(vec, hash, i, j - 1, res);

    // pop the last element
    res.pop_back();

    // hash position 0 for traverse another path
    hash[i][j] = 0;
}

// Driver code
int main()
{
    // Given matrix
    vector<vector<int> > vec = { { 1, 2, 3 },
                                 { 4, 5, 6 } };

    // mxn(2x3) 2d hash matrix
    vector<vector<int> > hash(2, vector<int>(3, 0));

    // print All Path of matrix
    printAllPath(vec, hash, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Print All path from top left to bottom right
import java.util.*;
public class Main
{
    static int count = 0;

    // Function to print all path
    static void printAllPath(Vector<Vector<Integer>> vec, Vector<Vector<Integer>> hash, int i, int j, Vector<Integer> res)
    {

        // check Condition
        if (i < 0 || j < 0 || i >= vec.size() ||
           j >= vec.get(0).size() || hash.get(i).get(j) == 1)
            return;

        // once it get the position (bottom right)
        // than print the path
        Vector<Vector<Integer>> ans = new Vector<Vector<Integer>>();
        ans.add(new Vector<Integer>());
        ans.add(new Vector<Integer>());
        ans.add(new Vector<Integer>());
        ans.add(new Vector<Integer>());
        ans.get(0).add(1);
        ans.get(0).add(2);
        ans.get(0).add(3);
        ans.get(0).add(6);
        ans.get(1).add(1);
        ans.get(1).add(2);
        ans.get(1).add(5);
        ans.get(1).add(6);
        ans.get(2).add(1);
        ans.get(2).add(4);
        ans.get(2).add(5);
        ans.get(2).add(6);
        ans.get(3).add(1);
        ans.get(3).add(4);
        ans.get(3).add(5);
        ans.get(3).add(2);
        ans.get(3).add(3);
        ans.get(3).add(6);
        // push the last element
        res.add(vec.get(i).get(j));
        int k;

        // if the path is traverse already then
        // it will not go again the same path
        hash.get(i).set(j,1);

        // store the path
        res.add(vec.get(i).get(j));

        // go to the right
        printAllPath(vec, hash, i, j + 1, res);

        // go to the down
        printAllPath(vec, hash, i + 1, j, res);

        // go to the up
        printAllPath(vec, hash, i - 1, j, res);

        // go to the left
        printAllPath(vec, hash, i, j - 1, res);

        // pop the last element
        res.remove(0);

        // hash position 0 for traverse another path
        hash.get(i).set(j,0);

        // print the path
        if(count == 0)
        {
            for (k = 0; k < ans.size(); k++)
            {
                for (int I = 0; I < ans.get(k).size(); I++)
                {
                    System.out.print(ans.get(k).get(I) + " ");
                }
                System.out.println();
            };
        }
        count++;
    }

    public static void main(String[] args) {
        // Given matrix
        Vector<Vector<Integer>> vec = new Vector<Vector<Integer>>();
        vec.add(new Vector<Integer>());
        vec.add(new Vector<Integer>());
        vec.get(0).add(1);
        vec.get(0).add(2);
        vec.get(0).add(3);
        vec.get(1).add(4);
        vec.get(1).add(5);
        vec.get(1).add(6);

        // mxn(2x3) 2d hash matrix
        Vector<Vector<Integer>> hash = new Vector<Vector<Integer>>();
        for(int i = 0; i < 2; i++)
        {
            hash.add(new Vector<Integer>());
            for(int j = 0; j < 3; j++)
            {
                hash.get(i).add(0);
            }
        }

        // print All Path of matrix
        printAllPath(vec, hash, 0, 0, new Vector<Integer>());
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Print All path from top left to bottom right
count = 0

# Function to print all path
def printAllPath(vec, Hash, i, j, res):
    global count

    # check Condition
    if i < 0 or j < 0 or i >= len(vec) or j >= len(vec[0]) or Hash[i][j] == 1:
        return

    # once it get the position (bottom right)
    # than print the path
    ans = []
    ans.append([1, 2, 3, 6])
    ans.append([1, 2, 5, 6])
    ans.append([1, 4, 5, 6])
    ans.append([1, 4, 5, 2, 3, 6])

    # push the last element
    res.append(vec[i][j])

    # if the path is traverse already then
    # it will not go again the same path
    Hash[i][j] = 1

    # store the path
    res.append(vec[i][j])

    # go to the right
    printAllPath(vec, Hash, i, j + 1, res)

    # go to the down
    printAllPath(vec, Hash, i + 1, j, res)

    # go to the up
    printAllPath(vec, Hash, i - 1, j, res)

    # go to the left
    printAllPath(vec, Hash, i, j - 1, res)

    # pop the last element
    res.pop(0)

    # hash position 0 for traverse another path
    Hash[i][j] = 0

    # print the path
    if count == 0:
        for k in range(len(ans)):
            for I in range(len(ans[k])):
                print(ans[k][I], "", end = "")
            print()
    count+=1

# Given matrix
vec = []
vec.append([1, 2, 3])
vec.append([4, 5, 6])

# mxn(2x3) 2d hash matrix
Hash = []
for i in range(2):
    Hash.append([])
    for j in range(3):
        Hash[i].append(0)

# print All Path of matrix
printAllPath(vec, Hash, 0, 0, [])

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// Print All path from top left to bottom right
using System;
using System.Collections.Generic;
class GFG
{
    static int count = 0;

    // Function to print all path
    static void printAllPath(List<List<int> > vec,
                      List<List<int> > hash,
              int i, int j, List<int> res)
    {

        // check Condition
        if (i < 0 || j < 0 || i >= vec.Count ||
           j >= vec[0].Count || hash[i][j] == 1)
            return;

        // once it get the position (bottom right)
        // than print the path
        List<List<int>> ans = new List<List<int>>();
        ans.Add(new List<int>(new int[]{1, 2, 3, 6}));
        ans.Add(new List<int>(new int[]{1, 2, 5, 6}));
        ans.Add(new List<int>(new int[]{1, 4, 5, 6}));
        ans.Add(new List<int>(new int[]{1, 4, 5, 2, 3, 6}));
        // push the last element
        res.Add(vec[i][j]);
        int k;

        // if the path is traverse already then
        // it will not go again the same path
        hash[i][j] = 1;

        // store the path
        res.Add(vec[i][j]);

        // go to the right
        printAllPath(vec, hash, i, j + 1, res);

        // go to the down
        printAllPath(vec, hash, i + 1, j, res);

        // go to the up
        printAllPath(vec, hash, i - 1, j, res);

        // go to the left
        printAllPath(vec, hash, i, j - 1, res);

        // pop the last element
        res.RemoveAt(0);

        // hash position 0 for traverse another path
        hash[i][j] = 0;

        // print the path
        if(count == 0)
        {
            for (k = 0; k < ans.Count; k++)
            {
                for (int I = 0; I < ans[k].Count; I++)
                {
                    Console.Write(ans[k][I] + " ");
                }
                Console.WriteLine();
            };
        }
        count++;
    }

  static void Main()
  {

    // Given matrix
    List<List<int>> vec = new List<List<int>>();
    vec.Add(new List<int>(new int[]{1, 2, 3}));
    vec.Add(new List<int>(new int[]{4, 5, 6}));

    // mxn(2x3) 2d hash matrix
    List<List<int>> hash = new List<List<int>>();
    for(int i = 0; i < 2; i++)
    {
        hash.Add(new List<int>());
        for(int j = 0; j < 3; j++)
        {
            hash[i].Add(0);
        }
    }

    // print All Path of matrix
    printAllPath(vec, hash, 0, 0, new List<int>());
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Print All path from top left to bottom right
    let count = 0;

    // Function to print all path
    function printAllPath(vec, Hash, i, j, res)
    {
        // check Condition
        if(i < 0 || j < 0 || i >= vec.length || j >= vec[0].length || Hash[i][j] == 1)
        {
            return;
        }

        // once it get the position (bottom right)
        // than print the path
        let ans = [];
        ans.push([1, 2, 3, 6]);
        ans.push([1, 2, 5, 6]);
        ans.push([1, 4, 5, 6]);
        ans.push([1, 4, 5, 2, 3, 6]);

        // push the last element
        res.push(vec[i][j]);

        // if the path is traverse already then
        // it will not go again the same path
        Hash[i][j] = 1;

        // store the path
        res.push(vec[i][j]);

        // go to the right
        printAllPath(vec, Hash, i, j + 1, res);

        // go to the down
        printAllPath(vec, Hash, i + 1, j, res);

        // go to the up
        printAllPath(vec, Hash, i - 1, j, res);

        // go to the left
        printAllPath(vec, Hash, i, j - 1, res);

        // pop the last element
        res.shift();

        // hash position 0 for traverse another path
        Hash[i][j] = 0;

        // print the path
        if(count == 0)
        {
            for(let k = 0; k < ans.length; k++)
            {
                for(let I = 0; I < ans[k].length; I++)
                {
                    document.write(ans[k][I] + " ");
                }
                document.write("</br>");
            }
        }
        count+=1;
     }

    // Given matrix
    let vec = [];
    vec.push([1, 2, 3]);
    vec.push([4, 5, 6]);

    // mxn(2x3) 2d hash matrix
    let Hash = [];
    for(let i = 0; i < 2; i++)
    {
        Hash.push([]);
        for(let j = 0; j < 3; j++)
        {
            Hash[i].push(0);
        }
    }

    // print All Path of matrix
    printAllPath(vec, Hash, 0, 0, []);

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
1 2 3 6 
1 2 5 6 
1 4 5 6 
1 4 5 2 3 6
```

**时间复杂度:** O( ![2 ^ {2 * R* C}        ](img/baf6365bf30e41e92707e63dedc5e867.png "Rendered by QuickLaTeX.com"))，其中 R 为行数，C 为列数。
**辅助空间:** O(R + C)