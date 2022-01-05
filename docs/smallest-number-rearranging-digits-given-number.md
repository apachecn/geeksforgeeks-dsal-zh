# 通过重新排列给定数字的位数得到的最小数字

> 原文:[https://www . geesforgeks . org/最小数字-重新排列-数字-给定数字/](https://www.geeksforgeeks.org/smallest-number-rearranging-digits-given-number/)

找出最小的数字(不是前导零)，它可以通过重新排列给定数字的数字来获得。

**示例:**

```
Input: n = 846903
Output: 304689

Input: n = 55010
Output: 10055

Input: n = -40505
Output: -55400
```

寻找最小数字的步骤。

1.  计算数字中每个数字的频率。
2.  如果它是非负数，那么
    1.  将最小的数字(0 除外)放在所需数字的最左边。
        并将该数字的频率减 1。
    2.  将所有剩余的数字按从左到右的升序排列。
3.  否则如果是负数
    1.  将最大的数字放在所需数字的最左边。并将该数字的频率递减 1。
    2.  将所有剩余的数字从右向左降序排列。

本解决方案基于[计数排序](https://www.geeksforgeeks.org/counting-sort/)。

## C++

```
// C++ program for finding smallest number
// from digits of given number
#include<iostream>
using namespace std;

// function to find the smallest number
int smallest(int num)
{
    // initialize frequency of each digit to Zero
    int freq[10] = {0};

      // Checking Number is positive or Negative
    bool is_pos = (num>0);

      // Getting the absolute value of num
    num = abs(num);

    // count frequency of each digit in the number
    while (num)
    {
        int d = num % 10; // extract last digit
        freq[d]++; // increment counting
        num = num / 10; //remove last digit
    }

    int result = 0;

      // If it is positive Number then it should be smallest
      if(is_pos)
    {
      // Set the Leftmost digit to minimum except 0
      for (int i = 1 ; i <= 9 ; i++)
      {
          if (freq[i])
          {
              result = i;
              freq[i]--;
              break;
          }
      }

      // arrange all remaining digits
      // in ascending order
      for (int i = 0 ; i <= 9 ; i++)
          while (freq[i]--)
              result = result * 10 + i;
    }
    else  // If negative then number should be Largest
    {
      // Set the Leftmost digit to maximum
      for (int i = 9 ; i >= 1 ; i--)
      {
         if (freq[i])
         {
            result = i;
            freq[i]--;
            break;
         }
      }

      // arrange all remaining digits
      // in descending order
      for (int i = 9 ; i >=0 ; i--)
         while (freq[i]--)
            result = result * 10 + i;

      // Negative number should be returned here
      result = -result;
    }
    return result;
}

// Driver Program
int main()
{
    int num = 570107;
    cout << smallest(num) << endl;

    int num2 = -691005;
    cout << smallest(num2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.lang.Math;

// Java program for finding smallest number
// from digits of given number
public class GFG {

    // function to find the smallest number
    static int smallest(int num)
    {
        // initialize frequency of each digit to Zero
        int[] freq = new int[10];

           // Checking Number is positive or Negative
        boolean is_pos = (num>0);

          // Getting the absolute value of num
        num = Math.abs(num);

        // count frequency of each digit in the number
        while (num > 0)
        {
            int d = num % 10; // extract last digit
            freq[d]++; // increment counting
            num = num / 10; //remove last digit
        }

       int result = 0;

          // If it is positive Number then it should be smallest
          if(is_pos)
        {
            // Set the LEFTMOST digit to minimum expect 0
            for (int i = 1 ; i <= 9 ; i++)
            {
                    if (freq[i] != 0)
                {
                        result = i;
                        freq[i]--;
                    break;
                }
            }

            // arrange all remaining digits
            // in ascending order
            for (int i = 0 ; i <= 9 ; i++)
                while (freq[i]-- != 0)
                    result = result * 10 + i;
         }
          else  // If negative then number should be Largest
        {
          // Set the Rightmost digit to maximum
          for (int i = 9 ; i >= 1 ; i--)
          {
             if (freq[i] !=0)
             {
                result = i;
                freq[i]--;
                break;
             }
          }

          // arrange all remaining digits
          // in descending order
          for (int i = 9 ; i >=0 ; i--)
             while (freq[i]-- != 0)
                result = result * 10 + i;

          // Negative number should be returned here
          result = -result;
        }
        return result;
    }

    // Driver Program
    public static void main(String args[])
    {
        int num = 570107;
        System.out.println(smallest(num));

        int num2 = -691005;
        System.out.println(smallest(num2));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Function to find the smallest number
def smallest(lst):

    # Here i is index and n is the number of the list
    for i,n in enumerate(lst):

        # Checking for the first non-zero digit in the sorted list
        if n != '0':

            # Remove and store the digit from the lst
            tmp = lst.pop(i)
            break

    # Place the first non-zero digit at the starting
    # and return the final number
    return str(tmp) + ''.join(lst)

# Driver program
if __name__ == '__main__':

    # Converting the given numbers into string to form a list
    lst = list(str(570107))
    lst.sort()

    # Calling the function using the above list
    print smallest(lst)

# This code is contributed by Mahendra Yadav
```

## C#

```
// C# program for finding smallest
// number from digits of given
// number
using System;

public class GFG {

    // function to find the smallest
    // number
    static int smallest(int num)
    {

        // initialize frequency of
        // each digit to Zero
        int[] freq = new int[10];

        // count frequency of each
        // digit in the number
        while (num > 0)
        {

            // extract last digit
            int d = num % 10;

            // increment counting
            freq[d]++;

            //remove last digit
            num = num / 10;
        }

        // Set the LEFTMOST digit to
        // minimum expect 0
        int result = 0;
        for (int i = 1 ; i <= 9 ; i++)
        {
            if (freq[i] != 0)
            {
                result = i;
                freq[i]--;
                break;
            }
        }

        // arrange all remaining digits
        // in ascending order
        for (int i = 0 ; i <= 9 ; i++)
            while (freq[i]-- != 0)
                result = result * 10 + i;

        return result;
    }

    // Driver Program
    public static void Main()
    {
        int num = 570107;
        Console.WriteLine(smallest(num));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding smallest
// number from digits of given number

// function to find the smallest number
function smallest($num)
{
    // initialize frequency of
    // each digit to Zero
    $freq = array_fill(0, 10, 0);

    // count frequency of each
    // digit in the number
    while ($num)
    {
        $d = $num % 10; // extract last digit
        $freq[$d]++; // increment counting
        $num = (int)($num / 10); // remove last digit
    }

    // Set the LEFTMOST digit
    // to minimum expect 0
    $result = 0;
    for ($i = 1 ; $i <= 9 ; $i++)
    {
        if ($freq[$i])
        {
            $result = $i;
            $freq[$i]--;
            break;
        }
    }

    // arrange all remaining digits
    // in ascending order
    for ($i = 0 ; $i <= 9 ; $i++)
        while ($freq[$i] > 0)
        {
            $result = $result * 10 + $i;
            $freq[$i] -= 1;
        }

    return $result;
}

// Driver Code
$num = 570107;
echo smallest($num);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for finding smallest number
// from digits of given number

// function to find the smallest number
function smallest(num)
{
    // initialize frequency of each digit to Zero
    var freq = Array(10).fill(0);

    // count frequency of each digit in the number
    while (num)
    {
        var d = num % 10; // extract last digit
        freq[d]++; // increment counting
        num = parseInt(num / 10); //remove last digit
    }

    // Set the LEFTMOST digit to minimum expect 0
    var result = 0;
    for (var i = 1 ; i <= 9 ; i++)
    {
        if (freq[i])
        {
            result = i;
            freq[i]--;
            break;
        }
    }

    // arrange all remaining digits
    // in ascending order
    for (var i = 0 ; i <= 9 ; i++)
        while (freq[i]--)
            result = result * 10 + i;

    return result;
}

// Driver Program
var num = 570107;
document.write(smallest(num));

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
100577
-965100
```

**另一种方法:** [求给定数的最小排列](https://www.geeksforgeeks.org/find-smallest-permutation-given-number/)
本文由**Ajay Kumar aghari(aJy aGr)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。