# 整齐号(非递减顺序的数字)

> 原文:[https://www . geesforgeks . org/tidy-number-digits-non-reducing-order/](https://www.geeksforgeeks.org/tidy-number-digits-non-decreasing-order/)

给定一个数字，任务是检查它是否整洁。整齐的数字是其位数不递减的数字。
**例:**

```
Input : 1234
Output : Yes

Input : 1243
Output : No
Digits "4" and "3" violate the property.
```

用弗雷肖卡茨语问道

**算法:**

```
1- One by one find all the digits.
2- Compare every digit with its next digit.
3- If any is in decreasing order then return false.
4- Otherwise return true.
```

**执行:**

## C++

```
// C++ program to check if a number is Tidy
// or not.
#include<iostream>
using namespace std;

// Returns true if num is Tidy
bool isTidy(int num)
{
    // To store previous digit (Assigning
    // initial value which is more than any
    // digit)
    int prev = 10;

    // Traverse all digits from right to
    // left and check if any digit is
    // smaller than previous.
    while (num)
    {
        int rem = num % 10;
        num /= 10;
        if (rem > prev)
           return false;
        prev = rem;
    }

    return true;
}

// Driver code
int main()
{
    int num = 1556;
    isTidy(num) ? cout << "Yes"
                : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number
// is Tidy or not.

class Test
{
    // Returns true if num is Tidy
    static boolean isTidy(int num)
    {
        // To store previous digit
        // (Assigning initial value
            // which is more than any
        // digit)
        int prev = 10;

        // Traverse all digits from right to
        // left and check if any digit is
        // smaller than previous.
        while (num!=0)
        {
            int rem = num % 10;
            num /= 10;
            if (rem > prev)
               return false;
            prev = rem;
        }

        return true;
    }

    // Driver method
    public static void main(String[] args)
    {
        int num = 1556;
        System.out.println(isTidy(num) ? "Yes" : "No");
    }
}
```

## 蟒蛇 3

```
# Python program to check if a number
# is Tidy or not.

# Returns true if num is Tidy
def isTidy(num):

    # To store previous digit (Assigning
    # initial value which is more than any
    # digit)
    prev = 10

    # Traverse all digits from right to
    # left and check if any digit is
    # smaller than previous.
    while (num):
        rem = num % 10
        num /= 10
        if rem > prev:
            return False
        prev = rem
    return True

# Driver code
num = 1556
if isTidy(num):
    print("Yes")
else:
    print("No")

# This code is contributed by Sharad_Bhardwaj.
```

## C#

```
// C# program to check if a
// number is Tidy or not.
using System;

class GFG
{
    // Returns true if num is Tidy
    static bool isTidy(int num)
    {
        // To store previous digit
        // (Assigning initial value
        // which is more than any
        // digit)
        int prev = 10;

        // Traverse all digits from
        // right to left and check
        // if any digit is smaller
        // than previous.
        while (num != 0)
        {
            int rem = num % 10;
            num /= 10;
            if (rem > prev)
            return false;
            prev = rem;
        }

        return true;
    }

// Driver Code
public static void Main ()
{
    int num = 1556;

    Console.WriteLine(isTidy(num) ?
                            "Yes" :
                             "No");
}
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// number is Tidy or not.

// Returns true if num is Tidy
function isTidy($num)
{
    // To store previous digit
    // (Assigning initial value
    // which is more than any
    // digit)
    $prev = 10;

    // Traverse all digits from
    // right to left and check
    // if any digit is smaller
    // than previous.
    while ($num)
    {
        $rem = $num % 10;
        $num = (int)$num / 10;
        if ($rem > $prev)
            return false;
        $prev = $rem;
    }

    return true;
}

// Driver code
$num = 1556;
if(isTidy($num) == true)
echo "Yes";
else
echo "No";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Returns true if num is Tidy
    function isTidy(num)
    {
        // To store previous digit
        // (Assigning initial value
            // which is more than any
        // digit)
        let prev = 10;

        // Traverse all digits from right to
        // left and check if any digit is
        // smaller than previous.
        while (num!=0)
        {
            let rem = num % 10;
            num /= 10;
            if (rem > prev)
               return false;
            prev = rem;
        }

        return true;
    }

// Driver Code
    let num = 1556;
    document.write(isTidy(num) ? "Yes" : "No");

// This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
Yes
```

**时间复杂度:** O(d)，其中 d 为给定数字中的位数。
**参考:**
[https://www.careercup.com/question?id=5136136486780928](https://www.careercup.com/question?id=5136136486780928)
本文由[**Sahil Chhabra(akku)**](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。