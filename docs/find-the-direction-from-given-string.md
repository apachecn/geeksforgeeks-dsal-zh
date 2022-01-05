# 从给定的字符串中找到方向

> 原文:[https://www . geeksforgeeks . org/从给定字符串中查找方向/](https://www.geeksforgeeks.org/find-the-direction-from-given-string/)

给定一个只包含左旋转和右旋转的字符串。任务是找到枢轴的最终方向(即北/东/南/西)。让一个支点指向罗盘上的北。

**示例:**

```
Input: str = "LLRLRRL"
Output: W
In this input string we rotate pivot to left
when a L char is encountered and right when 
R is encountered. 

Input: str = "LL"
Output: S
```

**进场:**

1.  使用一个在看到 R 时递增，在看到 l 时递减的计数器
2.  最后，在计数器上使用模来获得方向。
3.  如果计数为负，则方向将不同。检查代码是否也是负数。

下面是上述方法的实现:

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the final direction
string findDirection(string s)
{
    int count = 0;
    string d = "";

    for (int i = 0; i < s.length(); i++) {

        if (s[0] == '\n')
            return NULL;

        if (s[i] == 'L')
            count--;
        else {
            if (s[i] == 'R')
                count++;
        }
    }

    // if count is positive that implies
    // resultant is clockwise direction
    if (count > 0) {

        if (count % 4 == 0)
            d = "N";
        else if (count % 4 == 1)
            d = "E";
        else if (count % 4 == 2)
            d = "S";
        else if (count % 4 == 3)
            d = "W";
    }

    // if count is negative that implies
    // resultant is anti-clockwise direction
    if (count < 0) {

        if (count % 4 == 0)
            d = "N";
        else if (count % 4 == -1)
            d = "W";
        else if (count % 4 == -2)
            d = "S";
        else if (count % 4 == -3)
            d = "E";
    }
    return d;
}

// Driver code
int main()
{
    string s = "LLRLRRL";
    cout << (findDirection(s)) << endl;

    s = "LL";
    cout << (findDirection(s)) << endl;
}

// This code is contributed by
// SURENDRA_GANGWAR
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG {

    // Function to find the final direction
    static String findDirection(String s)
    {
        int count = 0;
        String d = "";

        for (int i = 0; i < s.length(); i++) {

            if (s.charAt(0) == '\n')
                return null;

            if (s.charAt(i) == 'L')
                count--;
            else {
                if (s.charAt(i) == 'R')
                    count++;
            }
        }

        // if count is positive that implies
        // resultant is clockwise direction
        if (count > 0) {

            if (count % 4 == 0)
                d = "N";
            else if (count % 4 == 1)
                d = "E";
            else if (count % 4 == 2)
                d = "S";
            else if (count % 4 == 3)
                d = "W";
        }

        // if count is negative that implies
        // resultant is anti-clockwise direction
        if (count < 0) {

            if (count % 4 == 0)
                d = "N";
            else if (count % 4 == -1)
                d = "W";
            else if (count % 4 == -2)
                d = "S";
            else if (count % 4 == -3)
                d = "E";
        }
        return d;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "LLRLRRL";
        System.out.println(findDirection(s));

        s = "LL";
        System.out.println(findDirection(s));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to find the
# final direction

def findDirection(s):

    count = 0
    d = ""

    for i in range(len(s)):
        if (s[i] == 'L'):
            count -= 1
        else:
            if (s[i] == 'R'):
                count += 1

    # if count is positive that
    # implies resultant is clockwise
    # direction
    if (count > 0):
        if (count % 4 == 0):
            d = "N"
        elif (count % 4 == 10):
            d = "E"
        elif (count % 4 == 2):
            d = "S"
        elif (count % 4 == 3):
            d = "W"

    # if count is negative that
    # implies resultant is anti-
    # clockwise direction
    if (count < 0):
        count *= -1
        if (count % 4 == 0):
            d = "N"
        elif (count % 4 == 1):
            d = "W"
        elif (count % 4 == 2):
            d = "S"
        elif (count % 4 == 3):
            d = "E"

    return d

# Driver code
if __name__ == '__main__':

    s = "LLRLRRL"
    print(findDirection(s))

    s = "LL"
    print(findDirection(s))

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    // Function to find the final direction
    static String findDirection(String s)
    {
        int count = 0;
        String d = "";

        for (int i = 0; i < s.Length; i++) {

            if (s[0] == '\n')
                return null;

            if (s[i] == 'L')
                count--;
            else {
                if (s[i] == 'R')
                    count++;
            }
        }

        // if count is positive that implies
        // resultant is clockwise direction
        if (count > 0) {

            if (count % 4 == 0)
                d = "N";
            else if (count % 4 == 1)
                d = "E";
            else if (count % 4 == 2)
                d = "S";
            else if (count % 4 == 3)
                d = "W";
        }

        // if count is negative that implies
        // resultant is anti-clockwise direction
        if (count < 0) {

            if (count % 4 == 0)
                d = "N";
            else if (count % 4 == -1)
                d = "W";
            else if (count % 4 == -2)
                d = "S";
            else if (count % 4 == -3)
                d = "E";
        }
        return d;
    }

    // Driver code
    public static void Main()
    {
        String s = "LLRLRRL";
        Console.WriteLine(findDirection(s));

        s = "LL";
        Console.WriteLine(findDirection(s));
    }
}

// This code is contributed by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the final direction
function findDirection($s)
{
    $count = 0;
    $d = "";

    for ($i = 0;
         $i < strlen($s); $i++)
    {
        if ($s[0] == '\n')
            return null;

        if ($s[$i] == 'L')
            $count -= 1;
        else
        {
            if ($s[$i] == 'R')
                $count += 1;
        }
    }

    // if count is positive that implies
    // resultant is clockwise direction
    if ($count > 0)
    {
        if ($count % 4 == 0)
            $d = "N";
        else if ($count % 4 == 1)
            $d = "E";
        else if ($count % 4 == 2)
            $d = "S";
        else if ($count % 4 == 3)
            $d = "W";
    }

    // if count is negative that
    // implies resultant is
    // anti-clockwise direction
    if ($count < 0)
    {
        if ($count % 4 == 0)
            $d = "N";
        else if ($count % 4 == -1)
            $d = "W";
        else if ($count % 4 == -2)
            $d = "S";
        else if ($count % 4 == -3)
            $d = "E";
    }
    return $d;
}

// Driver code
$s = "LLRLRRL";
echo findDirection($s)."\n";

$s = "LL";
echo findDirection($s)."\n";

// This code is contributed
// by ChitraNayal   
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function to find the final direction
    function findDirection(s)
    {
        let count = 0;
        let d = "";

        for (let i = 0; i < s.length; i++) {

            if (s[0] == '\n')
                return null;

            if (s[i] == 'L')
                count--;
            else {
                if (s[i] == 'R')
                    count++;
            }
        }

        // if count is positive that implies
        // resultant is clockwise direction
        if (count > 0) {

            if (count % 4 == 0)
                d = "N";
            else if (count % 4 == 1)
                d = "E";
            else if (count % 4 == 2)
                d = "S";
            else if (count % 4 == 3)
                d = "W";
        }

        // if count is negative that implies
        // resultant is anti-clockwise direction
        if (count < 0) {

            if (count % 4 == 0)
                d = "N";
            else if (count % 4 == -1)
                d = "W";
            else if (count % 4 == -2)
                d = "S";
            else if (count % 4 == -3)
                d = "E";
        }
        return d;
    }

    let s = "LLRLRRL";
    document.write(findDirection(s) + "</br>");

    s = "LL";
    document.write(findDirection(s));

        // This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
W
S
```

**时间复杂度:** O(N)其中 N 为弦的长度
T3】辅助空间: O(1)