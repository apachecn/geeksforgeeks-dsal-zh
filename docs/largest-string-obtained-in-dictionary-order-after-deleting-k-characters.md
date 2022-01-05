# 删除 K 个字符后按字典顺序获得的最大字符串

> 原文:[https://www . geesforgeks . org/最大字符串-字典中获得-删除后的顺序-k-字符/](https://www.geeksforgeeks.org/largest-string-obtained-in-dictionary-order-after-deleting-k-characters/)

给定长度为 **N** 的字符串**和一个整数 **K** ，任务是通过从该字符串中删除 **K** 个字符来返回字典顺序中最大的字符串。**

> 最大字符串字典顺序是字符串按字母顺序排列时的最后一个字符串。

**示例:**

> **输入:** str = "ritz" K = 2
> **输出:** tz
> **说明:**
> 从 s 中删除两个字符有 6 种可能的方式:“ri”、“rt”、“rz”、“it”、“iz”、“tz”。
> 在这些字符串中，“tz”是字典顺序中最大的。
> 因此“tz”是期望的输出。
> 
> **输入:** str = "jackie" K = 2
> **输出:** jkie
> **解释:**
> 删除字符“a”和“c”以获得最大可能的字符串。

**天真方法:**想法是[找到给定字符串](https://www.geeksforgeeks.org/print-subsequences-string/)长度**N–K**的所有子序列。将这些子序列存储在列表中。会有 **<sup>n</sup> C <sub>m</sub>** 这样的序列。完成上述步骤后，按存储在列表中的字母顺序打印最大的字符串。

**时间复杂度:** O(2 <sup>N-K</sup>

**高效途径:**思路是用一个[**德清**](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/) 。以下是步骤:

1.  将字符串的所有字符存储在 deque 中。
2.  遍历给定的字符串，对于字符串中的每个字符，如果它小于存储在 deque 中的最后一个字符，则继续从 deque 中弹出字符。执行该操作，直到 **K** 非零。
3.  现在，在上述操作之后，将当前字符插入到 deque 中。
4.  在上述操作之后，由存储在 deque 中的字符形成的字符串就是结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// string after deleting k characters
string largestString(int n, int k, string s)
{

    // Deque dq used to find the
    // largest string in dictionary
    // after deleting k characters
    deque<char> deq;

    // Iterate till the length
    // of the string
    for(int i = 0; i < n; ++i)
    {

        // Condition for popping
        // characters from deque
        while (deq.size() > 0 &&
               deq.back() < s[i] &&
                        k > 0)
        {
            deq.pop_front();
            k--;
        }

        deq.push_back(s[i]);
    }

    // To store the resultant string
    string st = "";

    // To form resultant string
    for(char c : deq)
        st = st + c;

    // Return the resultant string
    return st;
}

// Driver code   
int main()
{
    int n = 4;
    int k = 2;

    // Given String
    string sc = "ritz";

    // Function call
    string result = largestString(n, k, sc);

    // Print the answer
    cout << result << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.ArrayDeque;
import java.util.Deque;
import java.util.Scanner;
import java.io.IOException;

public class GFG {

    // Function to find the largest
    // string after deleting k characters
    public static String
    largestString(int n, int k, String sc)
    {
        char[] s = sc.toCharArray();

        // Deque dq used to find the
        // largest string in dictionary
        // after deleting k characters
        Deque<Character> deq
            = new ArrayDeque<>();

        // Iterate till the length
        // of the string
        for (int i = 0; i < n; ++i) {

            // Condition for popping
            // characters from deque
            while (deq.size() > 0
                   && deq.getLast() < s[i]
                   && k > 0) {
                deq.pollLast();
                k--;
            }

            deq.add(s[i]);
        }

        // To store the resultant string
        String st = "";

        // To form resultant string
        for (char c : deq)
            st = st + Character.toString(c);

        // Return the resultant string
        return st;
    }

    // Driver Code
    public static void main(String[] args)
        throws IOException
    {
        int n = 4;
        int k = 2;

        // Given String
        String sc = "ritz";

        // Function call
        String result = largestString(n, k, sc);

        // Print the answer
        System.out.println(result);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to find the largest
# string after deleting k characters
def largestString(n, k, sc):

    s = [i for i in sc]

    # Deque dq used to find the
    # largest string in dictionary
    # after deleting k characters
    deq = deque()

    # Iterate till the length
    # of the string
    for i in range(n):

        # Condition for popping
        # characters from deque
        while (len(deq) > 0 and
                deq[-1] < s[i] and
                      k > 0):
            deq.popleft()
            k -= 1

        deq.append(s[i])

    # To store the resultant string
    st = ""

    # To form resultant string
    for c in deq:
        st = st + c

    # Return the resultant string
    return st

# Driver Code
if __name__ == '__main__':

    n = 4
    k = 2

    # Given String
    sc = "ritz"

    # Function call
    result = largestString(n, k, sc)

    # Print the answer
    print(result)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the largest
// string after deleting k characters
function largestString(n, k, s)
{

    // Deque dq used to find the
    // largest string in dictionary
    // after deleting k characters
    var deq = [];

    // Iterate till the length
    // of the string
    for(var i = 0; i < n; ++i)
    {

        // Condition for popping
        // characters from deque
        while (deq.length > 0 &&
               deq[deq.length - 1] < s[i] &&
                            k > 0)
        {
            deq.shift();
            k--;
        }
        deq.push(s[i]);
    }

    // To store the resultant string
    var st = "";

    // To form resultant string
    deq.forEach(c => {
        st = st + c;
    });

    // Return the resultant string
    return st;
}

// Driver code   
var n = 4;
var k = 2;

// Given String
var sc = "ritz";

// Function call
var result = largestString(n, k, sc);

// Print the answer
document.write(result);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
tz
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)