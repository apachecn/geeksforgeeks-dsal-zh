# 给定基数的泛数字数

> 原文:[https://www.geeksforgeeks.org/pandigital-number-given-base/](https://www.geeksforgeeks.org/pandigital-number-given-base/)

给定一个整数 **n** 及其基数 **b** 。任务是检查给定号码是否为给定基数内的[泛数字号码](https://en.wikipedia.org/wiki/Pandigital_number)。泛数字是一个整数，其基数的每个数字至少有一次。
可以假设基数小于等于 36。在基数 36 中，数字是[0，1，…9。a、B、…Z]
**例:**

```
Input : n = "9651723480", b = 10
Output : Yes
Given number n has all digits from 0 to 9

Input : n = "23456789ABCDEFGHIJKLMNOPQRSTUVWXYZ", 
        b = 36
Output : No
Given number n doesn't have all digits in base
36\. For example 1 is missing.
```

创建一个大小等于基数的布尔散列数组，并用 false 初始化它。现在，迭代数字的每个数字，并在散列数组中将其对应的索引值标记为 true。最后，检查散列数组中的所有值是否都被标记，如果标记为“是”，则打印“是”，否则打印“否”。
以下是该方法的实现:

## C++

```
// C++ program to check if a number is pandigital
// in given base.
#include<bits/stdc++.h>
using namespace std;

// Return true if n is pandigit else return false.
bool checkPandigital(int b, char n[])
{
    // Checking length is less than base
    if (strlen(n) < b)
        return false;

    bool hash[b];
    memset(hash, false, sizeof(hash));

    // Traversing each digit of the number.
    for (int i = 0; i < strlen(n); i++)
    {
        // If digit is integer
        if (n[i] >= '0' && n[i] <= '9')
            hash[n[i] - '0'] = true;

        // If digit is alphabet
        else if (n[i] - 'A' <= b - 11)
            hash[n[i] - 'A' + 10] = true;
    }

    // Checking hash array, if any index is
    // unmarked.
    for (int i = 0; i < b; i++)
        if (hash[i] == false)
            return false;

    return true;
}

// Driver Program
int main()
{
    int b = 13;
    char n[] = "1298450376ABC";

    (checkPandigital(b, n))? (cout << "Yes" << endl):
                             (cout << "No" << endl);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number
// is pandigital in given base.
import java.util.*;

class GFG {

// Return true if n is pandigit
// else return false.
static boolean checkPandigital(int b, String n) {

    // Checking length is less than base
    if (n.length() < b)
    return false;

    boolean hash[] = new boolean[b];
    Arrays.fill(hash, false);

    // Traversing each digit of the number.
    for (int i = 0; i < n.length(); i++) {

    // If digit is integer
    if (n.charAt(i) >= '0' && n.charAt(i) <= '9')
        hash[n.charAt(i) - '0'] = true;

    // If digit is alphabet
    else if (n.charAt(i) - 'A' <= b - 11)
        hash[n.charAt(i) - 'A' + 10] = true;
    }

    // Checking hash array, if any
    // index is unmarked.
    for (int i = 0; i < b; i++)
    if (hash[i] == false)
        return false;

    return true;
}

// Driver code
public static void main(String[] args)
{
    int b = 13;
    String n = "1298450376ABC";

    if (checkPandigital(b, n))
    System.out.println("Yes");
    else
    System.out.println("No");
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to check if a number is
# pandigital in given base.

# Return true if n is pandigit else return false.
def checkPandigital(b, n):

    # Checking length is less than base
    if (len(n) < b):
        return 0;

    hash = [0] * b;

    # Traversing each digit of the number.
    for i in range(len(n)):

        # If digit is integer
        if (n[i] >= '0' and n[i] <= '9'):
            hash[ord(n[i]) - ord('0')] = 1;

        # If digit is alphabet
        elif (ord(n[i]) - ord('A') <= b - 11):
            hash[ord(n[i]) - ord('A') + 10] = 1;

    # Checking hash array, if any index is
    # unmarked.
    for i in range(b):
        if (hash[i] == 0):
            return 0;

    return 1;

# Driver Code
b = 13;
n = "1298450376ABC";

if(checkPandigital(b, n)):
    print("Yes");
else:
    print("No");

# This code is contributed by mits
```

## C#

```
// C# program to check if a number
// is pandigital in given base.
using System;

class GFG {

// Return true if n is pandigit
// else return false.
static bool checkPandigital(int b, string n) {

    // Checking length is less than base
    if (n.Length < b)
    return false;

    bool []hash = new bool[b];
    for(int i = 0; i < b; i++)
    hash[i] = false;

    // Traversing each digit of the number.
    for (int i = 0; i < n.Length; i++) {

    // If digit is integer
    if (n[i] >= '0' && n[i] <= '9')
        hash[n[i] - '0'] = true;

    // If digit is alphabet
    else if (n[i] - 'A' <= b - 11)
        hash[n[i] - 'A' + 10] = true;
    }

    // Checking hash array, if any
    // index is unmarked.
    for (int i = 0; i < b; i++)
    if (hash[i] == false)
        return false;

    return true;
}

// Driver code
public static void Main()
{
    int b = 13;
    String n = "1298450376ABC";

    if (checkPandigital(b, n))
    Console.Write("Yes");
    else
    Console.Write("No");
}
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to check if a number is pandigital
// in given base.

// Return true if n is pandigit else return false.
function checkPandigital($b, $n)
{
    // Checking length is less than base
    if (strlen($n) < $b)
        return 0;

    $hash = array();

    for($i = 0; $i< $b; $i++)
    $hash[$i] = 0;

    // Traversing each digit of the number.
    for ($i = 0; $i < strlen($n); $i++)
    {
        // If digit is integer
        if ($n[$i] >= '0' && $n[$i] <= '9')
            $hash[$n[$i] - '0'] = 1;

        // If digit is alphabet
        else if (ord($n[$i]) - ord('A') <= $b - 11)
            $hash[ord($n[$i]) - ord('A') + 10] = 1;
    }

    // Checking hash array, if any index is
    // unmarked.
    for ($i = 0; $i < $b; $i++)
        if ($hash[$i] == 0)
            return 0;

    return 1;
}

// Driver Program
$b = 13;
$n = "1298450376ABC";

if(checkPandigital($b, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Sam007.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if a number is pandigital
// in given base.

// Return true if n is pandigit else return false.
function checkPandigital(b, n)
{
    // Checking length is less than base
    if (n.length < b)
        return 0;

    let hash = [];

    for(let i = 0; i< b; i++)
    hash[i] = 0;

    // Traversing each digit of the number.
    for (let i = 0; i < n.length; i++)
    {
        // If digit is integer
        if (n[i] >= '0' && n[i] <= '9')
            hash[n[i] - '0'] = 1;

        // If digit is alphabet
        else if (n.charCodeAt(i) - 'A'.charCodeAt(0) <= b - 11)
            hash[n.charCodeAt(i) - 'A'.charCodeAt(0) + 10] = 1;
    }

    // Checking hash array, if any index is
    // unmarked.
    for (let i = 0; i < b; i++)
        if (hash[i] == 0)
            return 0;

    return 1;
}

// Driver Program
let b = 13;
let n = "1298450376ABC";

if(checkPandigital(b, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
Yes
```

**参考:**
https://en.wikipedia.org/wiki/Pandigital_number
本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。