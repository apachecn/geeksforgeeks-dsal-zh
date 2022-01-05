# 检查给定二进制字符串的十进制表示是否能被 K 整除

> 原文:[https://www . geesforgeks . org/检查给定二进制字符串的十进制表示是否可被 k 整除/](https://www.geeksforgeeks.org/check-if-decimal-representation-of-given-binary-string-is-divisible-by-k-or-not/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找出给定二进制字符串的[十进制表示是否能被整数 **K** 整除。](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)

**示例:**

> **输入:** S = 1010，k = 5
> **输出:**是
> **说明:**1010(= 10)的十进制表示可被 5 整除
> 
> **输入:** S = 1010，k = 6
> T3】输出:否

**方法:**由于**模运算符分布在加法**上，因此可以一点一点地检查给定的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)，以查看**十进制% k** 是否等于**零**。按照以下步骤进行操作:

*   初始化一个数组[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)的**大小的**幂两[**，以存储两的幂。**
*   迭代至**大小**并且对于每个 **i** 存储 **2 <sup>i</sup> % K** 于 **poweroftwo[]。**
*   初始化变量，说 **rem = 0，**存储当前剩余数直到 **i** 。
*   迭代直到**大小**并且对于每个 **i** ，如果 **S【大小–I-1】**是 **1** ，那么更新 **rem** 等于**rem+two[I]的幂。**
*   最后，返回**是**如果 rem 等于**零**否则返回**否**

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check the binary number is
// divisible by K
string divisibleByk(string s, int n, int k)
{
    // Array poweroftwo will store pow(2, i)%k
    int poweroftwo[n];

    // Initializing the first element in Array
    poweroftwo[0] = 1 % k;

    for (int i = 1; i < n; i++) {

        // Storing every pow(2, i)%k value in
        // the array
        poweroftwo[i] = (poweroftwo[i - 1]
                         * (2 % k))
                        % k;
    }

    // To store the remaining
    int rem = 0;

    // Iterating till N
    for (int i = 0; i < n; i++) {

        // If current bit is 1
        if (s[n - i - 1] == '1') {

            // Updating rem
            rem += (poweroftwo[i]);
            rem %= k;
        }
    }

    // If completely divisible
    if (rem == 0) {
        return "Yes";
    }

    // If not Completely divisible
    else
        return "No";
}

// Driver Code
int main()
{
    // Given Input
    string s = "1010001";
    int k = 9;

    // length of string s
    int n = s.length();

    // Function Call
    cout << divisibleByk(s, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG
{

    // Function to check the binary number is
    // divisible by K
    public static String divisibleByk(String s, int n, int k) {
        // Array poweroftwo will store pow(2, i)%k
        int[] poweroftwo = new int[n];

        // Initializing the first element in Array
        poweroftwo[0] = 1 % k;

        for (int i = 1; i < n; i++) {

            // Storing every pow(2, i)%k value in
            // the array
            poweroftwo[i] = (poweroftwo[i - 1] * (2 % k)) % k;
        }

        // To store the remaining
        int rem = 0;

        // Iterating till N
        for (int i = 0; i < n; i++) {

            // If current bit is 1
            if (s.charAt(n - i - 1) == '1') {

                // Updating rem
                rem += (poweroftwo[i]);
                rem %= k;
            }
        }

        // If completely divisible
        if (rem == 0) {
            return "Yes";
        }

        // If not Completely divisible
        else
            return "No";
    }

    // Driver Code
    public static void main(String args[])
    {

      // Given Input
        String s = "1010001";
        int k = 9;

        // length of string s
        int n = s.length();

        // Function Call
        System.out.println(divisibleByk(s, n, k));
    }

}

// This code is contributed by _saurabh_jaiswal,
```

## 蟒蛇 3

```
# python 3 program for above approach

# Function to check the binary number is
# divisible by K
def divisibleByk(s, n, k):

    # Array poweroftwo will store pow(2, i)%k
    poweroftwo = [0 for i in range(n)]

    # Initializing the first element in Array
    poweroftwo[0] = 1 % k

    for i in range(1,n,1):
        # Storing every pow(2, i)%k value in
        # the array
        poweroftwo[i] = (poweroftwo[i - 1] * (2 % k)) % k

    # To store the remaining
    rem = 0

    # Iterating till N
    for i in range(n):

        # If current bit is 1
        if (s[n - i - 1] == '1'):

            # Updating rem
            rem += (poweroftwo[i])
            rem %= k

    # If completely divisible
    if (rem == 0):
        return "Yes"

    # If not Completely divisible
    else:
        return "No"

# Driver Code
if __name__ == '__main__':

    # Given Input
    s = "1010001"
    k = 9

    # length of string s
    n = len(s)

    # Function Call
    print(divisibleByk(s, n, k))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for above approach
using System;
class GFG
{

    // Function to check the binary number is
    // divisible by K
    public static String divisibleByk(String s, int n, int k) {
        // Array poweroftwo will store pow(2, i)%k
        int[] poweroftwo = new int[n];

        // Initializing the first element in Array
        poweroftwo[0] = 1 % k;

        for (int i = 1; i < n; i++) {

            // Storing every pow(2, i)%k value in
            // the array
            poweroftwo[i] = (poweroftwo[i - 1] * (2 % k)) % k;
        }

        // To store the remaining
        int rem = 0;

        // Iterating till N
        for (int i = 0; i < n; i++) {

            // If current bit is 1
            if (s[n - i - 1] == '1') {

                // Updating rem
                rem += (poweroftwo[i]);
                rem %= k;
            }
        }

        // If completely divisible
        if (rem == 0) {
            return "Yes";
        }

        // If not Completely divisible
        else
            return "No";
    }

    // Driver Code
    public static void Main(String []args)
    {

      // Given Input
        String s = "1010001";
        int k = 9;

        // length of string s
        int n = s.Length;

        // Function Call
        Console.Write(divisibleByk(s, n, k));
    }

}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to check the binary number is
// divisible by K
function divisibleByk(s, n, k)
{

    // Array poweroftwo will store pow(2, i)%k
    let poweroftwo = new Array(n);

    // Initializing the first element in Array
    poweroftwo[0] = 1 % k;

    for (let i = 1; i < n; i++) {

        // Storing every pow(2, i)%k value in
        // the array
        poweroftwo[i] = (poweroftwo[i - 1]
            * (2 % k))
            % k;
    }

    // To store the remaining
    let rem = 0;

    // Iterating till N
    for (let i = 0; i < n; i++) {

        // If current bit is 1
        if (s[n - i - 1] == '1') {

            // Updating rem
            rem += (poweroftwo[i]);
            rem %= k;
        }
    }

    // If completely divisible
    if (rem == 0) {
        return "Yes";
    }

    // If not Completely divisible
    else
        return "No";
}

// Driver Code

// Given Input
let s = "1010001";
let k = 9;

// length of string s
let n = s.length;

// Function Call
document.write(divisibleByk(s, n, k));

// This code is contributed by gfgking.
</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)