# 检查一个字符串是否可以通过给定类型的相邻字符的交换转换成另一个字符串

> 原文:[https://www . geesforgeks . org/check-if-字符串可以通过给定类型的相邻字符的交换来转换为另一个字符串/](https://www.geeksforgeeks.org/check-if-a-string-can-be-converted-to-another-by-swapping-of-adjacent-characters-of-given-type/)

给定两个大小为 **N** 的字符串 **str1** 和 **str2** ，仅由三个字符 **A** 、 **B** 和 **C** 组成，任务是使用以下操作检查字符串 **str1** 是否可以更改为 **str2** :

*   将“BC”的一个出现替换为“CB”，即交换相邻的“B”和“C”。
*   用“交流”替换一次出现的“交流”，即交换相邻的“交流”和“交流”。

打印“**是”**如果能把字符串换成别的打印“**否”**。
**例:**

> **输入:**str 1 =“BCCABCBCA”，str 2 =“CBACCBBAC”
> **输出:**是
> **解释:**
> 使用以下步骤变换字符串:
> BCCABCBCA->CBCABCBCA->cbacbca->CBACCBBCA->CBACCBBAC。
> **输入:**str 1 =“BAC”，str 2 =“CAB”
> **输出:** False

**天真方法:**想法是通过执行给定的操作，从字符串的开始处递归生成所有可能的字符串 **str1** ，并将其存储在字符串的[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。然后检查该组中是否有任何字符串等于字符串 **str2** 。如果在集合中找到字符串 **str2** ，则打印“**是”**否则打印“**否”**。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*
**高效方法:**想法是同时横向移动两个字符串，检查是否有可能将字符串 **str1** 转换为 **str2** 直到某个特定的索引。以下是步骤:

1.  检查字符串 **str1** 和 **str2** 中的序列“A”和“B”，如果相同，则进入第二步。否则，打印“否”，因为所需的转换是不可能的。
2.  **str1** 中‘A’的索引应该大于等于 **str2** 中对应‘A’的索引，因为“CA”只能转换为“AC”。
3.  同样的， **str1** 字符串中的‘B’索引应该小于等于 **str2** 中的‘B’对应索引，因为“BC”只能转换为“CB”。
4.  如果不满足以上两个条件，则打印“**否”**。否则，打印“**是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
// to transform start to end
bool canTransform(string str1,
                string str2)
{
    string s1 = "";
    string s2 = "";

    // Check the sequence of A, B in
    // both strings str1 and str2
    for (char c : str1) {
        if (c != 'C') {
            s1 += c;
        }
    }

    for (char c : str2) {
        if (c != 'C') {
            s2 += c;
        }
    }

    // If both the strings
    // are not equal
    if (s1 != s2)
        return false;

    int i = 0;
    int j = 0;
    int n = str1.length();

    // Traverse the strings
    while (i < n and j < n) {
        if (str1[i] == 'C') {
            i++;
        }

        else if (str2[j] == 'C') {
            j++;
        }

        // Check for indexes of A and B
        else {
            if ((str1[i] == 'A'
                and i < j)
                or (str1[i] == 'B'
                    and i > j)) {
                return false;
            }
            i++;
            j++;
        }
    }

    return true;
}

// Driver Code
int main()
{
    string str1 = "BCCABCBCA";
    string str2 = "CBACCBBAC";

    // Function Call
    if (canTransform(str1, str2)) {
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
import java.util.*;
class GFG{

    // Function to check if it is possible
    // to transform start to end
    static boolean canTransform(String str1, String str2)
    {
        String s1 = "";
        String s2 = "";

        // Check the sequence of A, B in
        // both Strings str1 and str2
        for (char c : str1.toCharArray())
        {
            if (c != 'C')
            {
                s1 += c;
            }
        }

        for (char c : str2.toCharArray())
        {
            if (c != 'C')
            {
                s2 += c;
            }
        }

        // If both the Strings
        // are not equal
        if (!s1.equals(s2))
            return false;

        int i = 0;
        int j = 0;
        int n = str1.length();

        // Traverse the Strings
        while (i < n && j < n)
        {
            if (str1.charAt(i) == 'C')
            {
                i++;
            }
            else if (str2.charAt(j) == 'C')
            {
                j++;
            }

            // Check for indexes of A and B
            else
            {
                if ((str1.charAt(i) == 'A' && i < j) ||
                    (str1.charAt(i) == 'B' && i > j))
                {
                    return false;
                }
                i++;
                j++;
            }
        }
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str1 = "BCCABCBCA";
        String str2 = "CBACCBBAC";

        // Function Call
        if (canTransform(str1, str2))
        {
            System.out.print("Yes");
        }
        else
        {
            System.out.print("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to transform start to end
def canTransform(str1, str2):

    s1 = ""
    s2 = ""

    # Check the sequence of A, B in
    # both strings str1 and str2
    for c in str1:
        if (c != 'C'):
            s1 += c

    for c in str2:
        if (c != 'C'):
            s2 += c

    # If both the strings
    # are not equal
    if (s1 != s2):
        return False

    i = 0
    j = 0
    n = len(str1)

    # Traverse the strings
    while (i < n and j < n):
        if (str1[i] == 'C'):
            i += 1

        elif (str2[j] == 'C'):
            j += 1

        # Check for indexes of A and B
        else:
            if ((str1[i] == 'A' and i < j) or
                (str1[i] == 'B' and i > j)):
                return False

            i += 1
            j += 1

    return True

# Driver Code
if __name__ == '__main__':

    str1 = "BCCABCBCA"
    str2 = "CBACCBBAC"

    # Function call
    if (canTransform(str1, str2)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if it is possible
// to transform start to end
static bool canTransform(string str1, string str2)
{
    string s1 = "";
    string s2 = "";

    // Check the sequence of A, B in
    // both Strings str1 and str2
    foreach(char c in str1.ToCharArray())
    {
        if (c != 'C')
        {
            s1 += c;
        }
    }

    foreach(char c in str2.ToCharArray())
    {
        if (c != 'C')
        {
            s2 += c;
        }
    }

    // If both the Strings
    // are not equal
    if (s1 != s2)
        return false;

    int i = 0;
    int j = 0;
    int n = str1.Length;

    // Traverse the Strings
    while (i < n && j < n)
    {
        if (str1[i] == 'C')
        {
            i++;
        }
        else if (str2[j] == 'C')
        {
            j++;
        }

        // Check for indexes of A and B
        else
        {
            if ((str1[i] == 'A' && i < j) ||
                (str1[i] == 'B' && i > j))
            {
                return false;
            }
            i++;
            j++;
        }
    }
    return true;
}

// Driver Code
public static void Main(string[] args)
{
    string str1 = "BCCABCBCA";
    string str2 = "CBACCBBAC";

    // Function call
    if (canTransform(str1, str2))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to check if it is possible
      // to transform start to end
      function canTransform(str1, str2) {
        var s1 = "";
        var s2 = "";

        // Check the sequence of A, B in
        // both Strings str1 and str2
        for (const c of str1) {
          if (c !== "C") {
            s1 += c;
          }
        }

        for (const c of str2) {
          if (c !== "C") {
            s2 += c;
          }
        }

        // If both the Strings
        // are not equal
        if (s1 !== s2) return false;

        var i = 0;
        var j = 0;
        var n = str1.length;

        // Traverse the Strings
        while (i < n && j < n) {
          if (str1[i] === "C") {
            i++;
          } else if (str2[j] === "C") {
            j++;
          }

          // Check for indexes of A and B
          else {
            if ((str1[i] === "A" && i < j) || (str1[i] === "B" && i > j)) {
              return false;
            }
            i++;
            j++;
          }
        }
        return true;
      }

      // Driver Code
      var str1 = "BCCABCBCA";
      var str2 = "CBACCBBAC";

      // Function call
      if (canTransform(str1.split(""), str2.split(""))) {
        document.write("Yes");
      } else {
        document.write("No");
      }
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)