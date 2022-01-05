# 程序查找戴白帽子的人数

> 原文:[https://www . geesforgeks . org/program-find-number-persons-wear-white-hat/](https://www.geeksforgeeks.org/program-find-number-persons-wearing-white-hat/)

一个房间里有 **N** 个人，每个人都戴着一顶非黑即白的帽子。每个人都数着戴着白帽子的其他人的数量。给定每个人的人数，任务是找到戴白帽子的人数，如果给定的人数与有效情况不符，则打印-1。
示例:

```
Input : arr[] = {2, 1, 1}.
Output : 2
First person sees two white hats. Second
and third persons see one white hat. The 
first person must be wearing a black hat
and other two must be wearing a white hat.

Input : arr[] = {2, 2, 2}
Output : 3
All are wearing white hats.

Input : arr[] = {10, 10}
Output : -1
There are only two persons, count can't be 10.
```

人只有两种。如果每个人都数对了(有效情况)，那么每个戴白帽子的人的计数值都是一样的。而且，每个戴黑帽子的人的计数值都是一样的。所以数组中只有一两种类型的值。
假设白帽数量为 I，0 < = i < = N-1。
现在观察每个戴白色帽子的人，计数值为 I–1。所以会有 I 个人的计数是 i-1。
同样，戴黑色帽子的人数将为 N–I，他们的给定计数值将为 I。
一个有趣的案例是没有白色帽子。如果所有的值都是 0，那么每个人都戴着一顶黑色的帽子。否则，当有一个人戴着白帽子时，最多只能有一个零。在一个零的情况下，所有其他条目必须为 1。
解决这个问题的算法:

```
1\. Count the frequency of each element of the array.
2\. Since there are one or two types, say x and y.
   a) If the number of x's equal to x + 1 and number 
      of y's equal to n - y. The Number of hats equal
      to y or x + 1.
   b) Otherwise print -1\. 
```

解释示例:

```
Suppose, N = 5, the number of white hats can be range 
from 0 to 4.
For white hats = 1, array will be {0, 1, 1, 1, 1}.
Number of 0's = 0 + 1 = 1\. 
Number of 1's = 5 - 1 = 4.

For white hats = 2, array will be {1, 1, 2, 2, 2}.
Number of 1's = 1 + 1 = 2\. 
Number of 2's = 5 - 3 = 2.

For white hats = 3, array will be {2, 2, 2, 3, 3}.
Number of 2's = 2 + 1 = 3\. 
Number of 3's = 5 - 3 = 2.

For white hats = 5, array will be {4, 4, 4, 4, 4}.
Number of 4's = 4 + 1 = 5\. 
Number of 5's = 5 - 5 = 0\. 
```

以下是该方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count number of white hats
#include<bits/stdc++.h>
using namespace std;

// Given counts of White hats seen by n people,
// return count of white hats.
int numOfWhiteHats(int arr[], int n)
{
    // Counting frequencies of all values in given
    // array
    int freq[n+1];
    memset(freq, 0, sizeof(freq));
    for (int i=0; i<n; i++)
    {
        // Count of White hats cannot be more than
        // n for n persons.
        if (arr[i] >= n)
            return -1;
        freq[arr[i]]++;
    }

    // Counting number of different frequencies
    int diffFreq = 0;
    for (int i = n-1; i >= 0; i--)
        if (freq[i])
            diffFreq++;

    // Cases where all the persons wearing white hat.
    if (diffFreq == 1 && freq[n-1] == n)
        return n;

    // Case where no one wearing white hat.
    if (diffFreq == 1 && freq[0] == n)
        return 0;

    // Else : number of distinct frequency must be 2.
    if (diffFreq != 2)
        return -1;

    // Finding the last frequency with non zero value.
    // Note that we traverse from right side.
    int k;
    for (k = n-1; k >= 1; k--)
        if (freq[k])
            break;

    // Checking number of k's must be n - k.
    // And number of (k-1)'s must be k.
    if (freq[k-1] == k && freq[k] + k == n)
        return freq[k-1];
    else
        return -1;
}

// Driver code
int main()
{
    int arr[] = {2, 2, 2, 3, 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << numOfWhiteHats(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of white hats
import java.util.Arrays;

class GFG {

    // Given counts of White hats seen by n
    // people, return count of white hats.
    static int numOfWhiteHats(int arr[], int n)
    {

        // Counting frequencies of all values
        // in given array
        int freq[] = new int[n + 1];
        Arrays.fill(freq, 0);

        for (int i = 0; i < n; i++) {

            // Count of White hats cannot be
            // more than n for n persons.
            if (arr[i] >= n)
                return -1;

            freq[arr[i]]++;
        }

        // Counting number of different
        // frequencies
        int diffFreq = 0;

        for (int i = n - 1; i >= 0; i--)
            if (freq[i] > 0)
                diffFreq++;

        // Cases where all the persons wearing
        // white hat.
        if (diffFreq == 1 && freq[n - 1] == n)
            return n;

        // Case where no one wearing white hat.
        if (diffFreq == 1 && freq[0] == n)
            return 0;

        // Else : number of distinct frequency
        // must be 2.
        if (diffFreq != 2)
            return -1;

        // Finding the last frequency with non
        // zero value.
        // Note that we traverse from right side.
        int k;

        for (k = n - 1; k >= 1; k--)
            if (freq[k] > 0)
                break;

        // Checking number of k's must be n - k.
        // And number of (k-1)'s must be k.
        if (freq[k - 1] == k && freq[k] + k == n)
            return freq[k - 1];
        else
            return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 2, 2, 3, 3 };
        int n = arr.length;
        System.out.print(numOfWhiteHats(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# python program to count
# number of white hats

def numOfWhiteHats(arr, n):

    # Counting frequencies of
    # all values in given
    # array
    freq=[0 for i in range(n + 1 + 1)]
    for i in range(n):

        # Count of White hats
        # cannot be more than
        # n for n persons.
        if (arr[i] >= n):
            return -1
        freq[arr[i]]+=1

    # Counting number of
    # different frequencies
    diffFreq = 0
    for i in range(n-1,-1,-1):
        if (freq[i]):
            diffFreq+=1

    # Cases where all the
    # persons wearing white hat.
    if (diffFreq == 1 and freq[n-1] == n):
        return n

    # Case where no one
    # wearing white hat.
    if (diffFreq == 1 and freq[0] == n):
        return 0

    # Else : number of distinct
    # frequency must be 2.
    if (diffFreq != 2):
        return -1

    # Finding the last frequency
    # with non zero value.
    # Note that we traverse
    # from right side.
    for k in range(n - 1, 0, -1):
        if (freq[k]):
            break

    # Checking number of k's
    # must be n - k.
    # And number of (k-1)'s
    # must be k.
    if (freq[k-1] == k and freq[k] + k == n):
        return freq[k-1]
    else:
        return -1

# Driver code

arr= [2, 2, 2, 3, 3]
n= len(arr)
print(numOfWhiteHats(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count number of white hats
using System;

class GFG {

    // Given counts of White hats seen by n
    // people, return count of white hats.
    static int numOfWhiteHats(int []arr, int n)
    {
        // Counting frequencies of all values
        // in given array
        int []freq = new int[n + 1];
        //Arrays.fill(freq, 0);

        for (int i = 0; i < n; i++) {

            // Count of White hats cannot be
            // more than n for n persons.
            if (arr[i] >= n)
                return -1;

            freq[arr[i]]++;
        }

        // Counting number of different
        // frequencies
        int diffFreq = 0;

        for (int i = n - 1; i >= 0; i--)
            if (freq[i] > 0)
                diffFreq++;

        // Cases where all the persons wearing
        // white hat.
        if (diffFreq == 1 && freq[n - 1] == n)
            return n;

        // Case where no one wearing white hat.
        if (diffFreq == 1 && freq[0] == n)
            return 0;

        // Else : number of distinct frequency
        // must be 2.
        if (diffFreq != 2)
            return -1;

        // Finding the last frequency with non
        // zero value.
        // Note that we traverse from right side.
        int k;

        for (k = n - 1; k >= 1; k--)
            if (freq[k] > 0)
                break;

        // Checking number of k's must be n - k.
        // And number of (k-1)'s must be k.
        if (freq[k - 1] == k && freq[k] + k == n)
            return freq[k - 1];
        else
            return -1;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {2, 2, 2, 3, 3};
        int n = arr.Length;
        Console.WriteLine(numOfWhiteHats(arr, n));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>
// javascript program to count number of white hats

    // Given counts of White hats seen by n
    // people, return count of white hats.
    function numOfWhiteHats(arr, n)
    {

        // Counting frequencies of all values
        // in given array
        var freq = Array(n + 1).fill(0);
        for (i = 0; i < n; i++)
        {

            // Count of White hats cannot be
            // more than n for n persons.
            if (arr[i] >= n)
                return -1;
            freq[arr[i]]++;
        }

        // Counting number of different
        // frequencies
        var diffFreq = 0;
        for (i = n - 1; i >= 0; i--)
            if (freq[i] > 0)
                diffFreq++;

        // Cases where all the persons wearing
        // white hat.
        if (diffFreq == 1 && freq[n - 1] == n)
            return n;

        // Case where no one wearing white hat.
        if (diffFreq == 1 && freq[0] == n)
            return 0;

        // Else : number of distinct frequency
        // must be 2.
        if (diffFreq != 2)
            return -1;

        // Finding the last frequency with non
        // zero value.
        // Note that we traverse from right side.
        var k;

        for (k = n - 1; k >= 1; k--)
            if (freq[k] > 0)
                break;

        // Checking number of k's must be n - k.
        // And number of (k-1)'s must be k.
        if (freq[k - 1] == k && freq[k] + k == n)
            return freq[k - 1];
        else
            return -1;
    }

    // Driver code
    var arr = [ 2, 2, 2, 3, 3 ];
    var n = arr.length;
    document.write(numOfWhiteHats(arr, n));

// This code is contributed by Rajput-Ji.
</script>
```

输出:

```
3
```

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。