# 按字典顺序回答第 X 个最小子串的查询

> 原文:[https://www . geesforgeks . org/query-to-answer-the-x-th-minist-sub-string-按字典顺序/](https://www.geeksforgeeks.org/queries-to-answer-the-x-th-smallest-sub-string-lexicographically/)

给定一个字符串**字符串**和 **Q** 查询。每个查询由一个数字 **X** 组成，任务是打印给定字符串 **str** 的 **X <sup>th</sup>** 的字典最小子字符串。

**示例:**

> **输入:** str = "geek "，q[] = {1，5，10}
> **输出:**
> e
> ek
> k
> “e”“e”“ee”“eek”“ek”“g”“ge”“gee”“geek”“geek”“geek”和“k”是
> 所有可能的子串，按字典顺序排序。
> 
> **输入:**【str = " abcdgdhge】，q[]=【15，32】
> **输出:**
> 【bcgdhge】
> gdhge

**方法:**生成所有的子字符串，并将它们存储在任何数据结构中，并按照字典顺序对该数据结构进行排序。在下面的解决方案中，我们使用了一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来存储所有的子字符串，并且内置的排序函数按照给定的顺序对它们进行排序。现在，对于每个查询打印**vec【X–1】**，这将是 **X <sup>第</sup>** 个最小的子串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to pre-process the sub-strings
// in sorted order
void pre_process(vector<string>& substrings, string s)
{
    int n = s.size();

    // Generate all substrings
    for (int i = 0; i < n; i++) {
        string dup = "";

        // Iterate to find all sub-strings
        for (int j = i; j < n; j++) {
            dup += s[j];

            // Store the sub-string in the vector
            substrings.push_back(dup);
        }
    }

    // Sort the substrings lexicographically
    sort(substrings.begin(), substrings.end());
}

// Driver code
int main()
{
    string s = "geek";

    // To store all the sub-strings
    vector<string> substrings;
    pre_process(substrings, s);

    int queries[] = { 1, 5, 10 };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Perform queries
    for (int i = 0; i < q; i++)
        cout << substrings[queries[i] - 1] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to pre-process the sub-strings
// in sorted order
static void pre_process(String substrings[],String s)
{
    int n = s.length();

    // Generate all substrings
    int count = 0;
    for (int i = 0; i < n; i++)
    {
        String dup = "";

        // Iterate to find all sub-strings
        for (int j = i; j < n; j++)
        {
            dup += s.charAt(j);

            // Store the sub-string in the vector
            substrings[count++] = dup;
        }
    }

    // Sort the substrings lexicographically
    int size = substrings.length;

    for(int i = 0; i < size-1; i++) {
        for (int j = i + 1; j < substrings.length; j++)
        {
            if(substrings[i].compareTo(substrings[j]) > 0)
            {
                String temp = substrings[i];
                substrings[i] = substrings[j];
                substrings[j] = temp;
            }
        }

    //sort(substrings.begin(), substrings.end());
}
}

// Driver code
public static void main(String args[])
{
    String s = "geek";

    // To store all the sub-strings
    String substrings[] = new String[10];
    pre_process(substrings, s);

    int queries[] = { 1, 5, 10 };
    int q = queries.length;

    // Perform queries
    for (int i = 0; i < q; i++)
        System.out.println(substrings[queries[i]-1]);

}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to pre-process the sub-strings
# in sorted order
def pre_process(substrings, s) :

    n = len(s);

    # Generate all substrings
    for i in range(n) :
        dup = "";

        # Iterate to find all sub-strings
        for j in range(i,n) :
            dup += s[j];

            # Store the sub-string in the vector
            substrings.append(dup);

    # Sort the substrings lexicographically
    substrings.sort();
    return substrings;

# Driver code
if __name__ == "__main__" :

    s = "geek";

    # To store all the sub-strings
    substrings = [];
    substrings = pre_process(substrings, s);

    queries = [ 1, 5, 10 ];
    q = len(queries);

    # Perform queries
    for i in range(q) :
        print(substrings[queries[i] - 1]);

# This code is contributed by AnkitRai01
```

## C#

```
// C# code for above given approach
using System;

class GFG
{

// Function to pre-process the sub-strings
// in sorted order
static void pre_process(String []substrings,String s)
{
    int n = s.Length;

    // Generate all substrings
    int count = 0;
    for (int i = 0; i < n; i++)
    {
        String dup = "";

        // Iterate to find all sub-strings
        for (int j = i; j < n; j++)
        {
            dup += s[j];

            // Store the sub-string in the vector
            substrings[count++] = dup;
        }
    }

    // Sort the substrings lexicographically
    int size = substrings.Length;

    for(int i = 0; i < size-1; i++)
    {
        for (int j = i + 1; j < substrings.Length; j++)
        {
            if(substrings[i].CompareTo(substrings[j]) > 0)
            {
                String temp = substrings[i];
                substrings[i] = substrings[j];
                substrings[j] = temp;
            }
        }

    //sort(substrings.begin(), substrings.end());
}
}

// Driver code
public static void Main(String []args)
{
    String s = "geek";

    // To store all the sub-strings
    String []substrings = new String[10];
    pre_process(substrings, s);

    int []queries = { 1, 5, 10 };
    int q = queries.Length;

    // Perform queries
    for (int i = 0; i < q; i++)
        Console.WriteLine(substrings[queries[i]-1]);

}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to pre-process the sub-strings
// in sorted order
function pre_process(substrings, s)
{
    var n = s.length;

    // Generate all substrings
    for (var i = 0; i < n; i++) {
        var dup = "";

        // Iterate to find all sub-strings
        for (var j = i; j < n; j++) {
            dup += s[j];

            // Store the sub-string in the vector
            substrings.push(dup);
        }
    }

    // Sort the substrings lexicographically
    substrings.sort();
}

// Driver code
var s = "geek";
// To store all the sub-strings
var substrings = [];
pre_process(substrings, s);
var queries = [1, 5, 10];
var q = queries.length;
// Perform queries
for (var i = 0; i < q; i++)
    document.write( substrings[queries[i] - 1] + "<br>");

</script>
```

**Output:** 

```
e
ek
k
```