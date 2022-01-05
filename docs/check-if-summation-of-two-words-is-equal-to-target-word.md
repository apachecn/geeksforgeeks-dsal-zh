# 检查两个单词的总和是否等于目标单词

> 原文:[https://www . geesforgeks . org/check-if-summary-of-two-word-等于-target-word/](https://www.geeksforgeeks.org/check-if-summation-of-two-words-is-equal-to-target-word/)

给定三个大小分别为 L、M 和 N 的[字符串](https://www.geeksforgeeks.org/strings-in-c-and-how-to-create-them/)**A****B**和 **C** ，并且仅由小于“K”的小写英文字母组成。任务是通过将字母与字母列表中的索引值映射并串联起来，将字符串解码成整数后，检查字符串 **A** 和 **B** 的和是否等于字符串 **C** 。

**示例:**

> **输入:** A = "acb "，B = "cba "，C = " CDB "
> T3】输出:是
> T6】说明:
> 
> 1.  在用字母列表中的索引值(即 0、1 和 2)替换字符“A”、“b”和“c”后，字符串 A 修改为整数 021。
> 2.  字符串 B 在用字母列表中的索引值(即 0、1 和 2)替换字符“a”、“B”和“c”后，修改为整数 210。
> 3.  在用字母列表中的索引值(即 1、2 和 3)替换字符“b”、“C”和“d”后，字符串 C 修改为整数 231。
> 
> 字符串 A 和 B 的和(即 21+210 = 231)等于 231，是字符串 c 的值，因此打印“是”。
> 
> **输入:**A =“AAA”，B =“BCB”，C =“BCA”
> T3】输出:否

**方法:**这个问题可以使用类似的方法来解决，该方法用于寻找表示为字符串的两个大数的[和。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sum-two-large-numbers/)

*   [反转琴弦](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/)T2A**B**和 **C** 。
*   初始化两个变量，将 **curr** 和 **rem** 设为 **0** ，将值存储在 **i <sup>th</sup>** 位置以及字符串 **A** 和 **B** 之和的剩余部分。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，最大值(L，最大值(M，N))】**，并执行以下步骤:
    *   在变量 **curr** 中存储字符串 **A** 和 **B** 的**I<sup>th</sup>T3】索引处的字符总和。**
    *   将 **curr** 更新为 **curr = curr+rem** ，然后将 **rem** 更新为 **rem = curr/10。**
    *   现在检查 **i** 是否小于 **N** 和 **curr%10** 是否不等于字符串 **C** 的**C【I】-**即 **i <sup>第</sup>个**字符处的值，然后打印“ **No** ”和 [return](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/) 。
*   最后，完成上述步骤后，如果 **rem** 大于 **0** ，则打印“**否**”。否则，打印“**是**”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check weather summation
// of two words equal to target word
string isSumEqual(string A, string B, string C)
{

    // Store the length of each string
    int L = A.length();
    int M = B.length();
    int N = A.length();

    // Reverse the strings A, B and C
    reverse(A.begin(), A.end());
    reverse(B.begin(), B.end());
    reverse(C.begin(), C.end());

    // Stores the remainder
    int rem = 0;

    // Iterate in the range
    // [0, max(L, max(M, N))]
    for (int i = 0; i < max(L, max(M, N)); i++) {

        // Stores the integer at ith
        // position from the right in
        // the sum of A and B
        int curr = rem;

        // If i is less than L
        if (i < L)
            curr += A[i] - 'a';

        // If i is less than M
        if (i < M)
            curr += B[i] - 'a';

        // Update rem and curr
        rem = curr / 10;
        curr %= 10;

        // If i is less than N
        // and curr is not equal
        // to C[i]-'a', return "No"
        if (i < N && curr != C[i] - 'a') {
            return "No";
        }
    }

    // If rem is greater
    // than 0, return "No"
    if (rem)
        return "No";

    // Otherwise, return "Yes"
    else
        return "Yes";
}

// Driver Code
int main()
{

    // Given Input
    string A = "acb", B = "cba", C = "cdb";

    // Function Call
    cout << isSumEqual(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check weather summation
// of two words equal to target word
static String isSumEqual(String A, String B, String C)
{

    // Store the length of each String
    int L = A.length();
    int M = B.length();
    int N = A.length();

    // Reverse the Strings A, B and C
    A = reverse(A);
    B = reverse(B);
    C = reverse(C);

    // Stores the remainder
    int rem = 0;

    // Iterate in the range
    // [0, Math.max(L, Math.max(M, N))]
    for (int i = 0; i < Math.max(L, Math.max(M, N)); i++) {

        // Stores the integer at ith
        // position from the right in
        // the sum of A and B
        int curr = rem;

        // If i is less than L
        if (i < L)
            curr += A.charAt(i) - 'a';

        // If i is less than M
        if (i < M)
            curr += B.charAt(i) - 'a';

        // Update rem and curr
        rem = curr / 10;
        curr %= 10;

        // If i is less than N
        // and curr is not equal
        // to C[i]-'a', return "No"
        if (i < N && curr != C.charAt(i) - 'a') {
            return "No";
        }
    }

    // If rem is greater
    // than 0, return "No"
    if (rem>0)
        return "No";

    // Otherwise, return "Yes"
    else
        return "Yes";
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    String A = "acb", B = "cba", C = "cdb";

    // Function Call
    System.out.print(isSumEqual(A, B, C));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check weather summation
# of two words equal to target word
def isSumEqual(A, B, C):

    # Store the length of each string
    L = len(A)
    M = len(B)
    N = len(A)

    # Reverse the strings A, B and C
    A = A[::-1]
    B = B[::-1]
    C = C[::-1]

    # Stores the remainder
    rem = 0

    # Iterate in the range
    # [0, max(L, max(M, N))]
    for i in range(max(L, max(M, N))):

        # Stores the integer at ith
        # position from the right in
        # the sum of A and B
        curr = rem

        # If i is less than L
        if (i < L):
            curr += ord(A[i]) - ord('a')

        # If i is less than M
        if (i < M):
            curr += ord(B[i]) - ord('a')

        # Update rem and curr
        rem = curr // 10
        curr %= 10

        # If i is less than N
        # and curr is not equal
        # to C[i]-'a', return "No"
        if (i < N and curr != ord(C[i]) - ord('a')):
            return "No"

    # If rem is greater
    # than 0, return "No"
    if (rem):
        return "No"

    # Otherwise, return "Yes"
    else:
        return "Yes"

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = "acb"
    B = "cba"
    C = "cdb"

    # Function Call
    print (isSumEqual(A, B, C))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to check weather summation
// of two words equal to target word
static String isSumEqual(String A, String B, String C)
{

    // Store the length of each String
    int L = A.Length;
    int M = B.Length;
    int N = A.Length;

    // Reverse the Strings A, B and C
    A = reverse(A);
    B = reverse(B);
    C = reverse(C);

    // Stores the remainder
    int rem = 0;

    // Iterate in the range
    // [0, Math.Max(L, Math.Max(M, N))]
    for (int i = 0; i < Math.Max(L, Math.Max(M, N)); i++) {

        // Stores the integer at ith
        // position from the right in
        // the sum of A and B
        int curr = rem;

        // If i is less than L
        if (i < L)
            curr += A[i] - 'a';

        // If i is less than M
        if (i < M)
            curr += B[i] - 'a';

        // Update rem and curr
        rem = curr / 10;
        curr %= 10;

        // If i is less than N
        // and curr is not equal
        // to C[i]-'a', return "No"
        if (i < N && curr != C[i] - 'a') {
            return "No";
        }
    }

    // If rem is greater
    // than 0, return "No"
    if (rem>0)
        return "No";

    // Otherwise, return "Yes"
    else
        return "Yes";
}
static String reverse(String input) {
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("",a);
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    String A = "acb", B = "cba", C = "cdb";

    // Function Call
    Console.Write(isSumEqual(A, B, C));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check weather summation
// of two words equal to target word
function isSumEqual(A, B, C) {

    // Store the length of each string
    let L = A.length;
    let M = B.length;
    let N = A.length;

    // Reverse the strings A, B and C
    A.split("").reverse().join("");
    B.split("").reverse().join("");
    C.split("").reverse().join("");

    // Stores the remainder
    let rem = 0;

    // Iterate in the range
    // [0, max(L, max(M, N))]
    for (let i = 0; i < Math.max(L, Math.max(M, N)); i++) {

        // Stores the integer at ith
        // position from the right in
        // the sum of A and B
        let curr = rem;

        // If i is less than L
        if (i < L)
            curr += A[i].charCodeAt(0) - 'a'.charCodeAt(0);

        // If i is less than M
        if (i < M)
            curr += B[i].charCodeAt(0) - 'a'.charCodeAt(0);

        // Update rem and curr
        rem = Math.floor(curr / 10);
        curr %= 10;

        // If i is less than N
        // and curr is not equal
        // to C[i]-'a', return "No"
        if (i < N && curr != C[i].charCodeAt(0) -
        'a'.charCodeAt(0)) {
            return "No";
        }
    }

    // If rem is greater
    // than 0, return "No"
    if (rem)
        return "No";

    // Otherwise, return "Yes"
    else
        return "Yes";
}

// Driver Code

// Given Input
let A = "acb", B = "cba", C = "cdb";

// Function Call
document.write(isSumEqual(A, B, C));

</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(L+M+N)*
T5**辅助空间:** O(1)