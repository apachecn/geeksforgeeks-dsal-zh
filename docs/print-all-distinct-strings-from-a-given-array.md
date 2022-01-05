# 打印给定数组中所有不同的字符串

> 原文:[https://www . geesforgeks . org/print-all-distinct-strings-from-a-给定数组/](https://www.geeksforgeeks.org/print-all-distinct-strings-from-a-given-array/)

给定一个大小为 **N** 的[字符串数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/) **arr[]** ，任务是打印给定数组中所有不同的字符串。

**示例:**

> **输入:** arr[] = {“极客”、“For”、“极客”、“代码”、“编码器”}
> **输出:**编码器代码极客 For
> **解释:**由于数组中的所有字符串都是不同的，所以需要的输出是**编码器代码极客 For** 。
> 
> **输入:** arr[] = {“好”“神”“好”“神”“神”}
> T3】输出:神好神好

**天真方法:**解决这个问题最简单的方法是[根据字符串的字典顺序对](https://www.geeksforgeeks.org/sort-c-stl/)数组进行排序。[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查数组的当前字符串是否等于之前遍历的字符串。如果发现为假，则打印当前字符串。

***时间复杂度:** O(N * M * log(N))，其中 M 为最长字符串的长度。*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。按照以下步骤解决问题:

*   初始化一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如说 **DistString** ，来存储给定数组中的不同字符串。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将数组元素插入**字符串**。
*   最后，打印 **DistString** 中的所有字符串。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the distinct strings
// from the given array
void findDisStr(vector<string>& arr, int N)
{
    // Stores distinct strings
    // from the given array
    unordered_set<string> DistString;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If current string not
        // present into the set
        if (!DistString.count(arr[i])) {

            // Insert current string
            // into the set
            DistString.insert(arr[i]);
        }
    }

    // Traverse the set DistString
    for (auto String : DistString) {

        // Print distinct string
        cout << String << " ";
    }
}

// Driver Code
int main()
{
    vector<string> arr = { "Geeks", "For", "Geeks",
                           "Code", "Coder" };

    // Stores length of the array
    int N = arr.size();

    findDisStr(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the distinct strings
// from the given array
static void findDisStr(List<String> arr, int N)
{

    // Stores distinct strings
    // from the given array
    Set<String> DistString = new HashSet<String>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current string not
        // present into the set
        if (!DistString.contains(arr.get(i)))
        {

            // Insert current string
            // into the set
            DistString.add(arr.get(i));
        }
    }

    // Traverse the set DistString
    for(String string : DistString)
    {

        // Print distinct string
        System.out.print(string + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    List<String> arr = Arrays.asList(new String[]{
        "Geeks", "For", "Geeks", "Code", "Coder" });

    // Stores length of the array
    int N = arr.size();

    findDisStr(arr, N);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the distinct
# strings from the given array
def findDisStr(arr, N):

    # Stores distinct strings
    # from the given array
    DistString = set()

    # Traverse the array
    for i in range(N):

        # If current string not
        # present into the set
        if (arr[i] not in DistString):

            # Insert current string
            # into the set
            DistString.add(arr[i])

    # Traverse the set DistString
    for string in DistString:

        # Print distinct string
        print(string, end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ "Geeks", "For", "Geeks",
            "Code", "Coder" ]

    # Stores length of the array
    N = len(arr)

    findDisStr(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the distinct strings
// from the given array
static void findDisStr(List<string> arr, int N)
{

    // Stores distinct strings
    // from the given array
    HashSet<string> DistString = new HashSet<string>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If current string not
        // present into the set
        if (!DistString.Contains(arr[i]))
        {

            // Insert current string
            // into the set
            DistString.Add(arr[i]);
        }
    }

    // Traverse the set DistString
    foreach(string a in DistString)
    { 
      Console.Write(a +" "); 
    } 
}

// Driver code
public static void Main(String[] args)
{
    List<String> arr = new List<string>(new []{
        "Geeks", "For", "Geeks", "Code", "Coder" });

    // Stores length of the array
    int N = arr.Count;

    findDisStr(arr, N);
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the distinct strings
// from the given array
function findDisStr(arr, N) {
    // Stores distinct strings
    // from the given array
    let DistString = new Set();

    // Traverse the array
    for (let i = N - 1; i >= 0; i--) {
        // If current string not
        // present into the set
        if (!DistString.has(arr[i])) {

            // Insert current string
            // into the set
            DistString.add(arr[i]);
        }
    }

    for (let String of DistString) {

        // Print distinct string
        document.write(String + " ");
    }
}

// Driver Code

let arr = ["Geeks", "For", "Geeks",
    "Code", "Coder"];

// Stores length of the array
let N = arr.length;

findDisStr(arr, N);

</script>
```

**Output:** 

```
Coder Code Geeks For
```

***时间复杂度:** O(N * M)，其中 M 是最长字符串的长度。*
***辅助空间:** O(N * M)*