# C 程序，用于检查两个给定的字符串是否彼此同构

给定两个字符串`str1`和`str2`，任务是检查两个给定字符串[是否彼此同构](https://www.geeksforgeeks.org/check-if-two-given-strings-are-isomorphic-to-each-other/)。

> 如果`str1`的每个字符到`str2`的每个字符都有一个**一对一的映射**，则说两个字符串是**同构**。 并且`str1`中每个字符的所有出现都映射到`str2`中的相同字符。

**示例**：

> **输入**：`str1 = "egg"`，`str2 ="add"`
> 
> **输出**：是
> 
> **说明**：
> 
> `str1`中的 ASCII 值 101 的`'e'`映射为`str2`中的 ASCII 值 97 的`'a'`。`str1`中 ASCII 值 103 的`'g'`映射为`str2`中的 ASCII 值 100 的`'d'`。
> 
> **输入**：`str1 ="蛋"，str2 ="添加"`
> 
> **输出**：否

[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)方法：有关基于[`Hashmap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)的方法，请参考[先前的文章](https://www.geeksforgeeks.org/check-if-two-given-strings-are-isomorphic-to-each-other/)。
***时间复杂度**：`O(N)`
**辅助空间**：`O(256)`

[基于 ASCII 值](https://en.wikipedia.org/wiki/ASCII#Character_order)的方法：该想法与上述方法类似。 请按照以下步骤解决问题：

1.  初始化大小为 256 的两个数组。
2.  [遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符，并在`i`位置递增等于该字符的 ASCII 值的索引。
3.  如果在字符映射中没有冲突，则打印`Yes`。 否则，打印`No`。

下面是上述方法的实现：

## C

```c

// C Program to implement 
// the above approach 

#include <stdio.h> 
#include <string.h> 
#include <stdbool.h> 

// Function to check and return if strings 
// str1 and str2 are ismorphic 
bool areIsomorphic(char *str1, char *str2) 
{ 
    // If the length of the strings 
    // are not equal 
    if (strlen(str1) != strlen(str2)) { 
        return false; 
    } 

    // Initialise two arrays 
    int arr1[256] = { 0 }, arr2[256] = { 0 }; 

    // Travsersing both the strings 
    for (int i = 0; i < strlen(str1); i++) { 

        // If current characters don't map 
        if (arr1[(int)str1[i]]  
        != arr2[(int)str2[i]]) { 
            return false; 
        } 

        // Increment the count of characters 
        // at their respective ASCII indices 
        arr1[(int)str1[i]]++; 
        arr2[(int)str2[i]]++; 
    } 
    return true; 
} 

// Driver Code 
int main() 
{ 
    char s1[] = "aab", s2[] = "xxy"; 

    if (areIsomorphic(s1, s2)) 
        printf("Yes\n"); 
    else
        printf("No\n"); 

    return 0; 
} 

```

**Output:**

```
Yes

```

***时间复杂度**：`O(N)`
**辅助空间**：`O(256)`



* * *

* * *



