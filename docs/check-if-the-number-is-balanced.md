# 检查数字是否平衡

> 原文:[https://www . geesforgeks . org/check-如果数字是平衡的/](https://www.geeksforgeeks.org/check-if-the-number-is-balanced/)

给定一个字符串形式的数字 **N** ，任务是检查给定的数字是否**平衡**。

> **平衡数:**一个数如果前半部分的位数之和等于后半部分的位数之和，则称该数为平衡数。
> **注:**所有[回文号](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)均为平衡号。

**示例:**

> **输入:** N = 19091
> **输出:**平衡
> **说明:**
> 中间元素为 0
> 左半部分之和= 1 + 9 = 10
> 右半部分之和= 9 + 1 = 10
> 因此，给定的数字为平衡数。
> 
> **输入:** N = 133423
> **输出:**不平衡
> **解释:**
> 左半部分之和= 1 + 3 + 3 (7)
> 右半部分之和= 4 + 2 + 3 (9)
> 因此，给定的数字是不平衡的

**方法:**
从头开始迭代数字的一半长度。将**s【I】**和 **s【位数–1–I】**分别加到 **leftSum** 和 **rightSum** 上，同时计算前半部分和后半部分的位数之和。最后，检查**左总和**和**右总和**是否相等。

下面是上述方法的实现。

## C++

```
// C++ program to check
// if a number is
// Balanced or not

#include <bits/stdc++.h>
using namespace std;

// Function to check whether N is
// Balanced Number or not
void BalancedNumber(string s)
{
    int Leftsum = 0;
    int Rightsum = 0;

    // Calculating the Leftsum
    // and rightSum simultaneously
    for (int i = 0; i < s.size() / 2; i++) {

        // Typecasting each character
        // to integer and adding the
        // digit to respective sums
        Leftsum += int(s[i] - '0');
        Rightsum += int(s[s.size() - 1 - i]
                        - '0');
    }

    if (Leftsum == Rightsum)
        cout << "Balanced" << endl;
    else
        cout << "Not Balanced" << endl;
}

// Driver Code
int main()
{
    string s = "12321";

    // Function call
    BalancedNumber(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number
// is Balanced or not
import java.io.*;

class GFG{

// Function to check whether N is
// Balanced Number or not
private static void BalancedNumber(String s)
{
    int Leftsum = 0;
    int Rightsum = 0;

    // Calculating the Leftsum
    // and rightSum simultaneously
    for(int i = 0; i < s.length() / 2; i++)
    {

        // Typecasting each character
        // to integer and adding the
        // digit to respective sums
        Leftsum += (int)(s.charAt(i) - '0');
        Rightsum += (int)(s.charAt(
            s.length() - 1 - i) - '0');
    }

    if (Leftsum == Rightsum)
        System.out.println("Balanced");
    else
        System.out.println("Not Balanced");
}

// Driver Code
public static void main (String[] args)
{
    String s = "12321";

    // Function call
    BalancedNumber(s);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program to check
# if a number is
# Balanced or not

# Function to check whether N is
# Balanced Number or not
def BalancedNumber(s):

    Leftsum = 0
    Rightsum = 0

    # Calculating the Leftsum
    # and rightSum simultaneously
    for i in range(0, int(len(s) / 2)):

        # Typecasting each character
        # to integer and adding the
        # digit to respective sums
        Leftsum = Leftsum + int(s[i])
        Rightsum = (Rightsum +
                    int(s[len(s) - 1 - i]))

    if (Leftsum == Rightsum):
        print("Balanced", end = '\n')
    else:
        print("Not Balanced", end = '\n')

# Driver Code
s = "12321"

# Function call
BalancedNumber(s)

# This code is contributed by PratikBasu
```

## C#

```
// C# program to check
// if a number is
// Balanced or not
using System;
class GFG{

// Function to check whether N is
// Balanced Number or not
static void BalancedNumber(string s)
{
  int Leftsum = 0;
  int Rightsum = 0;

  // Calculating the Leftsum
  // and rightSum simultaneously
  for (int i = 0; i < s.Length / 2; i++)
  {
    // Typecasting each character
    // to integer and adding the
    // digit to respective sums
    Leftsum += (int)(Char.GetNumericValue(s[i]) -
                     Char.GetNumericValue('0'));
    Rightsum += (int)(Char.GetNumericValue(s[s.Length -
                                             1 - i]) -
                      Char.GetNumericValue('0'));
  }

  if (Leftsum == Rightsum)
    Console.WriteLine("Balanced");
  else
    Console.WriteLine("Not Balanced");
} 

// Driver code
static void Main()
{
  string s = "12321";

  // Function call
  BalancedNumber(s);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program to check if a number
// is Balanced or not

// Function to check whether N is
// Balanced Number or not
function BalancedNumber(s)
{
    let Leftsum = 0;
    let Rightsum = 0;

    // Calculating the Leftsum
    // and rightSum simultaneously
    for(let i = 0; i < s.length / 2; i++)
    {

        // Typecasting each character
        // to integer and adding the
        // digit to respective sums
        Leftsum += (s[i] - '0');
        Rightsum += (s[
            s.length - 1 - i] - '0');
    }

    if (Leftsum == Rightsum)
        document.write("Balanced");
    else
        document.write("Not Balanced");
}

// Driver Code

    let s = "12321";

    // Function call
    BalancedNumber(s);

</script>
```

**Output:** 

```
Balanced
```