# 在给定的约束条件下计算数字的数字分组

> 原文:[https://www . geesforgeks . org/count-groups-number-sum-digits-even-sub-group-less-equals-immediate-right-sub-group/](https://www.geeksforgeeks.org/count-groupings-number-sum-digits-every-sub-group-less-equals-immediate-right-sub-group/)

给我们一个由数字组成的字符串，我们可以将这些数字分组(但保持它们原来的顺序)。任务是计算分组的数量，使得对于除最后一个子组之外的每个子组，子组中的位数总和小于或等于紧邻其右侧的子组中的位数总和。
例如，数字 1119 的有效数字分组是(1-11-9)。第一个子组的位数总和是 1，下一个子组是 2，最后一个子组是 9。每个子群的和小于或等于它的右紧邻。
**例:**

```
Input : "1119"
Output: 7
Sub-groups: [1-119], [1-1-19], [1-11-9], [1-1-1-9],
            [11-19] and [111-9].
Note : Here we have included [1119] in the group and
       the sum of digits is 12 and this group has no 
       immediate right.

Input : "1234"
Output: 6
Sub-groups : [1234], [1-234], [12-34], [1-2-3-4],
             [12-3-4] and [1-2-34]
```

让“长度”是输入数字的长度。递归解决方案是考虑长度为 0-1 的每个位置。对于每个位置，递归地计算它后面所有可能的子组。下面是 C++实现的朴素递归解决方案。

## C++

```
// C++ program to count number of
// ways to group digits of a number
// such that sum of digits in every
// subgroup is less than or equal to
// its immediate right subgroup.
#include<bits/stdc++.h>
using namespace std;

// Function to find the subgroups
int countGroups(int position,
                int previous_sum,
                int length, char *num)
{
    // Terminating Condition
    if (position == length)
        return 1;

    int res = 0;

    // sum of digits
    int sum = 0;

    // Traverse all digits from
    // current position to rest
    // of the length of string
    for (int i = position; i < length; i++)
    {
        sum += (num[i] - '0');

        // If forward_sum is greater
        // than the previous sum,
        // then call the method again
        if (sum >= previous_sum)

        // Note : We pass current
        // sum as previous sum
        res += countGroups(i + 1, sum,
                           length, num);
    }

    // Total number of subgroups
    // till current position
    return res;
}

// Driver Code
int main()
{
    char num[] = "1119";
    int len = strlen(num);
    cout << countGroups(0, 0, len, num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of ways to group digits of 
// a number such that sum of 
// digits in every subgroup is
// less than or equal to its
// immediate right subgroup.
import java.io.*;

class GFG
{

// Function to find
// the subgroups
static int countGroups(int position,
                       int previous_sum,
                       int length,
                       String num)
{
    // Terminating Condition
    if (position == length)
        return 1;

    int res = 0;

    // sum of digits
    int sum = 0;

    // Traverse all digits from
    // current position to rest
    // of the length of string
    for (int i = position; i < length; i++)
    {
        sum += (num.charAt(i) - '0');

        // If forward_sum is greater
        // than the previous sum,
        // then call the method again
        if (sum >= previous_sum)

        // Note : We pass current
        // sum as previous sum
        res += countGroups(i + 1, sum,
                         length, num);
    }

    // Total number of subgroups
    // till current position
    return res;
}

// Driver Code
public static void main (String[] args)
{
    String num = "1119";
    int len =num .length();
    System.out.println(countGroups(0, 0,
                                   len, num));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to count
# number of ways to group digits
# of a number such that sum of
# digits in every subgroup
# is less than or equal to its immediate
# right subgroup.

# Function to find the subgroups
def countGroups(position, previous_sum,
               length, num):

    # Terminating Condition
    if(position == length):
        return 1

    res = 0
    # sum of digits
    sum = 0

    # Traverse all digits from
    # current position to rest
    # of the length of string
    for i in range(position, length):

        sum = sum + int(num[i])
        # If forward_sum is greater
        # than the previous sum,
        # then call the method again
        if (sum >= previous_sum):
            # Note : We pass current
            # sum as previous sum
            res = res + countGroups(i + 1, sum, length, num)

    # Total number of subgroups
    # till the current position
    return res

# Driver Code
if __name__=='__main__':
    num = "1119"
    len = len(num)
    print(countGroups(0, 0, len, num))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count number
// of ways to group digits of
// a number such that sum of
// digits in every subgroup is
// less than or equal to its
// immediate right subgroup.
using System;

class GFG
{

// Function to find
// the subgroups
static int countGroups(int position,
                       int previous_sum,
                       int length,
                       String num)
{
    // Terminating Condition
    if (position == length)
        return 1;

    int res = 0;

    // sum of digits
    int sum = 0;

    // Traverse all digits from
    // current position to rest
    // of the length of string
    for (int i = position; i < length; i++)
    {
        sum += (num[i] - '0');

        // If forward_sum is greater
        // than the previous sum,
        // then call the method again
        if (sum >= previous_sum)

        // Note : We pass current
        // sum as previous sum
        res += countGroups(i + 1, sum,
                           length, num);
    }

    // Total number of subgroups
    // till current position
    return res;
}

// Driver Code
public static void Main ()
{
    String num = "1119";
    int len = num.Length;
    Console.Write(countGroups(0, 0, len, num));
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of
// ways to group digits of a number
// such that sum of digits in every
// subgroup is less than or equal
// to its immediate right subgroup.

// Function to find the subgroups
function countGroups($position,
                     $previous_sum,
                     $length,$num)
{
    // Terminating Condition
    if ($position == $length)
        return 1;

    $res = 0;

    // sum of digits
    $sum = 0;

    // Traverse all digits from
    // current position to rest
    // of the length of string
    for ($i = $position; $i < $length; $i++)
    {
        $sum += ($num[$i] - '0');

        // If forward_sum is greater
        // than the previous sum,
        // then call the method again
        if ($sum >= $previous_sum)

        // Note : We pass current
        // sum as previous sum
        $res += countGroups($i + 1, $sum,
                            $length, $num);
    }

    // Total number of subgroups
    // till current position
    return $res;
}

// Driver Code
$num = "1119";
$len = strlen($num);
echo countGroups(0, 0, $len, $num);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to count number
    // of ways to group digits of
    // a number such that sum of
    // digits in every subgroup is
    // less than or equal to its
    // immediate right subgroup.

    // Function to find
    // the subgroups
    function countGroups(position,
                     previous_sum,
                      length, num)
    {
        // Terminating Condition
        if (position == length)
            return 1;

        let res = 0;

        // sum of digits
        let sum = 0;

        // Traverse all digits from
        // current position to rest
        // of the length of string
        for (let i = position; i < length; i++)
        {
            sum += (num[i].charCodeAt() - '0'.charCodeAt());

            // If forward_sum is greater
            // than the previous sum,
            // then call the method again
            if (sum >= previous_sum)

            // Note : We pass current
            // sum as previous sum
            res += countGroups(i + 1, sum, length, num);
        }

        // Total number of subgroups
        // till current position
        return res;
    }

    let num = "1119";
    let len = num.length;
    document.write(countGroups(0, 0, len, num));

</script>
```

**输出:**

```
7
```

如果我们仔细看看上面的递归解，我们会注意到可能有重叠的子问题。例如，如果输入数字是 12345，那么对于位置= 3 和 previous_sum = 3，我们重复两次。类似地，对于位置 4 和 previous_sum = 7，我们重复两次。因此，可以使用**动态编程**来优化上述解决方案。下面是一个基于动态规划的解决方案。

1.  数字的最大总和可以是 9 *长度，其中“长度”是输入数字的长度。
2.  创建一个 2D 数组 int dp[MAX][9*MAX]，其中 MAX 是输入数字的最大可能长度。值 DP[位置][上一个]将存储“位置”和“上一个 _ 总和”的结果。

3.  如果当前子问题已经过评估，即:DP[位置][上一个 _sum]！= -1，然后使用这个结果，否则递归计算它的值。

4.  如果将当前位置数字包括在总和中，即:sum = sum+num[位置]-'0 '，sum 变得大于等于前一个 sum，然后递增结果，并调用 num 中下一个位置的问题。
5.  如果 position == length，那么我们已经成功遍历了当前子群，返回 1；

下面是上述算法的实现。

## C++

```
// C++ program to count number of
// ways to group digits of a number
// such that sum of digits in every
// subgroup is less than or equal
// to its immediate right subgroup.
#include<bits/stdc++.h>
using namespace std;

// Maximum length of
// input number string
const int MAX = 40;

// A memoization table to store
// results of subproblems length
// of string is 40 and maximum
// sum will be 9 * 40 = 360.
int dp[MAX][9*MAX + 1];

// Function to find the count
// of splits with given condition
int countGroups(int position,
                int previous_sum,
                int length, char *num)
{
    // Terminating Condition
    if (position == length)
        return 1;

    // If already evaluated for
    // a given sub problem then
    // return the value
    if (dp[position][previous_sum] != -1)
        return dp[position][previous_sum];

    // countGroups for current
    // sub-group is 0
    dp[position][previous_sum] = 0;

    int res = 0;

    // sum of digits
    int sum = 0;

    // Traverse all digits from
    // current position to rest
    // of the length of string
    for (int i = position; i < length; i++)
    {
        sum += (num[i] - '0');

        // If forward_sum is greater
        // than the previous sum,
        // then call the method again
        if (sum >= previous_sum)

        // Note : We pass current
        // sum as previous sum
        res += countGroups(i + 1, sum,
                           length, num);
    }

    dp[position][previous_sum] = res;

    // total number of subgroups
    // till current position
    return res;
}

// Driver Code
int main()
{
    char num[] = "1119";
    int len = strlen(num);

    // Initialize dp table
    memset(dp, -1, sizeof(dp));

    cout << countGroups(0, 0, len, num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// Java program to count the number of
// ways to group digits of a number
// such that sum of digits in every
// subgroup is less than or equal
// to its immediate right subgroup.
class GFG
{

// Maximum length of
// input number string
static int MAX = 40;

// A memoization table to store
// results of subproblems length
// of string is 40 and maximum
// sum will be 9 * 40 = 360.
static int dp[][] = new int[MAX][9 * MAX + 1];

// Function to find the count
// of splits with given condition
static int countGroups(int position,
                int previous_sum,
                int length, char []num)
{
    // Terminating Condition
    if (position == length)
        return 1;

    // If already evaluated for
    // a given sub problem then
    // return the value
    if (dp[position][previous_sum] != -1)
        return dp[position][previous_sum];

    // countGroups for current
    // sub-group is 0
    dp[position][previous_sum] = 0;

    int res = 0;

    // sum of digits
    int sum = 0;

    // Traverse all digits from
    // current position to rest
    // of the length of string
    for (int i = position; i < length; i++)
    {
        sum += (num[i] - '0');

        // If forward_sum is greater
        // than the previous sum,
        // then call the method again
        if (sum >= previous_sum)

        // Note : We pass current
        // sum as previous sum
        res += countGroups(i + 1, sum,
                        length, num);
    }

    dp[position][previous_sum] = res;

    // total number of subgroups
    // till current position
    return res;
}

// Driver Code
public static void main(String[] args)
{
    char num[] = "1119".toCharArray();
    int len = num.length;

    // Initialize dp table
    for(int i = 0; i < dp.length; i++)
    {
        for(int j = 0;j < 9 * MAX + 1; j++){
            dp[i][j] = -1;
        }
    }
    System.out.println(countGroups(0, 0, len, num));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count the number of
# ways to group digits of a number
# such that sum of digits in every
# subgroup is less than or equal
# to its immediate right subgroup.

# Maximum length of
# input number string
MAX = 40

# A memoization table to store
# results of subproblems length
# of string is 40 and maximum
# sum will be 9 * 40 = 360.
dp = [[ -1 for i in range(9 * MAX + 1)]
           for i in range(MAX)]

# Function to find the count
# of splits with given condition
def countGroups(position, previous_sum,
                           length, num):

    # Terminating Condition
    if (position == length):
        return 1

    # If already evaluated for
    # a given sub problem then
    # return the value
    if (dp[position][previous_sum] != -1):
        return dp[position][previous_sum]

    # countGroups for current
    # sub-group is 0
    dp[position][previous_sum] = 0

    res = 0

    # sum of digits
    sum = 0

    # Traverse all digits from
    # current position to rest
    # of the length of string
    for i in range(position,length):
        sum += (ord(num[i]) - ord('0'))

        # If forward_sum is greater
        # than the previous sum,
        # then call the method again
        if (sum >= previous_sum):

            # Note : We pass current
            # sum as previous sum
            res += countGroups(i + 1, sum,
                               length, num)

    dp[position][previous_sum] = res

    # total number of subgroups
    # till the current position
    return res

# Driver Code
num = "1119"
len = len(num)

print(countGroups(0, 0, len, num))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to count number of
// ways to group digits of a number
// such that sum of digits in every
// subgroup is less than or equal
// to its immediate right subgroup.
using System;

class GFG
{
    // Maximum length of
    // input number string
    static int MAX = 40;

    // A memoization table to store
    // results of subproblems length
    // of string is 40 and maximum
    // sum will be 9 * 40 = 360.
    static int[,] dp = new int[MAX, 9 * MAX + 1];

    // Function to find the count
    // of splits with given condition
    static int countGroups(int position,
                            int previous_sum,
                            int length, char[] num)
    {
        // Terminating Condition
        if (position == length)
            return 1;

        // If already evaluated for
        // a given sub problem then
        // return the value
        if (dp[position,previous_sum] != -1)
            return dp[position,previous_sum];

        // countGroups for current
        // sub-group is 0
        dp[position,previous_sum] = 0;

        int res = 0;

        // sum of digits
        int sum = 0;

        // Traverse all digits from
        // current position to rest
        // of the length of string
        for (int i = position; i < length; i++)
        {
            sum += (num[i] - '0');

            // If forward_sum is greater
            // than the previous sum,
            // then call the method again
            if (sum >= previous_sum)

            // Note : We pass current
            // sum as previous sum
            res += countGroups(i + 1, sum,
                            length, num);
        }

        dp[position,previous_sum] = res;

        // total number of subgroups
        // till current position
        return res;
    }

    // Driver Code
    static void Main()
    {
        char[] num = {'1', '1', '1', '9'};
        int len = num.Length;

        // Initialize dp table
        for(int i = 0; i < MAX; i++)
            for(int j = 0; j < 9 * MAX + 1; j++)
                dp[i, j] = -1;

        Console.Write(countGroups(0, 0, len, num));
    }
}

// This code is contributed by DrRoot_
```

## java 描述语言

```
<script>

// Javascript program to count the number of
// ways to group digits of a number
// such that sum of digits in every
// subgroup is less than or equal
// to its immediate right subgroup.

    // Maximum length of
    // input number string
    let MAX = 40;
    // A memoization table to store
    // results of subproblems length
    // of string is 40 and maximum
    // sum will be 9 * 40 = 360.
    let dp=new Array(MAX);

    // Function to find the count
    // of splits with given condition
    function countGroups( position,previous_sum,length,num)
    {
        // Terminating Condition
    if (position == length)
        return 1;

    // If already evaluated for
    // a given sub problem then
    // return the value
    if (dp[position][previous_sum] != -1)
        return dp[position][previous_sum];

    // countGroups for current
    // sub-group is 0
    dp[position][previous_sum] = 0;

    let res = 0;

    // sum of digits
    let sum = 0;

    // Traverse all digits from
    // current position to rest
    // of the length of string
    for (let i = position; i < length; i++)
    {
        sum += (num[i] - '0');

        // If forward_sum is greater
        // than the previous sum,
        // then call the method again
        if (sum >= previous_sum)

        // Note : We pass current
        // sum as previous sum
        res += countGroups(i + 1, sum,
                        length, num);
    }

    dp[position][previous_sum] = res;

    // total number of subgroups
    // till current position
    return res;
    }

    // Driver Code
    let num = "1119".split("");
    let len = num.length;
    // Initialize dp table
    for(let i = 0; i < dp.length; i++)
    {   
        dp[i]=new Array(9 * MAX + 1)
        for(let j = 0;j < 9 * MAX + 1; j++){
            dp[i][j] = -1;
        }
    }
    document.write(countGroups(0, 0, len, num));

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
 7
```

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。本文由 GeeksForGeeks 团队审阅。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。