# 根据给定规则

生成大小为 N 的数组

> 原文:[https://www . geeksforgeeks . org/根据给定的规则生成 n 大小的数组/](https://www.geeksforgeeks.org/generate-an-array-of-size-n-according-to-the-given-rules/)

给定一个数字 **N** ，任务是创建一个大小为 **N** 的数组**arr【】**，其中每个索引 **i** 处的元素值根据以下规则填充:

1.  *arr[I]=((I–1)–k)*，其中 k 是最近第二次出现的 arr[I–1]的索引。当**arr[I–1]**在数组中出现不止一次时，应用此规则
2.  *arr[i] = 0* 。当**arr[I–1]**仅出现一次或当 **i = 1** 时，适用此规则。

**例:**

> **输入:** N = 8
> **输出:** 0 0 1 0 2 0 2 2
> **解释:**
> 对于 i = 0:数组 arr[]中没有元素。因此，0 被放在第一个索引中。arr[] = {0}。
> 对于 i = 1:数组 arr[]中只有一个元素。arr[I–1](= 0)的出现只有一次。因此，根据规则 2 填充数组。arr = {0，0}。
> 对于 i = 2:数组中有两个元素。第二多的 arr[I–1]= arr[0]= 0。所以，arr[2] = 1。arr[] = {0，0，1}。
> 对于 i = 3:没有第二次出现 arr[I–1]= 1。因此，arr[3] = 0。arr[] = {0，0，1，0}
> 对于 I = 4:arr[I–1]= 0 的最近第二次出现是 1。因此，(I–1–k)=(4–1–1)= 2。arr[] = {0，0，1，0，2}。
> 对于 I = 5:arr[I–1]= 2 只出现一次。因此，arr[5] = 0。arr[] = {0，0，1，0，2，0}。
> 对于 I = 6:arr[I–1]= 0 的最近第二次出现是 3。因此，(I–1–k)=(6–1–3)= 2。arr[] = {0，0，1，0，2，0，2}。
> 对于 I = 7:arr[I–1]= 2 的最近第二次出现是 4。因此，(I–1–k)=(7–1–4)= 2。arr[] = {0，0，1，0，2，0，2，2}
> **输入:** N = 5
> **输出:** 0 0 1 0 2

**方法:**想法是首先创建一个填充有大小为 n 的零的数组。然后对于每次迭代，我们搜索该元素是否发生在最近的过去。如果是，那么我们遵循**规则 1** 。否则，遵循**规则 2** 来填充阵列。
以下是上述方法的实现:

## C++

```
// C++ implementation to generate
// an array of size N by following
// the given rules
#include <bits/stdc++.h>
using namespace std;

// Function to search the most recent
// location of element N
// If not present in the array
// it will return -1
int search(int a[], int k, int x)
{
    int j;

    for ( j = k - 1; j > -1 ; j--)
    {
        if(a[j] == x)
            return j ;
    }

        return -1 ;
}

// Function to generate an array
// of size N by following the given rules
void genArray(int arr[], int N)
{

    // Loop to fill the array
    // as per the given rules
    for(int i = 0; i < N - 1; i++)
    {

        // Check for the occurrence
        // of arr[i - 1]
        if(search(arr, i, arr[i]) == -1)
                arr[i + 1] = 0 ;

        else
            arr[i + 1] = (i-search(arr, i, arr[i])) ;
    }
}

// Driver code
int main()
{
    int N = 5 ;
    int size = N + 1 ;
    int a[] = {0, 0, 0, 0, 0};
    genArray(a, N) ;

    for (int i = 0; i < N ; i ++)
        cout << a[i] << " " ;
        return 0;
}

// This code is contributed by shivanisinghss2110
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to generate
// an array of size N by following
// the given rules
class GFG
{

static int a[];

// Function to search the most recent
// location of element N
// If not present in the array
// it will return -1
static int search(int a[],int k, int x)
{
    int j;

    for ( j = k - 1; j > -1 ; j--)
    {
            if(a[j] == x)
                return j ;
        }

        return -1 ;
}

// Function to generate an array
// of size N by following the given rules
static void genArray(int []arr, int N)
{

    // Loop to fill the array
    // as per the given rules
    for(int i = 0; i < N - 1; i++)
    {

        // Check for the occurrence
        // of arr[i - 1]
        if(search(arr, i, arr[i]) == -1)
                arr[i + 1] = 0 ;

        else
            arr[i + 1] = (i-search(arr, i, arr[i])) ;
    }
}

// Driver code
public static void main (String[] args)
{
    int N = 5 ;
    int size = N + 1 ;
    int a[] = new int [N];
    genArray(a, N) ;

    for (int i = 0; i < N ; i ++)
        System.out.print(a[i]+" " );

}
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python implementation to generate
# an array of size N by following
# the given rules

# Function to search the most recent
# location of element N
# If not present in the array
# it will return -1
def search(a, k, x):
        for j in range(k-1, -1, -1) :
            if(a[j]== x):
                return j

        return -1

# Function to generate an array
# of size N by following the given rules
def genArray(arr, N):

    # Loop to fill the array
    # as per the given rules
    for i in range(0, N-1, 1):

        # Check for the occurrence
        # of arr[i - 1]
        if(search(arr, i, arr[i])==-1):
                arr[i + 1]= 0

        else:
            arr[i + 1]=(i-search(arr, i, arr[i]))

# Driver code     
if __name__ == "__main__":
    N = 5
    size = N + 1
    a =[0]*N
    genArray(a, N)

    print(a)
```

## C#

```
// C# implementation to generate
// an array of size N by following
// the given rules

using System;

public class GFG
{

static int []a;

// Function to search the most recent
// location of element N
// If not present in the array
// it will return -1
static int search(int []a,int k, int x)
{
    int j;

    for ( j = k - 1; j > -1 ; j--)
    {
            if(a[j] == x)
                return j ;
        }

        return -1 ;
}

// Function to generate an array
// of size N by following the given rules
static void genArray(int []arr, int N)
{

    // Loop to fill the array
    // as per the given rules
    for(int i = 0; i < N - 1; i++)
    {

        // Check for the occurrence
        // of arr[i - 1]
        if(search(arr, i, arr[i]) == -1)
                arr[i + 1] = 0 ;

        else
            arr[i + 1] = (i-search(arr, i, arr[i])) ;
    }
}

// Driver code
public static void Main (string[] args)
{
    int N = 5 ;
    int size = N + 1 ;
    int []a = new int [N];
    genArray(a, N) ;

    for (int i = 0; i < N ; i ++)
        Console.Write(a[i]+" " );

}
}
// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation to generate
// an array of size N by following
// the given rules

// Function to search the most recent
// location of element N
// If not present in the array
// it will return -1
function search( a, k, x)
{
    var j;

    for ( j = k - 1; j > -1 ; j--)
    {
        if(a[j] == x)
            return j ;
    }

        return -1 ;
}

// Function to generate an array
// of size N by following the given rules
function genArray(arr, N)
{

    // Loop to fill the array
    // as per the given rules
    for(var i = 0; i < N - 1; i++)
    {

        // Check for the occurrence
        // of arr[i - 1]
        if(search(arr, i, arr[i]) == -1)
                arr[i + 1] = 0 ;

        else
            arr[i + 1] = (i-search(arr, i, arr[i])) ;
    }
}

// Driver code
var N = 5 ;
var size = N + 1 ;
var a = [0, 0, 0, 0, 0];
genArray(a, N) ;
document.write("["+a+"]");

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
[0, 0, 1, 0, 2]
```

时间复杂度:O(N <sup>2</sup> )

辅助空间:0(1)