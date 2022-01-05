# 子阵列(元素范围)的异或|集合 2

> 原文:[https://www . geesforgeks . org/xor-of-a-subarray-range-of-elements-set-2/](https://www.geeksforgeeks.org/xor-of-a-subarray-range-of-elements-set-2/)

给定大小为 **N** 和 **Q** 查询的数组整数 **arr[]** 。每个查询的形式为 **(L，R)** ，其中 **L** 和 **R** 是数组的索引。任务是找到子阵列**arr【L…R】**的异或值。

**示例:**

> **输入:** arr[] = {2，5，1，6，1，2，5}查询[] = {{1，4}}
> **输出:**3
> arr[1…4]的异或值为 3。
> 
> **输入:** arr[] = {2，5，1，6，1，2，5}查询[] = {{0，6}}
> **输出:**6
> arr[0…6]的异或值为 6。

**O(N)辅助空间进场:**O(N)辅助空间进场请参考[本文](https://www.geeksforgeeks.org/xor-of-a-subarray-range-of-elements/)。

**方法:**这里我们将讨论一个常数空间解，但是我们将修改输入数组。

1.将输入数组从索引 **1** 更新为**N–1**，这样 **arr[i]** 存储从 **arr[0]** 到 **arr[i]** 的异或。

> arr[1]=异或(arr[0]，arr[1]，..，arr[i])

2.要处理从 **L** 到 **R** 的查询，只需返回**arr【l-1】^ arr【r】**。

**例如:**

> 考虑以下示例:arr[] = { 3，2，4，5，1，1，5，3 }，query[] = {{1，4 }，{ 3，7}}
> 对连续元素进行异或运算后，第一个查询的 arr[] = {3，1，5，0，1，0，5，6 }
> { 1，4} ans = arr[0] ^ arr[4] = 3 ^ 1 = 2
> 第二个查询的 arr[]= arr[2]^ arr[7]= 5 ^

下面是上述方法的实现:

## C++

```
// C++ program to find XOR
// in a range from L to R

#include <bits/stdc++.h>
using namespace std;

// Function to find XOR
// in a range from L to R
void find_Xor(int arr[],
              pair<int, int> query[],
              int N, int Q)
{
    // Compute xor from arr[0] to arr[i]
    for (int i = 1; i < N; i++) {
        arr[i] = arr[i] ^ arr[i - 1];
    }

    int ans = 0;

    // process every query
    // in constant time
    for (int i = 0; i < Q; i++) {

        // if L==0
        if (query[i].first == 0)
            ans = arr[query[i].second];
        else
            ans = arr[query[i].first - 1]
                  ^ arr[query[i].second];

        cout << ans << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 4, 5,
                  1, 1, 5, 3 };
    int N = 8;
    int Q = 2;
    pair<int, int> query[Q]
        = { { 1, 4 },
            { 3, 7 } };

    // query[]
    find_Xor(arr, query, N, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR
// in a range from L to R
class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find XOR
// in a range from L to R
static void find_Xor(int arr[],
                     pair query[],
                     int N, int Q)
{

    // Compute xor from arr[0] to arr[i]
    for(int i = 1; i < N; i++)
    {
       arr[i] = arr[i] ^ arr[i - 1];
    }

    int ans = 0;

    // Process every query
    // in constant time
    for(int i = 0; i < Q; i++)
    {

       // If L==0
       if (query[i].first == 0)
           ans = arr[query[i].second];
       else
           ans = arr[query[i].first - 1] ^
                 arr[query[i].second];

       System.out.print(ans + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 4, 5,
                  1, 1, 5, 3 };
    int N = 8;
    int Q = 2;

    pair query[] = { new pair(1, 4),
                     new pair(3, 7) };

    // query[]
    find_Xor(arr, query, N, Q);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to find XOR
# in a range from L to R

# Function to find XOR
# in a range from L to R
def find_Xor(arr, query, N, Q):

    # Compute xor from arr[0] to arr[i]
    for i in range(1, N):
        arr[i] = arr[i] ^ arr[i - 1]

    ans = 0

    # Process every query
    # in constant time
    for i in range(Q):

        # If L == 0
        if query[i][0] == 0:
            ans = arr[query[i][1]]
        else:
            ans = (arr[query[i][0] - 1] ^
                   arr[query[i][1]])
        print(ans)

# Driver code
def main():

    arr = [ 3, 2, 4, 5, 1, 1, 5, 3 ]
    N = 8
    Q = 2

    # query[]
    query = [ [ 1, 4 ],
              [ 3, 7 ] ]

    find_Xor(arr, query, N, Q)

main()

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program to find XOR
// in a range from L to R
using System;

class GFG{   
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find XOR
// in a range from L to R
static void find_Xor(int []arr,
                     pair []query,
                     int N, int Q)
{

    // Compute xor from arr[0] to arr[i]
    for(int i = 1; i < N; i++)
    {
       arr[i] = arr[i] ^ arr[i - 1];
    }

    int ans = 0;

    // Process every query
    // in constant time
    for(int i = 0; i < Q; i++)
    {

       // If L==0
       if (query[i].first == 0)
           ans = arr[query[i].second];
       else
           ans = arr[query[i].first - 1] ^
                 arr[query[i].second];

       Console.Write(ans + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 4, 5,
                  1, 1, 5, 3 };
    int N = 8;
    int Q = 2;

    pair []query = { new pair(1, 4),
                     new pair(3, 7) };

    // query[]
    find_Xor(arr, query, N, Q);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find XOR
// in a range from L to R

// Function to find XOR
// in a range from L to R
function find_Xor(arr, query, N, Q)
{
    // Compute xor from arr[0] to arr[i]
    for (var i = 1; i < N; i++) {
        arr[i] = arr[i] ^ arr[i - 1];
    }

    var ans = 0;

    // process every query
    // in constant time
    for (var i = 0; i < Q; i++) {

        // if L==0
        if (query[i][0] == 0)
            ans = arr[query[i][1]];
        else
            ans = arr[query[i][0] - 1]
                  ^ arr[query[i][1]];

        document.write( ans + "<br>");
    }
}

// Driver Code
var arr = [3, 2, 4, 5,
              1, 1, 5, 3];
var N = 8;
var Q = 2;
var query
    = [[1, 4],
        [3, 7]];
// query[]
find_Xor(arr, query, N, Q);

</script>
```

**Output:** 

```
2
3
```

***时间复杂度:** O (N + Q)*
***辅助空间:** O (1)*