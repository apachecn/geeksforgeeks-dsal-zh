# 检查给定的数字是否是花式

> 原文:[https://www . geesforgeks . org/check-如果给定的号码是花式的/](https://www.geeksforgeeks.org/check-if-a-given-number-is-fancy/)

花哨的数字是旋转 180 度也是一样的。给定一个数字，看看它是否花哨。
180 度旋转的 6、9、1、0 和 8 分别是 9、6、1、0 和 8
**例:**

```
Input:  num =  96
Output: Yes
If we rotate given number by 180, we get same number

Input:  num =  916
Output: Yes
If we rotate given number by 180, we get same number

Input:  num =  996
Output: No

Input:  num =  121
Output: No
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
想法是创建一个地图来存储花式对映射。创建地图后，从两端遍历给定的数字，如果当前端的任何一个字符不是花式对，则返回 false。这个算法类似于[回文检查算法](http://geeksquiz.com/c-program-check-given-string-palindrome/)。
以下是以上思路的实现。

## C++

```
// C++ program to find if a given number is fancy or not.
#include<bits/stdc++.h>
using namespace std;

bool isFancy(string& num)
{
    // To store mappings of fancy pair characters. For example
    // 6 is paired with 9 and 9 is paired with 6.
    map<char, char> fp;
    fp['0'] = '0';
    fp['1'] = '1';
    fp['6'] = '9';
    fp['8'] = '8';
    fp['9'] = '6';

    // Find number of digits in given number
    int n = num.length();

    // Traverse from both ends, and compare characters one by one
    int l = 0, r = n-1;
    while (l<=r)
    {
        // If current characters at both ends are not fancy pairs
        if (fp.find(num[l]) == fp.end() || fp[num[l]] != num[r])
            return false;
        l++;
        r--;
    }
    return true;
}

// Driver program
int main()
{
    string str = "9088806";
    isFancy(str)? cout << "Yes": cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a given number
// is fancy or not
import java.util.*;

class GFG
{
static boolean isFancy(String num)
{
    // To store mappings of fancy pair characters.
    // For example 6 is paired with 9 and 9 is paired with 6.
    Map<Character,
        Character> fp = new HashMap<Character,
                                    Character>();

    fp. put('0', '0');
    fp. put('1', '1');
    fp. put('6', '9');
    fp. put('8', '8');
    fp. put('9', '6');

    // Find number of digits in given number
    int n = num.length();

    // Traverse from both ends,
    // and compare characters one by one
    int l = 0, r = n-1;
    while (l <= r)
    {
        // If current characters at both ends
        // are not fancy pairs
        if (!fp.containsKey(num.charAt(l)) ||
             fp.get(num.charAt(l)) != num.charAt(r))
            return false;
        l++;
        r--;
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    String str = "9088806";
    if(isFancy(str))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find if a given number
// is fancy or not
using System;
using System.Collections.Generic;

class GFG
{
static bool isFancy(String num)
{
    // To store mappings of fancy pair characters.
    // For example 6 is paired with 9 and 9 is paired with 6.
    Dictionary<char, char> fp = new Dictionary<char, char>();

    fp.Add('0', '0');
    fp.Add('1', '1');
    fp.Add('6', '9');
    fp.Add('8', '8');
    fp.Add('9', '6');

    // Find number of digits in given number
    int n = num.Length;

    // Traverse from both ends,
    // and compare characters one by one
    int l = 0, r = n - 1;
    while (l <= r)
    {
        // If current characters at both ends
        // are not fancy pairs
        if (!fp.ContainsKey(num[l]) ||
             fp[num[l]] != num[r])
            return false;
        l++;
        r--;
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "9088806";
    if(isFancy(str))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find if a given number is fancy or not.
def isFancy(num):

    # To store mappings of fancy pair characters. For example
    # 6 is paired with 9 and 9 is paired with 6.
    fp = {}
    fp['0'] = '0'
    fp['1'] = '1'
    fp['6'] = '9'
    fp['8'] = '8'
    fp['9'] = '6'

    # Find number of digits in given number
    n = len(num)

    # Traverse from both ends, and compare characters one by one
    l = 0
    r = n-1
    while (l <= r):

        # If current characters at both ends are not fancy pairs
        if (num[l] not in fp or fp[num[l]] != num[r]):
            return False
        l += 1
        r -= 1
    return True

# Driver program
if __name__ == "__main__":

    st = "9088806"
    if isFancy(st):
        print("Yes")
    else:
        print("No")

# This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript program to find if a given number
// is fancy or not
    function isFancy( num)
    {

        // To store mappings of fancy pair characters.
        // For example 6 is paired with 9 and 9 is paired with 6.
        var fp = new Map();

        fp.set('0', '0');
        fp.set('1', '1');
        fp.set('6', '9');
        fp.set('8', '8');
        fp.set('9', '6');

        // Find number of digits in given number
        var n = num.length;

        // Traverse from both ends,
        // and compare characters one by one
        var l = 0, r = n - 1;
        while (l <= r) {
            // If current characters at both ends
            // are not fancy pairs
            if (!fp.has(num.charAt(l)) || fp.get(num.charAt(l)) != num.charAt(r))
                return false;
            l++;
            r--;
        }
        return true;
    }

    // Driver Code

        var str = "9088806";
        if (isFancy(str))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by aashish1995
</script>
```

**输出:**

```
Yes
```

感谢[高拉夫·阿赫瓦尔](http://qa.geeksforgeeks.org/user/Mr.Lazy)提出上述解决方案。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。