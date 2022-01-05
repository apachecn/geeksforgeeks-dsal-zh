# 字符串中子串的频率

> 原文:[https://www.geeksforgeeks.org/frequency-substring-string/](https://www.geeksforgeeks.org/frequency-substring-string/)

给定输入字符串和子字符串。查找给定字符串中子字符串出现的频率。

**例:**

```
Input : man (pattern)
        dhimanman (string)
Output : 2

Input : nn (pattern)
        Banana (String)
Output : 0

Input : man (pattern)
        dhimanman (string)
Output : 2

Input : aa (pattern)
        aaaaa (String)
Output : 4
```

一个**简单的解决方法**就是一个一个的匹配字符。每当我们看到完全匹配时，我们就增加计数。以下是基于[朴素模式搜索](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)的简单解决方案。

## c++

```
// Simple C++ program to count occurrences
// of pat in txt.
#include<bits/stdc++.h>
using namespace std;

int countFreq(string &pat, string &txt)
{
    int M = pat.length();
    int N = txt.length();
    int res = 0;

    /* A loop to slide pat[] one by one */
    for (int i = 0; i <= N - M; i++)
    {
        /* For current index i, check for
           pattern match */
        int j;
        for (j = 0; j < M; j++)
            if (txt[i+j] != pat[j])
                break;

        // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M) 
        {
           res++;
        }
    }
    return res;
}

/* Driver program to test above function */
int main()
{
   string txt = "dhimanman";
   string pat = "man";
   cout << countFreq(pat, txt);
   return 0;
}
```

## Java

```
// Simple Java program to count occurrences
// of pat in txt.

class GFG {

    static int countFreq(String pat, String txt) {       
        int M = pat.length();       
        int N = txt.length();       
        int res = 0;

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++) {
            /* For current index i, check for
        pattern match */
            int j;           
            for (j = 0; j < M; j++) {
                if (txt.charAt(i + j) != pat.charAt(j)) {
                    break;
                }
            }

            // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
            if (j == M) {               
                res++;               
                j = 0;               
            }           
        }       
        return res;       
    }

    /* Driver program to test above function */
    static public void main(String[] args) {
        String txt = "dhimanman";       
        String pat = "man";       
        System.out.println(countFreq(pat, txt));       
    }
}

// This code is contributed by 29AjayKumar
```

## python 3

```
# Simple python program to count
# occurrences of pat in txt.
def countFreq(pat, txt):
    M = len(pat)
    N = len(txt)
    res = 0

    # A loop to slide pat[] one by one
    for i in range(N - M + 1):

        # For current index i, check
        # for pattern match
        j = 0
        while j < M:
            if (txt[i + j] != pat[j]):
                break
            j += 1

        if (j == M):
            res += 1
            j = 0
    return res

# Driver Code
if __name__ == '__main__':
    txt = "dhimanman"
    pat = "man"
    print(countFreq(pat, txt))

# This code is contributed
# by PrinciRaj1992
```

## c#

```

// Simple C# program to count occurrences
// of pat in txt.
using System;
public class GFG {

    static int countFreq(String pat, String txt) {       
        int M = pat.Length;       
        int N = txt.Length;       
        int res = 0;

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++) {
            /* For current index i, check for
        pattern match */
            int j;           
            for (j = 0; j < M; j++) {
                if (txt[i + j] != pat[j]) {
                    break;
                }
            }

            // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
            if (j == M) {               
                res++;               
                j = 0;               
            }           
        }       
        return res;       
    }

    /* Driver program to test above function */
    static public void Main() {
        String txt = "dhimanman";       
        String pat = "man";       
        Console.Write(countFreq(pat, txt));       
    }
}

// This code is contributed by 29AjayKumar
```

## PHP

```
<?php
// Simple PHP program to count occurrences
// of pat in txt.

function countFreq($pat, $txt)
{
    $M = strlen($pat);
    $N = strlen($txt);
    $res = 0;

    /* A loop to slide pat[] one by one */
    for ($i = 0; $i <= $N - $M; $i++)
    {
        /* For current index i, check for
        pattern match */
        for ($j = 0; $j < $M; $j++)
            if ($txt[$i+$j] != $pat[$j])
                break;

        // if pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if ($j == $M)
        {
            $res++;
            $j = 0;
        }
    }
    return $res;
}

// Driver Code
$txt = "dhimanman";
$pat = "man";
echo countFreq($pat, $txt);

// This code is contributed
// by Akanksha Rai
```

## Javascript

```
<script>

// JavaScript program to count occurrences
// of pat in txt.
let mod = 100000007;

function countFreq(pat, txt)
{      
    let M = pat.length;      
    let N = txt.length;      
    let res = 0;

    // A loop to slide pat[] one by one
    for(let i = 0; i <= N - M; i++)
    {

        // For current index i, check for
        // pattern match
        let j;          
        for(j = 0; j < M; j++)
        {
            if (txt[i + j] != pat[j])
            {
                break;
            }
        }

        // If pat[0...M-1] = txt[i, i+1, ...i+M-1]
        if (j == M)
        {              
            res++;              
            j = 0;              
        }          
    }      
    return res;      
}

// Driver Code
let txt = "dhimanman";      
let pat = "man"; 

document.write(countFreq(pat, txt));

// This code is contributed by code_hunt

</script>
```

**输出**

```
2
```