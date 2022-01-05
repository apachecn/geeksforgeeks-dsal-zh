# 检查是否可以在 k 个子阵列中以相等的和进行划分

> 原文:[https://www . geeksforgeeks . org/check-in-k-subarrays-with-equal-sum/](https://www.geeksforgeeks.org/check-if-it-possible-to-partition-in-k-subarrays-with-equal-sum/)

给定一个大小为 N 的数组 A 和一个数字 K。任务是找出是否有可能将数组 A 划分成 K 个连续的子数组，使得每个子数组中的元素之和相同。
**先决条件:** [计算将一个数组分成三个相等和的连续部分的方法数量](https://www.geeksforgeeks.org/count-the-number-of-ways-to-divide-an-array-into-three-contiguous-parts-having-equal-sum/)

**示例:**

```
Input : arr[] = { 1, 4, 2, 3, 5 } K = 3
Output : Yes
Explanation :
Three possible partitions which have equal sum : 
(1 + 4), (2 + 3) and (5)

Input : arr[] = { 1, 1, 2, 2 } K = 2
Output : No
```

**方法:**
可以通过使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来求解。首先，请注意，数组中所有元素的总和应该可以被 K 整除，以创建 K 个分区，每个分区具有相等的总和。如果它是可分的，那么通过执行以下操作来检查每个分区是否有相等的和:
1。对于特定的 K，每个子阵列应该有一个要求的和= total_sum / K.
2。从第 0 <sup>个</sup>索引开始，开始比较前缀和，一旦
等于和，就意味着一个子数组的结束(假设在索引 j 处)。
3。从(j + 1) <sup>第</sup>个索引中，找到另一个合适的 I，其和(prefix _ sum[I]–
prefix _ sum[j])等于所需和。该过程一直进行到
找到所需数量的相邻子阵列，即 K。
4。如果在任何索引处，任何子阵列总和大于所需总和，则从循环中断开
，因为每个子阵列应包含相同的总和。

**以下是上述方法**的实施

## C++

```
// CPP Program to check if array
// can be split into K contiguous
// subarrays each having equal sum
#include <bits/stdc++.h>
using namespace std;

// function returns true to it is possible to
// create K contiguous partitions each having
// equal sum, otherwise false
bool KpartitionsPossible(int arr[], int n, int K)
{
    // Creating and filling prefix sum array
    int prefix_sum[n];
    prefix_sum[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefix_sum[i] =  prefix_sum[i - 1] + arr[i];

    // return false if total_sum is not
    // divisible by K  
    int total_sum = prefix_sum[n-1];
    if (total_sum % K != 0)
        return false;

    // a temporary variable to check
    // there are exactly K partitions
    int temp = 0;

    int pos = -1;
    for (int i = 0; i < n; i++)
    {       
        // find suitable i for which first
        // partition have the required sum
        // and then find next partition and so on
        if (prefix_sum[i] - (pos == -1 ? 0 :
            prefix_sum[pos]) == total_sum / K)
        {
            pos = i;
            temp++;
        }

        // if it becomes greater than
        // required sum break out
        else if (prefix_sum[i] - prefix_sum[pos] >
                total_sum / K)
            break;
    }

    // check if temp has reached to K
    return (temp == K);
}

// Driver Code
int main()
{
    int arr[] = { 4, 4, 3, 5, 6, 2 };   
    int n = sizeof(arr) / sizeof(arr[0]);

    int K = 3;
    if (KpartitionsPossible(arr, n, K))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if an array
// can be split into K contiguous
// subarrays each having equal sum
public class GfG{

    // Function returns true to it is possible to
    // create K contiguous partitions each having
    // equal sum, otherwise false
    static boolean KpartitionsPossible(int arr[], int n, int K)
    {
        // Creating and filling prefix sum array
        int prefix_sum[] = new int[n];
        prefix_sum[0] = arr[0];
        for (int i = 1; i < n; i++)
            prefix_sum[i] = prefix_sum[i - 1] + arr[i];

        // return false if total_sum is not divisible by K
        int total_sum = prefix_sum[n-1];
        if (total_sum % K != 0)
            return false;

        // a temporary variable to check
        // there are exactly K partitions
        int temp = 0, pos = -1;

        for (int i = 0; i < n; i++)
        {        
            // find suitable i for which first
            // partition have the required sum
            // and then find next partition and so on
            if (prefix_sum[i] - (pos == -1 ? 0 :
                prefix_sum[pos]) == total_sum / K)
            {
                pos = i;
                temp++;
            }

            // if it becomes greater than
            // required sum break out
            else if (prefix_sum[i] - (pos == -1 ? 0 :
                prefix_sum[pos]) > total_sum / K)
                break;
        }

        // check if temp has reached to K
        return (temp == K);
    }

     public static void main(String []args){

        int arr[] = { 4, 4, 3, 5, 6, 2 };    
        int n = arr.length;

        int K = 3;
        if (KpartitionsPossible(arr, n, K))
            System.out.println("Yes");
        else
            System.out.println("No");
     }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 Program to check if array
# can be split into K contiguous
# subarrays each having equal sum

# function returns true to it is possible to
# create K contiguous partitions each having
# equal sum, otherwise false
def KpartitionsPossible(arr, n, K):

    # Creating and filling prefix sum array
    prefix_sum = [0 for i in range(n)]
    prefix_sum[0] = arr[0]
    for i in range(1, n, 1):
        prefix_sum[i] = prefix_sum[i - 1] + arr[i]

    # return false if total_sum is not
    # divisible by K
    total_sum = prefix_sum[n - 1]
    if (total_sum % K != 0):
        return False

    # a temporary variable to check
    # there are exactly K partitions
    temp = 0

    pos = -1
    for i in range(0, n, 1):

        # find suitable i for which first
        # partition have the required sum
        # and then find next partition and so on
        if (pos == -1):
            sub = 0
        else:
            sub = prefix_sum[pos]
        if (prefix_sum[i] - sub == total_sum / K) :
            pos = i
            temp += 1

        # if it becomes greater than
        # required sum break out
        elif (prefix_sum[i] -
              prefix_sum[pos] > total_sum / K):
            break

    # check if temp has reached to K
    return (temp == K)

# Driver Code
if __name__ =='__main__':
    arr = [4, 4, 3, 5, 6, 2]
    n = len(arr)

    K = 3
    if (KpartitionsPossible(arr, n, K)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# Program to check if an array
// can be split into K contiguous
// subarrays each having equal sum
using System;

class GfG
{

    // Function returns true to it is possible to
    // create K contiguous partitions each having
    // equal sum, otherwise false
    static bool KpartitionsPossible(int[] arr, int n, int K)
    {
        // Creating and filling prefix sum array
        int[] prefix_sum = new int[n];
        prefix_sum[0] = arr[0];
        for (int i = 1; i < n; i++)
            prefix_sum[i] = prefix_sum[i - 1] + arr[i];

        // return false if total_sum is not divisible by K
        int total_sum = prefix_sum[n-1];
        if (total_sum % K != 0)
            return false;

        // a temporary variable to check
        // there are exactly K partitions
        int temp = 0, pos = -1;

        for (int i = 0; i < n; i++)
        {        
            // find suitable i for which first
            // partition have the required sum
            // and then find next partition and so on
            if (prefix_sum[i] - (pos == -1 ? 0 :
                prefix_sum[pos]) == total_sum / K)
            {
                pos = i;
                temp++;
            }

            // if it becomes greater than
            // required sum break out
            else if (prefix_sum[i] - (pos == -1 ? 0 :
                prefix_sum[pos]) > total_sum / K)
                break;
        }

        // check if temp has reached to K
        return (temp == K);
    }

    // Driver code
    public static void Main()
    {

        int[] arr = { 4, 4, 3, 5, 6, 2 };    
        int n = arr.Length;

        int K = 3;
        if (KpartitionsPossible(arr, n, K))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if array
// can be split into K contiguous
// subarrays each having equal sum

// function returns true to
// it is possible to create
// K contiguous partitions
// each having equal sum,
// otherwise false
function KpartitionsPossible($arr,
                             $n, $K)
{
    // Creating and filling
    // prefix sum array
    $prefix_sum = Array();
    $prefix_sum[0] = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $prefix_sum[$i] = $prefix_sum[$i - 1] +
                          $arr[$i];

    // return false if total_sum
    // is not divisible by K
    $total_sum = $prefix_sum[$n - 1];
    if ($total_sum % $K != 0)
        return false;

    // a temporary variable to
    // check there are exactly
    // K partitions
    $temp = 0;

    $pos = -1;
    for ($i = 0; $i < $n; $i++)
    {
        // find suitable i for which
        // first partition have the
        // required sum and then find
        // next partition and so on
        if ($prefix_sum[$i] - ($pos == -1 ? 0 :
                         $prefix_sum[$pos]) ==
                         (int)$total_sum / $K)
        {
            $pos = $i;
            $temp++;
        }
    }

    // check if temp has
    // reached to K
    return ($temp == $K);
}

// Driver Code
$arr = array (4, 4, 3,
              5, 6, 2);
$n = sizeof($arr) ;

$K = 3;
if (KpartitionsPossible($arr, $n, $K))
    echo "Yes";
else
    echo "No";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

    // Javascript Program to check if an array
    // can be split into K contiguous
    // subarrays each having equal sum

    // Function returns true to it is possible to
    // create K contiguous partitions each having
    // equal sum, otherwise false
    function KpartitionsPossible(arr, n, K)
    {
        // Creating and filling prefix sum array
        let prefix_sum = new Array(n);
        prefix_sum[0] = arr[0];
        for (let i = 1; i < n; i++)
            prefix_sum[i] = prefix_sum[i - 1] +
            arr[i];

        // return false if total_sum is
        // not divisible by K
        let total_sum = prefix_sum[n-1];
        if (total_sum % K != 0)
            return false;

        // a temporary variable to check
        // there are exactly K partitions
        let temp = 0, pos = -1;

        for (let i = 0; i < n; i++)
        {        
            // find suitable i for which first
            // partition have the required sum
            // and then find next partition and so on
            if (prefix_sum[i] - (pos == -1 ? 0 :
                prefix_sum[pos]) ==
                parseInt(total_sum / K, 10))
            {
                pos = i;
                temp++;
            }

            // if it becomes greater than
            // required sum break out
            else if (prefix_sum[i] - (pos == -1 ? 0 :
            prefix_sum[pos]) >
            parseInt(total_sum / K, 10))
                break;
        }

        // check if temp has reached to K
        return (temp == K);
    }

    let arr = [ 4, 4, 3, 5, 6, 2 ];    
    let n = arr.length;

    let K = 3;
    if (KpartitionsPossible(arr, n, K))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)，其中 N 是数组的大小。
**辅助空间:** O(N)，其中 N 为阵的大小。

我们可以进一步将**空间复杂度**降低到 **O(1)** 。
因为阵列将被分成 k 个子阵列，并且所有子阵列都是连续的。所以思路是计算子数组的个数，其和等于整个数组的和除以 k
如果个数== k 打印是否则打印否

**以下是上述方法**的实施

## C++

```
// CPP Program to check if array
// can be split into K contiguous
// subarrays each having equal sum
#include <bits/stdc++.h>
using namespace std;

// function returns true to it is possible to
// create K contiguous partitions each having
// equal sum, otherwise false
int KpartitionsPossible(int arr[], int n, int k)
{
    int sum = 0;
    int count = 0;

    // calculate the sum of the array
    for(int i = 0; i < n; i++)
    sum = sum + arr[i];

    if(sum % k != 0)
    return 0;

    sum = sum / k;
    int ksum = 0;

    // ksum denotes the sum of each subarray
    for(int i = 0; i < n; i++)
    {
    ksum=ksum + arr[i];

    // one subarray is found
    if(ksum == sum)
    {
        // to locate another
        ksum = 0;
        count++;
    }

    }

    if(count == k)
    return 1;
    else
    return 0;

}

// Driver code
int main() {

int arr[] = { 1, 1, 2, 2};
int k = 2;
    int n = sizeof(arr) / sizeof(arr[0]);
    if (KpartitionsPossible(arr, n, k) == 0)
        cout << "Yes";
    else
        cout<<"No";
    return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java Program to check if array
// can be split into K contiguous
// subarrays each having equal sum

public class GFG {

// function returns true to it is possible to
// create K contiguous partitions each having
// equal sum, otherwise false
    static int KpartitionsPossible(int arr[], int n, int k) {
        int sum = 0;
        int count = 0;

        // calculate the sum of the array
        for (int i = 0; i < n; i++) {
            sum = sum + arr[i];
        }

        if (sum % k != 0) {
            return 0;
        }

        sum = sum / k;
        int ksum = 0;

        // ksum denotes the sum of each subarray
        for (int i = 0; i < n; i++) {
            ksum = ksum + arr[i];

            // one subarray is found
            if (ksum == sum) {
                // to locate another
                ksum = 0;
                count++;
            }

        }

        if (count == k) {
            return 1;
        } else {
            return 0;
        }

    }

    // Driver Code
    public static void main(String[] args) {

        int arr[] = {1, 1, 2, 2};
        int k = 2;
        int n = arr.length;

        if (KpartitionsPossible(arr, n, k) == 0) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }

}

/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 Program to check if array
# can be split into K contiguous
# subarrays each having equal sum

# Function returns true to it is possible
# to create K contiguous partitions each
# having equal sum, otherwise false
def KpartitionsPossible(arr, n, k) :

    sum = 0
    count = 0

    # calculate the sum of the array
    for i in range(n) :
        sum = sum + arr[i]

    if(sum % k != 0) :
        return 0

    sum = sum // k
    ksum = 0

    # ksum denotes the sum of each subarray
    for i in range(n) :
        ksum = ksum + arr[i]

    # one subarray is found
    if(ksum == sum) :

        # to locate another
        ksum = 0
        count += 1

    if(count == k) :
        return 1
    else :
        return 0

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1, 2, 2]
    k = 2
    n = len(arr)
    if (KpartitionsPossible(arr, n, k) == 0) :
        print("Yes")
    else :
        print("No")

# This code is contributed by Ryuga
```

## C#

```
// C# Program to check if array
// can be split into K contiguous
// subarrays each having equal sum

using System;
public class GFG{

// function returns true to it is possible to
// create K contiguous partitions each having
// equal sum, otherwise false
    static int KpartitionsPossible(int []arr, int n, int k) {
        int sum = 0;
        int count = 0;

        // calculate the sum of the array
        for (int i = 0; i < n; i++) {
            sum = sum + arr[i];
        }

        if (sum % k != 0) {
            return 0;
        }

        sum = sum / k;
        int ksum = 0;

        // ksum denotes the sum of each subarray
        for (int i = 0; i < n; i++) {
            ksum = ksum + arr[i];

            // one subarray is found
            if (ksum == sum) {
                // to locate another
                ksum = 0;
                count++;
            }

        }

        if (count == k) {
            return 1;
        } else {
            return 0;
        }

    }

    // Driver Code
    public static void Main() {

        int []arr = {1, 1, 2, 2};
        int k = 2;
        int n = arr.Length;

        if (KpartitionsPossible(arr, n, k) == 0) {
            Console.Write("Yes");
        } else {
            Console.Write("No");
        }
    }

}

/*This code is contributed by PrinciRaj1992*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if array
// can be split into K contiguous
// subarrays each having equal sum

// function returns true to it is possible to
// create K contiguous partitions each having
// equal sum, otherwise false
function KpartitionsPossible($arr, $n, $k)
{
    $sum = 0;
    $count = 0;

    // calculate the sum of the array
    for($i = 0; $i < $n; $i++)
        $sum = $sum + $arr[$i];

    if($sum % $k != 0)
        return 0;

    $sum = $sum / $k;
    $ksum = 0;

    // ksum denotes the sum of each subarray
    for( $i = 0; $i < $n; $i++)
    {
        $ksum = $ksum + $arr[$i];

        // one subarray is found
        if($ksum == $sum)
        {
            // to locate another
            $ksum = 0;
            $count++;
        }
    }

    if($count == $k)
        return 1;
    else
        return 0;

}

// Driver code
$arr = array(1, 1, 2, 2);
$k = 2;
$n = count($arr);
if (KpartitionsPossible($arr, $n, $k) == 0)
    echo "Yes";
else
    echo "No";

// This code is contributed by
// Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript program to check if array
// can be split into K contiguous
// subarrays each having equal sum

// Function returns true to it is possible to
// create K contiguous partitions each having
// equal sum, otherwise false
function KpartitionsPossible(arr, n, k)
{
    let sum = 0;
    let count = 0;

    // Calculate the sum of the array
    for(let i = 0; i < n; i++)
        sum = sum + arr[i];

    if (sum % k != 0)
        return 0;

    sum = parseInt(sum / k, 10);
    let ksum = 0;

    // ksum denotes the sum of each subarray
    for(let i = 0; i < n; i++)
    {
        ksum = ksum + arr[i];

        // One subarray is found
        if (ksum == sum)
        {

            // To locate another
            ksum = 0;
            count++;
        }
    }

    if (count == k)
        return 1;
    else
        return 0;
}

// Driver code
let arr = [ 1, 1, 2, 2 ];
let k = 2;
let n = arr.length;

if (KpartitionsPossible(arr, n, k) == 0)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
Yes
```