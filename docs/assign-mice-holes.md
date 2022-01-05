# 给洞分配老鼠

> 原文:[https://www.geeksforgeeks.org/assign-mice-holes/](https://www.geeksforgeeks.org/assign-mice-holes/)

有 N 只老鼠，N 个洞排成一条直线。每个孔只能容纳 1 只鼠标。鼠标可以停留在自己的位置，从 x 向右移动一步到 x + 1，或者从 x 向左移动一步到 x -1。这些移动都会消耗 1 分钟。将老鼠分配到洞内，这样最后一只老鼠进入洞内的时间就最小化了。

**示例:**

```
Input : positions of mice are:
          4 -4 2
        positions of holes are:
          4 0 5
Output :  4
Assign mouse at position x = 4 to hole at 
position x = 4 : Time taken is 0 minutes 
Assign mouse at position x=-4 to hole at 
position x = 0 : Time taken is 4 minutes 
Assign mouse at position x=2 to hole at 
position x = 5 : Time taken is 3 minutes 
After 4 minutes all of the mice are in the holes.
Since, there is no combination possible where
the last mouse's time is less than 4, 
answer = 4.

Input :  positions of mice are:
        -10, -79, -79, 67, 93, -85, -28, -94 
          positions of holes are:
         -2, 9, 69, 25, -31, 23, 50, 78 
Output : 102
```

这个问题可以用贪婪策略来解决。我们可以把每只老鼠放在离它最近的洞里，以尽量减少时间。这可以通过对老鼠和洞的位置进行排序来完成。这允许我们将 ith 鼠标放入孔列表中相应的孔中。然后我们可以找到老鼠和相应洞位置之间的最大差异。

在示例 2 中，在对两个列表进行排序时，我们发现在位置-79 的鼠标是最后一个移动到洞 23 的，花费时间 102。

```
sort mice positions (in any order)
sort hole positions 

Loop i = 1 to N:
    update ans according to the value 
    of |mice(i) - hole(i)|. It should
    be maximum of all differences.
```

**正确性证明:**
设 i1 < i2 为两只老鼠的位置，设 j1 < j2 为两个洞的位置。
通过案例分析足以表明

```
max(|i1-j1|, |i2-j2|) <= max(|i1-j2|, |i2-j1|), 
   where '|a - b|' represent absolute value of (a - b)
```

因为根据归纳，每个赋值都可以通过一系列交换转换成排序赋值，这些交换都不会增加跨度。

## C++

```
// C++ program to find the minimum
// time to place all mice in all holes.
#include <bits/stdc++.h>
using namespace std;

// Returns minimum time required
// to place mice in holes.
int assignHole(int mices[], int holes[],
               int n, int m)
{

    // Base Condition
    // No. of mouse and holes should be same
    if (n != m)
        return -1;

    // Sort the arrays
    sort(mices, mices + n);
    sort(holes, holes + m);

    // Finding max difference between
    // ith mice and hole
    int max = 0;
    for(int i = 0; i < n; ++i)
    {
        if (max < abs(mices[i] - holes[i]))
            max = abs(mices[i] - holes[i]);
    }
    return max;
}

// Driver Code
int main()
{

    // Position of mouses 
    int mices[] = { 4, -4, 2 };

    // Position of holes
    int holes[] = { 4, 0, 5 };

    // Number of mouses
    int n = sizeof(mices) / sizeof(mices[0]);

    // Number of holes
    int m = sizeof(holes) / sizeof(holes[0]);

    // The required answer is returned
    // from the function
    int minTime = assignHole(mices, holes, n, m);

    cout << "The last mouse gets into the hole in time:"
         << minTime << endl;

    return 0;
}

// This code is contributed by Aayush Garg
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum time to place
// all mice in all holes.
import java.util.* ;

public class GFG
{
    // Returns minimum time required to place mice
    // in holes.
    public int assignHole(ArrayList<Integer> mice,
                         ArrayList<Integer> holes)
    {
        if (mice.size() != holes.size())
           return -1;

        /* Sort the lists */
        Collections.sort(mice);
        Collections.sort(holes);

        int size = mice.size();

        /* finding max difference between ith mice and hole */
        int max = 0;
        for (int i=0; i<size; i++)
            if (max < Math.abs(mice.get(i)-holes.get(i)))
                max = Math.abs(mice.get(i)-holes.get(i));

        return Math.abs(max);
    }

    /* Driver Function to test other functions */
    public static void main(String[] args)
    {
        GFG gfg = new GFG();
        ArrayList<Integer> mice = new ArrayList<Integer>();
        mice.add(4);
        mice.add(-4);
        mice.add(2);
        ArrayList<Integer> holes= new ArrayList<Integer>();
        holes.add(4);
        holes.add(0);
        holes.add(5);
        System.out.println("The last mouse gets into "+
         "the hole in time: "+gfg.assignHole(mice, holes));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# time to place all mice in all holes.

# Returns minimum time required
# to place mice in holes.
def assignHole(mices, holes, n, m):

    # Base Condition
    # No. of mouse and holes should be same
    if (n != m):
        return -1

    # Sort the arrays
    mices.sort()
    holes.sort()

    # Finding max difference between
    # ith mice and hole
    Max = 0

    for i in range(n):
        if (Max < abs(mices[i] - holes[i])):
            Max = abs(mices[i] - holes[i])

    return Max

# Driver code   

# Position of mouses
mices = [ 4, -4, 2 ]

# Position of holes
holes = [ 4, 0, 5 ]

# Number of mouses
n = len(mices)

# Number of holes
m = len(holes)

# The required answer is returned
# from the function
minTime = assignHole(mices, holes, n, m)

print("The last mouse gets into the hole in time:", minTime)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find the minimum
// time to place all mice in all holes.
using System;
class GFG
{

    // Returns minimum time required
    // to place mice in holes.
    static int assignHole(int[] mices, int[] holes,
                   int n, int m)
    {

        // Base Condition
        // No. of mouse and holes should be same
        if (n != m)
            return -1;

        // Sort the arrays
        Array.Sort(mices);
        Array.Sort(holes);

        // Finding max difference between
        // ith mice and hole
        int max = 0;
        for(int i = 0; i < n; ++i)
        {
            if (max < Math.Abs(mices[i] - holes[i]))
                max = Math.Abs(mices[i] - holes[i]);
        }
        return max;
    }

  // Driver code    
  static void Main()
  {

    // Position of mouses 
    int[] mices = { 4, -4, 2 };

    // Position of holes
    int[] holes = { 4, 0, 5 };

    // Number of mouses
    int n = mices.Length;

    // Number of holes
    int m = holes.Length;

    // The required answer is returned
    // from the function
    int minTime = assignHole(mices, holes, n, m);
    Console.WriteLine("The last mouse gets into the hole in time: " + minTime);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript program to find the minimum
    // time to place all mice in all holes.

    // Returns minimum time required
    // to place mice in holes.
    function assignHole(mices, holes, n, m)
    {

        // Base Condition
        // No. of mouse and holes should be same
        if (n != m)
            return -1;

        // Sort the arrays
        mices.sort();
        holes.sort();

        // Finding max difference between
        // ith mice and hole
        let max = 0;
        for(let i = 0; i < n; ++i)
        {
            if (max < Math.abs(mices[i] - holes[i]))
                max = Math.abs(mices[i] - holes[i]);
        }
        return max;
    }

    // Position of mouses
    let mices = [ 4, -4, 2 ];

    // Position of holes
    let holes = [ 4, 0, 5 ];

    // Number of mouses
    let n = mices.length;

    // Number of holes
    let m = holes.length;

    // The required answer is returned
    // from the function
    let minTime = assignHole(mices, holes, n, m);

    document.write("The last mouse gets into the hole in time:" + minTime);

     // This code is contributed by mukesh07.
</script>
```

**Output**

```
The last mouse gets into the hole in time: 4
```

本文由**萨罗尼·巴韦贾**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。