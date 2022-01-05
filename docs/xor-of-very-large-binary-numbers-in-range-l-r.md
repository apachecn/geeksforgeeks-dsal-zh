# 范围[L，R]

内非常大的二进制数的异或运算

> 原文:[https://www . geeksforgeeks . org/非常大二进制数的异或-范围-l-r/](https://www.geeksforgeeks.org/xor-of-very-large-binary-numbers-in-range-l-r/)

给定两个二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/) **L** 和 **R** ，任务是[找到从 L 到 R 的异或](https://www.geeksforgeeks.org/find-xor-of-numbers-from-the-range-l-r/)。二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/)的长度为 **< = 10e6** 。

**示例:**

> **输入:** L = 10，R = 100
> **输出:** 101
> **说明:** L = 2，R = 4 十进制。因此，异或将是 2^3^4 = 5(101)。
> 
> **输入:** L = 10，R = 10000
> T3】输出:10001T5】

**天真法:**解决问题最简单的方法就是找到**【L，R】**范围内的所有二进制字符串，然后对所有二进制字符串进行异或运算。

***时间复杂度:**(R–L+1)*(N)其中 N 为二进制字符串的长度 R.*
***辅助空间:** O(1)*

**有效方法:**通过观察以下内容，可以进一步优化上述方法

*   **(l ^(l+1)^……^(r–1)^ r)**可以写成 **(1^2^3 ^….^(R-1)^R) ^ (1^2^3 …..^(L-2) ^ (L-1))** 其中'^'表示元素的按位异或。所以问题简化为[求 1 到 n](https://www.geeksforgeeks.org/calculate-xor-1-n/) 的异或。
*   对于[计算从 1 到 n 的异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)，通过用 **4** 对其进行模运算，找到 **n** 的余数，并将其存储在一个变量中，比如 **rem** ，并且**rem**–
    *   如果 **rem =0** ，那么 **xor = n** 。
    *   如果 **rem = 1** ，那么 **xor = 1** 。
    *   如果 **rem = 2** ，那么 **xor = n+1** 。
    *   如果 **rem = 3** ，那么 **xor = 0** 。

观察以上几点后，按照以下步骤解决问题:

*   通过执行以下步骤，创建一个函数**子**，从大小为 N 的二进制字符串中减去 1:
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**中迭代，并执行以下步骤:
        *   如果 **S[i] = '0'** ，则将 **S[i]** 的值修改为 **1。**
        *   如果 **S[i] = '1'** ，则将 **S[i]** 的值修改为 **0** 并终止循环。
    *   返回[串](https://www.geeksforgeeks.org/string-data-structure/) **S** 作为答案。
*   通过执行下面提到的步骤，创建一个函数**和**，将 1 添加到大小为 N 的二进制字符串 S 中:
    *   初始化一个变量，说**携带**为 **0** 。
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**中迭代，并执行以下步骤:
        *   如果 **S[i] = '1'** ，则将 **S[i]** 的值修改为 **0** ，将**进位**的值修改为 **1** 。
        *   如果 **S[i] = '0'** ，则将 **S[i]** 的值修改为 **1** ，将**进位**的值修改为 **0** ，终止循环。
    *   如果**进位=1** ，则将 **S** 的值修改为 **'1' + S** ，并返回字符串 **S** 。
*   通过执行以下步骤，创建一个函数 **Xor_Finder** ，将 Xor 的值从 **1** 返回到 **S** :
    *   初始化一个变量，比如说 **val** 并将该值更新为 **S[n] + S[n-1]*2** ，其中 n 是字符串 S 的长度
    *   现在如果 **val = 0** ，那么返回字符串 **S** 作为答案。
    *   如果 **val = 1** ，则返回‘1’作为答案。
    *   如果 **val = 2** ，则返回 **ad(S)** 作为答案。
    *   如果 **val = 3** ，则返回 0 作为答案。
*   创建一个函数 **final_xor** ，通过执行以下步骤计算两个二进制字符串 L 和 R 的 xor:
    *   将字符“0”添加到字符串 **L** 中，而 **L.size()！= R.size()** 。
    *   初始化一个字符串，比如说**和**，它们将存储二进制字符串 **L** 和 **R** 的异或值。
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，r . size()-1】**中迭代，并执行以下步骤:
        *   如果 **L[i] = R[i]** ，则在字符串 ans 的末尾追加字符“0”。
        *   如果**L【I】！= R[i]** ，然后在字符串 ans 的末尾追加字符“1”。
    *   返回字符串**和**作为两个字符串的异或。
*   通过执行以下步骤，创建一个函数 **xorr** 来计算从 **L** 到 **R** 的 xor:
    *   将 **L** 的值修改为**子(L)** 。
    *   通过调用函数 **xor_finder(L)** 和 **xor_finder(R)** 分别计算从 **1** 到 **L** 和从 **1** 到 **R** 的 xor，修改 **L** 和 **R** 的值。
    *   初始化一个变量，说 **ans** ，通过更新值为 **final_xor(L，R)** 来更新 **ans** 的值。
    *   返回字符串**和**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to subtract one
// from the binary string
string sub(string s)
{
    int n = s.size();
    for (int i = n - 1; i >= 0; i--) {
        // If the current character
        // is 0 change it to 1
        if (s[i] == '0') {
            s[i] = '1';
        }
        else {
            // If the character is 1
            // Change is to 0 and
            // terminate the loop
            s[i] = '0';
            break;
        }
    }
    // Return the answer
    return s;
}

// Function to add 1 in the
// binary string
string ad(string s)
{
    int n = s.size();

    int carry = 0;
    for (int i = n - 1; i >= 0; i--) {
        // If s[i]=='1' it
        // will change s[i] to 0
        // and carry = 1
        if (s[i] == '1') {
            carry = 1;
            s[i] = '0';
        }
        else {
            // If s[i]=='0' it
            // will change s[i] to 1
            // and carry = 0 and
            // end the loop
            carry = 0;
            s[i] = '1';
            break;
        }
    }
    // If still carry left
    // append character 1 to the
    // beginning of the string
    if (carry) {
        s = '1' + s;
    }
    return s;
}

// Function to find xor from 1 to n
string xor_finder(string s)
{
    int n = s.size() - 1;

    // Variable val stores the
    // remainder when binary string
    // is divided by 4
    int val = s[n] - '0';
    val = val + (s[n - 1] - '0') * 2;

    // If val == 0 the xor from
    // 1 to n will be n itself
    if (val == 0) {
        return s;
    }
    else if (val == 1) {
        // If val ==      the xor from
        // 1 to n will be 1 itself
        s = '1';
        return s;
    }
    else if (val == 2) {
        // If val == 2 the xor from
        // 1 to n will be n+1 itself
        return (ad(s));
    }
    else if (val == 3) {
        // If val == 3 the xor from
        // 1 to n will be 0 itself
        s = '0';
        return s;
    }
}
// Function to find the xor of two
// binary string
string final_xor(string L, string R)
{
    // Using loop to equalise the size
    // of string L and R
    while (L.size() != R.size()) {
        L = '0' + L;
    }
    string ans = "";
    for (int i = 0; i < L.size(); i++) {
        // If ith bit of L is 0 and
        // ith bit of R is 0
        // then xor will be 0
        if (L[i] == '0' && R[i] == '0') {
            ans += '0';
        }
        else if (L[i] == '0' && R[i] == '1'
                 || L[i] == '1' && R[i] == '0') {
            // If ith bit of L is 0 and
            // ith bit of R is 1 or
            // vice versa then xor will be 1
            ans += '1';
        }
        else {
            // If ith bit of L is 1 and
            // ith bit of R is 1
            // then xor will be 0
            ans += '0';
        }
    }
    return ans;
}

// Function to find xor from L to R
string xorr(string L, string R)
{
    // changing L to L - 1
    L = sub(L);

    // Finding xor from 1 to L - 1
    L = xor_finder(L);

    // Finding xor from 1 to R
    R = xor_finder(R);

    // Xor of 1, 2, ..., L-1 and 1, 2, ...., R
    string ans = final_xor(L, R);

    return ans;
}

// Driver Code
int main()
{
    // Given Input
    string L = "10", R = "10000";

    // Function Call
    cout << xorr(L, R) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to subtract one
// from the binary string
public static String sub(String s)
{
    StringBuilder new_s = new StringBuilder(s);
    int n = s.length();
    for(int i = n - 1; i >= 0; i--)
    {

        // If the current character
        // is 0 change it to 1
        if (s.charAt(i) == '0')
        {
            new_s.setCharAt(i, '1');
        }
        else
        {

            // If the character is 1
            // Change is to 0 and
            // terminate the loop
            new_s.setCharAt(i, '0');
            break;
        }
    }

    // Return the answer
    return new_s.toString();
}

// Function to add 1 in the
// binary string
public static String ad(String s)
{
    int n = s.length();
    StringBuilder new_s = new StringBuilder(s);
    int carry = 0;
    for(int i = n - 1; i >= 0; i--)
    {

        // If s[i]=='1' it
        // will change s[i] to 0
        // and carry = 1
        if (s.charAt(i) == '1')
        {
            carry = 1;
            new_s.setCharAt(i, '0');
        }
        else
        {

            // If s[i]=='0' it
            // will change s[i] to 1
            // and carry = 0 and
            // end the loop
            carry = 0;
            new_s.setCharAt(i, '1');
            break;
        }
    }

    // If still carry left
    // append character 1 to the
    // beginning of the string
    if (carry != 0)
    {
        s = '1' + new_s.toString();
    }
    return s;
}

// Function to find xor from 1 to n
public static String xor_finder(String s)
{
    int n = s.length() - 1;

    // Variable val stores the
    // remainder when binary string
    // is divided by 4
    int val = s.charAt(n) - '0';
    val = val + (s.charAt(n - 1) - '0') * 2;

    // If val == 0 the xor from
    // 1 to n will be n itself
    if (val == 0)
    {
        return s;
    }
    else if (val == 1)
    {

        // If val == 1 the xor from
        // 1 to n will be 1 itself
        s = "1";
        return s;
    }
    else if (val == 2)
    {

        // If val == 2 the xor from
        // 1 to n will be n+1 itself
        return (ad(s));
    }
    else
    {

        // If val == 3 the xor from
        // 1 to n will be 0 itself
        s = "0";
        return s;
    }
}

// Function to find the xor of two
// binary string
public static String final_xor(String L, String R)
{

    // Using loop to equalise the size
    // of string L and R
    while (L.length() != R.length())
    {
        L = '0' + L;
    }
    String ans = "";
    for(int i = 0; i < L.length(); i++)
    {

        // If ith bit of L is 0 and
        // ith bit of R is 0
        // then xor will be 0
        if (L.charAt(i) == '0' && R.charAt(i) == '0')
        {
            ans += '0';
        }
        else if (L.charAt(i) == '0' && R.charAt(i) == '1' ||
                 L.charAt(i) == '1' && R.charAt(i) == '0')
        {
            // If ith bit of L is 0 and
            // ith bit of R is 1 or
            // vice versa then xor will be 1
            ans += '1';
        }
        else
        {

            // If ith bit of L is 1 and
            // ith bit of R is 1
            // then xor will be 0
            ans += '0';
        }
    }
    return ans;
}

// Function to find xor from L to R
public static String xorr(String L, String R)
{

    // Changing L to L - 1
    L = sub(L);

    // Finding xor from 1 to L - 1
    L = xor_finder(L);

    // Finding xor from 1 to R
    R = xor_finder(R);

    // Xor of 1, 2, ..., L-1 and 1, 2, ...., R
    String ans = final_xor(L, R);

    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    String L = "10", R = "10000";

    // Function Call
    System.out.println(xorr(L, R));
}
}

// This code is contributed by garry133
```

**Output:** 

```
10001
```

**时间复杂度:** O(N)其中 N 是弦的长度
T3】辅助空间: O(N)