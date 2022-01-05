# 生成字符串不同排列的迭代程序

> 原文:[https://www . geesforgeks . org/迭代程序生成字符串的不同排列/](https://www.geeksforgeeks.org/iterative-program-to-generate-distinct-permutations-of-a-string/)

给定一个字符串 **str** ，任务是迭代生成给定字符串的所有不同排列。

**示例:**

> **输入:**【str = " BBA】
> **输出:**
> 【abb】
> 【Bab】
> BBA
> 
> **输入:**【str = " ABC】
> **输出:**
> 【ABC】
> 【ACB】
> 【BAC】
> 【cab】
> CBA

**方法:**长度为 n 的字符串的排列数为 n！。下面的算法也可以扩展到任意对象的数组。这里只涉及生成字符串置换的情况。
算法以迭代的方式生成它们，如下所示:
我们将使用示例输入字符串“abca”来完成这些步骤。

算法的第一步是将每个字母映射成一个数字，并存储每个字母出现的次数。为此，首先对字符串进行排序。

修改的输入字符串:“aabc”

现在，字母将映射如下:

```
(first: mapped Number, second: Count)
a : 0, 2
b : 1, 1
c : 2, 0
```

我们使用的数字系统的基数是 3(等于输入字符串中不同字符的数量)
现在一个数组将保存每个字母的映射值。基本思想是将数组作为数字系统中的组合数递增，基数等于不同字符的数量。

所以最初数组会是[0，0，1，2]
我们在这个上加 1，新的数组是[0，0，2，0](数制是 3:我们只是在基数 3 的系统中加了 0012 和 1)
我们检查数组中每个数字的出现次数，并与原始引用数组中每个字母的出现次数进行核对。在这种情况下[0，0，2，0]是一个无效的序列，因为原始字符串中的零(或“a”，映射为 0 的字符)数量为 count(0) >

我们重复这个过程，直到我们的数组等于[2，1，0，0]，即可以生成的最大有效数，从而耗尽所有排列。
这种方法的复杂性为 **O(n <sup>(n + 1)</sup> )** 。

**优化算法**
基本前提依然不变。然而，现在算法试图避免许多不相关和无用的状态或排列。

函数 generatePermutation(string)准备引用表(代码中的 ref vector)，该表存储每个索引及其出现的映射字符。它还准备映射整数的单词。(要置换的整数数组)。
函数调用函数 getNext(args…)，将数组改变为下一个排列。当溢出时(生成所有置换)，函数返回结束。否则返回 VALID。

因此，为了获得下一个状态，我们首先按照前面的方法将数组增加 1。我们跟踪由于添加而改变的指数范围。

**示例:**
递增[0，2，2，2]给出[1，0，0，0]的变化指数范围{1，2，3}或[1，3]。之后，我们从最左边的索引开始，检查它是否是一个有效的数字。
如果左前子串(即[0，左])的值 a[left]的实例严格小于 n，则该数字有效，其中 n 是 a[left]在原始数组中出现的次数。

1.  检查左侧的有效性。
2.  如果没有冲突，向左递增进入步骤 1。如果 left ==数组的最后一个索引，则中断。
3.  否则递增 a[left]，如果 a[left] < base(不同元素的数量)，转到步骤 1。
4.  否则，在子阵列[0，左]上加 1，得到新的左索引，开始改变零件的范围。转到步骤 1。

如果生成的置换有效，函数返回 VALID，如果发生溢出，函数返回 END。

有效性检查是由助手函数 hasConflict(args…)完成的，它只是检查子数组[0，左]中是否出现了[left]。
如果出现的次数严格小于原始数组中某个[left]的出现次数，则返回 true，否则返回 false。

通过首先检查并添加到左边的索引中，我们跳过了许多原本会在算法中悄悄出现的状态。
算法对于每个状态经历最多 O(n)个状态。
因此，**时间复杂度:** O(n * n！)
**空间复杂度:** O(n)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// No more permutations can be generated
#define END -1

// Permutation is valid
#define VALID 1

// Utility function to print the
// generated permutation
void printString(vector<int>& word,
                 vector<pair<char, int> >& ref)
{

    for (int i = 0; i < word.size(); i++) {
        cout << ref[word[i]].first;
    }
    cout << "\n";
}

// Function that checks for any conflict present
// in the word/string for the index
bool hasConflict(vector<int>& word,
                 vector<pair<char, int> >& ref, int index)
{

    // Check number of instances where value of
    // the character is equal to the
    // value at checking index
    int conflictCount = 0;
    for (int i = 0; i < index; i++) {
        if (word[i] == word[index])
            conflictCount++;
    }

    // If the number of instances are greater
    // than the number of occurrences of the
    // character then conflict is present
    if (conflictCount < ref[word[index]].second) {
        return false;
    }

    return true;
}

// Function that returns the validity of the
// next permutation generated and makes
// changes to the word array
int getNext(vector<int>& word,
            vector<pair<char, int> >& ref, int mod)
{

    int left, right, carry;

    right = word.size() - 1;

    carry = 1;

    // Simply add 1 to the array word following
    // the number system with base mod
    // generates a new permutation
    for (left = right; left >= 0; left--) {
        if (left == 0 && word[left] + carry >= mod) {
            return END; // overflown
        }

        if (word[left] + carry >= mod) {
            word[left] = (word[left] + carry) % mod;
        }
        else {
            word[left] = word[left] + carry;
            break;
        }
    }

    // All the values between left and right (inclusive)
    // were changed and therefore need to be
    // adjusted to get a valid permutation
    while (left <= right) {
        while (hasConflict(word, ref, left) && word[left] < mod) {

            // Increment till conflict between substring [0, i)
            // is resolved or word[left] goes above mod
            word[left]++;
        }
        if (word[left] >= mod) {

            // The value for left has crossed mod therefore
            // all the values for word with [0, left)
            // constant have been converted therefore add 1
            // to the substring [0, left) to get a new value
            // of left which represents all affected parts.
            // Repeat the process of conflict resolvation
            // and validity checking from this new left
            word[left] %= mod;
            int carry = 1;
            left--;
            while (left >= 0) {
                if (left == 0 && word[left] + carry >= mod) {

                    // Overflow
                    return END;
                }

                if (word[left] + carry >= mod) {
                    word[left] = (word[left] + carry) % mod;
                    left--;
                }
                else {
                    word[left] = (word[left] + carry);
                    break;
                }
            }
        }
        else {

            // Increment left if conflict is resolved
            // for current index and do conflict
            // resolution for the next index
            left++;
        }
    }

    return VALID;
}

// Iterative function to generate all the
// distinct permutations of str
void generatePermutations(string str)
{
    if (str.size() == 0)
        return;

    // First sort the string to assign mapped values
    // and occurrences to each letter
    // Sorting needs to handle letters
    // with multiple occurrences
    sort(str.begin(), str.end());

    // Reference vector to store the mapping of
    // its index to its corresponding char
    // and the number of occurrences of the character
    // as the second element of the pair
    vector<pair<char, int> > ref(str.size());

    // Assign each character its index and the
    // number of occurrences
    int count = 0;
    ref[count] = make_pair(str[0], 1);

    for (int i = 1; i < str.size(); i++) {

        // Increment occurrences if character is repeated
        // Else create new mapping for the next character
        if (str[i] == str[i - 1]) {
            ref[count].second++;
        }
        else {
            count++;
            ref[count] = make_pair(str[i], 1);
        }
    }

    // Size may differ in case of multiple
    // occurrences of characters
    ref.resize(count + 1);

    // Construct the word
    // Word stores the mapped values for every letter
    // in a permuted sequence i.e. say for "abc"
    // word would be initially [0, 1, 2] or "aba", [0, 1, 0]
    vector<int> word;
    for (int i = 0; i < ref.size(); i++) {
        for (int j = 0; j < ref[i].second; j++)
            word.push_back(i);
    }

    // mod is the number of distinct letters in string
    int mod = ref.size();
    int flag = VALID;

    while (flag != END) {

        // If the permutation sent by getNext
        // is valid then print it
        printString(word, ref);

        // Get the next permutation, validity
        // stored in flag
        flag = getNext(word, ref, mod);
    }
}

// Driver code
int main()
{
    string str = "abc";

    generatePermutations(str);

    return 0;
}
```

**Output:** 

```
abc
acb
bac
bca
cab
cba
```