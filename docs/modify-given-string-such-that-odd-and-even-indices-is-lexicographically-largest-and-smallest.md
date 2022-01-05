# 修改给定的字符串，使奇数和偶数索引在字典上最大和最小

> 原文:[https://www . geeksforgeeks . org/modify-给定字符串-这样-奇数和偶数索引-按字典顺序-最大和最小/](https://www.geeksforgeeks.org/modify-given-string-such-that-odd-and-even-indices-is-lexicographically-largest-and-smallest/)

给定一个由 **N** 小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过用当前字符以外的字符替换所有字符来修改给定的字符串，使得由**奇数**和**偶数**索引形成的[后缀字符串](https://www.geeksforgeeks.org/check-if-a-string-is-suffix-of-another/)在字符串 **S** 的所有可能修改中分别按字典顺序最大和最小。

**示例:**

> **输入:**S = " giad "
> T3】输出:azbz
> T6】解释:
> 将给定字符串 S 修改为“azbz”。
> 现在从奇数索引{zbz，z}开始的后缀在所有可能的字符替换中是字典上最大的。
> 从偶数索引{azbz，bz}开始的所有后缀，在所有可能的字符替换中，在词典上是最小的。
> 
> **输入:**S = " ewdwnk "
> T3】输出:阿扎兹

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。想法是用字符**‘z’**替换所有奇数索引字符，如果字符**‘z’**存在，则用**‘y’**替换它。同样，将所有偶数索引字符替换为字符 **'a'** ，如果字符 **'a'** 存在，则替换为 **'b'** 。完成上述修改后，打印字符串 **S** 作为形成的结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify the given string
// satisfying the given criteria
string performOperation(string S, int N)
{
    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If i is even
        if (i % 2 == 0) {

            // If the S[i] is 'a', then
            // change S[i] to 'b'
            if (S[i] == 'a') {
                S[i] = 'b';
            }

            // Otherwise, change S[i]
            // to 'a'
            else {
                S[i] = 'a';
            }
        }
        else {

            // If S[i] is 'z', then
            // change S[i] to 'y'
            if (S[i] == 'z') {

                S[i] = 'y';
            }

            // Otherwise, change S[i]
            // to 'z'
            else {

                S[i] = 'z';
            }
        }
    }

    // Return the result
    return S;
}

// Driver Code
int main()
{
    string S = "giad";
    int N = S.size();
    cout << performOperation(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to modify the given String
// satisfying the given criteria
static String performOperation(char[] S, int N)
{

    // Traverse the String S
    for (int i = 0; i < N; i++) {

        // If i is even
        if (i % 2 == 0) {

            // If the S[i] is 'a', then
            // change S[i] to 'b'
            if (S[i] == 'a') {
                S[i] = 'b';
            }

            // Otherwise, change S[i]
            // to 'a'
            else {
                S[i] = 'a';
            }
        }
        else {

            // If S[i] is 'z', then
            // change S[i] to 'y'
            if (S[i] == 'z') {

                S[i] = 'y';
            }

            // Otherwise, change S[i]
            // to 'z'
            else {

                S[i] = 'z';
            }
        }
    }

    // Return the result
    return String.valueOf(S);
}

// Driver Code
public static void main(String[] args)
{
    String S = "giad";
    int N = S.length();
    System.out.print(performOperation(S.toCharArray(), N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach

# Function to modify the given string
# satisfying the given criteria
def performOperation(S, N):

    # Traverse the string S
    # we cannot directly change string
    # because it is immutable
    # so change of list of char
    S = list(S)
    for i in range(0, N):

                # If i is even
        if (i % 2 == 0):

                        # If the S[i] is 'a', then
                        # change S[i] to 'b'
            if (S[i] == 'a'):
                S[i] = 'b'

                # Otherwise, change S[i]
                # to 'a'
            else:
                S[i] = 'a'

        else:

                        # If S[i] is 'z', then
                        # change S[i] to 'y'
            if (S[i] == 'z'):
                S[i] = 'y'

                # Otherwise, change S[i]
                # to 'z'
            else:
                S[i] = 'z'

    # Return the result
    # join the list of char
    return "".join(S)

# Driver Code
if __name__ == "__main__":
    S = "giad"
    N = len(S)
    print(performOperation(S, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to modify the given string
// satisfying the given criteria
static string performOperation(string S, int N)
{

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If i is even
        if (i % 2 == 0) {

            // If the S[i] is 'a', then
            // change S[i] to 'b'
            if (S[i] == 'a') {
                S = S.Substring(0, i) + 'b' + S.Substring(i + 1);
            }

            // Otherwise, change S[i]
            // to 'a'
            else {
                S = S.Substring(0, i) + 'a' + S.Substring(i + 1);
            }
        }
        else {

            // If S[i] is 'z', then
            // change S[i] to 'y'
            if (S[i] == 'z') {
                S = S.Substring(0, i) + 'y' + S.Substring(i + 1);
            }

            // Otherwise, change S[i]
            // to 'z'
            else {
               S = S.Substring(0, i) + 'z' + S.Substring(i + 1);
            }
        }
    }

    // Return the result
    return S;
}

// Driver Code
public static void Main()
{
    string S = "giad";
    int N = S.Length;
    Console.Write(performOperation(S, N));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
// Function to modify the given string
// satisfying the given criteria
function performOperation(S, N)
{

    // Traverse the string S
    for (var i = 0; i < N; i++) {

        // If i is even
        if (i % 2 == 0) {

            // If the S[i] is 'a', then
            // change S[i] to 'b'
            if (S.charAt(i) == 'a') {
                S[i] = 'b';
            }

            // Otherwise, change S[i]
            // to 'a'
            else {
                S[i]= 'a';
            }
        }
        else {

            // If S[i] is 'z', then
            // change S[i] to 'y'
            if (S.charAt(i) == 'z') {

                S.charAt(i) = 'y';
            }

            // Otherwise, change S[i]
            // to 'z'
            else {

                S[i] = 'z';
            }
        }
    }

    // Return the result
    return S;
}

// Driver Code
    var S = "giad";
    var N = S.length;
    document.write(performOperation(S, N));

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
azbz
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)