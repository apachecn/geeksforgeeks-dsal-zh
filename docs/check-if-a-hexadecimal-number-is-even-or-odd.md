# 检查十六进制数是偶数还是奇数

> 原文:[https://www . geesforgeks . org/check-if-a-十六进制数是偶数还是奇数/](https://www.geeksforgeeks.org/check-if-a-hexadecimal-number-is-even-or-odd/)

给定一个十六进制数，检查它是偶数还是奇数。
**例:**

```
Input: N = ABC7787CC87AA
Output: Even

Input: N = 9322DEFCD
Output: Odd
```

**天真的方法:**

*   [将数字从十六进制基数转换为十进制基数](https://www.geeksforgeeks.org/program-for-hexadecimal-to-decimal/)。
*   然后[检查数字是偶数还是奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，除以 2 很容易检查出来。

**时间复杂度:** O(N)
**高效方法:**由于十六进制数包含 0 到 15 的数字，因此我们可以简单地**检查最后一个数字是‘0’、‘2’、‘4’、‘6’、‘8’、‘A’(= 10)、‘C’(= 12)还是‘E’(= 14)**。如果是，那么给定的十六进制数将是偶数，否则是奇数。
以下是上述方法的实现。

## C++

```
// C++ code to check if a HexaDecimal
// number is Even or Odd

#include <bits/stdc++.h>
using namespace std;

// Check if the number is odd or even
string even_or_odd(string N)
{
    int len = N.size();

    // check if the last digit
    // is either '0', '2', '4',
    // '6', '8', 'A'(=10),
    // 'C'(=12) or 'E'(=14)
    if (N[len - 1] == '0'
        || N[len - 1] == '2'
        || N[len - 1] == '4'
        || N[len - 1] == '6'
        || N[len - 1] == '8'
        || N[len - 1] == 'A'
        || N[len - 1] == 'C'
        || N[len - 1] == 'E')
        return ("Even");
    else
        return ("Odd");
}

// Driver code
int main()
{
    string N = "AB3454D";

    cout << even_or_odd(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a HexaDecimal
// number is Even or Odd
class GFG{

// Check if the number is odd or even
static String even_or_odd(String N)
{
    int len = N.length();

    // check if the last digit
    // is either '0', '2', '4',
    // '6', '8', 'A'(=10),
    // 'C'(=12) or 'E'(=14)
    if (N.charAt(len - 1) == '0'
        || N.charAt(len - 1) == '2'
        || N.charAt(len - 1) == '4'
        || N.charAt(len - 1) == '6'
        || N.charAt(len - 1) == '8'
        || N.charAt(len - 1) == 'A'
        || N.charAt(len - 1) == 'C'
        || N.charAt(len - 1) == 'E')
        return ("Even");
    else
        return ("Odd");
}

// Driver code
public static void main(String[] args)
{
    String N = "AB3454D";
    System.out.print(even_or_odd(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code to check if a HexaDecimal
# number is Even or Odd

# Check if the number is odd or even
def even_or_odd(N):
    l = len(N)

    # check if the last digit
    # is either '0', '2', '4',
    # '6', '8', 'A'(=10),
    # 'C'(=12) or 'E'(=14)
    if (N[l - 1] == '0'or N[l - 1] == '2'or
        N[l - 1] == '4'or N[l - 1] == '6'or
        N[l - 1] == '8'or N[l - 1] == 'A'or
        N[l - 1] == 'C'or N[l - 1] == 'E'):
        return ("Even")
    else:
        return ("Odd")

# Driver code
N = "AB3454D"

print(even_or_odd(N))

# This code is contributed by Atul_kumar_Shrivastava
```

## C#

```
// C# code to check if a HexaDecimal
// number is Even or Odd
using System;

public class GFG{

    // Check if the number is odd or even
    static string even_or_odd(string N)
    {
        int len = N.Length;

        // check if the last digit
        // is either '0', '2', '4',
        // '6', '8', 'A'(=10),
        // 'C'(=12) or 'E'(=14)
        if (N[len - 1] == '0'
            || N[len - 1] == '2'
            || N[len - 1] == '4'
            || N[len - 1] == '6'
            || N[len - 1] == '8'
            || N[len - 1] == 'A'
            || N[len - 1] == 'C'
            || N[len - 1] == 'E')
            return ("Even");
        else
            return ("Odd");
    }

    // Driver code
    static public void Main ()
    {
        string N = "AB3454D";

        Console.WriteLine(even_or_odd(N));
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// Javascript code to check if a HexaDecimal
// number is Even or Odd

    // Check if the number is odd or even
    function even_or_odd(N)
    {
        let len = N.length;

        // check if the last digit
        // is either '0', '2', '4',
        // '6', '8', 'A'(=10),
        // 'C'(=12) or 'E'(=14)
        if (N[len - 1] == '0'
            || N[len - 1] == '2'
            || N[len - 1] == '4'
            || N[len - 1] == '6'
            || N[len - 1] == '8'
            || N[len - 1] == 'A'
            || N[len - 1] == 'C'
            || N[len - 1] == 'E')
            return ("Even");
        else
            return ("Odd");
    }

// Driver Code

    let N = "AB3454D";

    document.write(even_or_odd(N));

</script>
```

**Output:** 

```
Odd
```