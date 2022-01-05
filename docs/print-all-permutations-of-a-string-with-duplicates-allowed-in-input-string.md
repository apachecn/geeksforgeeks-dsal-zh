# 用副本打印给定字符串的所有不同排列

> 原文:[https://www . geesforgeks . org/print-输入字符串中允许重复的字符串的所有排列/](https://www.geeksforgeeks.org/print-all-permutations-of-a-string-with-duplicates-allowed-in-input-string/)

给定一个可能包含重复的字符串，编写一个函数来打印给定字符串的所有排列，这样就不会在输出中重复排列。
示例:

```
Input:  str[] = "AB"
Output: AB BA

Input:  str[] = "AA"
Output: AA

Input:  str[] = "ABC"
Output: ABC ACB BAC BCA CBA CAB

Input:  str[] = "ABA"
Output: ABA AAB BAA

Input:  str[] = "ABCA"
Output: AABC AACB ABAC ABCA ACBA ACAB BAAC BACA 
        BCAA CABA CAAB CBAA
```

我们已经讨论了一个算法来打印所有排列在下面的帖子。强烈建议参考下面的帖子作为这个帖子的先决条件。
[写一个 C 程序打印给定字符串的所有排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)
上面链接讨论的算法不处理重复。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Program to print all permutations of a
// string in sorted order.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* Following function is needed for library
  function qsort(). */
int compare(const void* a, const void* b)
{
    return (*(char*)a - *(char*)b);
}

// A utility function two swap two characters
// a and b
void swap(char* a, char* b)
{
    char t = *a;
    *a = *b;
    *b = t;
}

// This function finds the index of the
// smallest character which is greater
// than 'first' and is present in str[l..h]
int findCeil(char str[], char first, int l, int h)
{
    // initialize index of ceiling element
    int ceilIndex = l;

    // Now iterate through rest of the
    // elements and find the smallest
    // character greater than 'first'
    for (int i = l + 1; i <= h; i++)
        if (str[i] > first && str[i] < str[ceilIndex])
            ceilIndex = i;

    return ceilIndex;
}

// Print all permutations of str in sorted order
void sortedPermutations(char str[])
{
    // Get size of string
    int size = strlen(str);

    // Sort the string in increasing order
    qsort(str, size, sizeof(str[0]), compare);

    // Print permutations one by one
    bool isFinished = false;
    while (!isFinished) {

        // print this permutation
        static int x = 1;
        printf("%d  %s \n", x++, str);

        // Find the rightmost character
        // which is smaller than its next
        // character. Let us call it 'first
        // char'
        int i;
        for (i = size - 2; i >= 0; --i)
            if (str[i] < str[i + 1])
                break;

        // If there is no such character, all
        // are sorted in decreasing order,
        // means we just printed the last
        // permutation and we are done.
        if (i == -1)
            isFinished = true;
        else {

            // Find the ceil of 'first char'
            // in right of first character.
            // Ceil of a character is the
            // smallest character greater
            // than it
            int ceilIndex = findCeil(str,
                     str[i], i + 1, size - 1);

            // Swap first and second characters
            swap(&str[i], &str[ceilIndex]);

            // Sort the string on right of 'first char'
            qsort(str + i + 1, size - i - 1,
                  sizeof(str[0]), compare);
        }
    }
}

// Driver program to test above function
int main()
{
    char str[] = "ACBC";
    sortedPermutations(str);
    return 0;
}
```

**Output**

```
1  ABCC 
2  ACBC 
3  ACCB 
4  BACC 
5  BCAC 
6  BCCA 
7  CABC 
8  CACB 
9  CBAC 
10  CBCA 
11  CCAB 
12  CCBA 

```

以上代码摘自懒汉先生下面的评论。
时间复杂度:O(n <sup>2</sup> * n！)
辅助空间:O(1)

上述算法在时间复杂度上为 O(n2 * n！)但是我们可以实现更好的时间复杂度 O(n！*n ),在输入中所有不同字符的情况下，通过该算法中的一些修改就存在这种情况。独特的字符算法可以在这里找到–[https://www . geeksforgeeks . org/write-a-c-program-to-print-all-排列-给定字符串/](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)

**高效的方法:**在我们寻找所有排列的递归函数中，我们可以使用无序集来处理活动字符串中剩余的重复元素。当迭代字符串的元素时，我们将在无序集中检查该元素，如果找到，我们将跳过该迭代，否则我们将把该元素插入无序集中。由于平均而言，所有无序集操作(如 insert()和 find()都在 O(1)时间内，因此使用无序集不会改变算法的时间复杂度。

算法实现如下–

## C++

```
#include <algorithm>
#include <iostream>
#include <unordered_set>
using namespace std;

void printAllPermutationsFast(string s, string l)
{
    if (s.length() < 1) {
        cout << l + s << endl;
    }
    unordered_set<char> uset;
    for (int i = 0; i < s.length(); i++) {
        if (uset.find(s[i]) != uset.end()) {
            continue;
        }
        else {
            uset.insert(s[i]);
        }
        string temp = "";
        if (i < s.length() - 1) {
            temp = s.substr(0, i) + s.substr(i + 1);
        }
        else {
            temp = s.substr(0, i);
        }
        printAllPermutationsFast(temp, l + s[i]);
    }
}

int main()
{
    string s = "ACBC";
    sort(s.begin(), s.end());
    printAllPermutationsFast(s, "");
    return 0;
}
```

**Output**

```
ABCC
ACBC
ACCB
BACC
BCAC
BCCA
CABC
CACB
CBAC
CBCA
CCAB
CCBA

```

时间复杂性–O(n * n！)
辅助空间–O(n)

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息