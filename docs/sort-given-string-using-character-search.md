# 使用字符搜索对给定字符串进行排序

> 原文:[https://www . geesforgeks . org/sort-given-string-use-character-search/](https://www.geeksforgeeks.org/sort-given-string-using-character-search/)

给定一根大小为 **n** 的绳子**绳子**。问题是在不使用任何排序技术(如[冒泡](https://www.geeksforgeeks.org/bubble-sort/)、[选择](https://www.geeksforgeeks.org/selection-sort/)等)的情况下对给定字符串进行排序。该字符串仅包含小写字符。
示例:

```
Input : geeksforgeeks
Output : eeeefggkkorss

Input : coding
Output : cdgino
```

**算法:**

```
sortString(str, n)
    Initialize new_str = ""

    for i = 'a' to 'z'
        for j = 0 to n-1
            if str[j] == i, then
                new_str += str[j]

    return new_str
```

## C++

```
// C++ implementation to sort the given string without
// using any sorting technique
#include <bits/stdc++.h>
using namespace std;

// function to sort the given string without
// using any sorting technique
string sortString(string str, int n) {

  // to store the final sorted string
  string new_str = "";

  // for each character 'i'
  for (int i = 'a'; i <= 'z'; i++)

    // if character 'i' is present at a particular
    // index then add character 'i' to 'new_str'
    for (int j = 0; j < n; j++)
      if (str[j] == i)
        new_str += str[j];

  // required final sorted string
  return new_str;
}

// Driver program to test above
int main() {
  string str = "geeksforgeeks";
  int n = str.size();
  cout << sortString(str, n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the given
// string without using any sorting technique
class GFG {

    // function to sort the given string
    // without using any sorting technique
    static String sortString(String str, int n)
    {

        // to store the final sorted string
        String new_str = "";

        // for each character 'i'
        for (int i = 'a'; i <= 'z'; i++)

            // if character 'i' is present at a
            // particular index then add character
            // 'i' to 'new_str'
            for (int j = 0; j < n; j++)
                if (str.charAt(j) == i)
                    new_str += str.charAt(j);

        // required final sorted string
        return new_str;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int n = str.length();

        System.out.print(sortString(str, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to sort
# the given string without using
# any sorting technique

# Function to sort the given string
# without using any sorting technique
def sortString(str, n):

    # To store the final sorted string
    new_str = ""

    # for each character 'i'
    for i in range(ord('a'), ord('z') + 1):

        # if character 'i' is present at a particular
        # index then add character 'i' to 'new_str'
        for j in range(n):
            if (str[j] == chr(i)):
                new_str += str[j]

    # required final sorted string
    return new_str

# Driver Code
str = "geeksforgeeks"
n = len(str)
print(sortString(str, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to sort the given
// string without using any sorting technique
using System;

class GFG {

    // function to sort the given string
    // without using any sorting technique
    static String sortString(String str, int n)
    {
        // to store the final sorted string
        String new_str = "";

        // for each character 'i'
        for (int i = 'a'; i <= 'z'; i++)

            // if character 'i' is present at a
            // particular index then add character
            // 'i' to 'new_str'
            for (int j = 0; j < n; j++)
                if (str[j] == i)
                    new_str += str[j];

        // required final sorted string
        return new_str;
    }

    // Driver code
    public static void Main()
    {
        String str = "geeksforgeeks";
        int n = str.Length;

        Console.Write(sortString(str, n));
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

// Javascript implementation to sort the given string without
// using any sorting technique

// function to sort the given string without
// using any sorting technique
function sortString(str, n) {

  // to store the final sorted string
  var new_str = "";

  // for each character 'i'
  for (var i = 'a'.charCodeAt(0); i <= 'z'.charCodeAt(0); i++)

    // if character 'i' is present at a particular
    // index then add character 'i' to 'new_str'
    for (var j = 0; j < n; j++)
      if (str[j].charCodeAt(0) == i)
        new_str += str[j];

  // required final sorted string
  return new_str;
}

// Driver program to test above
var str = "geeksforgeeks";
var n = str.length;
document.write( sortString(str, n));

</script>
```

**Output :** 

```
eeeefggkkorss
```

**方法 2:**
在上面的方法中，我们每次都要遍历整个字符串，寻找‘a’到‘z’集合中的每个字符。我们可以通过维护一个字符并用字符串中所有字符的出现次数来填充它来克服这个缺点。稍后，我们可以从字符数组中构造所需的排序字符串。
下面是实现。

## C++

```
// C++ implementation to sort the given
// string without using any sorting technique
#include <iostream>
using namespace std;

string sortString(string str, int n) {
int i;
//A character array to store the no.of occurrences of each character
//between 'a' to 'z'
char arr[26]={0};

//to store the final sorted string
string new_str = "";

//To store each occurrence of character by relative indexing
for (i = 0; i < n; i++)
   ++arr[str[i]-'a'];

//To traverse the character array and append it to new_str
for(i=0;i<26;i++)
  while(arr[i]--)
    new_str += i+'a';

return new_str;
}

// Driver program to test above
int main() {
string str = "geeksforgeeks";
int n = str.size();
cout << sortString(str, n);
return 0;
}

// This code is contributed by Aravind Alapati
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the given
// String without using any sorting technique
class GFG
{

    static String sortString(String str, int n)
    {
        int i;

        // A character array to store
        // the no.of occurrences of each
        // character between 'a' to 'z'
        char[] arr = new char[26];

        // to store the final sorted String
        String new_str = "";

        // To store each occurrence of
        // character by relative indexing
        for (i = 0; i < n; i++)
            ++arr[str.charAt(i) - 'a'];

        // To traverse the character
        // array and append it to new_str
        for (i = 0; i < 26; i++)
            while (arr[i]-- > 0)
            {
                new_str += String.valueOf((char)(i + 'a'));
            }

        return new_str;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int n = str.length();
        System.out.print(sortString(str, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation to sort the given
# string without using any sorting technique
def sortString(st, n):

    # A character array to store the no.of occurrences of each character
    # between 'a' to 'z'
    arr = [0] * 26

    # to store the final sorted string
    new_str = ""

    # To store each occurrence of character by relative indexing
    for i in range(n):
        arr[ord(st[i]) - ord('a')] += 1

    # To traverse the character array and append it to new_str
    for i in range(26):
        while(arr[i] > 0):
            new_str += chr(i+ord('a'))
            arr[i] -= 1

    return new_str

# Driver program to test above
if __name__ == "__main__":

    st = "geeksforgeeks"
    n = len(st)
    print(sortString(st, n))

    # This code is contributed by ukasp.
```

## C#

```
// C# implementation to sort the given
// String without using any sorting technique
using System;

class GFG
{

    static String sortString(String str, int n)
    {
        int i;

        // A character array to store
        // the no.of occurrences of each
        // character between 'a' to 'z'
        char[] arr = new char[26];

        // to store the readonly sorted String
        String new_str = "";

        // To store each occurrence of
        // character by relative indexing
        for (i = 0; i < n; i++)
            ++arr[str[i] - 'a'];

        // To traverse the character
        // array and append it to new_str
        for (i = 0; i < 26; i++)
            while (arr[i]-- > 0)
            {
                new_str += String.Join("",(char)(i + 'a'));
            }

        return new_str;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        int n = str.Length;
        Console.Write(sortString(str, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to sort the given
// string without using any sorting technique

function sortString(str, n) {
var i;
//A character array to store the no.of occurrences of each character
//between 'a' to 'z'
var arr = Array(26).fill(0);

//to store the final sorted string
var new_str = "";

//To store each occurrence of character by relative indexing
for (i = 0; i < n; i++)
   ++arr[str[i].charCodeAt(0) -'a'.charCodeAt(0)];

//To traverse the character array and append it to new_str
for(i=0;i<26;i++)
  while(arr[i]--)
    new_str += String.fromCharCode(i +'a'.charCodeAt(0));

return new_str;
}

// Driver program to test above

var str = "geeksforgeeks";
var n = str.length;
document.write( sortString(str, n));

</script>
```

**Output :** 

```
eeeefggkkorss
```