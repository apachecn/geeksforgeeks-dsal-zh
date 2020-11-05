# 在长度为`K`的所有完全平方中，可能是最长的异序词集中最大的数字。

> 原文：[https://www.geeksforgeeks.org/largest-number-from-the-longest-set-of-anagrams-possible-from-all-perfect-squares-of-length-k/](https://www.geeksforgeeks.org/largest-number-from-the-longest-set-of-anagrams-possible-from-all-perfect-squares-of-length-k/)

给定整数`K`，使得存在一组所有可能的[完全平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)，每个长度为`K`。 从这组完美的正方形中，形成一组具有尽可能多的长度的集合，其长度彼此为异序词。 任务是打印在生成的异序词集中存在的最大元素。

**注意**：[如果一组以上最大长度，则打印其中最大的一组](https://www.geeksforgeeks.org/check-if-two-integer-are-anagrams-of-each-other/)。

> 字符串的**字形图**是另一个包含相同字符的字符串，只是字符顺序不同。

**示例**：

> **输入**：`K = 2`
>
> **输出**：81
>
> **说明**：
>
> 长度`K = 2`的所有可能平方为`{16, 25 , 36, 49, 64, 81}`。
>
> 可能的异序词集为`[16], [25], [36], [49], [64], [81]`。
>
> 因此，每个集合的大小相同，即 1。
>
> 在这种情况下，打印包含最大元素的集合，即 81。
> 
> **输入**：`K = 5`
>
> **输出**：96100

**朴素的方法**：最简单的方法是存储所有可能的`K`个长度的完全平方，并使用[递归](http://www.geeksforgeeks.org/recursion/)形成有效的七字组。 然后，找到最长长度集中存在的最大元素。

***时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(n)`*

**高效方法**：该想法基于以下观察结果：对完美正方形的数字进行排序后，异序词数字的顺序变得相等。 步骤如下：

1.  初始化[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，以存储与数字按顺序排列的数字相对应的所有异序词数字。

2.  [生成长度为 **K** 的所有完全平方](https://www.geeksforgeeks.org/print-all-perfect-squares-from-the-given-range/)。

3.  对于生成的每个完全平方，在**映射**中插入对应于其数字以升序排列的数字的数字。

4.  遍历**映射**并从最大长度集中打印最大的数字。

下面是上述方法的实现：

## CPP

```

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Function to find the largest set of 
// perfect squares which are anagram 
// to each other 
void printResult( 
    map<string, set<long long int> > m) 
{ 
    auto max_itr = m.begin(); 

    long long maxi = -1; 

    for (auto itr = m.begin(); 
         itr != m.end(); ++itr) { 

        long long int siz1 
            = (itr->second).size(); 

        // Check if size of maximum set 
        // is less than the current set 
        if (maxi < siz1) { 

            // Update maximum set 
            maxi = siz1; 
            max_itr = itr; 
        } 

        // If lengths are equal 
        else if (maxi == siz1) { 

            // Update maximum set to store 
            // the set with maximum element 
            if ((*(max_itr->second).rbegin()) 
                < *(itr->second.rbegin())) { 
                maxi = siz1; 
                max_itr = itr; 
            } 
        } 
    } 

    // Stores the max element from the set 
    long long int result 
        = *(max_itr->second).rbegin(); 

    // Print final Result 
    cout << result << endl; 
} 

// Function to find the 
// perfect squares wich are anagrams 
void anagramicSquares(long long int k) 
{ 
    // Stores the sequence 
    map<string, set<long long int> > m; 

    // Initialize start and end 
    // of perfect squares 
    long long int end; 
    if (k % 2 == 0) 
        end = k / 2; 
    else
        end = ((k + 1) / 2); 

    long long int start = pow(10, end - 1); 
    end = pow(10, end); 

    // Iterate form start to end 
    for (long long int i = start; 
         i <= end; i++) { 

        long long int x = i * i; 

        // Converting int to string 
        ostringstream str1; 
        str1 << x; 

        string str = str1.str(); 
        if (str.length() == k) { 

            // Sort string for storing 
            // number at exact map position 
            sort(str.begin(), str.end()); 

            // Insert number at map 
            m[str].insert(x); 
        } 
    } 

    // Print result 
    printResult(m); 
} 

// Driver Code 
int main() 
{ 
    // Given K 
    long long int K = 2; 

    // Function Call 
    anagramicSquares(K); 

    return 0; 
} 

```

**Output:**

```
81

```

***时间复杂度**：`O(n)`

**辅助空间**：`O(n)`*



* * *

* * *



