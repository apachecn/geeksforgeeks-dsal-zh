# 通过向左移动数组元素的数字对数组进行排序

> 原文:[https://www . geeksforgeeks . org/按数组元素的左移位数字对数组进行排序/](https://www.geeksforgeeks.org/sort-an-array-by-left-shifting-digits-of-array-elements/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是左移数组元素的数字，使数组修改为排序形式。如果存在多个解决方案，则打印其中任何一个。否则，打印 **-1** 。

**示例:**

> **输入:** arr[] = { 511，321，323，432 }
> **输出:** { 115，132，233，243 }
> **解释:**
> 将 arr[0]的数字左移 1 将 arr[0]修改为 115。
> 将 arr[1]的数字左移 2 将 arr[1]修改为 132
> 将 arr[2]的数字左移 1 将 arr[2]修改为 233
> 将 arr[3]的数字左移 1 将 arr[3]修改为 243
> 
> **输入:** { 5，1，2，3，3 }
> **输出:** -1

**方法:**按照以下步骤解决问题:

1.  其思想是将每个数组元素的数字左移，使当前元素成为前一个数组元素中最近的较大元素。
2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并以所有可能的方式移动数组元素的位数，选择最小但大于前一个数组元素的那个。如果找不到这样的元素，那么打印 **-1** 。
3.  否则，在执行上述操作后打印数组元素

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if an array is
// sorted in increasing order or not
bool isIncreasing(vector<int> arr)
{

    // Traverse the array
    for(int i = 0; i < arr.size() - 1; i++)
    {
        if (arr[i] > arr[i + 1])
            return false;
    }
    return true;
}

// Function to sort the array
// by left shifting digits of
// array elements
vector<int> sortArr(vector<int> arr)
{

    // Stores previous array
    // element
    int prev = -1;

    // Traverse the array arr[]
    for(int i = 0; i < arr.size(); i++)
    {

        // Stores current element
        int optEle = arr[i];

        // Stores current element
        // in string format
        string strEle = to_string(arr[i]);

        // Left-shift digits of current
        // element in all possible ways
        for(int idx = 0; idx < strEle.size(); idx++)
        {

            // Left-shift digits of current
            // element by idx
            string strEle2 = strEle.substr(idx) +
                             strEle.substr(0, idx);
            int temp = stoi(strEle2);

            // If temp greater than or equal to
            // prev and temp less than optEle
            if (temp >= prev && temp < optEle)
                optEle = temp;
        }

        // Update arr[i]
        arr[i] = optEle;

        // Update prev
        prev = arr[i];
    }

    // If arr is in increasing order
    if (isIncreasing(arr))
        return arr;

    // Otherwise
    else
    {
        arr = { -1 };
        return arr;
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 511, 321, 323, 432, 433 };
    vector<int> res = sortArr(arr);

    for(int i = 0; i < res.size(); i++)
        cout << res[i] << " ";

    return 0;
}

// This code is contributed by subhammahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to check if an array is
// sorted in increasing order or not
static boolean isIncreasing(int []arr)
{

    // Traverse the array
    for(int i = 0; i < arr.length - 1; i++)
    {
        if (arr[i] > arr[i + 1])
            return false;
    }
    return true;
}

// Function to sort the array
// by left shifting digits of
// array elements
static int[] sortArr(int []arr)
{

    // Stores previous array
    // element
    int prev = -1;

    // Traverse the array arr[]
    for(int i = 0; i < arr.length; i++)
    {

        // Stores current element
        int optEle = arr[i];

        // Stores current element
        // in String format
        String strEle = String.valueOf(arr[i]);

        // Left-shift digits of current
        // element in all possible ways
        for(int idx = 0; idx < strEle.length(); idx++)
        {

            // Left-shift digits of current
            // element by idx
            String strEle2 = strEle.substring(idx) +
                             strEle.substring(0, idx);
            int temp = Integer.valueOf(strEle2);

            // If temp greater than or equal to
            // prev and temp less than optEle
            if (temp >= prev && temp < optEle)
                optEle = temp;
        }

        // Update arr[i]
        arr[i] = optEle;

        // Update prev
        prev = arr[i];
    }

    // If arr is in increasing order
    if (isIncreasing(arr))
        return arr;

    // Otherwise
    else
    {
        return new int[]{ -1 };
    }
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 511, 321, 323, 432, 433 };
    int []res = sortArr(arr);  
    for(int i = 0; i < res.length; i++)
        System.out.print(res[i]+ " ");  
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if an array is
# sorted in increasing order or not
def isIncreasing(arr):

    # Traverse the array
    for i in range(len(arr)-1):
        if arr[i] > arr[i + 1]:
            return False
    return True

# Function to sort the array
# by left shifting digits of
# array elements
def sortArr(arr):

    # Stores previous array
    # element
    prev = -1

    # Traverse the array arr[]
    for i in range(len(arr)):

        # Stores current element
        optEle = arr[i]

        # Stores current element
        # in string format
        strEle = str(arr[i])

        # Left-shift digits of current
        # element in all possible ways
        for idx in range(len(strEle)):

            # Left-shift digits of current
            # element by idx
            temp = int(strEle[idx:] + strEle[:idx])

            # If temp greater than or equal to
            # prev and temp less than optEle
            if temp >= prev and temp < optEle:
                optEle = temp

        # Update arr[i]
        arr[i] = optEle

        # Update prev
        prev = arr[i]

    # If arr is in increasing order
    if isIncreasing(arr):
        return arr

    # Otherwise
    else:
        return "-1"

# Driver Code
if __name__ == '__main__':

    arr = [511, 321, 323, 432, 433]
    res = sortArr(arr)

    for i in res:
        print(i, end = " ")
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to check if an array is
  // sorted in increasing order or not
  static bool isIncreasing(int []arr)
  {

    // Traverse the array
    for(int i = 0; i < arr.Length - 1; i++)
    {
      if (arr[i] > arr[i + 1])
        return false;
    }
    return true;
  }

  // Function to sort the array
  // by left shifting digits of
  // array elements
  static int[] sortArr(int []arr)
  {

    // Stores previous array
    // element
    int prev = -1;

    // Traverse the array []arr
    for(int i = 0; i < arr.Length; i++)
    {

      // Stores current element
      int optEle = arr[i];

      // Stores current element
      // in String format
      String strEle = String.Join("",arr[i]);

      // Left-shift digits of current
      // element in all possible ways
      for(int idx = 0; idx < strEle.Length; idx++)
      {

        // Left-shift digits of current
        // element by idx
        String strEle2 = strEle.Substring(idx) +
          strEle.Substring(0, idx);
        int temp = Int32.Parse(strEle2);

        // If temp greater than or equal to
        // prev and temp less than optEle
        if (temp >= prev && temp < optEle)
          optEle = temp;
      }

      // Update arr[i]
      arr[i] = optEle;

      // Update prev
      prev = arr[i];
    }

    // If arr is in increasing order
    if (isIncreasing(arr))
      return arr;

    // Otherwise
    else
    {
      return new int[]{ -1 };
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 511, 321, 323, 432, 433 };
    int []res = sortArr(arr);  
    for(int i = 0; i < res.Length; i++)
      Console.Write(res[i]+ " ");  
  }
}

// This code is contributed by shikhasingrajput.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to check if an array is
    // sorted in increasing order or not
    function isIncreasing(arr)
    {

        // Traverse the array
        for(let i = 0; i < arr.length - 1; i++)
        {
            if (arr[i] > arr[i + 1])
                return false;
        }
        return true;
    }

    // Function to sort the array
    // by left shifting digits of
    // array elements
    function sortArr(arr)
    {

        // Stores previous array
        // element
        let prev = -1;

        // Traverse the array arr[]
        for(let i = 0; i < arr.length; i++)
        {

            // Stores current element
            let optEle = arr[i];

            // Stores current element
            // in string format
            let strEle = arr[i].toString();

            // Left-shift digits of current
            // element in all possible ways
            for(let idx = 0; idx < strEle.length; idx++)
            {

                // Left-shift digits of current
                // element by idx
                let strEle2 = strEle.substr(idx) +
                                 strEle.substr(0, idx);
                let temp = parseInt(strEle2);

                // If temp greater than or equal to
                // prev and temp less than optEle
                if (temp >= prev && temp < optEle)
                    optEle = temp;
            }

            // Update arr[i]
            arr[i] = optEle;

            // Update prev
            prev = arr[i];
        }

        // If arr is in increasing order
        if (isIncreasing(arr))
            return arr;

        // Otherwise
        else
        {
            arr = [ -1 ];
            return arr;
        }
    }

    let arr = [ 511, 321, 323, 432, 433 ];
    let res = sortArr(arr);

    for(let i = 0; i < res.length; i++)
        document.write(res[i] + " ");

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
115 132 233 243 334
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)