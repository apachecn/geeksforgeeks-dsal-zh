# 子串 3 次查询可分性

> 原文:[https://www . geeksforgeeks . org/sub-string-可除以 3-query/](https://www.geeksforgeeks.org/sub-string-divisibility-by-3-queries/)

给定一个大的数字，n(具有 10^6 之前的数字)和各种形式的查询:
查询(l，r):查找索引 l 和 r(两者都包括)之间的子串是否可被 3 整除。
示例:

```
Input: n = 12468236544
Queries:
l=0 r=1
l=1 r=2
l=3 r=6
l=0 r=10
Output:
Divisible by 3 
Divisible by 3 
Not divisible by 3
Divisible by 3

Explanation:
In the first query, 12 is divisible by 3
In the second query, 24 is divisible by 3 and so on.
```

我们知道，任何一个数，如果它的位数之和能被 3 整除，它就能被 3 整除。因此，我们的想法是预处理一个存储数字总和的辅助数组。

```
Mathematically,
sum[0] = 0
and 
for i from 0 to number of digits of number:
    sum[i+1] = sum[i]+ toInt(n[i])
where toInt(n[i]) represents the integer value 
of i'th digit of n 
```

一旦我们的辅助数组被处理，我们就可以在 O(1)时间内回答每个查询，因为只有当(sum[r+1]-sum[l])%3 == 0 时，从索引 l 到 r 的子串才能被 3 整除。

## C++

```
// C++ program to answer multiple queries of
// divisibility by 3 in substrings of a number
#include <iostream>
using namespace std;

// Array to store the sum of digits
int sum[1000005];

// Utility function to evaluate a character's
// integer value
int toInt(char x)
{
    return int(x) - '0';
}

// This function receives the string representation
// of the number and precomputes the sum array
void prepareSum(string s)
{
    sum[0] = 0;
    for (int i=0; i<s.length(); i++)
        sum[i+1] = sum[i] + toInt(s[i]);
}

// This function receives l and r representing
// the indices and prints the required output
void query(int l,int r)
{
    if ((sum[r+1]-sum[l])%3 == 0)
        cout << "Divisible by 3\n";
    else
        cout << "Not divisible by 3\n";
}

// Driver function to check the program
int main()
{
    string n = "12468236544";

    prepareSum(n);
    query(0, 1);
    query(1, 2);
    query(3, 6);
    query(0, 10);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to answer multiple queries of
// divisibility by 3 in substrings of a number
class GFG
{

    // Array to store the sum of digits
    static int sum[] = new int[1000005];

    // Utility function to evaluate a character's
    // integer value
    static int toInt(char x)
    {
        return x - '0';
    }

    // This function receives the string representation
    // of the number and precomputes the sum array
    static void prepareSum(String s)
    {
        sum[0] = 0;
        for (int i = 0; i < s.length(); i++)
        {
            sum[i + 1] = sum[i] + toInt(s.charAt(i));
        }
    }

    // This function receives l and r representing
    // the indices and prints the required output
    static void query(int l, int r)
    {
        if ((sum[r + 1] - sum[l]) % 3 == 0)
        {
            System.out.println("Divisible by 3");
        }
        else
        {
            System.out.println("Not divisible by 3");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String n = "12468236544";

        prepareSum(n);
        query(0, 1);
        query(1, 2);
        query(3, 6);
        query(0, 10);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to answer multiple queries of
# divisibility by 3 in substrings of a number

# Array to store the sum of digits
sum = [0 for i in range(1000005)]

# Utility function to evaluate a character's
# integer value
def toInt(x):

    return int(x)

# This function receives the string representation
# of the number and precomputes the sum array
def prepareSum(s):

    sum[0] = 0
    for i in range(0, len(s)):
        sum[i + 1] = sum[i] + toInt(s[i])

# This function receives l and r representing
# the indices and prs the required output
def query(l, r):

    if ((sum[r + 1] - sum[l]) % 3 == 0):
        print("Divisible by 3")
    else:
        print("Not divisible by 3")

# Driver function to check the program
if __name__=='__main__':

    n = "12468236544"
    prepareSum(n)
    query(0, 1)
    query(1, 2)
    query(3, 6)
    query(0, 10)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to answer multiple queries of
// divisibility by 3 in substrings of a number
using System;

class GFG
{

    // Array to store the sum of digits
    static int []sum = new int[1000005];

    // Utility function to evaluate a character's
    // integer value
    static int toInt(char x)
    {
        return x - '0';
    }

    // This function receives the string representation
    // of the number and precomputes the sum array
    static void prepareSum(String s)
    {
        sum[0] = 0;
        for (int i = 0; i < s.Length; i++)
        {
            sum[i + 1] = sum[i] + toInt(s[i]);
        }
    }

    // This function receives l and r representing
    // the indices and prints the required output
    static void query(int l, int r)
    {
        if ((sum[r + 1] - sum[l]) % 3 == 0)
        {
            Console.WriteLine("Divisible by 3");
        }
        else
        {
            Console.WriteLine("Not divisible by 3");
        }
    }

    // Driver code
    public static void Main()
    {
        String n = "12468236544";

        prepareSum(n);
        query(0, 1);
        query(1, 2);
        query(3, 6);
        query(0, 10);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to answer multiple queries of
// divisibility by 3 in substrings of a number

    // Array to store the sum of digits
    let sum = [];

    // Utility function to evaluate a character's
    // integer value
    function toInt(x)
    {
        return x - '0';
    }

    // This function receives the string representation
    // of the number and precomputes the sum array
    function prepareSum(s)
    {
        sum[0] = 0;
        for (let i = 0; i < s.length; i++)
        {
            sum[i + 1] = sum[i] + toInt(s[i]);
        }
    }

    // This function receives l and r representing
    // the indices and prints the required output
    function query(l, r)
    {
        if ((sum[r + 1] - sum[l]) % 3 == 0)
        {
            document.write("Divisible by 3" + "<br />");
        }
        else
        {
            document.write("Not divisible by 3" + "<br />");
        }
    }

// Driver Code

        let n = "12468236544";

        prepareSum(n);
        query(0, 1);
        query(1, 2);
        query(3, 6);
        query(0, 10);

</script>
```

**输出:**

```
Divisible by 3
Divisible by 3
Not divisible by 3
Divisible by 3
```

本文由 [**阿舒托什·库马尔**](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。