# 平衡括号子串的数量

> 原文:[https://www . geeksforgeeks . org/平衡括号子字符串数/](https://www.geeksforgeeks.org/number-of-balanced-parenthesis-substrings/)

给定一个由“ **(** )和“ **)** 组成的平衡括号字符串。任务是找到给定字符串
中[平衡括号](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)子串的数量

**例:**

> **输入:**str =()())()”
> T3】输出: 6
> ()、()、()、()、()、()、())()
> T7】输入:str =(()))()”
> T10】输出: 4
> )、()、()、()、()、()、())()

**方法:**
让我们假设，每当我们遇到左括号时，深度增加 1，当遇到右括号时，深度减少 1。每当我们遇到结束括号时，将我们需要的答案增加 1，然后在这个深度用已经形成的平衡子串增加我们需要的答案。
以下是上述办法的实施:

## C++

```
// CPP program to find number of
// balanced parenthesis sub strings
#include <bits/stdc++.h>
using namespace std;

// Function to find number of
// balanced parenthesis sub strings
int Balanced_Substring(string str, int n)
{
    // To store required answer
    int ans = 0;

    // Vector to stores the number of
    // balanced brackets at each depth.
    vector<int> arr(n / 2 + 1, 0);

    // d stores checks the depth of our sequence
    // For example level of () is 1
    // and that of (()) is 2.
    int d = 0;
    for (int i = 0; i < n; i++) {
        // If open bracket
        // increase depth
        if (str[i] == '(')
            d++;

        // If closing bracket
        else {
            if (d == 1) {
                for (int j = 2; j <= n / 2 + 1 && arr[j] != 0; j++)
                    arr[j] = 0;
            }
            ++ans;
            ans += arr[d];
            arr[d]++;
            d--;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    string str = "()()()";

    int n = str.size();

    // Function call
    cout << Balanced_Substring(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// balanced parenthesis sub strings
class GFG {

    // Function to find number of
    // balanced parenthesis sub strings
    public static int Balanced_Substring(String str,
                                         int n)
    {

        // To store required answer
        int ans = 0;

        // Vector to stores the number of
        // balanced brackets at each depth.
        int[] arr = new int[n / 2 + 1];

        // d stores checks the depth of our sequence
        // For example level of () is 1
        // and that of (()) is 2.
        int d = 0;
        for (int i = 0; i < n; i++) {

            // If open bracket
            // increase depth
            if (str.charAt(i) == '(')
                d++;

            // If closing bracket
            else {
                if (d == 1) {
                    for (int j = 2; j <= n / 2 + 1 && arr[j] != 0; j++)
                        arr[j] = 0;
                }
                ++ans;
                ans += arr[d];
                arr[d]++;
                d--;
            }
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "()()()";
        int n = str.length();

        // Function call
        System.out.println(Balanced_Substring(str, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find number of
# balanced parenthesis sub strings

# Function to find number of
# balanced parenthesis sub strings
def Balanced_Substring(s, n):

    # To store required answer
    ans = 0;

    # Vector to stores the number of
    # balanced brackets at each depth.
    arr = [0] * (int(n / 2) + 1);

    # d stores checks the depth of our sequence
    # For example level of () is 1
    # and that of (()) is 2.
    d = 0;
    for i in range(n):

        # If open bracket
        # increase depth
        if (s[i] == '('):
            d += 1;

        # If closing bracket
        else:
            if (d == 1):
                j = 2
                while (j <= n//2 + 1 and arr[j] != 0):
                    arr[j] = 0
            ans += 1;
            ans += arr[d];
            arr[d] += 1;
            d -= 1;

    # Return the required answer
    return ans;

# Driver code
s = "()()()";
n = len(s);

# Function call
print(Balanced_Substring(s, n));

# This code contributed by Rajput-Ji
```

## C#

```
// C# program to find number of
// balanced parenthesis sub strings
using System;

class GFG {

    // Function to find number of
    // balanced parenthesis sub strings
    public static int Balanced_Substring(String str,
                                         int n)
    {

        // To store required answer
        int ans = 0;

        // Vector to stores the number of
        // balanced brackets at each depth.
        int[] arr = new int[n / 2 + 1];

        // d stores checks the depth of our sequence
        // For example level of () is 1
        // and that of (()) is 2.
        int d = 0;
        for (int i = 0; i < n; i++) {

            // If open bracket
            // increase depth
            if (str[i] == '(')
                d++;

            // If closing bracket
            else {
                if (d == 1) {
                    for (int j = 2; j <= n / 2 + 1 && arr[j] != 0; j++)
                        arr[j] = 0;
                }
                ++ans;
                ans += arr[d];
                arr[d]++;
                d--;
            }
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "()()()";
        int n = str.Length;

        // Function call
        Console.WriteLine(Balanced_Substring(str, n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find number of
// balanced parenthesis sub strings

// Function to find number of
// balanced parenthesis sub strings
function Balanced_Substring(str, n)
{
    // To store required answer
    let ans = 0;

    // Vector to stores the number of
    // balanced brackets at each depth.
    let arr = new Array(n / 2 + 1).fill(0);

    // d stores checks the depth of our sequence
    // For example level of () is 1
    // and that of (()) is 2.
    let d = 0;
    for (let i = 0; i < n; i++) {
        // If open bracket
        // increase depth
        if (str[i] == '(')
            d++;

        // If closing bracket
        else {
            if (d == 1) {
                for (let j = 2; j <= parseInt(n / 2) +
                1 && arr[j] != 0; j++)
                    arr[j] = 0;
            }
            ++ans;
            ans += arr[d];
            arr[d]++;
            d--;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
    let str = "()()()";

    let n = str.length;

    // Function call
    document.write(Balanced_Substring(str, n));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N)