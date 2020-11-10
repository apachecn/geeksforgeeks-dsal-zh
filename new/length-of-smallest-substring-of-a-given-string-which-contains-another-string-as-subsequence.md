# 给定字符串的最小子字符串的长度，该字符串包含另一个字符串作为子序列

> 原文：[https://www.geeksforgeeks.org/length-of-smallest-substring-of-a-given-string-which-contains-another-string-as-subsequence/](https://www.geeksforgeeks.org/length-of-smallest-substring-of-a-given-string-which-contains-another-string-as-subsequence/)

给定两个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **A** 和 **B** ，任务是找到具有**的 **A** 中最小的[子字符串](https://www.geeksforgeeks.org/substring-in-java/) ] B** 作为[子序列](https://www.geeksforgeeks.org/tag/subsequence/)。

**示例**：

> **输入**：`A = "abcdefababaef", B = "abf"`
>
> **输出**：5
>
> **说明**：
>
> `A`的最小子串`B`作为子序列是`abcdef`。
>
> 因此，所需长度为 5。
> 
> **输入**：`A = "abcdefababaef", B = "aef"`
>
> **输出**：3

**方法**：请按照以下步骤解决问题：

*   将 **A** 的字符的所有索引存储在 [Map](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **CharacterIndex** 中的 **B** 中。

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **B** 的所有字符。

*   检查字符串 **A** 中是否存在字符串 **B** 的第一个字符：

    1.  如果发现为真，则使用字符串 **A 中第一次出现的 **B [0]** 的索引初始化两个变量 **firstVar** 和 **lastVar**** 。

    2.  更新值后，从[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **CharacterIndex** 中删除该字符。

    3.  否则，将无法再有其他子字符串。

*   对于 **B** 的其余字符，请检查字符串 **A** 中是否存在该字符。 如果发现是真的，则遍历字符串 **A** 中该字符的所有出现，并且如果字符串 **A** 中该字符的索引超过 **lastVar** ， 然后使用该索引更新 **lastVar** 。 否则，将无法再有其他子字符串。

*   如果 **B** 被完全遍历，则用 **firstVar** 和 **lastVar 之间的差异更新答案。**

*   打印最终的最小化答案。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// smallest substring of a having
// string b as a subsequence
int minLength(string a, string b)
{

    // Stores the characters present
    // in string b
    map<char, int> Char;
    for (int i = 0; i < b.length(); i++) {

        Char[b[i]]++;
    }

    // Find index of characters of a
    // that are also present in string b
    map<char, vector<int> > CharacterIndex;

    for (int i = 0; i < a.length(); i++) {

        char x = a[i];

        // If character is present in string b
        if (Char.find(x) != Char.end()) {

            // Store the index of character
            CharacterIndex[x].push_back(i);
        }
    }

    int len = INT_MAX;

    // Flag is used to check if
    // substring is possible
    int flag;

    while (true) {

        // Assume that substring is
        // possible
        flag = 1;

        // Stores first and last
        // indices of the substring
        // respectively
        int firstVar, lastVar;

        for (int i = 0; i < b.length(); i++) {

            // For first character of string b
            if (i == 0) {

                // If the first character of
                // b is not present in a
                if (CharacterIndex.find(b[i])
                    == CharacterIndex.end()) {

                    flag = 0;
                    break;
                }

                // If the first character of b
                // is present in a
                else {

                    int x = *(
                        CharacterIndex[b[i]].begin());

                    // Remove the index from map
                    CharacterIndex[b[i]].erase(
                        CharacterIndex[b[i]].begin());

                    // Update indices of
                    // the substring
                    firstVar = x;
                    lastVar = x;
                }
            }

            // For the remaining characters of b
            else {

                int elementFound = 0;
                for (auto e : CharacterIndex[b[i]]) {

                    if (e > lastVar) {

                        // If index possible for
                        // current character
                        elementFound = 1;
                        lastVar = e;
                        break;
                    }
                }
                if (elementFound == 0) {

                    // If no index is possible
                    flag = 0;
                    break;
                }
            }
        }

        if (flag == 0) {

            // If no more substring
            // is possible
            break;
        }

        // Update the minimum length
        // of substring
        len = min(len,
                  abs(lastVar - firstVar) + 1);
    }

    // Return the result
    return len;
}

// Driver Code
int main()
{

    // Given two string
    string a = "abcdefababaef";
    string b = "abf";

    int len = minLength(a, b);
    if (len != INT_MAX) {

        cout << len << endl;
    }
    else {

        cout << "Impossible" << endl;
    }
}

```

## Python3

```py

# Python3 program to implement
# the above approach
import sys

# Function to find the length of
# smallest substring of a having
# string b as a subsequence
def minLength(a, b):

    # Stores the characters present
    # in string b
    Char = {}
    for i in range(len(b)):
        Char[b[i]] = Char.get(b[i], 0) + 1

    # Find index of characters of a
    # that are also present in string b
    CharacterIndex = {}

    for i in range(len(a)):
        x = a[i]

        # If character is present in string b
        if (x in Char):

            # Store the index of character
            CharacterIndex[x] = CharacterIndex.get(x, [])
            CharacterIndex[x].append(i)

    l = sys.maxsize

    # Flag is used to check if
    # substring is possible
    while(True):

        # Assume that substring is
        # possible
        flag = 1

        firstVar = 0
        lastVar = 0

        # Stores first and last
        # indices of the substring
        # respectively
        for i in range(len(b)):

            # For first character of string b
            if (i == 0):

                # If the first character of
                # b is not present in a
                if (b[i] not in CharacterIndex):
                    flag = 0
                    break

                # If the first character of b
                # is present in a
                else:
                    x = CharacterIndex[b[i]][0]

                    # Remove the index from map
                    CharacterIndex[b[i]].remove(
                    CharacterIndex[b[i]][0])

                    # Update indices of
                    # the substring
                    firstVar = x
                    lastVar = x

            # For the remaining characters of b
            else:
                elementFound = 0
                for e in CharacterIndex[b[i]]:
                    if (e > lastVar):

                        # If index possible for
                        # current character
                        elementFound = 1
                        lastVar = e
                        break

                if (elementFound == 0):

                    # If no index is possible
                    flag = 0
                    break

        if (flag == 0):

            # If no more substring
            # is possible
            break

        # Update the minimum length
        # of substring
        l = min(l, abs(lastVar - firstVar) + 1)

    # Return the result
    return l

# Driver Code
if __name__ == '__main__':

    # Given two string
    a = "abcdefababaef"
    b = "abf"

    l = minLength(a, b)
    if (l != sys.maxsize):
        print(l)
    else:
        print("Impossible")

# This code is contributed by SURENDRA_GANGWAR

```

**输出**： 

```
5

```

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`



* * *

* * *



