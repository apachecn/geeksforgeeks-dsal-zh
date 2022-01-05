# 检查八进制数是偶数还是奇数

> 原文:[https://www . geesforgeks . org/check-如果一个八进制数是偶数还是奇数/](https://www.geeksforgeeks.org/check-if-an-octal-number-is-even-or-odd/)

给定一个八进制数 **N** ，检查它是偶数还是奇数。
**例:**

```
Input: N = 7234
Output: Even

Input: N = 333333333
Output: Odd
```

**天真的方法:**

*   [将数字从八进制转换为十进制](https://www.geeksforgeeks.org/program-octal-decimal-conversion/)。
*   然后[检查数字是偶数还是奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，除以 2 很容易检查出来。

***时间复杂度:**O(N)*
T5】高效方法:由于八进制数包含 0 到 7 的数字，因此我们可以简单地**检查最后一个数字是‘0’、‘2’、‘4’还是‘6’**。如果是，那么给定的八进制数将是偶数，否则是奇数。
以下是上述方法的实施。

## C++

```
// C++ code to check if a Octal
// number is Even or Odd

#include <bits/stdc++.h>
using namespace std;

// Check if the number is odd or even
string even_or_odd(string N)
{
    int len = N.size();

    // Check if the last digit
    // is either '0', '2', '4',
    // or '6'
    if (N[len - 1] == '0'
        || N[len - 1] == '2'
        || N[len - 1] == '4'
        || N[len - 1] == '6')
        return ("Even");
    else
        return ("Odd");
}

// Driver code
int main()
{
    string N = "735";

    cout << even_or_odd(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a Octal
// number is Even or Odd
class GFG{

// Check if the number is odd or even
static String even_or_odd(String N)
{
    int len = N.length();

    // Check if the last digit
    // is either '0', '2', '4',
    // or '6'
    if (N.charAt(len - 1) == '0'
        || N.charAt(len - 1) == '2'
        || N.charAt(len - 1) == '4'
        || N.charAt(len - 1) == '6')
        return ("Even");
    else
        return ("Odd");
}

// Driver code
public static void main(String[] args)
{
    String N = "735";

    System.out.print(even_or_odd(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 code to check if a Octal
# number is Even or Odd

# Check if the number is odd or even
def even_or_odd( N):
    l = len(N);

    # Check if the last digit
    # is either '0', '2', '4',
    # or '6'
    if (N[l - 1] == '0'or N[l - 1] == '2'or
        N[l - 1] == '4' or N[l - 1] == '6'):
        return ("Even")
    else:
        return ("Odd")

# Driver code
N = "735"

print(even_or_odd(N))

# This code is contributed by ANKITKUMAR34
```

## C#

```

// C# code to check if a Octal
// number is Even or Odd
using System;

public class GFG{

// Check if the number is odd or even
static String even_or_odd(String N)
{
    int len = N.Length;

    // Check if the last digit
    // is either '0', '2', '4',
    // or '6'
    if (N[len - 1] == '0'
        || N[len - 1] == '2'
        || N[len - 1] == '4'
        || N[len - 1] == '6')
        return ("Even");
    else
        return ("Odd");
}

// Driver code
public static void Main(String[] args)
{
    String N = "735";

    Console.Write(even_or_odd(N));
}
}

// This code contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript code to check if a Octal
// number is Even or Odd

// Check if the number is odd or even
function even_or_odd(N)
{
    var len = N.length;

    // Check if the last digit
    // is either '0', '2', '4',
    // or '6'
    if (N[len - 1] == '0'
        || N[len - 1] == '2'
        || N[len - 1] == '4'
        || N[len - 1] == '6')
        return ("Even");
    else
        return ("Odd");
}

// Driver code

    var N = "735";
    document.write(even_or_odd(N));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Odd
```

时间复杂度:0(1)

辅助空间:0(1)