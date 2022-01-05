# 将给定的数字四舍五入到最接近的 10 的倍数

> 原文:[https://www . geeksforgeeks . org/将给定数字四舍五入为最接近的 10 的倍数/](https://www.geeksforgeeks.org/round-the-given-number-to-nearest-multiple-of-10/)

给定一个正整数 n，将其舍入到以零为最后一位的最近整数。

**示例:**

```
Input : 4722
Output : 4720

Input : 38
Output : 40

Input : 10
Output: 10
```

**方法:**
让我们将给定的数字 n 向下舍入到以 0 结尾的最近整数，并将该值存储在变量 a 中。
a = (n / 10) * 10。所以，向上舍入 n(称之为 b)是 b = a + 10。
如果 n–a>b–n，则答案为 b，否则答案为 a

下面是上述方法的实现:

## C++

```
// C++ program to round the given
// integer to a whole number
// which ends with zero.
#include <bits/stdc++.h>
using namespace std;

// function to round the number
int round(int n)
{
    // Smaller multiple
    int a = (n / 10) * 10;

    // Larger multiple
    int b = a + 10;

    // Return of closest of two
    return (n - a > b - n)? b : a;
}

// driver function
int main()
{
    int n = 4722;
    cout << round(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for Round the given number
// to nearest multiple of 10
import java.util.*;

class GFG {

    // function to round the number
    static int round(int n)
    {
        // Smaller multiple
        int a = (n / 10) * 10;

        // Larger multiple
        int b = a + 10;

        // Return of closest of two
        return (n - a > b - n)? b : a;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
         int n = 4722;
         System.out.println(round(n));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 code to round the given
# integer to a whole number
# which ends with zero.

# function to round the number
def round( n ):

    # Smaller multiple
    a = (n // 10) * 10

    # Larger multiple
    b = a + 10

    # Return of closest of two
    return (b if n - a > b - n else a)

# driver code
n = 4722
print(round(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Code for Round the given number
// to nearest multiple of 10
using System;

class GFG {

    // function to round the number
    static int round(int n)
    {
        // Smaller multiple
        int a = (n / 10) * 10;

        // Larger multiple
        int b = a + 10;

        // Return of closest of two
        return (n - a > b - n)? b : a;
    }

    // Driver program
    public static void Main()
    {
        int n = 4722;
        Console.WriteLine(round(n));
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to round the given integer
// to a whole number which ends with zero.

// function to round the number
function roundFunation($n)
{
    // Smaller multiple
    $a = (int)($n / 10) * 10;

    // Larger multiple
    $b = ($a + 10);

    // Return of closest of two
    return ($n - $a > $b - $n) ? $b : $a;
}

// Driver Code
$n = 4722;
echo roundFunation($n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Code for Round the given number
    // to nearest multiple of 10

    // function to round the number
    function round(n)
    {
        // Smaller multiple
        let a = parseInt(n / 10, 10) * 10;

        // Larger multiple
        let b = a + 10;

        // Return of closest of two
        return (n - a > b - n)? b : a;
    }

    let n = 4722;
      document.write(round(n));

        // THIS CODE IS CONTRIBUTED BY MUKESH07.
</script>
```

**输出:**

```
4720
```

**n 较大时的另一种方法:**
以上方法仅适用于 Integer 或 Long MAX 值。如果输入长度较大，则上述 int 或 long-range 方法不起作用。

我们可以用 String 来解决这个问题。

## C++

```
// C++ code for above approach
#include <bits/stdc++.h>
using namespace std;

// Program to round the number to the
// nearest number having one's digit 0
string Round(string s, int n)
{
    string c = s;

    // last character is 0 then return the
    // original string
    if(c[n - 1] == '0')
      return s;

    // if last character is
    // 1 or 2 or 3 or 4 or 5 make it 0
    else if(c[n - 1] == '1' || c[n - 1] == '2' ||
            c[n - 1] == '3' || c[n - 1] == '4' ||
            c[n - 1] == '5' )
    {
      c[n - 1] = '0';
      return c;
    }
    else
    {
      c[n - 1] = '0';

      // process carry
      for(int i = n - 2 ; i >= 0 ; i--)
      {
        if(c[i] == '9')
          c[i] = '0';
        else
        {
          int t = c[i] - '0' + 1;
          c[i] = (char)(48 + t);
          break;
        }
      }
    }

    string s1 = c;

    if(s1[0] == '0')
      s1 = "1" + s1;

    // return final string
    return s1;
}

// Driver code
int main()
{
    string s="5748965412485599999874589965999";
    int n=s.length();

    // Function Call
    cout << Round(s,n) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.io.*;

class GFG
{

  // Program to round the number to the
  // nearest number having one's digit 0
  public static String round(String s, int n)
  {
    char[] c=s.toCharArray();

    // last character is 0 then return the
    // original string
    if(c[n-1]=='0')
      return s;

    // if last character is
    // 1 or 2 or 3 or 4 or 5 make it 0
    else if(c[n-1] == '1' || c[n-1] == '2' ||
            c[n-1] == '3' || c[n-1] == '4' ||
            c[n-1] == '5' )
    {
      c[n-1]='0';
      return new String(c);
    }
    else
    {
      c[n-1]='0';

      // process carry
      for(int i = n - 2 ; i >= 0 ; i--)
      {
        if(c[i] == '9')
          c[i]='0';
        else
        {
          int t= c[i] - '0' + 1;
          c[i]=(char)(48+t);
          break;
        }
      }
    }

    String s1=new String(c);

    if(s1.charAt(0) == '0')
      s1="1"+s1;

    // return final string
    return s1;
  }

  // Driver Code
  public static void main (String[] args)
  {

    String s="5748965412485599999874589965999";
    int n=s.length();

    // Function Call
    System.out.println(round(s,n));

  }
}
```

## 蟒蛇 3

```
# Python3 code for above approach

# Function to round the number to the
# nearest number having one's digit 0
def Round(s, n):

    s = list(s)
    c = s.copy()

    # Last character is 0 then return the
    # original string
    if (c[n - 1] == '0'):
        return ("".join(s))

    # If last character is
    # 1 or 2 or 3 or 4 or 5 make it 0
    elif (c[n - 1] == '1' or c[n - 1] == '2' or
          c[n - 1] == '3' or c[n - 1] == '4' or
          c[n - 1] == '5'):
        c[n - 1] = '0'
        return ("".join(c))
    else:
        c[n - 1] = '0'

        # Process carry
        for i in range(n - 2, -1, -1):
            if (c[i] == '9'):
                c[i] = '0'
            else:
                t = ord(c[i]) - ord('0') + 1
                c[i] = chr(48 + t)
                break

    s1 = "".join(c)

    if (s1[0] == '0'):
        s1 = "1" + s1

    # Return final string
    return s1

# Driver code
s = "5748965412485599999874589965999"
n = len(s)

print(Round(s, n))

# This code is contributed by rag2127
```

## C#

```
// C# code for above approach
using System;
class GFG {

  // Program to round the number to the
  // nearest number having one's digit 0
  static string round(string s, int n)
  {
    char[] c = s.ToCharArray();

    // last character is 0 then return the
    // original string
    if(c[n - 1] == '0')
      return s;

    // if last character is
    // 1 or 2 or 3 or 4 or 5 make it 0
    else if(c[n - 1] == '1' || c[n - 1] == '2' ||
            c[n - 1] == '3' || c[n - 1] == '4' ||
            c[n - 1] == '5' )
    {
      c[n - 1] = '0';
      return new string(c);
    }
    else
    {
      c[n - 1] = '0';

      // process carry
      for(int i = n - 2 ; i >= 0 ; i--)
      {
        if(c[i] == '9')
          c[i] = '0';
        else
        {
          int t = c[i] - '0' + 1;
          c[i] = (char)(48 + t);
          break;
        }
      }
    }

    string s1 = new string(c);

    if(s1[0] == '0')
      s1 = "1" + s1;

    // return final string
    return s1;
  }

  static void Main() {
    string s="5748965412485599999874589965999";
    int n=s.Length;

    // Function Call
    Console.WriteLine(round(s,n));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript code for above approach

// Program to round the number to the
// nearest number having one's digit 0
function round(s, n)
{
    let c = s.split('');

    // Last character is 0 then return the
    // original string
    if (c[n - 1] == '0')
        return s;

    // If last character is
    // 1 or 2 or 3 or 4 or 5 make it 0
    else if (c[n - 1] == '1' || c[n - 1] == '2' ||
             c[n - 1] == '3' || c[n - 1] == '4' ||
             c[n - 1] == '5' )
    {
        c[n - 1] = '0';
        return c.join("");
    }
    else
    {
        c[n - 1] = '0';

        // process carry
        for(let i = n - 2 ; i >= 0 ; i--)
        {
            if (c[i] == '9')
                c[i] = '0';
            else
            {
                let t = c[i].charCodeAt() -
                         '0'.charCodeAt() + 1;
                c[i] = String.fromCharCode(48 + t);
                break;
            }
        }
    }

    let s1 = c.join("");

    if (s1[0] == '0')
        s1 = "1" + s1;

    // Return final string
    return s1;
}

// Driver code  
let s = "5748965412485599999874589965999";
let n = s.length;

// Function Call
document.write(round(s,n));

// This code is contributed by rameshtravel07

</script>
```

**Output**

```
5748965412485599999874589966000
```