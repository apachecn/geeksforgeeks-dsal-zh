# 在 O(1)空间找到字符串中的重复字符

> 原文:[https://www . geesforgeks . org/find-the-reply-characters-in-string-in-O1-space/](https://www.geeksforgeeks.org/find-the-duplicate-characters-in-a-string-in-o1-space/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是在不使用任何额外数据结构的情况下，按照字典顺序查找给定字符串中存在的所有重复字符。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:** e g k s
> **解释:**
> 字符' g '的频率= 2
> 字符' e '的频率= 4
> 字符' k '的频率= 2
> 字符' s '的频率= 2
> 因此，需要的输出为**e k s**。
> 
> **输入:** str = "apple"
> **输出:** p
> **解释:**
> 字符' p' = 2 的频率。
> 所以需要的输出是 **p** 。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，先说**第一个**，其中**第一个**的 **i <sup>第</sup>T5 位检查字符串中的字符**(I+‘a’)**是否至少出现一次。**
*   初始化一个变量，比如第二个，其中**第二个**的**I<sup>th</sup>T3】位检查字符串中的字符**(I+‘a’)**是否至少出现两次。**
*   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。对于每一个**I<sup>th</sup>T5【字符，检查字符串中是否已经出现**str【I】**。如果发现为真，则[设置**第二**](https://www.geeksforgeeks.org/set-k-th-bit-given-number/) 的**(str[I]–‘a’)<sup>第</sup>** 位。**
*   否则，[设置**(str[I]–‘a’)<sup>第</sup>** 位的**第**](https://www.geeksforgeeks.org/set-k-th-bit-given-number/) 。
*   最后，遍历**【0，25】**和[范围，检查**第一位**和**第二位**的 **i <sup>第</sup>** 位是否都已设置](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)。如果发现为真，则打印 **(i + 'a')** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find duplicate characters
// in string without using any additional
// data structure
void findDuplicate(string str, int N)
{

    // Check if (i + 'a') is present
    // in str at least once or not.
    int first = 0;

    // Check if (i + 'a') is present
    // in str at least twice or not.
    int second = 0;

    // Iterate over the characters
    // of the string str
    for (int i = 0; i < N; i++) {

        // If str[i] has already occurred in str
        if (first & (1 << (str[i] - 'a'))) {

            // Set (str[i] - 'a')-th bit of second
            second
                = second | (1 << (str[i] - 'a'));
        }
        else {

            // Set (str[i] - 'a')-th bit of second
            first
                = first | (1 << (str[i] - 'a'));
        }
    }

    // Iterate over the range [0, 25]
    for (int i = 0; i < 26; i++) {

        // If i-th bit of both first
        // and second is Set
        if ((first & (1 << i))
            && (second & (1 << i))) {

            cout << char(i + 'a') << " ";
        }
    }
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";
    int N = str.length();

    findDuplicate(str, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

  // Function to find duplicate characters
  // in string without using any additional
  // data structure
  static void findDuplicate(String str, int N)
  {

    // Check if (i + 'a') is present
    // in str at least once or not.
    int first = 0;

    // Check if (i + 'a') is present
    // in str at least twice or not.
    int second = 0;

    // Iterate over the characters
    // of the string str
    for (int i = 0; i < N; i++)
    {

      // If str[i] has already occurred in str
      if ((first & (1 << (str.charAt(i) - 'a'))) != 0)
      {

        // Set (str[i] - 'a')-th bit of second
        second
          = second | (1 << (str.charAt(i) - 'a'));
      }
      else
      {

        // Set (str[i] - 'a')-th bit of second
        first
          = first | (1 << (str.charAt(i) - 'a'));
      }
    }

    // Iterate over the range [0, 25]
    for (int i = 0; i < 26; i++)
    {

      // If i-th bit of both first
      // and second is Set
      if (((first & (1 << i))
           & (second & (1 << i))) != 0) {

        System.out.print((char)(i + 'a') + " ");
      }
    }
  }

  // Driver Code
  static public void main(String args[])
  {
    String str = "geeksforgeeks";
    int N = str.length();

    findDuplicate(str, N);
  }
}

// This code is contributed by AnkThon.
```

## 蟒蛇 3

```
# Python 3 code added. program to implement
# the above approach

# Function to find duplicate characters
# in str1ing without using any additional
# data str1ucture
def findDuplicate(str1, N):

    # Check if (i + 'a') is present
    # in str1 at least once or not.
    first = 0

    # Check if (i + 'a') is present
    # in str1 at least twice or not.
    second = 0

    # Iterate over the characters
    # of the str1ing str1
    for i in range(N):

        # If str1[i] has already occurred in str1
        if (first & (1 << (ord(str1[i]) - 97))):

            # Set (str1[i] - 'a')-th bit of second
            second = second | (1 << (ord(str1[i]) - 97))
        else:
            # Set (str1[i] - 'a')-th bit of second
            first = first | (1 << (ord(str1[i]) - 97))

    # Iterate over the range [0, 25]
    for i in range(26):

        # If i-th bit of both first
        # and second is Set
        if ((first & (1 << i)) and (second & (1 << i))):
            print(chr(i + 97), end = " ")

# Driver Code
if __name__ == '__main__':
    str1 = "geeksforgeeks"
    N = len(str1)
    findDuplicate(str1, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find duplicate characters
  // in string without using any additional
  // data structure
  static void findDuplicate(string str, int N)
  {

    // Check if (i + 'a') is present
    // in str at least once or not.
    int first = 0;

    // Check if (i + 'a') is present
    // in str at least twice or not.
    int second = 0;

    // Iterate over the characters
    // of the string str
    for (int i = 0; i < N; i++) {

      // If str[i] has already occurred in str
      if ((first & (1 << (str[i] - 'a'))) != 0)
      {

        // Set (str[i] - 'a')-th bit of second
        second
          = second | (1 << (str[i] - 'a'));
      }
      else
      {

        // Set (str[i] - 'a')-th bit of second
        first
          = first | (1 << (str[i] - 'a'));
      }
    }

    // Iterate over the range [0, 25]
    for (int i = 0; i < 26; i++)
    {

      // If i-th bit of both first
      // and second is Set
      if (((first & (1 << i))
           & (second & (1 << i))) != 0) {

        Console.Write((char)(i + 'a') + " ");
      }
    }
  }

  // Driver Code
  static public void Main()
  {
    string str = "geeksforgeeks";
    int N = str.Length;

    findDuplicate(str, N);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find duplicate characters
// in string without using any additional
// data structure
function findDuplicate(str, N)
{

    // Check if (i + 'a') is present
    // in str at least once or not.
    let first = 0;

    // Check if (i + 'a') is present
    // in str at least twice or not.
    let second = 0;

    // Iterate over the characters
    // of the string str
    for(let i = 0; i < N; i++)
    {

        // If str[i] has already occurred in str
        if ((first & (1 << (str[i].charCodeAt() -
                               'a'.charCodeAt()))) != 0)
        {

            // Set (str[i] - 'a')-th bit of second
            second = second | (1 << (str[i].charCodeAt() -
                                        'a'.charCodeAt()));
        }
        else
        {

            // Set (str[i] - 'a')-th bit of second
            first = first | (1 << (str[i].charCodeAt() -
                                      'a'.charCodeAt()));
        }
    }

    // Iterate over the range [0, 25]
    for(let i = 0; i < 26; i++)
    {

        // If i-th bit of both first
        // and second is Set
        if (((first & (1 << i)) &
            (second & (1 << i))) != 0)
        {
            document.write(String.fromCharCode(
                i + 'a'.charCodeAt()) + " ");
        }
    }
}

// Driver code
let str = "geeksforgeeks";
let N = str.length;

findDuplicate(str, N);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
e g k s
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)