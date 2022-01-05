# 求 N 串最大公约数的程序

> 原文:[https://www . geesforgeks . org/program-to-find-最大公约数-gcd-of-n-strings/](https://www.geeksforgeeks.org/program-to-find-greatest-common-divisor-gcd-of-n-strings/)

给定一个字符串的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]**，任务是给定字符串数组的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)。

> 在字符串**‘A’**和**‘B’**中，我们说“B 除 A”当且仅当 A = B 的串联超过 1 次。找出将 A 和 b 分开的最大字符串

**示例:**

> **输入:**arr[]= {“GFGGFG”、“GFGGFG”、“GFGGFG”}
> **输出:**【GFGGFG】
> **说明:**
> “GFGGFG”是划分整个数组元素的最大字符串。
> **输入:** arr = {“极客”，=“GFG”}
> **输出:**”

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)。以下是步骤:

1.  创建递归函数 **gcd(str1，str2)** 。
2.  如果 **str2** 的长度大于 **str1** ，那么我们将使用 **gcd(str2，str1)** 来重现。
3.  现在，如果 str1 不是以**开始，那么 str2** 返回一个空字符串。
4.  如果较长的字符串以较短的字符串开头，请切断较长字符串的公共前缀部分，并重复出现或重复，直到其中一个为空。
5.  在上述步骤之后返回的字符串是给定字符串数组的 gcd。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function that finds gcd of 2 strings
string gcd(string str1, string str2)
{

    // If str1 length is less than
    // that of str2 then recur
    // with gcd(str2, str1)
    if (str1.length() < str2.length())
    {
        return gcd(str2, str1);
    }

    // If str1 is not the
    // concatenation of str2
    else if(str1.find(str2) != 0)
    {
        return "";
    }
    else if (str2 == "")
    {

        // GCD string is found
        return str1;
    }
    else
    {

        // Cut off the common prefix
        // part of str1 & then recur
        return gcd(str1.substr(str2.length()), str2);
    }
}

// Function to find GCD of array of
// strings
string findGCD(string arr[], int n)
{
    string result = arr[0];
    for (int i = 1; i < n; i++)
    {
        result = gcd(result, arr[i]);
    }

    // Return the GCD of strings
    return result;
}

// Driver Code
int main()
{

    // Given array  of strings
    string arr[]={ "GFGGFG",
                         "GFGGFG",
                         "GFGGFGGFGGFG" };
    int n = sizeof(arr)/sizeof(arr[0]);

    // Function Call
    cout << findGCD(arr, n);
}

// This code is contributed by pratham76.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GCD {

    // Function that finds gcd of 2 strings
    static String gcd(String str1, String str2)
    {
        // If str1 length is less than
        // that of str2 then recur
        // with gcd(str2, str1)
        if (str1.length() < str2.length()) {
            return gcd(str2, str1);
        }

        // If str1 is not the
        // concatenation of str2
        else if (!str1.startsWith(str2)) {
            return "";
        }

        else if (str2.isEmpty()) {

            // GCD string is found
            return str1;
        }
        else {

            // Cut off the common prefix
            // part of str1 & then recur
            return gcd(str1.substring(str2.length()),
                       str2);
        }
    }

    // Function to find GCD of array of
    // strings
    static String findGCD(String arr[], int n)
    {
        String result = arr[0];

        for (int i = 1; i < n; i++) {
            result = gcd(result, arr[i]);
        }

        // Return the GCD of strings
        return result;
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given array  of strings
        String arr[]
            = new String[] { "GFGGFG",
                             "GFGGFG",
                             "GFGGFGGFGGFG" };
        int n = arr.length;

        // Function Call
        System.out.println(findGCD(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds gcd of 2 strings
def gcd(str1, str2):

    # If str1 length is less than
    # that of str2 then recur
    # with gcd(str2, str1)
    if(len(str1) < len(str2)):
        return gcd(str2, str1)

    # If str1 is not the
    # concatenation of str2
    elif(not str1.startswith(str2)):
        return ""
    elif(len(str2) == 0):

        # GCD string is found
        return str1
    else:

        # Cut off the common prefix
        # part of str1 & then recur
        return gcd(str1[len(str2):], str2)

# Function to find GCD of array of
# strings
def findGCD(arr, n):
    result = arr[0]

    for i in range(1, n):
        result = gcd(result, arr[i])

    # Return the GCD of strings
    return result

# Driver Code

# Given array  of strings
arr = ["GFGGFG", "GFGGFG", "GFGGFGGFGGFG" ]
n = len(arr)

# Function Call
print(findGCD(arr, n))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function that finds gcd
// of 2 strings
static String gcd(String str1,
                  String str2)
{
  // If str1 length is less than
  // that of str2 then recur
  // with gcd(str2, str1)
  if (str1.Length < str2.Length)
  {
    return gcd(str2, str1);
  }

  // If str1 is not the
  // concatenation of str2
  else if (!str1.StartsWith(str2))
  {
    return "";
  }
  else if (str2.Length == 0)
  {
    // GCD string is found
    return str1;
  }
  else
  {
    // Cut off the common prefix
    // part of str1 & then recur
    return gcd(str1.Substring(str2.Length),
                              str2);
  }
}

// Function to find GCD
// of array of strings
static String findGCD(String []arr,
                      int n)
{
  String result = arr[0];

  for (int i = 1; i < n; i++)
  {
    result = gcd(result, arr[i]);
  }

  // Return the GCD of strings
  return result;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array  of strings
  String []arr = new String[] {"GFGGFG",
                               "GFGGFG",
                               "GFGGFGGFGGFG"};
  int n = arr.Length;

  // Function Call
  Console.WriteLine(findGCD(arr, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function that finds gcd
    // of 2 strings
    function gcd(str1, str2)
    {
      // If str1 length is less than
      // that of str2 then recur
      // with gcd(str2, str1)
      if (str1.length < str2.length)
      {
        return gcd(str2, str1);
      }

      // If str1 is not the
      // concatenation of str2
      else if (!str1.startsWith(str2))
      {
        return "";
      }
      else if (str2.length == 0)
      {
        // GCD string is found
        return str1;
      }
      else
      {
        // Cut off the common prefix
        // part of str1 & then recur
        return gcd(str1.substr(str2.length), str2);
      }
    }

    // Function to find GCD
    // of array of strings
    function findGCD(arr, n)
    {
      let result = arr[0];

      for (let i = 1; i < n; i++)
      {
        result = gcd(result, arr[i]);
      }

      // Return the GCD of strings
      return result;
    }

    // Given array  of strings
    let arr = ["GFGGFG", "GFGGFG", "GFGGFGGFGGFG"];
    let n = arr.length;

    // Function Call
    document.write(findGCD(arr, n));

  // This code is contributed by decode2207.
</script>
```

**Output:** 

```
GFGGFG
```

**时间复杂度:** O(N*log(B))，其中 N 为字符串个数，B 为 arr[]中任意字符串的最大长度。
**辅助空间:** O(1)