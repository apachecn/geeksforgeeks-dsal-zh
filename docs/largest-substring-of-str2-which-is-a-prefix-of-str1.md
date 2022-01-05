# str 2 的最大子串，是 str1 的前缀

> 原文:[https://www . geeksforgeeks . org/str 2 的最大子串-也就是 str1 的前缀/](https://www.geeksforgeeks.org/largest-substring-of-str2-which-is-a-prefix-of-str1/)

给定两个字符串 **str1** 和 **str2** ，任务是找到 **str1** 的最长前缀，该前缀作为字符串 **str2** 的子串出现。如果可能，打印前缀，否则打印-1。
**举例:**

> **输入:** str1 =“极客 for”，str 2 =“forgeks”
> T3】输出:极客
> str 2
> 中出现的 str1 的所有前缀都是“g”、“ge”、“gee”、“极客”和“极客”。
> **输入:**str 1 =“ABC”，str 2 =“def”
> **输出:** -1

**方法:**检查 **str1** 是否作为子串出现在 **str2** 中。如果是，则 **str1** 是所需字符串，否则从 **str1** 中删除最后一个字符，并重复这些步骤，直到字符串 **str1** 变为空或找到所需字符串。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the largest substring
// in str2 which is a prefix of str1
string findPrefix(string str1, string str2)
{

    // To store the index in str2 which
    // matches the prefix in str1
    int pos = -1;

    // While there are characters left in str1
    while (!str1.empty()) {

        // If the prefix is not found in str2
        if (str2.find(str1) == string::npos)

            // Remove the last character
            str1.pop_back();
        else {

            // Prefix found
            pos = str2.find(str1);
            break;
        }
    }

    // No substring found in str2 that
    // matches the prefix of str1
    if (pos == -1)
        return "-1";

    return str1;
}

// Driver code
int main()
{
    string str1 = "geeksfor";
    string str2 = "forgeeks";

    cout << findPrefix(str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the largest substring
// in str2 which is a prefix of str1
static String findPrefix(String str1,
                         String str2)
{

    // To store the index in str2 which
    // matches the prefix in str1
    boolean pos = false;

    // While there are characters left in str1
    while (str1.length() > 0)
    {

        // If the prefix is not found in str2
        if (!str2.contains(str1))

            // Remove the last character
            str1 = str1.substring(0, str1.length() - 1);
        else
        {

            // Prefix found
            pos = str2.contains(str1);
            break;
        }
    }

    // No substring found in str2 that
    // matches the prefix of str1
    if (pos == false)
        return "-1";

    return str1;
}

// Driver code
public static void main(String[] args)
{
    String str1 = "geeksfor";
    String str2 = "forgeeks";

    System.out.println(findPrefix(str1, str2));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import operator

# Function to return the largest substring
# in str2 which is a prefix of str1
def findPrefix(str1, str2):

    # To store the index in str2 which
    # matches the prefix in str1
    pos = False;

    # While there are characters left in str1
    while (len(str1) != 0):

        # If the prefix is not found in str2
        if operator.contains(str2, str1) != True:

            # Remove the last character
            str1 = str1[0: len(str1) - 1];
        else:

            # Prefix found
            pos = operator.contains(str2, str1);
            break;

    # No substring found in str2 that
    # matches the prefix of str1
    if (pos == False):
        return "-1";

    return str1;

# Driver code
if __name__ == '__main__':
    str1 = "geeksfor";
    str2 = "forgeeks";

    print(findPrefix(str1, str2));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the largest substring
// in str2 which is a prefix of str1
static String findPrefix(String str1,
                         String str2)
{

    // To store the index in str2 which
    // matches the prefix in str1
    bool pos = false;

    // While there are characters left in str1
    while (str1.Length > 0)
    {

        // If the prefix is not found in str2
        if (!str2.Contains(str1))

            // Remove the last character
            str1 = str1.Substring(0, str1.Length - 1);
        else
        {

            // Prefix found
            pos = str2.Contains(str1);
            break;
        }
    }

    // No substring found in str2 that
    // matches the prefix of str1
    if (pos == false)
        return "-1";

    return str1;
}

// Driver code
public static void Main(String[] args)
{
    String str1 = "geeksfor";
    String str2 = "forgeeks";

    Console.WriteLine(findPrefix(str1, str2));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the largest substring
// in str2 which is a prefix of str1
function findPrefix(str1, str2)
{

    // To store the index in str2 which
    // matches the prefix in str1
    var pos = -1;

    // While there are characters left in str1
    while (str1.length!=0) {

        // If the prefix is not found in str2
        if (!str2.includes(str1))

            // Remove the last character
            str1 = str1.substring(0,str1.length-1)
        else {

            // Prefix found
            pos = str2.includes(str1);
            break;
        }
    }

    // No substring found in str2 that
    // matches the prefix of str1
    if (pos == -1)
        return "-1";

    return str1;
}

// Driver code
var str1 = "geeksfor";
var str2 = "forgeeks";
document.write( findPrefix(str1, str2));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
geeks
```

**时间复杂度:** O(N * M)，其中 N、M 为给定字符串的长度。