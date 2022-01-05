# 大于 Y 且位数之和等于 X 的最小数

> 原文:[https://www . geesforgeks . org/最小数字大于 y，数字总和等于 x/](https://www.geeksforgeeks.org/smallest-number-greater-than-y-with-sum-of-digits-equal-to-x/)

给定两个整数 **X** 和 **Y** ，求数字之和 **X、**的最小数，严格大于 **Y** 。

**示例:**

> **输入:** X = 18，Y = 99
> **输出:** 189
> **说明:**
> 189 是大于 99 的最小数，位数之和= 18。
> 
> **输入:** X = 12，Y = 72
> **输出:** 75
> **说明:**
> 75 是大于 72 的最小数，位数之和= 12。

**天真方法:**天真方法是从 **Y + 1** 开始迭代，检查是否有数字之和为 **X** 的数字。如果我们找到任何这样的号码，那么打印那个号码。

***时间复杂度:**O((R–Y)* log<sub>10</sub>N，其中 R 是我们迭代之前的最大数值，N 是范围**【Y，R】***
***内的数值辅助空间:** O(1)*

**高效途径:**思路是从右向左迭代 **Y** 的位数，尽量增加当前位数，向右改变位数，使位数之和等于 **X** 。以下是步骤:

*   如果我们从右边考虑第 **(k + 1) <sup>个</sup>数字**并增加它，那么有可能使 **k** 个最低有效数字之和成为**【0，9k】**范围内的任何数字。
*   当找到这样的位置时，停止该过程并在该迭代中打印数字。
*   如果 **k** 个最低有效数字有和 **M** (其中 0 ≤ M ≤ 9k)，则贪婪地获得答案**:

    *   从右向左遍历，插入 9 并从数字总和中减去 9。
    *   一旦总和小于 9，则放置剩余的总和。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum string
// of length d having the sum of digits s
string helper(int d, int s)
{

    // Return a string of length d
    string ans(d, '0');

    for (int i = d - 1; i >= 0; i--) {

        // Greedily put 9's in the end
        if (s >= 9) {
            ans[i] = '9';
            s -= 9;
        }

        // Put remaining sum
        else {
            char c = (char)s + '0';
            ans[i] = c;
            s = 0;
        }
    }

    return ans;
}

// Function to find the smallest
// number greater than Y
// whose sum of digits is X
string findMin(int x, int Y)
{

    // Convert number y to string
    string y = to_string(Y);

    int n = y.size();
    vector<int> p(n);

    // Maintain prefix sum of digits
    for (int i = 0; i < n; i++) {
        p[i] = y[i] - '0';
        if (i > 0)
            p[i] += p[i - 1];
    }

    // Iterate over Y from the back where
    // k is current length of suffix
    for (int i = n - 1, k = 0;; i--, k++) {

        // Stores current digit
        int d = 0;

        if (i >= 0)
            d = y[i] - '0';

        // Increase current digit
        for (int j = d + 1; j <= 9; j++) {

            // Sum upto current prefix
            int r = (i > 0) * p[i - 1] + j;

            // Return answer if remaining
            // sum can be obtained in suffix
            if (x - r >= 0 and x - r <= 9 * k) {

                // Find suffix of length k
                // having sum of digits x-r
                string suf = helper(k, x - r);

                string pre = "";
                if (i > 0)
                    pre = y.substr(0, i);

                // Append current character
                char cur = (char)j + '0';
                pre += cur;

                // Return the result
                return pre + suf;
            }
        }
    }
}

// Driver Code
int main()
{
    // Given Number and Sum
    int x = 18;
    int y = 99;

    // Function Call
    cout << findMin(x, y) << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

@SuppressWarnings("unchecked")
class GFG{

// Function to return the minimum String
// of length d having the sum of digits s
static String helper(int d, int s)
{

    // Return a String of length d
    StringBuilder ans = new StringBuilder();

    for(int i = 0; i < d; i++)
    {
        ans.append("0");
    }

    for(int i = d - 1; i >= 0; i--)
    {

        // Greedily put 9's in the end
        if (s >= 9)
        {
            ans.setCharAt(i,'9');
            s -= 9;
        }

        // Put remaining sum
        else
        {
            char c = (char)(s + (int)'0');
            ans.setCharAt(i,  c);
            s = 0;
        }
    }
    return ans.toString();
}

// Function to find the smallest
// number greater than Y
// whose sum of digits is X
static String findMin(int x, int Y)
{

    // Convert number y to String
    String y = Integer.toString(Y);

    int n = y.length();

    ArrayList p = new ArrayList();

    for(int i = 0; i < n; i++)
    {
        p.add(0);
    }

    // Maintain prefix sum of digits
    for(int i = 0; i < n; i++)
    {
        p.add(i, (int)((int) y.charAt(i) - (int)'0'));

        if (i > 0)
        {
            p.add(i, (int)p.get(i) +
                     (int)p.get(i - 1));
        }
    }

    // Iterate over Y from the back where
    // k is current length of suffix
    for(int i = n - 1, k = 0;; i--, k++)
    {

        // Stores current digit
        int d = 0;

        if (i >= 0)
        {
            d = (int) y.charAt(i) - (int)'0';
        }

        // Increase current digit
        for(int j = d + 1; j <= 9; j++)
        {
            int r = j;

            // Sum upto current prefix
            if (i > 0)
            {
                r += (int) p.get(i - 1);
            }

            // Return answer if remaining
            // sum can be obtained in suffix
            if (x - r >= 0 && x - r <= 9 * k)
            {

                // Find suffix of length k
                // having sum of digits x-r
                String suf = helper(k, x - r);

                String pre = "";

                if (i > 0)
                    pre = y.substring(0, i);

                // Append current character
                char cur = (char)(j + (int)'0');
                pre += cur;

                // Return the result
                return pre + suf;
            }
        }
    }
}

// Driver code
public static void main(String[] arg)
{

    // Given number and sum
    int x = 18;
    int y = 99;

    // Function call
    System.out.print(findMin(x, y));
}
}

// This code is contributed by pratham76
```

## **蟒蛇 3**

```
# Python3 program for the
# above approach

# Function to return the
# minimum string of length
# d having the sum of digits s
def helper(d, s):

    # Return a string of
    # length d
    ans = ['0'] * d

    for i in range(d - 1,
                   -1, -1):

        # Greedily put 9's
        # in the end
        if (s >= 9):
            ans[i] = '9'
            s -= 9

        # Put remaining sum
        else:
            c = chr(s +
                    ord('0'))
            ans[i] = c;
            s = 0;

    return ''.join(ans);

# Function to find the
# smallest number greater
# than Y whose sum of
# digits is X
def findMin(x, Y):

    # Convert number y
    # to string
    y = str(Y);
    n = len(y)
    p = [0] * n

    # Maintain prefix sum
    # of digits
    for i in range(n):
        p[i] = (ord(y[i]) -
                ord('0'))
        if (i > 0):
            p[i] += p[i - 1];

    # Iterate over Y from the
    # back where k is current
    # length of suffix
    n - 1
    k = 0

    while True:

        # Stores current digit
        d = 0;
        if (i >= 0):
            d = (ord(y[i]) -
                 ord('0'))

        # Increase current
        # digit
        for j in range(d + 1,
                       10):

            # Sum upto current
            # prefix
            r = ((i > 0) *
                 p[i - 1] + j);

            # Return answer if
            # remaining sum can
            # be obtained in suffix
            if (x - r >= 0 and
                x - r <= 9 * k):

                # Find suffix of length
                # k having sum of digits
                # x-r
                suf = helper(k,
                             x - r);

                pre = "";
                if (i > 0):
                    pre = y[0 : i]

                # Append current
                # character
                cur = chr(j +
                          ord('0'))
                pre += cur;

                # Return the result
                return pre + suf;

        i -= 1
        k += 1     

# Driver Code
if __name__ == "__main__":

   # Given Number and Sum
    x = 18;
    y = 99;

    # Function Call
    print ( findMin(x, y))

# This code is contributed by Chitranayal
```

## **C#**

```
// C# program for the above approach
using System;
using System.Text;
using System.Collections;

class GFG{

// Function to return the minimum string
// of length d having the sum of digits s
static string helper(int d, int s)
{

    // Return a string of length d
    StringBuilder ans = new StringBuilder();

    for(int i = 0; i < d; i++)
    {
        ans.Append("0");
    }

    for(int i = d - 1; i >= 0; i--)
    {

        // Greedily put 9's in the end
        if (s >= 9)
        {
            ans[i] = '9';
            s -= 9;
        }

        // Put remaining sum
        else
        {
            char c = (char)(s + (int)'0');
            ans[i] = c;
            s = 0;
        }
    }
    return ans.ToString();
}

// Function to find the smallest
// number greater than Y
// whose sum of digits is X
static string findMin(int x, int Y)
{

    // Convert number y to string
    string y = Y.ToString();

    int n = y.Length;

    ArrayList p = new ArrayList();

    for(int i = 0; i < n; i++)
    {
        p.Add(0);
    }

    // Maintain prefix sum of digits
    for(int i = 0; i < n; i++)
    {
        p[i] = (int)((int) y[i] - (int)'0');

        if (i > 0)
        {
            p[i] = (int)p[i] +
                   (int)p[i - 1];
        }
    }

    // Iterate over Y from the back where
    // k is current length of suffix
    for(int i = n - 1, k = 0;; i--, k++)
    {

        // Stores current digit
        int d = 0;

        if (i >= 0)
        {
            d = (int) y[i] - (int)'0';
        }

        // Increase current digit
        for(int j = d + 1; j <= 9; j++)
        {
            int r = j;

            // Sum upto current prefix
            if (i > 0)
            {
                r += (int) p[i - 1];
            }

            // Return answer if remaining
            // sum can be obtained in suffix
            if (x - r >= 0 && x - r <= 9 * k)
            {

                // Find suffix of length k
                // having sum of digits x-r
                string suf = helper(k, x - r);

                string pre = "";

                if (i > 0)
                    pre = y.Substring(0, i);

                // Append current character
                char cur = (char)(j + (int)'0');
                pre += cur;

                // Return the result
                return pre + suf;
            }
        }
    }
}

// Driver code
public static void Main(string[] arg)
{

    // Given number and sum
    int x = 18;
    int y = 99;

    // Function call
    Console.Write(findMin(x, y));
}
}

// This code is contributed by rutvik_56
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to return the minimum String
// of length d having the sum of digits s
function helper(d, s)
{

    // Return a String of length d
    let ans = [];

    for(let i = 0; i < d; i++)
    {
        ans.push("0");
    }

    for(let i = d - 1; i >= 0; i--)
    {

        // Greedily put 9's in the end
        if (s >= 9)
        {
            ans[i] ='9';
            s -= 9;
        }

        // Put remaining sum
        else
        {
            let c = String.fromCharCode(
                s + '0'.charCodeAt(0));
            ans[i] = c;
            s = 0;
        }
    }
    return ans.join("");
}

// Function to find the smallest
// number greater than Y
// whose sum of digits is X
function findMin(x, Y)
{

    // Convert number y to String
    let y = Y.toString();
    let n = y.length;
    let p = [];

    for(let i = 0; i < n; i++)
    {
        p.push(0);
    }

    // Maintain prefix sum of digits
    for(let i = 0; i < n; i++)
    {
        p[i] = y[i].charCodeAt(0) -
                '0'.charCodeAt(0);

        if (i > 0)
        {
            p[i] = p[i] + p[i - 1];
        }
    }

    // Iterate over Y from the back where
    // k is current length of suffix
    for(let i = n - 1, k = 0;; i--, k++)
    {

        // Stores current digit
        let d = 0;

        if (i >= 0)
        {
            d =  y[i].charCodeAt(0) -
                  '0'.charCodeAt(0);
        }

        // Increase current digit
        for(let j = d + 1; j <= 9; j++)
        {
            let r = j;

            // Sum upto current prefix
            if (i > 0)
            {
                r +=  p[i - 1];
            }

            // Return answer if remaining
            // sum can be obtained in suffix
            if (x - r >= 0 && x - r <= 9 * k)
            {

                // Find suffix of length k
                // having sum of digits x-r
                let suf = helper(k, x - r);
                let pre = "";

                if (i > 0)
                    pre = y.substring(0, i);

                // Append current character
                let cur = String.fromCharCode(
                    j + '0'.charCodeAt(0));
                pre += cur;

                // Return the result
                return pre + suf;
            }
        }
    }
}

// Driver code

// Given number and sum
let x = 18;
let y = 99;

// Function call
document.write(findMin(x, y));

// This code is contributed by avanitrachhadiya2155

</script>
```

****Output:** 

```
189
```** 

*****时间复杂度:**O(log<sub>10</sub>Y)*
***辅助空间:**O(log<sub>10</sub>Y)***