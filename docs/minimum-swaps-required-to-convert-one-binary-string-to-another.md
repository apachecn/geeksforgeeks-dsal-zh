# 将一个二进制字符串转换为另一个二进制字符串所需的最小交换次数

> 原文:[https://www . geesforgeks . org/minimum-swaps-required-convert-one-binary-string-to-other/](https://www.geeksforgeeks.org/minimum-swaps-required-to-convert-one-binary-string-to-another/)

给定两个长度相等的二进制字符串 **M** 和 **N** ，任务是找到将字符串 **N** 转换为 **M** 所需的最小操作数(交换)。
**举例:**

```
Input: str1 = "1101", str2 = "1110"
Output: 1
Swap last and second last element in the binary string, 
so that it become 1101

Input: str1 = "1110000", str2 = "0001101"
Output: 3
```

**方法:**初始化计数器并迭代 M，以便如果在两个二进制字符串中发现任何不相等的元素，则递增计数器。最后，如果计数器为偶数，则打印结果/2，因为对于一次交换，两个元素不相同。
假设**S1 =“10”**和**S2 =“01”**，那么两对不相同，计数= 2，由于计数为偶数，所以互换数量为计数/2，即 1。偶数决定了交换元素的机会。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Method to count swaps
void minSwaps(string str1, string str2)
{
    // Initialize the count
    int count = 0;

    // Iterate the loop with str1 length
    for (int i = 0; i < str1.length(); i++) {

        // If any non-equal elements are found
        // increment the counter
        if (str1[i] != str2[i])
            count++;
    }

    // If counter is even print the swap
    if (count % 2 == 0)
        cout << count / 2;
    else
        cout << "Not Possible";
}

// Driver code
int main()
{
    // Take two input
    string binaryString1 = "1110000";
    string binaryString2 = "0001101";

    // Call the method
    minSwaps(binaryString1, binaryString2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count minimum number of swap
// required to make string N to M
public class GFG {

    // Method to count swaps
    static void minSwaps(String str1, String str2)
    {
        // Initialize the count
        int count = 0;

        // Iterate the loop with str1 length
        for (int i = 0; i < str1.length(); i++) {

            // If any non-equal elements are found
            // increment the counter
            if (str1.charAt(i) != str2.charAt(i))
                count++;
        }

        // If counter is even print the swap
        if (count % 2 == 0)
            System.out.println(count / 2);
        else
            System.out.println("Not Possible");
    }

    // Driver Code
    public static void main(String args[])
    {
        // Take two input
        String binaryString1 = "1110000";
        String binaryString2 = "0001101";

        // Call the method
        minSwaps(binaryString1, binaryString2);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# function to count swaps
def minSwaps(str1, str2) :

    # Initialize the count
    count = 0

    # Iterate the loop with
    # length of str1
    for i in range(len(str1)) :

        # If any non-equal elements are
        # found increment the counter
        if str1[i] != str2[i] :
            count += 1

    # If counter is even print
    # the swap
    if count % 2 == 0 :
        print(count // 2)
    else :
        print("Not Possible")

# Driver code
if __name__ == "__main__" :

    # Take two input
    binaryString1 = "1110000"
    binaryString2 = "0001101"

    # Call the function
    minSwaps( binaryString1, binaryString2)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program to count minimum number of swap
// required to make string N to M
using System;
class GFG
{

// Method to count swaps
static void minSwaps(string str1, string str2)
{
    // Initialize the count
    int count = 0;

    // Iterate the loop with str1 length
    for (int i = 0; i < str1.Length; i++) {

        // If any non-equal elements are found
        // increment the counter
        if (str1[i] != str2[i])
            count++;
    }

    // If counter is even print the swap
    if (count % 2 == 0)
        Console.WriteLine(count / 2);
    else
        Console.WriteLine("Not Possible");
}

// Driver Code
public static void Main()
{
    // Take two input
    string binaryString1 = "1110000";
    string binaryString2 = "0001101";

    // Call the method
    minSwaps(binaryString1, binaryString2);
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above
// approach

// Method to count swaps
function minSwaps($str1, $str2)
{
    // Initialize the count
    $count = 0;

    // Iterate the loop with str1 length
    for ($i = 0; $i < strlen($str1); $i++)
    {

        // If any non-equal elements are
        // found increment the counter
        if ($str1[$i] != $str2[$i])
            $count++;
    }

    // If counter is even print the swap
    if ($count % 2 == 0)
        echo ($count / 2);
    else
        echo "Not Possible";
}

// Driver code

// Take two input
$binaryString1 = "1110000";
$binaryString2 = "0001101";

// Call the method
minSwaps($binaryString1, $binaryString2);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>
      // JavaScript Program to count minimum number of swap
      // required to make string N to M
      // Method to count swaps
      function minSwaps(str1, str2) {
        // Initialize the count
        var count = 0;

        // Iterate the loop with str1 length
        for (var i = 0; i < str1.length; i++) {
          // If any non-equal elements are found
          // increment the counter
          if (str1[i] !== str2[i]) count++;
        }

        // If counter is even print the swap
        if (count % 2 === 0) document.write(count / 2);
        else document.write("Not Possible");
      }

      // Driver Code
      // Take two input
      var binaryString1 = "1110000";
      var binaryString2 = "0001101";

      // Call the method
      minSwaps(binaryString1, binaryString2);
    </script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)