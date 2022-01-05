# 一个数的可能切割，使得最大部分可被 3 整除

> 原文:[https://www . geeksforgeeks . org/可能的最大零件数可被 3 整除/](https://www.geeksforgeeks.org/possible-cuts-of-a-number-such-that-maximum-parts-are-divisible-by-3/)

给定一个大的数字 N(N 中的位数最多可达 10 <sup>5</sup> )。任务是找到一个数所需的割，使得最大部分能被 3 整除。
**例:**

```
Input: N = 1269
Output: 3
Cut the number as 12|6|9\. So, 12, 6, 9 are the 
three numbers which are divisible by 3.

Input: N = 71
Output: 0
However, we make cuts there is no such number 
that is divisible by 3\. 
```

**方法:**
我们来计算数组 res[0…n]的值，其中 res[i]是长度为 I 的前缀的答案，显然，res[0]:=0，因为对于空字符串(长度为 0 的前缀)，答案是 0。
对于 i > 0，可以通过以下方式找到 RES[I:

*   我们来看长度为 I 的前缀的最后一位，它有索引 i-1。要么它不属于可被 3 整除的段，要么它属于。
*   如果不属于，表示最后一位数字不能用，所以 **res[i]=res[i-1]** 。如果它属于，那么找到最短的**s【j..可被 3 整除的 i-1]** 并尝试用值 **res[j]+1** 更新 **res[i]** 。
*   一个数可以被 3 整除，当且仅当它的数字之和可以被 3 整除。所以任务是找到 s[0…i-1]的最短后缀，数字之和可被 3 整除。如果这样的后缀是 s[j..i-1]然后 s[0..j-1]和 s[0..i-1]具有模 3 的数字和的相同余数。
*   让我们维护提醒索引[0..2]-长度为 3 的数组，其中 remIndex[r]是处理时间最长的前缀的长度，数字之和等于 r 模 3。如果没有这样的前缀，请使用 remIndex[r]= -1。很容易看出 j=remIndex[r]，其中 r 是以 3 为模的第 I 个前缀上的数字之和。
*   所以要找到子串 s[j]的最大 j<=i-1..i-1]可被 3 整除，只需检查 remIndex[r]不等于-1，并使用 j=remIndex[r]，其中 r 是第 I 个前缀上的数字之和，以 3 为模。
*   这意味着为了处理最后一个数字属于可被 3 整除的段的情况，尝试用值 res[remIndex[r]]+1 更新 res[i]。换句话说，只要做 if (remIndex[r]！= -1) => res[i] = max(res[i]，res[remIndex[r]] + 1)。

以下是上述方法的实现:

## C++

```
// CPP program to find the maximum number of
// numbers divisible by 3 in a large number
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of
// numbers divisible by 3 in a large number
int MaximumNumbers(string s)
{
    // store size of the string
    int n = s.length();

    // Stores last index of a remainder
    vector<int> remIndex(3, -1);

    // last visited place of remainder
    // zero is at 0.
    remIndex[0] = 0;

    // To store result from 0 to i
    vector<int> res(n + 1);

    int r = 0;
    for (int i = 1; i <= n; i++) {

        // get the remainder
        r = (r + s[i-1] - '0') % 3;

        // Get maximum res[i] value
        res[i] = res[i-1];
        if (remIndex[r] != -1)
            res[i] = max(res[i], res[remIndex[r]] + 1);

        remIndex[r] = i+1;
    }

    return res[n];
}

// Driver Code
int main()
{
    string s = "12345";
    cout << MaximumNumbers(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum number of
// numbers divisible by 3 in a large number
import java.util.*;

class GFG
{

// Function to find the maximum number of
// numbers divisible by 3 in a large number
static int MaximumNumbers(String s)
{
    // store size of the string
    int n = s.length();

    // Stores last index of a remainder
    int [] remIndex={-1, -1, -1};

    // last visited place of remainder
    // zero is at 0.
    remIndex[0] = 0;

    // To store result from 0 to i
    int[] res = new int[n + 1];

    int r = 0;
    for (int i = 1; i <= n; i++)
    {

        // get the remainder
        r = (r + s.charAt(i-1) - '0') % 3;

        // Get maximum res[i] value
        res[i] = res[i - 1];
        if (remIndex[r] != -1)
            res[i] = Math.max(res[i],
                    res[remIndex[r]] + 1);

        remIndex[r] = i + 1;
    }

    return res[n];
}

// Driver Code
public static void main (String[] args)
{
    String s = "12345";
    System.out.println(MaximumNumbers(s));
}
}

// This code is contributed by
// chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# number of numbers divisible by 3 in
# a large number
import math as mt

# Function to find the maximum number
# of numbers divisible by 3 in a
# large number
def MaximumNumbers(string):

    # store size of the string
    n = len(string)

    # Stores last index of a remainder
    remIndex = [-1 for i in range(3)]

    # last visited place of remainder
    # zero is at 0.
    remIndex[0] = 0

    # To store result from 0 to i
    res = [-1 for i in range(n + 1)]

    r = 0
    for i in range(n + 1):

        # get the remainder
        r = (r + ord(string[i - 1]) -
                 ord('0')) % 3

        # Get maximum res[i] value
        res[i] = res[i - 1]
        if (remIndex[r] != -1):
            res[i] = max(res[i], res[remIndex[r]] + 1)

        remIndex[r] = i + 1

    return res[n]

# Driver Code
s= "12345"
print(MaximumNumbers(s))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to find the maximum number of
// numbers divisible by 3 in a large number .
using System;

class GFG
{

    // Function to find the maximum number of
    // numbers divisible by 3 in a large number
    static int MaximumNumbers(String s)
    {
        // store size of the string
        int n = s.Length;

        // Stores last index of a remainder
        int [] remIndex = {-1, -1, -1};

        // last visited place of remainder
        // zero is at 0.
        remIndex[0] = 0;

        // To store result from 0 to i
        int[] res = new int[n + 1];

        int r = 0;
        for (int i = 1; i <= n; i++)
        {

            // get the remainder
            r = (r + s[i-1] - '0') % 3;

            // Get maximum res[i] value
            res[i] = res[i - 1];
            if (remIndex[r] != -1)
                res[i] = Math.Max(res[i],
                        res[remIndex[r]] + 1);

            remIndex[r] = i + 1;
        }
        return res[n];
    }

    // Driver Code
    public static void Main (String[] args)
    {
        String s = "12345";
        Console.WriteLine(MaximumNumbers(s));
    }
}

// This code has been contributed by
// PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum number of
// numbers divisible by 3 in a large number

// Function to find the maximum number of
// numbers divisible by 3 in a large number
function MaximumNumbers($s)
{
    // store size of the string
    $n = strlen($s) ;

    // Stores last index of a remainder
    $remIndex = array_fill(0,3,-1) ;

    // last visited place of remainder
    // zero is at 0.
    $remIndex[0] = 0;

    // To store result from 0 to i
    $res = array() ;

    $r = 0;
    for ($i = 1; $i <= $n; $i++) {

        // get the remainder
        $r = ($r + $s[$i-1] - '0') % 3;

        // Get maximum res[i] value
        $res[$i] = $res[$i-1];
        if ($remIndex[$r] != -1)
            $res[$i] = max($res[$i], $res[$remIndex[$r]] + 1);

        $remIndex[$r] = $i+1;
    }

    return $res[$n];
}

    // Driver Code
    $s = "12345";
    print(MaximumNumbers($s))

    # This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript program to find the maximum number of
// numbers divisible by 3 in a large number

// Function to find the maximum number of
// numbers divisible by 3 in a large number
function MaximumNumbers(s)
{
    // store size of the string
    let n = s.length;

    // Stores last index of a remainder
    let remIndex=[-1, -1, -1];

    // last visited place of remainder
    // zero is at 0.
    remIndex[0] = 0;

    // To store result from 0 to i
    let res = new Array(n + 1);
      for(let i=0;i<res.length;i++)
    {
        res[i]=0;
    }

    let r = 0;
    for (let i = 1; i <= n; i++)
    {

        // get the remainder
        r = (r + s[i-1].charCodeAt(0) - '0'.charCodeAt(0)) % 3;

        // Get maximum res[i] value
        res[i] = res[i - 1];
        if (remIndex[r] != -1)
            res[i] = Math.max(res[i],
                    res[remIndex[r]] + 1);

        remIndex[r] = i + 1;
    } 
    return res[n];
}

// Driver Code
let s = "12345";
document.write(MaximumNumbers(s));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
```

**另一种方法:**
我们可以使用 running_sum，它保持所有连续整数的和，其中没有一个单个整数可以被 3 整除。我们可以逐个传递每个整数，并执行以下操作:

1.  如果整数可被 3 整除，或者 running_sum 非零且可被 3 整除，则递增计数器并重置 running_sum。
2.  如果整数不能被 3 整除，记录所有连续整数的和。

## C++

```
// C++ program to find the maximum number
// of numbers divisible by 3 in large number
#include <iostream>
using namespace std;

int get_max_splits(string num_string)
{
    // This will contain the count of the splits
    int count = 0, current_num;

    // This will keep sum of all successive
    // integers, when they are indivisible by 3
    int running_sum = 0;
    for (int i = 0; i < num_string.length(); i++)
    {
        current_num = num_string[i] - '0';
        running_sum += current_num;

        // This is the condition of finding a split
        if (current_num % 3 == 0 ||
        (running_sum != 0 && running_sum % 3 == 0))
        {
            count += 1;
            running_sum = 0;
        }
    }

    return count;
}

// Driver code
int main()
{
    cout << get_max_splits("12345") << endl;
    return 0;
}

// This code is contributed by Rituraj Jain
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum number
// of numbers divisible by 3 in large number
class GFG
{

static int get_max_splits(String num_String)
{
    // This will contain the count of the splits
    int count = 0, current_num;

    // This will keep sum of all successive
    // integers, when they are indivisible by 3
    int running_sum = 0;
    for (int i = 0; i < num_String.length(); i++)
    {
        current_num = num_String.charAt(i) - '0';
        running_sum += current_num;

        // This is the condition of finding a split
        if (current_num % 3 == 0 ||
        (running_sum != 0 && running_sum % 3 == 0))
        {
            count += 1;
            running_sum = 0;
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    System.out.print(get_max_splits("12345") +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# number of numbers divisible by 3 in
# a large number
def get_max_splits(num_string):

    # This will contain the count of the splits
    count = 0

     # This will keep sum of all successive
     # integers, when they are indivisible by 3
    running_sum = 0
    for i in range(len(num_string)):
        current_num = int(num_string[i])
        running_sum += current_num

        # This is the condition of finding a split
        if current_num % 3 == 0 or (running_sum != 0 and running_sum % 3 == 0):
            count += 1
            running_sum = 0
    return count

print get_max_splits("12345")

# This code is contributed by Amit Ranjan
```

## C#

```
// C# program to find the maximum number
// of numbers divisible by 3 in large number
using System;

class GFG
{

static int get_max_splits(String num_String)
{
    // This will contain the count of the splits
    int count = 0, current_num;

    // This will keep sum of all successive
    // integers, when they are indivisible by 3
    int running_sum = 0;
    for (int i = 0; i < num_String.Length; i++)
    {
        current_num = num_String[i] - '0';
        running_sum += current_num;

        // This is the condition of finding a split
        if (current_num % 3 == 0 ||
        (running_sum != 0 && running_sum % 3 == 0))
        {
            count += 1;
            running_sum = 0;
        }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    Console.Write(get_max_splits("12345") +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum
// number of numbers divisible by 3 in
// a large number
function get_max_splits($num_string)
{
    // This will contain the count of
    // the splits
    $count = 0;

    // This will keep sum of all successive
    // integers, when they are indivisible by 3
    $running_sum = 0;
    for ($i = 0; $i < strlen($num_string); $i++)
    {
        $current_num = intval($num_string[$i]);
        $running_sum += $current_num;

        // This is the condition of finding a split
        if ($current_num % 3 == 0 or
           ($running_sum != 0 and $running_sum % 3 == 0))
            {
                $count += 1;
                $running_sum = 0;
            }
    }

    return $count;
}

// Driver Code
print(get_max_splits("12345"));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum number
// of numbers divisible by 3 in large number

function get_max_splits(num_String)
{
    // This will contain the count of the splits
    let count = 0, current_num;

    // This will keep sum of all successive
    // integers, when they are indivisible by 3
    let running_sum = 0;
    for (let i = 0; i < num_String.length; i++)
    {
        current_num = num_String[i].charCodeAt(0) -
        '0'.charCodeAt(0);
        running_sum += current_num;

        // This is the condition of finding a split
        if (current_num % 3 == 0 ||
        (running_sum != 0 && running_sum % 3 == 0))
        {
            count += 1;
            running_sum = 0;
        }
    }
    return count;
}

// Driver code
document.write(get_max_splits("12345") +"<br>");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
3
```