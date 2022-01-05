# 检查一个数字是否以另一个数字开头

> 原文:[https://www . geesforgeks . org/check-if-a-number-start-on-other-number-or-not/](https://www.geeksforgeeks.org/check-if-a-number-starts-with-another-number-or-not/)

给定两个数字 **A** 和 **B** ，其中( **A > B** ，任务是检查 B 是否是 A 的前缀。打印**“是”**如果是前缀 Else 打印**“否”**。

**示例:**

> **输入:** A = 12345，B = 12
> **输出:**是
> 
> **输入:** A = 12345，B = 345
> **输出:**否

**进场:**

1.  将给定的数字 **A** 和 **B** 分别转换为字符串 **str1** 和 **str2** 。
2.  从字符串开始遍历两个字符串。
3.  遍历字符串时，如果 **str1** 和 **str2** 的任何索引字符不相等，则打印**“否”**。
4.  否则打印**“是”。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to check if B is a
// prefix of A or not
bool checkprefix(int A, int B)
{

    // Convert numbers into strings
    string s1 = to_string(A);
    string s2 = to_string(B);

    // Find the lengths of strings
    // s1 and s2
    int n1 = s1.length();
    int n2 = s2.length();

    // Base Case
    if (n1 < n2) {
        return false;
    }

    // Traverse the strings s1 & s2
    for (int i = 0; i < n2; i++) {

        // If at any index characters
        // are unequals then return false
        if (s1[i]
            != s2[i]) {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver Code
int main()
{
    // Given numbers
    int A = 12345, B = 12;

    // Function Call
    bool result = checkprefix(A, B);

    // If B is a prefix of A, then
    // print "Yes"
    if (result) {
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
class GFG{

// Function to check if B is a
// prefix of A or not
static boolean checkprefix(int A, int B)
{

    // Convert numbers into Strings
    String s1 = String.valueOf(A);
    String s2 = String.valueOf(B);

    // Find the lengths of Strings
    // s1 and s2
    int n1 = s1.length();
    int n2 = s2.length();

    // Base Case
    if (n1 < n2)
    {
        return false;
    }

    // Traverse the Strings s1 & s2
    for(int i = 0; i < n2; i++)
    {

        // If at any index characters
        // are unequals then return false
        if (s1.charAt(i) != s2.charAt(1))
        {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver Code
public static void main(String[] args)
{

    // Given numbers
    int A = 12345, B = 12;

    // Function call
    boolean result = checkprefix(A, B);

    // If B is a prefix of A, then
    // print "Yes"
    if (!result)
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check if B is
# a prefix of A or not
def checkprefix(A, B):

    # Convert numbers into strings
    s1 = str(A)
    s2 = str(B)

    # Find the length of s1 and s2
    n1 = len(s1)
    n2 = len(s2)

    # Base case
    if n1 < n2:
        return False

    # Traverse the string s1 and s2
    for i in range(0, n2):

        # If at any index characters
        # are unequal then return False
        if s1[i] != s2[i]:
            return False

    return True

# Driver code
if __name__=='__main__':

    # Given numbers
    A = 12345
    B = 12

    # Function call
    result = checkprefix(A, B)

    # If B is a prefix of A ,
    # then print Yes
    if result:
        print("Yes")
    else:
        print("No")

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if B is a
// prefix of A or not
static bool checkprefix(int A, int B)
{

    // Convert numbers into Strings
    String s1 = A.ToString();
    String s2 = B.ToString();

    // Find the lengths of Strings
    // s1 and s2
    int n1 = s1.Length;
    int n2 = s2.Length;

    // Base Case
    if (n1 < n2)
    {
        return false;
    }

    // Traverse the Strings s1 & s2
    for(int i = 0; i < n2; i++)
    {

        // If at any index characters
        // are unequals then return false
        if (s1[i] != s2[i])
        {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver Code
static public void Main ()
{

    // Given numbers
    int A = 12345, B = 12;

    // Function call
    bool result = checkprefix(A, B);

    // If B is a prefix of A, then
    // print "Yes"
    if (result)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if B is a
// prefix of A or not

function checkprefix( A,  B)
{

    // Convert numbers into Strings

    var s1 = A.toString();
    var s2 = B.toString();

    // Find the lengths of Strings
    // s1 and s2

    var n1 = s1.length;
    var n2 = s2.length;

    // Base Case
    if (n1 < n2)
    {
        return false;
    }

    // Traverse the Strings s1 & s2
    for(var i = 0; i < n2; i++)
    {

        // If at any index characters
        // are unequals then return false
        if (s1[i] != s2[i])
        {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver Code

    // Given numbers
    var A = 12345, B = 12;

    // Function call
    var result = checkprefix(A, B);

    // If B is a prefix of A, then
    // print "Yes"
    if (result)
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }

</script>

```

**Output:** 

```
Yes
```

**使用内置函数:**使用内置函数[**STD::boost::algorithm::starts _ with()**](https://www.geeksforgeeks.org/c-boost-string-algorithms-library/)，可以检查任意字符串是否包含另一字符串的前缀。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <boost/algorithm/string.hpp>
using namespace std;

// Function to check if B is a
// prefix of A or not
void checkprefix(int A, int B)
{

    // Convert numbers into strings
    string s1 = to_string(A);
    string s2 = to_string(B);

    bool result;

    // Check if s2 is a prefix of s1
    // or not using starts_with() function
    result = boost::algorithm::starts_with(s1, s2);

    // If result is true, print "Yes"
    if (result) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    // Given numbers
    int A = 12345, B = 12;

    // Function Call
    checkprefix(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if B is a
// prefix of A or not
static void checkprefix(int A, int B)
{

    // Convert numbers into Strings
    String s1 = String.valueOf(A);
    String s2 = String.valueOf(B);

    boolean result;

    // Check if s2 is a prefix of s1
    // or not using starts_with() function
    result = s1.startsWith(s2);

    // If result is true, print "Yes"
    if (result)
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given numbers
    int A = 12345, B = 12;

    // Function call
    checkprefix(A, B);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check if B is
# a prefix of A or not
def checkprefix(A, B):

    # Convert numbers into strings
    s1 = str(A)
    s2 = str(B)

    # Check if s2 is a prefix of s1
    # or not using startswith() function
    result = s1.startswith(s2)

    # If result is true print Yes
    if result:
        print("Yes")
    else:
        print("No")

# Driver code
if __name__=='__main__':

    # Given numbers
    A = 12345
    B = 12

    # Function call
    checkprefix(A, B)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System.Threading;
using System.Globalization;
using System;

class GFG{

// Function to check if B is a
// prefix of A or not
static void checkprefix(int A, int B)
{

    // Convert numbers into Strings
    string s1 = A.ToString();
    string s2 = B.ToString();

    bool result;

    // Check if s2 is a prefix of s1
    // or not using starts_with() function
    result = s1.StartsWith(s2, false,
        CultureInfo.InvariantCulture);

    // If result is true, print "Yes"
    if (result)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}

// Driver code
static void Main()
{

    // Given numbers
    int A = 12345, B = 12;

    // Function call
    checkprefix(A, B);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach
      // Function to check if B is a
      // prefix of A or not
      function checkprefix(A, B) {
        // Convert numbers into Strings
        var s1 = A.toString();
        var s2 = B.toString();

        var result;

        // Check if s2 is a prefix of s1
        // or not using starts_with() function
        result = s1.startsWith(s2);

        // If result is true, print "Yes"
        if (result) {
          document.write("Yes");
        } else {
          document.write("No");
        }
      }

      // Driver code
      // Given numbers
      var A = 12345,
        B = 12;

      // Function call
      checkprefix(A, B);

 </script>
```

**Output:** 

```
Yes
```