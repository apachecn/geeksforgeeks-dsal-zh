# 用 10 的补码减去两个大数

> 原文:[https://www . geeksforgeeks . org/两个大数字相减-使用-10s-complex/](https://www.geeksforgeeks.org/subtraction-of-two-large-numbers-using-10s-compliment/)

给定两个长度分别为 **N** 和 **M** 的字符串 **str1** 和 **str2** ，每个字符串代表一个大数，任务是使用 [**10 的补码**](https://www.geeksforgeeks.org/10s-compliment-of-a-decimal-number/) 将两个字符串相减。

**示例:**

> **输入:** N = 10，str 1 =“3434243434”，M = 14，str 2 =“22324365765767”
> **输出:** 22320931522333
> 
> **输入:** N = 20，str 1 =“1234533423242431433”，M = 20，str 2 =“1234533423242431432”
> **输出:** 1

**方法:**基本思路类似于[用 2 的补码](https://www.geeksforgeeks.org/subtraction-of-two-numbers-using-2s-complement/)减去两个数。

> 给定字符串的减法可以写成
> T1】str 1–str 2 = str 1+(-str 2)= str 1+(str 2 的 10 补码)

按照以下步骤解决问题:

*   比较两个字符串的长度，并将两者中较小的存储在 **str2** 中。
*   计算 **str2** 的 **10 的补码**。
*   现在，将 **str2** 的 **10 补码**添加到 **str1** 中。
*   如果产生任何进位，则**放下**进位。
*   如果没有进位产生，那么 str1 的**补码就是最终的**答案**。**

下面是上述方法的实现:

## C++

```
// C++ Program to calculate the
// subtraction of two large number
// using 10's complement
#include <bits/stdc++.h>
using namespace std;

// Function to return sum of two
// large numbers given as strings
string sumBig(string a, string b)
{

    // Compare their lengths
    if (a.length() > b.length())
        swap(a, b);

    // Stores the result
    string str = "";

    // Store the respective lengths
    int n1 = a.length(), n2 = b.length();

    int diff = n2 - n1;

    // Initialize carry
    int carry = 0;

    // Traverse from end of both strings
    for (int i = n1 - 1; i >= 0; i--) {

        // Compute sum of
        // current digits and carry
        int sum
            = ((a[i] - '0')
               + (b[i + diff] - '0') + carry);

        // Store the result
        str.push_back(sum % 10 + '0');

        // Update carry
        carry = sum / 10;
    }

    // Add remaining digits of str2[]
    for (int i = n2 - n1 - 1; i >= 0; i--) {

        int sum = ((b[i] - '0') + carry);

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

// Function return 10's
// complement of given number
string complement10(string v)
{
    // Stores the complement
    string complement = "";

    // Calculate 9's complement
    for (int i = 0; i < v.size(); i++) {

        // Subtract every bit from 9
        complement += '9' - v[i] + '0';
    }

    // Add 1 to 9's complement
    // to find 10's complement
    complement = sumBig(complement, "1");
    return complement;
}

// Function returns subtraction
// of two given numbers as strings
string subtract(string a, string b)
{

    // If second string is larger
    if (a.length() < b.length())
        swap(a, b);

    // Calculate respective lengths
    int l1 = a.length(), l2 = b.length();

    // If lengths aren't equal
    int diffLen = l1 - l2;

    for (int i = 0; i < diffLen; i++) {

        // Insert 0's to the beginning
        // of b to make both the lengths equal
        b = "0" + b;
    }

    // Add (complement of B) and A
    string c = sumBig(a, complement10(b));

    // If length of new string is greater
    // than length of first string,
    // than carry is generated
    if (c.length() > a.length()) {
        string::iterator it;

        // Erase first bit
        it = c.begin();

        c.erase(it);

        // Trim zeros at the beginning
        it = c.begin();

        while (*it == '0')
            c.erase(it);

        return c;
    }

    // If both lengths are equal
    else {
        return complement10(c);
    }
}

// Driver Code
int main()
{

    string str1 = "12345334233242431433";
    string str2 = "12345334233242431432";

    cout << subtract(str1, str2) << endl;

    return 0;
}
```

**Output:** 

```
1
```

**时间复杂度:** O(max(N，M))
**辅助空间:** O(max(N，M))