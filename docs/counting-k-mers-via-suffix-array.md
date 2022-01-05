# 通过后缀数组计算 k-mers

> 原文:[https://www . geesforgeks . org/counting-k-mers-via-后缀-array/](https://www.geeksforgeeks.org/counting-k-mers-via-suffix-array/)

**前置条件:** [后缀数组。](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)

**什么是 k-mers？**
术语 [k-mer](http://contribute.geeksforgeeks.org/guide-to-write-an-article/) 通常指包含在字符串中的所有可能的长度为 k 的子字符串。计算 DNA/RNA 测序读数中的所有 k-mers 是许多生物信息学应用的第一步。

**什么是后缀数组？**
后缀数组是一个字符串所有后缀的排序数组。它是一种数据结构，用于全文索引、数据压缩算法等。更多信息可以在这里[找到。](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)

**问题:**给我们一个字符串和一个整数 k，我们必须找到所有对(substr，I)，这样 substr 就是一个长度为–k 的字符串子串，正好出现 I 次。

**进场所涉及的步骤:**
我们就拿**这个词“香蕉{content}”来说吧；**为例。
**第一步:**计算给定文本的后缀数组。

```
          6     $   
          5     a$
          3     ana$
          1     anana$
          0     banana$
          4     na$                    
          2     nana$

```

**第二步:**遍历后缀数组，保留**“curr _ count”**。
1。如果当前后缀的长度小于 k，则跳过迭代。也就是说，如果 **k = 2** ，那么当当前后缀为 **$** 时，迭代将被跳过。
2。如果当前后缀以与前一个后缀相同的长度-k 子字符串开始，则递增 curr_count。例如，在第四次迭代期间，当前后缀为“anana{content} ”;以长度为 k 的相同子字符串**“an”**作为前面的后缀“ana { content } # x201D 从。因此，在这种情况下，我们将增加 curr_count。
3。如果条件 2 不满足，那么如果前一个后缀的长度等于 k，那么它是一个有效的对，我们将输出它和它的当前计数，否则，我们将跳过那个迭代。

```
                 curr_count  Valid Pair
 6     $           1                     
 5     a$          1
 3     ana$        1         (a$, 1)
 1     anana$      1
 0     banana$     2         (an, 2)
 4     na$         1         (ba, 1)               
 2     nana$       1         (na, 2)

```

**示例:**

```
Input : banana$ // Input text
Output : (a$, 1) // k- mers
         (an, 2)
         (ba, 1)
         (na, 2)

Input : geeksforgeeks
Output : (ee, 2) 
         (ek, 2)
         (fo, 1)
         (ge, 2)
         (ks, 2)
         (or, 1)
         (sf, 1)

```

以下是上述方法的 C 代码:

```
// C program to solve K-mer counting problem
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to store data of a rotation
struct rotation {
    int index;
    char* suffix;
};

// Compares the rotations and
// sorts the rotations alphabetically
int cmpfunc(const void* x, const void* y)
{
    struct rotation* rx = (struct rotation*)x;
    struct rotation* ry = (struct rotation*)y;
    return strcmp(rx->suffix, ry->suffix);
}

// Takes input_text and its length as arguments
// and returns the corresponding suffix array
char** computeSuffixArray(char* input_text, 
                               int len_text)
{
    int i;

    // Array of structures to store rotations
    // and their indexes
    struct rotation suff[len_text];

    // Structure is needed to maintain old 
    // indexes of rotations after sorting them
    for (i = 0; i < len_text; i++) {
        suff[i].index = i;
        suff[i].suffix = (input_text + i);
    }

    // Sorts rotations using comparison function
    // defined above
    qsort(suff, len_text, sizeof(struct rotation), cmpfunc);

    // Stores the suffixes of sorted rotations
    char** suffix_arr = 
       (char**)malloc(len_text * sizeof(char*));

    for (i = 0; i < len_text; i++) {
        suffix_arr[i] = 
        (char*)malloc((len_text + 1) * sizeof(char));
        strcpy(suffix_arr[i], suff[i].suffix);
    }

    // Returns the computed suffix array
    return suffix_arr;
}

// Takes suffix array, its size and valid length as
// arguments and outputs the valid pairs of k - mers
void findValidPairs(char** suffix_arr, int n, int k)
{
    int curr_count = 1, i;
    char* prev_suff = (char*)malloc(n * sizeof(char));

    // Iterates over the suffix array,
    // keeping a current count
    for (i = 0; i < n; i++) {

        // Skipping the current suffix
        // if it has length < valid length
        if (strlen(suffix_arr[i]) < k) {

            if (i != 0 && strlen(prev_suff) == k) {
                printf("(%s, %d)\n", prev_suff, curr_count);
                curr_count = 1;}

            strcpy(prev_suff, suffix_arr[i]);
            continue;
        }

        // Incrementing the curr_count if first
        // k chars of prev_suff and current suffix
        // are same
        if (!(memcmp(prev_suff, suffix_arr[i], k))) {
            curr_count++;
        }
        else {

            // Pair is valid when i!=0 (as there is
            // no prev_suff for i = 0) and when strlen
            // of prev_suff is k
            if (i != 0 && strlen(prev_suff) == k) {
                printf("(%s, %d)\n", prev_suff, curr_count);
                curr_count = 1;
                memcpy(prev_suff, suffix_arr[i], k);
                prev_suff[k] = '\0';
            }
            else {
                memcpy(prev_suff, suffix_arr[i], k);
                prev_suff[k] = '\0';
                continue;
            }
        }

        // Modifying prev_suff[i] to current suffix
        memcpy(prev_suff, suffix_arr[i], k);
        prev_suff[k] = '\0';
    }

    // Printing the last valid pair
    printf("(%s, %d)\n", prev_suff, curr_count);
}

// Driver program to test functions above
int main()
{
    char input_text[] = "geeksforgeeks";
    int k = 2;
    int len_text = strlen(input_text);

    // Computes the suffix array of our text
    printf("Input Text: %s\n", input_text);
    char** suffix_arr = 
      computeSuffixArray(input_text, len_text);

    // Finds and outputs all valid pairs
    printf("k-mers: \n");
    findValidPairs(suffix_arr, len_text, k);

    return 0;
}
```

**输出:**

```
Input Text: banana$ 
k-mers: 
(a$, 1)
(an, 2)
(ba, 1)
(na, 2)

```

**时间复杂度:** O(s*len_text*log(len_text))，假设 s 是最长后缀的长度。

**来源:**
1。[后缀数组维基](https://en.wikipedia.org/wiki/Suffix_array)
2。[后缀数组 CMU](https://www.cs.cmu.edu/~ckingsf/bioinfo-lectures/suffixarrays.pdf)