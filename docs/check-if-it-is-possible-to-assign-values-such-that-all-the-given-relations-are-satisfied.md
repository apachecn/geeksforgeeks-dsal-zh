# 检查是否可以赋值，以满足所有给定的关系

> 原文:[https://www . geeksforgeeks . org/check-如果可以赋值，那么所有给定的关系都得到满足/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-assign-values-such-that-all-the-given-relations-are-satisfied/)

给定一组字符串 **arr[]** ，其中每个 **arr[i]** 的形式为**“I = = j”**或**“I！=j"** ，其中 **i** 和 **j** 是表示它们之间关系的变量，任务是检查是否有可能给满足所有关系的变量赋值。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**arr[]= {“I = = j”，“j！=i"}
> **输出:**否
> **解释:**
> 第一个关系对于值 i = 1 和 j = 1 成立，但是第二个关系对于同一组值失败。因此，打印编号。
> 
> **输入:**arr[]= {“p = = q”、“q==r”、“p = = r”]
> **输出:**是
> **说明:**
> p、q、r 中值 1 的赋值满足全部 3 个关系。因此，打印“是”。

**方法:**解决给定问题的方法是使用[联合查找算法](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)。其思想是[遍历字符串数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，遍历每一个等式关系，对两个变量进行并运算。遍历之后，转到每个字符串中的每个非相等关系，检查两个变量的父变量是否相同。按照以下步骤解决问题:

1.  使用 **0** 和变量**将大小为 **26** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、**父[]** 初始化为**真**以存储所需结果。**
2.  [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **父[]** ，将**父[i]** 设置为 **i** 。
3.  现在，[遍历字符串数组中的每一个字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果**S【I】【1】**的值为 **'='** ，那么对**S【I】【0 –' a '】**和**S【I】【3 –' a '】**执行并集操作。
4.  再次，[遍历字符串数组中的每个字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下操作:
    1.  如果 **S[i][1]** 的值等于**'！'**，将**S[I][0 –' a '】**和**S[I][3 –' a '】**的父代分别存储在 **X** 和 **Y** 中。
    2.  如果 **X** 的值等于 **Y** ，则将**答案**设置为**假**。
5.  经过上述步骤后，如果**答案**的值为**真**，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find parent of each node
int find(int v, vector<int>& parent)
{
    // If parent[v] is not v, then
    // recursively call to find the
    // parent of parent[v]
    if (parent[v] != v)
        return parent[v] = find(parent[v],
                                parent);

    // Otherwise, return v
    return v;
}

// Function to perform union of the
// two variables
void unions(int a, int b,
            vector<int>& parent)
{
    // Stores the parent of a and b
    int x = find(a, parent);
    int y = find(b, parent);

    // If they are not equal, make
    // parent[x] = parent[y]
    if (x != y)
        parent[x] = parent[y];
}

// Function to check whether it is
// possible to assign values to
// variables to satisfy relations
bool equationsPossible(
    vector<string>& relations)
{
    // Initialize parent array as 0s
    vector<int> parent(26, 0);

    // Iterate in range [0, 25]
    // and make parent[i] = i
    for (int i = 0; i < 26; i++) {
        parent[i] = i;
    }

    // Store the size of the string
    int n = relations.size();

    // Traverse the string
    for (auto string : relations) {

        // Check if it is of the
        // form "i==j" or not
        if (string[1] == '=')

            // Take union of both
            // the variables
            unions(string[0] - 'a',
                   string[3] - 'a',
                   parent);
    }

    // Traverse the string
    for (auto string : relations) {

        // Check if it is of the
        // form "i!=j" or not
        if (string[1] == '!') {

            // Store the parent of
            // i and j
            int x = find(string[0] - 'a',
                         parent);
            int y = find(string[3] - 'a',
                         parent);

            // If they are equal,
            // then return false
            if (x == y)
                return false;
        }
    }

    return true;
}

// Driver Code
int main()
{
    vector<string> relations
        = { "i==j", "j!=i" };

    if (equationsPossible(relations)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find parent of each node
static int find(int v, ArrayList<Integer> parent)
{

    // If parent[v] is not v, then
    // recursively call to find the
    // parent of parent[v]
    if (parent.get(v) != v)
    {
        parent.set(v, find(parent.get(v), parent));
        return parent.get(v);
    }

    // Otherwise, return v
    return v;
}

// Function to perform union of the
// two variables
static void unions(int a, int b,
                   ArrayList<Integer> parent)
{
    // Stores the parent of a and b
    int x = find(a, parent);
    int y = find(b, parent);

    // If they are not equal, make
    // parent[x] = parent[y]
    if (x != y)
        parent.set(x, parent.get(y));
}

// Function to check whether it is
// possible to assign values to
// variables to satisfy relations
static boolean equationsPossible(ArrayList<String> relations)
{

    // Initialize parent array as 0s
    ArrayList<Integer> parent = new ArrayList<Integer>();
    for(int i = 0; i < 26; i++)
        parent.add(0);

    // Iterate in range [0, 25]
    // and make parent[i] = i
    for(int i = 0; i < 26; i++)
    {
        parent.set(i, i);
    }

    // Store the size of the string
    int n = relations.size();

    // Traverse the string
    for(String str : relations)
    {

        // Check if it is of the
        // form "i==j" or not
        if (str.charAt(1) == '=')

        // Take union of both
        // the variables
        unions((int)str.charAt(0) - 97,
               (int)str.charAt(3) - 97,
               parent);
    }

    // Traverse the string
    for(String str : relations)
    {

        // Check if it is of the
        // form "i!=j" or not
        if (str.charAt(1) == '!')
        {

            // Store the parent of
            // i and j
            int x = find((int)str.charAt(0) - 97,
                         parent);
            int y = find((int)str.charAt(3) - 97,
                         parent);

            // If they are equal,
            // then return false
            if (x == y)
                return false;
        }
    }
    return true;
}

// Driver Code
public static void main (String[] args)
{
    ArrayList<String> relations = new ArrayList<String>(
        Arrays.asList("i==j", "j!=i"));
    if (equationsPossible(relations))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find parent of each node
def find(v, parent):

    # If parent[v] is not v, then
    # recursively call to find the
    # parent of parent[v]
    if (parent[v] != v):
        parent[v] = find(parent[v], parent)
        return parent[v]

    # Otherwise, return v
    return v

# Function to perform union of the
# two variables
def unions(a, b, parent):

    # Stores the parent of a and b
    x = find(a, parent)
    y = find(b, parent)

    # If they are not equal, make
    # parent[x] = parent[y]
    if (x != y):
        parent[x] = parent[y]

# Function to check whether it is
# possible to assign values to
# variables to satisfy relations
def equationsPossible(relations):

    # Initialize parent array as 0s
    parent = [0]*(26)

    # Iterate in range [0, 25]
    # and make parent[i] = i
    for i in range(26):
        parent[i] = i

    # Store the size of the string
    n = len(relations)

    # Traverse the string
    for string in relations:

        # Check if it is of the
        # form "i==j" or not
        if (string[1] == '='):

            # Take union of both
            # the variables
            unions(ord(string[0]) - ord('a'),ord(string[3]) - ord('a'), parent)

    # Traverse the string
    for string in relations:

        # Check if it is of the
        # form "i!=j" or not
        if (string[1] == '!'):

            # Store the parent of
            # i and j
            x = find(ord(string[0]) - ord('a'), parent)
            y = find(ord(string[3]) - ord('a'), parent)

            # If they are equal,
            # then return false
            if (x == y):
                return False
    return True

# Driver Code
if __name__ == '__main__':
    relations = ["i==j", "j!=i"]
    if (equationsPossible(relations)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to find parent of each node
  static int find(int v, List<int> parent)
  {
    // If parent[v] is not v, then
    // recursively call to find the
    // parent of parent[v]
    if (parent[v] != v)
      return parent[v] = find(parent[v],
                              parent);

    // Otherwise, return v
    return v;
  }

  // Function to perform union of the
  // two variables
  static void unions(int a, int b,
                     List<int> parent)
  {
    // Stores the parent of a and b
    int x = find(a, parent);
    int y = find(b, parent);

    // If they are not equal, make
    // parent[x] = parent[y]
    if (x != y)
      parent[x] = parent[y];
  }

  // Function to check whether it is
  // possible to assign values to
  // variables to satisfy relations
  static bool equationsPossible(List<string> relations)
  {
    // Initialize parent array as 0s
    List<int> parent = new List<int>();
    for(int i=0;i<26;i++)
      parent.Add(0);

    // Iterate in range [0, 25]
    // and make parent[i] = i
    for (int i = 0; i < 26; i++) {
      parent[i] = i;
    }

    // Store the size of the string
    int n = relations.Count;

    // Traverse the string
    foreach( string str in relations) {

      // Check if it is of the
      // form "i==j" or not
      if (str[1] == '=')

        // Take union of both
        // the variables
        unions((int)str[0] - 97,
               (int)str[3] - 97,
               parent);
    }

    // Traverse the string
    foreach (string str in relations) {

      // Check if it is of the
      // form "i!=j" or not
      if (str[1] == '!') {

        // Store the parent of
        // i and j
        int x = find((int)str[0] - 97,
                     parent);
        int y = find((int)str[3] - 97,
                     parent);

        // If they are equal,
        // then return false
        if (x == y)
          return false;
      }
    }

    return true;
  }

  // Driver Code
  public static void Main()
  {
    List<string> relations = new List<string>{ "i==j", "j!=i" };

    if (equationsPossible(relations)) {
      Console.WriteLine("Yes");
    }
    else {
      Console.WriteLine("No");
    }

  }
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find parent of each node
    function find(v, parent)
    {
      // If parent[v] is not v, then
      // recursively call to find the
      // parent of parent[v]
      if (parent[v] != v)
        return parent[v] = find(parent[v],
                                parent);

      // Otherwise, return v
      return v;
    }

    // Function to perform union of the
    // two variables
    function unions(a, b, parent)
    {
      // Stores the parent of a and b
      let x = find(a, parent);
      let y = find(b, parent);

      // If they are not equal, make
      // parent[x] = parent[y]
      if (x != y)
        parent[x] = parent[y];
    }

    // Function to check whether it is
    // possible to assign values to
    // variables to satisfy relations
    function equationsPossible(relations)
    {
      // Initialize parent array as 0s
      let parent = [];
      for(let i=0;i<26;i++)
        parent.push(0);

      // Iterate in range [0, 25]
      // and make parent[i] = i
      for (let i = 0; i < 26; i++) {
        parent[i] = i;
      }

      // Store the size of the string
      let n = relations.length;

      // Traverse the string
      for(let str = 0; str < relations.length; str++) {

        // Check if it is of the
        // form "i==j" or not
        if (relations[1] == '=')

          // Take union of both
          // the variables
          unions(relations[0].charCodeAt() - 97,
                 relations[3].charCodeAt() - 97,
                 parent);
      }

      // Traverse the string
      for(let str = 0; str < relations.length; str++) {
        return false;
        // Check if it is of the
        // form "i!=j" or not
        if (relations[1] == '!') {
          // Store the parent of
          // i and j
          let x = find(relations[0].charCodeAt() - 97,
                       parent);
          let y = find(relations[3].charCodeAt() - 97,
                       parent);

          // If they are equal,
          // then return false
          if (x == y)
            return false;
        }
      }

      return true;
    }

    let relations = [ "i==j", "j!=i" ];

    if (equationsPossible(relations)) {
      document.write("Yes");
    }
    else {
      document.write("No");
    }

  // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(N*log M)，其中 **M** 是 arr[]中唯一变量的个数。*
***辅助空间:** O(1)*