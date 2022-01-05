# 通过改变大小写来置换字符串

> 原文:[https://www.geeksforgeeks.org/permute-string-changing-case/](https://www.geeksforgeeks.org/permute-string-changing-case/)

打印字符串的所有排列，保持顺序但改变大小写。
**例:**

```
Input : ab
Output : AB Ab ab aB

Input : ABC
Output : abc Abc aBc ABc abC AbC aBC ABC
```

**方法 1(天真):**天真的方法是遍历整个字符串，对于每个字符，考虑两种情况，(1)改变大小写并重复出现(2)不改变大小写并重复出现。
**方法 2(更好)**对于长度为 n 的字符串，存在 2 个 <sup>n</sup> 最大组合。我们可以将其表示为按位运算。
在[打印所有子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中讨论了相同的想法。
以下是上述思路的实现:

## C++

```
// CPP code to print all permutations
// with respect to cases
#include <bits/stdc++.h>
using namespace std;

// Function to generate permutations
void permute(string input)
{
    int n = input.length();

    // Number of permutations is 2^n
    int max = 1 << n;

    // Converting string to lower case
        transform(input.begin(), input.end(), input.begin(),
                                                ::tolower);
    // Using all subsequences and permuting them
    for (int i = 0; i < max; i++) {

        // If j-th bit is set, we convert it to upper case
        string combination = input;
        for (int j = 0; j < n; j++)
            if (((i >> j) & 1) == 1)
                combination[j] = toupper(input.at(j));    

        // Printing current combination
        cout << combination << " ";
    }
}

// Driver code
int main()
{
    permute("ABC");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all permutations
// with respect to cases

public class PermuteString
{
    // Function to generate permutations
    static void permute(String input)
    {
        int n = input.length();

        // Number of permutations is 2^n
        int max = 1 << n;

        // Converting string to lower case
        input = input.toLowerCase();

        // Using all subsequences and permuting them
        for(int i = 0;i < max; i++)
        {
            char combination[] = input.toCharArray();

            // If j-th bit is set, we convert it to upper case
            for(int j = 0; j < n; j++)
            {
                if(((i >> j) &  1) == 1)
                    combination[j] = (char) (combination[j]-32);
            }

            // Printing current combination
            System.out.print(combination);
            System.out.print("   ");
        }
    }

    // Driver Program to test above function
    public static void main(String[] args)
    {
        permute("ABC");
    }
}

// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python code to print all permutations
# with respect to cases

# Function to generate permutations
def permute(inp):
    n = len(inp)

    # Number of permutations is 2^n
    mx = 1 << n

    # Converting string to lower case
    inp = inp.lower()

    # Using all subsequences and permuting them
    for i in range(mx):
        # If j-th bit is set, we convert it to upper case
        combination = [k for k in inp]
        for j in range(n):
            if (((i >> j) & 1) == 1):
                combination[j] = inp[j].upper()

        temp = ""
        # Printing current combination
        for i in combination:
            temp += i
        print temp,

# Driver code
permute("ABC")

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to print all permutations
// with respect to cases
using System;

class PermuteString  {

    // Function to generate
    // permutations
    static void permute(String input)
    {
        int n = input.Length;

        // Number of permutations is 2^n
        int max = 1 << n;

        // Converting string
        // to lower case
        input = input.ToLower();

        // Using all subsequences
        // and permuting them
        for(int i = 0;i < max; i++)
        {
            char []combination = input.ToCharArray();

            // If j-th bit is set, we
            // convert it to upper case
            for(int j = 0; j < n; j++)
            {
                if(((i >> j) & 1) == 1)
                    combination[j] = (char) (combination[j] - 32);
            }

            // Printing current combination
            Console.Write(combination);
            Console.Write(" ");
        }
    }

    // Driver Code
    public static void Main()
    {
        permute("ABC");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all permutations
// with respect to cases

// Function to generate permutations
function permute($input)
{
    $n = strlen($input);

    // Number of permutations is 2^n
    $max = 1 << $n;

    // Converting string to lower case
    $input = strtolower($input);

    // Using all subsequences and permuting them
    for($i = 0; $i < $max; $i++)
    {
        $combination = $input;

        // If j-th bit is set, we convert
        // it to upper case
        for($j = 0; $j < $n; $j++)
        {
            if((($i >> $j) & 1) == 1)
                $combination[$j] = chr(ord($combination[$j]) - 32);
        }

        // Printing current combination
        echo $combination . " ";
    }
}

// Driver Code
permute("ABC");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to print all permutations
// with respect to cases

// Function to generate permutations
function permute(input)
{
    var n = input.length;

    // Number of permutations is 2^n
    var max = 1 << n;

    // Converting string to lower case
    input = input.toLowerCase();

    // Using all subsequences and permuting them
    for(var i = 0;i < max; i++)
    {
        var combination = input.split('');

        // If j-th bit is set, we convert it to upper case
        for(var j = 0; j < n; j++)
        {
            if(((i >> j) &  1) == 1)
                combination[j] = String.fromCharCode(combination[j].charCodeAt(0)-32);
        }

        // Printing current combination
        document.write(combination.join(''));
        document.write("   ");
    }
}

// Driver Program to test above function
permute("ABC");

// This code contributed by Princi Singh
</script>
```

**输出:**

```
abc Abc aBc ABc abC AbC aBC ABC
```

问于:[脸书](https://www.geeksforgeeks.org/facebook-interview-preparation/)。
本文由**罗希特·塔普利亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。