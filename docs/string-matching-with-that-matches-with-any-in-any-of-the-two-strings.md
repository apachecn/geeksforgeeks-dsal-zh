# 在任意两个字符串中匹配有*(匹配任意)的字符串

> 原文:[https://www . geesforgeks . org/string-matching-with-with-matching-in-any-in-two-string/](https://www.geeksforgeeks.org/string-matching-with-that-matches-with-any-in-any-of-the-two-strings/)

给你两个字符串 A 和 b。字符串还包含特殊字符*。您可以用任何字母字符替换*。最后，您必须判断是否有可能使两个字符串相同。
**例:**

```
Input : A = "gee*sforgeeks"
        B = "geeksforgeeks"
Output :Yes

Input :A = "abs*"
       B = "abds"
Output :No
```

**说明:**如何解决以上问题，基本上我们三种情况，
情况 1:两个字符串在特定位置都包含*号，这时候我们可以用任意字符替换两个*号，使字符串在那个位置相等。
情况 2:如果一个字符串在该位置有字符，另一个字符串在该位置有*。因此，我们可以在其他字符串中用相同的字符替换*。
例 3:如果两个字符串在那个位置都有一个字符，那么它们一定是相同的，否则我们不能使它们相等。

## C++

```
// CPP program for string matching with *
#include <bits/stdc++.h>
using namespace std;

bool doMatch(string A, string B)
{
    for (int i = 0; i < A.length(); i++)

        // if the string don't have *
        // then character at that position
        // must be same.
        if (A[i] != '*' && B[i] != '*')
            if (A[i] != B[i])
               return false;

    return true;
}

int main()
{
    string A = "gee*sforgeeks";
    string B = "geeksforgeeks";
    cout << doMatch(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for string matching with *
import java.util.*;

public class GfG {

    // Function to check if the two
    // strings can be matched or not
    public static int doMatch(String A, String B) {

        for (int i = 0; i < A.length(); i++){

            // if the string don't have *
            // then character at that position
            // must be same.
            if (A.charAt(i) != '*' && B.charAt(i) != '*'){ 
                if (A.charAt(i) != B.charAt(i))
                   return 0;
            }
        }

        return 1;
    }

    // Driver code
    public static void main(String []args){

        String A = "gee*sforgeeks";
        String B = "geeksforgeeks";
        System.out.println(doMatch(A, B));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 program for string
# matching with *

def doMatch(A, B):

    for i in range(len(A)):

        # if the string don't have *
        # then character t that position
        # must be same.
        if A[i] != '*' and B[i] != '*':
            if A[i] != B[i]:
                return False
    return True

#Driver code
if __name__=='__main__':
    A = "gee*sforgeeks"
    B = "geeksforgeeks"
    print(int(doMatch(A, B)))

# this code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program for string matching with
using System;

class GfG
{

    // Function to check if the two
    // strings can be matched or not
    public static int doMatch(String A, String B)
    {

        for (int i = 0; i < A.Length; i++)
        {

            // if the string don't have *
            // then character at that position
            // must be same.
            if (A[i] != '*' && B[i] != '*')
                if (A[i] != B[i])
                    return 0;
        }

        return 1;
    }

    // Driver code
    public static void Main(String []args)
    {
        String A = "gee*sforgeeks";
        String B = "geeksforgeeks";
        Console.WriteLine(doMatch(A, B));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for string matching with *

function doMatch($A, $B)
{
    for ($i = 0; $i < strlen($A); $i++)

        // if the string don't have *
        // then character at that position
        // must be same.
        if ($A[$i] != '*' && $B[$i] != '*')
            if ($A[$i] != $B[$i])
            return false;

    return true;
}

// Driver Code
$A = "gee*sforgeeks";
$B = "geeksforgeeks";
echo doMatch($A, $B);

// This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>
// javascript program for string matching with * public class GfG {

    // Function to check if the two
    // strings can be matched or not
    function doMatch(A, B)
    {

        for (i = 0; i < A.length; i++)
        {

            // if the string don't have *
            // then character at that position
            // must be same.
            if (A.charAt(i) != '*' && B.charAt(i) != '*')
            {
                if (A.charAt(i) != B.charAt(i))
                    return 0;
            }
        }

        return 1;
    }

    // Driver code
        var A = "gee*sforgeeks";
        var B = "geeksforgeeks";
        document.write(doMatch(A, B));

// This code is contributed by aashish1995.
</script>
```

**Output:** 

```
1
```