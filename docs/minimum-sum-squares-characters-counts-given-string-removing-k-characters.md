# 去除 k 个字符后给定字符串中字符计数的最小平方和

> 原文:[https://www . geesforgeks . org/最小平方和-字符-计数-给定-字符串-删除-k-字符/](https://www.geeksforgeeks.org/minimum-sum-squares-characters-counts-given-string-removing-k-characters/)

给定一串小写字母和一个数字 k，任务是在去掉 k 个字符后打印字符串的最小值。字符串的值定义为每个不同字符计数的平方和。例如，考虑字符串“saideep ”,这里字符的频率是 s-1、a-1、i-1、e-2、d-1、p-1，字符串的值是 1^2 + 1^2 + 1^2 + 1^2 + 1^2 + 2^2 = 9。
预计时间复杂度:O(k*logn)
**示例:**

```
Input :  str = abccc, K = 1
Output :  6
We remove c to get the value as 12 + 12 + 22

Input :  str = aaab, K = 2
Output :  2
```

**问于:亚马逊**

一个明确的观察是，我们需要移除频率最高的字符。一个诀窍是字符 ma
A **简单的解决方案**是使用排序技术通过所有当前最高频率减少到 k 倍。对于每次降低排序频率后的数组。
一个**更好的解决方案**用于优先级队列，最高的元素在最上面。

1.  初始化空优先级队列。
2.  计算每个字符的频率并存储到临时数组中。
3.  从队列中删除出现频率最高的 K 个字符。
4.  最后计算每个元素的平方和并返回。

以下是上述想法的实现。

## C++

```
// C++ program to find min sum of squares
// of characters after k removals
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// Main Function to calculate min sum of
// squares of characters after k removals
int minStringValue(string str, int k)
{
    int l = str.length(); // find length of string

    // if K is greater than length of string
    // so reduced string will become 0
    if (k >= l)
        return 0;

    // Else find Frequency of each character and
    // store in an array
    int frequency[MAX_CHAR] = { 0 };
    for (int i = 0; i < l; i++)
        frequency[str[i] - 'a']++;

    // Push each char frequency into a priority_queue
    priority_queue<int> q;
    for (int i = 0; i < MAX_CHAR; i++)
        q.push(frequency[i]);

    // Removal of K characters
    while (k--) {
        // Get top element in priority_queue,
        // remove it. Decrement by 1 and again
        // push into priority_queue
        int temp = q.top();
        q.pop();
        temp = temp - 1;
        q.push(temp);
    }

    // After removal of K characters find sum
    // of squares of string Value
    int result = 0; // Initialize result
    while (!q.empty()) {
        int temp = q.top();
        result += temp * temp;
        q.pop();
    }

    return result;
}

// Driver Code
int main()
{
    string str = "abbccc"; // Input 1
    int k = 2;
    cout << minStringValue(str, k) << endl;

    str = "aaab"; // Input 2
    k = 2;
    cout << minStringValue(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find min sum of squares
// of characters after k removals
import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Collections;
public class GFG {

    static final int MAX_CHAR = 26;

    // Main Function to calculate min sum of
    // squares of characters after k removals
    static int minStringValue(String str, int k)
    {
        int l = str.length(); // find length of string

        // if K is greater than length of string
        // so reduced string will become 0
        if (k >= l)
            return 0;

        // Else find Frequency of each character and
        // store in an array
        int[] frequency = new int[MAX_CHAR];
        for (int i = 0; i < l; i++)
            frequency[str.charAt(i) - 'a']++;

        // creating a priority queue with comparator
        // such that elements in the queue are in
        // descending order.
        PriorityQueue<Integer> q = new PriorityQueue<>(Collections.reverseOrder());

        // Push each char frequency into a priority_queue
        for (int i = 0; i < MAX_CHAR; i++) {
            if (frequency[i] != 0)
                q.add(frequency[i]);
        }

        // Removal of K characters
        while (k != 0) {
            // Get top element in priority_queue,
            // remove it. Decrement by 1 and again
            // push into priority_queue
            q.add(q.poll() - 1);
            k--;
        }

        // After removal of K characters find sum
        // of squares of string Value
        int result = 0; // Initialize result
        while (!q.isEmpty()) {
            result += q.peek() * q.poll();
        }

        return result;
    }

    // Driver Code
    public static void main(String args[])
    {
        String str = "abbccc"; // Input 1
        int k = 2;
        System.out.println(minStringValue(str, k));

        str = "aaab"; // Input 2
        k = 2;
        System.out.println(minStringValue(str, k));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find min sum of
# squares of characters after k removals
from queue import PriorityQueue

MAX_CHAR = 26

# Main Function to calculate min sum of
# squares of characters after k removals
def minStringValue(str, k):
    l = len(str) # find length of string

    # if K is greater than length of string
    # so reduced string will become 0
    if(k >= l):
        return 0

    # Else find Frequency of each
    # character and store in an array
    frequency = [0] * MAX_CHAR
    for i in range(0, l):
        frequency[ord(str[i]) - 97] += 1

    # Push each char frequency negative
    # into a priority_queue as the queue
    # by default is minheap
    q = PriorityQueue()
    for i in range(0, MAX_CHAR):
        q.put(-frequency[i])

    # Removal of K characters
    while(k > 0):

        # Get top element in priority_queue
        # multiply it by -1 as temp is negative
        # remove it. Increment by 1 and again
        # push into priority_queue
        temp = q.get()
        temp = temp + 1
        q.put(temp, temp)
        k = k - 1

    # After removal of K characters find
    # sum of squares of string Value    
    result = 0; # initialize result
    while not q.empty():
        temp = q.get()
        temp = temp * (-1)
        result += temp * temp
    return result

# Driver Code
if __name__ == "__main__":
    str = "abbccc"
    k = 2
    print(minStringValue(str, k))

    str = "aaab"
    k = 2
    print(minStringValue(str, k))

# This code is contributed
# by Sairahul Jella
```

## C#

```
// C# program to find min sum of squares
// of characters after k removals
using System;
using System.Collections.Generic;
class GFG {

  static readonly int MAX_CHAR = 26;

  // Main Function to calculate min sum of
  // squares of characters after k removals
  static int minStringValue(String str, int k)
  {
    int l = str.Length; // find length of string

    // if K is greater than length of string
    // so reduced string will become 0
    if (k >= l)
      return 0;

    // Else find Frequency of each character and
    // store in an array
    int[] frequency = new int[MAX_CHAR];
    for (int i = 0; i < l; i++)
      frequency[str[i] - 'a']++;

    // creating a priority queue with comparator
    // such that elements in the queue are in
    // descending order.
    List<int> q = new List<int>();

    // Push each char frequency into a priority_queue
    for (int i = 0; i < MAX_CHAR; i++)
    {
      if (frequency[i] != 0)
        q.Add(frequency[i]);
    }

    // Removal of K characters
    while (k != 0)
    {
      q.Sort();
      q.Reverse();

      // Get top element in priority_queue,
      // remove it. Decrement by 1 and again
      // push into priority_queue
      q.Add(q[0] - 1);
      q.RemoveAt(0);
      k--;
    }

    // After removal of K characters find sum
    // of squares of string Value
    int result = 0; // Initialize result
    while (q.Count != 0)
    {
      result += q[0] * q[0];
      q.RemoveAt(0);
    }
    return result;
  }

  // Driver Code
  public static void Main(String []args)
  {
    String str = "abbccc"; // Input 1
    int k = 2;
    Console.WriteLine(minStringValue(str, k));
    str = "aaab"; // Input 2
    k = 2;
    Console.WriteLine(minStringValue(str, k));
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to find min sum of squares
// of characters after k removals

let MAX_CHAR = 26;

// Main Function to calculate min sum of
    // squares of characters after k removals
function minStringValue(str,k)
{
    let l = str.length; // find length of string

        // if K is greater than length of string
        // so reduced string will become 0
        if (k >= l)
            return 0;

        // Else find Frequency of each character and
        // store in an array
        let frequency = new Array(MAX_CHAR);
        for(let i=0;i<MAX_CHAR;i++)
            frequency[i]=0;
        for (let i = 0; i < l; i++)
            frequency[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // creating a priority queue with comparator
        // such that elements in the queue are in
        // descending order.
        let q = [];

        // Push each char frequency into a priority_queue
        for (let i = 0; i < MAX_CHAR; i++) {
            if (frequency[i] != 0)
                q.push(frequency[i]);
        }

        q.sort(function(a,b){return b-a;});

        // Removal of K characters
        while (k != 0) {
            // Get top element in priority_queue,
            // remove it. Decrement by 1 and again
            // push into priority_queue
            q.push(q.shift() - 1);
            q.sort(function(a,b){return b-a;});
            k--;
        }

        // After removal of K characters find sum
        // of squares of string Value
        let result = 0; // Initialize result
        while (q.length!=0) {
            result += q[0] * q.shift();
        }

        return result;
}

// Driver Code
let str = "abbccc"; // Input 1
let k = 2;
document.write(minStringValue(str, k)+"<br>");

str = "aaab"; // Input 2
k = 2;
document.write(minStringValue(str, k)+"<br>");

// This code is contributed by unknown2108

</script>
```

**输出:**

```
6
2
```

**时间复杂度:O(k*logn)**
本文由**Somesh Awasthi**先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。