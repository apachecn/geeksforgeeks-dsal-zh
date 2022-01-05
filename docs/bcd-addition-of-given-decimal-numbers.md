# 给定十进制数的 BCD 相加

> 原文:[https://www . geesforgeks . org/BCD-给定十进制数的加法/](https://www.geeksforgeeks.org/bcd-addition-of-given-decimal-numbers/)

给定两个数字 **A** 和 **B** ，任务是执行给定数字的 BCD 加法。

**示例:**

> **输入:** A = 12，B = 20
> **输出:** 110010
> **说明:**
> A 和 B 之和为 12 + 20 = 32。
> 3 = 0011 的二进制表示
> 2 = 0010 的二进制表示
> 因此，BCD 加法为“0011”+“0010”=“110010”
> 
> **输入:** A = 10，B = 10
> **输出:** 100000
> **说明:**
> A 和 B 之和为 10 + 10 = 20。
> 2 = 0010 的二进制表示
> 0 = 0000 的二进制表示
> 因此，BCD 加法为“0010”+“0000”=“100000”

**方法:**思路是把给定的两个数 A 和 B 的和转换成 BCD 数。以下是步骤:

1.  求两个给定数字 **A** 和 **B** 的和(说 **num** )。
2.  对于数字 **num** 中的每个数字，[将其转换为二进制表示](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)至 **4 位**。
3.  连接上面每个数字的二进制表示并打印结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform BCD Addition
string BCDAddition(int A, int B)
{

    // Store the summation of A and B
    // in form of string
    string s = to_string(A + B);
    int l = s.length();

    // To store the final result
    string ans;

    string str;

    // Forming BCD using Bitset
    for (int i = 0; i < l; i++) {

        // Find the binary representation
        // of the current characters
        str = bitset<4>(s[i]).to_string();
        ans.append(str);
    }

    // Stripping off leading zeroes.
    const auto loc1 = ans.find('1');

    // Return string ans
    if (loc1 != string::npos) {
        return ans.substr(loc1);
    }
    return "0";
}

// Driver Code
int main()
{
    // Given Numbers
    int A = 12, B = 20;

    // Function Call
    cout << BCDAddition(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to perform BCD Addition
static String BCDAddition(int A, int B)
{

    // Store the summation of A and B
    // in form of string
    String s = String.valueOf(A + B);
    int l = s.length();

    // Forming BCD using Bitset
    String temp[] = { "0000", "0001",
                      "0010", "0011",
                      "0100", "0101",
                      "0110", "0111",
                      "1000", "1001" };
    String ans = "";

    for(int i = 0; i < l; i++)
    {

        // Find the binary representation
        // of the current characters
        String t = temp[s.charAt(i) - '0'];
        ans = ans + String.valueOf(t);
    }

    // Stripping off leading zeroes.
    int loc1 = 0;
    while (loc1 < l && ans.charAt(loc1) != '1')
    {
        loc1++;
    }

    // Return string ans
    return ans.substring(loc1);
}

// Driver code    
public static void main(String[] args)
{

    // Given Numbers
    int A = 12;
    int B = 20;

    // Function Call
    System.out.println(BCDAddition(A, B));
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to perform BCD Addition
def BCDAddition(A, B):

    # Store the summation of A and B
    # in form of string
    s = str(A + B)
    l = len(s)

    # Forming BCD using Bitset
    temp = [ "0000", "0001", "0010", "0011", "0100",
             "0101", "0110", "0111", "1000", "1001" ]
    ans = ""

    for i in range(l):

        # Find the binary representation
        # of the current characters
        t = temp[ord(s[i]) - ord('0')]
        ans = ans + str(t)

    # Stripping off leading zeroes.
    loc1 = ans.find('1')

    # Return string ans
    return ans[loc1:]

# Driver Code

# Given Numbers
A = 12
B = 20

# Function Call
print(BCDAddition(A, B))

# This code is contributed by grand_master
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to perform BCD Addition
    static String BCDAddition(int A, int B)
    {

        // Store the summation of A and B
        // in form of string
        string s = (A + B).ToString();
        int l = s.Length;

        // Forming BCD using Bitset
        string[] temp = { "0000", "0001",
                          "0010", "0011",
                          "0100", "0101",
                          "0110", "0111",
                          "1000", "1001" };
        string ans = "";         
        for(int i = 0; i < l; i++)
        {

            // Find the binary representation
            // of the current characters
            string t = temp[s[i] - '0'];
            ans = ans + t.ToString();
        }

        // Stripping off leading zeroes.
        int loc1 = 0;
        while (loc1 < l && ans[loc1] != '1')
        {
            loc1++;
        }

        // Return string ans
        return ans.Substring(loc1);
    }

  // Driver code
  static void Main()
  {

    // Given Numbers
    int A = 12;
    int B = 20;

    // Function Call
    Console.Write(BCDAddition(A, B));
  }
}

// This code is contributed by divyeshrbadiya07.
```

## java 描述语言

```
<script>
// Javascript program for the above approach
// Function to perform BCD Addition
function BCDAddition(A, B)
{

    // Store the summation of A and B
    // in form of string
    var s = (A + B).toString();
    var l = s.length;

    // Forming BCD using Bitset
    temp = [ "0000", "0001",
                    "0010", "0011",
                    "0100", "0101",
                    "0110", "0111",
                    "1000", "1001" ]
    var ans = "";        
    for(var i = 0; i < l; i++)
    {

        // Find the binary representation
        // of the current characters
        var t = temp[s[i] - '0'];
        ans = ans + t.toString();
    }

    // Stripping off leading zeroes.
    var loc1 = 0;
    while (loc1 < l && ans[loc1] != '1')
    {
        loc1++;
    }

    // Return string ans
    return ans.substring(loc1);
}

// Driver code

// Given Numbers
var A = 12;
var B = 20;

// Function Call
document.write(BCDAddition(A, B));

// This code is contributed by     rutvik_56.
</script>
```

**Output:** 

```
110010
```

**时间复杂度:***O(log<sub>10</sub>(A+B))*