# 找到用数字 X 和 Y 组成的第 n 个偶数长度回文号

> 原文:[https://www . geesforgeks . org/find-n-偶数-长度-回文-数字-格式-使用数字-x-and-y/](https://www.geeksforgeeks.org/find-nth-even-length-palindromic-number-formed-using-digits-x-and-y/)

给定一个整数 **N** ，任务是找到偶数长度的 **N <sup>第</sup>T5】个偶数回文号，并且只包含数字 **X** 和 **Y** ，其中 **X，Y > 0** 。
**示例:**** 

> **输入:** N = 9，X = 4，Y = 5
> **输出:** 454454
> **解释:**
> 使用 4 & 5 的偶数长度回文数字为
> 44、55、4444、4554、5445、5555、44444、445544、454454、…
> 上述系列的第 9 项= 445 Y = 2
> **输出:** 2222
> **解释:**
> 使用 1 & 2 的偶数长度回文数字是
> 11、22、1111、1221、2112、2222、111111、112211、121121、……
> 上述系列的第 6 项= 2222

**进场:**

*   使用 X & Y 的偶数长度回文数字为

```
XX, YY, XXXX, XYYX, YXXY, YYYY, XXXXXX, XXYYXX, ...
```

*   上述顺序可以观察为:

```
XX,       -> Length (L) = 2
YY,       -> Length (L) = 2

XXXX,     -> Length (L) = 4
XYYX,     -> Length (L) = 4
YXXY,     -> Length (L) = 4
YYYY,     -> Length (L) = 4

XXXXXX,   -> Length (L) = 6
XXYYXX,   -> Length (L) = 6
XYXXYX,   -> Length (L) = 6
XYYYYX,   -> Length (L) = 6
YXXXXY,   -> Length (L) = 6
YXYYXY,   -> Length (L) = 6
YYXXYY,   -> Length (L) = 6
YYYYYY,   -> Length (L) = 6

XXXXXXXX, -> Length (L) = 8
...
```

*   如果我们把任何一个术语分成两半，后半部分正好是前半部分的反义词
    **例:**

```
Taking the term XXYYXX

Dividing this into 2 halves
XXYYXX = XXY | YXX

So YXX is just the reverse of XXY
```

*   只取术语的左半部分**，放入 **X = 0，Y = 1** 得到二进制字符串，长度 L 的数字可以看到形成一个从 0 到(2<sup>L/2</sup>–1)的整数序列，取为**秩(R)** 。因此**0&leq；r&leq；2<sup>L/2</sup>–1**
    因此顺序可观察如下:** 

```
L -> Left Half -> Binary String -> Rank (in Decimal) 

2 -> X    -> 0             -> 0
2 -> Y    -> 1             -> 1

4 -> XX   -> 00            -> 0
4 -> XY   -> 01            -> 1
4 -> YX   -> 10            -> 2
4 -> YY   -> 11            -> 3

6 -> XXX  -> 000           -> 0
6 -> XXY  -> 001           -> 1
6 -> XYX  -> 010           -> 2
6 -> XYY  -> 011           -> 3
6 -> YXX  -> 100           -> 4
6 -> YXY  -> 101           -> 5
6 -> YYX  -> 110           -> 6
6 -> YYY  -> 111           -> 7

8 -> XXXX -> 0000          -> 0
...
```

*   Therefore, For the required term N: 
    *   所需第 n 个术语的**长度(L)**:

        ![L=2(\left\lceil log_{2}(N + 2)\right\rceil-1)](img/c444044da2d0d85100a7bc3ec150bfb4.png "Rendered by QuickLaTeX.com")
    *   **所需第 n 个术语的等级(R)**:

        ![R = N - 2^{(\frac{L}{2})} + 1](img/28acc7efa22551952e4de79cc5525398.png "Rendered by QuickLaTeX.com")
    *   **所需第 n 项的前半部分**= R 在 L/2 位的二进制表示，将 0 替换为 X，将 1 替换为 Y
    *   **所需第 n 项的后半部分**=前半部分的反向

    以下是上述方法的实现:

    ## C++

    ```
    // C++ program to find nth even
    // palindromic number of only even
    // length composing of 4's and 5's.

    #include <bits/stdc++.h>
    using namespace std;

    // Utility function to compute
    // n'th palindrome number
    string solve(int n, char x, char y)
    {
        // Calculate the length from above
        // formula as discussed above
        int length = ceil(log2(n + 2)) - 1;

        // Calculate rank for length L
        int rank = n - (1 << length) + 1;

        string left = "", right = "";

        for (int i = length - 1; i >= 0; i--) {

            // Mask to check if i't bit
            // is set or not
            int mask = 1 << i;

            // If bit is set append '5' else append '4'
            bool bit = mask & rank;

            if (bit) {
                left += y;
                right += y;
            }
            else {
                left += x;
                right += x;
            }
        }

        reverse(right.begin(), right.end());

        return left + right;
    }

    // Driver Code
    int main()
    {
        int n = 23;
        char x = '4', y = '5';
        string ans = solve(n, x, y);
        cout << ans << '\n';

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to find nth even 
    // palindromic number of only even 
    // length composing of 4's and 5's. 
    import java.util.*;

    class GFG
    {

        // Utility function to compute 
        // n'th palindrome number 
        static String solve(int n, char x, char y) 
        { 
            // Calculate the length from above 
            // formula as discussed above 
            int length = (int)Math.ceil(Math.log(n + 2) / 
                                        Math.log(2)) - 1; 

            // Calculate rank for length L 
            int rank = n - (1 << length) + 1; 

            String left = "", right = ""; 

            for (int i = length -1 ; i >= 0; i--)
            { 

                // Mask to check if i't bit 
                // is set or not 
                int mask = (1 << i); 

                // If bit is set append '5' else append '4' 
                int bit = mask & rank; 

                if (bit > 0)
                { 
                    left += y; 
                    right += y; 
                } 
                else 
                { 
                    left += x; 
                    right += x; 
                } 
            } 

            StringBuilder sb = new StringBuilder(right); 
            sb.reverse(); 

            right = sb.toString(); 

            String res = left + right;
            return res; 
        } 

        // Driver Code 
        public static void main (String[] args)
        { 
            int n = 23; 
            char x = '4', y = '5'; 
            String ans = solve(n, x, y); 
            System.out.println(ans); 
        } 
    }

    // This code is contributed by AnkitRai01
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to find nth even 
    # palindromic number of only even 
    # length composing of 4's and 5's. 
    from math import ceil, log2

    # Utility function to compute 
    # n'th palindrome number 
    def solve(n, x, y) : 

        # Calculate the length from above 
        # formula as discussed above 
        length = ceil(log2(n + 2)) - 1; 

        # Calculate rank for length L 
        rank = n - (1 << length) + 1; 

        left = ""; right = ""; 

        for i in range(length - 1 , -1, -1):

            # Mask to check if i't bit 
            # is set or not 
            mask = (1 << i); 

            # If bit is set append '5' 
            # else append '4' 
            bit = (mask & rank); 

            if (bit) :
                left += y; 
                right += y; 

            else :
                left += x; 
                right += x; 

        right = right[::-1];

        res = left + right;
        return res;

    # Driver Code 
    if __name__ == "__main__" : 

        n = 23; 
        x = '4';
        y = '5'; 
        ans = solve(n, x, y); 
        print(ans); 

    # This code is contributed by kanugargng
    ```

    ## C#

    ```
    // C# program to find nth even 
    // palindromic number of only even 
    // length composing of 4's and 5's. 
    using System;

    class GFG
    {

        // Utility function to compute 
        // n'th palindrome number 
        static String solve(int n, char x, char y) 
        { 
            // Calculate the length from above 
            // formula as discussed above 
            int length = (int)Math.Ceiling(Math.Log(n + 2) / 
                                           Math.Log(2)) - 1; 

            // Calculate rank for length L 
            int rank = n - (1 << length) + 1; 

            String left = "", right = ""; 

            for (int i = length -1; i >= 0; i--)
            { 

                // Mask to check if i't bit 
                // is set or not 
                int mask = (1 << i); 

                // If bit is set append '5'
                // else append '4' 
                int bit = mask & rank; 

                if (bit > 0)
                { 
                    left += y; 
                    right += y; 
                } 
                else
                { 
                    left += x; 
                    right += x; 
                } 
            } 

            right = reverse(right);
            String res = left + right;
            return res; 
        } 

        static String reverse(String input) 
        {
            char[] a = input.ToCharArray();
            int l, r = 0;
            r = a.Length - 1;

            for (l = 0; l < r; l++, r--) 
            {
                // Swap values of l and r 
                char temp = a[l];
                a[l] = a[r];
                a[r] = temp;
            }
            return String.Join("", a);
        } 

        // Driver Code 
        public static void Main (String[] args)
        { 
            int n = 23; 
            char x = '4', y = '5'; 
            String ans = solve(n, x, y); 
            Console.WriteLine(ans); 
        } 
    }

    // This code is contributed by Rajput-Ji
    ```

    ## java 描述语言

    ```
    <script>

    // Javascript program to find nth even
    // palindromic number of only even
    // length composing of 4's and 5's.

    // Utility function to compute
    // n'th palindrome number
    function solve(n, x, y)
    {
        // Calculate the length from above
        // formula as discussed above
        var length = Math.ceil(Math.log2(n + 2)) - 1;

        // Calculate rank for length L
        var rank = n - (1 << length) + 1;

        var left = "", right = "";

        for (var i = length - 1; i >= 0; i--) {

            // Mask to check if i't bit
            // is set or not
            var mask = 1 << i;

            // If bit is set append '5' else append '4'
            var bit = mask & rank;

            if (bit) {
                left += y;
                right += y;
            }
            else {
                left += x;
                right += x;
            }
        }

        right = right.split('').reverse().join('');

        return left + right;
    }

    // Driver Code
    var n = 23;
    var x = '4', y = '5';
    var ans = solve(n, x, y);
    document.write( ans + "<br>");

    </script>
    ```

    **Output**

    ```
    54444445

    ```

    **时间复杂度:** ![ O(n) ](img/bcaca7cc76a89e9dc237e94fd4374242.png "Rendered by QuickLaTeX.com")其中 n 是字符串的长度