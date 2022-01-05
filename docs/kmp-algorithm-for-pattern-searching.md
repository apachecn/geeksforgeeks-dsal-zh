# 模式搜索的 KMP 算法

> 原文:[https://www . geesforgeks . org/KMP-模式搜索算法/](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)

给定一个文本*txt【0..n-1]* 和模式*帕特【0..m-1]* ，编写一个函数*搜索(char pat[]，char txt[])* ，打印 *txt[]* 中所有出现的 *pat[]* 。你可以假设 *n > m* 。

**示例:**

```
Input:  txt[] = "THIS IS A TEST TEXT"
        pat[] = "TEST"
Output: Pattern found at index 10

Input:  txt[] =  "AABAACAADAABAABA"
        pat[] =  "AABA"
Output: Pattern found at index 0
        Pattern found at index 9
        Pattern found at index 12

```

模式搜索是计算机科学中的一个重要问题。当我们在记事本/word 文件或浏览器或数据库中搜索字符串时，会使用模式搜索算法来显示搜索结果。

我们在[之前的帖子](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)中已经讨论过朴素模式搜索算法。朴素算法的最坏情况复杂度是 O(m(n-m+1))。在最坏的情况下，KMP 算法的时间复杂度为 O(n)。

**KMP (Knuth Morris Pratt)模式搜索**
[天真模式搜索算法](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)在我们看到许多匹配字符后面跟有一个不匹配字符的情况下效果不佳。以下是一些例子。

```
   txt[] = "AAAAAAAAAAAAAAAAAB"
   pat[] = "AAAAB"

   txt[] = "ABABABCABABABCABABABC"
   pat[] =  "ABABAC" (not a worst case, but a bad case for Naive)

```

KMP 匹配算法利用模式的退化特性(模式中相同的子模式出现不止一次)，并将最坏情况的复杂度提高到 0(n)。KMP 算法背后的基本思想是:每当我们检测到不匹配时(在一些匹配之后)，我们已经知道下一个窗口文本中的一些字符。我们利用这些信息来避免匹配我们知道无论如何都会匹配的字符。让我们考虑下面的例子来理解这一点。

```
Matching Overview
txt = "AAAAABAAABA" 
pat = "AAAA"

We compare first window of txt with pat
txt = "AAAAABAAABA" 
pat = "AAAA"  [Initial position]
We find a match. This is same as Naive String Matching.

In the next step, we compare next window of txt with pat.
txt = "AAAA<font color="Red">A</font>BAAABA" 
pat =  "AAA<font color="Red">A</font>" [Pattern shifted one position]
This is where KMP does optimization over Naive. In this 
second window, we only compare fourth A of pattern
with fourth character of current window of text to decide 
whether current window matches or not. Since we know 
first three characters will anyway match, we skipped 
matching first three characters. 

Need of Preprocessing?
An important question arises from the above explanation, 
how to know how many characters to be skipped. To know this, 
we pre-process pattern and prepare an integer array 
lps[] that tells us the count of characters to be skipped. 

```

**预处理概述:**

*   KMP 算法对 pat[]进行预处理，构造一个 m 大小(与模式大小相同)的辅助 **lps[]** ，用于匹配时跳过字符。
*   **名称 **lps** 表示最长的专有前缀，也是后缀。**。一个合适的前缀是整个字符串的前缀**不允许**。例如，“ABC”的前缀是“”、“A”、“AB”和“ABC”。合适的前缀是""、" A "和" AB "。字符串的后缀是""、" C "、" BC "和" ABC "。
*   我们在子模式中搜索 lps。更明确地说，我们关注的是前缀和后缀模式的子串。
*   For each sub-pattern pat[0..i] where i = 0 to m-1, lps[i] stores length of the maximum matching proper prefix which is also a suffix of the sub-pattern pat[0..i].

    ```
       lps[i] = the longest proper prefix of pat[0..i] 
                  which is also a suffix of pat[0..i]. 
    ```

    **注:** lps[i]也可以定义为最长前缀，也是合适的后缀。我们需要在一个地方正确使用，以确保不考虑整个子串。

    ```
    Examples of lps[] construction:
    For the pattern “AAAA”, 
    lps[] is [0, 1, 2, 3]

    For the pattern “ABCDE”, 
    lps[] is [0, 0, 0, 0, 0]

    For the pattern “AABAACAABAA”, 
    lps[] is [0, 1, 0, 1, 2, 0, 1, 2, 3, 4, 5]

    For the pattern “AAACAAAAAC”, 
    lps[] is [0, 1, 2, 0, 1, 2, 3, 3, 3, 4] 

    For the pattern “AAABAAA”, 
    lps[] is [0, 1, 2, 0, 1, 2, 3]

    ```

    **搜索算法:**
    与[朴素算法](https://www.geeksforgeeks.org/searching-for-patterns-set-1-naive-pattern-searching/)不同，在后者中，我们将模式一个一个地滑动，并在每次移动时比较所有字符，我们使用来自 lps[]的值来决定下一个要匹配的字符。这个想法是不匹配一个我们知道无论如何都会匹配的角色。

    如何使用 lps[]决定下一个位置(或者知道要跳过的字符数)？

    *   我们开始将 j = 0 的 pat[j]与当前文本窗口的字符进行比较。
    *   我们保持匹配字符 txt[i]和 pat[j]并保持递增 I 和 j，同时 pat[j]和 txt[i]保持**匹配**。
    *   当我们看到**不匹配**
        *   我们知道字符 pat[0..j-1]与 txt[i-j…i-1]匹配(注意 j 从 0 开始，只有匹配时才递增)。
        *   我们还知道(从上面的定义)lps[j-1]是 pat[0…j-1]的字符数，这些字符既是正确的前缀又是后缀。
        *   从以上两点，我们可以得出结论，我们不需要将这些 lps[j-1]字符与 txt[i-j…i-1]匹配，因为我们知道这些字符无论如何都会匹配。让我们考虑上面的例子来理解这一点。

    ```
    txt[] = "AAAAABAAABA" 
    pat[] = "AAAA"
    lps[] = {0, 1, 2, 3} 

    i = 0, j = 0
    txt[] = "<font color="Red">A</font>AAAABAAABA" 
    pat[] = "<font color="Red">A</font>AAA"
    txt[i] and pat[j] match, do i++, j++

    i = 1, j = 1
    txt[] = "A<font color="Red">A</font>AAABAAABA" 
    pat[] = "A<font color="Red">A</font>AA"
    txt[i] and pat[j] match, do i++, j++

    i = 2, j = 2
    txt[] = "AA<font color="Red">A</font>AABAAABA" 
    pat[] = "AA<font color="Red">A</font>A"
    pat[i] and pat[j] match, do i++, j++

    i = 3, j = 3
    txt[] = "AAA<font color="Red">A</font>ABAAABA" 
    pat[] = "AAA<font color="Red">A</font>"
    txt[i] and pat[j] match, do i++, j++

    i = 4, j = 4
    Since j == M, print pattern found and reset j,
    j = lps[j-1] = lps[3] = 3

    Here unlike Naive algorithm, we do not match first three 
    characters of this window. Value of lps[j-1] (in above 
    step) gave us index of next character to match.
    i = 4, j = 3
    txt[] = "AAAA<font color="Red">A</font>BAAABA" 
    pat[] =  "AAA<font color="Red">A</font>"
    txt[i] and pat[j] match, do i++, j++

    i = 5, j = 4
    Since j == M, print pattern found and reset j,
    j = lps[j-1] = lps[3] = 3

    Again unlike Naive algorithm, we do not match first three 
    characters of this window. Value of lps[j-1] (in above 
    step) gave us index of next character to match.
    i = 5, j = 3
    txt[] = "AAAAA<font color="Red">B</font>AAABA" 
    pat[] =   "AAA<font color="Red">A</font>"
    txt[i] and pat[j] do NOT match and j > 0, change only j
    j = lps[j-1] = lps[2] = 2

    i = 5, j = 2
    txt[] = "AAAAA<font color="Red">B</font>AAABA" 
    pat[] =    "AA<font color="Red">A</font>A"
    txt[i] and pat[j] do NOT match and j > 0, change only j
    j = lps[j-1] = lps[1] = 1 

    i = 5, j = 1
    txt[] = "AAAAA<font color="Red">B</font>AAABA" 
    pat[] =     "A<font color="Red">A</font>AA"
    txt[i] and pat[j] do NOT match and j > 0, change only j
    j = lps[j-1] = lps[0] = 0

    i = 5, j = 0
    txt[] = "AAAAA<font color="Red">B</font>AAABA" 
    pat[] =      "<font color="Red">A</font>AAA"
    txt[i] and pat[j] do NOT match and j is 0, we do i++.

    i = 6, j = 0
    txt[] = "AAAAAB<font color="Red">A</font>AABA" 
    pat[] =       "<font color="Red">A</font>AAA"
    txt[i] and pat[j] match, do i++ and j++

    i = 7, j = 1
    txt[] = "AAAAABA<font color="Red">A</font>ABA" 
    pat[] =       "A<font color="Red">A</font>AA"
    txt[i] and pat[j] match, do i++ and j++

    We continue this way...

    ```

    ## C++

    ```
    // C++ program for implementation of KMP pattern searching
    // algorithm
    #include <bits/stdc++.h>

    void computeLPSArray(char* pat, int M, int* lps);

    // Prints occurrences of txt[] in pat[]
    void KMPSearch(char* pat, char* txt)
    {
        int M = strlen(pat);
        int N = strlen(txt);

        // create lps[] that will hold the longest prefix suffix
        // values for pattern
        int lps[M];

        // Preprocess the pattern (calculate lps[] array)
        computeLPSArray(pat, M, lps);

        int i = 0; // index for txt[]
        int j = 0; // index for pat[]
        while (i < N) {
            if (pat[j] == txt[i]) {
                j++;
                i++;
            }

            if (j == M) {
                printf("Found pattern at index %d ", i - j);
                j = lps[j - 1];
            }

            // mismatch after j matches
            else if (i < N && pat[j] != txt[i]) {
                // Do not match lps[0..lps[j-1]] characters,
                // they will match anyway
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }
    }

    // Fills lps[] for given patttern pat[0..M-1]
    void computeLPSArray(char* pat, int M, int* lps)
    {
        // length of the previous longest prefix suffix
        int len = 0;

        lps[0] = 0; // lps[0] is always 0

        // the loop calculates lps[i] for i = 1 to M-1
        int i = 1;
        while (i < M) {
            if (pat[i] == pat[len]) {
                len++;
                lps[i] = len;
                i++;
            }
            else // (pat[i] != pat[len])
            {
                // This is tricky. Consider the example.
                // AAACAAAA and i = 7\. The idea is similar
                // to search step.
                if (len != 0) {
                    len = lps[len - 1];

                    // Also, note that we do not increment
                    // i here
                }
                else // if (len == 0)
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }

    // Driver program to test above function
    int main()
    {
        char txt[] = "ABABDABACDABABCABAB";
        char pat[] = "ABABCABAB";
        KMPSearch(pat, txt);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // JAVA program for implementation of KMP pattern
    // searching algorithm

    class KMP_String_Matching {
        void KMPSearch(String pat, String txt)
        {
            int M = pat.length();
            int N = txt.length();

            // create lps[] that will hold the longest
            // prefix suffix values for pattern
            int lps[] = new int[M];
            int j = 0; // index for pat[]

            // Preprocess the pattern (calculate lps[]
            // array)
            computeLPSArray(pat, M, lps);

            int i = 0; // index for txt[]
            while (i < N) {
                if (pat.charAt(j) == txt.charAt(i)) {
                    j++;
                    i++;
                }
                if (j == M) {
                    System.out.println("Found pattern "
                                       + "at index " + (i - j));
                    j = lps[j - 1];
                }

                // mismatch after j matches
                else if (i < N && pat.charAt(j) != txt.charAt(i)) {
                    // Do not match lps[0..lps[j-1]] characters,
                    // they will match anyway
                    if (j != 0)
                        j = lps[j - 1];
                    else
                        i = i + 1;
                }
            }
        }

        void computeLPSArray(String pat, int M, int lps[])
        {
            // length of the previous longest prefix suffix
            int len = 0;
            int i = 1;
            lps[0] = 0; // lps[0] is always 0

            // the loop calculates lps[i] for i = 1 to M-1
            while (i < M) {
                if (pat.charAt(i) == pat.charAt(len)) {
                    len++;
                    lps[i] = len;
                    i++;
                }
                else // (pat[i] != pat[len])
                {
                    // This is tricky. Consider the example.
                    // AAACAAAA and i = 7\. The idea is similar
                    // to search step.
                    if (len != 0) {
                        len = lps[len - 1];

                        // Also, note that we do not increment
                        // i here
                    }
                    else // if (len == 0)
                    {
                        lps[i] = len;
                        i++;
                    }
                }
            }
        }

        // Driver program to test above function
        public static void main(String args[])
        {
            String txt = "ABABDABACDABABCABAB";
            String pat = "ABABCABAB";
            new KMP_String_Matching().KMPSearch(pat, txt);
        }
    }
    // This code has been contributed by Amit Khandelwal.
    ```

    ## 计算机编程语言

    ```
    # Python program for KMP Algorithm
    def KMPSearch(pat, txt):
        M = len(pat)
        N = len(txt)

        # create lps[] that will hold the longest prefix suffix 
        # values for pattern
        lps = [0]*M
        j = 0 # index for pat[]

        # Preprocess the pattern (calculate lps[] array)
        computeLPSArray(pat, M, lps)

        i = 0 # index for txt[]
        while i < N:
            if pat[j] == txt[i]:
                i += 1
                j += 1

            if j == M:
                print ("Found pattern at index " + str(i-j))
                j = lps[j-1]

            # mismatch after j matches
            elif i < N and pat[j] != txt[i]:
                # Do not match lps[0..lps[j-1]] characters,
                # they will match anyway
                if j != 0:
                    j = lps[j-1]
                else:
                    i += 1

    def computeLPSArray(pat, M, lps):
        len = 0 # length of the previous longest prefix suffix

        lps[0] # lps[0] is always 0
        i = 1

        # the loop calculates lps[i] for i = 1 to M-1
        while i < M:
            if pat[i]== pat[len]:
                len += 1
                lps[i] = len
                i += 1
            else:
                # This is tricky. Consider the example.
                # AAACAAAA and i = 7\. The idea is similar 
                # to search step.
                if len != 0:
                    len = lps[len-1]

                    # Also, note that we do not increment i here
                else:
                    lps[i] = 0
                    i += 1

    txt = "ABABDABACDABABCABAB"
    pat = "ABABCABAB"
    KMPSearch(pat, txt)

    # This code is contributed by Bhavya Jain
    ```

    ## C#

    ```
    // C# program for implementation of KMP pattern
    // searching algorithm
    using System;

    class GFG {

        void KMPSearch(string pat, string txt)
        {
            int M = pat.Length;
            int N = txt.Length;

            // create lps[] that will hold the longest
            // prefix suffix values for pattern
            int[] lps = new int[M];
            int j = 0; // index for pat[]

            // Preprocess the pattern (calculate lps[]
            // array)
            computeLPSArray(pat, M, lps);

            int i = 0; // index for txt[]
            while (i < N) {
                if (pat[j] == txt[i]) {
                    j++;
                    i++;
                }
                if (j == M) {
                    Console.Write("Found pattern "
                                  + "at index " + (i - j));
                    j = lps[j - 1];
                }

                // mismatch after j matches
                else if (i < N && pat[j] != txt[i]) {
                    // Do not match lps[0..lps[j-1]] characters,
                    // they will match anyway
                    if (j != 0)
                        j = lps[j - 1];
                    else
                        i = i + 1;
                }
            }
        }

        void computeLPSArray(string pat, int M, int[] lps)
        {
            // length of the previous longest prefix suffix
            int len = 0;
            int i = 1;
            lps[0] = 0; // lps[0] is always 0

            // the loop calculates lps[i] for i = 1 to M-1
            while (i < M) {
                if (pat[i] == pat[len]) {
                    len++;
                    lps[i] = len;
                    i++;
                }
                else // (pat[i] != pat[len])
                {
                    // This is tricky. Consider the example.
                    // AAACAAAA and i = 7\. The idea is similar
                    // to search step.
                    if (len != 0) {
                        len = lps[len - 1];

                        // Also, note that we do not increment
                        // i here
                    }
                    else // if (len == 0)
                    {
                        lps[i] = len;
                        i++;
                    }
                }
            }
        }

        // Driver program to test above function
        public static void Main()
        {
            string txt = "ABABDABACDABABCABAB";
            string pat = "ABABCABAB";
            new GFG().KMPSearch(pat, txt);
        }
    }

    // This code has been contributed by Amit Khandelwal.
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // PHP program for implementation of KMP pattern searching
    // algorithm

    // Prints occurrences of txt[] in pat[]
    function KMPSearch($pat, $txt)
    {
        $M = strlen($pat);
        $N = strlen($txt);

        // create lps[] that will hold the longest prefix suffix
        // values for pattern
        $lps=array_fill(0,$M,0);

        // Preprocess the pattern (calculate lps[] array)
        computeLPSArray($pat, $M, $lps);

        $i = 0; // index for txt[]
        $j = 0; // index for pat[]
        while ($i < $N) {
            if ($pat[$j] == $txt[$i]) {
                $j++;
                $i++;
            }

            if ($j == $M) {
                printf("Found pattern at index ".($i - $j));
                $j = $lps[$j - 1];
            }

            // mismatch after j matches
            else if ($i < $N && $pat[$j] != $txt[$i]) {
                // Do not match lps[0..lps[j-1]] characters,
                // they will match anyway
                if ($j != 0)
                    $j = $lps[$j - 1];
                else
                    $i = $i + 1;
            }
        }
    }

    // Fills lps[] for given patttern pat[0..M-1]
    function computeLPSArray($pat, $M, &$lps)
    {
        // length of the previous longest prefix suffix
        $len = 0;

        $lps[0] = 0; // lps[0] is always 0

        // the loop calculates lps[i] for i = 1 to M-1
        $i = 1;
        while ($i < $M) {
            if ($pat[$i] == $pat[$len]) {
                $len++;
                $lps[$i] = $len;
                $i++;
            }
            else // (pat[i] != pat[len])
            {
                // This is tricky. Consider the example.
                // AAACAAAA and i = 7\. The idea is similar
                // to search step.
                if ($len != 0) {
                    $len = $lps[$len - 1];

                    // Also, note that we do not increment
                    // i here
                }
                else // if (len == 0)
                {
                    $lps[$i] = 0;
                    $i++;
                }
            }
        }
    }

    // Driver program to test above function

        $txt = "ABABDABACDABABCABAB";
        $pat = "ABABCABAB";
        KMPSearch($pat, $txt);

    // This code is contributed by chandan_jnu
    ?>
    ```

    **Output:**

    ```
    Found pattern at index 10
    ```

    **预处理算法:**
    在预处理部分，我们计算 lps[]中的值。为此，我们跟踪前一个索引的最长前缀后缀值的长度(为此，我们使用 len 变量)。我们将 lps[0]和 len 初始化为 0。如果 pat[len]和 pat[i]匹配，我们将 len 增加 1，并将增加的值分配给 lps[i]。如果 pat[i]和 pat[len]不匹配，并且 len 不是 0，我们将 len 更新为 lps[len-1]。有关详细信息，请参见下面代码中的 computeLPSArray()。

    **预处理说明(或 lps 的构建[])**

    ```
    pat[] = "AAACAAAA"

    len = 0, i  = 0.
    lps[0] is always 0, we move 
    to i = 1

    len = 0, i  = 1.
    Since pat[len] and pat[i] match, do len++, 
    store it in lps[i] and do i++.
    len = 1, lps[1] = 1, i = 2

    len = 1, i  = 2.
    Since pat[len] and pat[i] match, do len++, 
    store it in lps[i] and do i++.
    len = 2, lps[2] = 2, i = 3

    len = 2, i  = 3.
    Since pat[len] and pat[i] do not match, and len > 0, 
    set len = lps[len-1] = lps[1] = 1

    len = 1, i  = 3.
    Since pat[len] and pat[i] do not match and len > 0, 
    len = lps[len-1] = lps[0] = 0

    len = 0, i  = 3.
    Since pat[len] and pat[i] do not match and len = 0, 
    Set lps[3] = 0 and i = 4.
    We know that characters pat
    len = 0, i  = 4.
    Since pat[len] and pat[i] match, do len++, 
    store it in lps[i] and do i++.
    len = 1, lps[4] = 1, i = 5

    len = 1, i  = 5.
    Since pat[len] and pat[i] match, do len++, 
    store it in lps[i] and do i++.
    len = 2, lps[5] = 2, i = 6

    len = 2, i  = 6.
    Since pat[len] and pat[i] match, do len++, 
    store it in lps[i] and do i++.
    len = 3, lps[6] = 3, i = 7

    len = 3, i  = 7.
    Since pat[len] and pat[i] do not match and len > 0,
    set len = lps[len-1] = lps[2] = 2

    len = 2, i  = 7.
    Since pat[len] and pat[i] match, do len++, 
    store it in lps[i] and do i++.
    len = 3, lps[7] = 3, i = 8

    We stop here as we have constructed the whole lps[].

    ```

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。