# 通过最多插入 1 个字符串

检查给定的字符串是否可以相等

> 原文:[https://www . geesforgeks . org/check-if-给定字符串-最多插入 1 个字符串就可以使其相等/](https://www.geeksforgeeks.org/check-if-given-strings-can-be-made-equal-by-inserting-at-most-1-string/)

给定两个[句子](https://www.geeksforgeeks.org/python-spilt-a-sentence-into-list-of-words/)**【S1】**和 **S2** ，任务是通过在这两个句子的任何一个中最多插入一个句子(可能是空的)来检查句子是否可以相等。

**示例:**

> **输入:** S1 =“开始在 GeeksforGeeks 上练习”，S2 =“开始 GeeksforGeeks”
> **输出:**
> 真
> **说明:“**练习 on”可以插在 S2 中的“开始”和“geeks forgeeks”之间，使其等于 S1。
> 
> **输入:** S1=“新德里是印度首都”，S2 =“是首都”
> **输出:**
> 假

**方法:**以下观察有助于解决问题:

*   如果两个句子的大小相等，但它们本身不相同，就不能使它们相等。
*   这两个句子的[最长共同前缀](https://www.geeksforgeeks.org/longest-common-prefix-using-word-by-word-matching/)和最长共同后缀去掉后，如果其中至少有一个是空的，则表示可以使它们相等。

借助[deq](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)可以解决问题。按照以下步骤解决问题:

*   检查 **S1** 和 **S2** 的大小是否相等。如果它们相等，请执行以下操作:
    *   如果 **S1** 等于 **S2** ，则返回**真**。
    *   否则，返回**假**。
*   初始化两个[德格](https://www.geeksforgeeks.org/deque-cpp-stl/) **X** 和 **Y** 。
*   将 **S1** 的所有文字推入 **X** 。
*   将 **S2** 的所有文字推入 **Y** 。
*   虽然 **X** 和 **Y** 的[正面](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)相同，但是从 **X** 和 **Y** 的[正面](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)弹出。
*   当 **X** 和 **Y** 的[背面](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)相同时，从 **X** 和 **Y** 的[背面](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)弹出。
*   检查 **X** 或 **Y** 是否为空。如果有空的，返回**真**。
*   否则，返回**假**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// two sentences can be made equal
// by inserting at most
// one sentence in one of them
bool areSimilar(string S1, string S2)
{
    // size of sentence S1
    int N = S1.size();

    // size of sentence S2
    int M = S2.size();

    // check if S1 and S2
    // are of equal sizes
    if (N == M) {
        // if both sentences are
        // the same, return true
        if (S1 == S2)
            return true;

        // Otherwise, return false
        return false;
    }

    // Declare 2 deques X and Y
    deque<string> X, Y;

    // insert ' ' at the end of both
    // sentences so that the last
    // word can be identified
    S1.push_back(' ');
    S2.push_back(' ');

    string temp = "";

    // traverse the sentence S1
    for (int i = 0; i < N + 1; i++) {

        // push temp in deque
        // when a space comes in sentence
        // i.e a word has been formed
        if (S1[i] == ' ') {
            X.push_back(temp);
            temp = "";
        }
        else {
            // temp stores words
            // of the sentence
            temp += S1[i];
        }
    }

    // traverse the sentence S1
    for (int i = 0; i < M + 1; i++) {

        // push temp in deque
        // when a space comes in sentence
        // i.e a word has been formed
        if (S2[i] == ' ') {
            Y.push_back(temp);
            temp = "";
        }
        else {
            // temp stores words of the sentence
            temp += S2[i];
        }
    }

    // check for prefixes of both sentences
    while (X.size() > 0 && Y.size() > 0
           && X.front() == Y.front()) {

        // pop the prefix from both
        // deques till they are equal
        X.pop_front();
        Y.pop_front();
    }

    // check for suffixes of both sentences
    while (X.size() > 0 && Y.size() > 0
           && X.back() == Y.back()) {

        // pop the suffix from both deques
        // till they are equal
        X.pop_back();
        Y.pop_back();
    }

    // if any of the deques is empty
    // return true
    if (X.size() == 0 || Y.size() == 0)
        return true;

    // if both the deques are
    // not empty return false
    return false;
}
// Driver code
int main()
{
    // Input
    string S1 = "Start practicing on GeeksforGeeks";
    string S2 = "Start GeeksforGeeks";

    // function call
    if (areSimilar(S1, S2))
        cout << "True" << endl;
    else
        cout << "False" << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to check whether
# two sentences can be made equal
# by inserting at most
# one sentence in one of them
def areSimilar(S1, S2):

    S1 = [i for i in S1]
    S2 = [i for i in S2]

    # Size of sentence S1
    N = len(S1)

    # Size of sentence S2
    M = len(S2)

    # Check if S1 and S2
    # are of equal sizes
    if (N == M):

        # If both sentences are
        # the same, return True
        if (S1 == S2):
            return True

        # Otherwise, return false
        return False

    # Declare 2 deques X and Y
    X, Y = deque(), deque()

    # Insert ' ' at the end of both
    # sentences so that the last
    # word can be identified
    S1.append(' ')
    S2.append(' ')

    temp = ""

    # Traverse the sentence S1
    for i in range(N + 1):

        # Push temp in deque
        # when a space comes in sentence
        # i.e a word has been formed
        if (S1[i] == ' '):
            X.append(temp)
            temp = ""
        else:

            # temp stores words
            # of the sentence
            temp += S1[i]

    # Traverse the sentence S1
    for i in range(M + 1):

        # Push temp in deque
        # when a space comes in sentence
        # i.e a word has been formed
        if (S2[i] == ' '):
            Y.append(temp)
            temp = ""
        else:

            # temp stores words of the sentence
            temp += S2[i]

    # Check for prefixes of both sentences
    while (len(X) > 0 and
           len(Y) > 0 and X[0] == Y[0]):

        # Pop the prefix from both
        # deques till they are equal
        X.popleft()
        Y.popleft()

    # Check for suffixes of both sentences
    while (len(X) > 0 and len(Y) > 0 and
           X[-1] == Y[-1]):

        # Pop the suffix from both deques
        # till they are equal
        X.pop()
        Y.pop()

    # If any of the deques is empty
    # return True
    if (len(X) == 0 or len(Y) == 0):
        return True

    # If both the deques are
    # not empty return false
    return False

# Driver code
if __name__ == '__main__':

    # Input
    S1 = "Start practicing on GeeksforGeeks"
    S2 = "Start GeeksforGeeks"

    # Function call
    if (areSimilar(S1, S2)):
        print("True")
    else:
        print("False")

# This code is contributed by mohit kumar 29
```

**Output**

```
True
```

***时间复杂度:** O(N+M)，其中 N 和 M 分别是 S1 和 S2 的大小。*
***辅助空间:** O(N+M)*