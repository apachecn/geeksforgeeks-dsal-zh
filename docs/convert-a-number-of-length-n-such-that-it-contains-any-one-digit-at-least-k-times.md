# 转换一个长度为 N 的数字，使其至少包含“K”次的任意一个数字

> 原文:[https://www . geeksforgeeks . org/convert-a-number-of-length-n-so-it-包含任意一位数的至少 k 次/](https://www.geeksforgeeks.org/convert-a-number-of-length-n-such-that-it-contains-any-one-digit-at-least-k-times/)

给定数值**‘N’**，它是一个数字**‘A’**的长度。您的任务是转换这些数字，以便在数字**【A】**中至少存在**【K】**次任意数字。为了替换其中一个**‘N’**位，还需要计算成本，这是新旧位的绝对差值。任务是打印将初始数字转换为最终数字所需的最小成本，并打印最终数字。
**注意:**如果有几个这样的数字，那么打印字典最小的一个。

**示例:**

> **输入:** N = 6，K = 5，A = 898196
> **输出:** 4，888188
> Number =“898196”，第二位数字“9”将被“8”所取代成本| 9–8 | = 1。用“8”替换第五个数字的成本是一样的。替换第五位数成本| 6–8 | = 2。因此，总成本为 4，最终数字为“888188”。
> 
> **输入:** N = 16，K = 14，A = 6124258626539246
> T3】输出: 22，4444444844449444

**进场:**

1.  初始化长度为“N”的数字“A”。
2.  初始化一个 PAIR STL 来存储最小成本和数量。
3.  将数字作为字符串存储在 temp 变量中。
4.  使用两个 for 循环检查所有有“j”差异的数字，并用“I”替换它们，如果达到成本就中断。
5.  用前一个替换最小成本。
6.  最后，打印最小成本和最终数字。

下面是上述方法的实现:

## C++

```
// C++ program to illustrate
// the above problem
#include <bits/stdc++.h>
using namespace std;

// function to calculate the minimum
// value and the final number
int finalNumber(int n, int k, string a)
{
    // modtemp = modified temp string
    int modtemp;

    // store the count of numbers changed to k
    int co;

    // temporary temp string
    string temp;

    // To store the minimum cost and no
    pair<int, string> ans = make_pair(INT_MAX, "");

    for (int i = 0; i < 10; i++) {
        // 'i' will replace the digits of N's to
        // generate a number with k same digits

        // store the main str in temp str for modification
        temp = a;

        // To store the temporary value of the modified number
        modtemp = 0;

        // Initial count for the given number to replace 'i'
        co = count(a.begin(), a.end(), i + '0');

        // 'j' manages the difference 'i' and 'j'
        for (int j = 1; j < 10; j++) {

            // For the elements ahead of 'i' index
            if (i + j < 10) {

                // Checks all elements with difference 'j'
                // and replaces them with 'i'
                for (int p = 0; p < n; p++) {

                    // Break if count is achieved
                    if (co >= k)
                        break;

                    if (i + '0' == temp[p] - j) {

                        // Replaces all elements with difference
                        // 'j' and with 'i'
                        temp[p] = i + '0';
                        modtemp += j;
                        co++;
                    }
                }
            }
            // For the elements before 'i' index
            if (i - j >= 0) {
                for (int p = n - 1; p >= 0; p--) {
                    if (co >= k)
                        break;

                    if (i + '0' == temp[p] + j) {
                        temp[p] = i + '0';
                        modtemp += j;
                        co++;
                    }
                }
            }
        }

        // replace the minimum cost with the previous one
        ans = min(ans, make_pair(modtemp, temp));
    }
    // print the minimum cost and the final number
    cout << ans.first << endl
         << ans.second << endl;
}

// Driver code
int main()
{
    // initialize number length and k
    int n = 5, k = 4;

    // initialize the number
    string a = "21122";

    finalNumber(n, k, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{
    static class pair
    {
        int first;
        String second;
        static pair make_pair(int first, String second)
        {
            pair p = new pair();
            p.first = first;
            p.second = second;
            return p;
        }
    }

// count for the given character
static int count(String a,char c)
{
    int co = 0;
    for(int i = 0; i < a.length(); i++)
    if(a.charAt(i) == c)
        co++;
    return co;
}

// function to calculate the minimum
// value and the final number
static int finalNumber(int n, int k, String a)
{
    // modtemp = modified temp String
    int modtemp;

    // store the count of numbers changed to k
    int co;

    // temporary temp String
    char temp[] = new char[a.length()];

    // To store the minimum cost and no
    pair ans = pair.make_pair(Integer.MAX_VALUE, "");

    for (int i = 0; i < 10; i++)
    {
        // 'i' will replace the digits of N's to
        // generate a number with k same digits

        // store the main str in temp str for modification
        temp = a.toCharArray();

        // To store the temporary value of the modified number
        modtemp = 0;

        // Initial count for the given number to replace 'i'
        co = count(a, (char)(i + '0'));

        // 'j' manages the difference 'i' and 'j'
        for (int j = 1; j < 10; j++)
        {

            // For the elements ahead of 'i' index
            if (i + j < 10)
            {

                // Checks all elements with difference 'j'
                // and replaces them with 'i'
                for (int p = 0; p < n; p++)
                {

                    // Break if count is achieved
                    if (co >= k)
                        break;

                    if (i + '0' == temp[p] - j)
                    {

                        // Replaces all elements with difference
                        // 'j' and with 'i'
                        temp[p] = (char)(i + '0');
                        modtemp += j;
                        co++;
                    }
                }
            }

            // For the elements before 'i' index
            if (i - j >= 0)
            {
                for (int p = n - 1; p >= 0; p--)
                {
                    if (co >= k)
                        break;

                    if (i + '0' == temp[p] + j)
                    {
                        temp[p] = (char)(i + '0');
                        modtemp += j;
                        co++;
                    }
                }
            }
        }

        // replace the minimum cost with the previous one
        if(ans.first > modtemp)
        ans = pair.make_pair(modtemp, new String(temp));
    }

    // print the minimum cost and the final number
    System.out.print( ans.first + "\n"
                    + ans.second + "\n");

    return -1;
}

// Driver code
public static void main(String args[])
{
    // initialize number length and k
    int n = 5, k = 4;

    // initialize the number
    String a = "21122";

    finalNumber(n, k, a);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to illustrate
# the above problem
import sys

# function to calculate the
# minimum value and the final
# number
def finalNumber(n, k, a):

    # To store the minimum
    # cost and no
    ans = [sys.maxsize, ""]

    for i in range(10):

        # 'i' will replace the
        # digits of N's to generate
        # a number with k same digits

        # store the main str in temp
        # str for modification
        temp = a

        # To store the temporary
        # value of the modified number
        modtemp = 0

        # Initial count for the
        # given number to replace 'i'
        co = a.count(chr(i + ord('0')))

        # 'j' manages the difference
        # 'i' and 'j'
        for j in range(1, 10):

            # For the elements ahead
            # of 'i' index
            if (i + j < 10):

                # Checks all elements with
                # difference 'j' and replaces
                # them with 'i'
                for p in range(n):

                    # Break if count is
                    # achieved
                    if (co >= k):
                        break

                    if (i + ord('0') ==
                        ord(temp[p]) - j):

                        # Replaces all elements
                        # with difference 'j'
                        # and with 'i'
                        temp.replace(temp[p],
                                     chr(i +
                                         ord('0')), 1)
                        modtemp += j
                        co+= 1

            # For the elements
            # before 'i' index
            if (i - j >= 0):
                for p in range(n - 1,
                               -1, -1):
                    if (co >= k):
                        break
                    if (i + ord('0') ==
                        ord(temp[p]) + j):
                        temp.replace(temp[p],
                                     chr(i +
                                         ord('0')), 1)
                        modtemp += j
                        co += 1

        # replace the minimum cost
        # with the previous one
        ans = min(ans, [modtemp,
                        temp])

    # print the minimum cost
    # and the final number
    print(ans[0])
    print(ans[1])

# Driver code
if __name__ == "__main__":

    # Initialize number
    # length and k
    n = 5
    k = 4

    # initialize the number
    a = "21122"

    finalNumber(n, k, a)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to illustrate
// the above problem
using System;
using System.Collections.Generic;
class GFG {

    // count for the given character
    static int count(string a,char c)
    {
        int co = 0;
        for(int i = 0; i < a.Length; i++)
        if(a[i] == c)
            co++;
        return co;
    }

    // function to calculate the minimum
    // value and the final number
    static int finalNumber(int n, int k, string a)
    {
        // modtemp = modified temp String
        int modtemp;

        // store the count of numbers changed to k
        int co;

        // temporary temp String
        char[] temp = new char[a.Length];

        // To store the minimum cost and no
        Tuple<int, string> ans = new Tuple<int, string>(Int32.MaxValue, "");

        for (int i = 0; i < 10; i++)
        {
            // 'i' will replace the digits of N's to
            // generate a number with k same digits

            // store the main str in temp str for modification
            temp = a.ToCharArray();

            // To store the temporary value of the modified number
            modtemp = 0;

            // Initial count for the given number to replace 'i'
            co = count(a, (char)(i + '0'));

            // 'j' manages the difference 'i' and 'j'
            for (int j = 1; j < 10; j++)
            {

                // For the elements ahead of 'i' index
                if (i + j < 10)
                {

                    // Checks all elements with difference 'j'
                    // and replaces them with 'i'
                    for (int p = 0; p < n; p++)
                    {

                        // Break if count is achieved
                        if (co >= k)
                            break;

                        if (i + '0' == temp[p] - j)
                        {

                            // Replaces all elements with difference
                            // 'j' and with 'i'
                            temp[p] = (char)(i + '0');
                            modtemp += j;
                            co++;
                        }
                    }
                }

                // For the elements before 'i' index
                if (i - j >= 0)
                {
                    for (int p = n - 1; p >= 0; p--)
                    {
                        if (co >= k)
                            break;

                        if (i + '0' == temp[p] + j)
                        {
                            temp[p] = (char)(i + '0');
                            modtemp += j;
                            co++;
                        }
                    }
                }
            }

            // replace the minimum cost with the previous one
            if(ans.Item1 > modtemp)
            ans = new Tuple<int, string>(modtemp, new string(temp));
        }

        // print the minimum cost and the final number
        Console.Write( ans.Item1 + "\n" + ans.Item2 + "\n");

        return -1;
    }

  static void Main()
  {

    // initialize number length and k
    int n = 5, k = 4;

    // initialize the number
    string a = "21122";

    finalNumber(n, k, a);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// count for the given character
function count(a,c)
{
    let co = 0;
    for(let i = 0; i < a.length; i++)
        if(a[i] == c)
            co++;
    return co;
}

// function to calculate the minimum
// value and the final number
function finalNumber(n,k,a)
{
    // modtemp = modified temp String
    let modtemp;

    // store the count of numbers changed to k
    let co;

    // temporary temp String
    let temp = new Array(a.length);

    // To store the minimum cost and no
    let ans = [Number.MAX_VALUE, ""];

    for (let i = 0; i < 10; i++)
    {
        // 'i' will replace the digits of N's to
        // generate a number with k same digits

        // store the main str in temp str for modification
        temp = a.split("");

        // To store the temporary value of the modified number
        modtemp = 0;

        // Initial count for the given number to replace 'i'
        co = count(a, String.fromCharCode(i + '0'.charCodeAt(0)));

        // 'j' manages the difference 'i' and 'j'
        for (let j = 1; j < 10; j++)
        {

            // For the elements ahead of 'i' index
            if (i + j < 10)
            {

                // Checks all elements with difference 'j'
                // and replaces them with 'i'
                for (let p = 0; p < n; p++)
                {

                    // Break if count is achieved
                    if (co >= k)
                        break;

                    if (i + '0'.charCodeAt(0) == temp[p].charCodeAt(0) - j)
                    {

                        // Replaces all elements with difference
                        // 'j' and with 'i'
                        temp[p] = String.fromCharCode(i + '0'.charCodeAt(0));
                        modtemp += j;
                        co++;
                    }
                }
            }

            // For the elements before 'i' index
            if (i - j >= 0)
            {
                for (let p = n - 1; p >= 0; p--)
                {
                    if (co >= k)
                        break;

                    if (i + '0'.charCodeAt(0) == temp[p].charCodeAt(0) + j)
                    {
                        temp[p] = String.fromCharCode(i + '0'.charCodeAt(0));
                        modtemp += j;
                        co++;
                    }
                }
            }
        }

        // replace the minimum cost with the previous one
        if(ans[0] > modtemp)
        ans = [modtemp, temp.join("")];
    }

    // print the minimum cost and the final number
    document.write( ans[0] + "<br>"
                    + ans[1] + "<br>");

    return -1;
}

// Driver code
// initialize number length and k
let n = 5, k = 4;
// initialize the number
let a = "21122";
finalNumber(n, k, a);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1
21222
```

**解释:**就像一次把 1 转换成 2 一样。2 变成了数字的 k 倍。所以成本是 2-1 = 1。