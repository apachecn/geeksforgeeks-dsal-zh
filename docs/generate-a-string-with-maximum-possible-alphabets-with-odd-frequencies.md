# 生成一个最大可能字母数为奇数的字符串

> 原文:[https://www . geeksforgeeks . org/generate-a-string-with-oct-frequency-alphabets/](https://www.geeksforgeeks.org/generate-a-string-with-maximum-possible-alphabets-with-odd-frequencies/)

给定一个整数 **N** ，任务是生成一个字符串 **str** ，其中包含最大可能的小写字母，每个字母出现的次数都是奇数。
**例:**

> **输入:** N = 17
> **输出:** bcdefghijklmnopqr
> **说明:**为了最大化字符数，可以选择任意 17 个字符，使其出现一次。因此，abcdefghijklmnopq、bcdefghijklmnopqx 等也可以是有效输出。
> **输入:** N = 35
> **输出:**bcdefghijklmnopqrstuvwxyaaaaaaaaaa
> **说明:**为了最大化字符数，将任意 24 个不同的字符添加一次，剩余长度由任意其他字符填充。

**进场:**

*   如果 **N** 小于等于 26，我们用 **N** 个不同的字符填充字符串，每个字符出现一次。
*   否则:
    *   如果 **N** 是**奇数**，我们将所有 24 个字符从‘b’-‘y’加一次，用‘a’填充剩余的奇数长度。
    *   如果 **N** 是**偶数**，我们将所有 25 个字符从‘b’-‘z’加一次，剩下的奇数长度用‘a’填充。

以下是上述方法的实现:

## C++

```
// C++ program to generate a string
// of length n with maximum possible
// alphabets with each of them
// occuring odd number of times.

#include <bits/stdc++.h>
using namespace std;

// Function to generate a string
// of length n with maximum possible
// alphabets each occuring odd
// number of times.
string generateTheString(int n)
{
    string ans="";
    // If n is odd
    if(n%2)
    {
        // Add all characters from
        // b-y
        for(int i=0;i<min(n,24);i++)
        {
            ans+=(char)('b' + i);
        }
        // Append a to fill the
        // remaining length
        if(n>24)
        {
            for(int i=0;i<(n-24);i++)
                ans+='a';
        }
    }
    // If n is even
    else
    {
        // Add all characters from
        // b-z
        for(int i=0;i<min(n,25);i++)
        {
            ans+=(char)('b' + i);
        }
        // Append a to fill the
        // remaining length
        if(n>25)
        {
            for(int i=0;i<(n-25);i++)
                ans+='a';
        }
    }

    return ans;
}

// Driven code
int main()
{
    int n = 34;
    cout << generateTheString(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate a string
// of length n with maximum possible
// alphabets with each of them
// occuring odd number of times.
import java.util.*;

class GFG{

// Function to generate a string
// of length n with maximum possible
// alphabets each occuring odd
// number of times.
static String generateTheString(int n)
{
    String ans = "";

    // If n is odd
    if (n % 2 != 0)
    {

        // Add all characters from
        // b-y
        for(int i = 0;
                i < Math.min(n, 24); i++)
        {
            ans += (char)('b' + i);
        }

        // Append a to fill the
        // remaining length
        if (n > 24)
        {
            for(int i = 0;
                    i < (n - 24); i++)
                ans += 'a';
        }
    }

    // If n is even
    else
    {

        // Add all characters from
        // b-z
        for(int i = 0;
                i < Math.min(n, 25); i++)
        {
            ans += (char)('b' + i);
        }

        // Append a to fill the
        // remaining length
        if (n > 25)
        {
            for(int i = 0;
                    i < (n - 25); i++)
                ans += 'a';
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 34;

    System.out.println(generateTheString(n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to generate a string
# of length n with maximum possible
# alphabets with each of them
# occuring odd number of times.

# Function to generate a string
# of length n with maximum possible
# alphabets each occuring odd
# number of times.
def generateTheString( n):

    ans = ""

    # If n is odd
    if(n % 2):

        # Add all characters from
        # b-y
        for i in range(min(n, 24)):
            ans += chr(ord('b') + i)

        # Append a to fill the
        # remaining length
        if(n > 24):
            for i in range((n - 24)):
                ans += 'a'

    # If n is even
    else:

        # Add all characters from
        # b-z
        for i in range(min(n, 25)):
            ans += chr(ord('b') + i)

        # Append a to fill the
        # remaining length
        if(n > 25):
            for i in range((n - 25)):
                ans += 'a'
    return ans

# Driver code
if __name__ == "__main__":

    n = 34
    print(generateTheString(n))

# This code is contributed by chitranayal
```

## C#

```
// C# program to generate a string
// of length n with maximum possible
// alphabets with each of them
// occuring odd number of times.
using System;
class GFG{

// Function to generate a string
// of length n with maximum possible
// alphabets each occuring odd
// number of times.
static string generateTheString(int n)
{
    string ans = "";

    // If n is odd
    if(n % 2 == 0)
    {
        // Add all characters from
        // b-y
        for(int i = 0; i < Math.Min(n, 24); i++)
        {
            ans += (char)('b' + i);
        }

        // Append a to fill the
        // remaining length
        if(n > 24)
        {
            for(int i = 0; i < (n - 24); i++)
                ans += 'a';
        }
    }

    // If n is even
    else
    {
        // Add all characters from
        // b-z
        for(int i = 0; i < Math.Min(n, 25); i++)
        {
            ans += (char)('b' + i);
        }

        // Append a to fill the
        // remaining length
        if(n > 25)
        {
            for(int i = 0; i < (n - 25); i++)
                ans += 'a';
        }
    }
    return ans;
}

// Driven code
public static void Main()
{
    int n = 34;
    Console.Write(generateTheString(n));
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>

// Javascript program to generate a string
// of length n with maximum possible
// alphabets with each of them
// occuring odd number of times.

// Function to generate a string
// of length n with maximum possible
// alphabets each occuring odd
// number of times.
function generateTheString(n)
{
    var ans="";
    // If n is odd
    if(n%2)
    {
        // Add all characters from
        // b-y
        for(var i=0;i<min(n,24);i++)
        {
            ans+=(char)('b' + i);
        }
        // Append a to fill the
        // remaining length
        if(n>24)
        {
            for(var i=0;i<(n-24);i++)
                ans+='a';
        }
    }
    // If n is even
    else
    {
        // Add all characters from
        // b-z
        for(var i=0;i<Math.min(n,25);i++)
        {
            ans+= String.fromCharCode('b'.charCodeAt(0) + i);
        }
        // Append a to fill the
        // remaining length
        if(n>25)
        {
            for(var i=0;i<(n-25);i++)
                ans+='a';
        }
    }

    return ans;
}

// Driven code
var n = 34;
document.write( generateTheString(n));

</script>
```

**Output:** 

```
bcdefghijklmnopqrstuvwxyzaaaaaaaaa
```