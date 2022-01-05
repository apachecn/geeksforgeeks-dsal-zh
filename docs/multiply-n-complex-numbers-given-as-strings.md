# 将作为字符串给出的 N 个复数相乘

> 原文:[https://www . geesforgeks . org/multiply-n-complex-numbers-以字符串形式给出/](https://www.geeksforgeeks.org/multiply-n-complex-numbers-given-as-strings/)

给定字符串形式的 **N** 复数，任务是打印这些 **N** 复数的乘法。

**示例:**

> **输入:** N = 3，V = { 3 + 1i，2 + 1i，5 + -7i }
> **输出:** 10+-60i
> **说明:**
> 首先我们将(3 + 1i)和(2+1i)相乘得到 5+5i。下一步，我们将 5+5i 和-5+-7i 相乘，得到最终结果 **10+-60i** 。
> 
> **输入:** N = 3，V = {“7+4i”、“-12+1i”、“-16+-7i”、“12+18i”}
> **输出:** -9444+35442i

**接近**

*   首先，从头开始迭代，取前两个字符串，并删除它们。
*   接下来，将字符串转换为带有适当符号的数字。将字符串的实部和虚部存储在单独的变量中。取 **a** 为第一弦的实部， **b** 为第一弦的虚部。取 **c** 为第二弦的实部， **d** 为第二弦的虚部。
*   接下来，我们将通过计算 **a** 和 **c** 的乘积，并将其与 **b** 的乘积相减，再与 **b** 和 **d** 的乘积相减，来计算实数的合成值。对于虚部，我们将计算 **a** 和 **d** 的乘积之和，以及 **b** 和 **c** 的乘积。
*   然后，我们将生成一个临时字符串来获取之前计算的实值和虚值之和。
*   我们将把结果字符串推进向量。重复以上步骤，直到向量中只剩下一个元素。
*   返回向量中最后一个剩余的元素，这就是想要的答案。

下面是我们上述方法的实现:

## C++

```
// C++ Program to multiply
// N complex Numbers
#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function which returns the
// string in digit format
vector<long long int> findnum(string s1)
{
    vector<long long int> v;
    // a : real
    // b : imaginary
    int a = 0, b = 0;
    int sa = 0, sb = 0, i = 0;
    // sa : sign of a
    // sb : sign of b
    if (s1[0] == '-') {
        sa = 1;
        i = 1;
    }
    // Extract the real number
    while (isdigit(s1[i])) {
        a = a * 10 + (int(s1[i]) - 48);
        i++;
    }

    if (s1[i] == '+') {
        sb = 0;
        i += 1;
    }

    if (s1[i] == '-') {
        sb = 1;
        i += 1;
    }

    // Extract the imaginary part
    while (i < s1.length() && isdigit(s1[i])) {
        b = b * 10 + (int(s1[i]) - 48);
        i++;
    }

    if (sa)
        a *= -1;

    if (sb)
        b *= -1;

    v.push_back(a);
    v.push_back(b);

    return v;
}

string complexNumberMultiply(vector<string> v)
{
    // if size==1 means we reached at result
    while (v.size() != 1) {
        // Extract the first two elements
        vector<ll> v1 = findnum(v[0]);
        vector<ll> v2 = findnum(v[1]);

        // Remove them
        v.erase(v.begin());
        v.erase(v.begin());

        // Calculate and store the real part
        ll r = (v1[0] * v2[0] - v1[1] * v2[1]);
        // Calculate and store the imaginary part
        ll img = v1[0] * v2[1] + v1[1] * v2[0];

        string res = "";
        // Append the real part
        res += to_string(r);
        res += '+';
        // Append the imaginary part
        res += to_string(img) + 'i';

        // Insert into vector
        v.insert(v.begin(), res);
    }

    return v[0];
}

// Driver Function
int main()
{
    int n = 3;
    vector<string> v = { "3+1i",
                         "2+1i", "-5+-7i" };

    cout << complexNumberMultiply(v) << "\n";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to multiply
# N complex Numbers

# Function which returns the
# in digit format
def findnum(s1):

    v = []

    # a : real
    # b : imaginary
    a = 0
    b = 0
    sa = 0
    sb = 0
    i = 0

    # sa : sign of a
    # sb : sign of b
    if (s1[0] == '-'):
        sa = 1
        i = 1

    # Extract the real number
    while (s1[i].isdigit()):
        a = a * 10 + (int(s1[i]))
        i += 1

    if (s1[i] == '+'):
        sb = 0
        i += 1

    if (s1[i] == '-'):
        sb = 1
        i += 1

    # Extract the imaginary part
    while (i < len(s1) and s1[i].isdigit()):
        b = b * 10 + (int(s1[i]))
        i += 1

    if (sa):
        a *= -1

    if (sb):
        b *= -1

    v.append(a)
    v.append(b)

    return v

def complexNumberMultiply(v):

    # If size==1 means we reached at result
    while (len(v) != 1):

        # Extract the first two elements
        v1 = findnum(v[0])
        v2 = findnum(v[1])

        # Remove them
        del v[0]
        del v[0]

        # Calculate and store the real part
        r = (v1[0] * v2[0] - v1[1] * v2[1])

        # Calculate and store the imaginary part
        img = v1[0] * v2[1] + v1[1] * v2[0]

        res = ""

        # Append the real part
        res += str(r)
        res += '+'

        # Append the imaginary part
        res += str(img) + 'i'

        # Insert into vector
        v.insert(0, res)

    return v[0]

# Driver code
if __name__ == '__main__':

    n = 3
    v = [ "3+1i", "2+1i", "-5+-7i" ]

    print(complexNumberMultiply(v))

# This code is contributed by mohit kumar 29
```

**Output:** 

```
10+-60i

```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*