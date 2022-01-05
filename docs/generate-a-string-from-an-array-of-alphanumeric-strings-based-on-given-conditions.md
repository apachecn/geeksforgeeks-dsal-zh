# 根据给定条件从字母数字字符串数组中生成字符串

> 原文:[https://www . geesforgeks . org/基于给定条件从字母数字字符串数组生成字符串/](https://www.geeksforgeeks.org/generate-a-string-from-an-array-of-alphanumeric-strings-based-on-given-conditions/)

给定一个字符串数组 **arr[]** ，其中每个字符串的形式为**“名称:数字”**和一个字符 **T** 作为输入，任务是基于以下条件生成一个新字符串:

*   在每个字符串中找到**“数字”**中小于或等于字符串长度**“名称”**的最大数字。
*   如果获得了任何这样的数字 **d** ，那么将字符串**名称**的索引 **d** 处的字符追加到输出字符串中。否则，在输出字符串中添加字符 **T** 。

**示例:**

> **输入:**arr[]= {“Robert:36787”、“Tina:68721”、“Jo:56389”}，T = 'X'
> **输出:** tiX
> **解释:**
> 对于第一个字符串“Robert:36787”:长度“Robert”为 6。由于字符串“36787”中存在 6，因此答案后会附加“罗伯特”的第 6 个<sup>字符，即 t。
> 对于第二个字符串“Tina:68721”:“Tina”的长度为 4。“68721”中出现的小于或等于 4 的最高数字是 2。因此，“Tina”的第二个字符，即，被附加到答案中。
> 对于第三个字符串“Jo:56389”:“Jo”的长度为 2。由于“56389”中不存在小于或等于 2 的数字，因此答案后会附加一个 T( = 'X ')。
> 因此，上述操作后的最终字符串为“tiX”。
> **输入:** arr[] = {“极客:89167”、“gfg:68795”}，T = 'X'
> **输出:** GX
> **解释:**
> 对于第一个字符串“极客:89167”，“极客”的长度= 5，“89167”的数字有小于 5 的数字 1。
> 因此，结果字符串将在名称的第一个位置有字符，即“G”。
> 对于第二个字符串“gfg:68795”，长度“gfg”= 3，“68795”没有小于等于 3 的数字。
> 因此，结果字符串将具有字符 t。
> 因此，上述操作之后的最终字符串是“GX”。</sup>

**方法:**要解决问题，请按照下面给出的步骤操作:

1.  遍历字符串数组，[在“ **:** 周围拆分每一个字符串](https://www.geeksforgeeks.org/how-to-split-a-string-in-cc-python-and-java/)。第一部分包含名称，第二部分包含编号。
2.  将**名称**的长度存储在一个变量中，找到小于或等于**数字**长度的最大数字。
3.  如果找到任何这样的数字，提取名称为的**索引处的字符，并附加到结果字符串中。否则，将 **T** 追加到结果字符串中。**
4.  对数组中的所有字符串重复上述操作后，打印结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include<bits/stdc++.h>
using namespace std;

// Function to generate required string
string generatePassword(vector<string>arr,
                        char T)
{
  // To store the result
  string result;
  for (auto s:arr)
  {
    // Split name and number
    int index;

    for(int i = 0; i < s.size(); i++)
    {
      if(s[i] == ':')
      {
        index = i;
        break;
      }
    }

    string name = s.substr(0, index);
    string number = s.substr(index + 1,
                             s.size() -
                             index - 1);
    int n = name.length();

    // Stores the maximum number
    // less than or equal to the
    // length of name
    int max = 0;

    for (int i = 0; i < number.length(); i++)
    {
      // Check for number by parsing
      // it to integer if it is greater
      // than max number so far
      int temp = number[i] - '0';

      if (temp > max && temp <= n)
        max = temp;
    }

    // Check if no such number is
    // found then we append X
    // to the result.
    if (max == 0)
      result.push_back(T);

    // Otherwise
    else

      // Append max index
      // of the name
      result.push_back(name[max - 1]);
  }

  // Return the final string
  return result;
}

// Driver Code
int main()
{
  vector<string>arr = {"Geeks:89167",
                       "gfg:68795"};
  char T = 'X';

  // Function Call
  cout << (generatePassword(arr, T));
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to generate required string
    public static String
    generatePassword(String s[], char T)
    {
        // To store the result
        StringBuilder result
            = new StringBuilder();

        for (String currentString : s) {

            // Split name and number
            String person[]
                = currentString.split(":");
            String name = person[0];
            String number = person[1];

            int n = name.length();

            // Stores the maximum number
            // less than or equal to the
            // length of name
            int max = 0;

            for (int i = 0;
                 i < number.length(); i++) {

                // Check for number by parsing
                // it to integer if it is greater
                // than max number so far
                int temp = Integer.parseInt(
                    String.valueOf(number.charAt(i)));

                if (temp > max && temp <= n)
                    max = temp;
            }

            // Check if no such number is
            // found then we append X
            // to the result.
            if (max == 0)
                result.append(T);

            // Otherwise
            else

                // Append max index
                // of the name
                result.append(
                    String.valueOf(
                        name.charAt(max - 1)));
        }

        // Return the final string
        return result.toString();
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        String arr[] = { "Geeks:89167",
                         "gfg:68795" };
        char T = 'X';

        // Function Call
        System.out.println(
            generatePassword(arr, T));
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to generate
# required string
def generatePassword(s, T):

    # To store the result
    result = []

    for currentString in s:

        # Split name and number
        person = currentString.split(":")
        name = person[0]
        number = person[1]
        n = len(name)

        # Stores the maximum number
        # less than or equal to the
        # length of name
        max = 0

        for i in range(len(number)):

            # Check for number by parsing
            # it to integer if it is greater
            # than max number so far
            temp = int(number[i])

            if(temp > max and temp <= n):
                max = temp

        # Check if no such number is
        # found then we append X
        # to the result.
        if max == 0:
            result.append(T)

        # Otherwise
        else:

            # Append max index
            # of the name
            result.append(name[max - 1])

    # Return the
    # final string
    return result

# Driver Code
arr = ["Geeks:89167","gfg:68795"]
T = 'X'

# Function call
print(*generatePassword(arr, T),
       sep = "")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Text;
class GFG{

// Function to generate required string
public static String generatePassword(String []s,
                                      char T)
{
    // To store the result
    StringBuilder result = new StringBuilder();
    foreach (String currentString in s)
    {
        // Split name and number
        String []person = currentString.Split(':');
        String name = person[0];
        String number = person[1];

        int n = name.Length;

        // Stores the maximum number
        // less than or equal to the
        // length of name
        int max = 0;

        for (int i = 0; i < number.Length; i++)
        {
            // Check for number by parsing
            // it to integer if it is greater
            // than max number so far
            int temp = Int32.Parse(String.Join("",
                                   number[i]));
            if (temp > max && temp <= n)
                max = temp;
        }

        // Check if no such number is
        // found then we append X
        // to the result.
        if (max == 0)
            result.Append(T);

        // Otherwise
        else

            // Append max index
            // of the name
            result.Append(String.Join("",
                          name[max - 1]));
    }

    // Return the readonly string
    return result.ToString();
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = {"Geeks:89167",
                    "gfg:68795"};
    char T = 'X';

    // Function Call
    Console.WriteLine(generatePassword(arr, T));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to generate required string
      function generatePassword(s, T) {
        // To store the result
        var result = [];

        for (const currentString of s) {
          // Split name and number
          var person = currentString.split(":");
          var name = person[0];
          var number = person[1];

          var n = name.length;

          // Stores the maximum number
          // less than or equal to the
          // length of name
          var max = 0;

          for (var i = 0; i < number.length; i++) {
            // Check for number by parsing
            // it to integer if it is greater
            // than max number so far
            var temp = parseInt(number[i]);
            if (temp > max && temp <= n) max = temp;
          }

          // Check if no such number is
          // found then we append X
          // to the result.
          if (max === 0) result.push(T);
          // Otherwise
          // Append max index
          // of the name
          else result.push(name[max - 1]);
        }

        // Return the readonly string
        return result.join("");
      }

      // Driver Code
      var arr = ["Geeks:89167", "gfg:68795"];
      var T = "X";

      // Function Call
      document.write(generatePassword(arr, T) + "<br>");

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
GX
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*