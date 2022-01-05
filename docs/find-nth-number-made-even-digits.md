# 找到仅由偶数组成的第 n 个数字

> 原文:[https://www . geesforgeks . org/find-n-number-make-偶数/](https://www.geeksforgeeks.org/find-nth-number-made-even-digits/)

给定一个数字 n，找出仅由偶数(0，2，4，6，8)组成的第 n 个正数。最初几个由偶数组成的数字是 0、2、4、6、8、20、22、24……

**示例:**

```
Input  : 2
Output : 2
Second number made of 0, 2, 4, 6, 8 is 2

Input  : 10
Output : 28
```

**天真的方法**
天真的方法是从 0 开始，检查它是否只由{0，2，4，6，8}组成，当你找到第 n 个这样的数字时停止。

## C++

```
// Simple C++ program to find
// n-th number made of even
// digits only
#include<bits/stdc++.h>
using namespace std;

// function to calculate nth
// number made of even digits only
int findNthEvenDigitNumber(int n )
{
    // variable to note how
    // many such numbers have
    // been found till now
    int count = 0;
    for (int i = 0 ; ; i++)
    {
        int curr = i;

        // bool variable to check if
        // 1, 3, 5, 7, 9 is there or not
        bool isCurrEvenDigit = true ;

        // checking each digit
        // of the number
        while (curr != 0)
        {
            // If 1, 3, 5, 7, 9 is found
            // temp is changed to false
            if (curr % 10 == 1 || curr % 10 == 3 ||
                curr % 10 == 5 || curr % 10 == 7 ||
                curr % 10 == 9)
                isCurrEvenDigit = false;
            curr = curr / 10;
        }

        // temp is true it means that it
        // does not have 1, 3, 5, 7, 9
        if (isCurrEvenDigit == true)
            count++;

        // If nth such number is
        // found return it
        if (count == n)
            return i;
    }
}

// Driver Code
int main()
{
    cout << findNthEvenDigitNumber(2)
         << endl;
    cout << findNthEvenDigitNumber(10)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to
// find the n-th number made
// of even digits only

class GFG
{
    // function to calculate nth
    // number made of even digits only
    static int findNthEvenDigitNumber(int n )
    {
        // variable to note how
        // many such numbers have
        // been found till now
        int count = 0;
        for (int i = 0 ; ; i++)
        {
            int curr = i;

            // bool variable to check if
            // 1, 3, 5, 7, 9 is there or not
            boolean isCurrEvenDigit = true ;

            // checking each digit
            // of the number
            while (curr != 0)
            {
                // If 1, 3, 5, 7, 9 is found
                // temp is changed to false
                if (curr % 10 == 1 || curr % 10 == 3 ||
                    curr % 10 == 5 || curr % 10 == 7 ||
                    curr % 10 == 9)
                    isCurrEvenDigit = false;
                curr = curr / 10;
            }

            // temp is true it means that it
            // does not have 1, 3, 5, 7, 9
            if (isCurrEvenDigit == true)
                count++;

            // If nth such number
            // is found return it
            if (count == n)
                return i;
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        System.out.println(findNthEvenDigitNumber(2));
        System.out.println(findNthEvenDigitNumber(10));
    }
}
```

## 蟒蛇 3

```
# Simple Python3 program to find nth
# number made of even digits only

# function to calculate nth number
# made of even digits only
def findNthEvenDigitNumber(n):

    # variable to note how many such
    # numbers have been found till now
    count = 0;
    i = 0;
    while (True):

        curr = i;

        # bool variable to check if
        # 1, 3, 5, 7, 9 is there or not
        isCurrEvenDigit = True;

        # checking each digit of the number
        while (curr != 0):

            # If 1, 3, 5, 7, 9 is found
            # temp is changed to false
            if (curr % 10 == 1 or curr % 10 == 3 or
                curr % 10 == 5 or curr % 10 == 7 or
                curr % 10 == 9):
                isCurrEvenDigit = False;
            curr = curr // 10;

        # temp is true it means that it
        # does not have 1, 3, 5, 7, 9
        if (isCurrEvenDigit == True):
            count += 1;

        # If nth such number is found,
        # return it
        if (count == n):
            return i;

        i += 1;

# Driver Code
print(findNthEvenDigitNumber(2));
print(findNthEvenDigitNumber(10));

# This code is contributed by mits
```

## C#

```
// Simple C# program to
// find the n-th number
// made of even digits only
using System;

class GFG
{
    // function to calculate nth
    // number made of even digits only
    static int findNthEvenDigitNumber(int n )
    {
        // variable to note how
        // many such numbers have
        // been found till now
        int count = 0;
        for (int i = 0 ; ; i++)
        {
            int curr = i;

            // bool variable to check if
            // 1, 3, 5, 7, 9 is there or not
            bool isCurrEvenDigit = true ;

            // checking each digit
            // of the number
            while (curr != 0)
            {
                // If 1, 3, 5, 7, 9 is found
                // temp is changed to false
                if (curr % 10 == 1 || curr % 10 == 3 ||
                    curr % 10 == 5 || curr % 10 == 7 ||
                    curr % 10 == 9 )
                    isCurrEvenDigit = false;
                curr = curr / 10;
            }

            // temp is true it means that it
            // does not have 1, 3, 5, 7, 9
            if (isCurrEvenDigit == true)
                count++;

            // If nth such number
            // is found return it
            if (count == n)
                return i;
        }
    }

    // Driver code
    public static void Main ()
    {
        Console.WriteLine(findNthEvenDigitNumber(2));
        Console.WriteLine(findNthEvenDigitNumber(10));
    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple C++ program to find
// nth number made of even
// digits only

// function to calculate nth
// number made of even digits only
function findNthEvenDigitNumber($n )
{
    // variable to note how
    // many such numbers have
    // been found till now
    $count = 0;
    for ($i = 0 ; ; $i++)
    {
        $curr = $i;

        // bool variable to check if
        // 1, 3, 5, 7, 9 is there or not
        $isCurrEvenDigit = true ;

        // checking each digit
        // of the number
        while ($curr != 0)
        {
            // If 1, 3, 5, 7, 9 is found
            // temp is changed to false
            if ($curr % 10 == 1 || $curr % 10 == 3 ||
                $curr % 10 == 5 || $curr % 10 == 7 ||
                $curr % 10 == 9)
                $isCurrEvenDigit = false;
            $curr = $curr / 10;
        }

        // temp is true it means that it
        // does not have 1, 3, 5, 7, 9
        if ($isCurrEvenDigit == true)
            $count++;

        // If nth such number
        // is found return it
        if ($count == $n)
            return $i;
    }
}

// Driver Code
echo findNthEvenDigitNumber(2),"\n" ;
echo findNthEvenDigitNumber(10) ;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Simple JavaScript program to find
// n-th number made of even
// digits only

// Function to calculate nth
// number made of even digits only
function findNthEvenDigitNumber(n)
{

    // Variable to note how
    // many such numbers have
    // been found till now
    let count = 0;

    for(let i = 0;; i++)
    {
        let curr = i;

        // Bool variable to check if
        // 1, 3, 5, 7, 9 is there or not
        let isCurrEvenDigit = true;

        // Checking each digit
        // of the number
        while (curr != 0)
        {

            // If 1, 3, 5, 7, 9 is found
            // temp is changed to false
            if (curr % 10 == 1 || curr % 10 == 3 ||
                curr % 10 == 5 || curr % 10 == 7 ||
                curr % 10 == 9)
                isCurrEvenDigit = false;

            curr = Math.floor(curr / 10);
        }

        // temp is true it means that it
        // does not have 1, 3, 5, 7, 9
        if (isCurrEvenDigit === true)
            count++;

        // If nth such number is
        // found return it
        if (count === n)
            return i;
    }
}

// Driver Code
document.write(findNthEvenDigitNumber(2) + "<br>");
document.write(findNthEvenDigitNumber(10) + "<br>");

// This code is contributed by Manoj.

</script>
```

**输出:**

```
2
28
```

**高效方法**
我们需要找到由 5 位数组成的数字，0，2，4，6 和 8。当我们把一个数字转换成基数为 5 的数字时，它将只由数字{0，1，2，3，4}组成。可以清楚地看到，所需数字组{0，2，4，6，8}中的每个数字都是基数为 5 的数字组的相应索引中的数字的两倍。因此，要找到仅由偶数组成的第 n 个数字，请遵循下面提到的步骤
步骤 1:将 n 转换为 n-1 这样做是为了排除零。
第二步:将 n 转换为 5 位十进制数。
第三步:将上面找到的数字乘以 2。这是必需的号码

## C++

```
// Efficient C++ program to
// find n-th number made of
// even digits only
#include<bits/stdc++.h>
using namespace std;

// function to find nth number
// made of even digits only
int findNthEvenDigitNumber(int n)
{
    // If n=1 return 0
    if (n == 1)
        return 0;

    // vector to store the digits
    // when converted into base 5
    vector< int> v;

    // Reduce n to n-1 to exclude 0
    n = n - 1;

    // Reduce n to base 5
    // number and store digits
    while (n > 0)
    {
        // pushing the digits
        // into vector
        v.push_back(n % 5);
        n = n / 5;
    }

    // variable to represent the
    // number after converting it
    // to base 5\. Since the digits
    // are be in reverse order,
    // we traverse vector from back
    int result = 0;
    for (int i = v.size() - 1; i >= 0; i--)
    {
        result = result * 10;
        result = result + v[i];
    }

    // return 2*result (to convert
    // digits 0, 1, 2, 3, 4 to
    // 0, 2, 4, 6, 8.
    return 2*result;
}

// Driver Code
int main()
{
    cout << findNthEvenDigitNumber(2)
         << endl;
    cout << findNthEvenDigitNumber(10)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
// Efficient Java program to
// find n-th number made of
// even digits only

class GFG {

// function to find nth number
// made of even digits only
    static int findNthEvenDigitNumber(int n) {
        // If n=1 return 0
        if (n == 1) {
            return 0;
        }

        // vector to store the digits
        // when converted into base 5
        Vector< Integer> v = new Vector<>();

        // Reduce n to n-1 to exclude 0
        n = n - 1;

        // Reduce n to base 5
        // number and store digits
        while (n > 0) {
            // pushing the digits
            // into vector
            v.add(n % 5);
            n = n / 5;
        }

        // variable to represent the
        // number after converting it
        // to base 5\. Since the digits
        // are be in reverse order,
        // we traverse vector from back
        int result = 0;
        for (int i = v.size() - 1; i >= 0; i--) {
            result = result * 10;
            result = result + v.get(i);
        }

        // return 2*result (to convert
        // digits 0, 1, 2, 3, 4 to
        // 0, 2, 4, 6, 8.
        return 2 * result;
    }

// Driver Code
    public static void main(String[] args) {
        System.out.println(findNthEvenDigitNumber(2));
        System.out.println(findNthEvenDigitNumber(10));
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Efficient Python 3 program to find n-th
# number made of even digits only

# function to find nth number made of
# even digits only
def findNthEvenDigitNumber( n):

    # If n = 1 return 0
    if (n == 1):
        return 0

    # vector to store the digits
    # when converted into base 5
    v = []

    # Reduce n to n-1 to exclude 0
    n = n - 1

    # Reduce n to base 5 number and
    # store digits
    while (n > 0):

        # pushing the digits into vector
        v.append(n % 5)
        n = n // 5

    # variable to represent the number 
    # after converting it to base 5.
    # Since the digits are be in reverse
    # order, we traverse vector from back
    result = 0
    for i in range(len(v) - 1, -1, -1):
        result = result * 10
        result = result + v[i]

    # return 2*result (to convert
    # digits 0, 1, 2, 3, 4 to
    # 0, 2, 4, 6, 8.
    return 2 * result

# Driver Code
if __name__ == "__main__":

    print(findNthEvenDigitNumber(2))
    print(findNthEvenDigitNumber(10))

# This code is contributed by ita_c
```

## C#

```
// Efficient C# program to
// find n-th number made of
// even digits only
using System;
using System.Collections;

class GFG {

    // function to find nth number
    // made of even digits only
    static int findNthEvenDigitNumber(int n)
    {
        // If n=1 return 0
        if (n == 1)
        {
            return 0;
        }

        // vector to store the digits
        // when converted into base 5
        ArrayList v = new ArrayList();

        // Reduce n to n-1 to exclude 0
        n = n - 1;

        // Reduce n to base 5
        // number and store digits
        while (n > 0)
        {
            // pushing the digits
            // into vector
            v.Add(n % 5);
            n = n / 5;
        }

        // variable to represent the
        // number after converting it
        // to base 5\. Since the digits
        // are be in reverse order,
        // we traverse vector from back
        int result = 0;
        for (int i = v.Count - 1; i >= 0; i--)
        {
            result = result * 10;
            result = result + (int)v[i];
        }

        // return 2*result (to convert
        // digits 0, 1, 2, 3, 4 to
        // 0, 2, 4, 6, 8.
        return 2 * result;
    }

    // Driver Code
    public static void Main()
    {
        Console.WriteLine(findNthEvenDigitNumber(2));
        Console.WriteLine(findNthEvenDigitNumber(10));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find n-th
// number made of even digits only

// function to find nth number
// made of even digits only
function findNthEvenDigitNumber($n)
{
    // If n=1 return 0
    if ($n == 1)
        return 0;

    // vector to store the digits
    // when converted into base 5
    $v = array();

    // Reduce n to n-1 to exclude 0
    $n = $n - 1;

    // Reduce n to base 5
    // number and store digits
    while ($n > 0)
    {
        // pushing the digits
        // into vector
        array_push($v, $n % 5);
        $n = (int)($n / 5);
    }

    // variable to represent the number
    // after converting it to base 5.
    // Since the digits are be in
    // reverse order, we traverse vector
    // from back
    $result = 0;
    for ($i = count($v) - 1; $i >= 0; $i--)
    {
        $result = $result * 10;
        $result = $result + $v[$i];
    }

    // return 2*result (to convert
    // digits 0, 1, 2, 3, 4 to
    // 0, 2, 4, 6, 8.
    return 2 * $result;
}

// Driver Code
echo findNthEvenDigitNumber(2) . "\n";
echo findNthEvenDigitNumber(10) . "\n"

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Efficient Javascript program to
// find n-th number made of
// even digits only

    // function to find nth number
    // made of even digits only
    function findNthEvenDigitNumber(n)
    {
        // If n=1 return 0
        if (n == 1) {
            return 0;
        }

        // vector to store the digits
        // when converted into base 5
        let v = [];

        // Reduce n to n-1 to exclude 0
        n = n - 1;

        // Reduce n to base 5
        // number and store digits
        while (n > 0) {
            // pushing the digits
            // into vector
            v.push(n % 5);
            n = Math.floor(n / 5);
        }

        // variable to represent the
        // number after converting it
        // to base 5\. Since the digits
        // are be in reverse order,
        // we traverse vector from back
        let result = 0;
        for (let i = v.length - 1; i >= 0; i--) {
            result = result * 10;
            result = result + v[i];
        }

        // return 2*result (to convert
        // digits 0, 1, 2, 3, 4 to
        // 0, 2, 4, 6, 8.
        return 2 * result;
    }

    // Driver Code
    document.write(findNthEvenDigitNumber(2)+"<br>");
    document.write(findNthEvenDigitNumber(10));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
2
28
```

**时间复杂度:** O(log <sub>5</sub> (n))

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。