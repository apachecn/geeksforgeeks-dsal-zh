# 通过重复附加和修剪来构建二元回文

> 原文： [https://www.geeksforgeeks.org/construct-binary-palindrome-by-repeated-appending-and-trimming/](https://www.geeksforgeeks.org/construct-binary-palindrome-by-repeated-appending-and-trimming/)

在给定 n 和 k 的情况下，使用大小为 k 的二进制数重复构造自身以包裹在回文中，以构造大小为 n 的回文。 **回文必须始终以 1 开头，并且最大数目为零。**

**示例**：

```
Input : n = 5,  k = 3
Output : 11011 
Explanation : the 3 sized substring is
110 combined twice and trimming the extra 
0 in the end to give 11011.

Input : n = 2,  k = 8
Output : 11 
Explanation : the 8 sized substring is 11...... 
wrapped to two places to give 11.

```

**天真的方法**将尝试从 1 开始的每个大小为 k 的回文，以便形成大小为 n 的回文。 这种方法具有指数复杂性。

**更好的方法**进行此操作是使用索引初始化 k 大小的二进制数，并以应有的方式连接回文。 像回文的最后一个字符应该匹配到第一个一样，找出那些索引将出现在那些位置并将它们链接起来。 将与第 0 个索引链接的每个字符设置为 1，然后字符串就准备好了。 这种方法将具有线性复杂性。

在这种方法中，首先放置 k 个大小二进制文件的索引以保存到数组中，例如，如果 n = 7，则 k = 3 arr 变为[0，1，2，0，1，2，0]。 接着在 connectchars 图中，通过回文的第 k 个属性和第（n – k – 1）个变量应相同的属性来连接应该为 k 大小的二进制数的索引，从而将 0 链接到 1 （反之亦然），则 1 链接到 2（反之亦然），依此类推。 之后，使用 dfs 方法检查 connectchars 数组中与 0 链接的内容，并使所有关联的索引为 1（因为第一个数字应为非零）。 在 dfs 中，传递 0，最终答案字符串和图形。 首先，使父级 1 并检查其子级是否为零，是否使它们及其子级 1 为零。这仅使 k 大小的字符串的所需索引为 1，其他索引为零。 最后，答案包含从 0 到 k – 1 的索引，并且对应于打印数字的 arr。

## C++

```cpp

// CPP code to form binary palindrome 
#include <iostream> 
#include <vector> 
using namespace std; 

// function to apply DFS 
void dfs(int parent, int ans[], vector<int> connectchars[]) 
{ 
    // set the parent marked 
    ans[parent] = 1; 

    // if the node has not been visited set it and 
    // its children marked 
    for (int i = 0; i < connectchars[parent].size(); i++) { 
        if (!ans[connectchars[parent][i]]) 
            dfs(connectchars[parent][i], ans, connectchars); 
    } 
} 

void printBinaryPalindrome(int n, int k) 
{ 
    int arr[n], ans[n] = { 0 }; 

    // link which digits must be equal 
    vector<int> connectchars[k]; 

    for (int i = 0; i < n; i++) 
        arr[i] = i % k; 

    // connect the two indices 
    for (int i = 0; i < n / 2; i++) { 
        connectchars[arr[i]].push_back(arr[n - i - 1]); 
        connectchars[arr[n - i - 1]].push_back(arr[i]); 
    } 

    // set everything connected to  
    // first character as 1 
    dfs(0, ans, connectchars); 

    for (int i = 0; i < n; i++) 
        cout << ans[arr[i]]; 
} 

// driver code 
int main() 
{ 
    int n = 10, k = 4; 
    printBinaryPalindrome(n, k); 
    return 0; 
} 

```