# 检查二进制字符串中的所有 1 是否等距

> 原文:[https://www . geesforgeks . org/check-如果二进制字符串中的所有 1 都是等距或非等距/](https://www.geeksforgeeks.org/check-if-all-the-1s-in-a-binary-string-are-equidistant-or-not/)

给定一个二进制字符串 **str** ，任务是检查字符串中所有的 **1 的**是否等距。术语等距是指每两个相邻的 **1 的**之间的距离相同。**注意**弦至少包含两个 **1 的**。

**示例:**

> **输入:** str = "00111000"
> **输出:**是
> 所有 1 之间的距离相同，等于 1。
> 
> **输入:** str = "0101001"
> **输出:**否
> 1<sup>ST</sup>与 2 <sup>nd</sup> 1 的距离为 2
> ，2 <sup>nd</sup> 与 3 <sup>rd</sup> 1 的距离为 3。

**方法:**将字符串中所有 **1 的**的位置存储在一个向量中，然后检查每两个连续位置之间的差异是否相同。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#include <stdio.h>
using namespace std;

// Function that returns true if all the 1's
// in the binary string s are equidistant
bool check(string s, int l)
{

    // Initialize vector to store
    // the position of 1's
    vector<int> pos;

    for (int i = 0; i < l; i++) {

        // Store the positions of 1's
        if (s[i] == '1')
            pos.push_back(i);
    }

    // Size of the position vector
    int t = pos.size();
    for (int i = 1; i < t; i++) {

        // If condition isn't satisfied
        if ((pos[i] - pos[i - 1]) != (pos[1] - pos[0]))
            return false;
    }

    return true;
}

// Drivers code
int main()
{
    string s = "100010001000";
    int l = s.length();
    if (check(s, l))
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

// Function that returns true if all the 1's
// in the binary string s are equidistant
static boolean check(String s, int l)
{

    // Initialize vector to store
    // the position of 1's
    Vector<Integer> pos = new Vector<Integer>();

    for (int i = 0; i < l; i++)
    {

        // Store the positions of 1's
        if (s.charAt(i)== '1')
            pos.add(i);
    }

    // Size of the position vector
    int t = pos.size();
    for (int i = 1; i < t; i++)
    {

        // If condition isn't satisfied
        if ((pos.get(i) - pos.get(i-1)) != (pos.get(1) - pos.get(0)))
            return false;
    }

    return true;
}

// Drivers code
public static void main(String args[])
{
    String s = "100010001000";
    int l = s.length();
    if (check(s, l))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if all the 1's
# in the binary s are equidistant
def check(s, l):

    # Initialize vector to store
    # the position of 1's
    pos = []

    for i in range(l):

        # Store the positions of 1's
        if (s[i] == '1'):
            pos.append(i)

    # Size of the position vector
    t = len(pos)
    for i in range(1, t):

        # If condition isn't satisfied
        if ((pos[i] -
             pos[i - 1]) != (pos[1] -
                             pos[0])):
            return False

    return True

# Driver code
s = "100010001000"
l = len(s)
if (check(s, l)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function that returns true if all the 1's
// in the binary string s are equidistant
static bool check(String s, int l)
{

    // Initialize vector to store
    // the position of 1's
    List<int> pos = new List<int>();

    for (int i = 0; i < l; i++)
    {

        // Store the positions of 1's
        if (s[i]== '1')
        {

            pos.Add(i);
        }
    }

    // Size of the position vector
    int t = pos.Count;
    for (int i = 1; i < t; i++)
    {

        // If condition isn't satisfied
        if ((pos[i] - pos[i - 1]) != (pos[1] - pos[0]))
            return false;
    }

    return true;
}

// Drivers code
public static void Main(String []args)
{
    String s = "100010001000";
    int l = s.Length;
    if (check(s, l))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if all the 1's
// in the binary string s are equidistant
function check(s, l)
{

    // Initialize vector to store
    // the position of 1's
    var pos = [];

    for(var i = 0; i < l; i++)
    {

        // Store the positions of 1's
        if (s[i] == '1')
            pos.push(i);
    }

    // Size of the position vector
    var t = pos.length;
    for(var i = 1; i < t; i++)
    {

        // If condition isn't satisfied
        if ((pos[i] - pos[i - 1]) !=
            (pos[1] - pos[0]))
            return false;
    }
    return true;
}

// Drivers code
var s = "100010001000";
var l = s.length;

if (check(s, l))
    document.write( "Yes");
else
    document.write("No");

// This code is contributed by noob2000

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)，其中 N 是字符串的长度。