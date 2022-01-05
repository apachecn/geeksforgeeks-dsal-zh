# 所有对之间的位差之和

> 原文:[https://www . geesforgeks . org/全对位差总和/](https://www.geeksforgeeks.org/sum-of-bit-differences-among-all-pairs/)

给定一个由 n 个整数组成的整数数组，求由数组元素组成的所有对中的位差之和。一对(x，y)的比特差是在 x 和 y 的二进制表示中相同位置的不同比特的计数。
例如，2 和 7 的比特差是 2。2 的二进制表示是 010，7 是 111(第一位和最后一位在两个数字上不同)。

**示例:**

```
Input: arr[] = {1, 2}
Output: 4
All pairs in array are (1, 1), (1, 2)
                       (2, 1), (2, 2)
Sum of bit differences = 0 + 2 +
                         2 + 0
                      = 4

Input:  arr[] = {1, 3, 5}
Output: 8
All pairs in array are (1, 1), (1, 3), (1, 5)
                       (3, 1), (3, 3) (3, 5),
                       (5, 1), (5, 3), (5, 5)
Sum of bit differences =  0 + 1 + 1 +
                          1 + 0 + 2 +
                          1 + 2 + 0 
                       = 8
```

来源:谷歌面试问题

**天真解决方案–**
A**简单解决方案**是运行两个循环来逐个考虑所有对。对于每一对，计算位差。最后返回计数总和。这个解的时间复杂度为 O(n <sup>2</sup> )。我们正在使用 [**位集::count()**](https://www.geeksforgeeks.org/bitsetcount-in-c-stl/) ，这是 C++中的一个内置 STL，它返回一个数的二进制表示中的集位数。

## C++

```
// C++ program to compute sum of pairwise bit differences
#include <bits/stdc++.h>
using namespace std;

int sum_bit_diff(vector<int> a)
{
    int n = a.size();
    int ans = 0;

    for (int i = 0; i < n - 1; i++) {
        int count = 0;

        for (int j = i; j < n; j++) {
            // Bitwise and of pair (a[i], a[j])
            int x = a[i] & a[j];
            // Bitwise or of pair (a[i], a[j])
            int y = a[i] | a[j];

            bitset<32> b1(x);
            bitset<32> b2(y);

            // to count set bits in and of two numbers
            int r1 = b1.count();
            // to count set bits in or of two numbers
            int r2 = b2.count();

            // Absolute differences at individual bit positions of two
            // numbers is contributed by pair (a[i], a[j]) in count
            count = abs(r1 - r2);

            // each pair adds twice of contributed count
            // as both (a, b) and (b, a) are considered
            // two separate pairs.
            ans = ans + (2 * count);
        }
    }
    return ans;
}

int main()
{

    vector<int> nums{ 10, 5 };
    int ans = sum_bit_diff(nums);

    cout << ans;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {

    static int sumBitDiff(int[] arr){
        int diff = 0;                                //hold the ans

          for(int i=0; i<arr.length; i++){
            for(int j=i; j<arr.length; j++){

              //XOR toggles the bits and will form a number that will have
              //set bits at the places where the numbers bits differ
              //eg: 010 ^ 111 = 101...diff of bits = count of 1's = 2

                 int xor = arr[i]^arr[j];
                  int count = countSetBits(xor);        //Integer.bitCount() can also be used

                  //when i == j (same numbers) the xor would be 0,
                  //thus our ans will remain unaffected as (2*0 = 0)
                  diff += 2*count;
            }
        }

          return diff;
    }

    //Kernighan algo
      static int countSetBits(int n){
        int count = 0;            // `count` stores the total bits set in `n`

        while (n != 0) {
            n = n & (n - 1);    // clear the least significant bit set
            count++;
        }

        return count;
    }

    public static void main (String[] args) {
        int[] arr = {5,10};
          int ans  = sumBitDiff(arr);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
def sumBitDiff(arr):
    diff = 0    #hold the ans

    for i in range(len(arr)):
        for j in range(i, len(arr)):

        # XOR toggles the bits and will form a number that will have
        # set bits at the places where the numbers bits differ
        # eg: 010 ^ 111 = 101...diff of bits = count of 1's = 2          
            xor = arr[i]^arr[j]
            count = countSetBits(xor)        #Integer.bitCount() can also be used

            # when i == j (same numbers) the xor would be 0,
            # thus our ans will remain unaffected as (2*0 = 0)
            diff += (2*count)

    return diff

# Kernighan algo
def countSetBits(n):
    count = 0            # `count` stores the total bits set in `n`

    while (n != 0) :
        n = n & (n - 1)    # clear the least significant bit set
        count += 1

    return count

# Driver code
if __name__ == "__main__":

    arr = [5,10]
    ans  = sumBitDiff(arr)
    print(ans)

    # This code is contributed by sanjoy_62.
```

## C#

```
/*package whatever //do not write package name here */

using System;

public class GFG {

    static int sumBitDiff(int[] arr){
        int diff = 0;                                //hold the ans

          for(int i=0; i<arr.Length; i++){
            for(int j=i; j<arr.Length; j++){

              //XOR toggles the bits and will form a number that will have
              //set bits at the places where the numbers bits differ
              //eg: 010 ^ 111 = 101...diff of bits = count of 1's = 2

                 int xor = arr[i]^arr[j];
                  int count = countSetBits(xor);        //int.bitCount() can also be used

                  //when i == j (same numbers) the xor would be 0,
                  //thus our ans will remain unaffected as (2*0 = 0)
                  diff += 2*count;
            }
        }

          return diff;
    }

    //Kernighan algo
      static int countSetBits(int n){
        int count = 0;            // `count` stores the total bits set in `n`

        while (n != 0) {
            n = n & (n - 1);    // clear the least significant bit set
            count++;
        }

        return count;
    }

    public static void Main(String[] args) {
        int[] arr = {5,10};
          int ans  = sumBitDiff(arr);
        Console.WriteLine(ans);
    }
}

// This code contributed by umadevi9616
```

## java 描述语言

```
<script>

// javascript program for above approach
    function sumBitDiff(arr)
    {
        let diff = 0;                               
        // hold the ans

          for(let i = 0; i < arr.length; i++){
            for(let j = i; j < arr.length; j++){

              // XOR toggles the bits and will form a number that will have
              // set bits at the places where the numbers bits differ
              // eg: 010 ^ 111 = 101...diff of bits = count of 1's = 2

                 let xor = arr[i]^arr[j];
                  let count = countSetBits(xor);       
                  // Integer.bitCount() can also be used

                  // when i == j (same numbers) the xor would be 0,
                  // thus our ans will remain unaffected as (2*0 = 0)
                  diff += 2*count;
            }
        }

          return diff;
    }

    // Kernighan algo
      function countSetBits(n){
        let count = 0;            // `count` stores the total bits set in `n`

        while (n != 0) {
            n = n & (n - 1);    // clear the least significant bit set
            count++;
        }

        return count;
    }

// Driver code
    let arr = [5,10];
    let ans  = sumBitDiff(arr);
    document.write(ans);

    // This code is contributed by splevel62.
</script>
```

**Output**

```
8
```

***时间复杂度:** O(n <sup>2</sup> )*

***辅助空间:** O(1)*

**高效解决方案–**

一个**有效的解决方案**可以在 O(n)时间内解决这个问题，利用所有数字都用 32 位(或某个固定的位数)表示的事实。其思想是计算各个位位置的差异。我们从 0 到 31 遍历，用第 I 个位组计数。让这个计数成为“计数”。会有第 I 位未置位的“n 计数”数字。因此，第 I 位的差异计数将是“计数*(n-计数)* 2”，这个公式的原因是，每个具有在第 I 位设置了位的元素和在第 I 位具有未设置位的第二个元素的配对对总和的贡献正好是 1，因此总置换计数将是计数*(n-计数)并乘以 2，这是因为根据对 1 的给定条件，所有这种类型的配对又重复了一次< =i，j < =N。

下面是上述想法的实现。

## C++

```
// C++ program to compute sum of pairwise bit differences
#include <bits/stdc++.h>
using namespace std;

int sumBitDifferences(int arr[], int n)
{
    int ans = 0; // Initialize result

    // traverse over all bits
    for (int i = 0; i < 32; i++) {
        // count number of elements with i'th bit set
        int count = 0;
        for (int j = 0; j < n; j++)
            if ((arr[j] & (1 << i)))
                count++;

        // Add "count * (n - count) * 2" to the answer
        ans += (count * (n - count) * 2);
    }

    return ans;
}

// Driver prorgram
int main()
{
    int arr[] = { 1, 3, 5 };
    int n = sizeof arr / sizeof arr[0];
    cout << sumBitDifferences(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute sum of pairwise
// bit differences

import java.io.*;

class GFG {

    static int sumBitDifferences(int arr[], int n)
    {

        int ans = 0; // Initialize result

        // traverse over all bits
        for (int i = 0; i < 32; i++) {

            // count number of elements
            // with i'th bit set
            int count = 0;

            for (int j = 0; j < n; j++)
                if ((arr[j] & (1 << i)) != 0)
                    count++;

            // Add "count * (n - count) * 2"
            // to the answer...(n - count = unset bit count)
            ans += (count * (n - count) * 2);
        }

        return ans;
    }

    // Driver prorgram
    public static void main(String args[])
    {

        int arr[] = { 1, 3, 5 };
        int n = arr.length;

        System.out.println(sumBitDifferences(
            arr, n));
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python program to compute sum of pairwise bit differences

def sumBitDifferences(arr, n):

    ans = 0  # Initialize result

    # traverse over all bits
    for i in range(0, 32):

        # count number of elements with i'th bit set
        count = 0
        for j in range(0, n):
            if ( (arr[j] & (1 << i)) ):
                count+= 1

        # Add "count * (n - count) * 2" to the answer
        ans += (count * (n - count) * 2);

    return ans

# Driver prorgram
arr = [1, 3, 5]
n = len(arr )
print(sumBitDifferences(arr, n))

# This code is contributed by
# Smitha Dinesh Semwal   
```

## C#

```
// C# program to compute sum
// of pairwise bit differences
using System;

class GFG {
    static int sumBitDifferences(int[] arr,
                                 int n)
    {
        int ans = 0; // Initialize result

        // traverse over all bits
        for (int i = 0; i < 32; i++) {

            // count number of elements
            // with i'th bit set
            int count = 0;
            for (int j = 0; j < n; j++)
                if ((arr[j] & (1 << i)) == 0)
                    count++;

            // Add "count * (n - count) * 2"
            // to the answer
            ans += (count * (n - count) * 2);
        }

        return ans;
    }
    // Driver Code
    public static void Main()
    {

        int[] arr = { 1, 3, 5 };
        int n = arr.Length;

        Console.Write(sumBitDifferences(arr, n));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute sum
// of pairwise bit differences

function sumBitDifferences($arr, $n)
{
    // Initialize result
    $ans = 0;

    // traverse over all bits
    for ($i = 0; $i < 32; $i++)
    {
        // count number of elements
        // with i'th bit set
        $count = 0;
        for ($j = 0; $j < $n; $j++)
            if (($arr[$j] & (1 << $i)))
                $count++;

        // Add "count * (n - count) * 2"
        // to the answer
        $ans += ($count * ($n -
                           $count) * 2);
    }

    return $ans;
}

// Driver Code
$arr = array(1, 3, 5);
$n = sizeof($arr);
echo sumBitDifferences($arr, $n), "\n";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to compute sum
// of pairwise bit differences
function sumBitDifferences(arr, n)
{

    // Initialize result
    let ans = 0;

    // Traverse over all bits
    for(let i = 0; i < 32; i++)
    {

        // count number of elements with i'th bit set
        let count = 0;
        for(let j = 0; j < n; j++)
            if ((arr[j] & (1 << i)))
                count++;

        // Add "count * (n - count) * 2" to the answer
        ans += (count * (n - count) * 2);
    }
    return ans;
}

// Driver code
let arr = [ 1, 3, 5 ];
let n = arr.length;

document.write(sumBitDifferences(arr, n));

// This code is contributed by subhammahato348

</script>
```

**输出:**

```
8
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

Asked in: [Google](https://practice.geeksforgeeks.org/company/Google/)

感谢 Gaurav Ahirwar 提出这个解决方案。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。