# 倒置时检查号码是否有效

> 原文:[https://www . geeksforgeeks . org/check-number-is-valid-what-flip-over-inverted/](https://www.geeksforgeeks.org/check-if-the-number-is-valid-when-flipped-upside-down/)

给定一个代表一个数字的字符串 **str** ，任务是找出这个数字是否有效，如果它颠倒了。
**例:**

> **输入:** str = "1183"
> **输出:**是
> 颠倒(1183) = 1183
> **输入:** str = "983"
> **输出:**否

**进场:**只有 **1** 、 **3** 和 **8** 这几个数字，在颠倒过来的时候，才能形成另一个有效数字。如果数字中包含这些数字以外的数字，则打印**否**否则打印**是**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// str is Topsy Turvy
bool topsyTurvy(string str)
{

    // For every character of the string
    for (int i = 0; i < str.length(); i++) {

        // If the current digit cannot form a
        // valid digit when turned upside-down
        if (str[i] == '2' || str[i] == '4'
            || str[i] == '5' || str[i] == '6'
            || str[i] == '7' || str[i] == '9') {
            return false;
        }
    }

    return true;
}

// Driver code
int main()
{
    string str = "1234";

    if (topsyTurvy(str))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if
// str is Topsy Turvy
static boolean topsyTurvy(char[] str)
{

    // For every character of the string
    for (int i = 0; i < str.length; i++)
    {

        // If the current digit cannot form a
        // valid digit when turned upside-down
        if (str[i] == '2' || str[i] == '4' ||
            str[i] == '5' || str[i] == '6' ||
            str[i] == '7' || str[i] == '9')
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    String str = "1234";

    if (topsyTurvy(str.toCharArray()))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if
# str is Topsy Turvy
def topsyTurvy(string) :

    # For every character of the string
    for i in range(len(string)) :

        # If the current digit cannot form a
        # valid digit when turned upside-down
        if (string[i] == '2' or string[i] == '4' or
            string[i] == '5' or string[i] == '6' or
            string[i] == '7' or string[i] == '9') :
            return False;

    return True;

# Driver code
if __name__ == "__main__" :

    string = "1234";

    if (topsyTurvy(string)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function that returns true if
// str is Topsy Turvy
static bool topsyTurvy(char[] str)
{

    // For every character of the string
    for (int i = 0; i < str.Length; i++)
    {

        // If the current digit cannot form a
        // valid digit when turned upside-down
        if (str[i] == '2' || str[i] == '4' ||
            str[i] == '5' || str[i] == '6' ||
            str[i] == '7' || str[i] == '9')
        {
            return false;
        }
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    String str = "1234";

    if (topsyTurvy(str.ToCharArray()))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if
// str is Topsy Turvy
function topsyTurvy( str)
{

    // For every character of the string
    for (var i = 0; i < str.length; i++) {

        // If the current digit cannot form a
        // valid digit when turned upside-down
        if (str[i] == '2' || str[i] == '4'
            || str[i] == '5' || str[i] == '6'
            || str[i] == '7' || str[i] == '9') {
            return false;
        }
    }

    return true;
}

// Driver code
var str = "1234";
if (topsyTurvy(str))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
No
```