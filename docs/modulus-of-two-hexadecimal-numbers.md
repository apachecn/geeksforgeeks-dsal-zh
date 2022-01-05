# 两个十六进制数的模

> 原文:[https://www . geeksforgeeks . org/二进制数字模数/](https://www.geeksforgeeks.org/modulus-of-two-hexadecimal-numbers/)

给定两个[十六进制数](https://www.geeksforgeeks.org/arithmetic-operations-of-hexadecimal-numbers/) **N** 和 **K** ，任务是找到**N**T8】模 T10】K .

**示例:**

> **输入:** N = 3E8，K = 13
> **输出:** C
> **说明:**
> N(= 3e 8)的十进制表示为 1000
> K(= 13)的十进制表示为 19
> 的十进制表示为(N % K) = 1000 % 19 = 12 ( = C)。
> 因此，要求的输出是 c。
> 
> **输入:** N = 2A3，K = 1A
> T3】输出: 19

**方法:**按照以下步骤解决问题:

*   [将十六进制数 N 和 K 分别转换成它们等价的十进制数](https://www.geeksforgeeks.org/program-for-hexadecimal-to-decimal/)比如说 **X** 和 **Y** 。
*   [将十进制数(X % Y)转换成其等价的十六进制数](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)比如说 **res**
*   最后，打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate modulus of
// two Hexadecimal numbers
void hexaModK(string s, string k)
{

    // Store all possible
    // hexadecimal digits
    map<char, int> mp;

    // Iterate over the range ['0', '9']
    for(char i = 1; i <= 9; i++)
    {
        mp[i + '0'] = i;
    }

    mp['A'] = 10;
    mp['B'] = 11;
    mp['C'] = 12;
    mp['D'] = 13;
    mp['E'] = 14;
    mp['F'] = 15;

    // Convert given string to long
    long m = stoi(k, 0, 16);

    // Base to get 16 power
    long base = 1;

    // Store N % K
    long ans = 0;

    // Iterate over the digits of N
    for(int i = s.length() - 1;
            i >= 0; i--)
    {

        // Stores i-th digit of N
        long n = mp[s[i]] % m;

        // Update ans
        ans = (ans + (base % m * n
                      % m) % m) % m;

        // Update base
        base = (base % m * 16 % m) % m;
    }

    // Print the answer converting
    // into hexadecimal
    stringstream ss;
    ss << hex << ans;
    string su = ss.str();
    transform(su.begin(), su.end(),
              su.begin(), ::toupper);
    cout << (su);
}

// Driver Code
int main()
{

    // Given string N and K
    string n = "3E8";
    string k = "13";

    // Function Call
    hexaModK(n, k);
    return 0;
}

// This code is contributed by sallagondaavinashreddy7
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;
public class Main {

    // Function to calculate modulus of
    // two Hexadecimal numbers
    static void hexaModK(String N, String k)
    {
        // Store all possible
        // hexadecimal digits
        HashMap<Character, Integer> map
            = new HashMap<>();

        // Iterate over the range ['0', '9']
        for (char i = '0'; i <= '9'; i++) {
            map.put(i, i - '0');
        }
        map.put('A', 10);
        map.put('B', 11);
        map.put('C', 12);
        map.put('D', 13);
        map.put('E', 14);
        map.put('F', 15);

        // Convert given string to long
        long m = Long.parseLong(k, 16);

        // Base to get 16 power
        long base = 1;

        // Store N % K
        long ans = 0;

        // Iterate over the digits of N
        for (int i = N.length() - 1;
            i >= 0; i--) {

            // Stores i-th digit of N
            long n
                = map.get(N.charAt(i)) % m;

            // Update ans
            ans = (ans + (base % m * n % m) % m) % m;

            // Update base
            base = (base % m * 16 % m) % m;
        }

        // Print the answer converting
        // into hexadecimal
        System.out.println(
            Long.toHexString(ans).toUpperCase());
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given string N and K
        String n = "3E8";
        String k = "13";

        // Function Call
        hexaModK(n, k);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate modulus of
# two Hexadecimal numbers
def hexaModK(s, k) :

    # Store all possible
    # hexadecimal digits
    mp = {};

    # Iterate over the range ['0', '9']
    for i in range(1, 10) :

        mp[chr(i + ord('0'))] = i;

    mp['A'] = 10;
    mp['B'] = 11;
    mp['C'] = 12;
    mp['D'] = 13;
    mp['E'] = 14;
    mp['F'] = 15;

    # Convert given string to long
    m = int(k);

    # Base to get 16 power
    base = 1;

    # Store N % K
    ans = 0;

    # Iterate over the digits of N
    for i in range(len(s) - 1, -1, -1) :

        # Stores i-th digit of N
        n = mp[s[i]] % m;

        # Update ans
        ans = (ans + (base % m * n
                      % m) % m) % m;

        # Update base
        base = (base % m * 16 % m) % m;

    # Print the answer converting
    # into hexadecimal
    ans = hex(int(ans))[-1].upper()

    print(ans)

# Driver Code
if __name__ == "__main__" :

    # Given string N and K
    n = "3E8";
    k = "13";

    # Function Call
    hexaModK(n, k);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate modulus of
// two Hexadecimal numbers
static void hexaModK(String N, String k)
{

    // Store all possible
    // hexadecimal digits
    Dictionary<char,
               int> map = new Dictionary<char,
                                         int>();

    // Iterate over the range ['0', '9']
    for(char i = '0'; i <= '9'; i++)
    {
        map.Add(i, i - '0');
    }
    map.Add('A', 10);
    map.Add('B', 11);
    map.Add('C', 12);
    map.Add('D', 13);
    map.Add('E', 14);
    map.Add('F', 15);

    // Convert given string to long
    long m = long.Parse(k);

    // Base to get 16 power
    long Base = 1;

    // Store N % K
    long ans = 0;

    // Iterate over the digits of N
    for(int i = N.Length - 1; i >= 0; i--)
    {

        // Stores i-th digit of N
        long n = map[N[i]] % m;

        // Update ans
        ans = (ans + (Base % m * n % m) % m) % m;

        // Update base
        Base = (Base % m * 16 % m) % m;
    }

    // Print the answer converting
    // into hexadecimal
    Console.WriteLine(ans.ToString("X"));
}

// Driver Code
public static void Main(String []args)
{

    // Given string N and K
    String n = "3E8";
    String k = "13";

    // Function Call
    hexaModK(n, k);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to calculate modulus of
// two Hexadecimal numbers
function hexaModK(s, k)
{

    // Store all possible
    // hexadecimal digits
    var mp = new Map();

    // Iterate over the range ['0', '9']
    for(var i = 1; i <= 9; i++)
    {
        mp.set(String.fromCharCode(
            i + '0'.charCodeAt(0)), i);
    }

    mp.set('A', 10);
    mp.set('B', 11);
    mp.set('C', 12);
    mp.set('D', 13);
    mp.set('E', 14);
    mp.set('F', 15);

    // Convert given string to long
    var m = parseInt(k, 16);

    // Base to get 16 power
    var base = 1;

    // Store N % K
    var ans = 0;

    // Iterate over the digits of N
    for(var i = s.length - 1;
            i >= 0; i--)
    {

        // Stores i-th digit of N
        var n = mp.get(s[i]) % m;

        // Update ans
        ans = (ans + (base % m * n % m) % m) % m;

        // Update base
        base = (base % m * 16 % m) % m;
    }
    document.write(ans.toString(16).toUpperCase());
}

// Driver Code

// Given string N and K
var n = "3E8";
var k = "13";

// Function Call
hexaModK(n, k);

// This code is contributed by famously

</script>
```

**Output:** 

```
C
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)