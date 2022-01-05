# 可被 10 的幂整除的最小清除数上升到 K

> 原文:[https://www . geeksforgeeks . org/最小移除数可被 10 次方的 k 整除/](https://www.geeksforgeeks.org/minimum-removals-in-a-number-to-be-divisible-by-10-power-raised-to-k/)

给定两个正整数 **N** 和 **K** 。找出可以从数字 N 中删除的最小位数，这样删除后的数字可以被 **10 <sup>K</sup>** 整除，否则打印-1。
**举例:**

```
Input : N = 10904025, K = 2
Output : 3
Explanation : We can remove the digits 4, 2 and 5 such that the number 
becomes 10900 which is divisible by 102.

Input : N = 1000, K = 5
Output : 3
Explanation : We can remove the digits 1 and any two zeroes such that the
number becomes 0 which is divisible by 105

Input : N = 23985, K = 2
Output : -1
```

**方法:**想法是从最后一位开始遍历数字，同时保留一个计数器。如果当前数字不为零，递增计数器变量，否则递减变量 K。当 K 变为零时，返回计数器作为答案。遍历整数后，检查 K 的当前值是否为零。如果是零，返回计数器作为答案，否则返回答案作为 N–1 中的位数，因为我们需要将整个数字减少到一个可被任何数字整除的零。此外，如果给定的数字不包含任何零，则返回-1 作为答案。
以下是上述办法的实施情况。

## C++

```
// CPP Program to count the number
// of digits that can be removed such
// that number is divisible by 10^K
#include <bits/stdc++.h>
using namespace std;

// function to return the required
// number of digits to be removed
int countDigitsToBeRemoved(int N, int K)
{
    // Converting the given number
    // into string
    string s = to_string(N);

    // variable to store number of
    // digits to be removed
    int res = 0;

    // variable to denote if atleast
    // one zero has been found
    int f_zero = 0;
    for (int i = s.size() - 1; i >= 0; i--) {
        if (K == 0)
            return res;
        if (s[i] == '0') {

            // zero found
            f_zero = 1;
            K--;
        }
        else
            res++;
    }

    // return size - 1 if K is not zero and
    // atleast one zero is present, otherwise
    // result
    if (!K)
        return res;
    else if (f_zero)
        return s.size() - 1;
    return -1;
}

// Driver Code to test above function
int main()
{
    int N = 10904025, K = 2;
    cout << countDigitsToBeRemoved(N, K) << endl;

    N = 1000, K = 5;
    cout << countDigitsToBeRemoved(N, K) << endl;

    N = 23985, K = 2;
    cout << countDigitsToBeRemoved(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count the number
// of digits that can be removed such
// that number is divisible by 10^K

public class GFG{

    // function to return the required
    // number of digits to be removed
    static int countDigitsToBeRemoved(int N, int K)
    {
        // Converting the given number
        // into string
        String s = Integer.toString(N);

        // variable to store number of
        // digits to be removed
        int res = 0;

        // variable to denote if atleast
        // one zero has been found
        int f_zero = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            if (K == 0)
                return res;
            if (s.charAt(i) == '0') {

                // zero found
                f_zero = 1;
                K--;
            }
            else
                res++;
        }

        // return size - 1 if K is not zero and
        // atleast one zero is present, otherwise
        // result
        if (K == 0)
            return res;
        else if (f_zero == 1)
            return s.length() - 1;
        return -1;
    }

    // Driver Code to test above function
    public static void main(String []args)
    {
        int N = 10904025;
        int K = 2;
        System.out.println(countDigitsToBeRemoved(N, K)) ;

        N = 1000 ;
        K = 5;
        System.out.println(countDigitsToBeRemoved(N, K))  ;

        N = 23985;
        K = 2;
        System.out.println(countDigitsToBeRemoved(N, K)) ;
    }

    // This code is contributed by Ryuga
    }
```

## 蟒蛇 3

```
# Python3 Program to count the number
# of digits that can be removed such
# that number is divisible by 10^K

# function to return the required
# number of digits to be removed
def countDigitsToBeRemoved(N, K):

    # Converting the given number
    # into string
    s = str(N);

    # variable to store number of
    # digits to be removed
    res = 0;

    # variable to denote if atleast
    # one zero has been found
    f_zero = 0;
    for i in range(len(s) - 1, -1, -1):
        if (K == 0):
            return res;
        if (s[i] == '0'):

            # zero found
            f_zero = 1;
            K -= 1;
        else:
            res += 1;

    # return size - 1 if K is not zero and
    # atleast one zero is present, otherwise
    # result
    if (K == 0):
        return res;
    elif (f_zero > 0):
        return len(s) - 1;
    return -1;

# Driver Code
N = 10904025;
K = 2;
print(countDigitsToBeRemoved(N, K));

N = 1000;
K = 5;
print(countDigitsToBeRemoved(N, K));

N = 23985;
K = 2;
print(countDigitsToBeRemoved(N, K));

# This code is contributed by mits
```

## C#

```
// C# Program to count the number
// of digits that can be removed such
// that number is divisible by 10^K

using System;
public class GFG{

    // function to return the required
    // number of digits to be removed
    static int countDigitsToBeRemoved(int N, int K)
    {
        // Converting the given number
        // into string
        string s = Convert.ToString(N);

        // variable to store number of
        // digits to be removed
        int res = 0;

        // variable to denote if atleast
        // one zero has been found
        int f_zero = 0;
        for (int i = s.Length - 1; i >= 0; i--) {
            if (K == 0)
                return res;
            if (s[i] == '0') {

                // zero found
                f_zero = 1;
                K--;
            }
            else
                res++;
        }

        // return size - 1 if K is not zero and
        // atleast one zero is present, otherwise
        // result
        if (K == 0)
            return res;
        else if (f_zero == 1)
            return s.Length - 1;
        return -1;
    }

    // Driver Code to test above function
    public static void Main()
    {
        int N = 10904025;
        int K = 2;
        Console.Write(countDigitsToBeRemoved(N, K)+"\n") ;

        N = 1000 ;
        K = 5;
        Console.Write(countDigitsToBeRemoved(N, K)+"\n")  ;

        N = 23985;
        K = 2;
        Console.Write(countDigitsToBeRemoved(N, K)+"\n") ;
    }

    }
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count the number
// of digits that can be removed such
// that number is divisible by 10^K

// function to return the required
// number of digits to be removed
function countDigitsToBeRemoved($N, $K)
{
    // Converting the given number
    // into string
    $s = strval($N);

    // variable to store number of
    // digits to be removed
    $res = 0;

    // variable to denote if atleast
    // one zero has been found
    $f_zero = 0;
    for ($i = strlen($s)-1; $i >= 0; $i--) {
        if ($K == 0)
            return $res;
        if ($s[$i] == '0') {

            // zero found
            $f_zero = 1;
            $K--;
        }
        else
            $res++;
    }

    // return size - 1 if K is not zero and
    // atleast one zero is present, otherwise
    // result
    if (!$K)
        return $res;
    else if ($f_zero)
        return strlen($s) - 1;
    return -1;
}

// Driver Code to test above function

    $N = 10904025;
    $K = 2;
    echo countDigitsToBeRemoved($N, $K)."\n";

    $N = 1000;
    $K = 5;
    echo countDigitsToBeRemoved($N, $K)."\n";

    $N = 23985;
    $K = 2;
    echo countDigitsToBeRemoved($N, $K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

      // JavaScript Program to count the number
      // of digits that can be removed such
      // that number is divisible by 10^K

      // Function to return the required
      // number of digits to be removed
      function countDigitsToBeRemoved(N, K) {
        // Converting the given number
        // into string
        var s = N.toString();

        // variable to store number of
        // digits to be removed
        var res = 0;

        // variable to denote if atleast
        // one zero has been found
        var f_zero = 0;
        for (var i = s.length - 1; i >= 0; i--) {
          if (K === 0) return res;
          if (s[i] === "0") {
            // zero found
            f_zero = 1;
            K--;
          } else res++;
        }

        // return size - 1 if K is not zero and
        // atleast one zero is present, otherwise
        // result
        if (K === 0) return res;
        else if (f_zero === 1) return s.length - 1;
        return -1;
      }

      // Driver Code to test above function
      var N = 10904025;
      var K = 2;
      document.write(countDigitsToBeRemoved(N, K) + "<br>");

      N = 1000;
      K = 5;
      document.write(countDigitsToBeRemoved(N, K) + "<br>");

      N = 23985;
      K = 2;
      document.write(countDigitsToBeRemoved(N, K) + "<br>");

    </script>
```

**Output:** 

```
3
3
-1
```

**时间复杂度:**给定数字中的位数。