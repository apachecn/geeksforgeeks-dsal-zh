# 检查给定字符串的字符是否按字母顺序排列

> 原文:[https://www . geesforgeks . org/check-如果给定字符串的字符是按字母顺序排列的/](https://www.geeksforgeeks.org/check-if-the-characters-of-a-given-string-are-in-alphabetical-order/)

给定一个字符串，任务是找出该字符串的字符是否按字母顺序排列。该字符串仅包含小写字符。

**示例:**

```
Input: Str = "aabbbcc"
Output: In alphabetical order

Input: Str = "aabbbcca"
Output: Not in alphabetical order
```

**简单的方法:**

*   将字符串存储到字符数组中，并对数组进行排序。
*   如果排序数组中的字符与字符串的顺序相同，则打印“按字母顺序”。
*   否则打印“不按字母顺序”。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that checks whether
// the string is in alphabetical
// order or not
bool isAlphabaticOrder(string s)
{
    // length of the string
    int n = s.length();

    // create a character array
    // of the length of the string
    char c[n];

    // assign the string
    // to character array
    for (int i = 0; i < n; i++) {
        c[i] = s[i];
    }

    // sort the character array
    sort(c, c + n);

    // check if the character array
    // is equal to the string or not
    for (int i = 0; i < n; i++)
        if (c[i] != s[i])
            return false;

    return true;   
}

// Driver code
int main()
{
    string s = "aabbbcc";

    // check whether the string is
    // in alphabetical order or not
    if (isAlphabaticOrder(s))
       cout << "Yes";
    else
       cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

// import  Arrays class
import java.util.Arrays;

public class GFG {

    // Function that checks whether
    // the string is in alphabetical
    // order or not
    static boolean isAlphabaticOrder(String s)
    {
        // length of the string
        int n = s.length();

        // create a character array
        // of the length of the string
        char c[] = new char [n];

        // assign the string
        // to character array
        for (int i = 0; i < n; i++) {
            c[i] = s.charAt(i);
        }

        // sort the character array
        Arrays.sort(c);

        // check if the character array
        // is equal to the string or not
        for (int i = 0; i < n; i++)
            if (c[i] != s.charAt(i)) 
                return false;

        return true;    
    }

    public static void main(String args[])
    {
        String s = "aabbbcc";

        // check whether the string is
        // in alphabetical order or not
        if (isAlphabaticOrder(s))
           System.out.println("Yes");
        else
            System.out.println("No");

    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function that checks whether
# the string is in alphabetical
# order or not
def isAlphabaticOrder(s):

    # length of the string
    n = len(s)

    # create a character array
    # of the length of the string
    c = [s[i] for i in range(len(s))]

    # sort the character array
    c.sort(reverse = False)

    # check if the character array
    # is equal to the string or not
    for i in range(n):
        if (c[i] != s[i]):
            return False

    return True

# Driver code
if __name__ == '__main__':
    s = "aabbbcc"

    # check whether the string is
    # in alphabetical order or not
    if (isAlphabaticOrder(s)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
// import Arrays class

using System;

public class GFG{

    // Function that checks whether
    // the string is in alphabetical
    // order or not
    static bool isAlphabaticOrder(String s)
    {
        // length of the string
        int n = s.Length;

        // create a character array
        // of the length of the string
        char []c = new char [n];

        // assign the string
        // to character array
        for (int i = 0; i < n; i++) {
            c[i] = s[i];
        }

        // sort the character array
        Array.Sort(c);

        // check if the character array
        // is equal to the string or not
        for (int i = 0; i < n; i++)
            if (c[i] != s[i])
                return false;

        return true;    
    }

    static public void Main (){
        String s = "aabbbcc";

        // check whether the string is
        // in alphabetical order or not
        if (isAlphabaticOrder(s))
        Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that checks whether
// the string is in alphabetical
// order or not
Function isAlphabaticOrder($s)
{

    // length of the string
    $n = strlen($s);

    $c = array();

    // assign the string
    // to character array
    for ($i = 0; $i < $n; $i++)
    {
        $c[$i] = $s[$i];
    }

    // sort the character array
    sort($c);

    // check if the character array
    // is equal to the string or not
    for ($i = 0; $i < $n; $i++)
        if ($c[$i] != $s[$i])
            return false;

    return true;
}

// Driver code
$s = "aabbbcc";

// check whether the string is
// in alphabetical order or not
if (isAlphabaticOrder($s))
    echo "Yes";
else
    echo "No";

// This Code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
//Javascript implementation of above approach

// Function that checks whether
// the string is in alphabetical
// order or not
function isAlphabaticOrder(s)
{
    // length of the string
    var n = s.length;

    // create a character array
    // of the length of the string
    var c = new Array(n);

    // assign the string
    // to character array
    for (var i = 0; i < n; i++) {
        c[i] = s[i];
    }

    // sort the character array
    c.sort();

    // check if the character array
    // is equal to the string or not
    for (var i = 0; i < n; i++)
        if (c[i] != s[i])
            return false;

    return true;   
}

s = "aabbbcc";

// check whether the string is
// in alphabetical order or not
if (isAlphabaticOrder(s))
  document.write( "Yes");
else
  document.write( "No");

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N*log(N))

**辅助空间:**O(N)
T3】高效进场:

*   运行从 1 到(n-1)的循环(其中 n 是字符串的长度)
*   检查索引“I”处的元素是否小于索引“i-1”处的元素。
*   如果是，则打印“按字母顺序”。
*   否则打印“不按字母顺序”。

下面是上述方法的实现

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that checks whether
// the string is in alphabetical
// order or not
bool isAlphabaticOrder(string s)
{
    int n = s.length();

    for (int i = 1; i < n; i++) {

        // if element at index 'i' is less
        // than the element at index 'i-1'
        // then the string is not sorted
        if (s[i] < s[i - 1])
           return false;
    }

    return true;
}

// Driver code
int main()
{
    string s = "aabbbcc";

    // check whether the string is
    // in alphabetical order or not
    if (isAlphabaticOrder(s))
       cout << "Yes";
    else
       cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
public class GFG {

// Function that checks whether
// the string is in alphabetical
// order or not
    static boolean isAlphabaticOrder(String s) {
        int n = s.length();

        for (int i = 1; i < n; i++) {

            // if element at index 'i' is less
            // than the element at index 'i-1'
            // then the string is not sorted
            if (s.charAt(i) < s.charAt(i - 1)) {
                return false;
            }
        }

        return true;
    }

// Driver code
    static public void main(String[] args) {
        String s = "aabbbcc";
        // check whether the string is
        // in alphabetical order or not
        if (isAlphabaticOrder(s)) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}
//This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function that checks whether
# the string is in alphabetical
# order or not
def isAlphabaticOrder(s):

    n = len(s)

    for i in range(1, n):

        # if element at index 'i' is less
        # than the element at index 'i-1'
        # then the string is not sorted
        if (s[i] < s[i - 1]) :
            return False

    return True

# Driver code
if __name__ == "__main__":

    s = "aabbbcc"

    # check whether the string is
    # in alphabetical order or not
    if (isAlphabaticOrder(s)):
        print("Yes")
    else:
        print("No")
```

## C#

```
// C# implementation of above approach
using System;

public class GFG{

// Function that checks whether
// the string is in alphabetical
// order or not
static bool isAlphabaticOrder(string s)
{
    int n = s.Length;

    for (int i = 1; i < n; i++) {

        // if element at index 'i' is less
        // than the element at index 'i-1'
        // then the string is not sorted
        if (s[i] < s[i - 1])
        return false;
    }

    return true;
}

// Driver code
    static public void Main (){
    string s = "aabbbcc";
    // check whether the string is
    // in alphabetical order or not
    if (isAlphabaticOrder(s))
    Console.WriteLine ("Yes");
        else
    Console.WriteLine  ("No");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that checks whether
// the string is in alphabetical
// order or not
function isAlphabaticOrder($s)
{
    $n = strlen($s);
    for ($i = 1; $i < $n; $i++)
    {

        // if element at index 'i' is less
        // than the element at index 'i-1'
        // then the string is not sorted
        if ($s[$i] < $s[$i - 1])
        return false;
    }

    return true;
}

// Driver code
$s = "aabbbcc";

// check whether the string is
// in alphabetical order or not
if (isAlphabaticOrder($s))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>
// JavaScript implementation of above approach

// Function that checks whether
// the string is in alphabetical
// order or not
function isAlphabaticOrder( s){
    let n = s.length;

    for (let i = 1; i < n; i++) {
        // if element at index 'i' is less
        // than the element at index 'i-1'
        // then the string is not sorted
        if (s[i] < s[i - 1])
           return false;
    }
    return true;
}

// Driver code
let s = "aabbbcc";
// check whether the string is
// in alphabetical order or not
if (isAlphabaticOrder(s))
    document.write("Yes");
else
    document.write("No");
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)