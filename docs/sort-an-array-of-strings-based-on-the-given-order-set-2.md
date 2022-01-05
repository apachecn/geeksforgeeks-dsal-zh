# 根据给定的顺序对字符串数组进行排序| Set-2

> 原文:[https://www . geeksforgeeks . org/sort-基于给定顺序的字符串数组-set-2/](https://www.geeksforgeeks.org/sort-an-array-of-strings-based-on-the-given-order-set-2/)

给定一个字符串数组**单词[]** 和字母的顺序，任务是根据给定的顺序对数组进行排序。假设字典和单词只包含小写英文字母。

**示例:**

> ***输入:**单词[] = {“你好”、“geeksforgeeks”}，顺序[]=“hlabcdefgijkmnopqrstuvwxyz”*
> ***输出:**你好 geeksforgeeks*
> ***解释:**根据给定的顺序‘h’出现在‘g’之前，因此单词被认为是排序的。*
> 
> ***输入:**字数= {“word”、“world”、“row”}，顺序=“worldabcegfghijkmnpqstuxyz”*
> ***输出:**世界字数 row*
> ***解释:**按照给定的顺序‘l’出现在‘d’之前遂将‘world’这几个字保留在先。*

**方法:**给定的问题已经在文章[这里](https://www.geeksforgeeks.org/sort-an-array-of-strings-based-on-the-given-order/)中讨论过了。本文提出了一种使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)的不同方法。因为给出了字母的顺序，所以它可以用作键，其中**顺序【I】<sup>第</sup>** 字母可以被 **i <sup>第</sup>** 字母代替。例如，在给定的顺序[]=*“hlabcdefgijknmopqrstuvwxyz”中，*字符**‘h’**可以用**‘a’**代替，字符**‘l’**可以用**‘b’**代替，以此类推*。*利用该观察，可以通过以下步骤解决给定的问题:

*   创建一个**散列函数**，该函数接受一个**键**作为参数，并根据给定的键替换字符串的所有字符，即字符 **x** 将被存储在**键【x】**中的字符替换。
*   使用无序映射**编码**，按照给定的顺序存储字符序列，即**编码['h'] = 'a'** ，**编码['l'] = 'b'…** 等等。同样，将反转存储在 **decode** 中，即 **decode['a'] = 'h'** ，**decode[' b ']= ' l '**……等等，可以用来恢复原始数组。
*   使用**编码**作为关键字对数组进行散列后排序。
*   使用**解码**作为键恢复排序数组中的字符串。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to replace all the
// characters in the array of strings
// according to the given key
void hashFunction(vector<string>& words,
                  unordered_map<char, char> key)
{
    for (auto& x : words) {
        for (int i = 0; i < x.size(); i++) {
            x[i] = key[x[i]];
        }
    }
}

// Function to pring the strings
// according to the given order
void printSorted(vector<string> words, string order)
{
    // Stores the characters in order
    // to encode and decode the string
    unordered_map<char, char> encode, decode;

    // Loop to iterate over all characters
    for (int i = 0; i < 26; i++) {
        // Replace the order[i]th character
        // from the ith character
        encode[order[i]] = 'a' + i;

        // Replace the ith character
        // from the order[i]th character
        decode['a' + i] = order[i];
    }

    // Function Call to replace all characters
    // in words according to encode
    hashFunction(words, encode);

    // STL Function to sort the array
    sort(words.begin(), words.end());

    // Function Call to replace all characters
    // in words according to decode in order
    // to restore original strings
    hashFunction(words, decode);

    // Printing the sorted order of words
    for (auto x : words) {
        cout << x << " ";
    }
}

// Driver code
int main()
{
    vector<string> words = { "word", "world", "row" };
    string order = "worldabcefghijkmnpqstuvxyz";

    // Function Call
    printSorted(words, order);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to replace all the
# characters in the array of strings
# according to the given key
def hashFunction(words, key):
    for x in words:
        x = list(x)
        for i in range(len(x)):
            x[i] = key[x[i]]
        x = ''.join(x)

# Function to pring the strings
# according to the given order
def printSorted(words, order):

    # Stores the characters in order
    # to encode and decode the string
    encode = {}
    decode = {}

    # Loop to iterate over all characters
    for i in range(26):
        # Replace the order[i]th character
        # from the ith character
        encode[order[i]] = chr(ord('a') + i)

        # Replace the ith character
        # from the order[i]th character
        decode[chr(ord('a') + i)] = order[i]

    # Function Call to replace all characters
    # in words according to encode
    hashFunction(words, encode)

    # STL Function to sort the array
    words.sort(reverse = True)

    # Function Call to replace all characters
    # in words according to decode in order
    # to restore original strings
    hashFunction(words, decode)

    # Printing the sorted order of words
    for x in words:
        print(x,end = " ")

# Driver code
if __name__ == '__main__':
    words = ["word", "world", "row"]
    order = "worldabcefghijkmnpqstuvxyz"

    # Function Call
    printSorted(words, order)

    # This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// Function to replace all the
// characters in the array of strings
// according to the given key
function hashFunction(words, key) {
  for (x of words) {
    for (let i = 0; i < x.length; i++) {
      x[i] = key.get(x[i]);
    }
  }
  console.log(words);
}

// Function to pring the strings
// according to the given order
function printSorted(words, order) {
  // Stores the characters in order
  // to encode and decode the string
  let encode = new Map();
  let decode = new Map();

  // Loop to iterate over all characters
  for (let i = 0; i < 26; i++) {
    // Replace the order[i]th character
    // from the ith character
    encode.set(order[i], "a".charCodeAt(0) + i);

    // Replace the ith character
    // from the order[i]th character
    decode.set("a".charCodeAt(0) + i, order[i]);
  }

  // Function Call to replace all characters
  // in words according to encode
  hashFunction(words, encode);

  // Function to sort the array
  words.sort().reverse();

  // Function Call to replace all characters
  // in words according to decode in order
  // to restore original strings
  hashFunction(words, decode);

  // Printing the sorted order of words
  for (x of words) {
    document.write(x + " ");
  }
}

// Driver code

let words = ["word", "world", "row"];
let order = "worldabcefghijkmnpqstuvxyz";

// Function Call
printSorted(words, order);

</script>
```

**Output**

```
world word row 
```

***时间复杂度:** O(N*M*log(N))其中 M 是所有字符串的平均长度。*
***辅助空间:** O(1)*