# 不超过 N 的最大数字，不包含任何 S 的数字

> 原文:[https://www . geesforgeks . org/最大数字不超过不包含任何数字的 s/](https://www.geeksforgeeks.org/largest-number-not-exceeding-n-that-does-not-contain-any-of-the-digits-of-s/)

给定一个数字字符串**N**(*1≤| N |≤10<sup>5</sup>*)和另一个数字字符串**S**(*1≤**| S |**≤10<sup>5</sup>*)，任务是找到最大数字≤ **N** 使其不包含字符串**S**的数字如果需要，删除前导零。

***注:**弦 **S** 不含**‘0’**。*

**示例:**

> **输入:**N =“2004”，S =“2”
> **输出:** 1999
> **解释:**
> **2** 004 有数字 2，在字符串 S 中，
> 因此，继续减少 1，直到得到的数字不包含 2。
> 因此，能得到的最大数字是 1999 年。
> 
> **输入:** N = "12345 "，S = " 23 "
> T3】输出: 11999

**天真方法:**对于 **N** 的每个值，检查它是否包含 **S** 的任何数字。继续将 **N** 减少 **1** ，直到 **S** 中出现的任何数字都不会出现在 **N** 中。

***时间复杂度:**O(| N | * log(| N |)* | S |)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)进行优化。按照以下步骤解决问题:

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并将 **S** 的不同字符存储在 [**地图**](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 中。
*   [穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **N** 。
*   如果发现 **S** 中存在 **N** 的任意一个数字，则说**idx<sup>th</sup>T7】数字，将**N【idx】**减少到 **S** 中不存在的最大数字，说 **LargestDig** 。**
*   范围**【idx+1，| N |–1】**内的数字变为**大数字**。

> **图解:**
> 考虑 N =“2004”和 S =“2”。
> 去掉 **2** ，改为 **1** ，其余数字改为 **S** 中不存在的最大数字，即数字 **9** 。

*   去掉数字的所有前导零。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to obtain the largest number not exceeding
// num which does not contain any digits present in S
string greatestReducedNumber(string num, string s)
{
    // Stores digits of S
    vector<bool> vis_s(10, false);

    // Traverse the string S
    for (int i = 0; i < (int)s.size(); i++) {

        // Set occurrence as true
        vis_s[int(s[i]) - 48] = true;
    }

    int n = num.size();
    int in = -1;

    // Traverse the string n
    for (int i = 0; i < n; i++) {
        if (vis_s[(int)num[i] - '0']) {
            in = i;
            break;
        }
    }

    // All digits of num are not
    // present in string s
    if (in == -1) {
        return num;
    }

    for (char dig = num[in]; dig >= '0'; dig--) {
        if (vis_s[(int)dig - '0'] == 0) {
            num[in] = dig;
            break;
        }
    }

    char LargestDig = '0';

    for (char dig = '9'; dig >= '0'; dig--) {
        if (vis_s[dig - '0'] == false) {

            // Largest Digit not present
            // in the string s
            LargestDig = dig;
            break;
        }
    }

    // Set all digits from positions
    // in + 1 to n - 1 as LargestDig
    for (int i = in + 1; i < n; i++) {
        num[i] = LargestDig;
    }

    // Counting leading zeroes
    int Count = 0;
    for (int i = 0; i < n; i++) {
        if (num[i] == '0')
            Count++;
        else
            break;
    }

    // Removing leading zeroes
    num.erase(0, Count);

    // If the string becomes null
    if ((int)num.size() == 0)
        return "0";

    // Return the largest number
    return num;
}

// Driver Code
int main()
{
    string N = "12345";
    string S = "23";

    cout << greatestReducedNumber(N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.Arrays;

class GFG {

    // Function to obtain the largest number not exceeding
    // num which does not contain any digits present in S
    static String greatestReducedNumber(String num,
                                        String s)
    {
        // Stores digits of S
        Boolean[] vis_s = new Boolean[10];
        Arrays.fill(vis_s, Boolean.FALSE);

        // Traverse the string S
        for (int i = 0; i < (int)s.length(); i++) {

            // Set occurrence as true
            vis_s[(int)(s.charAt(i)) - 48] = true;
        }

        int n = num.length();
        int in = -1;

        // Traverse the string n
        for (int i = 0; i < n; i++) {
            if (vis_s[(int)num.charAt(i) - '0']) {
                in = i;
                break;
            }
        }

        // All digits of num are not
        // present in string s
        if (in == -1) {
            return num;
        }

    for (char dig = num.charAt(in); dig >= '0'; dig--) {
        if (vis_s[(int)dig - '0'] == false) {
            num = num.substring(0, in) + dig
                  + num.substring(in + 1, n);
            break;
        }
    }

    char LargestDig = '0';

    for (char dig = '9'; dig >= '0'; dig--) {
        if (vis_s[dig - '0'] == false) {

            // Largest Digit not present
            // in the string s
            LargestDig = dig;
            break;
        }
    }

    // Set all digits from positions
    // in + 1 to n - 1 as LargestDig
    for (int i = in + 1; i < n; i++) {
        num = num.substring(0, i) + LargestDig;
    }

    // Counting leading zeroes
    int Count = 0;
    for (int i = 0; i < n; i++) {
        if (num.charAt(i) == '0')
            Count++;
        else
            break;
    }

    // Removing leading zeroes
    num = num.substring(Count, n);

    // If the string becomes null
    if ((int)num.length() == 0)
        return "0";

    // Return the largest number
    return num;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String N = "12345";
        String S = "23";

        System.out.print(greatestReducedNumber(N, S));
    }
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to obtain the largest number not exceeding
# num which does not contain any digits present in S
def greatestReducedNumber(num, s) :

    # Stores digits of S
    vis_s = [False] * 10

    # Traverse the string S
    for i in range(len(s)) :

      # Set occurrence as true
      vis_s[(ord)(s[i]) - 48] = True   
    n = len(num)
    In = -1

    # Traverse the string n
    for i in range(n) :
      if (vis_s[ord(num[i]) - ord('0')]) :
        In = i
        break

    # All digits of num are not
    # present in string s
    if (In == -1) :
      return num   
    for dig in range(ord(num[In]), ord('0') - 1, -1) :
      if (vis_s[dig - ord('0')] == False) :
        num = num[0 : In] + chr(dig) + num[In + 1 : n - In - 1]
        break   
    LargestDig = '0'
    for dig in range(ord('9'), ord('0') - 1, -1) :
      if (vis_s[dig - ord('0')] == False) :

        # Largest Digit not present
        # in the string s
        LargestDig = dig
        break

    # Set all digits from positions
    # in + 1 to n - 1 as LargestDig
    for i in range(In + 1, n) :
      num = num[0 : i] + chr(LargestDig)

    # Counting leading zeroes
    Count = 0
    for i in range(n) :
      if (num[i] == '0') :
        Count += 1
      else :
        break

    # Removing leading zeroes
    num = num[Count : n]

    # If the string becomes null
    if (int(len(num)) == 0) :
      return "0"

    # Return the largest number
    return num

    # Driver code
N = "12345"
S = "23"

print(greatestReducedNumber(N, S))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;  
class GFG
{

  // Function to obtain the largest number not exceeding
  // num which does not contain any digits present in S
  static string greatestReducedNumber(string num, string s)
  {

    // Stores digits of S
    bool[] vis_s = new bool[10];

    // Traverse the string S
    for (int i = 0; i < (int)s.Length; i++) {

      // Set occurrence as true
      vis_s[(int)(s[i]) - 48] = true;
    }

    int n = num.Length;
    int In = -1;

    // Traverse the string n
    for (int i = 0; i < n; i++) {
      if (vis_s[(int)num[i] - '0']) {
        In = i;
        break;
      }
    }

    // All digits of num are not
    // present in string s
    if (In == -1) {
      return num;
    }

    for (char dig = num[In]; dig >= '0'; dig--) {
      if (vis_s[(int)dig - '0'] == false) {
        num = num.Substring(0, In) + dig + num.Substring(In + 1, n - In - 1);
        break;
      }
    }

    char LargestDig = '0';

    for (char dig = '9'; dig >= '0'; dig--) {
      if (vis_s[dig - '0'] == false) {

        // Largest Digit not present
        // in the string s
        LargestDig = dig;
        break;
      }
    }

    // Set all digits from positions
    // in + 1 to n - 1 as LargestDig
    for (int i = In + 1; i < n; i++) {
      num = num.Substring(0, i) + LargestDig;
    }

    // Counting leading zeroes
    int Count = 0;
    for (int i = 0; i < n; i++) {
      if (num[i] == '0')
        Count++;
      else
        break;
    }

    // Removing leading zeroes
    num = num.Substring(Count, n);

    // If the string becomes null
    if ((int)num.Length == 0)
      return "0";

    // Return the largest number
    return num;
  }

  // Driver code
  static void Main() {
    string N = "12345";
    string S = "23";

    Console.Write(greatestReducedNumber(N, S));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to obtain the largest number not exceeding
// num which does not contain any digits present in S
function greatestReducedNumber( num, s){
    // Stores digits of S
    let vis_s = [false,false,false,false,false,false,false,false,false,false];

    // Traverse the string S
    for (let i = 0; i < s.length; i++) {
        // Set occurrence as true
        vis_s[Number(s[i]) - 48] = true;
    }

    let n = num.length;
    let inn = -1;

    // Traverse the string n
    for (let i = 0; i < n; i++) {
        if (vis_s[Number(num[i]) - '0']) {
            inn = i;
            break;
        }
    }

    // All digits of num are not
    // present in string s
    if (inn == -1) {
        return num;
    }

    for (let dig = String(num[inn]); dig >= '0'; dig--) {
        if (vis_s[Number(dig) - '0'] == 0) {
            num[inn] = dig;
            break;
        }
    }

    let LargestDig = '0';

    for (let dig = '9'; dig >= '0'; dig--) {
        if (vis_s[dig - '0'] == false) {

            // Largest Digit not present
            // in the string s
            LargestDig = dig;
            break;
        }
    }

    // Set all digits from positions
    // in + 1 to n - 1 as LargestDig
    for (let i = inn + 1; i < n; i++) {
        num[i] = LargestDig;
    }

    // Counting leading zeroes
    let Count = 0;
    for (let i = 0; i < n; i++) {
        if (num[i] == '0')
            Count++;
        else
            break;
    }

    // Removing leading zeroes
    num = Number(num).toString();

    // If the string becomes null
    if (num.length == 0)
        return "0";

    // Return the largest number
    return num;
}

// Driver Code
let N = "12345";
let S = "23";
document.write( greatestReducedNumber(N, S));

// This code is contributed by rohitsingh07052
</script>
```

**Output:** 

```
11999
```

***时间复杂度:**O(| N |+| s |)*
T5**辅助空间:** O(1)