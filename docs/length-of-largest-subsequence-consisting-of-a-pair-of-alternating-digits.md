# 由一对交替数字组成的最大子序列的长度

> 原文:[https://www . geesforgeks . org/最大子序列长度-由一对交替数字组成/](https://www.geeksforgeeks.org/length-of-largest-subsequence-consisting-of-a-pair-of-alternating-digits/)

给定一个由数字 0 到 9 组成的数字串 **s** ，任务是找出由一对交替的数字组成的最大子序列的长度。

> 由两个不同的数字 a 和 b 组成的交替的数字子序列可以表示为【abababababababababab”。

**示例:**

> **输入:** s = "1542745249842"
> **输出:** 6
> **解释:**
> 给定字符串中交替数字的最大子串为 424242。
> 
> **输入:** s = "1212312323232"
> **输出:** 9
> **解释:**
> 给定字符串中交替数字的最大子串为 2323232323232。

**方法:**字符串仅由十进制数字组成，即 0-9，因此可以检查序列是否存在由两个交替数字组成的所有可能的子序列。为此，请遵循以下方法:

*   使用从 0 到 9 的嵌套循环来选择有序的数字对。当数字为相同的**时，不遍历字符串。当数字**不同时，**则遍历字符串，并找到由出现交替数字的有序对的数字组成的子序列的长度。**
*   **如果**最大长度为 1** ，则意味着任何有序对中的第二个数字从未出现在给定序列中，从而使其成为单数字序列。这样的序列中所需的子序列类型将不存在，因此输出 0。**
*   **如果发现的最大长度**大于 1** ，这意味着在给定的序列中存在至少 2 个不同的数字，因此输出该发现的长度。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the length of the
// largest subsequence consisting of
// a pair of alternating digits
void largestSubsequence(string s)
{
    // Variable initialization
    int maxi = 0;
    char prev1;

    // Nested loops for iteration
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < 10; j++) {

            // Check if i is not equal to j
            if (i != j) {

                // Initialize length as 0
                int len = 0;
                prev1 = j + '0';

                // Iterate from 0 till the
                // size of the string
                for (int k = 0; k < s.size(); k++) {

                    if (s[k] == i + '0'
                        && prev1 == j + '0') {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                    else if (s[k] == j + '0'
                             && prev1 == i + '0') {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                }

                // Update maxi
                maxi = max(len, maxi);
            }
        }
    }

    // Check if maxi is not equal to
    // 1 the print it otherwise print 0
    if (maxi != 1)
        cout << maxi << endl;
    else
        cout << 0 << endl;
}

// Driver Code
int main()
{
    // Given string
    string s = "1542745249842";

    // Function call
    largestSubsequence(s);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the length of the
// largest subsequence consisting of
// a pair of alternating digits
static void largestSubsequence(char []s)
{
    // Variable initialization
    int maxi = 0;
    char prev1;

    // Nested loops for iteration
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {

            // Check if i is not equal to j
            if (i != j)
            {

                // Initialize length as 0
                int len = 0;
                prev1 = (char) (j + '0');

                // Iterate from 0 till the
                // size of the String
                for (int k = 0; k < s.length; k++)
                {
                    if (s[k] == i + '0' &&
                        prev1 == j + '0')
                    {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                    else if (s[k] == j + '0' &&
                             prev1 == i + '0')
                    {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                }

                // Update maxi
                maxi = Math.max(len, maxi);
            }
        }
    }

    // Check if maxi is not equal to
    // 1 the print it otherwise print 0
    if (maxi != 1)
        System.out.print(maxi + "\n");
    else
        System.out.print(0 + "\n");
}

// Driver Code
public static void main(String[] args)
{
    // Given String
    String s = "1542745249842";

    // Function call
    largestSubsequence(s.toCharArray());
}
}

// This code is contributed by Rohit_ranjan
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the length of the
# largest subsequence consisting of
# a pair of alternating digits
def largestSubsequence(s):

    # Variable initialization
    maxi = 0

    # Nested loops for iteration
    for i in range(10):
        for j in range(10):

            # Check if i is not equal to j
            if (i != j):

                # Initialize length as 0
                lenn = 0
                prev1 = chr(j + ord('0'))

                # Iterate from 0 till the
                # size of the string
                for k in range(len(s)):
                    if (s[k] == chr(i + ord('0')) and
                       prev1 == chr(j + ord('0'))):
                        prev1 = s[k]

                        # Increment length
                        lenn += 1

                    elif (s[k] == chr(j + ord('0')) and
                         prev1 == chr(i + ord('0'))):
                        prev1 = s[k]

                        # Increment length
                        lenn += 1

                # Update maxi
                maxi = max(lenn, maxi)

    # Check if maxi is not equal to
    # 1 the print otherwise pr0
    if (maxi != 1):
        print(maxi)
    else:
        print(0)

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "1542745249842"

    # Function call
    largestSubsequence(s)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
class GFG{

// Function to find the length of the
// largest subsequence consisting of
// a pair of alternating digits
static void largestSubsequence(char []s)
{
    // Variable initialization
    int maxi = 0;
    char prev1;

    // Nested loops for iteration
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < 10; j++)
        {

            // Check if i is not equal to j
            if (i != j)
            {

                // Initialize length as 0
                int len = 0;
                prev1 = (char) (j + '0');

                // Iterate from 0 till the
                // size of the String
                for (int k = 0; k < s.Length; k++)
                {
                    if (s[k] == i + '0' &&
                        prev1 == j + '0')
                    {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                    else if (s[k] == j + '0' &&
                             prev1 == i + '0')
                    {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                }

                // Update maxi
                maxi = Math.Max(len, maxi);
            }
        }
    }

    // Check if maxi is not equal to
    // 1 the print it otherwise print 0
    if (maxi != 1)
        Console.Write(maxi + "\n");
    else
        Console.Write(0 + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    // Given String
    String s = "1542745249842";

    // Function call
    largestSubsequence(s.ToCharArray());
}
}

// This code is contributed by Rohit_ranjan
```

## **java 描述语言**

```
<script>
// Js program for the above approach
// Function to find the length of the
// largest subsequence consisting of
// a pair of alternating digits
function largestSubsequence(s)
{
    // Variable initialization
    let maxi = 0;
    let prev1;

    // Nested loops for iteration
    for (let i = 0; i < 10; i++) {
        for (let j = 0; j < 10; j++) {

            // Check if i is not equal to j
            if (i != j) {

                // Initialize length as 0
                let len = 0;
                prev1 = String(j) ;

                // Iterate from 0 till the
                // size of the string
                for (let k = 0; k < s.length; k++) {
                    if (s[k] == String(i )
                        && prev1 == String(j)) {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                    else if (s[k] == String(j)
                             && prev1 == String(i)) {
                        prev1 = s[k];

                        // Increment length
                        len++;
                    }
                }

                // Update maxi
                maxi = Math.max(len, maxi);
            }
        }
    }

    // Check if maxi is not equal to
    // 1 the print it otherwise print 0
    if (maxi != 1)
        document.write( maxi ,'<br>');
    else
        document.write( 0 ,'<br>');
}

// Driver Code

    // Given string
    let s = "1542745249842";

    // Function call
    largestSubsequence(s);

// This code is contributed by rohitsingh07052.
</script>
```

****Output:** 

```
6
```** 

*****时间复杂度:**O(10 * 10 * N)*
T5**辅助空间:** O(1)**