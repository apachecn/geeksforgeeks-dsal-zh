# 按字典顺序排列的幂集

> 原文:[https://www . geesforgeks . org/powet-set-词典顺序/](https://www.geeksforgeeks.org/powet-set-lexicographic-order/)

本文是关于按字典顺序生成[幂集](https://www.geeksforgeeks.org/power-set/)。
**例:**

```
Input : abc
Output : a ab abc ac b bc c
```

想法是先排序数组。排序后，逐个固定字符，并从它们开始递归生成所有子集。每次递归调用后，我们移除最后一个字符，以便生成下一个置换。

## C++

```
// CPP program to generate power set in
// lexicographic order.
#include <bits/stdc++.h>
using namespace std;

// str : Stores input string
// n : Length of str.
void func(string s, vector<string>& str, int n, int pow_set)
{
    int i, j;
    for (i = 0; i < pow_set; i++) {
        string x;
        for (j = 0; j < n; j++) {
            if (i & 1 << j) {
                x = x + s[j];
            }
        }
        if (i != 0)
            str.push_back(x);
    }
}
int main()
{
    int n;
    string s;
    vector<string> str;
    s = "cab";
    n = s.length();
    int pow_set = pow(2, n);
    func(s, str, n, pow_set);
    sort(str.begin(), str.end());
    for (int i = 0; i < str.size(); i++)
        cout << str[i] << " ";
    cout << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate power set in
// lexicographic order.
import java.util.*;

class GFG {

    // str : Stores input string
    // n : Length of str.
    // curr : Stores current permutation
    // index : Index in current permutation, curr
    static void permuteRec(String str, int n,
                           int index, String curr)
    {
        // base case
        if (index == n) {
            return;
        }
        System.out.println(curr);
        for (int i = index + 1; i < n; i++) {

            curr += str.charAt(i);
            permuteRec(str, n, i, curr);

            // backtracking
            curr = curr.substring(0, curr.length() - 1);
        }
        return;
    }

    // Generates power set in lexicographic
    // order.
    static void powerSet(String str)
    {
        char[] arr = str.toCharArray();
        Arrays.sort(arr);
        permuteRec(new String(arr), str.length(), -1, "");
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "cab";
        powerSet(str);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to generate power
# set in lexicographic order.

# str : Stores input string
# n : Length of str.
# curr : Stores current permutation
# index : Index in current permutation, curr
def permuteRec(string, n, index = -1, curr = ""):

    # base case
    if index == n:
        return

    if len(curr) > 0:
        print(curr)

    for i in range(index + 1, n):
        curr += string[i]
        permuteRec(string, n, i, curr)

        # backtracking
        curr = curr[:len(curr) - 1]

# Generates power set in lexicographic order
def powerSet(string):
    string = ''.join(sorted(string))
    permuteRec(string, len(string))

# Driver Code
if __name__ == "__main__":
    string = "cab"
    powerSet(string)

# This code is contributed by vibhu4agarwal
```

## C#

```
// C# program to generate power set in
// lexicographic order.
using System;

class GFG {

    // str : Stores input string
    // n : Length of str.
    // curr : Stores current permutation
    // index : Index in current permutation, curr
    static void permuteRec(String str, int n,
                           int index, String curr)
    {
        // base case
        if (index == n) {
            return;
        }
        Console.WriteLine(curr);
        for (int i = index + 1; i < n; i++) {

            curr += str[i];
            permuteRec(str, n, i, curr);

            // backtracking
            curr = curr.Substring(0, curr.Length - 1);
        }
        return;
    }

    // Generates power set in lexicographic
    // order.
    static void powerSet(String str)
    {
        char[] arr = str.ToCharArray();
        Array.Sort(arr);
        permuteRec(new String(arr), str.Length, -1, "");
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "cab";
        powerSet(str);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate power
// set in lexicographic order.

// str : Stores input string
// n : Length of str.
// curr : Stores current permutation
// index : Index in current permutation, curr
function permuteRec($str, $n, $index = -1,
                              $curr = "")
{
    // base case
    if ($index == $n)
        return;

    echo $curr."\n";
    for ($i = $index + 1; $i < $n; $i++)
    {

        $curr=$curr.$str[$i];
        permuteRec($str, $n, $i, $curr);

        // backtracking
        $curr ="";
    }
    return;
}

// Generates power set in lexicographic
// order.
function powerSet($str)
{

    $str = str_split($str);
    sort($str);
    permuteRec($str, sizeof($str));
}

// Driver code
$str = "cab";
powerSet($str);

// This code is contributed by Mithun Kumar
?>
```

## java 描述语言

```
<script>
// javascript program to generate power set in
// lexicographic order.

    // str : Stores input string
    // n : Length of str.
    // curr : Stores current permutation
    // index : Index in current permutation, curr
    function permuteRec( str , n , index,  curr) {
        // base case
        if (index == n) {
            return;
        }
        document.write(curr+" ");
        for (var i = index + 1; i < n; i++) {

            curr += str[i];
            permuteRec(str, n, i, curr);

            // backtracking
            curr = curr.substring(0, curr.length - 1);
        }
        return;
    }

    // Generates power set in lexicographic
    // order.
    function powerSet(str) {
        var arr = str.split("");
        arr.sort();
        permuteRec(arr, str.length, -1, "");
    }

    // Driver code

        var str = "cab";
        powerSet(str);

// This code contributed by umadevi9616
</script>
```

**Output**

```
a ab b c ca cab cb 
```