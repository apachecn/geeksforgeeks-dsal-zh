# 将字符串转换为二进制序列

> 原文:[https://www . geesforgeks . org/convert-string-binary-sequence/](https://www.geeksforgeeks.org/convert-string-binary-sequence/)

给定一个字符串，任务是将字符串的每个字符转换成等价的二进制数。
**例:**

```

Input : GFG
Output : 1000111 1000110 1000111  

Input :  geeks
Output : 1100111 1100101 1100101 1101011 1110011  
```

其思想是首先将字符串的长度计算为 n，然后循环 n 次。在每次迭代中，将字符的 ASCII 值存储在变量 val 中，然后将其转换为二进制数，并将结果存储在数组中，最后以相反的顺序打印数组。

## C++

```
// C++ program to convert
// string into binary string
#include <bits/stdc++.h>
using namespace std;

// utility function
void strToBinary(string s)
{
    int n = s.length();

    for (int i = 0; i <= n; i++)
    {
        // convert each char to
        // ASCII value
        int val = int(s[i]);

        // Convert ASCII value to binary
        string bin = "";
        while (val > 0)
        {
            (val % 2)? bin.push_back('1') :
                       bin.push_back('0');
            val /= 2;
        }
        reverse(bin.begin(), bin.end());

        cout << bin << " ";
    }
}

// driver code
int main()
{

    string s = "geeks";
    strToBinary(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert
// string into binary string
import java.util.*;

class Node
{

    // utility function
    static void strToBinary(String s)
    {
        int n = s.length();

        for (int i = 0; i < n; i++)
        {
            // convert each char to
            // ASCII value
            int val = Integer.valueOf(s.charAt(i));

            // Convert ASCII value to binary
            String bin = "";
            while (val > 0)
            {
                if (val % 2 == 1)
                {
                    bin += '1';
                }
                else
                    bin += '0';
                val /= 2;
            }
            bin = reverse(bin);

            System.out.print(bin + " ");
        }
    }

    static String reverse(String input)
    {
        char[] a = input.toCharArray();
        int l, r = 0;
        r = a.length - 1;

        for (l = 0; l < r; l++, r--)
        {
            // Swap values of l and r
            char temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return String.valueOf(a);
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "geeks";
        strToBinary(s);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to convert
# string into binary string

# utility function
def strToBinary(s):
    bin_conv = []

    for c in s:

        # convert each char to
        # ASCII value
        ascii_val = ord(c)

        # Convert ASCII value to binary
        binary_val = bin(ascii_val)
        bin_conv.append(binary_val[2:])

    return (' '.join(bin_conv))

# Driver Code
if __name__ == '__main__':
    s = 'geeks'

print (strToBinary(s))

# This code is contributed
# by Vikas Chitturi
```

## C#

```
// C# program to convert
// string into binary string
using System;

public class Node
{

    // utility function
    static void strToBinary(String s)
    {
        int n = s.Length;

        for (int i = 0; i < n; i++)
        {
            // convert each char to
            // ASCII value
            int val = s[i];

            // Convert ASCII value to binary
            String bin = "";
            while (val > 0)
            {
                if (val % 2 == 1)
                {
                    bin += '1';
                }
                else
                    bin += '0';
                val /= 2;
            }
            bin = reverse(bin);

            Console.Write(bin + " ");
        }
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
        return String.Join("",a);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeks";
        strToBinary(s);
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to convert
// string into binary string

// utility function
function strToBinary($s)
{
    $n = strlen($s);

    for ($i = 0; $i < $n; $i++)
    {
        // convert each char to
        // ASCII value
        $val = ord($s[$i]);

        // Convert ASCII value to
        // binary
        $bin = "";
        while ($val > 0)
        {
            ($val % 2)? $bin=$bin.'1' :
                         $bin=$bin.'0';

            $val= floor($val / 2);
        }
        for($x = strlen($bin) - 1;
                    $x >= 0; $x--)

        echo $bin[$x];
        echo " ";
    }
}

// Driver code
$s = "geeks";
strToBinary($s);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to convert
// string into binary string

 // utility function
function strToBinary(s)
{
    let n = s.length;

        for (let i = 0; i < n; i++)
        {
            // convert each char to
            // ASCII value
            let val = (s[i]).charCodeAt(0);

            // Convert ASCII value to binary
            let bin = "";
            while (val > 0)
            {
                if (val % 2 == 1)
                {
                    bin += '1';
                }
                else
                    bin += '0';
                val = Math.floor(val/2);
            }
            bin = reverse(bin);

            document.write(bin + " ");
        }
}

function reverse(input)
{
    a = input.split("");
        let l, r = 0;
        r = a.length - 1;

        for (l = 0; l < r; l++, r--)
        {
            // Swap values of l and r
            let temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return (a).join("");
}

// Driver code
let s = "geeks";
strToBinary(s);

// This code is contributed by rag2127
</script>
```

**输出:**

```
1100111 1100101 1100101 1101011 1110011  
```