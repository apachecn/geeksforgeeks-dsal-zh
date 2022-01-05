# 模式搜索的优化朴素算法

> 原文:[https://www . geeksforgeeks . org/优化-朴素算法模式搜索/](https://www.geeksforgeeks.org/optimized-naive-algorithm-for-pattern-searching/)

**问题:**我们在这里讨论了朴素字符串匹配算法[。考虑模式的所有字符都不同的情况。我们能否修改](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)[原始的朴素字符串匹配算法](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)，使其更好地适用于这些类型的模式。如果可以，那么对原有算法有哪些改变？

**解决方案:**在[独创的幼稚字符串匹配算法](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)中，我们总是将模式滑动 1。当图案的所有字符都不同时，我们可以将图案滑动 1 以上。让我们看看如何才能做到这一点。当 j 个匹配后出现不匹配时，我们知道模式的第一个字符不会匹配 j 个匹配的字符，因为模式的所有字符都不同。因此，我们总是可以将模式滑动 j，而不会遗漏任何有效的移位。下面是针对特殊模式优化的修改代码。

## C++

```
/* C++ program for A modified Naive Pattern Searching
algorithm that is optimized for the cases when all
characters of pattern are different */
#include <bits/stdc++.h>
using namespace std;

/* A modified Naive Pattern Searching
algorithm that is optimized for the
cases when all characters of pattern are different */
void search(string pat, string txt)
{
    int M = pat.size();
    int N = txt.size();
    int i = 0;

    while (i <= N - M)
    {
        int j;

        /* For current index i, check for pattern match */
        for (j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;

        if (j == M) // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
        {
            cout << "Pattern found at index " << i << endl;
            i = i + M;
        }
        else if (j == 0)
            i = i + 1;
        else
            i = i + j; // slide the pattern by j
    }
}

/* Driver code*/
int main()
{
    string txt = "ABCEABCDABCEABCD";
    string pat = "ABCD";
    search(pat, txt);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
/* C program for A modified Naive Pattern Searching
  algorithm that is optimized for the cases when all
  characters of pattern are different */
#include<stdio.h>
#include<string.h>

/* A modified Naive Pattern Searching algorithm that is optimized
   for the cases when all characters of pattern are different */
void search(char pat[], char txt[])
{
    int M = strlen(pat);
    int N = strlen(txt);
    int i = 0;

    while (i <= N - M)
    {
        int j;

        /* For current index i, check for pattern match */
        for (j = 0; j < M; j++)
            if (txt[i+j] != pat[j])
                break;

        if (j == M)  // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
        {
           printf("Pattern found at index %d \n", i);
           i = i + M;
        }
        else if (j == 0)
           i = i + 1;
        else
           i = i + j; // slide the pattern by j
    }
}

/* Driver program to test above function */
int main()
{
   char txt[] = "ABCEABCDABCEABCD";
   char pat[] = "ABCD";
   search(pat, txt);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program for A modified Naive Pattern Searching
algorithm that is optimized for the cases when all
characters of pattern are different */

class GFG
{

/* A modified Naive Pattern Searching
algorithm that is optimized for the
cases when all characters of pattern are different */
static void search(String pat, String txt)
{
    int M = pat.length();
    int N = txt.length();
    int i = 0;

    while (i <= N - M)
    {
        int j;

        /* For current index i, check for pattern match */
        for (j = 0; j < M; j++)
            if (txt.charAt(i + j) != pat.charAt(j))
                break;

        if (j == M) // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
        {
            System.out.println("Pattern found at index "+i);
            i = i + M;
        }
        else if (j == 0)
            i = i + 1;
        else
            i = i + j; // slide the pattern by j
    }
}

/* Driver code*/
public static void main (String[] args)
{
    String txt = "ABCEABCDABCEABCD";
    String pat = "ABCD";
    search(pat, txt);
}
}

// This code is contributed by chandan_jnu
```

## 计算机编程语言

```
# Python program for A modified Naive Pattern Searching
# algorithm that is optimized for the cases when all
# characters of pattern are different
def search(pat, txt):
    M = len(pat)
    N = len(txt)
    i = 0

    while i <= N-M:
        # For current index i, check for pattern match
        for j in xrange(M):
            if txt[i+j] != pat[j]:
                break
            j += 1

        if j==M:    # if pat[0...M-1] = txt[i,i+1,...i+M-1]
            print "Pattern found at index " + str(i)
            i = i + M
        elif j==0:
            i = i + 1
        else:
            i = i+ j    # slide the pattern by j

# Driver program to test the above function
txt = "ABCEABCDABCEABCD"
pat = "ABCD"
search(pat, txt)

# This code is contributed by Bhavya Jain
```

## C#

```
/* C# program for A modified Naive Pattern Searching
algorithm that is optimized for the cases when all
characters of pattern are different */

using System;

class GFG
{

/* A modified Naive Pattern Searching
algorithm that is optimized for the
cases when all characters of pattern are different */
static void search(string pat, string txt)
{
    int M = pat.Length;
    int N = txt.Length;
    int i = 0;

    while (i <= N - M)
    {
        int j;

        /* For current index i, check for pattern match */
        for (j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;

        if (j == M) // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
        {
            Console.WriteLine("Pattern found at index "+i);
            i = i + M;
        }
        else if (j == 0)
            i = i + 1;
        else
            i = i + j; // slide the pattern by j
    }
}

/* Driver code*/
static void Main()
{
    string txt = "ABCEABCDABCEABCD";
    string pat = "ABCD";
    search(pat, txt);
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for A modified Naive
// Pattern Searching algorithm that
// is optimized for the cases when all
// characters of pattern are different

/* A modified Naive Pattern Searching
   algorithm that is optimized for the
   cases when all characters of
   pattern are different */
function search($pat, $txt)
{
    $M = strlen($pat);
    $N = strlen($txt);
    $i = 0;

    while ($i <= $N - $M)
    {
        $j;

        /* For current index i,
           check for pattern match */
        for ($j = 0; $j < $M; $j++)
            if ($txt[$i + $j] != $pat[$j])
                break;

        // if pat[0...M-1] =
        // txt[i, i+1, ...i+M-1]
        if ($j == $M)
        {
            echo("Pattern found at index $i"."\n" );
            $i = $i + $M;
        }
        else if ($j == 0)
            $i = $i + 1;
        else

            // slide the pattern by j
            $i = $i + $j;
    }
}

// Driver Code
$txt = "ABCEABCDABCEABCD";
$pat = "ABCD";
search($pat, $txt);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program for A modified
// Naive Pattern Searching algorithm
// that is optimized for the cases
// when all characters of pattern
// are different

// A modified Naive Pattern Searching
// algorithm that is optimized for the
// cases when all characters of pattern
// are different
function search(pat, txt)
{
    let M = pat.length;
    let N = txt.length;
    let i = 0;

    while (i <= N - M)
    {
        let j;

        // For current index i, check
        // for pattern match
        for(j = 0; j < M; j++)
            if (txt[i + j] != pat[j])
                break;

        // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M) 
        {
            document.write("Pattern found at index " +
                           i + "<br/>");
            i = i + M;
        }
        else if (j == 0)
            i = i + 1;
        else

            // Slide the pattern by j
            i = i + j;
    }
}

// Driver code
let txt = "ABCEABCDABCEABCD";
let pat = "ABCD";

search(pat, txt);

// This code is contributed by target_2

</script>
```

**输出:**

```
Pattern found at index 4
Pattern found at index 12
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。