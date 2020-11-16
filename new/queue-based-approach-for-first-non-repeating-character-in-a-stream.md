# 获取流中第一个非重复字符的基于队列的方法

> 原文：[https://www.geeksforgeeks.org/queue-based-approach-for-first-non-repeating-character-in-a-stream/](https://www.geeksforgeeks.org/queue-based-approach-for-first-non-repeating-character-in-a-stream/)

给定字符流，每次将字符插入流中时，我们都必须找到第一个非重复字符。

**示例**：

```
Input  : a a b c
Output : a -1 b b

Input  : a a c
Output : a -1 c

```c

我们已经在[先前的文章](https://www.geeksforgeeks.org/find-first-non-repeating-character-stream-characters/)中讨论了基于双链表的方法。

**方法**：

1.  创建一个大小为 26 的计数数组（假定仅存在小写字符），并将其初始化为零。

2.  创建字符数据类型的队列。

3.  将每个字符存储在队列中，并增加其在哈希数组中的频率。

4.  对于流的每个字符，我们检查队列的前面。

5.  如果队列开头的字符频率为 1，则它将是第一个非重复字符。

6.  否则，如果频率大于 1，则我们弹出该元素。

7.  如果队列变空，则意味着没有非重复字符，因此我们将打印 -1。

下面是上述方法的实现：

## C++

```cpp

// C++ program for a Queue based approach  
// to find first non-repeating character 
#include <bits/stdc++.h> 
using namespace std; 
const int MAX_CHAR = 26; 

// function to find first non repeating 
// character of sa stream 
void firstnonrepeating(char str[]) 
{ 
    queue<char> q; 
    int charCount[MAX_CHAR] = { 0 }; 

    // traverse whole stream 
    for (int i = 0; str[i]; i++) { 

        // push each character in queue 
        q.push(str[i]); 

        // increment the frequency count 
        charCount[str[i] - 'a']++; 

        // check for the non pepeating character 
        while (!q.empty()) { 
            if (charCount[q.front() - 'a'] > 1) 
                q.pop(); 
            else { 
                cout << q.front() << " "; 
                break; 
            } 
        } 

        if (q.empty()) 
            cout << -1 << " "; 
    } 
    cout << endl; 
} 

// Driver function 
int main() 
{ 
    char str[] = "aabc"; 
    firstnonrepeating(str); 
    return 0; 
} 

```

## Java

```java

// Java Program for a Queue based approach  
// to find first non-repeating character 

import java.util.LinkedList; 
import java.util.Queue; 

public class NonReapatingCQueue { 
    final static int MAX_CHAR = 26; 

    // function to find first non repeating 
    // character of stream 
    static void firstNonRepeating(String str) 
    { 
        // count array of size 26(assuming 
        // only lower case characters are present) 
        int[] charCount = new int[MAX_CHAR]; 

        // Queue to store Characters 
        Queue<Character> q = new LinkedList<Character>(); 

        // traverse whole stream 
        for (int i = 0; i < str.length(); i++) { 
            char ch = str.charAt(i); 

            // push each character in queue 
            q.add(ch); 

            // increment the frequency count 
            charCount[ch - 'a']++; 

            // check for the non repeating character 
            while (!q.isEmpty()) { 
                if (charCount[q.peek() - 'a'] > 1) 
                    q.remove(); 
                else { 
                    System.out.print(q.peek() + " "); 
                    break; 
                } 
            } 
            if (q.isEmpty()) 
                System.out.print(-1 + " "); 
        } 
        System.out.println(); 
    } 

    // Driver function 
    public static void main(String[] args) 
    { 
        String str = "aabc"; 
        firstNonRepeating(str); 
    } 
} 
// This code is Contributed by Sumit Ghosh 

```

## Python3

```py

# Python3 program for a Queue based approach  
# to find first non-repeating character  
from queue import Queue  

# function to find first non  
# repeating character of sa Stream  
def firstnonrepeating(Str): 
    global MAX_CHAR 
    q = Queue() 
    charCount = [0] * MAX_CHAR  

    # traverse whole Stream 
    for i in range(len(Str)): 

        # push each character in queue  
        q.put(Str[i])  

        # increment the frequency count  
        charCount[ord(Str[i]) - 
                  ord('a')] += 1

        # check for the non pepeating 
        # character  
        while (not q.empty()):  
            if (charCount[ord(q.queue[0]) - 
                          ord('a')] > 1):  
                q.get()  
            else: 
                print(q.queue[0], end = " ")  
                break

        if (q.empty()):  
            print(-1, end = " ") 
    print() 

# Driver Code 
MAX_CHAR = 26
Str = "aabc"
firstnonrepeating(Str) 

# This code is contributed by PranchalK 

```

## C#

```cs

using System; 
using System.Collections.Generic; 

// C# Program for a Queue based approach   
// to find first non-repeating character  

public class NonReapatingCQueue 
{ 
    public const int MAX_CHAR = 26; 

    // function to find first non repeating  
    // character of stream  
    public static void firstNonRepeating(string str) 
    { 
        // count array of size 26(assuming  
        // only lower case characters are present)  
        int[] charCount = new int[MAX_CHAR]; 

        // Queue to store Characters  
        LinkedList<char> q = new LinkedList<char>(); 

        // traverse whole stream  
        for (int i = 0; i < str.Length; i++) 
        { 
            char ch = str[i]; 

            // push each character in queue  
            q.AddLast(ch); 

            // increment the frequency count  
            charCount[ch - 'a']++; 

            // check for the non repeating character  
            while (q.Count > 0) 
            { 
                if (charCount[q.First.Value - 'a'] > 1) 
                { 
                    q.RemoveFirst(); 
                } 
                else
                { 
                    Console.Write(q.First.Value + " "); 
                    break; 
                } 
            } 
            if (q.Count == 0) 
            { 
                Console.Write(-1 + " "); 
            } 
        } 
        Console.WriteLine(); 
    } 

    // Driver function  
    public static void Main(string[] args) 
    { 
        string str = "aabc"; 
        firstNonRepeating(str); 
    } 
} 

//This code is contributed by Shrikant13 

```

**输出**：

```
a -1 b b

```

**视频**：

本文由 **Niteesh Kumar** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

