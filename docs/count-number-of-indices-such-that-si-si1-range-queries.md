# 计算索引数量，使得 s[i] = s[i+1]:范围查询

> 原文:[https://www . geesforgeks . org/count-number-of-indexes-so-si-si1-range-query/](https://www.geeksforgeeks.org/count-number-of-indices-such-that-si-si1-range-queries/)

给定一根弦**弦**。现在，对于由两个整数 **L** 和 **R** 组成的每个查询，任务是找到索引的数量，使得 **str[i] = str[i+1]** 和 **L ≤ i，i+1 ≤ R** 。
**举例:**

> **输入:**str = " gggggggggg "，query[] = {{1，2}，{1，5}}
> **输出:** 1 4
> 第一次查询答案为 1，第二次查询答案为 4。
> 除了每个查询中的最后一个索引外，该条件对所有索引都成立。
> **输入:** str = "geeg "，查询[] = {{0，3}}
> **输出:** 1
> 条件只对 i = 1 成立。

**方法:**创建前缀数组 **pref** 使得**pref【I】**保存从 **1** 到 **i-1** 的所有索引的计数，使得 **str[i] = str[i+1]** 。现在对于每个查询 **(L，R)** ，结果将是**pref[R]–pref[L]**。
以下是上述方法的实施:

## C++

```
// C++ program to find substring with 
#include <bits/stdc++.h>
using namespace std;

// Function to create prefix array
void preCompute(int n, string s, int pref[])
{
    pref[0] = 0;
    for (int i = 1; i < n; i++) {
        pref[i] = pref[i - 1];
        if (s[i - 1] == s[i])
            pref[i]++;
    }
}

// Function to return the result of the query
int query(int pref[], int l, int r)
{
    return pref[r] - pref[l];
}

// Driver Code
int main()
{
    string s = "ggggggg";
    int n = s.length();

    int pref[n];
    preCompute(n, s, pref);

    // Query 1
    int l = 1;
    int r = 2;
    cout << query(pref, l, r) << endl;

    // Query 2
    l = 1;
    r = 5;
    cout << query(pref, l, r) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find substring with

import java.io.*;

class GFG {

// Function to create prefix array
static void preCompute(int n, String s, int pref[])
{
    pref[0] = 0;
    for (int i = 1; i < n; i++) {
        pref[i] = pref[i - 1];
        if (s.charAt(i - 1)== s.charAt(i))
            pref[i]++;
    }
}

// Function to return the result of the query
static int query(int pref[], int l, int r)
{
    return pref[r] - pref[l];
}

// Driver Code

    public static void main (String[] args) {
    String s = "ggggggg";
    int n = s.length();

    int pref[] = new int[n];
    preCompute(n, s, pref);

    // Query 1
    int l = 1;
    int r = 2;
    System.out.println( query(pref, l, r));

    // Query 2
    l = 1;
    r = 5;
    System.out.println(query(pref, l, r));
    }
}
// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 program for the given approach

# Function to create prefix array
def preCompute(n, s, pref):

    for i in range(1,n): 
        pref[i] = pref[i - 1]
        if s[i - 1] == s[i]:
            pref[i] += 1

# Function to return the result of the query
def query(pref, l, r):

    return pref[r] - pref[l]

if __name__ == "__main__":

    s = "ggggggg"
    n = len(s)

    pref = [0] * n
    preCompute(n, s, pref)

    # Query 1
    l = 1
    r = 2
    print(query(pref, l, r))

    # Query 2
    l = 1
    r = 5
    print(query(pref, l, r))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find substring with

using System;

class GFG {

// Function to create prefix array
static void preCompute(int n, string s, int []pref)
{
    pref[0] = 0;
    for (int i = 1; i < n; i++) {
        pref[i] = pref[i - 1];
        if (s[i - 1]== s[i])
            pref[i]++;
    }
}

// Function to return the result of the query
static int query(int []pref, int l, int r)
{
    return pref[r] - pref[l];
}

// Driver Code

    public static void Main () {
    string s = "ggggggg";
    int n = s.Length;

    int []pref = new int[n];
    preCompute(n, s, pref);

    // Query 1
    int l = 1;
    int r = 2;
    Console.WriteLine( query(pref, l, r));

    // Query 2
    l = 1;
    r = 5;
    Console.WriteLine(query(pref, l, r));
    }
}
// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find substring with

// Function to create prefix array
function preCompute($n, $s, &$pref)
{
    $pref[0] = 0;
    for ($i = 1; $i < $n; $i++)
    {
        $pref[$i] = $pref[$i - 1];
        if ($s[$i - 1] == $s[$i])
            $pref[$i]++;
    }
}

// Function to return the result of the query
function query(&$pref, $l, $r)
{
    return $pref[$r] - $pref[$l];
}

// Driver Code
$s = "ggggggg";
$n = strlen($s);

$pref = array_fill(0, $n, NULL);
preCompute($n, $s, $pref);

// Query 1
$l = 1;
$r = 2;
echo query($pref, $l, $r) . "\n";

// Query 2
$l = 1;
$r = 5;
echo query($pref, $l, $r) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to find substring with

    // Function to create prefix array
    function preCompute(n,s,pref)
    {
        pref[0] = 0;
    for (let i = 1; i < n; i++) {
        pref[i] = pref[i - 1];
        if (s[i - 1]== s[i])
            pref[i]++;
    }
    }

    // Function to return the result of the query
    function query(pref,l,r)
    {
        return pref[r] - pref[l];
    }

    // Driver Code

    let s = "ggggggg";
    let n = s.length;

    let pref = new Array(n);
    preCompute(n, s, pref);

    // Query 1
    let l = 1;
    let r = 2;
    document.write( query(pref, l, r)+"<br>");

    // Query 2
    l = 1;
    r = 5;
    document.write(query(pref, l, r)+"<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
1
4
```