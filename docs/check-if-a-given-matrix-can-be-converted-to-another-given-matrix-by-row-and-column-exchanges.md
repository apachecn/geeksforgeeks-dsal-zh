# 检查给定矩阵是否可以通过行和列交换转换成另一个给定矩阵

> 原文:[https://www . geeksforgeeks . org/check-if-给定矩阵-可以按行和列转换为另一个给定矩阵-exchange/](https://www.geeksforgeeks.org/check-if-a-given-matrix-can-be-converted-to-another-given-matrix-by-row-and-column-exchanges/)

给定一个矩阵 **startMatrix** 和另一个矩阵 **finalMatrix** ，任务是检查 **startMatrix** 是否可以通过列交换和行交换转换为 **finalMatrix** 。

**示例:**

> **输入:**开始[][] = {{1，2，3，4}，
> {5，6，7，8}
> {9，10，11，12}，
> {13，14，15，16}}
> 最终[][] = {{1，4，3，2}，
> {5，8，7，6}，
> {13，16，15，14}，
> {9，12
> 
> **输入:**开始[][] = {{1，2，3，4}，
> {5，6，7，8}
> {9，10，11，12}，
> {13，14，15，16}}
> 最终[][] = {{1，4，3，2}，
> {5，6，7，8}，
> {13，16，15，14}，
> {9，12

**方法:**
为了解决这个问题，我们只需要检查 **startMatrix** 中所有行和列中的元素是否保留在 **finalMatrix** 矩阵中，而不管它们的顺序如何。任何违反此条件的行为都将确保无法获得**最终矩阵**矩阵。遍历每一行的循环，检查该行在**开始矩阵**中的所有元素是否在**结束矩阵**中的一行中。然后转置**开始矩阵**和**结束矩阵**并重复相同的验证。

下面的代码是上述方法的实现:

## C++

```
// CPP program to check if a
// given matrix can be converted
// to another given matrix by row
// and column exchanges
#include <bits/stdc++.h>
using namespace std;

// Function to get transpose of a matrix
vector<vector<int>> getTranspose(vector<vector<int>> matrix)
{
  int n = matrix.size();
  vector<vector<int>> transpose(n, vector<int>(n));
  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < n; j++)
    {
      transpose[j][i] = matrix[i][j];
    }
  }
  return transpose;
}

// Function to check for row preservation
bool rowEquality(vector<vector<int>> s,
                 vector<vector<int>> f)
{
  vector<set<int>> sets, setf;
  unordered_map<int, int> map;

  // Creating sets from the initial matrix
  for (int i = 0; i < s.size(); i++)
  {

    // Create set for corresponding row
    set<int> sett;

    // Add first element to the set
    sett.insert(s[i][0]);
    sets.push_back(sett);

    // Store the row number in map
    map[s[i][0]] = i;

    // Add remaining elements to the set
    for (int j = 1; j < s.size(); j++)
    {
      sett.insert(s[i][j]);
    }
  }

  // Create sets for final matrix
  // and check with the initial matrix
  int rowIndex = -1;
  for (int i = 0; i < f.size(); i++)
  {
    rowIndex = -1;
    set<int> sett;

    for (int j = 0; j < f.size(); j++)
    {
      sett.insert(f[i][j]);
      if (map.find(f[i][j]) != map.end())
      {
        rowIndex = map[f[i][j]];
      }
    }

    setf.push_back(sett);
    if (setf[i] != sets[rowIndex])
      return true;
  }

  return false;
}

// Driver code
int main()
{
  vector<vector<int>> startMatrix = {
      {1, 2, 3, 4},
      {5, 6, 7, 8},
      {9, 10, 11, 12},
      {13, 14, 15, 16}
  };
  vector<vector<int>> finalMatrix = {
      {3, 4, 1, 2},
      {15, 16, 13, 14},
      {7, 8, 5, 6},
      {11, 12, 9, 10}
  };

  vector<vector<int>> startTranspose = getTranspose(startMatrix);
  vector<vector<int>> finalTranspose = getTranspose(finalMatrix);

  if (rowEquality(startMatrix, finalMatrix) &&
      rowEquality(startTranspose, finalTranspose))
    cout << "Yes" << endl;
  else
    cout << "No" << endl;
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// given matrix can be converted
// to another given matrix by row
// and column exchanges

import java.util.*;
public class Solution{

    // Function to get transpose of a matrix
    static int[][] getTranspose(int[][] matrix){
        int n = matrix.length;
        int[][] transpose = new int[n][n];
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                transpose[j][i] = matrix[i][j];
            }
        }
        return transpose;
    }

    // Function to check for row preservation
    static boolean rowEquality(int[][] s, int[][] f){
        ArrayList<Set<Integer>> sets = new ArrayList<>();
        ArrayList<Set<Integer>> setf = new ArrayList<>();
        HashMap<Integer,Integer> map = new HashMap<>();

        // Creating sets from the initial matrix
        for(int i=0; i<s.length; i++){   
            // Create set for corresponding row
            Set<Integer> set = new HashSet<Integer>();
            // Add first element to the set
            set.add(s[i][0]);
            sets.add(set);
            // Store the row number in map
            map.put(s[i][0], i);
            // Add remaining elements to the set
            for(int j=1; j<s.length; j++){
                set.add(s[i][j]);
            }
        }

        // Create sets for final matrix
        // and check with the initial matrix
        int rowIndex = -1;
        for(int i=0; i<f.length; i++){

            rowIndex = -1;
            Set<Integer> set = new HashSet<Integer>();

            for(int j=0; j<f.length; j++){
                set.add(f[i][j]);
                if(map.containsKey(f[i][j])){
                    rowIndex = map.get(f[i][j]);
                }

            }

            setf.add(set);
            if(rowIndex != -1 && !setf.get(i).equals(
                               sets.get(rowIndex)))
                return false;
        }

        return true;

    }

    // Driver code
    public static void main(String []args){

        int[][] startMatrix = {{ 1, 2, 3, 4 },
                               { 5, 6, 7, 8 },
                               { 9, 10, 11, 12 },
                               { 13, 14, 15, 16 }};
        int[][] finalMatrix = {{ 3, 4, 1, 2 },
                               { 15, 16, 13, 14 },
                               { 7, 8, 5, 6 },
                               { 11, 12, 9, 10 }};

        int[][] startTranspose = getTranspose(startMatrix);
        int[][] finalTranspose = getTranspose(finalMatrix);

        if(rowEquality(startMatrix,finalMatrix) &&
           rowEquality(startTranspose,finalTranspose))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}
```

## 蟒蛇 3

```
# Python3 program to check if a
# given matrix can be converted
# to another given matrix by row
# and column exchanges

# Function to get transpose of a matrix
def getTranspose(matrix):
    n = len(matrix)
    transpose = [[0 for i in range(n)] for j in range(n)]
    for i in range(n):
        for j in range(n):
            transpose[j][i] = matrix[i][j]
    return transpose

# Function to check for row preservation
def rowEquality(s, f):
    sets = []
    setf = []
    mp = {i : 0 for i in range(100)}

    # Creating sets from the initial matrix
    for i in range(len(s)):

        # Create set for corresponding row
        st = set()

        # Add first element to the set
        st.add(s[i][0])
        sets.append(st)

        # Store the row number in mp
        mp[s[i][0]] = i

        # Add remaining elements to the set
        for j in range(1, len(s)):
            st.add(s[i][j])

    # Create sets for final matrix
    # and check with the initial matrix
    rowIndex = -1
    for i in range(len(f)):
        rowIndex = -1;
        st1 = set()

        for j in range(len(f)):
            st1.add(f[i][j])
            if(f[i][j] in mp):
                rowIndex = mp[f[i][j]]

        setf.append(st1)
        if(rowIndex != -1 and setf[i] !=
           sets[rowIndex]):
            return True

    return False

#Driver code
if __name__ == '__main__':
    startMatrix = [[ 1, 2, 3, 4 ],
                    [ 5, 6, 7, 8 ],
                    [ 9, 10, 11, 12 ],
                    [ 13, 14, 15, 16 ]]
    finalMatrix = [[ 3, 4, 1, 2],
                        [ 15, 16, 13, 14 ],
                        [ 7, 8, 5, 6 ],
                        [ 11, 12, 9, 10 ]]

    startTranspose = getTranspose(startMatrix)
    finalTranspose = getTranspose(finalMatrix)

    if(rowEquality(startMatrix, finalMatrix) and
       rowEquality(startTranspose, finalTranspose)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Samarth
```

## C#

```
// C# program to check if a
// given matrix can be converted
// to another given matrix by row
// and column exchanges
using System;
using System.Collections.Generic;

class GFG{

// Function to get transpose of a matrix
static int[,] getTranspose(int[,] matrix)
{
    int n = matrix.GetLength(0);
    int[,] transpose = new int[n, n];

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            transpose[j, i] = matrix[i, j];
        }
    }
    return transpose;
}

// Function to check for row preservation
static bool rowEquality(int[,] s, int[,] f)
{
    List<HashSet<int>> sets = new List<HashSet<int>>();
    List<HashSet<int>> setf = new List<HashSet<int>>();

    Dictionary<int,
               int> map = new Dictionary<int,
                                         int>();

    // Creating sets from the initial matrix
    for(int i = 0; i < s.GetLength(0); i++)
    {

        // Create set for corresponding row
        HashSet<int> set = new HashSet<int>();

        // Add first element to the set
        set.Add(s[i, 0]);
        sets.Add(set);

        // Store the row number in map
        map.Add(s[i, 0], i);

        // Add remaining elements to the set
        for(int j = 1; j < s.GetLength(1); j++)
        {
            set.Add(s[i, j]);
        }
    }

    // Create sets for readonly matrix
    // and check with the initial matrix
    int rowIndex = -1;

    for(int i = 0; i < f.GetLength(0); i++)
    {
        rowIndex = -1;
        HashSet<int> set = new HashSet<int>();

        for(int j = 0; j < f.GetLength(1); j++)
        {
            set.Add(f[i, j]);
            if (map.ContainsKey(f[i, j]))
            {
                rowIndex = map[f[i, j]];
            }
        }

        setf.Add(set);
        if (rowIndex != -1 &&
           !setf[i].Equals(sets[rowIndex]))
            return true;
    }
    return false;

}

// Driver code
public static void Main(String []args)
{
    int[,] startMatrix = { { 1, 2, 3, 4 },
                           { 5, 6, 7, 8 },
                           { 9, 10, 11, 12 },
                           { 13, 14, 15, 16 } };
    int[,] finalMatrix = { { 3, 4, 1, 2 },
                           { 15, 16, 13, 14 },
                           { 7, 8, 5, 6 },
                           { 11, 12, 9, 10 } };

    int[,] startTranspose = getTranspose(startMatrix);
    int[,] finalTranspose = getTranspose(finalMatrix);

    if (rowEquality(startMatrix,finalMatrix) &&
        rowEquality(startTranspose,finalTranspose))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
Yes
```