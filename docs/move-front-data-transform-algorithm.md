# 移动到前方数据转换算法

> 原文:[https://www . geesforgeks . org/move-front-data-transform-algorithm/](https://www.geeksforgeeks.org/move-front-data-transform-algorithm/)

**什么是 MTF 变换？**
[MTF(移动到前端)](https://en.wikipedia.org/wiki/Move-to-front_transform)是一种数据转换算法，它以这样一种方式重构数据，即转换后的消息更具可压缩性，因此被用作压缩的额外步骤。从技术上讲，它是输入字符序列到输出数字数组的可逆转换。

**为什么是 MTF？**
1。在许多情况下，输出数组给出频繁重复字符的较低索引，这在 [**数据压缩算法中很有用。**](https://www.geeksforgeeks.org/greedy-algorithms-set-3-huffman-coding/)

2.这是在实现 Burrows-Wheeler 数据压缩算法时连续执行的三个步骤中的第一个，该算法构成了 Unix 压缩实用程序 bzip2 的基础。

**MTF 背后的主要思想:**

1.MTF 背后的主要思想是维护一个法律符号的有序列表(在我们的例子中是 a 到 z)。

2.从输入字符串中一次读取一个字符。

3.打印出该字符在列表中出现的位置。

4.将该字符移到列表的前面，并重复该过程，直到获得所有输入字符的索引。

```
Illustration for "panama".  
List initially contains English alphabets in order. 
We one by one characters of input to front.
 input_str chars   output_arr       list
  p              15               abcdefghijklmnopqrstuvwxyz
  a              15 1             pabcdefghijklmnoqrstuvwxyz
  n              15 1 14          apbcdefghijklmnoqrstuvwxyz
  a              15 1 14 1        napbcdefghijklmoqrstuvwxyz
  m              15 1 14 1 14     anpbcdefghijklmoqrstuvwxyz
  a              15 1 14 1 14     manpbcdefghijkloqrstuvwxyz

```

**推断:**
1。如果字母在输入中出现多次，那么许多输出值将是小整数，如 0、1、2 等。

2.因此，对这些字母进行极高频率的编码是 [**霍夫曼编码的理想场景。**T3】](https://www.geeksforgeeks.org/greedy-algorithms-set-3-huffman-coding/)

**示例:**

```
Input : panama
Output : 15 1 14 1 14 1

Input : geeksforgeeks
Output : 6 5 0 10 18 8 15 18 6 6 0 6 6 

```

下面是上面解释的 idea 代码:

```
// C program to find move to front transform of
// a given string
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Returns index at which character of the input text
// exists in the list
int search(char input_char, char* list)
{
    int i;
    for (i = 0; i < strlen(list); i++) {
        if (list[i] == input_char) {
            return i;
            break;
        }
    }
}

// Takes curr_index of input_char as argument
// to bring that character to the front of the list
void moveToFront(int curr_index, char* list)
{
    char* record = (char*)malloc(sizeof(char) * 26);
    strcpy(record, list);

    // Characters pushed one position right
    // in the list up until curr_index
    strncpy(list + 1, record, curr_index);

    // Character at curr_index stored at 0th position
    list[0] = record[curr_index];
}

// Move to Front Encoding
void mtfEncode(char* input_text, int len_text, char* list)
{
    int i;
    int* output_arr = (int*)malloc(len_text * sizeof(int));

    for (i = 0; i < len_text; i++) {

        // Linear Searches the characters of input_text 
        // in list
        output_arr[i] = search(input_text[i], list);

        // Printing the Move to Front Transform
        printf("%d ", output_arr[i]);

        // Moves the searched character to the front 
        // of the list
        moveToFront(output_arr[i], list);
    }
}

// Driver program to test functions above
int main()
{
    char* input_text = "panama";
    int len_text = strlen(input_text);

    // Maintains an ordered list of legal symbols
    char* list = (char*)malloc(sizeof(char) * 26);
    strcpy(list, "abcdefghijklmnopqrstuvwxyz");

    printf("Input text: %s", input_text);
    printf("\nMove to Front Transform: ");

    // Computes Move to Front transform of given text
    mtfEncode(input_text, len_text, list);

    return 0;
}
```

**输出:**

```
Input text: panama
Move to Front Transform: 15 1 14 1 14 1

```

**时间复杂度:** O(n^2)

**练习:**执行移动到前方变换的逆变换。