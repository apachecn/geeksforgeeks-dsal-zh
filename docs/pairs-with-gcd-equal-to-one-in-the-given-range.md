# 给定范围内 GCD 等于 1 的对

> 原文:[https://www . geesforgeks . org/pairs-with-gcd-等于给定范围内的 1/](https://www.geeksforgeeks.org/pairs-with-gcd-equal-to-one-in-the-given-range/)

给定一个范围，即 L 和 R，任务是找出我们是否能形成对，使得每对的 GCD 为 1。L-R 范围内的每个数字都应该正好包含在一对中。
**例:**

```
Input: L = 1, R = 8
Output: Yes
{2, 7}, {4, 1}, {3, 8}, {6, 5}
All pairs have GCD as 1\. 

Input: L = 2, R = 4
Output: No
```

**接近**:因为范围(L，R)中的每个数字在每对中必须恰好包含一次。因此，如果 L-R 是一个偶数，那么它是不可能的。如果 L-R 是奇数，则打印所有相邻对，因为相邻对的 GCD 始终为 1。
以下是上述办法的实施情况:

## C++

```
// C++ program to print all pairs
#include <bits/stdc++.h>
using namespace std;

// Function to print all pairs
bool checkPairs(int l, int r)
{
    // check if even
    if ((l - r) % 2 == 0)
        return false;

    /* We can print all adjacent pairs
      for (int i = l; i < r; i += 2) {
          cout << "{" << i << ", " << i + 1 << "}, ";
      } */

    return true;
}

// Driver Code
int main()
{
    int l = 1, r = 8;
    if (checkPairs(l, r))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all pairs
class GFG
{
// Function to print all pairs
static boolean checkPairs(int l, int r)
{
    // check if even
    if ((l - r) % 2 == 0)
        return false;

    /* We can print all adjacent pairs
    for (int i = l; i < r; i += 2)
    {
        System.out.print("{"+i+", "+i + 1+"}, ");
    } */

    return true;
}

// Driver Code
public static void main(String[] args)
{
    int l = 1, r = 8;
    if (checkPairs(l, r))
    System.out.println("Yes");
    else
    System.out.println("No");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to print all pairs

# Function to print all pairs
def checkPairs(l, r) :

    # check if even
    if (l - r) % 2 == 0 :
        return False

    """ we can print all adjacent pairs
    for i in range(l,r,2) :
        print("{",i,",",i + 1, "},")
    """

    return True

# Driver Code
if __name__ == "__main__" :

    l, r = 1, 8

    if checkPairs(l, r) :
        print("Yes")
    else :
        print("No")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to print all pairs
using System;

class GFG
{
// Function to print all pairs
static bool checkPairs(int l, int r)
{
    // check if even
    if ((l - r) % 2 == 0)
        return false;

    /* We can print all adjacent pairs
    for (int i = l; i < r; i += 2)
    {
        System.out.print("{"+i+", "+i + 1+"}, ");
    } */

    return true;
}

// Driver Code
static public void Main ()
{
    int l = 1, r = 8;
    if (checkPairs(l, r))
    Console.Write("Yes");
    else
    Console.Write("No");
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all pairs

// Function to print all pairs
function checkPairs($l, $r)
{
    // check if even
    if (($l - $r) % 2 == 0)
        return false;

    /* We can print all adjacent pairs
    for (int i = l; i < r; i += 2)
    {
        cout << "{" << i << ", " << i + 1 << "}, ";
    } */

    return true;
}

// Driver Code
$l = 1;
$r = 8;
if (checkPairs($l, $r))
    echo ("Yes");
else
    echo ("No");

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript program to print all pairs

    // Function to print all pairs
    function checkPairs(l , r) {
        // check if even
        if ((l - r) % 2 == 0)
            return false;

        /*
         We can print all adjacent pairs
         for (i = l; i < r; i += 2) {
         document.write("{"+i+", "+i + 1+"], "); }
         */

        return true;
    }

    // Driver Code

        var l = 1, r = 8;
        if (checkPairs(l, r))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)