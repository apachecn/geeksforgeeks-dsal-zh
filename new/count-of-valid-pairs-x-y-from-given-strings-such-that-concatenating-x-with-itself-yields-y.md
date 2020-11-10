# 来自给定字符串的有效对`(X, Y)`的计数，以使`X`与自身连接产生`Y`

> 原文：[https://www.geeksforgeeks.org/count-of-valid-pairs-x-y-from-given-strings-such-that-concatenating-x-with-itself-yields-y/](https://www.geeksforgeeks.org/count-of-valid-pairs-x-y-from-given-strings-such-that-concatenating-x-with-itself-yields-y/)

给定`N`个字符串的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`。 假设`X`和`Y`为两个字符串，如果重排，则`X`和`Y`是有效的对。 从`X`与`X`连接（即`X + X`）得到的字符串的结果为`Y`。 任务是计算此类有效对的数量。

**示例**：

> **输入**：`N = 4, arr[] = {"hacker", "ackerhackerh", "int", "iittnn", "long"}`
>
> **输出**：2
>
> **说明**：
>
> 连接`{"hacker", "ackerhackerh"}`的`"hacker"`与`"hacker"}`后，会在重新排列后给出`"ackerhackerh"`。
>
> 连接`{"int", "iittnn"}`的`"int"`与`"int"`时，在重新排列后会给出`"iittnn"`。
> 
> **输入**：`N = 3, arr[] = {"easy", "yeasseay", "medium"}`
>
> **输出**：1
>
> **说明**：
>
> 连接`{"easy", "yeasseay"}`的`"easy"`与`"easy"`时，在重新排列后会得到`"yeasseay"`。

**朴素的方法**：想法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并根据给定条件检查是否有任何对形成有效对。 如果是，则计算该对并检查下一对。 完成上述步骤后，打印计数值。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(1)`

**高效方法**：想法是将排序后的字符串及其计数存储在[`Hashmap`](http://www.geeksforgeeks.org/java-util-hashmap-in-java/)中，并遍历数组中的每个字符串，将其自身连接起来并在`Hashmap`中找到其计数将其添加到对数中。 步骤如下：

1.  创建一个哈希映射。

2.  对数组中给定的字符串进行排序，并将其计数存储在哈希映射中。

3.  再次遍历所有字符串，并将每个字符串与其自身连接，[对字符串进行排序](https://www.geeksforgeeks.org/sort-string-characters/)，然后在[`Hashmap`](https://www.geeksforgeeks.org/java-program-to-count-the-occurrence-of-each-character-in-a-string-using-hashmap/)中找到其计数。

4.  在上述步骤中更新最终计数，并在上述所有步骤之后打印最终计数。

下面是上述方法的实现：

## C++ 14

```

// C++14 program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to implement sorting on
// strings
string sorted(string s)
{

    // Convert string to char array
    char ch[s.length()];
    for(int i = 0; i < s.length(); i++)
    {
        ch[i] = s[i];
    }

    // Sort the array 
    sort(ch, ch + s.length());
    string sb;

    for(char c : ch)
      sb += c;

    // Return string
     return sb;
}

// Function that count total number
// of valid pairs
int countPairs(string arr[], int N)
{

    // Create hashmap to store the
    // frequency of each string
    // in sorted form
    map<string, int> mp;

    // Initialise the count of pairs
    int count = 0;

    for(int i = 0; i < N; i++) 
    {
        // Store each string in sorted
        // form along with it's count
        string s = sorted(arr[i]);
        mp[s]++;
    }

    // Iterate through each string
    // in the array
    for(int i = 0; i < N; i++) 
    {

        // Concatenate each string with itself
        arr[i] = arr[i] + arr[i];
        sorted(arr[i]);

        // Find its count in the hashmap
        count += mp[sorted(arr[i])];
    }

    // Return answer
    return count;
}

// Driver Code
int main()
{
    int N = 3;

    // Given array of strings
    string arr[] = { "easy", "yeasseay",
                     "medium" };

    // Function Call
    cout << countPairs(arr, N) << endl;
    return 0;
}

// This code is contributed by sallagondaavinashreddy7

```

## Java

```java

// Java program for the above approach 
import java.util.*; 
public class Main { 

    // Function that count total number 
    // of valid pairs 
    public static int
    countPairs(String arr[], int N) 
    { 

        // Create hashmap to store the 
        // frequency of each string 
        // in sorted form 
        HashMap<String, Integer> map 
            = new HashMap<>(); 

        // Initialise the count of pairs 
        int count = 0; 
        for (int i = 0; i < N; i++) { 
            String s = sort(arr[i]); 

            // Store each string in sorted 
            // form along with it's count 
            map.put(s, map.getOrDefault(s, 0) + 1); 
        } 

        // Iterate through each string 
        // in the array 
        for (int i = 0; i < N; i++) { 

            // Concatenate each string with itself 
            String s = sort(arr[i] + arr[i]); 

            // Find its count in the hashmap 
            count += map.getOrDefault(s, 0); 
        } 

        // Return answer 
        return count; 
    } 

    // Function to implement sorting on 
    // strings 
    public static String sort(String s) 
    { 

        // Convert string to char array 
        char ch[] = s.toCharArray(); 

        // Sort the array 
        Arrays.sort(ch); 
        StringBuffer sb = new StringBuffer(); 
        for (char c : ch) 
            sb.append(c); 

        // Return string 
        return sb.toString(); 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        int N = 3; 

        // Given array of strings 
        String arr[] = { "easy", "yeasseay", 
                        "medium" }; 

        // Function Call 
        System.out.println(countPairs(arr, N)); 
    } 
}

```

## Python3

```py

# Python3 program for the above approach
from collections import defaultdict

# Function that count total number
# of valid pairs 
def countPairs(arr, N):

    # Create hashmap to store the
    # frequency of each string
    # in sorted form
    map = defaultdict(lambda : 0)

    # Initialise the count of pairs
    count = 0
    for i in range(N):
        s = sorted(arr[i])

        # Store each string in sorted
        # form along with it's count
        map["".join(s)] += 1

    # Iterate through each string
    # in the array
    for i in range(N):

        # Concatenate each string with itself
        s = sorted(arr[i] + arr[i])

        # Find its count in the hashmap
        count += map["".join(s)]

    # Return answer
    return count

# Driver Code
N = 3

# Given array of strings
arr = [ "easy", "yeasseay", "medium" ]

# Function call
print(countPairs(arr, N))

# This code is contributed by Shivam Singh

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Text; 

class GFG{

// Function that count total number
// of valid pairs
public static int countPairs(string []arr, int N)
{

    // Create hashmap to store the
    // frequency of each string
    // in sorted form
    Dictionary<string,
               int> map = new Dictionary<string,
                                         int>();

    // Initialise the count of pairs
    int count = 0;
    for(int i = 0; i < N; i++) 
    {
        string s = sort(arr[i]);

        // Store each string in sorted
        // form along with it's count
        if (map.ContainsKey(s))
        {
            map[s]++;
        }
        else
        {
            map[s] = 1;
        }
    }

    // Iterate through each string
    // in the array
    for(int i = 0; i < N; i++) 
    {

        // Concatenate each string with itself
        string s = sort(arr[i] + arr[i]);

        // Find its count in the hashmap
        count += map.GetValueOrDefault(s, 0);
    }

    // Return answer
    return count;
}

// Function to implement sorting on
// strings
public static string sort(string s)
{

    // Convert string to char array
    char []ch = s.ToCharArray();

    // Sort the array
    Array.Sort(ch);

    StringBuilder sb = new StringBuilder();
    foreach(char c in ch)
        sb.Append(c);

    // Return string
    return sb.ToString();
}

// Driver Code
public static void Main(string []args)
{
    int N = 3;

    // Given array of strings
    string []arr = { "easy", "yeasseay",
                     "medium" };

    // Function call
    Console.Write(countPairs(arr, N));
}
}

// This code is contributed by rutvik_56

```

**输出**： 

```
1

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



