# 打印给定字符串的所有字典式更大排列

> 原文:[https://www . geeksforgeeks . org/print-all-辞书-给定字符串的更大排列/](https://www.geeksforgeeks.org/print-all-lexicographical-greater-permutations-of-a-given-string/)

给定一个**字符串 S** ，打印那些按字典顺序大于 S 的字符串 S 的排列。如果没有这样的字符串排列，打印-1。

**示例:**

> **输入:** BCA
> **输出:** CAB，CBA
> **解释:**
> 这里，S =“BCA”，有 2 个字符串“CAB，CBA”，按字典顺序大于 S。
> 
> **输入:** CBA
> **输出:** -1
> 没有字典顺序大于 S 的字符串，所以输出为-1。

**方法:**为了解决上面提到的问题，我们将使用 [STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 。使用[next _ performation()和 prev _ performation()](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)函数来检查和字典顺序更大的字符串。如果字符串较大，则打印它，否则打印-1。

下面是上述方法的实现:

```
// C++ program to print the lexicographically
// greater strings then the given string
#include <bits/stdc++.h>
using namespace std;

// Function to print the lexicographically
// greater strings then the given string
void print_lexiStrings(string S)
{

    // Condition to check if there is no
    // string which is lexicographically
    // greater than string S
    if (!next_permutation(S.begin(), S.end()))
        cout << "-1";

    // Move to the previous permutation
    prev_permutation(S.begin(), S.end());

    // Iterate over all the
    // lexicographically greater strings
    while (next_permutation(S.begin(), S.end())) {
        cout << S << "\n";
    }
}

// Driver Code
int main()
{

    string S = "ABC";

    print_lexiStrings(S);
}
```

**Output:**

```
ACB
BAC
BCA
CAB
CBA

```