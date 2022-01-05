# 给定时间表的 n 批次 m 个活动的最小房间数

> 原文:[https://www . geeksforgeeks . org/给定时间表的 n 批活动最少房间数/](https://www.geeksforgeeks.org/minimum-rooms-for-m-events-of-n-batches-with-given-schedule/)

这所学校有 n 个学生团体。在学校的每一天，都有 m 个时间段。学生团体在某个时间段可能有空，也可能没有空。给定 n 个二进制字符串，其中每个二进制字符串的长度为 m。如果第 I 个组在第 j 个槽中空闲，则第 I 个字符串中第 j 个位置的字符为 0，如果第 I 个组忙，则为 1。
我们的任务是确定在一个学习日内为所有小组上课所需的最小房间数。请注意，一个房间在一个时间段内最多只能容纳一个团体课。
**例:**

> 输入:n = 2，m = 7，槽[]= {“0101010”、“1010101”}
> 输出:1
> 说明:两组都可以在一个房间里上课，因为他们有备选班级。
> 输入:n = 3，m = 7，槽[]= {“0101011”、“0011001”、“0110111”}
> 输出:3

**使用的方法:**这里我们遍历我们拥有的字符串的每个字符，并在遍历时保持字符串每个位置的 1 的计数，因此我们知道每个特定时隙的重合类的数量。然后我们只需要在所有时隙中找到最大数量的重合类。

## C++

```
// CPP program to find minimum number of rooms
// required
#include <bits/stdc++.h>
using namespace std;

// Returns minimum number of rooms required
// to perform classes of n groups in m slots
// with given schedule.
int findMinRooms(string slots[], int n, int m)
{
    // Store count of classes happening in
    // every slot.
    int counts[m] = { 0 };
    for (int i = 0; i < n; i++)    
        for (int j = 0; j < m; j++)        
            if (slots[i][j] == '1')
                counts[j]++;

    // Number of rooms required is equal to
    // maximum classes happening in a
    // particular slot.
    return *max_element(counts, counts+m);     
}

// Driver Code
int main()
{
    int n = 3, m = 7;
    string slots[n] = { "0101011",
                        "0011001",
                        "0110111" };
    cout << findMinRooms(slots, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find the minimum number
// of rooms required
class GFG {

    // Returns minimum number of rooms required
    // to perform classes of n groups in m slots
    // with given schedule.
    static int findMinRooms(String slots[],
                                   int n, int m)
    {

        // Store number of class happening in
        //empty slot
        int counts[] = new int[m];

        //initialize all values to zero
        for (int i = 0; i < m; i++)
            counts[i] = 0;

        for (int i = 0; i < n; i++)    
            for (int j = 0; j < m; j++)        
                if (slots[i].charAt(j) == '1')
                    counts[j]++;

        // Number of rooms required is equal to
        // maximum classes happening in a
        // particular slot.

        int max = -1;
        // find the max element
        for (int i = 0; i < m; i++)
            if(max < counts[i])
                max = counts[i];

        return max;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 3, m = 7;
        String slots[] = { "0101011",
                           "0011001",
                           "0110111" };
        System.out.println( findMinRooms(slots, n, m));
    }
}

// This code is contributed by Arnab Kundu.
```

## 蟒蛇 3

```
# Python3 program to find minimum
# number of rooms required

# Returns minimum number of
# rooms required to perform
# classes of n groups in m
# slots with given schedule.
def findMinRooms(slots, n, m):

    # Store count of classes
    # happening in every slot.
    counts = [0] * m;
    for i in range(n):
        for j in range(m):
            if (slots[i][j] == '1'):
                counts[j] += 1;

    # Number of rooms required is
    # equal to maximum classes
    # happening in a particular slot.
    return max(counts);

# Driver Code
n = 3;
m = 7;
slots = ["0101011", "0011001", "0110111"];
print(findMinRooms(slots, n, m));

# This code is contributed by mits
```

## C#

```
// C# program to find the minimum number
// of rooms required
using System;
class GFG {

    // Returns minimum number of rooms required
    // to perform classes of n groups in m slots
    // with given schedule.
    static int findMinRooms(string []slots,
                                   int n, int m)
    {

        // Store number of class happening in
        //empty slot
        int []counts = new int[m];

        //initialize all values to zero
        for (int i = 0; i < m; i++)
            counts[i] = 0;

        for (int i = 0; i < n; i++)    
            for (int j = 0; j < m; j++)        
                if (slots[i][j] == '1')
                    counts[j]++;

        // Number of rooms required is equal to
        // maximum classes happening in a
        // particular slot.

        int max = -1;
        // find the max element
        for (int i = 0; i < m; i++)
            if(max < counts[i])
                max = counts[i];

        return max;
    }

    // Driver Code
    public static void Main()
    {
        int n = 3, m = 7;
        String []slots = { "0101011",
                           "0011001",
                           "0110111" };
        Console.Write( findMinRooms(slots, n, m));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// number of rooms required

// Returns minimum number of
// rooms required to perform
// classes of n groups in m
// slots with given schedule.
function findMinRooms($slots, $n, $m)
{
    // Store count of classes
    // happening in every slot.
    $counts = array_fill(0, $m, 0);
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $m; $j++)    
            if ($slots[$i][$j] == '1')
                $counts[$j]++;

    // Number of rooms required is
    // equal to maximum classes
    // happening in a particular slot.
    return max($counts);    
}

// Driver Code
$n = 3;
$m = 7;
$slots = array("0101011", "0011001",
                          "0110111");
echo findMinRooms($slots, $n, $m);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the minimum number
// of rooms required

    // Returns minimum number of rooms required
    // to perform classes of n groups in m slots
    // with given schedule.
    function findMinRooms(slots, n, m)
    {

        // Store number of class happening in
        //empty slot
        let counts = Array(m).fill(0);

        //initialize all values to zero
        for (let i = 0; i < m; i++)
            counts[i] = 0;

        for (let i = 0; i < n; i++)    
            for (let j = 0; j < m; j++)        
                if (slots[i][j] == '1')
                    counts[j]++;

        // Number of rooms required is equal to
        // maximum classes happening in a
        // particular slot.

        let max = -1;
        // find the max element
        for (let i = 0; i < m; i++)
            if(max < counts[i])
                max = counts[i];

        return max;
    }

// driver code

     let n = 3, m = 7;
        let slots = [ "0101011",
                           "0011001",
                           "0110111" ];
        document.write( findMinRooms(slots, n, m));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(m * n)
T3】辅助空间: O(m)