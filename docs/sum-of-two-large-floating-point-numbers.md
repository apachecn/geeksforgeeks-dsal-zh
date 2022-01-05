# 两个大浮点数之和

> 原文:[https://www . geeksforgeeks . org/两个大浮点数之和/](https://www.geeksforgeeks.org/sum-of-two-large-floating-point-numbers/)

给定两个非常大的[浮点数](https://www.geeksforgeeks.org/ieee-standard-754-floating-point-numbers/)以大字符串的形式 **str1** 和 **str2** ，任务是将给定的两个数字相加。

**示例:**

> **输入:**str 1 =“584506134 . 87368350839565308”，str 2 =“30598657 . 03304735605874756 . 34983”
> T3】输出:6151 . 44446466665
> 
> **输入:**str 1 =“38.30”，str 2 =“37.0983”
> T3】输出: 75.3983

**方法:**
要找到不能存储在内置数据类型中的两个大整数 的 **[加法，我们将使用](https://www.geeksforgeeks.org/sum-two-large-numbers/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)来存储数字的位数，然后从 LSB 开始逐位执行加法。**

利用这个概念，我们还可以找到大型[浮点数](https://www.geeksforgeeks.org/ieee-standard-754-floating-point-numbers/)的求和。

将两个给定的浮点数相加的步骤:

1.  相对于小数点以字符串形式拆分给定的浮点数，以分隔数字的小数部分和整数部分。
2.  分别将两个数的小数部分和整数部分相加，并将小数相加的最后进位部分转发给整数部分。
    **例如:**

    ```
    str1 = "23.94" and str2 = "34.23"

    For fractional part:
    f1[] = {4, 9}
    f2[] = {3, 2}
    --------------
    Sum  = {7, 1, 1}
    Therefore, Carry = 1

    For Integer part:
    Carry = 1
    I1[] = {3, 2}
    I2[] = {4, 3}
    --------------
    Sum  = {8, 5}

    ```

3.  用一个十进制**'连接存储的整数和小数部分的数字**获取两个大浮点数的所需和。

    ```
    From Integer part = 58
    From fractional part = 17

    Sum = 58.17

    ```

下面是上述方法的实现:

```
// C++ program to find Sum of two
// large Floating-point numbers

#include <bits/stdc++.h>
using namespace std;

// Function to make fractional part
// with equal digits
void makeEqualAtFront(vector<int>& A,
                      vector<int>& B)
{
    int n = A.size();
    int m = B.size();
    int diff = abs(n - m);

    if (n < m) {
        for (int i = 0; i < diff; i++) {
            A.insert(A.begin(), 0);
        }
    }
    else {
        for (int i = 0; i < diff; i++) {
            B.insert(B.begin(), 0);
        }
    }
}

// Function to make Integral part
// with equal digits
void makeEqualAtback(vector<int>& A,
                     vector<int>& B)
{
    int n = A.size();
    int m = B.size();
    int diff = abs(n - m);

    if (n < m) {
        for (int i = 0; i < diff; i++) {
            A.push_back(0);
        }
    }
    else {
        for (int i = 0; i < diff; i++) {
            B.push_back(0);
        }
    }
}

// Function to add the given large
// floating point number string
void findSum(string s1, string s2)
{

    int i;

    // To store the integer and
    // fractional part of numbers
    vector<int> Ints1, Ints2;
    vector<int> Fracs1, Fracs2;

    // Separating integer and
    // fractional part of s1
    for (i = s1.length() - 1; i > -1; i--) {

        // If decimal occurs break
        if (s1[i] == '.') {
            break;
        }
        Fracs1.push_back(s1[i] - '0');
    }

    i--;
    for (; i > -1; i--) {
        Ints1.push_back(s1[i] - '0');
    }

    // Separating integer and
    // fractional part of s2
    for (i = s2.length() - 1; i > -1; i--) {

        // If decimal occurs break
        if (s2[i] == '.') {
            break;
        }
        Fracs2.push_back(s2[i] - '0');
    }

    i--;
    for (; i > -1; i--) {
        Ints2.push_back(s2[i] - '0');
    }

    // Making number of digits in
    // fractional and Integer
    // part equal
    makeEqualAtFront(Fracs1, Fracs2);
    makeEqualAtback(Ints1, Ints2);

    // Adding fractional parts of
    // s1 and s2
    int n = Fracs1.size();
    int m = Fracs2.size();
    i = 0;
    int carry = 0;

    while (i < n && i < m) {

        // Traverse the Fracs1[] and
        // Fracs2[] and add the digit
        // and store the carry
        int sum = Fracs1[i]
                  + Fracs2[i]
                  + carry;

        Fracs1[i] = sum % 10;
        carry = sum / 10;
        i++;
    }

    int N = Ints1.size();
    int M = Ints2.size();
    i = 0;

    // Adding integer part of
    // s1 and s2
    while (i < N && i < M) {
        int sum = Ints1[i]
                  + Ints2[i]
                  + carry;
        Ints1[i] = sum % 10;
        carry = sum / 10;
        i++;
    }
    if (carry != 0)
        Ints1.push_back(carry);

    // Print the result by appending
    // Integer and decimal part stored
    // in Ints1[] and Fracs1[]
    for (int i = Ints1.size() - 1; i > -1; i--) {
        cout << Ints1[i];
    }
    cout << '.';
    for (int i = Fracs1.size() - 1; i > -1; i--) {
        cout << Fracs1[i];
    }
}

// Driver Code
int main()
{
    string str1
        = "584506134.87368350839565308";
    string str2
        = "30598657.0330473560587475634983";

    findSum(str1, str2);

    return 0;
}
```

**Output:**

```
615104791.9067308644544006434983

```