# 检查每个单词的字符是否可以重新排列以形成算术级数(AP)

> 原文:[https://www . geeksforgeeks . org/check-如果每个单词的字符可以重新排列以形成算术级数-ap/](https://www.geeksforgeeks.org/check-if-characters-of-each-word-can-be-rearranged-to-form-an-arithmetic-progression-ap/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是检查是否有可能重新排列字符串，使得给定字符串的每个单词的字符都在[算术级数](https://www.geeksforgeeks.org/arithmetic-progression/)中。

**示例:**

> **输入:** str = "ace yzx fbd"
> **输出:**真
> 说明:给定字符串重新排列为“ace xyz bdf”。
> ace 这个词的所有字符都在 AP 中，共同的区别是 2。
> 单词“xyz”的所有字符都在 AP 中，共有差异为 1
> 单词“bdf”的所有字符都在 AP 中，共有差异为 2。
> 因此，要求的输出为真。
> 
> **输入:** str = "极客换极客"
> T3】输出:假

**方法:**思路是[对给定字符串](https://www.geeksforgeeks.org/python-sort-words-sentence-ascending-order/)的每个单词进行排序，检查所有单词中相邻字符之间的差异是否相等。如果发现是真的，那么打印**是**。否则，打印**否**。按照以下步骤解决问题。

1.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **字符串**，[用空格分隔符分隔**字符串**的每个单词](https://www.geeksforgeeks.org/python-spilt-a-sentence-into-list-of-words/)。
2.  [给定字符串的每个单词按升序排序](https://www.geeksforgeeks.org/python-sort-words-sentence-ascending-order/)。
3.  检查单词的所有相邻字符之间的差异是否相等。
4.  如果发现是真的，打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check str can be
// rearranged such that characters
// of each word forms an AP

int checkWordAP(string str)
{
    // Stores the string
    // in stringstream
    stringstream ss(str);

    // Stores each word of
    // the given string
    string temp;
    while (getline(ss, temp, ' ')) {
        // Sort the current word
        sort(temp.begin(), temp.end());

        // Check if the current word
        // of the given string is in AP
        for (int i = 2; i < temp.length();
             i++) {
            // Store the value of difference
            // between adjacent characters
            int diff = temp[1] - temp[0];

            // Check if difference between all
            // adjacent characters are equal
            if (diff != temp[i] - temp[i - 1]) {
                return false;
            }
        }
    }

    // If all words are in AP.
    return true;
}

// Driver Code
int main()
{
    string str = "ace yzx fbd";

    // If all words of the given
    // string are in AP
    if (checkWordAP(str)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to check str can be
// rearranged such that characters
// of each word forms an AP
static boolean checkWordAP(String s)
{
  // Stores the String
  // in Stringstream
  String str[] = s.split(" ");

  // Stores each word of
  // the given String

  for (String temp : str )
  {
    // Sort the current word
    temp = sort(temp);

    // Check if the current word
    // of the given String is in AP
    for (int i = 2; i < temp.length(); i++)
    {
      // Store the value of difference
      // between adjacent characters
      int diff = temp.charAt(1) - temp.charAt(0);

      // Check if difference between all
      // adjacent characters are equal
      if (diff != temp.charAt(i) - temp.charAt(i - 1))
      {
        return false;
      }
    }
  }

  // If all words are in AP.
  return true;
}

static String sort(String inputString)
{
  // convert input string to char array
  char tempArray[] = inputString.toCharArray();

  // sort tempArray
  Arrays.sort(tempArray);

  // return new sorted string
  return new String(tempArray);
}

// Driver Code
public static void main(String[] args)
{
  String str = "ace yzx fbd";

  // If all words of the given
  // String are in AP
  if (checkWordAP(str))
  {
    System.out.print("Yes");
  }
  else
  {
    System.out.print("No");
  }
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check st can be
# rearranged such that characters
# of each word forms an AP
def checkWordAP(st):

    # Stores each word of
    # the given sting
    st = st.split(" ")

    for temp in st:

        # Sort the current word
        temp = sorted(temp)

        # Check if the current word
        # of the given is in AP
        for i in range(2, len(temp)):

            # Store the value of difference
            # between adjacent characters
            diff = ord(temp[1]) - ord(temp[0])

            # Check if difference between all
            # adjacent characters are equal
            if (diff != ord(temp[i]) -
                        ord(temp[i - 1])):
                return False

    # If all words are in AP.
    return True

# Driver Code
if __name__ == '__main__':

    st = "ace yzx fbd"

    # If all words of the given
    # are in AP
    if (checkWordAP(st)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to check str can be
// rearranged such that characters
// of each word forms an AP
static bool checkWordAP(String s)
{
  // Stores the String
  // in Stringstream
  String []str = s.Split(' ');

  // Stores each word of
  // the given String
  String temp = "";
  foreach (String temp1 in str )
  {
    // Sort the current word
    temp = sort(temp1);

    // Check if the current word
    // of the given String is in AP
    for (int i = 2; i < temp.Length; i++)
    {
      // Store the value of difference
      // between adjacent characters
      int diff = temp[1] - temp[0];

      // Check if difference between all
      // adjacent characters are equal
      if (diff != temp[i] - temp[i - 1])
      {
        return false;
      }
    }
  }

  // If all words are in AP.
  return true;
}

static String sort(String inputString)
{
  // convert input string to char array
  char []tempArray = inputString.ToCharArray();

  // sort tempArray
  Array.Sort(tempArray);

  // return new sorted string
  return new String(tempArray);
}

// Driver Code
public static void Main(String[] args)
{
  String str = "ace yzx fbd";

  // If all words of the given
  // String are in AP
  if (checkWordAP(str))
  {
    Console.Write("Yes");
  }
  else
  {
    Console.Write("No");
  }
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to check str can be
// rearranged such that characters
// of each word forms an AP
function checkWordAP(s)
{

    // Stores the String
  // in Stringstream
  let str = s.split(" ");

  // Stores each word of
  // the given String

  for (let temp = 0; temp < str.length; temp++ )
  {

    // Sort the current word
    str[temp] = sort(str[temp]);

    // Check if the current word
    // of the given String is in AP
    for (let i = 2; i < str[temp].length; i++)
    {

      // Store the value of difference
      // between adjacent characters
      let diff = str[temp][1].charCodeAt(0) - str[temp][0].charCodeAt(0);

      // Check if difference between all
      // adjacent characters are equal
      if (diff != str[temp][i].charCodeAt(0) - str[temp][i-1].charCodeAt(0))
      {
        return false;
      }
    }
  }

  // If all words are in AP.
  return true;
}

function sort(inputString)
{

    // convert input string to char array
  let tempArray = inputString.split("");

  // sort tempArray
  (tempArray).sort();

  // return new sorted string
  return (tempArray).join("");
}

// Driver Code
let str = "ace yzx fbd";

  // If all words of the given
  // String are in AP
  if (checkWordAP(str))
  {
    document.write("Yes");
  }
  else
  {
    document.write("No");
  }

// This code is contributed by patel2127
</script>
```

**Output**

```
Yes
```

***时间复杂度:**O(N log<sub>2</sub>N)*
***辅助空间:** O(N)*