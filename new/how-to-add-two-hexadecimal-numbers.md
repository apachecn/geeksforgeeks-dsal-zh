# 如何将两个十六进制数字相加

> 原文：[https://www.geeksforgeeks.org/how-to-add-two-hexadecimal-numbers/](https://www.geeksforgeeks.org/how-to-add-two-hexadecimal-numbers/)

给定两个十六进制数字 **str1** 和 **str2** ，任务是将两个十六进制数相加。

> [**十六进制数字**](https://www.geeksforgeeks.org/arithmetic-operations-of-hexadecimal-numbers/) 系统通常缩写为“十六进制”，它是由 16 个符号组成的数字系统。 它使用十进制数字系统中的 10 个符号（由 0-9 表示）和六个额外的符号 A-F（代表十进制 10-15）。

**示例**：

> **输入**：`str1 = "01B", str2 = "378"`
>
> **输出**：393
>
> **解释**：
>
> `B (十进制 11) + 8 = 19 (十六进制 13)`，因此加法位 = 3，进位为 1
>
> `1 + 7 + 1 (进位) = 9`，因此加法位为 9，进位为 0
>
> `0 + 3 + 0 (进位) = 3`，因此加法位为 3，进位为 0
>
> `01B + 378 = 393`
> 
> **输入**：`str1 = "AD", str2 = "1B"`
>
> **输出**：C8
>
> **说明**：
>
> `D (十进制 13) + B(十进制 11) = 24 (十六进制 18)`，因此加法位为 8，进位为 1
>
> `A (十进制 10) + 1 + 1 (进位)= 12 (十六进制 C)`，因此加法位为 C，进位为 0
>
> `AD + 1B = C8`  

**方法**：的想法是使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)模板来存储从**十六进制到十进制**和**十进制到十六进制**的映射值。

1.  迭代直到给定字符串之一达到其长度。

2.  从进位零开始，从末尾将两个数字（带有进位）相加，并在每次加法中更新进位。

3.  在另一个字符串的剩余长度上执行相同的操作（如果两个字符串的长度不同）。

4.  返回已添加的值。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Map for converting hexadecimal 
// values to decimal 
map<char, int> hex_value_of_dec(void) 
{ 
    // Map the values to decimal values 
    map<char, int> m{ { '0', 0 }, { '1', 1 },  
                      { '2', 2 }, { '3', 3 },  
                      { '4', 4 }, { '5', 5 },  
                      { '6', 6 }, { '7', 7 },  
                      { '8', 8 }, { '9', 9 },  
                      { 'A', 10 }, { 'B', 11 },  
                      { 'C', 12 }, { 'D', 13 },  
                      { 'E', 14 }, { 'F', 15 } }; 

    return m; 
} 

// Map for converting decimal values 
// to hexadecimal 
map<int, char> dec_value_of_hex(void) 
{ 
    // Map the values to the 
    // hexadecimal values 
    map<int, char> m{ { 0, '0' }, { 1, '1' },  
                      { 2, '2' }, { 3, '3' },  
                      { 4, '4' }, { 5, '5' },  
                      { 6, '6' }, { 7, '7' },  
                      { 8, '8' }, { 9, '9' },  
                      { 10, 'A' }, { 11, 'B' },  
                      { 12, 'C' }, { 13, 'D' },  
                      { 14, 'E' }, { 15, 'F' } }; 

    return m; 
} 

// Function to add the two hexadecimal numbers 
string Add_Hex(string a, string b) 
{ 
    map<char, int> m = hex_value_of_dec(); 
    map<int, char> k = dec_value_of_hex(); 

    // Check if length of string first is 
    // greater than or equal to string second 
    if (a.length() < b.length()) 
        swap(a, b); 

    // Store length of both strings 
    int l1 = a.length(), l2 = b.length(); 

    string ans = ""; 

    // Initialize carry as zero 
    int carry = 0, i, j; 

    // Traverse till second string 
    // get traversal completely 
    for (i = l1 - 1, j = l2 - 1; 
         j >= 0; i--, j--) { 

        // Decimal value of element at a[i] 
        // Decimal value of element at b[i] 
        int sum = m[a[i]] + m[b[j]] + carry; 

        // Hexadecimal value of sum%16 
        // to get addition bit 
        int addition_bit = k[sum % 16]; 

        // Add addition_bit to answer 
        ans.push_back(addition_bit); 

        // Update carry 
        carry = sum / 16; 
    } 

    // Traverse remaining element 
    // of string a 
    while (i >= 0) { 

        // Decimal value of element 
        // at a[i] 
        int sum = m[a[i]] + carry; 

        // Hexadecimal value of sum%16 
        // to get addition bit 
        int addition_bit = k[sum % 16]; 

        // Add addition_bit to answer 
        ans.push_back(addition_bit); 

        // Update carry 
        carry = sum / 16; 
        i--; 
    } 

    // Check if still carry remains 
    if (carry) { 
        ans.push_back(k[carry]); 
    } 

    // Reverse the final string 
    // for desired output 
    reverse(ans.begin(), ans.end()); 

    // Return the answer 
    return ans; 
} 

// Driver Code 
int main(void) 
{ 
    // Initialize the hexadecimal values 
    string str1 = "1B", str2 = "AD"; 

    // Function call 
    cout << Add_Hex(str1, str2) << endl; 
} 

```

**Output:**

```
C8

```

**时间复杂度**：`O(max(N, M))`，其中字符串第一和第二的长度为`N`和`M`。

**辅助空间**：`O(max(N, M))`，其中字符串`first`和`second`的长度为`N`和`M`。



* * *

* * *



