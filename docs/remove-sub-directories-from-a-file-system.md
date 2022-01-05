# 从文件系统中删除子目录

> 原文:[https://www . geesforgeks . org/remove-子目录-从文件系统/](https://www.geeksforgeeks.org/remove-sub-directories-from-a-file-system/)

给定一个由字符串形式的 **N** 个唯一目录组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**[**字符串**](https://www.geeksforgeeks.org/string-data-structure/) **arr[]** ，任务是删除所有子目录并打印最终数组。**

> **A **目录**T2 S 是**子目录**如果存在任何目录 **D** 使得 **S** 是 **D** 的前缀。**

****示例:****

> ****输入:**arr[]= {“/a”、“/a/j”、“/c/d/e”、“/c/d”、“/b”}
> **输出:**{“/a”、“/c/d”、“/b”}
> **说明:**目录“/a/j”是目录“/a”的子目录，“/c/d/e”是目录“/c/d”的子目录。
> 因此，把两者都去掉。**
> 
>  ****输入:**arr[]=**{“/a”、“/a/b”、“/a/b/c”、“/a/b/c/d”}
> **输出:**{“/a”}
> **说明:**所有目录都是“/a”的子目录****

******天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)来检查每个字符串，如果存在以它为前缀的字符串，则从数组中移除这些字符串。****

*******时间复杂度:** O(len * N <sup>2</sup> )* ，其中 len 为数组中最长字符串的长度。
***辅助空间:** O(N)*****

******高效方法:**思路是[对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，并将位置 **i** 处的当前目录与索引 **(i -1)** 处的先前目录进行比较。如果**arr[I–1]**是 **arr[i]** 的前缀，则移除 **arr[i]** 。检查整个阵列后，打印剩余的目录。按照以下步骤解决问题:****

*   ****将所有目录按字母顺序排序，并初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **res** 。****
*   ****将第一个目录插入 **res** 。****
*   ****用最后一个有效目录检查每个目录，即从**到**的最后一个目录。****
*   ****如果目录等于先前有效目录的某个前缀，则该目录无效(子目录)。否则有效。****
*   ****如果当前目录有效，则将其添加到 **res** 。****
*   ****遍历完成后，打印 **res** 中的所有目录。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to remove sub-directories
// from the given lists dir
void eraseSubdirectory(vector<string>& dir)
{
    // Store final result
    vector<string> res;

    // Sort the given directories
    sort(dir.begin(), dir.end());

    // Insert 1st directory
    res.push_back(dir[0]);

    cout << "{" << dir[0] << ", ";

    // Iterating in directory
    for (int i = 1; i < dir.size(); i++) {

        // Current directory
        string curr = dir[i];

        // Our previous valid directory
        string prev = res.back();

        // Find length of previous directory
        int l = prev.length();

        // If subdirectory is found
        if (curr.length() > l && curr[l] == '/'
            && prev == curr.substr(0, l))
            continue;

        // Else store it in result
        // valid directory
        res.push_back(curr);

        cout << curr << ", ";
    }

    cout << "}\n";
}

// Driver Code
int main()
{
    // Given lists of directories dir[]
    vector<string> dir
        = { "/a", "/a/j", "/c/d/e",
            "/c/d", "/b" };

    // Function Call
    eraseSubdirectory(dir);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to remove sub-directories
// from the given lists dir
static void eraseSubdirectory(ArrayList<String> dir)
{

    // Store final result
    ArrayList<String> res = new ArrayList<String>();

    // Sort the given directories
    Collections.sort(dir);

    // Insert 1st directory
    res.add(dir.get(0));

    System.out.print("{" + dir.get(0) + ", ");

    // Iterating in directory
    for(int i = 1; i < dir.size(); i++)
    {

        // Current directory
        String curr = dir.get(i);

        // Our previous valid directory
        String prev = res.get(res.size() - 1);

        // Find length of previous directory
        int l = prev.length();

        // If subdirectory is found
        if (curr.length() > l &&
           curr.charAt(l) == '/' &&
           prev.equals(curr.substring(0, l)))
            continue;

        // Else store it in result
        // valid directory
        res.add(curr);

        System.out.print(curr + ", ");
    }
    System.out.print("}\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given lists of directories dir[]
    ArrayList<String> dir = new ArrayList<String>(Arrays.asList(
            "/a", "/a/j", "/c/d/e", "/c/d", "/b"));

    // Function Call
    eraseSubdirectory(dir);
}
}

// This code is contributed by akhilsaini**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function to remove sub-directories
# from the given lists dir
def eraseSubdirectory(dir):

    # Store final result
    res = []

    # Sort the given directories
    dir.sort()

    # Insert 1st directory
    res.append(dir[0])

    print("{", dir[0], end = ", ")

    # Iterating in directory
    for i in range(1, len(dir)):

        # Current directory
        curr = dir[i]

        # Our previous valid directory
        prev = res[len(res) - 1]

        # Find length of previous directory
        l = len(prev)

        # If subdirectory is found
        if (len(curr) > l and
           curr[l] == '/' and
              prev == curr[:l]):
            continue

        # Else store it in result
        # valid directory
        res.append(curr)
        print(curr, end = ", ")

    print("}")

# Driver Code
if __name__ == '__main__':

    # Given lists of directories dir[]
    dir = [ "/a", "/a/j", "/c/d/e", "/c/d", "/b" ]

    # Function Call
    eraseSubdirectory(dir)

# This code is contributed by akhilsaini**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections;

class GFG{

// Function to remove sub-directories
// from the given lists dir
static void eraseSubdirectory(ArrayList dir)
{

    // Store final result
    ArrayList res = new ArrayList();

    // Sort the given directories
    dir.Sort();

    // Insert 1st directory
    res.Add(dir[0]);

    Console.Write("{" + dir[0] + ", ");

    // Iterating in directory
    for(int i = 1; i < dir.Count; i++)
    {

        // Current directory
        string curr = (string)dir[i];

        // Our previous valid directory
        string prev = (string)res[(res.Count - 1)];

        // Find length of previous directory
        int l = prev.Length;

        // If subdirectory is found
        if (curr.Length > l && curr[l] == '/' &&
            prev.Equals(curr.Substring(0, l)))
            continue;

        // Else store it in result
        // valid directory
        res.Add(curr);

        Console.Write(curr + ", ");
    }
    Console.Write("}\n");
}

// Driver Code
public static void Main()
{

    // Given lists of directories dir[]
    ArrayList dir = new ArrayList(){ "/a", "/a/j",
                                     "/c/d/e",
                                     "/c/d", "/b" };

    // Function Call
    eraseSubdirectory(dir);
}
}

// This code is contributed by akhilsaini**
```

******Output:** 

```
{/a, /b, /c/d, }
```**** 

*******时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*****