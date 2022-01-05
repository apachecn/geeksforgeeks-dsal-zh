# 找出数字 d 在[0..n]

> 原文:[https://www . geeksforgeeks . org/find-of-y-in-of-x/](https://www.geeksforgeeks.org/find-the-occurrences-of-y-in-the-range-of-x/)

给定一个数字 n 和一个数字 d，计算从 0 到 n 范围内 d 的所有出现次数。
**示例:**

```
Input :  n = 25 
         d = 2
Output : 9
The occurrences are 2, 12, 20, 21
22 (Two occurrences), 23, 24, 25

Input : n = 25 
        d = 3
Output :3
The occurrences are 3, 13, 23

Input : n = 32 
        d = 3
Output : 6
The occurrences are 3, 13, 23, 30, 31, 32
```

d 的第一次出现不能在数字 d 之前，所以我们从 d 开始迭代，反复做以下检查。除了步骤 2.a 和 2.b 中提到的情况外，我们大多数情况下都会将数字加 10(在步骤 2 中)
**步骤 1** :检查数字的最后一位是否等于 d，如果是，则递增计数。
**第二步** :
a)如果数完全能被 10 整除，那么计数和数都要递增(例如，如果我们达到数 30，而数 30 完全能被 10 整除，并且 d=3，那么我们必须从 31-39 中对所有数进行计数，这就是我们为什么要递增 1 并递增 1 的原因)
b)否则，如果数的第一个数字比 d 小 1，那么这意味着我们已经到了必须将数递增 10 并从中减去 d 的那一行。例如，如果 d=3，我们达到 23，那么我们将该数增加 23+10-3 = 30)
c)否则只增加 10。(例如:d=3，itr=3，然后递增 10，即 13，23)
**步骤 3:-** 返回计数。

## C++

```
// C++ program to count appearances of
// a digit 'd' in range from [0..n]
#include <bits/stdc++.h>
using namespace std;

int getOccurence(int n, int d)
{
    int result = 0; // Initialize result

    // Count appearances in numbers starting
    // from d.
    int itr = d;
    while (itr <= n)
    {
        // When the last digit is equal to d
        if (itr%10 == d)
            result++;

        // When the first digit is equal to d then
        if (itr != 0 && itr/10 == d)
        {
            // increment result as well as number
            result++;
            itr++;
        }

        // In case of reverse of number such as 12 and 21
        else if (itr/10 == d-1)
            itr = itr + (10 - d);
        else
            itr = itr+10;
    }
    return result;
}

// Driver code
int main(void)
{
    int n = 11, d = 1;
    cout << getOccurence(n, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to count appearances of
// a digit 'd' in range from [0..n]
import java.*;

public class GFG {

    static int getOccurence(int n, int d)
    {

        // Initialize result
        int result = 0;

        // Count appearances in numbers
        // starting from d.
        int itr = d;

        while (itr <= n)
        {

            // When the last digit is
            // equal to d
            if (itr % 10 == d)
                result++;

            // When the first digit is
            // equal to d then
            if (itr != 0 && itr/10 == d)
            {

                // increment result as
                // well as number
                result++;
                itr++;
            }

            // In case of reverse of number
            // such as 12 and 21
            else if (itr/10 == d-1)
                itr = itr + (10 - d);
            else
                itr = itr + 10;
        }

        return result;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 11, d = 1;

        System.out.println(getOccurence(n, d) );
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python3 program to count appearances
# of a digit 'd' in range from [0..n]
import math;
def getOccurence(n, d):

    # Initialize result
    result = 0;

    # Count appearances in numbers
    # starting from d.
    itr = d;
    while(itr <= n):

        # When the last digit is equal to d
        if (itr % 10 == d):
            result += 1;

        # When the first digit is equal to d then
        if (itr != 0 and math.floor(itr / 10) == d):

            # increment result as well as number
            result += 1;
            itr += 1;

        # In case of reverse of number
        # such as 12 and 21
        elif (math.floor(itr / 10) == d - 1):
            itr = itr + (10 - d);
        else:
            itr = itr + 10;

    return result;

# Driver code
n = 11;
d = 1;
print(getOccurence(n, d));

# This code is contributed by mits
```

## C#

```
// C# program to count appearances of
// a digit 'd' in range from [0..n]
using System;

public class GFG {

    static int getOccurence(int n, int d)
    {

        // Initialize result
        int result = 0;

        // Count appearances in numbers
        // starting from d.
        int itr = d;
        while (itr <= n)
        {

            // When the last digit is
            // equal to d
            if (itr % 10 == d)
                result++;

            // When the first digit is
            // equal to d then
            if (itr != 0 && itr/10 == d)
            {

                // increment result as
                // well as number
                result++;
                itr++;
            }

            // In case of reverse of number
            // such as 12 and 21
            else if (itr/10 == d-1)
                itr = itr + (10 - d);
            else
                itr = itr + 10;
        }

        return result;
    }

    // Driver code
    public static void Main()
    {
        int n = 11, d = 1;

        Console.Write(getOccurence(n, d));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count appearances of
// a digit 'd' in range from [0..n]

function getOccurence($n, $d)
{

    // Initialize result
    $result = 0;

    // Count appearances in numbers
    // starting from d.
    $itr = $d;
    while($itr <= $n)
    {

        // When the last digit
        // is equal to d
        if ($itr % 10 == $d)
            $result++;

        // When the first digit
        // is equal to d then
        if ($itr != 0 && floor($itr / 10) == $d)
        {

            // increment result as
            // well as number
            $result++;
            $itr++;
        }

        // In case of reverse of
        // number such as 12 and 21
        else if (floor($itr / 10) == $d - 1)
            $itr = $itr + (10 - $d);
        else
            $itr = $itr + 10;
    }
    return $result;
}

    // Driver code
    $n = 11;
    $d = 1;
    echo getOccurence($n, $d);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript program to count appearances of
// a digit 'd' in range from [0..n]

function getOccurence(n, d)
{

    // Initialize result
    let result = 0;

    // Count appearances in numbers
    // starting from d.
    let itr = d;
    while(itr <= n)
    {

        // When the last digit
        // is equal to d
        if (itr % 10 == d)
            result++;

        // When the first digit
        // is equal to d then
        if (itr != 0 && Math.floor(itr / 10) == d)
        {

            // increment result as
            // well as number
            result++;
            itr++;
        }

        // In case of reverse of
        // number such as 12 and 21
        else if (Math.floor(itr / 10) == d - 1)
            itr = itr + (10 - d);
        else
            itr = itr + 10;
    }
    return result;
}

    // Driver code
    let n = 11;
    let d = 1;
    document.write(getOccurence(n, d));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
4
```

本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。