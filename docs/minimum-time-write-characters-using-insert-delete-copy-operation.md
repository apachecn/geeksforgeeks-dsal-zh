# 使用插入、删除和复制操作写入字符的最短时间

> 原文:[https://www . geesforgeks . org/最短时间-写入-字符-使用-插入-删除-复制-操作/](https://www.geeksforgeeks.org/minimum-time-write-characters-using-insert-delete-copy-operation/)

我们需要在一个屏幕上写 N 个相同的字符，每次我们可以插入一个字符，删除最后一个字符，复制并粘贴所有写入的字符，即在复制操作后，总写入字符的计数将变成两次。现在我们有时间插入、删除和复制。我们需要输出使用这些操作在屏幕上写 N 个字符的最短时间。

**示例:**

```
Input : N = 9    
        insert time = 1    
        removal time = 2    
        copy time = 1
Output : 5
N character can be written on screen in 5 time units as shown below,
insert a character    
characters = 1  total time = 1
again insert character      
characters = 2  total time = 2
copy characters             
characters = 4  total time = 3
copy characters             
characters = 8  total time = 4
insert character           
characters = 9  total time = 5
```

我们可以用动态规划来解决这个问题。我们可以在手工解决一些例子后观察到一种模式，对于书写每个字符，我们有两种选择，要么通过插入得到它，要么通过复制得到它，以时间较短者为准。现在写关系相应地，
让 dp[i]是在屏幕上写 I 个字符的最佳时间，

```
If i is even then,
   dp[i] = min((dp[i-1] + insert_time), 
               (dp[i/2] + copy_time))
Else (If i is odd)
   dp[i] = min(dp[i-1] + insert_time),
              (dp[(i+1)/2] + copy_time + removal_time)
```

在奇数情况下，删除时间被增加，因为当(i+1)/2 个字符将被复制时，一个额外的字符将出现在需要删除的屏幕上。

## C++

```
// C++ program to write characters in
// minimum time by inserting, removing
// and copying operation
#include <bits/stdc++.h>
using namespace std;

//  method returns minimum time to write
// 'N' characters
int minTimeForWritingChars(int N, int insert,
                       int remove, int copy)
{
    if (N == 0)
       return 0;
    if (N == 1)
       return insert;

    //  declare dp array and initialize with zero
    int dp[N + 1];
    memset(dp, 0, sizeof(dp));

    // first char will always take insertion time
    dp[1] = insert;

    //  loop for 'N' number of times
    for (int i = 2; i <= N; i++)
    {
        /*  if current char count is even then
            choose minimum from result for (i-1)
            chars and time for insertion and
            result for half of chars and time
            for copy  */
        if (i % 2 == 0)
            dp[i] = min(dp[i-1] + insert,
                        dp[i/2] + copy);

        /*  if current char count is odd then
            choose minimum from
            result for (i-1) chars and time for
            insertion and
            result for half of chars and time for
            copy and one extra character deletion*/
        else
            dp[i] = min(dp[i-1] + insert,
                        dp[(i+1)/2] + copy + remove);
    }
    return dp[N];
}

// Driver code
int main()
{
    int N = 9;
    int insert = 1, remove = 2, copy = 1;
    cout << minTimeForWritingChars(N, insert,
                                remove, copy);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to write characters in
// minimum time by inserting, removing
// and copying operation

public class GFG{

    // method returns minimum time to write
    // 'N' characters
    static int minTimeForWritingChars(int N, int insert,
                                      int remove, int copy)
    {
        if (N == 0)
        return 0;
        if (N == 1)
        return insert;

        // declare dp array and initialize with zero
        int dp[] = new int [N + 1];

          // first char will always take insertion time
          dp[1] = insert;

        // loop for 'N' number of times
        for (int i = 2; i <= N; i++)
        {
            /* if current char count is even then
                choose minimum from result for (i-1)
                chars and time for insertion and
                result for half of chars and time
                for copy */
            if (i % 2 == 0)
                dp[i] = Math.min(dp[i-1] + insert, dp[i/2] + copy);

            /* if current char count is odd then
                choose minimum from
                result for (i-1) chars and time for
                insertion and
                result for half of chars and time for
                copy and one extra character deletion*/
            else
                dp[i] = Math.min(dp[i-1] + insert,
                                 dp[(i+1)/2] + copy + remove);
        }
        return dp[N];
    }

    // Driver code to test above methods
    public static void main(String []args)
    {
        int N = 9;
        int insert = 1, remove = 2, copy = 1;
        System.out.println(minTimeForWritingChars(N, insert,remove, copy));
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 program to write characters in
# minimum time by inserting, removing
# and copying operation

def minTimeForWritingChars(N, insert,
                           remove, cpy):

    # method returns minimum time
    # to write 'N' characters
    if N == 0:
        return 0
    if N == 1:
        return insert

    # declare dp array and initialize
    # with zero
    dp = [0] * (N + 1)

    # first char will always take insertion time
    dp[1] = insert

    # loop for 'N' number of times
    for i in range(2, N + 1):

        # if current char count is even then
        # choose minimum from result for (i-1)
        # chars and time for insertion and
        # result for half of chars and time
        # for copy
        if i % 2 == 0:
            dp[i] = min(dp[i - 1] + insert,
                        dp[i // 2] + cpy)

        # if current char count is odd then
        # choose minimum from
        # result for (i-1) chars and time for
        # insertion and
        # result for half of chars and time for
        # copy and one extra character deletion
        else:
            dp[i] = min(dp[i - 1] + insert,
                        dp[(i + 1) // 2] +
                        cpy + remove)

    return dp[N]

# Driver Code
if __name__ == "__main__":
    N = 9
    insert = 1
    remove = 2
    cpy = 1
    print(minTimeForWritingChars(N, insert,
                                 remove, cpy))

# This code is contributed
# by vibhu4agarwal
```

## C#

```
// C# program to write characters in
// minimum time by inserting, removing
// and copying operation
using System;

class GFG
{
    // method returns minimum time to write
    // 'N' characters
    static int minTimeForWritingChars(int N, int insert,
                                        int remove, int copy)
    {
        if (N == 0)
            return 0;
        if (N == 1)
            return insert;

        // declare dp array and initialize with zero
        int[] dp = new int[N + 1];
        for(int i = 0; i < N + 1; i++)
            dp[i] = 0;

          // first char will always take insertion time
          dp[1] = insert;

        // loop for 'N' number of times
        for (int i = 2; i <= N; i++)
        {

            /* if current char count is even then
                choose minimum from result for (i-1)
                chars and time for insertion and
                result for half of chars and time
                for copy */
            if (i % 2 == 0)
                dp[i] = Math.Min(dp[i - 1] + insert,
                            dp[i / 2] + copy);

            /* if current char count is odd then
                choose minimum from
                result for (i-1) chars and time for
                insertion and
                result for half of chars and time for
                copy and one extra character deletion*/
            else
                dp[i] = Math.Min(dp[i - 1] + insert,
                            dp[(i + 1) / 2] + copy + remove);
        }
        return dp[N];
    }

    // Driver code
    static void Main()
    {
        int N = 9;
        int insert = 1, remove = 2, copy = 1;
        Console.Write(minTimeForWritingChars(N, insert,
                                            remove, copy));
    }
}

//This code is contributed by DrRoot_
```

## java 描述语言

```
<script>
    // Javascript program to write characters in
    // minimum time by inserting, removing
    // and copying operation

    // method returns minimum time to write
    // 'N' characters
    function minTimeForWritingChars(N, insert, remove, copy)
    {
        if (N == 0)
            return 0;
        if (N == 1)
            return insert;

        // declare dp array and initialize with zero
        let dp = new Array(N + 1);
        for(let i = 0; i < N + 1; i++)
            dp[i] = 0;

          // first char will always take insertion time
          dp[1] = insert;

        // loop for 'N' number of times
        for (let i = 2; i <= N; i++)
        {

            /* if current char count is even then
                choose minimum from result for (i-1)
                chars and time for insertion and
                result for half of chars and time
                for copy */
            if (i % 2 == 0)
                dp[i] = Math.min(dp[i - 1] + insert, dp[parseInt(i / 2, 10)] + copy);

            /* if current char count is odd then
                choose minimum from
                result for (i-1) chars and time for
                insertion and
                result for half of chars and time for
                copy and one extra character deletion*/
            else
                dp[i] = Math.min(dp[i - 1] + insert,
                            dp[parseInt((i + 1) / 2, 10)] + copy + remove);
        }
        return dp[N];
    }

    let N = 9;
    let insert = 1, remove = 2, copy = 1;
    document.write(minTimeForWritingChars(N, insert,
                                         remove, copy));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output**

```
5
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)。

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。