# 计算使用给定单行键盘输入单词所需的时间

> 原文:[https://www . geesforgeks . org/calculate-使用给定单行键盘键入单词所需的时间/](https://www.geeksforgeeks.org/calculate-time-required-to-type-a-word-using-given-single-row-keyboard/)

给定一个大小为 **26** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **键盘布局**和一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **单词**，任务是计算输入单词所花费的总时间，从 **0 <sup>第</sup>** 键开始，如果移动到相邻的键需要单位时间。

**示例:**

> **输入:**Keyboardlayout =“abcdefghijklmnopqrstuvwxyz”， word = "dog"
> **输出:** 22
> **说明:**
> 按键‘d’需要 3 个时间单位(即‘a’->‘b’->‘c’->‘d’)
> 按键‘o’需要 11 个时间单位(即‘d’->‘e’->‘f’->‘g’->‘h
> 按键‘g’需要 8 个时间单位(即‘o’->‘n’->‘m’->‘l’->‘k’->‘j’->‘I’->‘h’->‘g’)
> 因此，所用总时间= 3 + 11 + 8 = 22。
> 
> **输入:**keyboardLayout = " abcdefghijklmnopqrstuvwxyz "，word = " abcdefghijklmnopqrstuvwxyz "
> **输出:** 25

**方法:**按照以下步骤解决问题:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如 **pos，**来存储所有字符的位置。
*   初始化两个变量，说**最后一个**，存储最后一次更新的索引，**结果，**存储输入单词的总时间。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)中的字符**单词**:
    *   初始化两个变量，说**目的地，**存储需要输入的下一个字符的索引，**距离**，存储该索引与当前索引的距离。
    *   将**距离**的值加到**结果**上。
    *   更新最后到**目的地**。
*   完成上述操作后，打印**结果的值。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate time
// taken to type the given word
int timeTakenToType(string& keyboardLayout,
                    string& word)
{
    // Stores position of characters
    vector<int> pos(26);

    // Iterate over the range [0, 26]
    for (int i = 0; i < 26; ++i) {

        // Set position of each character
        char ch = keyboardLayout[i];
        pos[ch - 'a'] = i;
    }

    // Store the last index
    int last = 0;

    // Stores the total time taken
    int result = 0;

    // Iterate over the characters of word
    for (int i = 0; i < (int)word.size(); ++i) {
        char ch = word[i];

        // Stores index of the next character
        int destination = pos[ch - 'a'];

        // Stores the distance of current
        // character from the next character
        int distance = abs(destination - last);

        // Update the result
        result += distance;

        // Update last position
        last = destination;
    }

    // Print the result
    cout << result;
}

// Driver Code
int main()
{
    // Given keyboard layout
    string keyboardLayout
        = "acdbefghijlkmnopqrtsuwvxyz";

    // Given word
    string word = "dog";

    // Function call to find the minimum
    // time required to type the word
    timeTakenToType(keyboardLayout, word);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

  // Function to calculate time
  // taken to type the given word
  static void timeTakenToType(String keyboardLayout,
                              String word)
  {

    // Stores position of characters
    int[] pos = new int[26];

    // Iterate over the range [0, 26]
    for (int i = 0; i < 26; i++) {

      // Set position of each character
      char ch = keyboardLayout.charAt(i);
      pos[ch - 'a'] = i;
    }

    // Store the last index
    int last = 0;

    // Stores the total time taken
    int result = 0;

    // Iterate over the characters of word
    for (int i = 0; i < word.length(); i++) {
      char ch = word.charAt(i);

      // Stores index of the next character
      int destination = pos[ch - 'a'];

      // Stores the distance of current
      // character from the next character
      int distance = Math.abs(destination - last);

      // Update the result
      result += distance;

      // Update last position
      last = destination;
    }

    System.out.println(result);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given keyboard layout
    String keyboardLayout
      = "acdbefghijlkmnopqrtsuwvxyz";

    // Given word
    String word = "dog";

    // Function call to find the minimum
    // time required to type the word
    timeTakenToType(keyboardLayout, word);
  }
}

// This code is contributed by aadityapburujwale.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate time
# taken to type the given word
def timeTakenToType(keyboardLayout, word):

    # Stores position of characters
    pos = [0]*(26)

    # Iterate over the range [0, 26]
    for i in range(26):

      # Set position of each character
        ch = keyboardLayout[i]
        pos[ord(ch) - ord('a')] = i

    # Store the last index
    last = 0

    # Stores the total time taken
    result = 0

    # Iterate over the characters of word
    for i in range(len(word)):
        ch = word[i]

        # Stores index of the next character
        destination = pos[ord(ch) - ord('a')]

        # Stores the distance of current
        # character from the next character
        distance = abs(destination - last)

        # Update the result
        result += distance

        # Update last position
        last = destination

    # Prthe result
    print (result)

# Driver Code
if __name__ == '__main__':

    # Given keyboard layout
    keyboardLayout = "acdbefghijlkmnopqrtsuwvxyz"

    # Given word
    word = "dog"

    # Function call to find the minimum
    # time required to type the word
    timeTakenToType(keyboardLayout, word)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

  // Function to calculate time
  // taken to type the given word
  static void timeTakenToType(String keyboardLayout,
                              String word)
  {

    // Stores position of characters
    int[] pos = new int[26];

    // Iterate over the range [0, 26]
    for (int i = 0; i < 26; i++) {

      // Set position of each character
      char ch = keyboardLayout[i];
      pos[ch - 'a'] = i;
    }

    // Store the last index
    int last = 0;

    // Stores the total time taken
    int result = 0;

    // Iterate over the characters of word
    for (int i = 0; i < word.Length; i++) {
      char ch = word[i];

      // Stores index of the next character
      int destination = pos[ch - 'a'];

      // Stores the distance of current
      // character from the next character
      int distance = Math.Abs(destination - last);

      // Update the result
      result += distance;

      // Update last position
      last = destination;
    }

    Console.WriteLine(result);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given keyboard layout
    String keyboardLayout
      = "acdbefghijlkmnopqrtsuwvxyz";

    // Given word
    String word = "dog";

    // Function call to find the minimum
    // time required to type the word
    timeTakenToType(keyboardLayout, word);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate time
// taken to type the given word
function timeTakenToType(keyboardLayout, word)
{

    // Stores position of characters
    var pos = Array(26).fill(0);

    // Iterate over the range [0, 26]
    for(var i = 0; i < 26; ++i)
    {

        // Set position of each character
        var ch = keyboardLayout[i];
        pos[ch.charCodeAt(0) -
           'a'.charCodeAt(0)] = i;
    }

    // Store the last index
    var last = 0;

    // Stores the total time taken
    var result = 0;

    // Iterate over the characters of word
    for(var i = 0; i < word.length; ++i)
    {
        var ch = word[i];

        // Stores index of the next character
        var destination = pos[ch.charCodeAt(0) -
                             'a'.charCodeAt(0)];

        // Stores the distance of current
        // character from the next character
        var distance = Math.abs(destination - last);

        // Update the result
        result += distance;

        // Update last position
        last = destination;
    }

    // Print the result
    document.write(result);
}

// Driver Code

// Given keyboard layout
var keyboardLayout = "acdbefghijlkmnopqrtsuwvxyz";

// Given word
var word = "dog";

// Function call to find the minimum
// time required to type the word
timeTakenToType(keyboardLayout, word);

// This code is contributed by rutvik_56

</script>
```

**Output**

```
22
```

***时间复杂度:** O(N)，其中 N 是字符串单词的大小。*
***辅助空间:** O(1)*