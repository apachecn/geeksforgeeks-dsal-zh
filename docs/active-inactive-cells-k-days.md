# k 天后的活跃和不活跃细胞

> 原文:[https://www.geeksforgeeks.org/active-inactive-cells-k-days/](https://www.geeksforgeeks.org/active-inactive-cells-k-days/)

给定大小为 n 的二进制数组，其中 **n > 3** 。数组中的真(或 1)值表示活动，假(或 0)表示不活动。给定一个数字 k，任务是找到 k 天后活动和非活动细胞的计数。每天之后，如果左右单元格不相同，则第 I 个单元格的状态变为活动，如果左右单元格相同(均为 0 或均为 1)，则变为非活动。
由于最左边和最右边的单元格前没有单元格，所以最左边和最右边的单元格前的值单元格总是被认为是 0(或无效)。

**例:**

```
Input  : cells[] = {1, 0, 1, 1}, k = 2
Output : Active cells = 3, Inactive cells = 1
After 1 day,  cells[] = {0, 0, 1, 1}
After 2 days, cells[] = {0, 1, 1, 1}

Input : cells[] = {0, 1, 0, 1, 0, 1, 0, 1},  k = 3
Output: Active Cells = 2 , Inactive Cells = 6
Explanation : 
After 1 day, cells[] = {1, 0, 0, 0, 0, 0, 0, 0}
After 2 days, cells[] = {0, 1, 0, 0, 0, 0, 0, 0}
After 3 days, cells[] =  {1, 0, 1, 0, 0, 0, 0, 0}

Input : cells[] = {0, 1, 1, 1, 0, 1, 1, 0},  k = 4
Output: Active Cells = 3 , Inactive Cells = 5
```

唯一重要的是确保我们维护给定数组的副本，因为我们需要以前的值来更新第二天。下面是详细的步骤。

1.  首先，我们将单元格[]数组复制到 temp[]数组中，并根据给定的条件在 temp[]数组中进行更改。
2.  在这种情况下，假设如果第一个单元格的左单元格和右单元格不活动或活动，第二天我就变得不活动，即；(单元格[i-1] == 0 和单元格[i+1] == 0)或(单元格[i-1] == 1 和单元格[i+1] == 1)然后单元格[i] = 0，这些条件可以使用单元格[i-1]和单元格[i+1]的异或来应用。
3.  对于第 0 个索引单元温度[0] = 0^cells[1]和第(n-1)个索引单元温度[n-1] = 0^cells[n-2].
4.  现在对于索引 1 到 n-2，执行以下操作 temp[i] = cells[i-1] ^ cells[i+1]
5.  重复这个过程，直到 k 天完成。

以下是上述步骤的实现。

## C++

```
// C++ program to count active and inactive cells after k
// days
#include<bits/stdc++.h>
using namespace std;

// cells[] - store current status of cells
// n - Number of cells
// temp[] - to perform intermediate operations
// k - number of days
// active - count of active cells after k days
// inactive - count of active cells after k days
void activeAndInactive(bool cells[], int n, int k)
{
    // copy cells[] array into temp [] array
    bool temp[n];
    for (int i=0; i<n ; i++)
        temp[i] = cells[i];

    // Iterate for k days
    while (k--)
    {
        // Finding next values for corner cells
        temp[0]   = 0^cells[1];
        temp[n-1] = 0^cells[n-2];

        // Compute values of intermediate cells
        // If both cells active or inactive, then temp[i]=0
        // else temp[i] = 1.
        for (int i=1; i<=n-2; i++)
            temp[i] = cells[i-1] ^ cells[i+1];

        // Copy temp[] to cells[] for next iteration
        for (int i=0; i<n; i++)
            cells[i] = temp[i];
    }

    // count active and inactive cells
    int active = 0, inactive = 0;
    for (int i=0; i<n; i++)
        (cells[i] == 1)? active++ : inactive++;

    printf("Active Cells = %d, Inactive Cells = %d",
           active, inactive);
}

// Driver program to check the test case
int main()
{
    bool cells[] = {0, 1, 0, 1, 0, 1, 0, 1};
    int k = 3;
    int n =  sizeof(cells)/sizeof(cells[0]);
    activeAndInactive(cells, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count active and
// inactive cells after k days

class GFG {

// cells[] - store current status
// of cells n - Number of cells
// temp[] - to perform intermediate operations
// k - number of days
// active - count of active cells after k days
// inactive - count of active cells after k days
static void activeAndInactive(boolean cells[],
                                 int n, int k)
{
    // copy cells[] array into temp [] array
    boolean temp[] = new boolean[n];
    for (int i = 0; i < n; i++)
    temp[i] = cells[i];

    // Iterate for k days
    while (k-- > 0) {

    // Finding next values for corner cells
    temp[0] = false ^ cells[1];
    temp[n - 1] = false ^ cells[n - 2];

    // Compute values of intermediate cells
    // If both cells active or inactive, then
    // temp[i]=0 else temp[i] = 1.
    for (int i = 1; i <= n - 2; i++)
        temp[i] = cells[i - 1] ^ cells[i + 1];

    // Copy temp[] to cells[] for next iteration
    for (int i = 0; i < n; i++)
        cells[i] = temp[i];
    }

    // count active and inactive cells
    int active = 0, inactive = 0;
    for (int i = 0; i < n; i++)
    if (cells[i] == true)
        active++;
    else
        inactive++;

    System.out.print("Active Cells = " + active + ", " +
                     "Inactive Cells = " + inactive);
}

// Driver code
public static void main(String[] args)
{
    boolean cells[] = {false, true, false, true,
                       false, true, false, true};
    int k = 3;
    int n = cells.length;
    activeAndInactive(cells, n, k);
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to count
# active and inactive cells after k
# days

# cells[] - store current
# status of cells
# n - Number of cells
# temp[] - to perform
# intermediate operations
# k - number of days
# active - count of active
# cells after k days
# inactive - count of active
# cells after k days
def activeAndInactive(cells,n,k):

    # copy cells[] array into temp [] array
    temp=[]
    for i in range(n+1):
        temp.append(False)
    for i in range(n):
        temp[i] = cells[i]

    # Iterate for k days
    while (k >0):

        # Finding next values for corner cells
        temp[0]   = False^cells[1]
        temp[n-1] = False^cells[n-2]

        # Compute values of intermediate cells
        # If both cells active or
        # inactive, then temp[i]=0
        # else temp[i] = 1.
        for i in range(1,n-2+1):
            temp[i] = cells[i-1] ^ cells[i+1]

        # Copy temp[] to cells[]
        # for next iteration
        for i in range(n):
            cells[i] = temp[i]
        k-=1

    # count active and inactive cells
    active = 0
    inactive = 0;
    for i in range(n):
        if(cells[i] == True):
            active+=1
        else:
            inactive+=1

    print("Active Cells =",active," , "
          , "Inactive Cells =",
           inactive)

# Driver code

cells = [False, True, False, True,
         False, True, False, True]
k = 3
n =len(cells)

activeAndInactive(cells, n, k)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to count active and
// inactive cells after k days
using System;

class GFG {

// cells[] - store current status
// of cells n - Number of cells
// temp[] - to perform intermediate
// operations k - number of days
// active - count of active cells
// after k days inactive - count
// of active cells after k days
static void activeAndInactive(bool []cells,
                              int n, int k)
{

    // copy cells[] array into
    // temp [] array
    bool []temp = new bool[n];
    for (int i = 0; i < n; i++)
    temp[i] = cells[i];

    // Iterate for k days
    while (k-- > 0) {

    // Finding next values
    // for corner cells
    temp[0] = false ^ cells[1];
    temp[n - 1] = false ^ cells[n - 2];

    // Compute values of intermediate cells
    // If both cells active or inactive, then
    // temp[i]=0 else temp[i] = 1.
    for (int i = 1; i <= n - 2; i++)
        temp[i] = cells[i - 1] ^ cells[i + 1];

    // Copy temp[] to cells[]
    // for next iteration
    for (int i = 0; i < n; i++)
        cells[i] = temp[i];
    }

    // count active and inactive cells
    int active = 0, inactive = 0;
    for (int i = 0; i < n; i++)
    if (cells[i] == true)
        active++;
    else
        inactive++;

    Console.Write("Active Cells = " + active + ", " +
                  "Inactive Cells = " + inactive);
}

// Driver code
public static void Main()
{
    bool []cells = {false, true, false, true,
                    false, true, false, true};
    int k = 3;
    int n = cells.Length;
    activeAndInactive(cells, n, k);
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count active
// and inactive cells after k
// days

// cells[] - store current status
// of cells n - Number of cells
// temp[] - to perform intermediate
// operations k - number of days
// active - count of active cells
// after k days inactive - count of
// active cells after k days
function activeAndInactive($cells, $n, $k)
{

    // copy cells[] array into
    // temp [] array
    $temp = array();
    for ($i = 0; $i < $n ; $i++)
        $temp[$i] = $cells[$i];

    // Iterate for k days
    while ($k--)
    {

        // Finding next values
        // for corner cells
        $temp[0] = 0 ^ $cells[1];
        $temp[$n - 1] = 0 ^ $cells[$n - 2];

        // Compute values of
        // intermediate cells
        // If both cells active
        // or inactive, then temp[i]=0
        // else temp[i] = 1.
        for ($i = 1; $i <= $n - 2; $i++)
            $temp[$i] = $cells[$i - 1] ^
                        $cells[$i + 1];

        // Copy temp[] to cells[]
        // for next iteration
        for ($i = 0; $i < $n; $i++)
            $cells[$i] = $temp[$i];
    }

    // count active and
    // inactive cells
    $active = 0;$inactive = 0;
    for ($i = 0; $i < $n; $i++)
        ($cells[$i] == 1)? $active++ : $inactive++;

    echo "Active Cells = ", $active, " ,Inactive Cells = ",
    $inactive;
}

    // Driver Code
    $cells= array(0, 1, 0, 1, 0, 1, 0, 1);
    $k = 3;
    $n = count($cells);
    activeAndInactive($cells, $n, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to count active and
// inactive cells after k days
    // cells - store current status
    // of cells n - Number of cells
    // temp - to perform intermediate operations
    // k - number of days
    // active - count of active cells after k days
    // inactive - count of active cells after k days
    function activeAndInactive(cells , n , k)
    {

        // copy cells array into temp  array
        var temp =  Array(n).fill(false);
        for (i = 0; i < n; i++)
            temp[i] = cells[i];

        // Iterate for k days
        while (k-- > 0)
        {

            // Finding next values for corner cells
            temp[0] = false ^ cells[1];
            temp[n - 1] = false ^ cells[n - 2];

            // Compute values of intermediate cells
            // If both cells active or inactive, then
            // temp[i]=0 else temp[i] = 1.
            for (i = 1; i <= n - 2; i++)
                temp[i] = cells[i - 1] ^ cells[i + 1];

            // Copy temp to cells for next iteration
            for (i = 0; i < n; i++)
                cells[i] = temp[i];
        }

        // count active and inactive cells
        var active = 0, inactive = 0;
        for (i = 0; i < n; i++)
            if (cells[i] == true)
                active++;
            else
                inactive++;

        document.write("Active Cells = " + active + ", " + "Inactive Cells = " + inactive);
    }

    // Driver code
        var cells = [ false, true, false, true, false, true, false, true ];
        var k = 3;
        var n = cells.length;
        activeAndInactive(cells, n, k);

// This code is contributed by Rajput-Ji
</script>
```

输出:

```
Active Cells = 2 , Inactive Cells = 6
```

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。本文由 geeksforgeeks 团队审阅。如果你有更好的方法解决这个问题，请分享。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。