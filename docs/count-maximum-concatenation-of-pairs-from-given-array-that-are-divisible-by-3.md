# 计算给定数组中可被 3 整除的最大对连接数

> 原文:[https://www . geeksforgeeks . org/count-给定可被 3 整除的数组中的最大对串联数/](https://www.geeksforgeeks.org/count-maximum-concatenation-of-pairs-from-given-array-that-are-divisible-by-3/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算其元素串联可被 **3** 整除的对，并且每个数组元素最多出现在一对中。

**示例:**

> **输入:** arr[] = { 5，3，2，8，7 }
> **输出:** 1
> **解释:**
> 串联可被 3 整除的可能对是{ 27，72，78，87 }，但数组元素 arr[4]最多出现在一对中。因此，所需的输出为 1
> 
> **输入:** arr[] = { 10，6，3，7，2 }
> T3】输出: 2

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对。对于每一对，检查该对元素的连接是否可被 **3** 整除。如果发现是真的，则将两个元素都标记为假，这样该对的两个元素就不能出现在多个对中。

下面是天真方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs whose concatenation
// is divisible by 3 and each element can be
// present in at most one pair
int countDivBy3InArray(int arr[], int N)
{

    // Stores count pairs whose concatenation
    // is divisible by 3 and each element can
    // be present in at most one pair
    int ans = 0;

    // Check if an element present
    // in any pair or not
    bool taken[N];
    memset(taken, false, sizeof(taken));

    // Generate all possible pairs
    for(int i = 0; i < N; i++)
    {

        // If the element already
        // present in a pair
        if (taken[i] == true)
        {
            continue;
        }
        for(int j = i + 1; j < N; j++)
        {

            // If the element already
            // present in a pair
            if (taken[j] == true)
            {
                continue;
            }

            // If concatenation of elements
            // is divisible by 3
            if (stoi(to_string(arr[i]) +
                    to_string(arr[j])) % 3 == 0 ||
                stoi(to_string(arr[j]) +
                    to_string(arr[i])) % 3 == 0)
            {

                // Update ans
                ans += 1;

                // Mark i is True
                taken[i] = true;

                // Mark j is True
                taken[j] = true;
            }
        }
    }
    return ans;
}

int main()
{
    int arr[] = { 5, 3, 2, 8, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // To display the result
    cout << countDivBy3InArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to count pairs whose concatenation
// is divisible by 3 and each element can be
// present in at most one pair
public static int countDivBy3InArray(int[] arr)
{

    // Stores count pairs whose concatenation
    // is divisible by 3 and each element can
    // be present in at most one pair
    int ans = 0;

    // Check if an element present
    // in any pair or not
    boolean[] taken = new boolean[arr.length];
    Arrays.fill(taken, false);

    // Generate all possible pairs
    for(int i = 0; i < arr.length; i++)
    {

        // If the element already
        // present in a pair
        if (taken[i] == true)
        {
            continue;
        }
        for(int j = i + 1; j < arr.length; j++)
        {

            // If the element already
            // present in a pair
            if (taken[j] == true)
            {
                continue;
            }

            // If concatenation of elements
            // is divisible by 3
            if (Integer.parseInt(
                    Integer.toString(arr[i]) +
                    Integer.toString(arr[j])) % 3 == 0 ||
                Integer.parseInt(
                    Integer.toString(arr[j]) +
                    Integer.toString(arr[i])) % 3 == 0)
            {

                // Update ans
                ans += 1;

                // Mark i is True
                taken[i] = true;

                // Mark j is True
                taken[j] = true;
            }
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 5, 3, 2, 8, 7 };

    // To display the result
    System.out.println(countDivBy3InArray(arr));
}
}

// This code is contributed by aditya7409
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count pairs whose concatenation is
# divisible by 3 and each element can be present
# in at most one pair
def countDivBy3InArray(arr):

    # Stores count pairs whose concatenation is
    # divisible by 3 and each element can be present
    # in at most one pair
    ans = 0

    # Check if an element present
    # in any pair or not
    taken = [False] * len(arr)

    # Generate all possible pairs
    for i in range(len(arr)):

        # If the element already
        # present in a pair
        if taken[i]:
            continue

        for j in range(i + 1, len(arr)):

            # If the element already
            # present in a pair
            if taken[j]:
                continue

            # If concatenation of elements
            # is divisible by 3
            if (not int(str(arr[i])+str(arr[j])) % 3 or
                 not int(str(arr[j])+str(arr[i])) % 3):

                # Update ans    
                ans += 1

                # Mark i is True
                taken[i] = True

                # Mark j is True
                taken[j] = True
    return ans

# Driver Code
arr = [5, 3, 2, 8, 7]

# To display the result
print(countDivBy3InArray(arr))
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

  // Function to count pairs whose concatenation
  // is divisible by 3 and each element can be
  // present in at most one pair
  public static int countDivBy3InArray(int[] arr)
  {

    // Stores count pairs whose concatenation
    // is divisible by 3 and each element can
    // be present in at most one pair
    int ans = 0;

    // Check if an element present
    // in any pair or not
    bool[] taken = new bool[arr.Length];

    // Generate all possible pairs
    for(int i = 0; i < arr.Length; i++)
    {

      // If the element already
      // present in a pair
      if (taken[i] == true)
      {
        continue;
      }
      for(int j = i + 1; j < arr.Length; j++)
      {

        // If the element already
        // present in a pair
        if (taken[j] == true)
        {
          continue;
        }

        // If concatenation of elements
        // is divisible by 3
        if (Int32.Parse(
          (arr[i]).ToString() +
          (arr[j]).ToString()) % 3 == 0 ||
            Int32.Parse(
              (arr[j]).ToString() +
              (arr[i]).ToString()) % 3 == 0)
        {

          // Update ans
          ans += 1;

          // Mark i is True
          taken[i] = true;

          // Mark j is True
          taken[j] = true;
        }
      }
    }
    return ans;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 5, 3, 2, 8, 7 };

    // To display the result
    Console.WriteLine(countDivBy3InArray(arr));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to count pairs whose concatenation
    // is divisible by 3 and each element can be
    // present in at most one pair
    function countDivBy3InArray(arr)
    {

      // Stores count pairs whose concatenation
      // is divisible by 3 and each element can
      // be present in at most one pair
      let ans = 0;

      // Check if an element present
      // in any pair or not
      let taken = new Array(arr.length);
      taken.fill(false);

      // Generate all possible pairs
      for(let i = 0; i < arr.length; i++)
      {

        // If the element already
        // present in a pair
        if (taken[i] == true)
        {
          continue;
        }
        for(let j = i + 1; j < arr.length; j++)
        {

          // If the element already
          // present in a pair
          if (taken[j] == true)
          {
            continue;
          }

          // If concatenation of elements
          // is divisible by 3
          if (parseInt((arr[i]).toString() + (arr[j]).toString(), 10) % 3 == 0 ||
              parseInt((arr[j]).toString() + (arr[i]).toString(), 10) % 3 == 0)
          {

            // Update ans
            ans += 1;

            // Mark i is True
            taken[i] = true;

            // Mark j is True
            taken[j] = true;
          }
        }
      }
      return ans;
    }

    let arr = [ 5, 3, 2, 8, 7 ];

    // To display the result
    document.write(countDivBy3InArray(arr));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**利用[检查一个数是否能被 3 整除](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)的概念，可以优化上述方法。按照以下步骤解决问题:

*   初始化三个变量，比如 **rem0** 、 **rem1** 和 **rem2** ，以存储数组元素的计数，当被 **3** 除时，数组元素的余数分别为 **0** 、 **1** 和 **2** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件:
    *   如果 **arr[i] %3 == 0** ，则更新 **cnt0 += 1** 。
    *   如果 **arr[i] %3 == 1** ，则更新 **cnt1 += 1** 。
    *   如果 **arr[i] %3 == 2** ，则更新 **cnt2 += 1** 。
*   最后，打印对的计数，即 **(rem0 / 2 + min(rem1，rem2))** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs whose concatenation is
// divisible by 3 and each element can be present
// in at most one pair
int countDiv(int arr[], int n)
{

    // Stores count of array elements whose
    // remainder is 0 by taking modulo by 3
    int rem0 = 0;

    // Stores count of array elements whose
    // remainder is 1 by taking modulo by 3
    int rem1 = 0;

    // Stores count of array elements whose
    // remainder is 2 by taking modulo by 3
    int rem2 = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Stores sum of digits
        // of arr[i]
        int digitSum = 0;

        // Update digitSum
        digitSum += arr[i];

        // If remainder of digitSum by
        // by taking modulo 3 is 0
        if (digitSum % 3 == 0)
        {

            // Update rem0
            rem0 += 1;
        }

        // If remainder of digitSum by
        // by taking modulo 3 is 1
        else if (digitSum % 3 == 1)
        {

            // Update rem1
            rem1 += 1;
        }
        else
        {

            // Update rem2
            rem2 += 1;
        }
    }
    return (rem0 / 2 + min(rem1, rem2));
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 2, 8, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // To display the result
    cout << (countDiv(arr, n));
}

// This code is contributed by ukasp
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
public class GFG
{

  // Function to count pairs whose concatenation is
  // divisible by 3 and each element can be present
  // in at most one pair
  static int countDiv(int[] arr)
  {

    // Stores count of array elements whose
    // remainder is 0 by taking modulo by 3
    int rem0 = 0;

    // Stores count of array elements whose
    // remainder is 1 by taking modulo by 3
    int rem1 = 0;

    // Stores count of array elements whose
    // remainder is 2 by taking modulo by 3
    int rem2 = 0;

    // Traverse the array
    for(int i : arr)
    {

      // Stores sum of digits
      // of arr[i]
      int digitSum = 0;

      // Update digitSum
      digitSum += i;

      // If remainder of digitSum by
      // by taking modulo 3 is 0
      if(digitSum % 3 == 0)
      {

        // Update rem0
        rem0 += 1;
      }

      // If remainder of digitSum by
      // by taking modulo 3 is 1
      else if(digitSum % 3 == 1)
      {

        // Update rem1
        rem1 += 1;
      }
      else
      {

        // Update rem2
        rem2 += 1;
      }
    }

    return (rem0 / 2 + Math.min(rem1, rem2));
  }

  // Driver code
  public static void main(String[] args) {
    int[] arr = {5, 3, 2, 8, 7};

    // To display the result
    System.out.println(countDiv(arr));
  }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count pairs whose concatenation is
# divisible by 3 and each element can be present
# in at most one pair
def countDiv(arr):

    # Stores count of array elements whose
    # remainder is 0 by taking modulo by 3
    rem0 = 0

    # Stores count of array elements whose
    # remainder is 1 by taking modulo by 3
    rem1 = 0

    # Stores count of array elements whose
    # remainder is 2 by taking modulo by 3
    rem2 = 0

    # Traverse the array
    for i in arr:

       # Stores sum of digits
       # of arr[i]
        digitSum = 0

        for digit in str(i):

            # Update digitSum
            digitSum += int(digit)

        # If remainder of digitSum by
        # by taking modulo 3 is 0
        if digitSum % 3 == 0:

            # Update rem0
            rem0 += 1

        # If remainder of digitSum by
        # by taking modulo 3 is 1
        elif digitSum % 3 == 1:

            # Update rem1
            rem1 += 1
        else:

            # Update rem2
            rem2 += 1

    return (rem0 // 2 + min(rem1, rem2))

# Driver Code
arr = [5, 3, 2, 8, 7]

# To display the result
print(countDiv(arr))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to count pairs whose concatenation is
  // divisible by 3 and each element can be present
  // in at most one pair
  static int countDiv(int[] arr)
  {

    // Stores count of array elements whose
    // remainder is 0 by taking modulo by 3
    int rem0 = 0;

    // Stores count of array elements whose
    // remainder is 1 by taking modulo by 3
    int rem1 = 0;

    // Stores count of array elements whose
    // remainder is 2 by taking modulo by 3
    int rem2 = 0;

    // Traverse the array
    foreach(int i in arr)
    {

      // Stores sum of digits
      // of arr[i]
      int digitSum = 0;

      // Update digitSum
      digitSum += i;

      // If remainder of digitSum by
      // by taking modulo 3 is 0
      if(digitSum % 3 == 0)
      {

        // Update rem0
        rem0 += 1;
      }

      // If remainder of digitSum by
      // by taking modulo 3 is 1
      else if(digitSum % 3 == 1)
      {

        // Update rem1
        rem1 += 1;
      }
      else
      {

        // Update rem2
        rem2 += 1;
      }
    }

    return (rem0 / 2 + Math.Min(rem1, rem2));
  }

  // Driver code
  static void Main() {
    int[] arr = {5, 3, 2, 8, 7};

    // To display the result
    Console.Write(countDiv(arr));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to count pairs
    // whose concatenation is
    // divisible by 3 and each
    // element can be present
    // in at most one pair
    function countDiv(arr)
    {

      // Stores count of array elements whose
      // remainder is 0 by taking modulo by 3
      let rem0 = 0;

      // Stores count of array elements whose
      // remainder is 1 by taking modulo by 3
      let rem1 = 0;

      // Stores count of array elements whose
      // remainder is 2 by taking modulo by 3
      let rem2 = 0;

      // Traverse the array
      for(let i = 0; i < arr.length; i++)
      {

        // Stores sum of digits
        // of arr[i]
        let digitSum = 0;

        // Update digitSum
        digitSum += arr[i];

        // If remainder of digitSum by
        // by taking modulo 3 is 0
        if(digitSum % 3 == 0)
        {

          // Update rem0
          rem0 += 1;
        }

        // If remainder of digitSum by
        // by taking modulo 3 is 1
        else if(digitSum % 3 == 1)
        {

          // Update rem1
          rem1 += 1;
        }
        else
        {

          // Update rem2
          rem2 += 1;
        }
      }

      return (parseInt(rem0 / 2, 10) +
      Math.min(rem1, rem2));
    }

    let arr = [5, 3, 2, 8, 7];

    // To display the result
    document.write(countDiv(arr));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O()