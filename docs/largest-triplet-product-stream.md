# 一个流中最大的三元组产品

> 原文:[https://www . geesforgeks . org/maximum-triple-product-stream/](https://www.geeksforgeeks.org/largest-triplet-product-stream/)

给定表示为 arr[]的整数流。对于从 0 到 n-1 的每个索引 I，打印子阵列 arr[0…i]的最大、第二大、第三大元素的乘积。如果我< 2 打印-1。

示例:

```
Input : arr[] = {1, 2, 3, 4, 5}
Output :-1
        -1
         6
         24
         60
Explanation : for i = 2 only three elements 
are there {1, 2, 3} so answer is 6\. For i = 3
largest three elements are {2, 3, 4} their
product is 2*3*4 = 24 ....so on            
```

这里我们将使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。

1.  在优先级队列中插入 arr[i]
2.  由于优先级队列中的顶部元素最大，所以将其弹出并存储为 x。现在优先级队列中的顶部元素将是子阵列 arr[0…i]中的第二大元素，将其弹出并存储为 y。现在顶部元素是子阵列 arr[0…i]中的第三大元素，因此将其弹出并存储为 z。
3.  打印 x*y*z
4.  重新插入 x，y，z。

## C++

```
// C++ implementation of largest triplet
// multiplication
#include <bits/stdc++.h>
using namespace std;

// Prints the product of three largest numbers
// in subarray arr[0..i]
void LargestTripletMultiplication(int arr[], int n)
{
    // call a priority queue
    priority_queue<int> q;

    // traversing the array
    for (int i = 0; i < n; i++) {
        // pushing arr[i] in the array
        q.push(arr[i]);

        // if less than three elements are present
        // in array print -1
        if (q.size() < 3)
            cout << "-1" << endl;
        else {
            // pop three largest elements
            int x = q.top();
            q.pop();
            int y = q.top();
            q.pop();
            int z = q.top();
            q.pop();

            // Reinsert x, y, z in priority_queue
            int ans = x * y * z;
            cout << ans << endl;
            q.push(x);
            q.push(y);
            q.push(z);
        }
    }
    return;
}

// Driver Function
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    LargestTripletMultiplication(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of largest triplet
// multiplication
import java.util.Collections;
import java.util.PriorityQueue;

class GFG {

    // Prints the product of three largest numbers
    // in subarray arr[0..i]
    static void LargestTripletMultiplication(int arr[], int n)
    {
        // call a priority queue
        PriorityQueue<Integer> q = new PriorityQueue(Collections.reverseOrder());

        // traversing the array
        for (int i = 0; i < n; i++) {
            // pushing arr[i] in array
            q.add(arr[i]);

            // if less than three elements are present
            // in array print -1
            if (q.size() < 3)
                System.out.println("-1");
            else {
                // pop three largest elements
                int x = q.poll();
                int y = q.poll();
                int z = q.poll();

                // Reinsert x, y, z in priority_queue
                int ans = x * y * z;
                System.out.println(ans);
                q.add(x);
                q.add(y);
                q.add(z);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;
        LargestTripletMultiplication(arr, n);
    }
}

// This code is contributed by shubham96301
```

## 蟒蛇 3

```
# Python3 implementation of largest triplet
# multiplication
from queue import PriorityQueue

# Prints the product of three largest
# numbers in subarray arr[0..i]
def LargestTripletMultiplication(arr, n):

    # Call a priority queue
    q = PriorityQueue()

    # Traversing the array
    for i in range(n):

        # Pushing -arr[i] in array
        # to get max PriorityQueue
        q.put(-arr[i])

        # If less than three elements
        # are present in array print -1
        if (q.qsize() < 3):
            print(-1)
        else:

            # pop three largest elements
            x = q.get()
            y = q.get()
            z = q.get()

            # Reinsert x, y, z in
            # priority_queue
            ans = x * y * z

            print(-ans)

            q.put(x);
            q.put(y);
            q.put(z);

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5 ]
    n = len(arr)

    LargestTripletMultiplication(arr, n)

# This code is contributed by math_lover
```

## C#

```
// C# implementation of largest triplet
// multiplication
using System;
using System.Collections.Generic;
public class GFG {

  // Prints the product of three largest numbers
  // in subarray arr[0..i]
  static void LargestTripletMultiplication(int []arr, int n)
  {
    // call a priority queue
    List<int> q = new List<int>();

    // traversing the array
    for (int i = 0; i < n; i++)
    {

      // pushing arr[i] in array
      q.Add(arr[i]);
      q.Sort();
      q.Reverse();

      // if less than three elements are present
      // in array print -1
      if (q.Count < 3)
        Console.WriteLine("-1");
      else
      {

        // pop three largest elements
        int x = q[0];
        int y = q[1];
        int z = q[2];
        q.RemoveRange(0, 3);

        // Reinsert x, y, z in priority_queue
        int ans = x * y * z;
        Console.WriteLine(ans);
        q.Add(x);
        q.Add(y);
        q.Add(z);
      }
    }
  }

  // Driver code
  public static void Main(String[] args)
  {
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;
    LargestTripletMultiplication(arr, n);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of largest triplet
// multiplication
    // Prints the product of three largest numbers
    // in subarray arr[0..i]
    function LargestTripletMultiplication(arr , n) {
        // call a priority queue
        var q = [];

        // traversing the array
        for (i = 0; i < n; i++) {
            // pushing arr[i] in array
            q.push(arr[i]);
q.sort();

            // if less than three elements are present
            // in array print -1
            if (q.length < 3)
                document.write("-1<br/>");
            else {
                // pop three largest elements
                q.sort();

                var x = q.pop();
                var y = q.pop();
                var z = q.pop();

                // Reinsert x, y, z in priority_queue
                var ans = x * y * z;
                document.write(ans+"<br/>");
                q.push(x);
                q.push(y);
                q.push(z);
                q.sort();
                q.reverse();
            }
        }
    }

    // Driver code

        var arr = [ 1, 2, 3, 4, 5 ];
        var n = arr.length;
        LargestTripletMultiplication(arr, n);

// This code contributed by umadevi9616
</script>
```

**输出:**

```
-1
-1
6
24
60
```

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。