# 通过仅交换第三个字符串

使两个字符串相等的最小交换

> 原文:[https://www . geesforgeks . org/minimum-swap-to-make-two-string-equal-by-swap-only-with-third-string/](https://www.geeksforgeeks.org/minimum-swaps-to-make-two-strings-equal-by-swapping-only-with-third-string/)

给定长度相等的三个字符串 **A** 、 **B** 和 **C** ，任务是找到可以执行的交换操作的最小数量，使得当任何交换只能用 **C** 完成时，字符串 **A** 和 **B** 变得相等。

**示例:**

> **输入:**A =“XYZ”，B =“yzx”，C =“yzx”
> T3】输出: 3
> **解释:**
> 将字符串 C 的所有字符与字符串 A 一一互换
> **输入:**A =“pqr”，B =“stu”，C =“vwx”
> **输出:** -1
> **解释**
> It

**方法:**由于字符串的长度相等，因此想法是遍历字符串并检查字符串中存在的字符。
对于每个指数‘I’，出现以下情况:

1.  如果字符串 **A** 给定索引处的字符与 **B** 中的字符相同，那么我们可以继续检查下一个字符。
2.  如果字符串 A 和 B 的给定索引处的字符不相等，那么我们检查字符串 **B 和 C** 或 **A 和 C** 处的字符是否相等，并相应地交换这些字符。
3.  如果以上条件都不满足，那么**不可能**让字符串 A 和 B 相等。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of swaps to make
// two strings equal

#include <bits/stdc++.h>
using namespace std;

// Function to swap the characters
void swap(char& x, char& y)
{
    char temp = x;
    x = y;
    y = temp;
}

// Function to find the minimum number of swaps
// to make two strings equal
void swapOperations(string a, string b, string c)
{
    // Counting length of string
    int l = a.length();
    int i = 0;

    // Initializing the answer
    int total_swaps = 0;

    // For loop to iterate through the
    // given strings
    for (i = 0; i < l; i++) {

        // Condition if both character of
        // string a and b are equal
        if (a[i] == b[i])
            continue;

        // Condition if character of
        // string a and c are equal
        if (a[i] == c[i]) {

            // If yes, then swap
            // the characters
            swap(b[i], c[i]);
            total_swaps++;
            continue;
        }

        // Condition if character of
        // string b and c are equal
        if (b[i] == c[i]) {

            // If yes, then swap
            // the characters
            swap(a[i], c[i]);
            total_swaps++;
            continue;
        }

        // Else, it is impossible to make
        // both the strings equal
        break;
    }

    // Printing the answer
    if (i == l)
        cout << total_swaps << endl;
    else
        cout << -1 << endl;
}

// Driver Code
int main()
{
    string a = "xyz";
    string b = "yzx";
    string c = "yzx";

    swapOperations(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of swaps to make
// two strings equal
class GFG {

    // Function to find the minimum number of swaps
    // to make two strings equal
    static void swapOperations(char []a, char []b, char []c)
    {
        // Counting length of string
        int l = a.length;
        int i = 0;

        // Initializing the answer
        int total_swaps = 0;
        char temp;

        // For loop to iterate through the
        // given strings
        for (i = 0; i < l; i++) {

            // Condition if both character of
            // string a and b are equal
            if (a[i] == b[i])
                continue;

            // Condition if character of
            // string a and c are equal
            if (a[i] == c[i]) {

                // If yes, then swap
                // the characters
                //    swap(b[i], c[i]);
                temp = b[i];
                b[i] = c[i];
                c[i] = temp;

                total_swaps++;
                continue;
            }

            // Condition if character of
            // string b and c are equal
            if (b[i] == c[i]) {

                // If yes, then swap
                // the characters
                //swap(a[i], c[i]);
                temp = a[i];
                a[i] = c[i];
                c[i] = temp;

                total_swaps++;
                continue;
            }

            // Else, it is impossible to make
            // both the strings equal
            break;
        }

        // Printing the answer
        if (i == l)
                System.out.println(total_swaps) ;
        else
                System.out.println(-1) ;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String a = "xyz";
        String b = "yzx";
        String c = "yzx";

        swapOperations(a.toCharArray(), b.toCharArray(), c.toCharArray());

    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of swaps to make
# two strings equal

# Function to find the minimum number of swaps
# to make two strings equal
def swapOperations(a, b, c) :

    # Counting length of string
    l = len(a);
    i = 0;

    # Initializing the answer
    total_swaps = 0;

    # For loop to iterate through the
    # given strings
    for i in range(l) :

        # Condition if both character of
        # string a and b are equal
        if (a[i] == b[i]) :
            continue;

        # Condition if character of
        # string a and c are equal
        if (a[i] == c[i]) :

            # If yes, then swap
            # the characters
            #swap(b[i], c[i]);
            b[i], c[i] = c[i], b[i];
            total_swaps += 1;
            continue;

        # Condition if character of
        # string b and c are equal
        if (b[i] == c[i]) :

            # If yes, then swap
            # the characters
            # swap(a[i], c[i]);
            a[i], c[i] = c[i], a[i];
            total_swaps += 1;
            continue;

        # Else, it is impossible to make
        # both the strings equal
        break;

    i += 1;

    # Printing the answer
    if (i == l) :
        print(total_swaps) ;
    else :
        print(-1);

# Driver Code
if __name__ == "__main__" :

    a = "xyz";
    b = "yzx";
    c = "yzx";

    swapOperations(list(a), list(b), list(c));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation to find the
// minimum number of swaps to make
// two strings equal
using System;

class GFG {

    // Function to find the minimum number of swaps
    // to make two strings equal
    static void swapOperations(char []a, char []b, char []c)
    {
        // Counting length of string
        int l = a.Length;
        int i = 0;

        // Initializing the answer
        int total_swaps = 0;
        char temp;

        // For loop to iterate through the
        // given strings
        for (i = 0; i < l; i++) {

            // Condition if both character of
            // string a and b are equal
            if (a[i] == b[i])
                continue;

            // Condition if character of
            // string a and c are equal
            if (a[i] == c[i]) {

                // If yes, then swap
                // the characters
                //    swap(b[i], c[i]);
                temp = b[i];
                b[i] = c[i];
                c[i] = temp;

                total_swaps++;
                continue;
            }

            // Condition if character of
            // string b and c are equal
            if (b[i] == c[i]) {

                // If yes, then swap
                // the characters
                //swap(a[i], c[i]);
                temp = a[i];
                a[i] = c[i];
                c[i] = temp;

                total_swaps++;
                continue;
            }

            // Else, it is impossible to make
            // both the strings equal
            break;
        }

        // Printing the answer
        if (i == l)
                Console.WriteLine(total_swaps) ;
        else
                Console.WriteLine(-1) ;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string a = "xyz";
        string b = "yzx";
        string c = "yzx";

        swapOperations(a.ToCharArray(), b.ToCharArray(), c.ToCharArray());

    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
      // JavaScript implementation to find the
      // minimum number of swaps to make
      // two strings equal
      // Function to find the minimum number of swaps
      // to make two strings equal
      function swapOperations(a, b, c) {
        // Counting length of string
        var l = a.length;
        var i = 0;

        // Initializing the answer
        var total_swaps = 0;

        // For loop to iterate through the
        // given strings
        for (i = 0; i < l; i++) {
          // Condition if both character of
          // string a and b are equal
          if (a[i] === b[i]) continue;

          // Condition if character of
          // string a and c are equal
          if (a[i] === c[i]) {
            // If yes, then swap
            // the characters
            // swap(b[i], c[i]);
            var temp = b[i];
            b[i] = c[i];
            c[i] = temp;

            total_swaps++;
            continue;
          }

          // Condition if character of
          // string b and c are equal
          if (b[i] === c[i]) {
            // If yes, then swap
            // the characters
            //swap(a[i], c[i]);
            var temp = a[i];
            a[i] = c[i];
            c[i] = temp;

            total_swaps++;
            continue;
          }

          // Else, it is impossible to make
          // both the strings equal
          break;
        }

        // Printing the answer
        if (i === l) document.write(total_swaps);
        else document.write(-1);
      }

      // Driver Code
      var a = "xyz";
      var b = "yzx";
      var c = "yzx";

      swapOperations(a.split(""), b.split(""), c.split(""));
    </script>
```

**Output:** 

```
3
```