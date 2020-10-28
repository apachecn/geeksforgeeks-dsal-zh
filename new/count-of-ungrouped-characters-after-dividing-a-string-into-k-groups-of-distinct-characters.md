# 将字符串分成 K 组不同字符后的未分组字符数

给定大小为 **N** 的小写字母字符串**“ S”** ，以及整数 **K** ； 任务是在将给定的字符串分成 K 组不同的字符后，找到将保持未分组的字符数。

**范例**：

> **输入**：S =“保持居家生活”，K = 1
> **输出**：6
> **说明**：
> 在字符串 S 中其元素为 发生不止一次是'e'-> 3 次，'s'-> 3 次，'a'-> 2 次，'i'-> 2 次并休息所有元素 每次发生 1 次。
> 由于 K = 1 只能形成一个基团，因此这些元素中只有一个副本存在，其余所有元素都不能在该组中。
> 因此， 组是 2 次'e'，2 次's'，1 次'a'和 1 次'i'。
> 剩余元素总数为 6。
> 
> **输入**：S =“保持居家生活”，K = 2
> **输出**：2
> **说明**：
> 在字符串 S 中其元素为 发生不止一次是'e'-> 3 次，'s'-> 3 次，'a'-> 2 次，'i'-> 2 次并休息所有元素 每次发生 1 次。
> 由于可以形成 2 个组，所以一组包含所有元素的 1 个副本。 第二组将包含 1 个额外元素的副本，即“ e”，“ s”，“ a”和“ i”。 将被忽略的元素是 1 次“ e”和 1 次“ s”。
> 遗漏的元素总数为 2。

**方法**：这个想法是使用[频率计数](https://www.geeksforgeeks.org/basic/frequency-counting/)。

1.  创建一个哈希数据结构，以存储字符“ a”-“ z”的频率。

2.  在给定的字符串中找到每个字符的初始频率，并将其存储在哈希数据结构中。

3.  由于组只能包含 1 个字符。 因此，请从散列数据结构中每个字符的出现次数减少 K。

4.  现在，在哈希数据结构中添加字符的其余频率。 这将是保持未分组的所需字符数。

下面是上述方法的实现：

## C++

```cpp

// C++ code to implement the above approach 

#include <bits/stdc++.h> 
using namespace std; 

void findUngroupedElement(string s, 
                          int k) 
{ 

    int n = s.length(); 

    // create array where 
    // index represents alphabets 
    int b[26]; 

    for (int i = 0; i < 26; i++) 
        b[i] = 0; 

    // fill count of every 
    // alphabet to corresponding 
    // array index 
    for (int i = 0; i < n; i++) { 
        char p = s.at(i); 
        b[p - 'a'] += 1; 
    } 

    int sum = 0; 

    // count for every element 
    // how much is exceeding 
    // from no. of groups then 
    // sum them 
    for (int i = 0; i < 26; i++) { 
        if (b[i] > k) 
            sum += b[i] - k; 
    } 

    // print answer 
    cout << sum << endl; 
} 

// Driver code 
int main() 
{ 
    string s = "stayinghomesaveslife"; 
    int k = 1; 

    findUngroupedElement(s, k); 

    return 0; 
} 

```

## Java

```java

// Java code to implement the above approach 
import java.util.*; 

class GFG{ 

static void findUngroupedElement(String s, 
                                 int k) 
{ 
    int n = s.length(); 

    // Create array where 
    // index represents alphabets 
    int []b = new int[26]; 

    for(int i = 0; i < 26; i++) 
        b[i] = 0; 

    // Fill count of every 
    // alphabet to corresponding 
    // array index 
    for(int i = 0; i < n; i++)  
    { 
        char p = s.charAt(i); 
        b[p - 'a'] += 1; 
    } 

    int sum = 0; 

    // Count for every element 
    // how much is exceeding 
    // from no. of groups then 
    // sum them 
    for(int i = 0; i < 26; i++) 
    { 
        if (b[i] > k) 
            sum += b[i] - k; 
    } 

    // Print answer 
    System.out.println(sum); 
} 

// Driver code 
public static void main(String srgs[]) 
{ 
    String s = "stayinghomesaveslife"; 
    int k = 1; 

    findUngroupedElement(s, k); 
} 
} 

// This code is contributed by ANKITKUMAR34 

```

## Python3

```py

# Python3 code to implement the above approach 
def findUngroupedElement(s, k): 

    n = len(s); 

    # Create array where 
    # index represents alphabets 
    b = [0] * 26

    # Fill count of every 
    # alphabet to corresponding 
    # array index 
    for i in range(n): 
        p = s[i] 
        b[ord(p) - ord('a')] += 1

    sum = 0; 

    # Count for every element 
    # how much is exceeding 
    # from no. of groups then 
    # sum them 
    for i in range(26): 
        if (b[i] > k): 
            sum += b[i] - k 

    # Print answer 
    print(sum) 

# Driver code 
s = "stayinghomesaveslife"
k = 1

findUngroupedElement(s, k) 

# This code is contributed by ANKITKUMAR34 

```

## C#

```cs

// C# code to implement the above approach 
using System; 

class GFG{ 

static void findUngroupedElement(String s, 
                                 int k) 
{ 
    int n = s.Length; 

    // Create array where 
    // index represents alphabets 
    int []b = new int[26]; 

    for(int i = 0; i < 26; i++) 
        b[i] = 0; 

    // Fill count of every 
    // alphabet to corresponding 
    // array index 
    for(int i = 0; i < n; i++)  
    { 
        char p = s[i]; 
        b[p - 'a'] += 1; 
    } 

    int sum = 0; 

    // Count for every element 
    // how much is exceeding 
    // from no. of groups then 
    // sum them 
    for(int i = 0; i < 26; i++) 
    { 
        if (b[i] > k) 
            sum += b[i] - k; 
    } 

    // Print answer 
    Console.WriteLine(sum); 
} 

// Driver code 
public static void Main(String []srgs) 
{ 
    String s = "stayinghomesaveslife"; 
    int k = 1; 

    findUngroupedElement(s, k); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:** 

```
6

```

***时间复杂度**：O（N）*

***辅助空间复杂度**：O（26）等效于 O（1）*



* * *

* * *



