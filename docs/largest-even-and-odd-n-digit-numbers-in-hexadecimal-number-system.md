# 十六进制数制中最大的偶数和奇数 N 位数

> 原文:[https://www . geesforgeks . org/最大偶数和奇数 n 位十六进制数字系统/](https://www.geeksforgeeks.org/largest-even-and-odd-n-digit-numbers-in-hexadecimal-number-system/)

给定一个整数 **N** ，任务是在[十六进制数字系统](https://www.geeksforgeeks.org/number-system-and-base-conversions/)中找到最大的偶数和奇数 **N 位**数字。
**举例:**

> **输入:** N = 1
> **输出:**
> 偶数:E
> 奇数:F
> **输入:** N = 2
> **输出:**
> 偶数:FE
> 奇数:FF

**方法:**要得到最大的数字，该数字的位数必须尽可能多。因为在十六进制数字系统中，最大位数是**‘F’**。所以，生成**【F】****(N–1)**次，最后追加**【E】**为偶数，**【F】**为奇数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the largest n-digit even
// and odd numbers in hexadecimal number system
void findNumbers(int n)
{

    // Append 'F' (N - 1) times
    string ans = string(n - 1, 'F');

    // Append 'E' for an even number
    string even = ans + 'E';

    // Append 'F' for an odd number
    string odd = ans + 'F';

    cout << "Even: " << even << endl;
    cout << "Odd: " << odd << endl;
}

// Driver code
int main()
{
    int n = 2;

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
    // and odd numbers in hexadecimal number system
    static void findNumbers(int n)
    {

        // Append 'F' (N - 1) times
        String ans = string(n - 1, 'F');

        // Append 'E' for an even number
        String even = ans + 'E';

        // Append 'F' for an odd number
        String odd = ans + 'F';

        System.out.print("Even: " + even + "\n");
        System.out.print("Odd: " + odd + "\n");
    }

    private static String string(int n, char c)
    {
        String str = "";
        for (int i = 0; i < n; i++)
            str += c;
        return str;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 2;

        findNumbers(n);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the largest n-digit even
# and odd numbers in hexadecimal number system
def findNumbers(n) :

    # Append 'F' (N - 1) times
    ans = 'F'*(n - 1);

    # Append 'E' for an even number
    even = ans + 'E';

    # Append 'F' for an odd number
    odd = ans + 'F';

    print("Even: " , even);
    print( "Odd: " , odd);

# Driver code
if __name__ == "__main__" :

    n = 2;

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
    // and odd numbers in hexadecimal number system
    static void findNumbers(int n)
    {

        // Append 'F' (N - 1) times
        String ans = strings(n - 1, 'F');

        // Append 'E' for an even number
        String even = ans + 'E';

        // Append 'F' for an odd number
        String odd = ans + 'F';

        Console.Write("Even: " + even + "\n");
        Console.Write("Odd: " + odd + "\n");
    }

    private static String strings(int n, char c)
    {
        String str = "";
        for (int i = 0; i < n; i++)
            str += c;
        return str;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 2;

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
// and odd numbers in hexadecimal number system
function findNumbers(n)
{

    // Append 'F' (N - 1) times
    var ans = "F".repeat(n-1);

    // Append 'E' for an even number
    var even = ans + 'E';

    // Append 'F' for an odd number
    var odd = ans + 'F';

    document.write("Even: " + even + "<br>");
    document.write("Odd: " + odd + "<br>");
}

// Driver code
var n = 2;
findNumbers(n);

</script>
```

**Output:** 

```
Even: FE
Odd: FF
```