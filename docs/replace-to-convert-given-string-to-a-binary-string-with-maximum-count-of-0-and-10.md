# 替换“？”将给定字符串转换为最大计数为“0”和“10”的二进制字符串

> 原文:[https://www . geesforgeks . org/replace-to-convert-给定字符串到二进制字符串的最大计数为 0 和 10/](https://www.geeksforgeeks.org/replace-to-convert-given-string-to-a-binary-string-with-maximum-count-of-0-and-10/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，由三种不同类型的字符**“0”**、**“1”**和**“？”**，任务是通过替换**“？”将给定字符串转换为二进制字符串**带有**“0”**或**“1”**的字符，使得二进制字符串中 **0** s 和 **10** 的计数最大。

**示例:**

> **输入:** str = 10？0?11
> **输出:** 1000011
> **说明:**
> 替换 str[2] = '0 '，str[4] = '0 '修改 string str = "1000011 "。
> 字符串中 0 的计数是 4，字符串 1 中 10 的计数是从给定字符串获得的最大可能计数。
> 
> **输入:** str = 1？1?
> T3【输出: 1010

**方法:**想法是利用替换**“？”**字符加上**‘0’**字符总是最大化 **0** 和 **10** 的计数。以下是观察结果:

> 如果字符**“？”**后面跟着**“0”**，然后替换字符**“？”**至**“0”**如果字符**“1”**后面跟有**“？”**然后替换字符**“？”**至“0”增加 **0** s 和 **10** 的计数。

按照以下步骤解决问题:

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并检查当前字符是否为**“？”**还是不行。如果发现为真，则将当前字符替换为**‘0’**。
*   最后，打印字符串。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maximize count of 0 and 10
// by replacing character '?' to '0' or '1'
void findMaxOccurence(string str, int N)
{
    // Traverse the given string
    for (int i = 0; i < N; i++) {

        // If current character
        // is '?'
        if (str[i] == '?') {

            // Replace str[i] to '0'
            str[i] = '0';
         }
    }
    cout << str <<endl;

}

// Driver Code
int main()
{
    //Given string
    string str = "10?0?11";

    int N = str.length();

    findMaxOccurence(str,N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

  // Function to maximize count of 0 and 10
  // by replacing character '?' to '0' or '1'
  static void findMaxOccurence(char[] str, int N)
  {
    // Traverse the given String
    for (int i = 0; i < N; i++)
    {

      // If current character
      // is '?'
      if (str[i] == '?')
      {

        // Replace str[i] to '0'
        str[i] = '0';
      }
    }
    System.out.print(str);

  }

  // Driver Code
  public static void main(String[] args)
  {
    // Given String
    String str = "10?0?11";
    int N = str.length();
    findMaxOccurence(str.toCharArray(),N);
  }
}

// This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to maximize count of 0 and 10
  // by replacing character '?' to '0' or '1'
  static void findMaxOccurence(char[] str, int N)
  {

    // Traverse the given String
    for (int i = 0; i < N; i++)
    {

      // If current character
      // is '?'
      if (str[i] == '?')
      {

        // Replace str[i] to '0'
        str[i] = '0';
      }
    }
    Console.Write(str);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given String
    String str = "10?0?11";
    int N = str.Length;
    findMaxOccurence(str.ToCharArray(),N);
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to maximize count of 0 and 10
# by replacing character '?' to '0' or '1'
def findMaxOccurence(str, N) :

    # Traverse the given String
    for i in range(N) :

        # If current character
        # is '?'
        if (str[i] == '?') :

            # Replace str[i] to '0'
            str[i] = '0'       
    print("".join(str))

# Driver Code

# Given String
str = list("10?0?11")
N = len(str)
findMaxOccurence(str, N)

# This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to maximize count of 0 and 10
// by replacing character '?' to '0' or '1'
function findMaxOccurence(str, N)
{
    // Traverse the given string
    for (var i = 0; i < N; i++) {

        // If current character
        // is '?'
        if (str[i] == '?') {

            // Replace str[i] to '0'
            str[i] = '0';
        }
    }
    document.write(str.join(''));

}

// Driver Code
//Given string
var str = "10?0?11".split('');

var N = str.length;

findMaxOccurence(str,N);

</script>
```

**Output:** 

```
1000011
```

***时间复杂度:** O(N)，其中 N 为弦的长度*
***辅助空间:** O(1)*