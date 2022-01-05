# 比较两个版本号

> 原文:[https://www.geeksforgeeks.org/compare-two-version-numbers/](https://www.geeksforgeeks.org/compare-two-version-numbers/)

版本号是一个字符串，用于标识软件产品的唯一状态。版本号看起来像 a.b.c.d，其中 a、b 等是数字，因此版本号是一个字符串，其中数字用点分隔。这些数字通常代表从大调到小调的层次结构(a 是大调，d 是小调)。
在这个问题中，给了我们两个版本号。我们需要对它们进行比较，得出哪个是最新的版本号(也就是哪个版本号更小)。

**示例:**

```
Input: 
V1 = “1.0.31”
V2 = “1.0.27”
Output:  v2 is latest
Because V2 < V1

Input: 
V1 = “1.0.10”
V2 = “1.0.27”
Output:  v1 is latest
Because V1 < V2 
```

**方法:**由于点的原因，不可能直接比较，但是版本可以按数字部分比较，然后可以找到最新版本。遍历字符串，分离数字部分并进行比较。如果相等，则比较下一个数字部分，以此类推，直到它们不同，否则将它们标记为相等。
实施一种方法来比较两个版本。如果有两个以上的版本，那么下面的 versionCompare 方法可以作为排序方法的比较方法，它将根据指定的比较对所有版本进行排序。

## C++

```
// C/C++ program to compare
// two version number
#include <bits/stdc++.h>
using namespace std;

// Method to compare two versions.
// Returns 1 if v2 is smaller, -1
// if v1 is smaller, 0 if equal
int versionCompare(string v1, string v2)
{
    // vnum stores each numeric
    // part of version
    int vnum1 = 0, vnum2 = 0;

    // loop until both string are
    // processed
    for (int i = 0, j = 0; (i < v1.length()
                            || j < v2.length());) {
        // storing numeric part of
        // version 1 in vnum1
        while (i < v1.length() && v1[i] != '.') {
            vnum1 = vnum1 * 10 + (v1[i] - '0');
            i++;
        }

        // storing numeric part of
        // version 2 in vnum2
        while (j < v2.length() && v2[j] != '.') {
            vnum2 = vnum2 * 10 + (v2[j] - '0');
            j++;
        }

        if (vnum1 > vnum2)
            return 1;
        if (vnum2 > vnum1)
            return -1;

        // if equal, reset variables and
        // go for next numeric part
        vnum1 = vnum2 = 0;
        i++;
        j++;
    }
    return 0;
}

// Driver method to check above
// comparison function
int main()
{
    string version1 = "1.0.3";
    string version2 = "1.0.7";

    if (versionCompare(version1, version2) < 0)
        cout << version1 << " is smaller\n";
    else if (versionCompare(version1, version2) > 0)
        cout << version2 << " is smaller\n";
    else
        cout << "Both version are equal\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compare two version number
import java.util.*;

class GFG {

    // Method to compare two versions.
    // Returns 1 if v2 is
    // smaller, -1 if v1 is smaller, 0 if equal
    static int versionCompare(String v1, String v2)
    {
        // vnum stores each numeric part of version
        int vnum1 = 0, vnum2 = 0;

        // loop until both String are processed
        for (int i = 0, j = 0; (i < v1.length()
                                || j < v2.length());) {
            // Storing numeric part of
            // version 1 in vnum1
            while (i < v1.length()
                   && v1.charAt(i) != '.') {
                vnum1 = vnum1 * 10
                        + (v1.charAt(i) - '0');
                i++;
            }

            // storing numeric part
            // of version 2 in vnum2
            while (j < v2.length()
                   && v2.charAt(j) != '.') {
                vnum2 = vnum2 * 10
                        + (v2.charAt(j) - '0');
                j++;
            }

            if (vnum1 > vnum2)
                return 1;
            if (vnum2 > vnum1)
                return -1;

            // if equal, reset variables and
            // go for next numeric part
            vnum1 = vnum2 = 0;
            i++;
            j++;
        }
        return 0;
    }

    // Driver method to check above
    // comparison function
    public static void main(String[] args)
    {
        String version1 = "1.0.3";
        String version2 = "1.0.7";

        if (versionCompare(version1, version2) < 0)
            System.out.println(version1 + " is smaller");
        else if (versionCompare(version1, version2) > 0)
            System.out.println(version2 + " is smaller");
        else
            System.out.println("Both version are equal");
    }
}

// This code is contributed by shivanisinghss2110
```

## 计算机编程语言

```
# Python program to compare two version number

# Method to compare two versions.
# Return 1 if v2 is smaller,
# -1 if v1 is smaller,,
# 0 if equal
def versionCompare(v1, v2):

    # This will split both the versions by '.'
    arr1 = v1.split(".")
    arr2 = v2.split(".")
    n = len(arr1)
    m = len(arr2)

    # converts to integer from string
    arr1 = [int(i) for i in arr1]
    arr2 = [int(i) for i in arr2]

    # compares which list is bigger and fills
    # smaller list with zero (for unequal delimiters)
    if n>m:
      for i in range(m, n):
         arr2.append(0)
    elif m>n:
      for i in range(n, m):
         arr1.append(0)

    # returns 1 if version 1 is bigger and -1 if
    # version 2 is bigger and 0 if equal
    for i in range(len(arr1)):
      if arr1[i]>arr2[i]:
         return 1
      elif arr2[i]>arr1[i]:
         return -1
    return 0

# Driver program to check above comparison function
version1 = "1.0.3"
version2 = "1.0.7"

ans = versionCompare(version1, version2)
if ans < 0:
    print version1 + " is smaller"
elif ans > 0:
    print version2 + " is smaller"
else:
    print "Both versions are equal"

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
# and improved by Tuhin Das (tuhindas221b)
```

## C#

```
// C# program to compare
// two version number
using System;
class GFG
{

  // Method to compare two versions.
  // Returns 1 if v2 is smaller, -1
  // if v1 is smaller, 0 if equal
  static int versionCompare(string v1, string v2)
  {
    // vnum stores each numeric
    // part of version
    int vnum1 = 0, vnum2 = 0;

    // loop until both string are
    // processed
    for (int i = 0, j = 0; (i < v1.Length || j < v2.Length);)
    {

      // storing numeric part of
      // version 1 in vnum1
      while (i < v1.Length && v1[i] != '.')
      {
        vnum1 = vnum1 * 10 + (v1[i] - '0');
        i++;
      }

      // storing numeric part of
      // version 2 in vnum2
      while (j < v2.Length && v2[j] != '.')
      {
        vnum2 = vnum2 * 10 + (v2[j] - '0');
        j++;
      }

      if (vnum1 > vnum2)
        return 1;
      if (vnum2 > vnum1)
        return -1;

      // if equal, reset variables and
      // go for next numeric part
      vnum1 = vnum2 = 0;
      i++;
      j++;
    }
    return 0;
  }

  // Driver code
  static void Main()
  {
    string version1 = "1.0.3";
    string version2 = "1.0.7";

    if (versionCompare(version1, version2) < 0)
      Console.WriteLine(version1 + " is smaller");
    else if (versionCompare(version1, version2) > 0)
      Console.WriteLine(version2 + " is smaller");
    else
      Console.WriteLine("Both version are equal");
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// Javascript implementation

// Method to compare two versions.
// Returns 1 if v2 is smaller, -1
// if v1 is smaller, 0 if equal
function versionCompare(v1, v2)
{
    // vnum stores each numeric
    // part of version
    var vnum1 = 0, vnum2 = 0;

    // loop until both string are
    // processed
    for (var i = 0, j = 0; (i < v1.length
                            || j < v2.length);) {
        // storing numeric part of
        // version 1 in vnum1
        while (i < v1.length && v1[i] != '.') {
            vnum1 = vnum1 * 10 + (v1[i] - '0');
            i++;
        }

        // storing numeric part of
        // version 2 in vnum2
        while (j < v2.length && v2[j] != '.') {
            vnum2 = vnum2 * 10 + (v2[j] - '0');
            j++;
        }

        if (vnum1 > vnum2)
            return 1;
        if (vnum2 > vnum1)
            return -1;

        // if equal, reset variables and
        // go for next numeric part
        vnum1 = vnum2 = 0;
        i++;
        j++;
    }
    return 0;
}

// Driver method to check above
// comparison function
var version1 = "1.0.3";
var version2 = "1.0.7";

if (versionCompare(version1, version2) < 0)
    document.write(version1 + " is smaller" + "<br>");
else if (versionCompare(version1, version2) > 0)
    document.write(version2 + " is smaller" + "<br>");
else
    document.write("Both version are equal" + "<br>");

// This is code is contributed
// by shubhamsingh10
</script>
```

**输出:**

```
1.0.3 is smaller
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为字符串的长度。
    只需要遍历字符串一次。
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。