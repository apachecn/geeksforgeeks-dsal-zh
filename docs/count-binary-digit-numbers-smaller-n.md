# 小于 N 的二进制数字计数

> 原文:[https://www . geesforgeks . org/count-binary-digits-numbers-small-n/](https://www.geeksforgeeks.org/count-binary-digit-numbers-smaller-n/)

给定一个极限 N，我们需要找出小于 N 的二进制数字的个数，二进制数字是那些只包含 0 和 1 作为数字的数字，像 1、10、101 等都是二进制数字。

**示例:**

```
Input : N = 200
Output : 7
Count of binary digit number smaller than N is 7, 
enumerated below,
1, 10, 11, 110, 101, 100, 111 
```

解决这个问题的一个简单方法是从 1 到 N 循环，检查每个数字是否是二进制数字。如果是二进制数字，则增加此类数字的计数，但此过程需要 O(N)个时间。我们可以做得更好，因为我们知道这种数字的计数将比 N 小得多。我们可以只迭代二进制数字，并检查生成的数字是否小于 N。
在下面的代码中，实现了类似 BFS 的方法，只迭代二进制数字。我们从 1 开始，每次我们将(t*10)和(t*10 + 1)推入队列，其中 t 是弹出的元素。如果 t 是一个二进制数字，那么(t*10)和(t*10 + 1)也将是数字，所以我们将只使用队列来迭代这些数字。当弹出的数字越过 n
时，我们将停止推送队列中的元素

## C++

```
// C++ program to count all binary digit
// numbers smaller than N
#include <bits/stdc++.h>
using namespace std;

//  method returns count of binary digit
//  numbers smaller than N
int countOfBinaryNumberLessThanN(int N)
{
    //  queue to store all intermediate binary
    // digit numbers
    queue<int> q;

    //  binary digits start with 1
    q.push(1);
    int cnt = 0;
    int t;

    //  loop until we have element in queue
    while (!q.empty())
    {
        t = q.front();
        q.pop();

        //  push next binary digit numbers only if
        // current popped element is N
        if (t <= N)
        {
            cnt++;

            // uncomment below line to print actual
            // number in sorted order
            // cout << t << " ";

            q.push(t * 10);
            q.push(t * 10 + 1);
        }
    }

    return cnt;
}

//    Driver code to test above methods
int main()
{
    int N = 200;
    cout << countOfBinaryNumberLessThanN(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.LinkedList;
import java.util.Queue;

// java program to count all binary digit
// numbers smaller than N
public class GFG {

//  method returns count of binary digit
//  numbers smaller than N
    static int countOfBinaryNumberLessThanN(int N) {
        //  queue to store all intermediate binary
        // digit numbers
        Queue<Integer> q = new LinkedList<>();

        //  binary digits start with 1
        q.add(1);
        int cnt = 0;
        int t;

        //  loop until we have element in queue
        while (q.size() > 0) {
            t = q.peek();
            q.remove();

            //  push next binary digit numbers only if
            // current popped element is N
            if (t <= N) {
                cnt++;

                // uncomment below line to print actual
                // number in sorted order
                // cout << t << " ";
                q.add(t * 10);
                q.add(t * 10 + 1);
            }
        }

        return cnt;
    }

//    Driver code to test above methods
    static public void main(String[] args) {
        int N = 200;
        System.out.println(countOfBinaryNumberLessThanN(N));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count all binary digit
# numbers smaller than N
from collections import deque

# method returns count of binary digit
# numbers smaller than N
def countOfBinaryNumberLessThanN(N):
    # queue to store all intermediate binary
    # digit numbers
    q = deque()

    # binary digits start with 1
    q.append(1)
    cnt = 0

    # loop until we have element in queue
    while (q):
        t = q.popleft()

        # push next binary digit numbers only if
        # current popped element is N
        if (t <= N):
            cnt = cnt + 1
            # uncomment below line to print actual
            # number in sorted order
            q.append(t * 10)
            q.append(t * 10 + 1)

    return cnt

# Driver code to test above methods
if __name__=='__main__':
    N = 200
    print(countOfBinaryNumberLessThanN(N))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count all binary digit
// numbers smaller than N
using System;
using System.Collections.Generic;

class GFG
{

    // method returns count of binary digit
    // numbers smaller than N
    static int countOfBinaryNumberLessThanN(int N)
    {

        // queue to store all intermediate binary
        // digit numbers
        Queue<int> q = new Queue<int>();

        // binary digits start with 1
        q.Enqueue(1);
        int cnt = 0;
        int t;

        // loop until we have element in queue
        while (q.Count > 0)
        {
            t = q.Peek();
            q.Dequeue();

            // push next binary digit numbers only if
            // current popped element is N
            if (t <= N)
            {
                cnt++;

                // uncomment below line to print actual
                // number in sorted order
                q.Enqueue(t * 10);
                q.Enqueue(t * 10 + 1);
            }
        }

        return cnt;
    }

    // Driver code 
    static void Main()
    {
        int N = 200;
        Console.WriteLine(countOfBinaryNumberLessThanN(N));
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all binary digit
// numbers smaller than N

// method returns count of binary digit
// numbers smaller than N
function countOfBinaryNumberLessThanN($N)
{
    // queue to store all intermediate
    // binary digit numbers
    $q = array();

    // binary digits start with 1
    array_push($q, 1);
    $cnt = 0;
    $t = 0;

    // loop until we have element in queue
    while (!empty($q))
    {
        $t = array_pop($q);

        // push next binary digit numbers only
        // if current popped element is N
        if ($t <= $N)
        {
            $cnt++;

            // uncomment below line to print
            // actual number in sorted order
            // cout << t << " ";

            array_push($q, $t * 10);
            array_push($q, ($t * 10 + 1));
        }
    }

    return $cnt;
}

// Driver Code
$N = 200;
echo countOfBinaryNumberLessThanN($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
      // JavaScript program to count all binary digit
      // numbers smaller than N
      // method returns count of binary digit
      // numbers smaller than N
      function countOfBinaryNumberLessThanN(N) {
        // queue to store all intermediate binary
        // digit numbers
        var q = [];

        // binary digits start with 1
        q.push(1);
        var cnt = 0;
        var t;

        // loop until we have element in queue
        while (q.length > 0) {
          t = q.pop();

          // push next binary digit numbers only if
          // current popped element is N
          if (t <= N) {
            cnt++;

            // uncomment below line to print actual
            // number in sorted order
            q.push(t * 10);
            q.push(t * 10 + 1);
          }
        }

        return cnt;
      }

      // Driver code
      var N = 200;
      document.write(countOfBinaryNumberLessThanN(N) + "<br>");
</script>
```

**输出:**

```
7
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。