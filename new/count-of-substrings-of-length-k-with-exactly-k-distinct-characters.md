# 长度为`K`的子字符串的计数，其中恰好有`K`个不同的字符

> 原文：[https://www.geeksforgeeks.org/count-of-substrings-of-length-k-with-exactly-k-distinct-characters/](https://www.geeksforgeeks.org/count-of-substrings-of-length-k-with-exactly-k-distinct-characters/)

给定一个小写字母的字符串`str`和一个整数`K`，任务是计算长度为`K`的所有子字符串，这些子字符串的正好为`K`不同的字符。

**示例**：

> **输入**：`str = "abcc", K = 2`
>
> **输出**：2
>
> **说明**：
>
> 长度为`K = 2`的可能子串是：
>
> `ab`：2 个不同的字符
>
> `bc`：2 个不同的字符
>
> `cc`：1 个不同的字符
>
> 仅存在两个有效的子字符串`{"ab", "bc"}`。
> 
> **输入**：`str = "aabab", K = 3`
>
> **输出**：0
>
> **说明**：
>
> 长度为`K = 3`的可能子串 是
>
> `aab`：2 个不同的字符
>
> `aba`：2 个不同的字符
>
> `bab`：2 个不同的字符
>
> 不存在长度为 3 的子字符串，而恰好有 3 个不同的字符

**朴素的方法**：

这个想法是生成所有长度为`K`的子字符串，并为每个子字符串计数不同字符。 如果字符串的长度为`N`，则可以有`N – K + 1`个子字符串，长度为`K`。 生成这些子字符串将需要`O(n)`复杂度，而检查每个子字符串将需要`O(K)`复杂度，因此将整体复杂度设为`O(N * K)`。

**高效方法**：

这个想法是使用[窗口滑动技术](https://www.geeksforgeeks.org/window-sliding-technique/)。 保持大小为`K`的窗口，并使用[`HashMap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)保留窗口中所有字符的计数。 遍历字符串会减少`HashMap`中前一个窗口的第一个字符的计数，并增加当前窗口的最后一个字符的频率。 如果在长度为`K`的窗口中不同字符的计数等于`K`，则将答案增加 1。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the  
// count of k length substrings  
// with k distinct characters  
// using sliding window  
#include <bits/stdc++.h>  
using namespace std;  

// Function to return the  
// required count of substrings  
int countSubstrings(string str, int K)  
{  
    int N = str.size();  
    // Store the count  
    int answer = 0;  

    // Store the count of  
    // distinct characters  
    // in every window  
    unordered_map<char, int> map;  

    // Store the frequency of  
    // the first K length substring  
    for (int i = 0; i < K; i++) {  

        // Increase frequency of  
        // i-th character  
        map[str[i]]++;  
    }  

    // If K distinct characters  
    // exist  
    if (map.size() == K)  
        answer++;  

    // Traverse the rest of the  
    // substring  
    for (int i = K; i < N; i++) {  

        // Increase the frequency  
        // of the last character  
        // of the current substring  
        map[str[i]]++;  
        // Decrease the frequency  
        // of the first character  
        // of the previous substring  
        map[str[i - K]]--;  

        // If the character is not present  
        // in the current substring  
        if (map[str[i - K]] == 0) {  
            map.erase(str[i - K]);  
        }  

        // If the count of distinct  
        // characters is 0  
        if (map.size() == K) {  
            answer++;  
        }  
    }  

    // Return the count  
    return answer;  
}  

// Driver code  
int main()  
{  
    // string str  
    string str = "aabcdabbcdc";  

    // integer K  
    int K = 3;  

    // Print the count of K length  
    // substrings with k distinct characters  
    cout << countSubstrings(str, K) << endl;  

    return 0;  
}  

```

## Java

```java

// Java program to find the count  
// of k length substrings with k  
// distinct characters using  
// sliding window  
import java.util.*;  

class GFG{  

// Function to return the  
// required count of substrings  
public static int countSubstrings(String str,  
                                int K)  
{  
    int N = str.length();  

    // Store the count  
    int answer = 0;  

    // Store the count of  
    // distinct characters  
    // in every window  
    Map<Character,  
        Integer> map = new HashMap<Character,  
                                Integer>();  

    // Store the frequency of  
    // the first K length substring  
    for(int i = 0; i < K; i++)  
    {  

        // Increase frequency of  
        // i-th character  
        if (map.get(str.charAt(i)) == null)  
        {  
            map.put(str.charAt(i), 1);  
        }  
        else
        {  
            map.put(str.charAt(i),  
            map.get(str.charAt(i)) + 1);  
        }  
    }  

    // If K distinct characters  
    // exist  
    if (map.size() == K)  
        answer++;  

    // Traverse the rest of the  
    // substring  
    for(int i = K; i < N; i++)  
    {  

        // Increase the frequency  
        // of the last character  
        // of the current substring  
        if (map.get(str.charAt(i)) == null)  
        {  
            map.put(str.charAt(i), 1);  
        }  
        else
        {  
            map.put(str.charAt(i),  
            map.get(str.charAt(i)) + 1);  
        }  

        // Decrease the frequency  
        // of the first character  
        // of the previous substring  
        map.put(str.charAt(i - K),  
        map.get(str.charAt(i - K)) - 1);  

        // If the character is not present  
        // in the current substring  
        if (map.get(str.charAt(i - K)) == 0)  
        {  
            map.remove(str.charAt(i - K));  
        }  

        // If the count of distinct  
        // characters is 0  
        if (map.size() == K)  
        {  
            answer++;  
        }  
    }  

    // Return the count  
    return answer;  
}  

// Driver code  
public static void main(String[] args)  
{  

    // string str  
    String str = "aabcdabbcdc";  

    // integer K  
    int K = 3;  

    // Print the count of K length  
    // substrings with k distinct characters  
    System.out.println(countSubstrings(str, K));  
}  
}  

// This code is contributed by grand_master  

```

## Python3

```py

# Python3 program to find the  
# count of k length substrings  
# with k distinct characters  
# using sliding window  

# Function to return the  
# required count of substrings  
def countSubstrings(str, K):  

    N = len(str)  

    # Store the count  
    answer = 0

    # Store the count of  
    # distinct characters  
    # in every window  
    map = {}  

    # Store the frequency of  
    # the first K length substring  
    for i in range(K):  

        # Increase frequency of  
        # i-th character  
        map[str[i]] = map.get(str[i], 0) + 1

    # If K distinct characters  
    # exist  
    if (len(map) == K):  
        answer += 1

    # Traverse the rest of the  
    # substring  
    for i in range(K, N):  

        # Increase the frequency  
        # of the last character  
        # of the current substring  
        map[str[i]] = map.get(str[i], 0) + 1

        # Decrease the frequency  
        # of the first character  
        # of the previous substring  
        map[str[i - K]] -= 1

        # If the character is not present  
        # in the current substring  
        if (map[str[i - K]] == 0):  
            del map[str[i - K]]  

        # If the count of distinct  
        # characters is 0  
        if (len(map) == K):  
            answer += 1

    # Return the count  
    return answer  

# Driver code  
if __name__ == '__main__':  

    str = "aabcdabbcdc"

    # Integer K  
    K = 3

    # Print the count of K length  
    # substrings with k distinct characters  
    print(countSubstrings(str, K))  

# This code is contributed by mohit kumar 29  

```

## C#

```cs

// C# program to find the count 
// of k length substrings with k  
// distinct characters using  
// sliding window  
using System; 
using System.Collections.Generic;  

class GFG{ 

// Function to return the  
// required count of substrings  
public static int countSubstrings(string str, 
                                  int K)  
{  
    int N = str.Length; 

    // Store the count  
    int answer = 0;  

    // Store the count of  
    // distinct characters  
    // in every window  
    Dictionary<char,  
               int> map = new Dictionary<char,  
                                         int>();  

    // Store the frequency of  
    // the first K length substring  
    for(int i = 0; i < K; i++)  
    {  

        // Increase frequency of  
        // i-th character 
        if(!map.ContainsKey(str[i])) 
        { 
            map[str[i]] = 1; 
        } 
        else
        { 
            map[str[i]]++;  
        } 
    }  

    // If K distinct characters  
    // exist  
    if (map.Count == K)  
        answer++;  

    // Traverse the rest of the  
    // substring  
    for(int i = K; i < N; i++) 
    {  

        // Increase the frequency  
        // of the last character  
        // of the current substring  
        if(!map.ContainsKey(str[i])) 
        { 
            map[str[i]] = 1; 
        } 
        else
        { 
            map[str[i]]++;  
        } 

        // Decrease the frequency  
        // of the first character  
        // of the previous substring 
        map[str[i - K]]--; 

        // If the character is not present  
        // in the current substring  
        if (map[str[i - K]] == 0) 
        {  
            map.Remove(str[i - K]);  
        }  

        // If the count of distinct  
        // characters is 0  
        if (map.Count == K) 
        {  
            answer++;  
        }  
    }  

    // Return the count  
    return answer;  
}  

// Driver code  
public static void Main(string[] args)  
{  

    // string str  
    string str = "aabcdabbcdc";  

    // integer K  
    int K = 3;  

    // Print the count of K length  
    // substrings with k distinct characters  
    Console.Write(countSubstrings(str, K)); 
}  
} 

// This code is contributed by rutvik_56 

```

**Output:**

```
5

```

**时间复杂度**：`O(n)`



* * *

* * *



