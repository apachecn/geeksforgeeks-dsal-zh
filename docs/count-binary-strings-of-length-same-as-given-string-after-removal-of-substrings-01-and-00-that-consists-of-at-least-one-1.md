# 在删除至少包含一个‘1’的子字符串“01”和“00”后，对长度与给定字符串相同的二进制字符串进行计数

> 原文:[https://www . geeksforgeeks . org/count-二进制-长度与给定字符串相同-移除子字符串后-01 和-00-由至少一个-1 组成/](https://www.geeksforgeeks.org/count-binary-strings-of-length-same-as-given-string-after-removal-of-substrings-01-and-00-that-consists-of-at-least-one-1/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是在从给定字符串中重复删除所有出现的子字符串**【10】**和**【00】**后，计算由至少一个长度等于给定字符串长度的**【1】**组成的总二进制字符串。

**示例:**

> **输入:** S = "111"
> **输出:** 7
> **说明:**由于给定字符串中没有出现“10”或“01”，所以剩余字符串的长度为 3。由至少一个设置位组成的长度为 3 的所有可能的二进制字符串为{“001”、“010”、“011”、“100”、“101”、“110”、“111”}
> 
> **输入:**S =“0101”
> T3】输出: 3
> **说明:**删除“10”后，S =“01”。因此，剩余字符串的长度为 2。由至少一个设置位组成的长度为 2 的字符串为{“01”、“10”、“11”}

**方法:**思路是在去掉表单的所有子串**“10”**和**“00”**后，计算给定字符串的[长度。考虑剩下的；字符串长度为 **N** ，由至少一个设定位组成的字符串总数将等于 **2 <sup>N</sup> -1** 。](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)

按照以下步骤解决问题:

1.  初始化一个变量，说**计数**。
2.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 的字符。每个字符检查是否为 **'0'** ，**计数**是否大于 **0** 。如果发现为真，则按 **1** 递减计数。
3.  否则，如果当前字符为**‘1’**，则按 **1** 递增**计数**。
4.  完成字符串遍历后，打印 **2 <sup>计数</sup>–1**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the strings
// consisting of at least 1 set bit
void countString(string S)
{
    // Initialize count
    long long count = 0;

    // Iterate through string
    for (auto it : S) {

        if (it == '0' and count > 0) {
            count--;
        }
        else {
            count++;
        }
    }

    // The answer is 2^N-1
    cout << ((1 << count) - 1) << "\n";
}

// Driver Code
int main()
{

    // Given string
    string S = "1001";

    // Function call
    countString(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the strings
// consisting of at least 1 set bit
static void countString(String S)
{

    // Initialize count
    int count = 0;

    // Iterate through string
    for(char it : S.toCharArray())
    {
        if (it == '0' && count > 0)
        {
            count--;
        }
        else
        {
            count++;
        }
    }

    // The answer is 2^N-1
    System.out.print((1 << count) - 1);
}

// Driver Code
public static void main(String[] args)
{

    // Given string
    String S = "1001";

    // Function call
    countString(S);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the
# above approach 

# Function to count the
# strings consisting of
# at least 1 set bit
def countString(S):

    # Initialize count
    count = 0

    # Iterate through
    # string
    for i in S:
        if (i == '0' and
            count > 0):           
            count -= 1

        else:           
            count += 1

    # The answer is 2^N-1    
    print((1 << count) - 1) 

# Driver Code
if __name__ == "__main__":

    # Given string   
    S = "1001"

    # Function call   
    countString(S)

# This code is contributed by Virusbuddah_
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the strings
// consisting of at least 1 set bit
static void countString(string S)
{

    // Initialize count
    int count = 0;

    // Iterate through string
    foreach(char it in S)
    {
        if (it == '0' && count > 0)
        {
            count--;
        }
        else
        {
            count++;
        }
    }

    // The answer is 2^N-1
    Console.Write((1 << count) - 1);
}

// Driver Code
public static void Main(string[] args)
{

    // Given string
    string S = "1001";

    // Function call
    countString(S);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to count the strings
    // consisting of at least 1 set bit
    function countString( S) {

        // Initialize count
        var count = 0;

        // Iterate through string
        for (var it =0;it< S.length; it++) {
            if (S[it] == '0' && count > 0) {
                count--;
            } else {
                count++;
            }
        }

        // The answer is 2^N-1
        document.write((1 << count) - 1);
    }

    // Driver Code

        // Given string
        var S = "1001";

        // Function call
        countString(S);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(L)其中 L 是字符串的长度。*
***辅助空间:** O(1)*