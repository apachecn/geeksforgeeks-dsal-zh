# 找到出现一次的元素

> 原文:[https://www . geeksforgeeks . org/find-出现的元素-出现-一次/](https://www.geeksforgeeks.org/find-the-element-that-appears-once/)

给定一个数组，其中每个元素出现三次，只有一个元素只出现一次。找到出现一次的元素。预期的时间复杂度是 O(n)和 O(1)个额外空间。

**示例:**

> **输入:** arr[] = {12，1，12，3，12，1，1，2，3，3}
> **输出:** 2
> 在给定数组中，除了出现一次的 2 之外，所有元素都出现三次。
> 
> **输入:** arr[] = {10，20，10，30，10，30，30}
> **输出:** 20
> 在给定数组中，除了出现一次的 20 之外，所有元素都出现三次。

我们可以用排序在 O(nLogn)时间内完成。我们也可以使用哈希，它的最坏情况时间复杂度为 O(n)，但是需要额外的空间。
想法是对时间为 O(n)且使用 O(1)个额外空间的解使用按位运算符。该解决方案不像其他基于异或的解决方案那样容易，因为所有元素在这里出现的次数都是奇数。这个想法取自[这里](http://www.careercup.com/question?id=7902674)。
对数组中的所有元素运行循环。在每次迭代结束时，保持以下两个值。
*1:*第一次、第四次或第七次出现的位..等等。
*2:*出现第 2 次、第 5 次或第 8 次的位..等等。
最后我们返回‘一’的值
*如何维护‘一’和‘二’的值？*
“1”和“2”初始化为 0。对于数组中的每个新元素，找出新元素中的公共集合位和“1”的前一个值。这些公共设置位实际上是应该加到“二”上的位。所以用“二”对公共集合位进行按位异或运算。“二”还会获得一些第三次出现的额外位。这些额外的比特稍后被移除。
用“1”的前一个值对新元素进行异或运算，更新“1”。有些位可能会出现第三次。这些额外的位稍后也会被移除。
1 和 2 都包含第三次出现的额外位。通过找出“1”和“2”中常见的设置位来删除这些多余的位。

下面是上述方法的实现:

## C++

```
// C++ program to find the element
// that occur only once
#include <bits/stdc++.h>
using namespace std;

int getSingle(int arr[], int n)
{
    int ones = 0, twos = 0;

    int common_bit_mask;

    // Let us take the example of
    // {3, 3, 2, 3} to understand
    // this
    for (int i = 0; i < n; i++) {

        /* The expression "one & arr[i]" gives the bits that
        are there in both 'ones' and new element from arr[].
        We add these bits to 'twos' using bitwise OR

        Value of 'twos' will be set as 0, 3, 3 and 1 after
        1st, 2nd, 3rd and 4th iterations respectively */
        twos = twos | (ones & arr[i]);

        /* XOR the new bits with previous 'ones' to get all
        bits appearing odd number of times

        Value of 'ones' will be set as 3, 0, 2 and 3 after
        1st, 2nd, 3rd and 4th iterations respectively */
        ones = ones ^ arr[i];

        /* The common bits are those bits which appear third
        time So these bits should not be there in both
        'ones' and 'twos'. common_bit_mask contains all
        these bits as 0, so that the bits can be removed
        from 'ones' and 'twos'

        Value of 'common_bit_mask' will be set as 00, 00, 01
        and 10 after 1st, 2nd, 3rd and 4th iterations
        respectively */
        common_bit_mask = ~(ones & twos);

        /* Remove common bits (the bits that appear third
        time) from 'ones'

        Value of 'ones' will be set as 3, 0, 0 and 2 after
        1st, 2nd, 3rd and 4th iterations respectively */
        ones &= common_bit_mask;

        /* Remove common bits (the bits that appear third
        time) from 'twos'

        Value of 'twos' will be set as 0, 3, 1 and 0 after
        1st, 2nd, 3rd and 4th iterations respectively */
        twos &= common_bit_mask;

        // uncomment this code to see intermediate values
        // printf (" %d %d n", ones, twos);
    }

    return ones;
}

// Driver code
int main()
{
    int arr[] = { 3, 3, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "The element with single occurrence is  "
         << getSingle(arr, n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to find the element
// that occur only once
#include <stdio.h>

int getSingle(int arr[], int n)
{
    int ones = 0, twos = 0;

    int common_bit_mask;

    // Let us take the example of {3, 3, 2, 3} to understand this
    for (int i = 0; i < n; i++) {
        /* The expression "one & arr[i]" gives the bits that are
           there in both 'ones' and new element from arr[].  We
           add these bits to 'twos' using bitwise OR

           Value of 'twos' will be set as 0, 3, 3 and 1 after 1st,
           2nd, 3rd and 4th iterations respectively */
        twos = twos | (ones & arr[i]);

        /* XOR the new bits with previous 'ones' to get all bits
           appearing odd number of times

           Value of 'ones' will be set as 3, 0, 2 and 3 after 1st,
           2nd, 3rd and 4th iterations respectively */
        ones = ones ^ arr[i];

        /* The common bits are those bits which appear third time
           So these bits should not be there in both 'ones' and 'twos'.
           common_bit_mask contains all these bits as 0, so that the bits can
           be removed from 'ones' and 'twos'  

           Value of 'common_bit_mask' will be set as 00, 00, 01 and 10
           after 1st, 2nd, 3rd and 4th iterations respectively */
        common_bit_mask = ~(ones & twos);

        /* Remove common bits (the bits that appear third time) from 'ones'

           Value of 'ones' will be set as 3, 0, 0 and 2 after 1st,
           2nd, 3rd and 4th iterations respectively */
        ones &= common_bit_mask;

        /* Remove common bits (the bits that appear third time) from 'twos'

           Value of 'twos' will be set as 0, 3, 1 and 0 after 1st,
           2nd, 3rd and 4th iterations respectively */
        twos &= common_bit_mask;

        // uncomment this code to see intermediate values
        // printf (" %d %d n", ones, twos);
    }

    return ones;
}

int main()
{
    int arr[] = { 3, 3, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("The element with single occurrence is %d ",
           getSingle(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the element
// that occur only once

class GFG {
    // Method to find the element that occur only once
    static int getSingle(int arr[], int n)
    {
        int ones = 0, twos = 0;
        int common_bit_mask;

        for (int i = 0; i < n; i++) {
            /*"one & arr[i]" gives the bits that are there in
            both 'ones' and new element from arr[]. We
            add these bits to 'twos' using bitwise OR*/
            twos = twos | (ones & arr[i]);

            /*"one & arr[i]" gives the bits that are
            there in both 'ones' and new element from arr[].
            We add these bits to 'twos' using bitwise OR*/
            ones = ones ^ arr[i];

            /* The common bits are those bits which appear third time
            So these bits should not be there in both 'ones' and 'twos'.
            common_bit_mask contains all these bits as 0, so that the bits can
            be removed from 'ones' and 'twos'*/
            common_bit_mask = ~(ones & twos);

            /*Remove common bits (the bits that appear third time) from 'ones'*/
            ones &= common_bit_mask;

            /*Remove common bits (the bits that appear third time) from 'twos'*/
            twos &= common_bit_mask;
        }
        return ones;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 3, 3, 2, 3 };
        int n = arr.length;
        System.out.println("The element with single occurrence is " + getSingle(arr, n));
    }
}
// Code contributed by Rishab Jain
```

## 蟒蛇 3

```
# Python3 code to find the element that
# appears once

def getSingle(arr, n):
    ones = 0
    twos = 0

    for i in range(n):
        # one & arr[i]" gives the bits that
        # are there in both 'ones' and new
        # element from arr[]. We add these
        # bits to 'twos' using bitwise XOR
        twos = twos ^ (ones & arr[i])

        # one & arr[i]" gives the bits that
        # are there in both 'ones' and new
        # element from arr[]. We add these
        # bits to 'twos' using bitwise XOR
        ones = ones ^ arr[i]

        # The common bits are those bits
        # which appear third time. So these
        # bits should not be there in both
        # 'ones' and 'twos'. common_bit_mask
        # contains all these bits as 0, so
        # that the bits can be removed from
        # 'ones' and 'twos'
        common_bit_mask = ~(ones & twos)

        # Remove common bits (the bits that
        # appear third time) from 'ones'
        ones &= common_bit_mask

        # Remove common bits (the bits that
        # appear third time) from 'twos'
        twos &= common_bit_mask
    return ones

# driver code
arr = [3, 3, 2, 3]
n = len(arr)
print("The element with single occurrence is ",
        getSingle(arr, n))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# code to find the element
// that occur only once
using System;
class GFG {
    // Method to find the element
    // that occur only once
    static int getSingle(int[] arr, int n)
    {
        int ones = 0, twos = 0;
        int common_bit_mask;

        for (int i = 0; i < n; i++) {
            // "one & arr[i]" gives the bits
            // that are there in both 'ones'
            // and new element from arr[].
            // We add these bits to 'twos'
            // using bitwise OR
            twos = twos | (ones & arr[i]);

            // "one & arr[i]" gives the bits
            // that are there in both 'ones'
            // and new element from arr[].
            // We add these bits to 'twos'
            // using bitwise OR
            ones = ones ^ arr[i];

            // The common bits are those bits
            // which appear third time So these
            // bits should not be there in both
            // 'ones' and 'twos'. common_bit_mask
            // contains all these bits as 0,
            // so that the bits can be removed
            // from 'ones' and 'twos'
            common_bit_mask = ~(ones & twos);

            // Remove common bits (the bits that
            // appear third time) from 'ones'
            ones &= common_bit_mask;

            // Remove common bits (the bits that
            // appear third time) from 'twos'
            twos &= common_bit_mask;
        }
        return ones;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 3, 3, 2, 3 };
        int n = arr.Length;
        Console.WriteLine("The element with single"
                          + "occurrence is " + getSingle(arr, n));
    }
}

// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the element
// that occur only once

function getSingle($arr, $n)
{
    $ones = 0; $twos = 0 ;

    $common_bit_mask;

    // Let us take the example of
    // {3, 3, 2, 3} to understand this
    for($i = 0; $i < $n; $i++ )
    {
        /* The expression "one & arr[i]"
        gives the bits that are there in
        both 'ones' and new element from
        arr[]. We add these bits to 'twos'
        using bitwise OR
        Value of 'twos' will be set as 0,
        3, 3 and 1 after 1st, 2nd, 3rd
        and 4th iterations respectively */
        $twos = $twos | ($ones & $arr[$i]);

        /* XOR the new bits with previous
        'ones' to get all bits appearing
        odd number of times

        Value of 'ones' will be set as 3,
        0, 2 and 3 after 1st, 2nd, 3rd and
        4th iterations respectively */
        $ones = $ones ^ $arr[$i];

        /* The common bits are those bits
        which appear third time. So these
        bits should not be there in both
        'ones' and 'twos'. common_bit_mask
        contains all these bits as 0, so
        that the bits can be removed from
        'ones' and 'twos'

        Value of 'common_bit_mask' will be
        set as 00, 00, 01 and 10 after 1st,
        2nd, 3rd and 4th iterations respectively */
        $common_bit_mask = ~($ones & $twos);

        /* Remove common bits (the bits
        that appear third time) from 'ones'

        Value of 'ones' will be set as 3,
        0, 0 and 2 after 1st, 2nd, 3rd
        and 4th iterations respectively */
        $ones &= $common_bit_mask;

        /* Remove common bits (the bits
        that appear third time) from 'twos'

        Value of 'twos' will be set as 0, 3,
        1 and 0 after 1st, 2nd, 3rd and 4th
        iterations respectively */
        $twos &= $common_bit_mask;

        // uncomment this code to see
        // intermediate values
        // printf (" %d %d n", ones, twos);
    }

    return $ones;
}

// Driver Code
$arr = array(3, 3, 2, 3);
$n = sizeof($arr);
echo "The element with single " .
                "occurrence is ",
             getSingle($arr, $n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Method to find the element that occur only once
    function getSingle(arr, n)
    {
        let ones = 0, twos = 0;
        let common_bit_mask;

        for (let i = 0; i < n; i++) {
            /*"one & arr[i]" gives the bits that are there in
            both 'ones' and new element from arr[]. We
            add these bits to 'twos' using bitwise OR*/
            twos = twos | (ones & arr[i]);

            /*"one & arr[i]" gives the bits that are
            there in both 'ones' and new element from arr[].
            We add these bits to 'twos' using bitwise OR*/
            ones = ones ^ arr[i];

            /* The common bits are those bits which appear third time
            So these bits should not be there in both 'ones' and 'twos'.
            common_bit_mask contains all these bits as 0, so that the bits can
            be removed from 'ones' and 'twos'*/
            common_bit_mask = ~(ones & twos);

            /*Remove common bits (the bits that appear third time) from 'ones'*/
            ones &= common_bit_mask;

            /*Remove common bits (the bits that appear third time) from 'twos'*/
            twos &= common_bit_mask;
        }
        return ones;
    }

// Driver Code

    let arr = [ 3, 3, 2, 3 ];
    let n = arr.length;
    document.write("The element with single occurrence is " + getSingle(arr, n));

</script>
```

**Output**

```
The element with single occurrence is  2
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

下面是 *aj* 建议的另一种 O(n)时间复杂度和 O(1)额外空间的方法。我们可以对所有数字的相同位置的位求和，并取 3 的模。总和不是 3 的倍数的位是出现一次的位数。
让我们考虑一下示例数组{5，5，5，8}。101，101，101，1000
第一位的和% 3 =(1+1+1+0)% 3 = 0；
第二位总和% 3 =(0+0+0+0)% 3 = 0；
第三位之和% 3 =(1+1+1+0)% 3 = 0；
第四位之和% 3 =(1)% 3 = 1；
因此出现一次的数字是 1000

**注意:**这种方法不适用于负数

下面是上述方法的实现:

## C++

```
// C++ program to find the element
// that occur only once
#include <bits/stdc++.h>
using namespace std;
#define INT_SIZE 32

int getSingle(int arr[], int n)
{
    // Initialize result
    int result = 0;

    int x, sum;

    // Iterate through every bit
    for (int i = 0; i < INT_SIZE; i++) {

        // Find sum of set bits at ith position in all
        // array elements
        sum = 0;
        x = (1 << i);
        for (int j = 0; j < n; j++) {
            if (arr[j] & x)
                sum++;
        }

        // The bits with sum not multiple of 3, are the
        // bits of element with single occurrence.
        if ((sum % 3) != 0)
            result |= x;
    }

    return result;
}

// Driver code
int main()
{
    int arr[] = { 12, 1, 12, 3, 12, 1, 1, 2, 3, 2, 2, 3, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "The element with single occurrence is " << getSingle(arr, n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to find the element
// that occur only once
#include <stdio.h>
#define INT_SIZE 32

int getSingle(int arr[], int n)
{
    // Initialize result
    int result = 0;

    int x, sum;

    // Iterate through every bit
    for (int i = 0; i < INT_SIZE; i++) {
        // Find sum of set bits at ith position in all
        // array elements
        sum = 0;
        x = (1 << i);
        for (int j = 0; j < n; j++) {
            if (arr[j] & x)
                sum++;
        }

        // The bits with sum not multiple of 3, are the
        // bits of element with single occurrence.
        if ((sum % 3) != 0)
            result |= x;
    }

    return result;
}

// Driver program to test above function
int main()
{
    int arr[] = { 12, 1, 12, 3, 12, 1, 1, 2, 3, 2, 2, 3, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("The element with single occurrence is %d ",
           getSingle(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the element
// that occur only once

class GFG {
    static final int INT_SIZE = 32;

    // Method to find the element that occur only once
    static int getSingle(int arr[], int n)
    {
        int result = 0;
        int x, sum;

        // Iterate through every bit
        for (int i = 0; i < INT_SIZE; i++) {
            // Find sum of set bits at ith position in all
            // array elements
            sum = 0;
            x = (1 << i);
            for (int j = 0; j < n; j++) {
                if ((arr[j] & x) != 0)
                    sum++;
            }
            // The bits with sum not multiple of 3, are the
            // bits of element with single occurrence.
            if ((sum % 3) != 0)
                result |= x;
        }
        return result;
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = { 12, 1, 12, 3, 12, 1, 1, 2, 3, 2, 2, 3, 7 };
        int n = arr.length;
        System.out.println("The element with single occurrence is " + getSingle(arr, n));
    }
}
// Code contributed by Rishab Jain
```

## 蟒蛇 3

```
# Python3 code to find the element
# that occur only once
INT_SIZE = 32

def getSingle(arr, n) :

    # Initialize result
    result = 0

    # Iterate through every bit
    for i in range(0, INT_SIZE) :

        # Find sum of set bits
        # at ith position in all
        # array elements
        sm = 0
        x = (1 << i)
        for j in range(0, n) :
            if (arr[j] & x) :
                sm = sm + 1

        # The bits with sum not
        # multiple of 3, are the
        # bits of element with
        # single occurrence.
        if ((sm % 3)!= 0) :
            result = result | x

    return result

# Driver program
arr = [12, 1, 12, 3, 12, 1, 1, 2, 3, 2, 2, 3, 7]
n = len(arr)
print("The element with single occurrence is ", getSingle(arr, n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# code to find the element
// that occur only once
using System;

class GFG {
    static int INT_SIZE = 32;

    // Method to find the element
    // that occur only once
    static int getSingle(int[] arr, int n)
    {
        int result = 0;
        int x, sum;

        // Iterate through every bit
        for (int i = 0; i < INT_SIZE; i++) {
            // Find sum of set bits at ith
            // position in all array elements
            sum = 0;
            x = (1 << i);
            for (int j = 0; j < n; j++) {
                if ((arr[j] & x) != 0)
                    sum++;
            }

            // The bits with sum not multiple
            // of 3, are the bits of element
            // with single occurrence.
            if ((sum % 3) != 0)
                result |= x;
        }
        return result;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 12, 1, 12, 3, 12, 1,
                      1, 2, 3, 2, 2, 3, 7 };
        int n = arr.Length;
        Console.WriteLine("The element with single "
                          + "occurrence is " + getSingle(arr, n));
    }
}

// This code is contributed ny vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the element
// that occur only once
$INT_SIZE= 32;

function getSingle($arr, $n)
{
    global $INT_SIZE;

    // Initialize result
    $result = 0;

    $x; $sum;

    // Iterate through every bit
    for ($i = 0; $i < $INT_SIZE; $i++)
    {
    // Find sum of set bits at ith
    // position in all array elements
    $sum = 0;
    $x = (1 << $i);
    for ($j = 0; $j < $n; $j++ )
    {
        if ($arr[$j] & $x)
            $sum++;
    }

    // The bits with sum not multiple
    // of 3, are the bits of element
    // with single occurrence.
    if (($sum % 3)  !=0 )
        $result |= $x;
    }

    return $result;
}

// Driver Code
$arr = array (12, 1, 12, 3, 12, 1,
              1, 2, 3, 2, 2, 3, 7);
$n = sizeof($arr);
echo "The element with single occurrence is ",
                          getSingle($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the element
    // that occur only once
    let INT_SIZE = 32;

    function getSingle(arr, n)
    {

        // Initialize result
        let result = 0;
        let x, sum;

        // Iterate through every bit
        for (let i = 0; i < INT_SIZE; i++)
        {

            // Find sum of set bits at ith position in all
            // array elements
            sum = 0;
            x = (1 << i);
            for (let j = 0; j < n; j++)
            {
                if (arr[j] & x)
                    sum++;
            }

            // The bits with sum not multiple of 3, are the
            // bits of element with single occurrence.
            if ((sum % 3) != 0)
                result |= x;
        }
        return result;
    }

// Driver code
    let arr = [ 12, 1, 12, 3, 12, 1, 1, 2, 3, 2, 2, 3, 7 ];
    let n = arr.length;
    document.write("The element with single occurrence is " + getSingle(arr, n));

// This code is contributed by mukesh07.
</script>
```

**Output**

```
The element with single occurrence is 7
```