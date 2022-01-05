# 八进制中最大的偶数和奇数 N 位数

> 原文:[https://www . geesforgeks . org/八进制最大偶数和奇数 n 位数/](https://www.geeksforgeeks.org/largest-even-and-odd-n-digit-numbers-in-octal-number-system/)

给定一个整数 **N** ，任务是找出八进制数制中最大的偶数和奇数 **N 位**数。
**例:**

> **输入:** N = 4
> **输出:**
> 偶数:7776
> 奇数:7777
> **输入:** N = 2
> **输出:**
> 偶数:76
> 奇数:77

**方法:**要得到最大的数字，该数字的位数必须尽可能多。因为在八进制数制中，最大位数是**‘7’**。所以，生成**‘7’****(N–1)**次，最后追加**‘6’**为偶数，**‘7’**为奇数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the largest n-digit even
// and odd numbers in octal number system
void findNumbers(int n)
{

    // Append '7' (N - 1) times
    string ans = string(n - 1, '7');

    // Append '6' for an even number
    string even = ans + '6';

    // Append '7' for an odd number
    string odd = ans + '7';

    cout << "Even : " << even << endl;
    cout << "Odd : " << odd << endl;
}

// Driver code
int main()
{
    int n = 4;

    findNumbers(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print the largest n-digit even
// and odd numbers in octal number system
static void findNumbers(int n)
{

    // Append '7' (N - 1) times
    String ans = "";
    for (int i = 0; i < n - 1; i++)
        ans += '7';

    // Append '6' for an even number
    String even = ans + '6';

    // Append '7' for an odd number
    String odd = ans + '7';

    System.out.println("Even : " + even);
    System.out.println("Odd : " + odd);
}

// Driver code
public static void main(String args[])
{
    int n = 4;

    findNumbers(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach ;

# Function to print the largest n-digit even
# and odd numbers in octal number system
def findNumbers(N) :

    # Append '7' (N - 1) times
    ans = '7' * (N - 1)

    # Append '6' for an even number
    even = ans + '6';

    # Append '7' for an odd number
    odd = ans + '7';

    print("Even : ", even);
    print("Odd : ", odd );

# Driver code
if __name__ == "__main__" :

    n = 4;

    findNumbers(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the largest n-digit even
// and odd numbers in octal number system
static void findNumbers(int n)
{

    // Append '7' (N - 1) times
    String ans = "";
    for (int i = 0; i < n - 1; i++)
        ans += '7';

    // Append '6' for an even number
    String even = ans + '6';

    // Append '7' for an odd number
    String odd = ans + '7';

    Console.WriteLine("Even : " + even);
    Console.WriteLine("Odd : " + odd);
}

// Driver code
public static void Main(String []args)
{
    int n = 4;

    findNumbers(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the largest n-digit even
// and odd numbers in octal number system
function findNumbers(n)
{

    // Append '7' (N - 1) times
    var ans = "";
    for (var i = 0; i < n - 1; i++)
        ans += '7';

    // Append '6' for an even number
    var even = ans + '6';

    // Append '7' for an odd number
    var odd = ans + '7';

    document.write("Even : " + even + "<br>");
    document.write("Odd : " + odd + "<br>");
}

// Driver code
    var n = 4;

    findNumbers(n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Even : 7776
Odd : 7777
```

**时间复杂度:** O(n)