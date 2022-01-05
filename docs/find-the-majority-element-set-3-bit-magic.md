# 找到多数元素|集合 3(位魔法)

> 原文:[https://www . geesforgeks . org/find-多数元素集-3 位魔法/](https://www.geeksforgeeks.org/find-the-majority-element-set-3-bit-magic/)

**先决条件:** [多数元素](https://www.geeksforgeeks.org/majority-element/)、[多数元素|集合-2(散列)](https://www.geeksforgeeks.org/majority-element-set-2-hashing/)
给定大小为 N 的数组，找到多数元素。多数元素是在给定数组中出现 n/2 次以上的元素。

**示例:**

```
Input: {3, 3, 4, 2, 4, 4, 2, 4, 4}
Output: 4

Input: {3, 3, 6, 2, 4, 4, 2, 4}
Output: No Majority Element

```

**方法:**
在这篇文章中，我们借助数组中存在的数字的二进制表示来解决这个问题。
任务是找到出现 n/2 次以上的元素。所以，它看起来比所有其他数字加起来还要多。
所以，我们从数组的每个数字的 LSB(最低有效位)开始，我们数一数它被设置在数组的多少个数字中。如果在**中设置的任何位多于 n/2 个数**，则该位在我们的多数元素中设置。

上述方法之所以有效，是因为对于所有其他数字的组合，设置的位数不能超过 n/2，因为多数元素的出现次数超过 n/2 次。

让我们借助例子来看看

```
Input : {3, 3, 4, 2, 4, 4, 2, 4, 4}
Binary representation of the same are:

3 - 0 1 1
3 - 0 1 1
4 - 1 0 0
2 - 0 1 0
4 - 1 0 0
4 - 1 0 0
2 - 0 1 0
4 - 1 0 0
4 - 1 0 0
----------
  - 5 4 0 
```

这里 n 是 9，所以 n/2 = 4，并且仅从右数起的第三位满足计数> 4，因此在多数元素中被设置，并且所有其他位不被设置。

所以，我们的多数元素是 1 0 0，也就是 **4**
但是还有更多，当多数元素出现在数组中时，这种方法有效。如果它不存在呢？

让我们借助这个例子来看看:

```
Input : {3, 3, 6, 2, 4, 4, 2, 4}
Binary representation of the same are:

3 - 0 1 1
3 - 0 1 1
6 - 1 1 0
2 - 0 1 0
4 - 1 0 0
4 - 1 0 0
2 - 0 1 0
4 - 1 0 0
----------
  - 4 5 0 
```

这里 n 是 8，所以 n/2 = 4，并且仅从右数第二位满足计数> 4，因此设置它应该在多数元素中设置，而所有其他位不设置。

所以，根据这个，我们的多数元素是 0 1 0，也就是 **2** ，但实际上多数元素不在数组中。所以，我们对数组再做一遍，以确保这个元素出现的次数超过 n/2 次。

下面是上述想法的实现

## C++

```
#include <iostream>
using namespace std;

void findMajority(int arr[], int n)
{
    // Number of bits in the integer
    int len = sizeof(int) * 8;

    // Variable to calculate majority element
    int number = 0;

    // Loop to iterate through all the bits of number
    for (int i = 0; i < len; i++) {
        int count = 0;
        // Loop to iterate through all elements in array
        // to count the total set bit
        // at position i from right
        for (int j = 0; j < n; j++) {
            if (arr[j] & (1 << i))
                count++;
        }
        // If the total set bits exceeds n/2,
        // this bit should be present in majority Element.
        if (count > (n / 2))
            number += (1 << i);
    }

    int count = 0;

    // iterate through array get
    // the count of candidate majority element
    for (int i = 0; i < n; i++)
        if (arr[i] == number)
            count++;

    // Verify if the count exceeds n/2
    if (count > (n / 2))
        cout << number;
    else
        cout << "Majority Element Not Present";
}

// Driver Program
int main()
{

    int arr[] = { 3, 3, 4, 2, 4, 4, 2, 4, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findMajority(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
    static void findMajority(int arr[], int n)
    {
        // Number of bits in the integer
        int len = 32;

        // Variable to calculate majority element
        int number = 0;

        // Loop to iterate through all the bits of number
        for (int i = 0; i < len; i++)
        {
            int count = 0;
            // Loop to iterate through all elements in array
            // to count the total set bit
            // at position i from right
            for (int j = 0; j < n; j++)
            {
                if ((arr[j] & (1 << i)) != 0)
                    count++;
            }

            // If the total set bits exceeds n/2,
            // this bit should be present in majority Element.
            if (count > (n / 2))
                number += (1 << i);
        }

        int count = 0;

        // iterate through array get
        // the count of candidate majority element
        for (int i = 0; i < n; i++)
            if (arr[i] == number)
                count++;

        // Verify if the count exceeds n/2
        if (count > (n / 2))
            System.out.println(number);
        else
            System.out.println("Majority Element Not Present");
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 3, 3, 4, 2, 4, 4, 2, 4, 4 };
        int n = arr.length;
        findMajority(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
def findMajority(arr, n):

    # Number of bits in the integer
    Len = 32

    # Variable to calculate majority element
    number = 0

    # Loop to iterate through
    # all the bits of number
    for i in range(Len):
        count = 0

        # Loop to iterate through all elements
        # in array to count the total set bit
        # at position i from right
        for j in range(n):
            if (arr[j] & (1 << i)):
                count += 1

        # If the total set bits exceeds n/2,
        # this bit should be present in
        # majority Element.
        if (count > (n // 2)):
            number += (1 << i)

    count = 0

    # iterate through array get
    # the count of candidate majority element
    for i in range(n):
        if (arr[i] == number):
            count += 1

    # Verify if the count exceeds n/2
    if (count > (n // 2)):
        print(number)
    else:
        print("Majority Element Not Present")

# Driver Code
arr = [3, 3, 4, 2, 4, 4, 2, 4, 4]
n = len(arr)
findMajority(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
using System;

class GFG
{
    static void findMajority(int []arr, int n)
    {
        // Number of bits in the integer
        int len = 32;

        // Variable to calculate majority element
        int number = 0;

        // Loop to iterate through all the bits of number
        for (int i = 0; i < len; i++)
        {
            int countt = 0;

            // Loop to iterate through all elements
            // in array to count the total set bit
            // at position i from right
            for (int j = 0; j < n; j++)
            {
                if ((arr[j] & (1 << i)) != 0)
                    countt++;
            }

            // If the total set bits exceeds n/2,
            // this bit should be present in majority Element.
            if (countt > (n / 2))
                number += (1 << i);
        }

        int count = 0;

        // iterate through array get
        // the count of candidate majority element
        for (int i = 0; i < n; i++)
            if (arr[i] == number)
                count++;

        // Verify if the count exceeds n/2
        if (count > (n / 2))
            Console.Write(number);
        else
            Console.Write("Majority Element Not Present");
    }

    // Driver Code
    static public void Main ()
    {
        int []arr = { 3, 3, 4, 2, 4, 4, 2, 4, 4 };
        int n = arr.Length;
        findMajority(arr, n);
    }
}

// This code is contributed by @Tushi..
```

## java 描述语言

```
<script>

function findMajority(arr, n)
{

    // Number of bits in the integer
    let len = 32;

    // Variable to calculate majority element
    let number = 0;

    // Loop to iterate through all
    // the bits of number
    for(let i = 0; i < len; i++)
    {
        let countt = 0;

        // Loop to iterate through all elements
        // in array to count the total set bit
        // at position i from right
        for(let j = 0; j < n; j++)
        {
            if ((arr[j] & (1 << i)) != 0)
                countt++;
        }

        // If the total set bits exceeds n/2,
        // this bit should be present in
        // majority Element.
        if (countt > parseInt(n / 2, 10))
            number += (1 << i);
    }

    let count = 0;

    // Iterate through array get
    // the count of candidate
    // majority element
    for(let i = 0; i < n; i++)
        if (arr[i] == number)
            count++;

    // Verify if the count exceeds n/2
    if (count > parseInt(n / 2, 10))
        document.write(number);
    else
        document.write("Majority Element Not Present");
}

// Driver Code
let arr = [ 3, 3, 4, 2, 4, 4, 2, 4, 4 ];
let n = arr.length;

findMajority(arr, n);

// This code is contributed by decode2207

</script>
```

**Output:** 

```
4
```

**时间复杂度:O(N)**
**空间复杂度:O(1)**