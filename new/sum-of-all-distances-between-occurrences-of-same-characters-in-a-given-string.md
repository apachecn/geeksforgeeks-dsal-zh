# 给定字符串中出现相同字符之间的所有距离之和

> 原文：[https://www.geeksforgeeks.org/sum-of-all-distances-between-occurrences-of-same-characters-in-a-given-string/](https://www.geeksforgeeks.org/sum-of-all-distances-between-occurrences-of-same-characters-in-a-given-string/)


给定字符串`S`，任务是从包含相同字符的给定字符串中查找所有索引对对之间的距离之和。

**示例**：

> **输入**：`S = "ababa"`
>
> **输出**：10
>
> **说明**：
>
> 具有相同字符的一对索引为：`(0, 2) (0, 4) (1, 3) (2, 4)`
>
> 这些对索引之间的绝对差之和为`|2 – 0| + |4 – 0| + |1 – 3| + |2 – 4| = 10`。
>
> 因此，必需的答案是 10。
> 
> **输入**：`S = "ttt"`
>
> **输出**：4

**朴素的方法**：解决该问题的最简单方法是遍历字符串，对于遇到的每个字符，遍历右边的其余字符串以查找该字符的出现。 对于找到的每一个重复字符，请继续在答案中添加相关索引之间的绝对差。 最后，打印获得的总和。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(1)`

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// of distances between occurrences
// of same characters in a string
int findSum(string s)
{
    int sum = 0;
    for (int i = 0; i < s.size(); i++) {
        for (int j = i + 1; j < s.size(); j++) {

            // If similar characters are found
            if (s[i] == s[j]) {

                // Add the difference
                // of their positions
                sum += (j - i);
            }
        }
    }

    // Return the answer
    return sum;
}

// Driver Code
int main()
{
    string s = "ttt";
    cout << findSum(s) << endl;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
class GFG{

// Function to calculate the sum
// of distances between occurrences
// of same characters in a String
static int findSum(String s)
{
    int sum = 0;
    for (int i = 0; i < s.length(); i++) 
    {
        for (int j = i + 1; j < s.length(); j++) 
        {
            // If similar characters are found
            if (s.charAt(i) == s.charAt(j)) 
            {
                // Add the difference
                // of their positions
                sum += (j - i);
            }
        }
    }

    // Return the answer
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    String s = "ttt";
    System.out.print(findSum(s) + "\n");
}
}
// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 program for the above approach 

# Function to calculate the sum
# of distances between occurrences
# of same characters in a string
def findSum(s):

    sum = 0
    for i in range(len(s)):
        for j in range(i + 1, len(s)):

            # If similar characters are found
            if (s[i] == s[j]):

                # Add the difference
                # of their positions
                sum += (j - i)

    # Return the answer
    return sum

# Driver Code
s = "ttt"

print(findSum(s))

# This code is contributed by code_hunt

```

## C#

```cs

// C# program for 
// the above approach
using System;
class GFG{

// Function to calculate the sum
// of distances between occurrences
// of same characters in a String
static int findSum(String s)
{
  int sum = 0;
  for (int i = 0; i < s.Length; i++) 
  {
    for (int j = i + 1; j < s.Length; j++) 
    {
      // If similar characters 
      // are found
      if (s[i] == s[j]) 
      {
        // Add the difference
        // of their positions
        sum += (j - i);
      }
    }
  }

  // Return the answer
  return sum;
}

// Driver Code
public static void Main(String[] args)
{
  String s = "ttt";
  Console.Write(findSum(s) + "\n");
}
}

// This code is contributed by shikhasingrajput

```

**输出**： 

```
4

```

**有效方法**：可以基于以下观察来优化上述方法：

*   最初，假定每个字符的所有相似字符都位于索引`0`处。

*   根据以上假设，所需的总和等于：

> 先前访问过的相似字符的数量*字符索引–那些相似字符到索引 0 的距离之和

因此，请按照以下步骤解决问题：

*   初始化两个数组`Visited[]`和`distance[]`，以分别存储字符串中每个字符的频率和每个字符的先前出现之间的距离。

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，对于遇到的每个字符，即`S[i]`，更新以下内容：

    *   将`Visited[S[i] * i – distance[S[i]]`加到所需的总和中。

    *   递增`Visited[S[i]]`以增加字符的频率。

    *   将`distance[S[i]]`增加`i`，以增加与先前出现的`S[i]`，的距离为 0。

*   完成上述步骤后，打印获得的总和。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// of distances between occurrences
// of same characters in a string
int findSum(string s)
{
    int visited[256];
    int distance[256];

    // Initially make all the distances
    // and number of characters visited as 0
    for (int i = 0; i < 256; i++) {
        visited[i] = 0;
        distance[i] = 0;
    }

    int sum = 0;

    for (int i = 0; i < s.size(); i++) {

        // Assuming that all the similar
        // characters are located at index 0

        // Add visited[s[i]]*i to sum
        // and subtract the distances of
        // characters from index 0
        sum += visited[s[i]] * i
               - distance[s[i]];

        // Increment the number of
        // visited characters
        visited[s[i]]++;

        // Add the distance of the
        // character from position 0
        // i.e., (i - 0) = i
        distance[s[i]] += i;
    }

    // Return the answer
    return sum;
}

// Driver code
int main()
{
    string s = "ttt";

    // Function call
    cout << findSum(s) << endl;
}

```

## Java

```java

// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate the sum
// of distances between occurrences
// of same characters in a string
static int findSum(String s)
{
    int[] visited = new int[256];
    int[] distance = new int[256];

    // Initially make all the distances
    // and number of characters visited as 0
    for(int i = 0; i < 256; i++)
    {
        visited[i] = 0;
        distance[i] = 0;
    }

    int sum = 0;

    for(int i = 0; i < s.length(); i++)
    {

        // Assuming that all the similar
        // characters are located at index 0

        // Add visited[s[i]]*i to sum
        // and subtract the distances of
        // characters from index 0
        sum += visited[s.charAt(i)] * i - 
              distance[s.charAt(i)];

        // Increment the number of
        // visited characters
        visited[s.charAt(i)]++;

        // Add the distance of the
        // character from position 0
        // i.e., (i - 0) = i
        distance[s.charAt(i)] += i;
    }

    // Return the answer
    return sum;
} 

// Driver code
public static void main (String[] args)
{
    String s = "ttt";

    // Function call
    System.out.println(findSum(s));
}
}

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program for the above approach

# Function to calculate the sum
# of distances between occurrences
# of same characters in a string
def findSum(s):
    visited = [0 for i in range(256)];
    distance = [0 for i in range(256)];

    # Initially make all 
    # the distances and number 
    # of characters visited as 0
    for i in range(256):
        visited[i] = 0;
        distance[i] = 0;    

    sum = 0;

    for i in range(len(s)):

        # Assuming that all the similar
        # characters are located at index 0

        # Add visited[s[i]]*i to sum
        # and subtract the distances of
        # characters from index 0
        sum += visited[ord(s[i])] * i - distance[ord(s[i])];

        # Increment the number of
        # visited characters
        visited[ord(s[i])] += 1;

        # Add the distance of the
        # character from position 0
        # i.e., (i - 0) = i
        distance[ord(s[i])] += i;    

    # Return the answer
    return sum;

# Driver code
if __name__ == '__main__':

    s = "ttt";

    # Function call
    print(findSum(s));

# This code is contributed by Rajput-Ji

```

## C#

```cs

// C# program for the above approach
using System;

class GFG{

// Function to calculate the sum
// of distances between occurrences
// of same characters in a string
static int findSum(String s)
{
    int[] visited = new int[256];
    int[] distance = new int[256];

    // Initially make all the distances
    // and number of characters visited as 0
    for(int i = 0; i < 256; i++)
    {
        visited[i] = 0;
        distance[i] = 0;
    }

    int sum = 0;

    for(int i = 0; i < s.Length; i++)
    {

        // Assuming that all the similar
        // characters are located at index 0

        // Add visited[s[i]]*i to sum
        // and subtract the distances of
        // characters from index 0
        sum += visited[s[i]] * i - 
              distance[s[i]];

        // Increment the number of
        // visited characters
        visited[s[i]]++;

        // Add the distance of the
        // character from position 0
        // i.e., (i - 0) = i
        distance[s[i]] += i;
    }

    // Return the answer
    return sum;
} 

// Driver code
public static void Main(String[] args)
{
    String s = "ttt";

    // Function call
    Console.WriteLine(findSum(s));
}
}

// This code is contributed by Amit Katiyar

```

**输出**： 

```
4

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *



