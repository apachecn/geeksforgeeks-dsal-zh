# 根据指定的数组索引反转给定字符串的子字符串

> 原文：[https://www.geeksforgeeks.org/reverse-substrings-of-given-string-according-to-specified-array-indices/](https://www.geeksforgeeks.org/reverse-substrings-of-given-string-according-to-specified-array-indices/)

给定长度为`N`的字符串`str`和整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，对于数组元素`arr[i]`（**基于 1 的索引**），[反转索引`[arr[i], N – arr[i] + 1]`中的子字符串**](https://www.geeksforgeeks.org/reverse-the-substrings-of-the-given-string-according-to-the-given-array-of-indices/)。 任务是在每次反转后打印字符串。

**示例**：

> **输入**：`str = "GeeksforGeeks", arr[] = {2}`
>
> **输出**：`GkeeGrofskees`
>
> **说明**：
>
> 对于数组的第一个元素为 2：
>
> 反转子字符串`(2, 12)`。 现在，更新后的字符串为`"GkeeGrofskees"`。
> 
> **输入**：`str = "abcdef", arr[] = {1,2,3}`
>
> **输出**：`fbdcea`
>
> **说明**：
>
> 对于数组的第一个元素为 1：
>
> 反转子字符串`(1, 6)`。 现在，更新后的字符串为`"fedcba"`。
>
> 对于数组的第二个元素是 2：
>
> 反转子字符串`(2, 5)`。 现在，更新后的字符串为`"fbcdea"`。
>
> 对于数组的第三个元素为 3：
>
> 反转子字符串`(3, 4)`。 现在，更新后的字符串为`"fbdcea"`。

**朴素的方法**：最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并对每个数组元素`arr[i]`[反转子串`{s[arr[i]], …, s[N – arr[i] + 1]}`](https://www.geeksforgeeks.org/reverse-the-substrings-of-the-given-string-according-to-the-given-array-of-indices/)，并打印非常更新后获得的结果字符串。

**时间复杂度**：`O(N * K)`，其中`N`是字符串的长度，`K`是反转的子字符串的最大长度。

**辅助空间**：`O(1)`。

**高效方法**：可以通过跟踪索引处任何字符被反转的次数来优化上述方法。 如果**反向计数是偶数**，则字符将返回其原始位置，因此不会有变化，并且如果**反向计数是奇数**，则字符具有 被交换。 步骤如下：

*   初始化数组`count[]`，以存储在字符串的任何索引处的反转次数。

*   遍历给定数组`arr[]`并将索引`count[arr[i]]`的计数增加`1`。

*   现在，使用变量`i`遍历`[1, N / 2]`范围内的数组`count[]`并执行以下操作：

    *   将当前索引处的元素更新为当前索引与先前索引的和。

    *   现在，如果当前元素`count[i]`为奇数，则交换`str[i]`和`str[N – i + 1]`。

*   完成上述步骤后，打印字符串。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <iostream> 
using namespace std; 

// Function to perform the reversal 
// operation on the given string 
string modifyString(int A[], string str, 
                    int K) 
{ 
    // Size of string 
    int N = str.size(); 

    // Stores the count of indices 
    int count[N + 1] = { 0 }; 

    // Count the positions where 
    // reversals will begin 
    for (int i = 0; i < K; i++) { 
        count[A[i]]++; 
    } 

    for (int i = 1; i <= N / 2; i++) { 

        // Store the count of reversals 
        // beginning at position i 
        count[i] = count[i] + count[i - 1]; 

        // Check if the count[i] is 
        // odd the swap the character 
        if (count[i] & 1) { 
            swap(str[i - 1], str[N - i]); 
        } 
    } 

    // Return the updated string 
    return str; 
} 

// Driver Code 
int main() 
{ 
    // Given string str 
    string str = "abcdef"; 

    // Given array of reversing index 
    int arr[] = { 1, 2, 3 }; 

    int K = sizeof(arr) / sizeof(arr[0]); 

    // Function Call 
    cout << modifyString(arr, str, K); 

    return 0; 
} 

```

**输出**：

```
fbdcea

```

**时间复杂度**：`O(N + K)`，其中`N`是字符串的长度，`K`是反转的子字符串的最大长度。

**辅助空间**：`O(n)`。



* * *

* * *



