# 使二进制字符串交替所需的最小交换次数

> 原文:[https://www . geesforgeks . org/minimum-swaps-需要进行二进制字符串交替/](https://www.geeksforgeeks.org/minimum-swaps-required-to-make-a-binary-string-alternating/)

给你一个长度为偶数、0 和 1 相等的二进制字符串。使该字符串交替出现的最小交换次数是多少？如果没有两个连续的元素相等，则二进制字符串是交替的。

**示例:**

```
Input : 000111
Output : 1
Explanation : Swap index 2 and index 5 to get 010101

Input : 1010
Output : 0 
```

我们要么在第一个位置得到 1，要么在第一个位置得到 0。我们考虑两种情况，找到两种情况的最小值。请注意，假设字符串中 1 和 0 的数量相等，并且字符串的长度为偶数。
1。计算字符串奇数位置和偶数位置的零个数。让它们的计数分别为奇数 _0 和偶数 _0。
2。计算字符串奇数位置和偶数位置的 1 的数量。让它们的计数分别为奇数 _1 和偶数 _1。
3。我们总是用 0 交换 1(永远不要用 1 交换 1，也不要用 0 交换 0)。所以我们只需要检查我们的交替字符串是否以 0 开始，那么交换的数量是最小的(偶数 _0，奇数 _1)，如果我们的交替字符串以 1 开始，那么交换的数量是最小的(偶数 _1，奇数 _0)。答案是这两者中的最小值。

下面是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    // returns the minimum number of swaps
    // of a binary string
    // passed as the argument
    // to make it alternating
    int countMinSwaps(string st)
    {

        int min_swaps = 0;

        // counts number of zeroes at odd
        // and even positions
        int odd_0 = 0, even_0 = 0;

        // counts number of ones at odd
        // and even positions
        int odd_1 = 0, even_1 = 0;

        int n = st.length();
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                if (st[i] == '1')
                    even_1++;
                else
                    even_0++;
            }
            else {
                if (st[i] == '1')
                    odd_1++;
                else
                    odd_0++;
            }
        }

        // alternating string starts with 0
        int cnt_swaps_1 = min(even_0, odd_1);

        // alternating string starts with 1
        int cnt_swaps_2 = min(even_1, odd_0);

        // calculates the minimum number of swaps
        return min(cnt_swaps_1, cnt_swaps_2);
    }

    // Driver code
    int main()
    {
        string st = "000111";
        cout<<countMinSwaps(st)<<endl;

         return 0;
    }

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

    // returns the minimum number of swaps
    // of a binary string
    // passed as the argument
    // to make it alternating
    static int countMinSwaps(String st)
    {

        int min_swaps = 0;

        // counts number of zeroes at odd
        // and even positions
        int odd_0 = 0, even_0 = 0;

        // counts number of ones at odd
        // and even positions
        int odd_1 = 0, even_1 = 0;

        int n = st.length();
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                if (st.charAt(i) == '1')
                    even_1++;
                else
                    even_0++;
            }
            else {
                if (st.charAt(i) == '1')
                    odd_1++;
                else
                    odd_0++;
            }
        }

        // alternating string starts with 0
        int cnt_swaps_1 = Math.min(even_0, odd_1);

        // alternating string starts with 1
        int cnt_swaps_2 = Math.min(even_1, odd_0);

        // calculates the minimum number of swaps
        return Math.min(cnt_swaps_1, cnt_swaps_2);
    }

    // Driver code
    public static void main(String[] args)
    {
        String st = "000111";
        System.out.println(countMinSwaps(st));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# returns the minimum number of swaps
# of a binary string
# passed as the argument
# to make it alternating
def countMinSwaps(st) :

    min_swaps = 0

    # counts number of zeroes at odd
    # and even positions
    odd_0, even_0 = 0, 0

    # counts number of ones at odd
    # and even positions
    odd_1, even_1 = 0, 0

    n = len(st)

    for i in range(0, n) :

        if i % 2 == 0 :

            if st[i] == "1" :
                even_1 += 1
            else :
                even_0 += 1

        else :
            if st[i] == "1" :
                odd_1 += 1
            else :
                odd_0 += 1

    # alternating string starts with 0
    cnt_swaps_1 = min(even_0, odd_1)

    # alternating string starts with 1
    cnt_swaps_2 = min(even_1, odd_0)

    # calculates the minimum number of swaps
    return min(cnt_swaps_1, cnt_swaps_2)

# Driver code    
if __name__ == "__main__" :

    st = "000111"

    # Function call
    print(countMinSwaps(st))

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# implementation of the approach
using System;

public class GFG
{

    // returns the minimum number of swaps
    // of a binary string
    // passed as the argument
    // to make it alternating
    public static int countMinSwaps(string st)
    {

        int min_swaps = 0;

        // counts number of zeroes at odd 
        // and even positions
        int odd_0 = 0, even_0 = 0;

        // counts number of ones at odd 
        // and even positions
        int odd_1 = 0, even_1 = 0;

        int n = st.Length;
        for (int i = 0; i < n; i++)
        {
            if (i % 2 == 0)
            {
                if (st[i] == '1')
                {
                    even_1++;
                }
                else
                {
                    even_0++;
                }
            }
            else
            {
                if (st[i] == '1')
                {
                    odd_1++;
                }
                else
                {
                    odd_0++;
                }
            }
        }

        // alternating string starts with 0
        int cnt_swaps_1 = Math.Min(even_0, odd_1);

        // alternating string starts with 1
        int cnt_swaps_2 = Math.Min(even_1, odd_0);

        // calculates the minimum number of swaps
        return Math.Min(cnt_swaps_1, cnt_swaps_2);
    }

    // Driver code
    public static void Main(string[] args)
    {
        string st = "000111";
        Console.WriteLine(countMinSwaps(st));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// returns the minimum number of swaps
// of a binary string passed as the
// argument to make it alternating
function countMinSwaps($st)
{
    $min_swaps = 0;

    // counts number of zeroes at odd
    // and even positions
    $odd_0 = 0;
    $even_0 = 0;

    // counts number of ones at odd
    // and even positions
    $odd_1 = 0;
    $even_1 = 0;

    $n = strlen($st);
    for ($i = 0; $i < $n; $i++)
    {
        if ($i % 2 == 0)
        {
            if ($st[$i] == '1')
            {
                $even_1++;
            }
            else
            {
                $even_0++;
            }
        }
        else
        {
            if ($st[$i] == '1')
            {
                $odd_1++;
            }
            else
            {
                $odd_0++;
            }
        }
    }

    // alternating string starts with 0
    $cnt_swaps_1 = min($even_0, $odd_1);

    // alternating string starts with 1
    $cnt_swaps_2 = min($even_1, $odd_0);

    // calculates the minimum number of swaps
    return min($cnt_swaps_1, $cnt_swaps_2);
}

// Driver code
$st = "000111";
echo (countMinSwaps($st));

// This code is contributed by Sachin.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // returns the minimum number of swaps
    // of a binary string
    // passed as the argument
    // to make it alternating
    function countMinSwaps(st)
    {

        let min_swaps = 0;

        // counts number of zeroes at odd
        // and even positions
        let odd_0 = 0, even_0 = 0;

        // counts number of ones at odd
        // and even positions
        let odd_1 = 0, even_1 = 0;

        let n = st.length;
        for (let i = 0; i < n; i++)
        {
            if (i % 2 == 0)
            {
                if (st[i] == '1')
                {
                    even_1++;
                }
                else
                {
                    even_0++;
                }
            }
            else
            {
                if (st[i] == '1')
                {
                    odd_1++;
                }
                else
                {
                    odd_0++;
                }
            }
        }

        // alternating string starts with 0
        let cnt_swaps_1 = Math.min(even_0, odd_1);

        // alternating string starts with 1
        let cnt_swaps_2 = Math.min(even_1, odd_0);

        // calculates the minimum number of swaps
        return Math.min(cnt_swaps_1, cnt_swaps_2);
    }

    let st = "000111";
      document.write(countMinSwaps(st));

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
1
```

**奇数和偶数长度字符串的方法:**

让弦长为 **N.**

在这种方法中，我们将考虑三种情况:
1。当总 1 数>总 0 数+ 1 或总 0 数>总 1 数+ 1 时，答案是不可能的。
2。字符串长度为偶数:
我们将计算奇数位置(一 _ 奇数)的 1 数和偶数位置(一 _ 偶数)的 1 数，然后答案是 min(N/2–一 _ 奇数，N/2–一 _ 偶数)
3。字符串是奇数长度:
这里我们考虑两种情况:
I)1 的总数>0 的总数(那么我们已经把 1 放在偶数位置)所以，答案是((N+1)/2–偶数位置的 1 的数量)。
ii)零的总数>1 的总数(那么我们已经在偶数位置放了零)所以，答案是((N+1)/2–偶数位置的零的数量)。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// function to count minimum swaps
// required to make binary string
// alternating
int countMinSwaps(string s)
{
    int N = s.size();

    // stores total number of ones
    int one = 0;

    // stores total number of zeroes
    int zero = 0;

    for (int i = 0; i < N; i++) {
        if (s[i] == '1')
            one++;
        else
            zero++;
    }

    // checking impossible condition
    if (one > zero + 1 || zero > one + 1)
        return -1;

    // odd length string
    if (N % 2) {
        // number of even positions
        int num = (N + 1) / 2;

        // stores number of zeroes and
        // ones at even positions
        int one_even = 0, zero_even = 0;

        for (int i = 0; i < N; i++) {
            if (i % 2 == 0) {
                if (s[i] == '1')
                    one_even++;
                else
                    zero_even++;
            }
        }

        if (one > zero)
            return num - one_even;

        else
            return num - zero_even;
    }

    // even length string
    else {
        // stores number of ones at odd
        // and even position respectively
        int one_odd = 0, one_even = 0;

        for (int i = 0; i < N; i++) {
            if (s[i] == '1') {
                if (i % 2)
                    one_odd++;

                else
                    one_even++;
            }
        }

        return min(N / 2 - one_odd, N / 2 - one_even);
    }
}

// Driver code
int main()
{
    string s = "111000";

    cout << countMinSwaps(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// function to count minimum swaps
// required to make binary String
// alternating
static int countMinSwaps(String s)
{
    int N = s.length();

    // stores total number of ones
    int one = 0;

    // stores total number of zeroes
    int zero = 0;

    for (int i = 0; i < N; i++) {
        if (s.charAt(i) == '1')
            one++;
        else
            zero++;
    }

    // checking impossible condition
    if (one > zero + 1 || zero > one + 1)
        return -1;

    // odd length String
    if (N % 2 == 1)
    {

        // number of even positions
        int num = (N + 1) / 2;

        // stores number of zeroes and
        // ones at even positions
        int one_even = 0, zero_even = 0;

        for (int i = 0; i < N; i++) {
            if (i % 2 == 0) {
                if (s.charAt(i) == '1')
                    one_even++;
                else
                    zero_even++;
            }
        }

        if (one > zero)
            return num - one_even;

        else
            return num - zero_even;
    }

    // even length String
    else
    {

        // stores number of ones at odd
        // and even position respectively
        int one_odd = 0, one_even = 0;

        for (int i = 0; i < N; i++) {
            if (s.charAt(i) == '1') {
                if (i % 2 == 1)
                    one_odd++;

                else
                    one_even++;
            }
        }

        return Math.min(N / 2 - one_odd, N / 2 - one_even);
    }
}

// Driver code
public static void main(String[] args)
{
    String s = "111000";

    System.out.print(countMinSwaps(s));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python implementation of the above approach
# function to count minimum swaps
# required to make binary string
# alternating
def countMinSwaps(s):
    N = len(s)

    # stores total number of ones
    one = 0

    # stores total number of zeroes
    zero = 0

    for i in range(N):
        if (s[i] == '1'):
            one += 1
        else:
            zero += 1

    # checking impossible condition
    if (one > zero + 1 or zero > one + 1):
        return -1

    # odd length string
    if (N % 2):

        # number of even positions
        num = (N + 1) / 2

        # stores number of zeroes and
        # ones at even positions
        one_even = 0
        zero_even = 0

        for i in range(N):
            if (i % 2 == 0):
                if (s[i] == '1'):
                    one_even+=1
                else:
                    zero_even+=1

        if (one > zero):
            return num - one_even

        else:
            return num - zero_even

    # even length string
    else:
        # stores number of ones at odd
        # and even position respectively
        one_odd = 0
        one_even = 0

        for i in range(N):
            if (s[i] == '1'):
                if (i % 2):
                    one_odd+=1

                else:
                    one_even+=1

        return min(N // 2 - one_odd, N // 2 - one_even)

# Driver code
s = "111000"
print(countMinSwaps(s))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to count minimum swaps
// required to make binary String
// alternating
static int countMinSwaps(string s)
{
    int N = s.Length;

    // Stores total number of ones
    int one = 0;

    // Stores total number of zeroes
    int zero = 0;

    for(int i = 0; i < N; i++)
    {
        if (s[i] == '1')
            one++;
        else
            zero++;
    }

    // Checking impossible condition
    if (one > zero + 1 || zero > one + 1)
        return -1;

    // Odd length String
    if (N % 2 == 1)
    {

        // Number of even positions
        int num = (N + 1) / 2;

        // Stores number of zeroes and
        // ones at even positions
        int one_even = 0, zero_even = 0;

        for(int i = 0; i < N; i++)
        {
            if (i % 2 == 0)
            {
                if (s[i] == '1')
                    one_even++;
                else
                    zero_even++;
            }
        }
        if (one > zero)
            return num - one_even;
        else
            return num - zero_even;
    }

    // Even length String
    else
    {

        // Stores number of ones at odd
        // and even position respectively
        int one_odd = 0, one_even = 0;

        for(int i = 0; i < N; i++)
        {
            if (s[i] == '1')
            {
                if (i % 2 == 1)
                    one_odd++;
                else
                    one_even++;
            }
        }
        return Math.Min(N / 2 - one_odd,
                        N / 2 - one_even);
    }
}

// Driver code
public static void Main(String[] args)
{
    string s = "111000";

    Console.Write(countMinSwaps(s));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript implementation of the above approach
// function to count minimum swaps
// required to make binary String
// alternating
function countMinSwaps(s)
{
    var N = s.length;

    // stores total number of ones
    var one = 0;

    // stores total number of zeroes
    var zero = 0;

    for (var i = 0; i < N; i++) {
        if (s.charAt(i) == '1')
            one++;
        else
            zero++;
    }

    // checking impossible condition
    if (one > zero + 1 || zero > one + 1)
        return -1;

    // odd length String
    if (N % 2 == 1)
    {

        // number of even positions
        var num = (N + 1) / 2;

        // stores number of zeroes and
        // ones at even positions
        var one_even = 0, zero_even = 0;

        for (var i = 0; i < N; i++) {
            if (i % 2 == 0) {
                if (s.charAt(i) == '1')
                    one_even++;
                else
                    zero_even++;
            }
        }

        if (one > zero)
            return num - one_even;

        else
            return num - zero_even;
    }

    // even length String
    else
    {

        // stores number of ones at odd
        // and even position respectively
        var one_odd = 0, one_even = 0;

        for (var i = 0; i < N; i++) {
            if (s.charAt(i) == '1') {
                if (i % 2 == 1)
                    one_odd++;

                else
                    one_even++;
            }
        }

        return Math.min(N / 2 - one_odd, N / 2 - one_even);
    }
}

// Driver code
var s = "111000";

document.write(countMinSwaps(s));

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
1
```

**时间复杂度:** O(字符串长度)