# 串联形成回文字符串的字符串对的计数

> 原文：[https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/](https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/)

给定由 **N** 个字符串组成的数组 **A []** ，任务是计算在合并后形成**回文字符串**或 重新排列以形成[回文字符串](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

**示例**：

> **输入**：N = 6，A [] = {aab，abcac，dffe，ed，aa，aade}
> **输出**：6
> **说明： HTG7]
> 所有可能产生回文字符串的字符串对：
> {aab，abcac} = aabccbaa
> {aab，aa} = aabaa
> {abcac，aa} = aacbcaa
> { dffe，ed} = fdeedf
> {dffe，aade} = edfaafde
> {ed，aade} = edaade 或 aeddea
> 因此，可能的总对数= 6**
> 
> **输入**：N = 3，A [] = {aa，bb，cd}
> **输出**：1
> **说明**：
> The 仅会产生回文字符串的可能的字符串对：
> {aa，bb} = abba
> 因此，总可能的对= 1

**天真的方法**：

解决此问题的最简单方法是从给定数组生成所有可能的对，并将这些对合并以生成新的字符串。 对于每个合并的字符串，[都会生成字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能排列，对于每个排列，请检查其是否为回文字符串，并相应地增加计数。

***时间复杂度**：O（N <sup>2</sup> * L！* L），其中 L 是字符串的最大长度。*

***辅助空间**：O（M）*

**有效方法**：

当 ***最多一个字符*** 具有 ***奇数*** 时，总是可以形成回文串 ]出现，其余每个字符均出现一次。 由于允许重新排列合并字符串中的字符，因此我们只需要计算合并字符串中字符的频率，并检查其是否满足回文字符串。

> **插图**：
> **1.每个字符都有偶数出现**
> 字符串**“ aab”** 和**“ abcac”** 可以合并 并重新排列以形成回文字符串“ **aababcac”** ，每个字符具有偶数频率
> 
> **2.一个字符具有奇数出现**
> 字符串**“ aab”** 和**“ aa”** 可以合并形成回文字符串“ **aabaa” 具有字符（**'b'**）的**具有奇数频率，其余字符具有偶数频率。

因此，可以观察到可以将两对以下类型的字符串合并成回文字符串：

*   两个字符串中每个字符的频率都是 ***相同*** 。

*   两个字符串中最多一个字符具有 ***不同的*** 频率。

请按照以下步骤解决问题：

*   遍历给定的数组并为每个字符串存储每个字符的频率。

*   为每个频率分配 ***奇偶校验（0** 或 **1）*** 。 将 **0** 分配给偶数频率，将 **1** 分配给奇数频率。

*   初始化映射以存储每个生成的频率阵列的频率。

*   由于允许重新排列，因此请反转每个字符的奇偶校验并将频率数组包括在映射中。

*   最后，返回相似频率阵列的总数，这将给出所需的对数。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to find  
// palindromic string  
#include <bits/stdc++.h>  
using namespace std;  

int getCount(int N, vector<string>& s)  
{  
    // Stores frequency array  
    // and its count  
    map<vector<int>, int> mp;  

    // Total number of pairs  
    int ans = 0;  

    for (int i = 0; i < N; i++) {  

        // Initializing array of size 26  
        // to store count of character  
        vector<int> a(26, 0);  

        // Counting occurrence of each  
        // character of current string  
        for (int j = 0; j < s[i].size(); j++) {  

            a[s[i][j] - 'a']++;  
        }  

        // Convert each count to parity(0 or 1)  
        // on the basis of its frequency  
        for (int j = 0; j < 26; j++) {  

            a[j] = a[j] % 2;  
        }  

        // Adding to anser  
        ans += mp[a];  

        // Frequency of single character  
        // can be possibly changed,  
        // so change its parity  
        for (int j = 0; j < 26; j++) {  

            vector<int> changedCount = a;  

            if (a[j] == 0)  
                changedCount[j] = 1;  
            else
                changedCount[j] = 0;  

            ans += mp[changedCount];  
        }  

        mp[a]++;  
    }  

    return ans;  
}  

int main()  
{  
    int N = 6;  
    vector<string> A  
        = { "aab", "abcac", "dffe",  
            "ed", "aa", "aade" };  

    cout << getCount(N, A);  

    return 0;  
} 

```

## Java

```java

// Java program to find  
// palindromic string  
import java.util.*; 

class GFG{ 

static int getCount(int N, List<String> s)  
{  

    // Stores frequency array  
    // and its count  
    Map<List<Integer>, Integer> mp = new HashMap<>();  

    // Total number of pairs  
    int ans = 0;  

    for(int i = 0; i < N; i++) 
    {  

        // Initializing array of size 26  
        // to store count of character  
        List<Integer> a = new ArrayList<>(26); 
        for(int k = 0; k < 26; k++) 
            a.add(0); 

        // Counting occurrence of each  
        // character of current string  
        for(int j = 0; j < s.get(i).length(); j++) 
        {  
            a.set((s.get(i).charAt(j) - 'a'), 
             a.get(s.get(i).charAt(j) - 'a') + 1);  
        }  

        // Convert each count to parity(0 or 1)  
        // on the basis of its frequency  
        for(int j = 0; j < 26; j++) 
        {  
            a.set(j, a.get(j) % 2); 
        }  

        // Adding to anser  
        ans += mp.getOrDefault(a, 0);  

        // Frequency of single character  
        // can be possibly changed,  
        // so change its parity  
        for(int j = 0; j < 26; j++)  
        {  
            List<Integer> changedCount = new ArrayList<>(); 
            changedCount.addAll(a); 

            if (a.get(j) == 0)  
                changedCount.set(j, 1);  
            else
                changedCount.set(j, 0);  

            ans += mp.getOrDefault(changedCount, 0);  
        }  
        mp.put(a, mp.getOrDefault(a, 0) + 1); 
    }  
    return ans;  
} 

// Driver code 
public static void main (String[] args) 
{ 
    int N = 6;  
    List<String> A = Arrays.asList("aab", "abcac", 
                                   "dffe", "ed",  
                                   "aa", "aade");  

    System.out.print(getCount(N, A));  
} 
} 

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program to find  

> 原文：[https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/](https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/)
# palindromic string  

> 原文：[https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/](https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/)
from collections import defaultdict  

def getCount(N, s):  

    # Stores frequency array  
    # and its count  
    mp = defaultdict(lambda: 0)  

    # Total number of pairs  
    ans = 0

    for i in range(N):  

        # Initializing array of size 26  
        # to store count of character  
        a = [0] * 26

        # Counting occurrence of each  
        # character of current string  
        for j in range(len(s[i])):  
            a[ord(s[i][j]) - ord('a')] += 1

        # Convert each count to parity(0 or 1)  
        # on the basis of its frequency  
        for j in range(26):  
            a[j] = a[j] % 2

        # Adding to anser  
        ans += mp[tuple(a)]  

        # Frequency of single character  
        # can be possibly changed,  
        # so change its parity  
        for j in range(26):  
            changedCount = a[:]  
            if (a[j] == 0):  
                changedCount[j] = 1
            else:  
                changedCount[j] = 0
            ans += mp[tuple(changedCount)]  

        mp[tuple(a)] += 1

    return ans  

# Driver code  

> 原文：[https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/](https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/)
if __name__ == '__main__':  

    N = 6
    A = [ "aab", "abcac", "dffe",  
        "ed", "aa", "aade" ]  

    print(getCount(N, A))  

# This code is contributed by Shivam Singh  

> 原文：[https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/](https://www.geeksforgeeks.org/count-of-pairs-of-strings-whose-concatenation-forms-a-palindromic-string/)

```

**Output:** 

```
6

```

***时间复杂度**：O（N *（L + log（N））），其中 L 是字符串的最大长度*

***辅助空间**：O（N）*



* * *

* * *



