# 一个字符串可以具有的不同排列的数量

> 原文:[https://www . geesforgeks . org/number-distinct-arrange-string-can/](https://www.geeksforgeeks.org/number-distinct-permutation-string-can/)

给我们一个只有小写字母的字符串。任务是找出该字符串可以生成的不同排列的总数。
示例:

```
Input : aab
Output : 3
Different permutations are "aab",
"aba" and "baa".

Input : ybghjhbuytb
Output : 1663200
```

一个**简单的解决方案**是找到所有[不同的排列](https://www.geeksforgeeks.org/print-all-permutations-of-a-string-with-duplicates-allowed-in-input-string/)并对它们进行计数。
我们可以找到计数**而不需要找到所有排列**。想法是找到所有重复的字符，即所有字符的频率。然后，我们用字符串长度的阶乘除以字符频率的阶乘。
在第二个例子中，字符数为 11，这里 **h** 和 **y** 重复 **2** 次，而 **g** 重复 **3** 次。
所以，排列数是 **11！/ (2!2!3!)= 1663200**
下面是上面想法的实现。

## C++

```
// C++ program to find number of distinct
// permutations of a string.
#include<bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// Utility function to find factorial of n.
int factorial(int n)
{
    int fact = 1;
    for (int i = 2; i <= n; i++)
        fact = fact * i;
    return fact;
}

// Returns count of distinct permutations
// of str.
int countDistinctPermutations(string str)
{
    int length = str.length();

    int freq[MAX_CHAR];
    memset(freq, 0, sizeof(freq));

    // finding frequency of all the lower case
    // alphabet and storing them in array of
    // integer
    for (int i = 0; i < length; i++)
        if (str[i] >= 'a')
            freq[str[i] - 'a']++;

    // finding factorial of number of appearances
    // and multiplying them since they are
    // repeating alphabets
    int fact = 1;
    for (int i = 0; i < MAX_CHAR; i++)
        fact = fact * factorial(freq[i]);

    // finding factorial of size of string and
    // dividing it by factorial found after
    // multiplying
    return factorial(length) / fact;
}

// Driver code
int main()
{
    string str = "fvvfhvgv";
    printf("%d", countDistinctPermutations(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of distinct
// permutations of a string.
public class GFG {

    static final int MAX_CHAR = 26;

    // Utility function to find factorial of n.
    static int factorial(int n)
    {
        int fact = 1;
        for (int i = 2; i <= n; i++)
            fact = fact * i;
        return fact;
    }

    // Returns count of distinct permutations
    // of str.
    static int countDistinctPermutations(String str)
    {
        int length = str.length();

        int[] freq = new int[MAX_CHAR];

        // finding frequency of all the lower case
        // alphabet and storing them in array of
        // integer
        for (int i = 0; i < length; i++)
            if (str.charAt(i) >= 'a')
                freq[str.charAt(i) - 'a']++;

        // finding factorial of number of appearances
        // and multiplying them since they are
        // repeating alphabets
        int fact = 1;
        for (int i = 0; i < MAX_CHAR; i++)
            fact = fact * factorial(freq[i]);

        // finding factorial of size of string and
        // dividing it by factorial found after
        // multiplying
        return factorial(length) / fact;
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "fvvfhvgv";
        System.out.println(countDistinctPermutations(str));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to find number of distinct
# permutations of a string.

MAX_CHAR = 26

# Utility function to find factorial of n.
def factorial(n) :

    fact = 1;
    for i in range(2, n + 1) :
        fact = fact * i;
    return fact

# Returns count of distinct permutations
# of str.
def countDistinctPermutations(st) :

    length = len(st)
    freq = [0] * MAX_CHAR

    # finding frequency of all the lower
    # case alphabet and storing them in
    # array of integer
    for i in range(0, length) :
        if (st[i] >= 'a') :
            freq[(ord)(st[i]) - 97] = freq[(ord)(st[i]) - 97] + 1;

    # finding factorial of number of
    # appearances and multiplying them
    # since they are repeating alphabets
    fact = 1
    for i in range(0, MAX_CHAR) :
        fact = fact * factorial(freq[i])

    # finding factorial of size of string
    # and dividing it by factorial found
    # after multiplying
    return factorial(length) / fact

# Driver code
st = "fvvfhvgv"
print (countDistinctPermutations(st))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find number of distinct
// permutations of a string.
using System;

public class GFG {

    static int MAX_CHAR = 26;

    // Utility function to find factorial of n.
    static int factorial(int n)
    {
        int fact = 1;
        for (int i = 2; i <= n; i++)
            fact = fact * i;

        return fact;
    }

    // Returns count of distinct permutations
    // of str.
    static int countDistinctPermutations(String str)
    {
        int length = str.Length;

        int[] freq = new int[MAX_CHAR];

        // finding frequency of all the lower case
        // alphabet and storing them in array of
        // integer
        for (int i = 0; i < length; i++)
            if (str[i] >= 'a')
                freq[str[i] - 'a']++;

        // finding factorial of number of appearances
        // and multiplying them since they are
        // repeating alphabets
        int fact = 1;
        for (int i = 0; i < MAX_CHAR; i++)
            fact = fact * factorial(freq[i]);

        // finding factorial of size of string and
        // dividing it by factorial found after
        // multiplying
        return factorial(length) / fact;
    }

    // Driver code
    public static void Main(String []args)
    {
        String str = "fvvfhvgv";

        Console.Write(countDistinctPermutations(str));
    }
}

// This code is contributed by parashar.
```

## java 描述语言

```
<script>
    // Javascript program to find number of distinct
    // permutations of a string.

    let MAX_CHAR = 26;

    // Utility function to find factorial of n.
    function factorial(n)
    {
        let fact = 1;
        for (let i = 2; i <= n; i++)
            fact = fact * i;
        return fact;
    }

    // Returns count of distinct permutations
    // of str.
    function countDistinctPermutations(str)
    {
        let length = str.length;

        let freq = new Array(MAX_CHAR);
        freq.fill(0);

        // finding frequency of all the lower case
        // alphabet and storing them in array of
        // integer
        for (let i = 0; i < length; i++)
            if (str[i].charCodeAt() >= 'a'.charCodeAt())
                freq[str[i].charCodeAt() - 'a'.charCodeAt()]++;

        // finding factorial of number of appearances
        // and multiplying them since they are
        // repeating alphabets
        let fact = 1;
        for (let i = 0; i < MAX_CHAR; i++)
            fact = fact * factorial(freq[i]);

        // finding factorial of size of string and
        // dividing it by factorial found after
        // multiplying
        return parseInt(factorial(length) / fact, 10);
    }

    let str = "fvvfhvgv";
    document.write(countDistinctPermutations(str));

    // This code is contributed by vaibhavrabadiya117.
</script>
```

输出:

```
840
```

本文由[阿迪蒂亚·库马尔](https://www.linkedin.com/in/aditya-kumar-837315100/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。