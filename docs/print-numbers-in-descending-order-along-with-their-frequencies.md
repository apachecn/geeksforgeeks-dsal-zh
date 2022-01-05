# 按照频率降序打印数字

> 原文:[https://www . geesforgeks . org/print-numbers-in-降序-连同它们的频率/](https://www.geeksforgeeks.org/print-numbers-in-descending-order-along-with-their-frequencies/)

给定一个数组 **arr** ，任务是按照降序打印数组的元素及其频率。
**例:**

> **输入:** arr[] = {1，3，3，3，4，4，5}
> **输出:** 5 发生 1 次
> 4 发生 2 次
> 3 发生 3 次
> 1 发生 1 次
> **输入:** arr[] = {1，1，1，2，3，4，9，10}
> **输出:** 10 发生 1 次
> 9 发生 2 次【T15

**简单方法:**使用一些[数据结构](https://www.geeksforgeeks.org/data-structures/)(例如[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/))，以降序存储元素，然后用它的计数逐个打印元素，然后从数据结构中删除它。对于所使用的数据结构，时间复杂度为 0(N 对数 N)，辅助空间为 0(N)。
以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print the elements in
// descending along with their frequencies
#include <bits/stdc++.h>
using namespace std;

// Function to print the elements in descending
// along with their frequencies
void printElements(int a[], int n)
{

    // A multiset to store elements in decreasing order
    multiset<int, greater<int> > ms;

    // Insert elements in the multiset
    for (int i = 0; i < n; i++) {
        ms.insert(a[i]);
    }

    // Print the elements along with their frequencies
    while (!ms.empty()) {

        // Find the maximum element
        int maxel = *ms.begin();

        // Number of times it occurs
        int times = ms.count(maxel);

        cout << maxel << " occurs " << times << " times\n";

        // Erase the maxel
        ms.erase(maxel);
    }
}

// Driver Code
int main()
{
    int a[] = { 1, 1, 1, 2, 3, 4, 9, 9, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    printElements(a, n);
    return 0;
}
```

**Output:** 

```
10 occurs 1 times
9 occurs 2 times
4 occurs 1 times
3 occurs 1 times
2 occurs 1 times
1 occurs 3 times
```

**高效方法:** [按降序排列数组](https://www.geeksforgeeks.org/sort-c-stl/)，然后开始打印元素及其频率。
以下是上述方法的实施:

## C++

```
// C++ program to print the elements in
// descending along with their frequencies
#include <bits/stdc++.h>
using namespace std;

// Function to print the elements in descending
// along with their frequencies
void printElements(int a[], int n)
{

    // Sorts the element in decreasing order
    sort(a, a + n, greater<int>());
    int cnt = 1;

    // traverse the array elements
    for (int i = 0; i < n - 1; i++) {

        // Prints the number and count
        if (a[i] != a[i + 1]) {
            cout << a[i] << " occurs " << cnt << " times\n";
            cnt = 1;
        }
        else
            cnt += 1;
    }

    // Prints the last step
    cout << a[n - 1] << " occurs " << cnt << " times\n";
}

// Driver Code
int main()
{
    int a[] = { 1, 1, 1, 2, 3, 4, 9, 9, 10 };
    int n = sizeof(a) / sizeof(a[0]);

    printElements(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the elements in
// descending along with their frequencies
import java.util.*;

class GFG
{

// Function to print the elements in descending
// along with their frequencies
static void printElements(int a[], int n)
{

    // Sorts the element in decreasing order
    Arrays.sort(a);
    a = reverse(a);
    int cnt = 1;

    // traverse the array elements
    for (int i = 0; i < n - 1; i++)
    {

        // Prints the number and count
        if (a[i] != a[i + 1])
        {
            System.out.print(a[i]+ " occurs " +
                            cnt + " times\n");
            cnt = 1;
        }
        else
            cnt += 1;
    }

    // Prints the last step
    System.out.print(a[n - 1]+ " occurs " +
                    cnt + " times\n");
}

static int[] reverse(int a[])
{
    int i, n = a.length, t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 1, 1, 2, 3, 4, 9, 9, 10 };
    int n = a.length;

    printElements(a, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to print the elements in
# descending along with their frequencies

# Function to print the elements in
# descending along with their frequencies
def printElements(a, n) :

    # Sorts the element in decreasing order
    a.sort(reverse = True)
    cnt = 1

    # traverse the array elements
    for i in range(n - 1) :

        # Prints the number and count
        if (a[i] != a[i + 1]) :
            print(a[i], " occurs ", cnt, "times")
            cnt = 1

        else :
            cnt += 1

    # Prints the last step
    print(a[n - 1], "occurs", cnt, "times")

# Driver Code
if __name__ == "__main__" :

    a = [ 1, 1, 1, 2,
          3, 4, 9, 9, 10 ]
    n = len(a)

    printElements(a, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to print the elements in
// descending along with their frequencies
using System;

class GFG
{

// Function to print the elements in descending
// along with their frequencies
static void printElements(int []a, int n)
{

    // Sorts the element in decreasing order
    Array.Sort(a);
    a = reverse(a);
    int cnt = 1;

    // traverse the array elements
    for (int i = 0; i < n - 1; i++)
    {

        // Prints the number and count
        if (a[i] != a[i + 1])
        {
            Console.Write(a[i]+ " occurs " +
                            cnt + " times\n");
            cnt = 1;
        }
        else
            cnt += 1;
    }

    // Prints the last step
    Console.Write(a[n - 1]+ " occurs " +
                    cnt + " times\n");
}

static int[] reverse(int []a)
{
    int i, n = a.Length, t;
    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 1, 1, 1, 2, 3, 4, 9, 9, 10 };
    int n = a.Length;

    printElements(a, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the elements in
// descending along with their frequencies

// Function to print the elements in
// descending along with their frequencies
function printElements(&$a, $n)
{

    // Sorts the element in
    // decreasing order
    rsort($a);
    $cnt = 1;

    // traverse the array elements
    for ($i = 0; $i < $n - 1; $i++)
    {

        // Prints the number and count
        if ($a[$i] != $a[$i + 1])
        {
            echo ($a[$i]);
            echo (" occurs " );
            echo $cnt ;
            echo (" times\n");
            $cnt = 1;
        }
        else
            $cnt += 1;
    }

    // Prints the last step
    echo ($a[$n - 1]);
    echo (" occurs ");
    echo $cnt;
    echo (" times\n");
}

// Driver Code
$a = array(1, 1, 1, 2, 3,
           4, 9, 9, 10 );
$n = sizeof($a);

printElements($a, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// javascript program to print the elements in
// descending along with their frequencies

// Function to print the elements in descending
// along with their frequencies
  function printElements(a,  n)

{

    // Sorts the element in decreasing order
    a=a.sort(compare);
    a = reverse(a);
    var cnt = 1;

    // traverse the array elements
    for (var i = 0; i < n - 1; i++)
    {

        // Prints the number and count
        if (a[i] != a[i + 1])
        {
            document.write(a[i]+ " occurs " +   cnt + " times" + "<br>");
            cnt = 1;
        }
        else
            cnt += 1;
    }

    // Prints the last step
    document.write(a[n - 1]+ " occurs " + cnt + " times" + "<br>");
}

  function reverse(a){
    var i, n = a.length, t;

    for (i = 0; i < n / 2; i++)
    {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

function compare(a, b) {
    if (a < b) {
        return -1;
    } else if (a > b) {
        return 1;
    } else {
        return 0;
    }
}

// Driver Code

    var a = [ 1, 1, 1, 2, 3, 4, 9, 9, 10 ];
    var n = a.length;

    printElements(a, n);

 // This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
10 occurs 1 times
9 occurs 2 times
4 occurs 1 times
3 occurs 1 times
2 occurs 1 times
1 occurs 3 times
```