# 检查一个数字是否以另一个数字结束

> 原文:[https://www . geesforgeks . org/check-if-a-number-end-other-number-or-not/](https://www.geeksforgeeks.org/check-if-a-number-ends-with-another-number-or-not/)

给定两个数字 **A** 和 **B** ，其中( **A > B** ，任务是检查 B 是否是 A 的后缀。打印**“是”**如果是后缀 Else 打印**“否”**。
**举例:**

> **输入:** A = 12345，B = 45
> **输出:**是
> **输入:** A = 12345，B = 123
> **输出:**否

**方法 1:**

1.  将给定的数字 **A 和 B** 分别转换为字符串 **str1** 和 **str2** 。
2.  从字符串的末尾开始遍历两个字符串。
3.  遍历字符串时，如果 **str1** 和 **str2** 的任何索引字符不相等，则打印**“否”**。
4.  否则打印**“是”。**

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to check if B is a
// suffix of A or not
bool checkSuffix(int A, int B)
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
        if (s1[n1 - i - 1]
            != s2[n2 - i - 1]) {
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
    int A = 12345, B = 45;

    // Function Call
    bool result = checkSuffix(A, B);

    // If B is a suffix of A, then
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

// Function to check if B  
// is a suffix of A or not
public static boolean checkSuffix(int A,
                                  int B)
{

    // Convert numbers into strings
    String s1 = String.valueOf(A);
    String s2 = String.valueOf(B);

    // Find the lengths of strings
    // s1 and s2
    int n1 = s1.length();
    int n2 = s2.length();

    // Base case
    if (n1 < n2)
    {
        return false;
    }

    // Traverse the strings s1 & s2
    for(int i = 0; i < n2; i++)
    {

       // If at any index characters
       // are unequals then return false
       if (s1.charAt(n1 - i - 1) !=
           s2.charAt(n2 - i - 1))
       {
           return false;
       }
    }

    // Return true
    return true;
}

// Driver code
public static void main(String[] args)
{

    // Given numbers
    int A = 12345, B = 45;

    // Function Call
    boolean result = checkSuffix(A, B);

    // If B is a suffix of A, 
    // then print "Yes"
    if (result)
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if B is a
# suffix of A or not
def checkSuffix(A, B):

    # Convert numbers into strings
    s1 = str(A);
    s2 = str(B);

    # Find the lengths of strings
    # s1 and s2
    n1 = len(s1)
    n2 = len(s2)

    # Base Case
    if (n1 < n2):
        return False;

    # Traverse the strings s1 & s2
    for i in range(n2):

        # If at any index characters
        # are unequals then return false
        if (s1[n1 - i - 1] != s2[n2 - i - 1]):
            return False;

    # Return true
    return True;

# Driver Code

# Given numbers
A = 12345
B = 45;

# Function Call
result = checkSuffix(A, B);

# If B is a suffix of A, then
# print "Yes"
if (result):
    print("Yes")
else:
    print("No")

# This code is contributed by grand_master   
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if B
// is a suffix of A or not
public static bool checkSuffix(int A,
                               int B)
{

    // Convert numbers into strings
    string s1 = A.ToString();
    string s2 = B.ToString();

    // Find the lengths of strings
    // s1 and s2
    int n1 = s1.Length;
    int n2 = s2.Length;

    // Base case
    if (n1 < n2)
    {
        return false;
    }

    // Traverse the strings s1 & s2
    for(int i = 0; i < n2; i++)
    {

        // If at any index characters
        // are unequals then return false
        if (s1[n1 - i - 1] !=  s2[n2 - i - 1])
        {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver code
public static void Main(string[] args)
{

    // Given numbers
    int A = 12345, B = 45;

    // Function Call
    bool result = checkSuffix(A, B);

    // If B is a suffix of A,
    // then print "Yes"
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

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if B
// is a suffix of A or not

    function checkSuffix( A, B)
{

    // Convert numbers into strings
    var s1 = A.toString();
    var s2 = B.toString();

    // Find the lengths of strings
    // s1 and s2

    var n1 = s1.length;
    var n2 = s2.length;

    // Base case
    if (n1 < n2)
    {
        return false;
    }

    // Traverse the strings s1 & s2
    for(var i = 0; i < n2; i++)
    {

        // If at any index characters
        // are unequals then return false
        if (s1[n1 - i - 1] !=  s2[n2 - i - 1])
        {
            return false;
        }
    }

    // Return true
    return true;
}

// Driver code

    // Given numbers
    var A = 12345, B = 45;

    // Function Call
    var result = checkSuffix(A, B);

    // If B is a suffix of A,
    // then print "Yes"
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

**方法二:**使用内置函数**STD::Boost::algorithm::ends _ with()**包含在 C++ 的 [Boost 库中，用于检查某个字符串是否包含另一个字符串的后缀。
以下是上述方法的实现:](https://www.geeksforgeeks.org/advanced-c-boost-library/) 

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <boost/algorithm/string.hpp>
using namespace std;

// Function to check if B is a
// suffix of A or not
void checkSuffix(int A, int B)
{

    // Convert numbers into strings
    string s1 = to_string(A);
    string s2 = to_string(B);

    bool result;

    // Check if s2 is a suffix of s1
    // or not using ends_with() function
    result = boost::algorithm::ends_with(s1,
                                         s2);

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
    int A = 12345, B = 45;

    // Function Call
    checkSuffix(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if B is a
// suffix of A or not
static void checkSuffix(int A, int B)
{

    // Convert numbers into Strings
    String s1 = String.valueOf(A);
    String s2 = String.valueOf(B);

    boolean result;

    // Check if s2 is a suffix of s1
    // or not
    result = s1.endsWith(s2);

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
    int A = 12345, B = 45;

    // Function Call
    checkSuffix(A, B);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if B is
# a suffix of A or not
def checkSuffix(A, B):

    # Convert numbers into strings
    s1 = str(A)
    s2 = str(B)

    # Check if s2 is a suffix of s1
    # or not
    result = s1.endswith(s2)

    # If result is true print "Yes"
    if (result):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':

    # Given numbers
    A = 12345
    B = 45

    # Function call
    checkSuffix(A, B)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if B is a
// suffix of A or not
static void checkSuffix(int A, int B)
{

    // Convert numbers into Strings
    String s1 = String.Join("", A);
    String s2 = String.Join("", B);

    bool result;

    // Check if s2 is a suffix of s1
    // or not
    result = s1.EndsWith(s2);

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

// Driver Code
public static void Main(String[] args)
{
    // Given numbers
    int A = 12345, B = 45;

    // Function Call
    checkSuffix(A, B);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if B is a
// suffix of A or not
function checkSuffix( A, B)
{

    // Convert numbers into Strings
    let s1 = A.toString();
    let s2 = B.toString();

    let result;

    // Check if s2 is a suffix of s1
    // or not
    result = s1.endsWith(s2);

    // If result is true, print "Yes"
    if (result)
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }
}

// Driver Code

    // Given numbers
    let A = 12345, B = 45;

    // Function Call
    checkSuffix(A, B);

</script>
```

**Output:** 

```
Yes
```

**方法三:**

1.  从 **A** 中减去 **B** 。
2.  使用[这篇](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)文章中讨论的**方法 3** 找到 B 中的位数(比如 **X** )。
3.  检查 **A** 是否以至少 **X** 数字零结尾。如果是，则打印**“是”**。
4.  否则打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <boost/algorithm/string.hpp>
using namespace std;

// Function to check if B is a
// suffix of A or not
bool checkSuffix(int A, int B)
{

    // Find the number of digit in B
    int digit_B = log10(B) + 1;

    // Subtract B from A
    A -= B;

    // Returns true,
    // if B is a suffix of A
    return (A % int(pow(10, digit_B)));
}

// Driver Code
int main()
{
    // Given numbers
    int A = 12345, B = 45;

    // Function Call
    bool result = checkSuffix(A, B);

    // If B is a suffix of A, then
    // print "Yes"
    if (!result) {
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

// Function to check if B
// is a suffix of A or not
static boolean checkSuffix(int A, int B)
{

    // Find the number of digit in B
    int digit_B = (int) (Math.log10(B) + 1);

    // Subtract B from A
    A -= B;

    // Returns true,
    // if B is a suffix of A
    return (A % (int)(Math.pow(10, digit_B)) > 0);
}

// Driver code
public static void main(String[] args)
{

    // Given numbers
    int A = 12345, B = 45;

    // Function call
    boolean result = checkSuffix(A, B);

    // If B is a suffix of A,
    // then print "Yes"
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

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if B is a
# suffix of A or not
def checkSuffix(A, B):

    # Find the number of digit in B
    digit_B = int(math.log10(B)) + 1;

    # Subtract B from A
    A -= B;

    # Returns true,
    # if B is a suffix of A
    return (A % int(math.pow(10, digit_B)));

# Driver Code

# Given numbers
A = 12345; B = 45;

# Function Call
result = checkSuffix(A, B);

# If B is a suffix of A, then
# print "Yes"
if (result == 0):
    print("Yes");

else:
    print("No");

# This code is contributed by Nidhi_biet
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if B
// is a suffix of A or not
static bool checkSuffix(int A, int B)
{

    // Find the number of digit in B
    int digit_B = (int)(Math.Log10(B) + 1);

    // Subtract B from A
    A -= B;

    // Returns true,
    // if B is a suffix of A
    return (A % (int)(Math.Pow(10, digit_B)) > 0);
}

// Driver code
public static void Main()
{

    // Given numbers
    int A = 12345, B = 45;

    // Function call
    bool result = checkSuffix(A, B);

    // If B is a suffix of A,
    // then print "Yes"
    if (!result)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if B
    // is a suffix of A or not
    function checkSuffix(A, B)
    {

        // Find the number of digit in B
        let digit_B = parseInt(Math.log10(B) + 1, 10);

        // Subtract B from A
        A -= B;

        // Returns true,
        // if B is a suffix of A
        return (A % (Math.pow(10, digit_B)) > 0);
    }

    // Given numbers
    let A = 12345, B = 45;

    // Function call
    let result = checkSuffix(A, B);

    // If B is a suffix of A,
    // then print "Yes"
    if (!result)
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

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*