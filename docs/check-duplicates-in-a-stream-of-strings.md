# 检查字符串流中的重复项

> 原文:[https://www . geeksforgeeks . org/check-字符串流中的重复项/](https://www.geeksforgeeks.org/check-duplicates-in-a-stream-of-strings/)

给定包含公司员工姓名的字符串数组 **arr[]** 。假设姓名正在一个接一个地输入到系统中，任务是检查当前姓名是否是第一次输入。
**例:**

> **输入:**arr【】= {“极客”、“为”、“极客”}
> **输出:**
> 否
> 否
> 是
> **输入:**arr【】= {“ABC”、“aaa”、“CBA”}
> **输出:**
> 否
> 否
> 否

**方法:**创建一个[无序集](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)来存储员工的姓名并开始遍历数组，如果当前姓名已经存在于该集中，则打印是，否则打印否并将其插入该集中。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to insert the names
// and check whether they appear
// for the first time
void insertNames(string arr[], int n)
{

    // To store the names
    // of the employees
    unordered_set<string> set;
    for (int i = 0; i < n; i++) {

        // If current name is appearing
        // for the first time
        if (set.find(arr[i]) == set.end()) {
            cout << "No\n";
            set.insert(arr[i]);
        }
        else {
            cout << "Yes\n";
        }
    }
}

// Driver code
int main()
{
    string arr[] = { "geeks", "for", "geeks" };
    int n = sizeof(arr) / sizeof(string);

    insertNames(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to insert the names
// and check whether they appear
// for the first time
static void insertNames(String arr[], int n)
{

    // To store the names
    // of the employees
    HashSet<String> set = new HashSet<String>();
    for (int i = 0; i < n; i++)
    {

        // If current name is appearing
        // for the first time
        if (!set.contains(arr[i]))
        {
            System.out.print("No\n");
            set.add(arr[i]);
        }
        else
        {
            System.out.print("Yes\n");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    String arr[] = { "geeks", "for", "geeks" };
    int n = arr.length;

    insertNames(arr, n);
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to insert the names
# and check whether they appear
# for the first time
def insertNames(arr, n) :

    # To store the names
    # of the employees
    string = set();

    for i in range(n) :

        # If current name is appearing
        # for the first time
        if arr[i] not in string :
            print("No");
            string.add(arr[i]);

        else :
            print("Yes");

# Driver code
if __name__ == "__main__" :

    arr = [ "geeks", "for", "geeks" ];
    n = len(arr);

    insertNames(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to insert the names
// and check whether they appear
// for the first time
static void insertNames(String []arr, int n)
{

    // To store the names
    // of the employees
    HashSet<String> set = new HashSet<String>();
    for (int i = 0; i < n; i++)
    {

        // If current name is appearing
        // for the first time
        if (!set.Contains(arr[i]))
        {
            Console.Write("No\n");
            set.Add(arr[i]);
        }
        else
        {
            Console.Write("Yes\n");
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    String []arr = { "geeks", "for", "geeks" };
    int n = arr.Length;

    insertNames(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

// Function to insert the names
// and check whether they appear
// for the first time
function insertNames(arr, n)
{

    // To store the names
    // of the employees
    let set = new Set();
    for (let i = 0; i < n; i++)
    {

        // If current name is appearing
        // for the first time
        if (!set.has(arr[i]))
        {
            document.write("No"  + "<br/>");
            set.add(arr[i]);
        }
        else
        {
            document.write("Yes" + "<br/>");
        }
    }
}

    // Driver code

    let arr = [ "geeks", "for", "geeks" ];
    let n = arr.length;

    insertNames(arr, n);

 // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
No
No
Yes
```