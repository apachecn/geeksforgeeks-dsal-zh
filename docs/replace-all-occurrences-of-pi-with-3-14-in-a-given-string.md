# 在给定的字符串中用 3.14 替换圆周率的所有出现

> 原文:[https://www . geesforgeks . org/用给定字符串中的 3-14 替换所有出现的 pi/](https://www.geeksforgeeks.org/replace-all-occurrences-of-pi-with-3-14-in-a-given-string/)

给定一个字符串，任务是用给定字符串中的 3.14 替换 pi 的所有出现。
**例** :

```
Input : str = "2 * pi + 3 * pi = 5 * pi"
Output : 2 * 3.14 + 3 * 3.14 = 5 * 3.14

Input : str = "pippppiiiipi"
Output : 3.14ppp3.14iii3.14

Input : str = "xpix"
Output : x3.14x
```

**进场 1:**

1.  创建一个空输出字符串。
2.  从第 0 个索引到第二个索引遍历字符串，因为 pi 的长度是 2。
3.  如果当前和(当前+1)<sup>索引处的字母组成单词“pi”，则在输出字符串中添加“3.14”。</sup>
4.  否则在当前索引处追加字母表。

以下是上述方法的实现:

## C++

```
// C++ program to replace all
// pi in a given string with 3.14

#include <bits/stdc++.h>
using namespace std;

// Function to replace all occurrences
// of pi in a given with 3.14
string replacePi(string input)
{
    string output;

    int size = input.length();

    // Iterate through second last
    // element of the string
    for (int i = 0; i < size; ++i) {

        // If current and current +1 alphabets
        // form the word 'pi'
        // append 3.14 to output
        if (i + 1 < size and input[i] == 'p' and input[i + 1] == 'i') {
            output += "3.14";
            i++;
        }

        // Append the current letter
        else {
            output += input[i];
        }
    }

    // Return the output string
    return output;
}

// Driver Code
int main()
{
    string input = "2 * pi + 3 * pi = 5 * pi";
    cout << replacePi(input);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace all
// pi in a given String with 3.14

class GFG {

    // Function to replace all occurrences
    // of pi in a given with 3.14
    public String replacePi(String input)
    {
        String output = "";

        int size = input.length();

        // Iterate through second last
        // element of the String
        for (int i = 0; i < size; ++i) {
            // If current and current +1 alphabets
            // form the word 'pi'
            // append 3.14 to output
            if (i + 1 < size && input.charAt(i) == 'p' && input.charAt(i + 1) == 'i') {
                output += "3.14";
                i++;
            }

            // Append the current letter
            else {
                output += input.charAt(i);
            }
        }

        // Return the output String
        return output;
    }

    // Driver Code
    public static void main(String args[])
    {
        GFG g = new GFG();
        String input = "2 * pi + 3 * pi = 5 * pi";
        System.out.println(g.replacePi(input));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to replace all
# pi in a given string with 3.14

# Function to replace all occurrences
# of pi in a given with 3.14
def replacePi(input):
    output ="";

    size = len(input);

    # Iterate through second last
    # element of the string
    for i in range(size):

        # If current and current + 1 alphabets
        # form the word 'pi'
        # append 3.14 to output
        if (i + 1 < size and input[i] == 'p' and
                            input[i + 1] == 'i'):
            output += "3.14";
            i+= 1;

        # Append the current letter
        else:
            output += input[i];
    # Return the output string
    return output;

# Driver Code
input = "2 * pi + 3 * pi = 5 * pi";
print(replacePi(input));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to replace all
// pi in a given string with 3.14

using System;
// Function to replace all occurrences
// of pi in a given with 3.14
class gfg {
    public string replacePi(string input)
    {
        string output = "";

        int size = input.Length;

        // Iterate through second last
        // element of the string
        for (int i = 0; i < size; ++i) {
            // If current and current +1 alphabets
            // form the word 'pi'
            // append 3.14 to output
            if (i + 1 < size && input[i] == 'p' && input[i + 1] == 'i') {
                output += "3.14";
                i++;
            }

            // Append the current letter
            else {
                output += input[i];
            }
        }

        // Return the output string
        return output;
    }
}

// Driver Code
class geek {
    public static int Main()
    {
        gfg g = new gfg();
        string input = "2 * pi + 3 * pi = 5 * pi";
        Console.WriteLine(g.replacePi(input));
        return 0;
    }
}
// This code is contributed by Soumik
```

## java 描述语言

```
<script>

      // JavaScript program to replace all
      // pi in a given string with 3.14

      // Function to replace all occurrences
      // of pi in a given with 3.14
      function replacePi(input) {
        var output = "";

        var size = input.length;

        // Iterate through second last
        // element of the string
        for (var i = 0; i < size; ++i) {
          // If current and current +1 alphabets
          // form the word 'pi'
          // append 3.14 to output
          if (i + 1 < size && input[i] === "p"
          && input[i + 1] === "i")
          {
            output += "3.14";
            i++;
          }

          // Append the current letter
          else {
            output += input[i];
          }
        }

        // Return the output string
        return output;
      }

      // Driver Code
      var input = "2 * pi + 3 * pi = 5 * pi";
      document.write(replacePi(input));

</script>
```

**Output:** 

```
2 * 3.14 + 3 * 3.14 = 5 * 3.14
```

**时间复杂度** : O(N)，其中 N 为给定字符串的长度。
**方法 2:(在 Java 中)**
要将所有 PI 事件替换为 3.14，请使用 Java String 类的 replace all()方法。

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class ReplacePI {
    public static void main(String[] args)
    {
        // Declare a String
        String expression = "2 * pi + 3 * pi = 5 * pi";

        // Call replaceAll() method to replace PI to 3.14
        expression = expression.replaceAll("pi", "3.14");

        // Print the result
        System.out.println(expression);
    }
}
```

**Output:** 

```
2 * 3.14 + 3 * 3.14 = 5 * 3.14
```