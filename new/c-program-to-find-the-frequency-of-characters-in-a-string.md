# C 程序，用于查找字符串中的字符频率

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 包含小写英文字符，任务是[查找字符串](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)中所有字符的频率。

**示例**：

> **输入**：S =“ geeksforgeeks”
> **输出**：
> e – 4
> f – 1
> g – 2
> k – 2
> o – 1
> r – 1
> s – 2
> 
> **输入**：S =“ gfg”
> **输出**：
> f – 1
> g – 2

**方法**：请按照以下步骤解决问题：

1.  初始化数组 **freq []** ，以将每个字母的[频率存储在给定的字符串](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)中。 **0** <sup>第</sup>索引存储字符' **a'**的频率，1 <sup>st / sup >索引存储字符' b'，依此类推。</sup>
2.  [迭代给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** ，并通过执行 **freq [S [i] –'a' ] + = 1** 。 如果 **S [i] ='a'**，则 **S [i] –'a'**等于 0，因此'a'的频率在数组中增加。
3.  完整遍历字符串后，[通过遍历数组](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/) **freq []** 来打印字符串中所有字符的频率。

下面是上述方法的实现：

## C

```c

// C program for the above approach 
#include <stdio.h> 
#include <string.h> 

// Function to print the frequencies 
// of each character of the string 
void printFrequency(int freq[]) 
{ 
    for (int i = 0; i < 26; i++) { 

        // If frequency of the 
        // alphabet is non-zero 
        if (freq[i] != 0) { 

            // Print the character and 
            // its respective frequency 
            printf("%c - %d\n", 
                   i + 'a', freq[i]); 
        } 
    } 
} 

// Function to calculate the frequencies 
// of each character of the string 
void findFrequncy(char S[]) 
{ 
    int i = 0; 

    // Stores the frequencies 
    // of each character 
    int freq[26] = { 0 }; 

    // Traverse over the string 
    while (S[i] != '\0') { 

        // Increment the count of 
        // each character by 1 
        freq[S[i] - 'a']++; 

        // Increment the index 
        i++; 
    } 

    // Function call to print 
    // the frequencies 
    printFrequency(freq); 
} 

// Driver Code 
int main() 
{ 
    char S[100] = "geeksforgeeks"; 
    findFrequncy(S); 
}

```

**Output:**

```
e - 4
f - 1
g - 2
k - 2
o - 1
r - 1
s - 2

```

***时间复杂度**：O（N）*
***辅助空间**：O（26）*



* * *

* * *



