# 检查从不同点出发的两个人是否相遇

> 原文:[https://www . geesforgeks . org/check-if-two-people-from-from-points-ever-meeting/](https://www.geeksforgeeks.org/check-if-two-people-starting-from-different-points-ever-meet/)

有两个人从两个不同的位置开始，比如 x1 和 x2。两者都可以分别向前跳 v1 和 v2 米。我们必须找到两者是否会相遇，因为两者的跳跃次数必须相同。
打‘是’如果他们会见面，
打‘否’他们不会。

**示例:**

```
Input  : x1 = 5, v1 = 8, x2 = 4, v2 = 7
Output : No
Explanation: The first person is starting ahead of the second one.
and his speed is also greater than the second one, so they will never meet.

Input  : x1 = 6, v1 = 6, x2 = 4, v2 = 8
Output : Yes
```

**天真的做法:**在这种情况下，我们计算每个人每次跳跃后的位置，并检查他们是否已经降落在同一个地点。这个有复杂性 O(n)。

## C++

```
// C++ program to find if two people
// starting from different positions
// ever meet or not.
#include <bits/stdc++.h>
using namespace std;

bool everMeet(int x1, int x2, int v1, int v2)
{
    // If speed of a person at a position before
    // other person is smaller, then return false.
    if (x1 < x2 && v1 <= v2)
       return false;
    if (x1 > x2 && v1 >=v2)
       return false; 

    // Making sure that x1 is greater
    if (x1 < x2)
    {
        swap(x1, x2);
        swap(v1, v2);
    }    

     // Until one person crosses other
     while (x1 >= x2) {
        if (x1 == x2)
            return true;

        // first person taking one
        // jump in each iteration
        x1 = x1 + v1;

        // second person taking
        // one jump in each iteration
        x2 = x2 + v2;
    }

    return false;  
}

// Driver code
int main()
{
    int x1 = 5, v1 = 8, x2 = 4, v2 = 7;
    if (everMeet(x1, x2, v1, v2))
        printf("Yes");   
    else
        printf("No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// if two people starting
// from different positions
// ever meet or not.
import java.io.*;

class GFG
{
    static void swap(int a, int b)
    {
        int t = a;
        a = b;
        b = t;
    }
    static boolean everMeet(int x1, int x2,
                            int v1, int v2)
    {
        // If speed of a person
        // at a position before
        // other person is smaller,
        // then return false.
        if (x1 < x2 && v1 <= v2)
        return false;
        if (x1 > x2 && v1 >= v2)
        return false;

        // Making sure that
        // x1 is greater
        if (x1 < x2)
        {
            swap(x1, x2);
            swap(v1, v2);
        }

        // Until one person
        // crosses other
        while (x1 >= x2)
        {
            if (x1 == x2)
                return true;

            // first person taking one
            // jump in each iteration
            x1 = x1 + v1;

            // second person taking
            // one jump in each iteration
            x2 = x2 + v2;
        }

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int x1 = 5, v1 = 8,
            x2 = 4, v2 = 7;
        if (everMeet(x1, x2, v1, v2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python3 program to find if two
# people starting from different
# positions ever meet or not.

def everMeet(x1, x2, v1, v2):

    # If speed of a person at
    # a position before other
    # person is smaller, then
    # return false.
    if (x1 < x2 and v1 <= v2):
        return False;
    if (x1 > x2 and v1 >= v2):
        return False;

    # Making sure that
    # x1 is greater
    if (x1 < x2):

        x1, x2 = x2,x1;
        v1, v2 = v2,v1;

    # Until one person
    # crosses other
    while (x1 >= x2):

        if (x1 == x2):
            return True;

        # first person taking one
        # jump in each iteration
        x1 = x1 + v1;

        # second person taking
        # one jump in each iteration
        x2 = x2 + v2;

    return False;

# Driver code
x1 = 5;
v1 = 8;
x2 = 4;
v2 = 7;
if (everMeet(x1, x2,v1, v2)):
    print("Yes");
else:
    print("No");

# This code is contributed by mits
```

## C#

```
// C# program to find if two
// people starting from different
// positions ever meet or not.
using System;

class GFG
{
    static void swap(ref int a,
                     ref int b)
    {
        int t = a;
        a = b;
        b = t;
    }
    static bool everMeet(int x1, int x2,
                         int v1, int v2)
    {
        // If speed of a person at a
        // position before other person
        // is smaller, then return false.
        if (x1 < x2 && v1 <= v2)
        return false;
        if (x1 > x2 && v1 >= v2)
        return false;

        // Making sure that x1 is greater
        if (x1 < x2)
        {
            swap(ref x1, ref x2);
            swap(ref v1, ref v2);
        }

        // Until one person crosses other
        while (x1 >= x2)
        {
            if (x1 == x2)
                return true;

            // first person taking one
            // jump in each iteration
            x1 = x1 + v1;

            // second person taking
            // one jump in each iteration
            x2 = x2 + v2;
        }

        return false;
    }

    // Driver code
    static void Main()
    {
        int x1 = 5, v1 = 8,
            x2 = 4, v2 = 7;
        if (everMeet(x1, x2, v1, v2))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if two
// people starting from different
// positions ever meet or not.

function everMeet($x1, $x2,
                  $v1, $v2)
{
    // If speed of a person at
    // a position before other
    // person is smaller, then
    // return false.
    if ($x1 < $x2 && $v1 <=$v2)
        return false;
    if ($x1 > $x2 && $v1 >= $v2)
        return false;

    // Making sure that
    // x1 is greater
    if ($x1 < $x2)
    {
        list($x1, $x2) = array($x2,
                               $x1);
        list($v1, $v2) = array($v2,
                               $v1);

    }

    // Until one person
    // crosses other
    while ($x1 >= $x2)
    {
        if ($x1 == $x2)
            return true;

        // first person taking one
        // jump in each iteration
        $x1 = $x1 + $v1;

        // second person taking
        // one jump in each iteration
        $x2 = $x2 + $v2;
    }

    return false;
}

// Driver code
$x1 = 5;
$v1 = 8;
$x2 = 4;
$v2 = 7;
if (everMeet($x1, $x2,
             $v1, $v2))
    echo "Yes";
else
    echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // if two people starting
    // from different positions
    // ever meet or not.

    function swap(a, b)
    {
        let t = a;
        a = b;
        b = t;
    }

    function everMeet(x1, x2, v1, v2)
    {
        // If speed of a person
        // at a position before
        // other person is smaller,
        // then return false.
        if (x1 < x2 && v1 <= v2)
            return false;
        if (x1 > x2 && v1 >= v2)
            return false;

        // Making sure that
        // x1 is greater
        if (x1 < x2)
        {
            swap(x1, x2);
            swap(v1, v2);
        }

        // Until one person
        // crosses other
        while (x1 >= x2)
        {
            if (x1 == x2)
                return true;

            // first person taking one
            // jump in each iteration
            x1 = x1 + v1;

            // second person taking
            // one jump in each iteration
            x2 = x2 + v2;
        }

        return false;
    }

    let x1 = 5, v1 = 8, x2 = 4, v2 = 7;
    if (everMeet(x1, x2, v1, v2))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output:** 

```
No
```