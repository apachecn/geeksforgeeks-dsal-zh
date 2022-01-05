# 表示为字符串的大十进制数快速乘法的 Karatsuba 算法

> 原文:[https://www . geesforgeks . org/karatsuba-大十进制数快速乘法算法-表示为字符串/](https://www.geeksforgeeks.org/karatsuba-algorithm-for-fast-multiplication-of-large-decimal-numbers-represented-as-strings/)

给定两个数字串**A**和 **B** ，任务是高效地找到这两个数字串的乘积。

**示例:**

> **输入:**A =**T3】5678，B = 1234
> T5】输出:** 7006652
> 
> **输入:**A =**T3】74638463789，B = 35284567382
> T5】输出:** 2633585904851937530398

**方法:**给定的问题可以使用[卡拉斯图巴的快速乘法算法](https://www.geeksforgeeks.org/karatsuba-algorithm-for-fast-multiplication-using-divide-and-conquer-algorithm/)来解决，其思想是在整数前面附加零，使得两个整数都具有相等的偶数位数 **n** 。此后，按以下方式划分数字:

> A = Al * 10 <sup>n/2</sup> + Ar [Al 和 Ar 包含 A 最左边和最右边的 n/2 位数]
> B = Bl * 10 <sup>n/2</sup> + Br [Bl 和 Br 包含 B 最左边和最右边的 n/2 位数]

*   因此，乘积 **A * B** 也可以表示如下:

> a * b =(al * 10<sup>n/2</sup>+ar)*(bl * 10<sup>n/2</sup>+br)
> =>a * b = 10<sup>* al * bl+10<sup>n/2</sup></sup>

注意，上面的表达式只需要三次乘法 **Al*Bl** 、 **Ar*Br** 和 **(Al + Ar)*(Bl + Br)** ，而不是标准的四次乘法。因此，复发变为 **T(n) = 3T(n/2) + O(n)** ，该复发的解为 **O(n <sup>1.59</sup> )** 。这个想法在[这篇文章](https://www.geeksforgeeks.org/karatsuba-algorithm-for-fast-multiplication-using-divide-and-conquer-algorithm/)中已经讨论得比较透彻了。因此，上述问题可以通过以下步骤解决:

*   创建一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **findSum()** ，该函数查找两个用字符串表示的大数的[和。同样，创建一个函数 **findDiff()** ，该函数查找表示为字符串](https://www.geeksforgeeks.org/sum-two-large-numbers/)的两个大数的[差。](https://www.geeksforgeeks.org/difference-of-two-large-numbers/)
*   在[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **乘法(A，B)** 中，使用 Karatsuba 的算法对数字进行乘法，首先在 **A** 和 **B** 的前面加上零，使它们的位数相等且均匀。
*   然后计算上述定义的 **Al** 、 **Ar** 、 **Bl** 和 **Br** 的值，递归求**乘(Al，Bl)** 、**乘(Ar，Br)** 和**乘((Al + Ar)、(Bl + Br))** 的值，并将它们的值代入上述公式。
*   在[去掉前导零](https://www.geeksforgeeks.org/remove-leading-zeros-from-a-number-given-as-a-string/)后，打印等式的答案。

下面是上述方法的实现:

## C++

```
// C++ progrram for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of larger
// numbers represented as a string
string findSum(string str1, string str2)
{
    // Before proceeding further, make
    // sure length of str2 is larger
    if (str1.length() > str2.length())
        swap(str1, str2);

    // Stores the result
    string str = "";

    // Calculate length of both string
    int n1 = str1.length();
    int n2 = str2.length();

    // Reverse both of strings
    reverse(str1.begin(), str1.end());
    reverse(str2.begin(), str2.end());

    int carry = 0;
    for (int i = 0; i < n1; i++) {

        // Find the sum of the current
        // digits and carry
        int sum
            = ((str1[i] - '0')
               + (str2[i] - '0')
               + carry);
        str.push_back(sum % 10 + '0');

        // Calculate carry for next step
        carry = sum / 10;
    }

    // Add remaining digits of larger number
    for (int i = n1; i < n2; i++) {
        int sum = ((str2[i] - '0') + carry);
        str.push_back(sum % 10 + '0');
        carry = sum / 10;
    }

    // Add remaining carry
    if (carry)
        str.push_back(carry + '0');

    // Reverse resultant string
    reverse(str.begin(), str.end());

    return str;
}

// Function to find difference of larger
// numbers represented as strings
string findDiff(string str1, string str2)
{
    // Stores the result of difference
    string str = "";

    // Calculate length of both string
    int n1 = str1.length(), n2 = str2.length();

    // Reverse both of strings
    reverse(str1.begin(), str1.end());
    reverse(str2.begin(), str2.end());

    int carry = 0;

    // Run loop till small string length
    // and subtract digit of str1 to str2
    for (int i = 0; i < n2; i++) {

        // Compute difference of the
        // current digits
        int sub
            = ((str1[i] - '0')
               - (str2[i] - '0')
               - carry);

        // If subtraction < 0 then add 10
        // into sub and take carry as 1
        if (sub < 0) {
            sub = sub + 10;
            carry = 1;
        }
        else
            carry = 0;

        str.push_back(sub + '0');
    }

    // Subtract the remaining digits of
    // larger number
    for (int i = n2; i < n1; i++) {
        int sub = ((str1[i] - '0') - carry);

        // If the sub value is -ve,
        // then make it positive
        if (sub < 0) {
            sub = sub + 10;
            carry = 1;
        }
        else
            carry = 0;

        str.push_back(sub + '0');
    }

    // Reverse resultant string
    reverse(str.begin(), str.end());

    // Return answer
    return str;
}

// Function to remove all leading 0s
// from a given string
string removeLeadingZeros(string str)
{
    // Regex to remove leading 0s
    // from a string
    const regex pattern("^0+(?!$)");

    // Replaces the matched value
    // with given string
    str = regex_replace(str, pattern, "");
    return str;
}

// Function to multiply two numbers
// using Karatsuba algorithm
string multiply(string A, string B)
{
    if (A.length() > B.length())
        swap(A, B);

    // Make both numbers to have
    // same digits
    int n1 = A.length(), n2 = B.length();
    while (n2 > n1) {
        A = "0" + A;
        n1++;
    }

    // Base case
    if (n1 == 1) {

        // If the length of strings is 1,
        // then return their product
        int ans = stoi(A) * stoi(B);
        return to_string(ans);
    }

    // Add zeros in the beginning of
    // the strings when length is odd
    if (n1 % 2 == 1) {
        n1++;
        A = "0" + A;
        B = "0" + B;
    }

    string Al, Ar, Bl, Br;

    // Find the values of Al, Ar,
    // Bl, and Br.
    for (int i = 0; i < n1 / 2; ++i) {
        Al += A[i];
        Bl += B[i];
        Ar += A[n1 / 2 + i];
        Br += B[n1 / 2 + i];
    }

    // Recursively call the function
    // to compute smaller product

    // Stores the value of Al * Bl
    string p = multiply(Al, Bl);

    // Stores the value of Ar * Br
    string q = multiply(Ar, Br);

    // Stores value of ((Al + Ar)*(Bl + Br)
    // - Al*Bl - Ar*Br)
    string r = findDiff(
        multiply(findSum(Al, Ar),
                 findSum(Bl, Br)),
        findSum(p, q));

    // Multiply p by 10^n
    for (int i = 0; i < n1; ++i)
        p = p + "0";

    // Multiply s by 10^(n/2)
    for (int i = 0; i < n1 / 2; ++i)
        r = r + "0";

    // Calculate final answer p + r + s
    string ans = findSum(p, findSum(q, r));

    // Remove leading zeroes from ans
    ans = removeLeadingZeros(ans);

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    string A = "74638463789";
    string B = "35284567382";

    cout << multiply(A, B);

    return 0;
}
```

**Output:**

```
2633585904851937530398

```

***时间复杂度:** O(N <sup>log 3</sup> 或 O(N <sup>1.59</sup> ，其中 N 是给定字符串 A 和 b 的长度中的最大值。*
***辅助空间:** O(N <sup>2</sup> )*