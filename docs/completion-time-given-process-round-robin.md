# 循环中给定流程的完成时间

> 原文:[https://www . geesforgeks . org/completion-time-给定-process-round-robin/](https://www.geeksforgeeks.org/completion-time-given-process-round-robin/)

给定 n 个进程，它们的完成时间以数组的形式表示。如果调度过程为[循环](https://www.geeksforgeeks.org/program-round-robin-scheduling-set-1/)，时间片为 1 秒，我们需要找到给定过程 p 结束的时刻。
注:数组索引从 0 开始。
**示例:**

```
Input : arr[] = {3, 2, 4, 2}, p = 1
Output : Completion time = 6
Explanation : Snap of process for every second is as:
Time    |   Process Array
0       |   {3, 2, 4, 2}
1       |   {2, 2, 4, 2}
2       |   {2, 1, 4, 2}
3       |   {2, 1, 3, 2}
4       |   {2, 1, 3, 1}
5       |   {1, 1, 3, 1}
6       |   {1, 0, 3, 1}

Input : arr[] = {2, 4, 1, 3}, p = 2
Output :Completion time = 3
Explanation : Snap of process for every second is as:
Time    |   Process Array
0       |   {2, 4, 1, 3}
1       |   {1, 4, 1, 3}
2       |   {1, 3, 1, 3}
3       |   {1, 3, 0, 3}
```

**蛮力:**解决这个问题的基本方法是应用时间片为 1 的循环算法。但是该方法的时间复杂度将是 O(σAi)，即所有进程时间的总和，这是相当高的。
**有效方法:**这个想法基于以下观察。
1)CPU 时间小于 arr[p]的所有进程将在 arr[p]之前完成。我们只需要增加这些过程的时间。
2)我们还需要加上 arr 的时间[p]。
3)对于 CPU 时间超过 arr[p]的每个进程 x，会出现两种情况:
…..(I)如果 x 在 arr[p]的左边(在 arr[p]之前调度)，那么这个过程在 p 结束之前占用 CPU 的 arr[p]时间。
…..(ii)如果 x 在 arr[p]的右边(arr[p]之后调度)，那么这个过程在 p 结束之前占用 arr[p]-1 个 CPU 时间。
算法:

```
time_req = 0;

// Add time for process on left of p 
// (Scheduled before p in a round of 
// 1 unit time slice)
for (int i=0; i<p; i++)
{
    if (arr[i] < arr[p])
        time_req += arr[i];
    else
        time_req += arr[p];
}

// step 2 : Add time of process p
time_req += arr[p];

// Add time for process on right
// of p (Scheduled after p in
// a round of 1 unit time slice)
for (int i=p+1; i<n; i++)
{
    if (arr[i] < arr[p])
        time_req += arr[i];
    else
        time_req += arr[p]-1;
}
```

## C++

```
// Program to find end time of a process
// p in round robin scheduling with unit
// time slice.
#include <bits/stdc++.h>
using namespace std;

// Returns completion time of p.
int completionTime(int arr[], int n, int p) {

  // Initialize result
  int time_req = 0;

  // Step 1 : Add time of processes on left
  //  of p (Scheduled before p)
  for (int i = 0; i < p; i++) {
    if (arr[i] < arr[p])
      time_req += arr[i];
    else
      time_req += arr[p];
  }

  // Step 2 : Add time of p
  time_req += arr[p];

  // Step 3 : Add time of processes on right
  //  of p (Scheduled after p)
  for (int i = p + 1; i < n; i++) {
    if (arr[i] < arr[p])
      time_req += arr[i];
    else
      time_req += arr[p] - 1;
  }

  return time_req;
}

// driver program
int main() {
  int arr[] = {3, 5, 2, 7, 6, 1};
  int n = sizeof(arr) / sizeof(arr[0]);
  int p = 2;
  cout << "Completion time = "
       << completionTime(arr, n, p);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find end time of a process
// p in round robin scheduling with unit
// time slice.
class GFG
{
    // Returns completion time of p.
    static int completionTime(int arr[], int n, int p) {

        // Initialize result
        int time_req = 0;

        // Step 1 : Add time of processes on left
        // of p (Scheduled before p)
        for (int i = 0; i < p; i++) {
            if (arr[i] < arr[p])
                time_req += arr[i];
            else
                time_req += arr[p];
        }

        // Step 2 : Add time of p
        time_req += arr[p];

        // Step 3 : Add time of processes on right
        // of p (Scheduled after p)
        for (int i = p + 1; i < n; i++) {
            if (arr[i] < arr[p])
                time_req += arr[i];
            else
                time_req += arr[p] - 1;
        }

        return time_req;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {3, 5, 2, 7, 6, 1};
        int n =arr.length;;
        int p = 2;

        System.out.print("Completion time = "+
            completionTime(arr, n, p));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Program to find end time of a process
# p in round robin scheduling with unit
# time slice.

# Returns completion time of p.
def completionTime(arr, n, p) :

    # Initialize result
    time_req = 0

    # Step 1 : Add time of processes on
    # left of p (Scheduled before p)
    for i in range(0, p):
        if (arr[i] < arr[p]):
            time_req += arr[i]
        else:
            time_req += arr[p]

    # Step 2 : Add time of p
    time_req += arr[p]

    # Step 3 : Add time of processes on
    # right of p (Scheduled after p)
    for i in range(p + 1, n):
        if (arr[i] < arr[p]):
            time_req += arr[i]
        else:
            time_req += arr[p] - 1

    return time_req

# driver program
arr = [3, 5, 2, 7, 6, 1]
n = len(arr)
p = 2
print("Completion time =",
        completionTime(arr, n, p))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find end time of a process
// p in round robin scheduling with unit
// time slice.
using System;

class GFG {

    // Returns completion time of p.
    static int completionTime(int []arr,
                            int n, int p)
    {

        // Initialize result
        int time_req = 0;

        // Step 1 : Add time of processes
        // on left of p (Scheduled before p)
        for (int i = 0; i < p; i++) {
            if (arr[i] < arr[p])
                time_req += arr[i];
            else
                time_req += arr[p];
        }

        // Step 2 : Add time of p
        time_req += arr[p];

        // Step 3 : Add time of processes on
        // right of p (Scheduled after p)
        for (int i = p + 1; i < n; i++) {
            if (arr[i] < arr[p])
                time_req += arr[i];
            else
                time_req += arr[p] - 1;
        }

        return time_req;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {3, 5, 2, 7, 6, 1};
        int n =arr.Length;;
        int p = 2;

        Console.WriteLine("Completion time = "+
                    completionTime(arr, n, p));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find end time
// of a process p in round
// robin scheduling with
// unit time slice.

// Returns completion time of p.
function completionTime($arr, $n, $p)
{

// Initialize result
$time_req = 0;

// Step 1 : Add time of processes on
// left of p (Scheduled before p)
for ($i = 0; $i < $p; $i++)
{
    if ($arr[$i] < $arr[$p])
    $time_req += $arr[$i];
    else
    $time_req += $arr[$p];
}

// Step 2 : Add time of p
$time_req += $arr[$p];

// Step 3 : Add time of processes on
// right of p (Scheduled after p)
for ($i = $p + 1; $i < $n; $i++)
{
    if ($arr[$i] < $arr[$p])
    $time_req += $arr[$i];
    else
    $time_req += $arr[$p] - 1;
}

return $time_req;
}

// Driver Code
$arr = array(3, 5, 2, 7, 6, 1);
$n = count($arr);
$p = 2;
echo"Completion time = " ,
     completionTime($arr, $n, $p);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Program to find end time of a process
// p in round robin scheduling with unit
// time slice.

// Returns completion time of p.
function completionTime(arr, n, p) {

  // Initialize result
  var time_req = 0;

  // Step 1 : Add time of processes on left
  //  of p (Scheduled before p)
  for (var i = 0; i < p; i++) {
    if (arr[i] < arr[p])
      time_req += arr[i];
    else
      time_req += arr[p];
  }

  // Step 2 : Add time of p
  time_req += arr[p];

  // Step 3 : Add time of processes on right
  //  of p (Scheduled after p)
  for (var i = p + 1; i < n; i++) {
    if (arr[i] < arr[p])
      time_req += arr[i];
    else
      time_req += arr[p] - 1;
  }

  return time_req;
}

// driver program
var arr = [3, 5, 2, 7, 6, 1];
var n = arr.length;
var p = 2;
document.write( "Completion time = "
     + completionTime(arr, n, p));

// This code is contributed by noob2000.
</script>
```

**输出:**

```
Completion time = 9
```

**时间复杂度:** O(n)