# 要删除的最少位数，使数字成为完美的正方形

> 原文:[https://www . geesforgeks . org/required-minimum-digits-remove-number-make-perfect-square/](https://www.geeksforgeeks.org/required-minimum-digits-remove-number-make-perfect-square/)

给定一个整数 n，我们需要找出从这个数中去掉多少个数字，使它成为一个完美的正方形。

**示例:**

> 输入:8314
> 输出:81 2
> 说明:如果我们去掉 3 和 4，数字就变成了 81，这是一个完美的正方形。
> 
> 输入:57
> 输出:-1

其思想是生成[所有可能的子序列](https://www.geeksforgeeks.org/print-subsequences-string/)，并使用[设置位](https://www.geeksforgeeks.org/print-subsequences-string-iterative-method/)返回最佳字符串。假设我们有一个字符串 8314。使用集合位，我们形成所有可能的子序列，即
**8、3、83、1、81、31、831、4、84、34、834、14、814、314、8314。**
在形成所有可能的子序列后，我们检查哪一个是完美的正方形。我们返回一个最小长度的完美平方数。

在上面的例子中，三个完美的正方形是 1 4 和 81，所以答案是 81，因为 81 的最大长度是 2。

## C++

```
// C++ program to find required minimum digits
// need to remove to make a number perfect square
#include <bits/stdc++.h>
using namespace std;

// function to check minimum number of digits
// should be removed to make this number
// a perfect square
int perfectSquare(string s)
{
    // size of the string
    int n = s.size();

    // our final answer
    int ans = -1;

    // to store string which is perfect square.
    string num;

    // We make all possible subsequences
    for (int i = 1; i < (1 << n); i++) {
        string str = "";

        for (int j = 0; j < n; j++) {

            // to check jth bit is set or not.
            if ((i >> j) & 1) {
                str += s[j];
            }
        }

        // we do not consider a number with leading zeros
        if (str[0] != '0') {

            // convert our temporary string into integer
            int temp = 0;
            for (int j = 0; j < str.size(); j++)
                temp = temp * 10 + (int)(str[j] - '0');

            int k = sqrt(temp);

            // checking temp is perfect square or not.
            if (k * k == temp) {

                // taking maximum sized string
                if (ans < (int)str.size()) {
                    ans = (int)str.size();
                    num = str;
                }
            }
        }
    }

    if (ans == -1)
        return ans;
    else {

        // print PerfectSquare
        cout << num << " ";
        return n - ans;
    }
}

// Driver code
int main()
{
    cout << perfectSquare("8314") << endl;
    cout << perfectSquare("753") << endl; 
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find required minimum digits
// need to remove to make a number perfect square
import java.io.*;
import java.lang.*;

public class GFG {

    // function to check minimum
    // number of digits should
    // be removed to make this
    // number a perfect square
    static int perfectSquare(String s)
    {
        // size of the string
        int n = s.length();

        // our final answer
        int ans = -1;

        // to store string which
        // is perfect square.
        String num = "";

        // We make all possible subsequences
        for (int i = 1; i < (1 << n); i++) {
            String str = "";

            for (int j = 0; j < n; j++) {

                // to check jth bit is set or not.
                if (((i >> j) & 1) == 1) {
                    str += s.charAt(j);
                }
            }

            // we do not consider a number
            // with leading zeros
            if (str.charAt(0) != '0') {

                // convert our temporary
                // string into integer
                int temp = 0;
                for (int j = 0; j <
                              str.length(); j++)
                    temp = temp * 10 +
                      (int)(str.charAt(j) - '0');

                int k = (int)Math.sqrt(temp);

                // checking temp is perfect
                // square or not.
                if (k * k == temp) {

                    // taking maximum sized string
                    if (ans < (int)str.length()) {
                        ans = (int)str.length();
                        num = str;
                    }
                }
            }
        }

        if (ans == -1)
            return ans;
        else {

            // print PerfectSquare
            System.out.print(num + " ");
            return n - ans;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        System.out.println(perfectSquare("8314"));
        System.out.println(perfectSquare("753"));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# C++ program to find required minimum
# digits need to remove to make a
# number perfect square

import math
# function to check minimum number of
# digits should be removed to make
# this number a perfect square
def perfectSquare(s) :

    # size of the string
    n = len(s)

    # our final answer
    ans = -1

    # to store string which is
    # perfect square.
    num = ""

    # We make all possible subsequences
    for i in range(1, (1 << n)) :
        str = ""

        for j in range(0, n) :

            # to check jth bit is
            # set or not.
            if ((i >> j) & 1) :
                str = str + s[j]

        # we do not consider a number
        # with leading zeros
        if (str[0] != '0') :

            # convert our temporary
            # string into integer
            temp = 0;
            for j in range(0, len(str)) :
                temp = (temp * 10 +
                 (ord(str[j]) - ord('0')))

            k = int(math.sqrt(temp))

            # checking temp is perfect
            # square or not.
            if (k * k == temp) :

                # taking maximum sized
                # string
                if (ans < len(str)) :
                    ans = len(str)
                    num = str

    if (ans == -1) :
        return ans
    else :        

        # print PerfectSquare
        print ("{} ".format(num), end="")
        return n - ans

# Driver code
print (perfectSquare("8314"))
print (perfectSquare("753"));

# This code is contributed by
# manishshaw1.
```

## C#

```
// C# program to find required minimum digits
// need to remove to make a number perfect square
using System;
class GFG {

    // function to check minimum
    // number of digits should
    // be removed to make this
    // number a perfect square
    static int perfectSquare(string s)
    {
        // size of the string
        int n = s.Length;

        // our final answer
        int ans = -1;

        // to store string which
        // is perfect square.
        string num = "";

        // We make all possible subsequences
        for (int i = 1; i < (1 << n); i++) {
            string str = "";

            for (int j = 0; j < n; j++) {

                // to check jth bit is set or not.
                if (((i >> j) & 1) == 1) {
                    str += s[j];
                }
            }

            // we do not consider a number
            // with leading zeros
            if (str[0] != '0') {

                // convert our temporary
                // string into integer
                int temp = 0;
                for (int j = 0; j < str.Length; j++)
                    temp = temp * 10 + (int)(str[j] - '0');

                int k = (int)Math.Sqrt(temp);

                // checking temp is perfect
                // square or not.
                if (k * k == temp) {

                    // taking maximum sized string
                    if (ans < (int)str.Length) {
                        ans = (int)str.Length;
                        num = str;
                    }
                }
            }
        }

        if (ans == -1)
            return ans;
        else {

            // print PerfectSquare
            Console.Write(num + " ");
            return n - ans;
        }
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(perfectSquare("8314"));
        Console.WriteLine(perfectSquare("753"));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find required
// minimum digits need to remove
// to make a number perfect square

// function to check minimum
// number of digits should be
// removed to make this number
// a perfect square
function perfectSquare($s)
{
    // size of the string
    $n = strlen($s);

    // our final answer
    $ans = -1;

    // to store string which
    // is perfect square.
    $num = "";

    // We make all possible
    // subsequences
    for ($i = 1; $i < (1 << $n); $i++)
    {
        $str = "";
        for ($j = 0; $j < $n; $j++)
        {

            // to check jth bit
            // is set or not.
            if (($i >> $j) & 1)
            {
                $str = $str.$s[$j];
            }
        }

        // we do not consider a
        // number with leading zeros
        if ($str[0] != '0')
        {
            // convert our temporary
            // string into integer
            $temp = 0;
            for ($j = 0; $j < strlen($str); $j++)
                $temp = $temp * 10 +
                        (ord($str[$j]) - ord('0'));

            $k = (int)(sqrt($temp));

            // checking temp is perfect
            // square or not.
            if (($k * $k) == $temp)
            {

                // taking maximum sized string
                if ($ans < strlen($str))
                {
                    $ans = strlen($str);
                    $num = $str;
                }
            }
        }
    }

    if ($ans == -1)
        return $ans;
    else
    {        
        // print PerfectSquare
        echo ($num." ");
        return ($n - $ans);
    }
}

// Driver code
echo (perfectSquare("8314"). "\n");
echo (perfectSquare("753"). "\n");

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to find required
// minimum digits need to remove
// to make a number perfect square

// Function to check minimum
// number of digits should be
// removed to make this number
// a perfect square
function perfectSquare(s)
{

    // Size of the string
    let n = s.length;

    // Our final answer
    let ans = -1;

    // To store string which
    // is perfect square.
    let num = "";

    // We make all possible
    // subsequences
    for(let i = 1; i < (1 << n); i++)
    {
        let str = "";
        for(j = 0; j < n; j++)
        {

            // To check jth bit
            // is set or not.
            if ((i >> j) & 1)
            {
                str = str + s[j];
            }
        }

        // We do not consider a
        // number with leading zeros
        if (str[0] != '0')
        {

            // Convert our temporary
            // string into integer
            let temp = 0;
            for(let j = 0; j < str.length; j++)
                temp = temp * 10 + (str[j].charCodeAt(0) -
                                       '0'.charCodeAt(0));

            k = Math.floor(Math.sqrt(temp));

            // Checking temp is perfect
            // square or not.
            if ((k * k) == temp)
            {

                // Taking maximum sized string
                if (ans < str.length)
                {
                    ans = str.length;
                    num = str;
                }
            }
        }
    }

    if (ans == -1)
        return ans;
    else
    {

        // Print PerfectSquare
        document.write(num + " ");
        return (n - ans);
    }
}

// Driver code
document.write(perfectSquare("8314") + "<br>");
document.write(perfectSquare("753") + "<br>");

// This code is contributed by gfgking

</script>
```

**Output :** 

```
81 2
-1
```