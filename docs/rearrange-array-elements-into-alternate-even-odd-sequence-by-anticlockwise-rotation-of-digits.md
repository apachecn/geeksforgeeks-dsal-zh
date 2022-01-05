# 通过逆时针旋转数字

将数组元素重新排列成交替的奇偶序列

> 原文:[https://www . geeksforgeeks . org/重排-数组-元素-进入-交替-偶数-奇数-序列-逆时针-数字旋转/](https://www.geeksforgeeks.org/rearrange-array-elements-into-alternate-even-odd-sequence-by-anticlockwise-rotation-of-digits/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是[逆时针旋转数组元素的数字](https://www.geeksforgeeks.org/generate-all-rotations-of-a-number/)，使得[数组元素的元素呈交替的奇偶或奇偶形式](https://www.geeksforgeeks.org/rearrange-odd-and-even-values-in-alternate-fashion-in-ascending-order/)。如果存在多个解决方案，则打印其中任何一个。否则，打印 **-1** 。

**示例:**

> **输入:** arr[] = { 143，251，534，232，854 }
> **输出:** 143 512 345 232 485
> **解释:**
> 逆时针方向将 arr[1]旋转 1 将 arr[1]修改为 512。
> 逆时针方向将 arr[2]旋转 1 会将 arr[2]修改为 345°。
> 逆时针旋转 arr[4]2 将 arr[4]修改为 485。
> 
> **输入:** arr[] = { 44，23，21，33，14 }
> T3】输出: 44 23 12 33 14

**方法:**上述问题可以通过将第一个数组元素修改为奇数或偶数来解决。可以通过[将数字转换为字符串](https://www.geeksforgeeks.org/convert-integer-to-string-in-python/)然后[根据需要向左旋转字符串](https://www.geeksforgeeks.org/left-rotation-right-rotation-string-2/)的字符来修改数组元素。按照以下步骤解决问题:

*   将第一个数组元素重新排列为偶数，并检查剩余的数组元素是否可以交替重新排列为奇偶。如果发现为真，那么将数组元素重新排列成奇偶交替[打印数组元素](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/)。
*   否则，将第一个数组元素重新排列为奇数，并检查剩余的数组元素是否可以交替重新排列为奇偶。如果发现是真的，那么将剩余的数组元素重新排列成奇偶交替，并打印数组元素。
*   否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// c++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to rotate the digits of
// array elements such that array elements are
// in placed even-odd or odd-even alternately
bool is_possible(vector<int>& arr, bool check)
{

    // Checks if array can be converted
    // into even-odd or odd-even form
    bool exists = true;

    // Store array elements
    vector<int> cpy = arr;
    bool flag;
    // Traverse the array
    for (int i = 0; i < arr.size(); i++) {

        // Check if arr[i] is already
        // at correct position
        if (arr[i] % 2 == check) {
            check = !(check);
            continue;
        }

        // Checks if it is possible
        // to modify the number arr[i]
        // by rotating the digits of
        // the number anticlockwise
        flag = false;

        // Stores the number arr[i] as
        // string
        string strEle = to_string(arr[i]);

        // Traverse over the digits of
        // the current element
        for (int j = 0; j < strEle.size(); j++) {

            // Checks if parity of check and
            // current digit is same or not
            if (int(strEle[j]) % 2 == check) {

                // Rotates the string by j + 1 times
                // in anticlockwise
                arr[i] = stoi(strEle.substr(j + 1)
                              + strEle.substr(0, j + 1));

                // Marks the flag
                // as true and break
                flag = true;
                break;
            }
        }

        // If flag is false
        if (flag == false) {
            // Update exists
            exists = false;
            break;
        }

        // Changes the
        // parity of check
        check = !(check);
    }

    // Checks if arr[] cannot be
    // modified, then returns false
    if (!exists) {
        arr = cpy;
        return false;
    }

    // Otherwise, return true
    else
        return true;
}

// Function to rotate the digits of array
// elements such that array elements are
// in the form of even-odd or odd-even form
void convert_arr(vector<int>& arr)
{

    // If array elements can be arranged
    // in even-odd manner alternately
    if (is_possible(arr, 0)) {
        for (auto& i : arr)
            cout << i << " ";
    }

    // If array elements can be arranged
    // in odd-even manner alternately
    else if (is_possible(arr, 1)) {
        for (auto& i : arr)
            cout << i << " ";
    }

    // Otherwise, prints -1
    else
        cout << "-1" << endl;
}

// Driver Code
int main()
{

    vector<int> arr = { 143, 251, 534, 232, 854 };
    convert_arr(arr);
}

// This code is contributed by grand_master.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Utility function to rotate the digits of
  // array elements such that array elements are
  // in placed even-odd or odd-even alternately
  static boolean is_possible(int arr[], int check)
  {

    // Checks if array can be converted
    // into even-odd or odd-even form
    boolean exists = true;

    // Store array elements
    int cpy[] = arr.clone();
    boolean flag;
    // Traverse the array
    for (int i = 0; i < arr.length; i++) {

      // Check if arr[i] is already
      // at correct position
      if (arr[i] % 2 == check) {
        // Changes the
        // parity of check
        check = (check == 0 ? 1 : 0);
        continue;
      }

      // Checks if it is possible
      // to modify the number arr[i]
      // by rotating the digits of
      // the number anticlockwise
      flag = false;

      // Stores the number arr[i] as
      // string
      String strEle = Integer.toString(arr[i]);

      // Traverse over the digits of
      // the current element
      for (int j = 0; j < strEle.length(); j++) {

        // Checks if parity of check and
        // current digit is same or not
        if ((strEle.charAt(j) - '0') % 2 == check) {

          // Rotates the string by j + 1 times
          // in anticlockwise
          arr[i] = Integer.parseInt(
            strEle.substring(j + 1)
            + strEle.substring(0, j + 1));

          // Marks the flag
          // as true and break
          flag = true;
          break;
        }
      }

      // If flag is false
      if (flag == false) {
        // Update exists
        exists = false;
        break;
      }

      // Changes the
      // parity of check
      check = (check == 0 ? 1 : 0);
    }

    // Checks if arr[] cannot be
    // modified, then returns false
    if (!exists) {
      arr = cpy;
      return false;
    }

    // Otherwise, return true
    else
      return true;
  }

  // Function to rotate the digits of array
  // elements such that array elements are
  // in the form of even-odd or odd-even form
  static void convert_arr(int arr[])
  {

    // If array elements can be arranged
    // in even-odd manner alternately
    if (is_possible(arr, 0)) {
      for (int v : arr) {
        System.out.print(v + " ");
      }
    }

    // If array elements can be arranged
    // in odd-even manner alternately
    else if (is_possible(arr, 1)) {
      for (int v : arr) {
        System.out.print(v + " ");
      }
    }

    // Otherwise, prints -1
    else
      System.out.println(-1);
  }

  // Driver code
  public static void main(String[] args)
  {
    // Given array
    int arr[] = { 143, 251, 534, 232, 854 };

    // FUnction call
    convert_arr(arr);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python program of the above approach

# Utility function to rotate the digits of
# array elements such that array elements are
# in placed even-odd or odd-even alternately
def is_possible(arr, check):

    # Checks if array can be converted
    # into even-odd or odd-even form
    exists = True

    # Store array elements
    cpy = arr

    # Traverse the array
    for i in range(len(arr)):

        # Check if arr[i] is already
        # at correct position
        if (arr[i] % 2 == check):
            check = not(check)
            continue

        # Checks if it is possible
        # to modify the number arr[i]
        # by rotating the digits of
        # the number anticlockwise
        flag = False

        # Stores the number arr[i] as
        # string
        strEle = str(arr[i])

        # Traverse over the digits of
        # the current element
        for j in range(len(strEle)):

            # Checks if parity of check and
            # current digit is same or not
            if int(strEle[j]) % 2 == check:

                # Rotates the string by j + 1 times
                # in anticlockwise
                arr[i] = int(strEle[j + 1:] + strEle[:j + 1])

                # Marks the flag
                # as true and break
                flag = True
                break

        # If flag is false
        if flag == False:

            # Update exists
            exists = False
            break

        # Changes the
        # parity of check
        check = not(check)

    # Checks if arr[] cannot be
    # modified, then returns false
    if not exists:
        arr = cpy
        return False

    # Otherwise, return True
    else:
        return True

# Function to rotate the digits of array
# elements such that array elements are
# in the form of even-odd or odd-even form
def convert_arr(arr):

    # If array elements can be arranged
    # in even-odd manner alternately
    if(is_possible(arr, 0)):
        print(*arr)

    # If array elements can be arranged
    # in odd-even manner alternately
    elif(is_possible(arr, 1)):
        print(*arr)

    # Otherwise, prints -1
    else:
        print(-1)

# Driver Code
if __name__ == '__main__':

    arr = [143, 251, 534, 232, 854]
    convert_arr(arr)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Utility function to rotate the digits of
// array elements such that array elements are
// in placed even-odd or odd-even alternately
static bool ispossible(List<int> arr, bool check)
{

    // Checks if array can be converted
    // into even-odd or odd-even form
    bool exists = true;

    // Store array elements
    List<int> cpy = arr;
    bool flag;
    // Traverse the array
    for (int i=0;i<arr.Count;i++) {

        // Check if arr[i] is already
        // at correct position
        int temp = check ? 1 : 0;
        if (arr[i] % 2 == temp) {
            check = !(check);
            continue;
        }

        // Checks if it is possible
        // to modify the number arr[i]
        // by rotating the digits of
        // the number anticlockwise
        flag = false;

        // Stores the number arr[i] as
        // string
        int p = arr[i];
        string strEle = p.ToString();

        // Traverse over the digits of
        // the current element
        for (int j = 0; j < strEle.Length; j++) {

            // Checks if parity of check and
            // current digit is same or not
             temp = check ? 1 : 0;
            if ((int)(strEle[j] - '0')% 2 == temp) {

                // Rotates the string by j + 1 times
                // in anticlockwise
                string s  = strEle.Substring(j + 1) + strEle.Substring(0, j + 1);
                arr[i] = Int32.Parse(s);

                // Marks the flag
                // as true and break
                flag = true;
                break;
            }
        }

        // If flag is false
        if (flag == false) {
            // Update exists
            exists = false;
            break;
        }

        // Changes the
        // parity of check
        check = !(check);
    }

    // Checks if arr[] cannot be
    // modified, then returns false
    if (exists==false) {
        arr = cpy;
        return false;
    }

    // Otherwise, return true
    else
        return true;
}

// Function to rotate the digits of array
// elements such that array elements are
// in the form of even-odd or odd-even form
static void convert_arr(List<int> arr)
{

    // If array elements can be arranged
    // in even-odd manner alternately
    if (ispossible(arr, false)) {
        foreach (int i in arr)
            Console.Write(i +" ");
    }

    // If array elements can be arranged
    // in odd-even manner alternately
    else if (ispossible(arr, true)) {
        foreach (int i in arr)
           Console.Write(i + " ");
    }

    // Otherwise, prints -1
    else
        Console.Write("-1");
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){143, 251, 534, 232, 854};
    convert_arr(arr);
}
}
```

## java 描述语言

```
<script>

    // JavaScript program of the above approach

    // Utility function to rotate the digits of
    // array elements such that array elements are
    // in placed even-odd or odd-even alternately
    function is_possible(arr,check)
    {

        // Checks if array can be converted
        // into even-odd or odd-even form
        let exists = true;

        // Store array elements
        let cpy = arr;
          let flag;
        // Traverse the array
        for (let i = 0; i < arr.length; i++) {

            // Check if arr[i] is already
            // at correct position
            if (arr[i] % 2 == check) {
                check = !(check);
                continue;
            }

            // Checks if it is possible
            // to modify the number arr[i]
            // by rotating the digits of
            // the number anticlockwise
            flag = false;

            // Stores the number arr[i] as
            // string
            let strEle = arr[i].toString();

            // Traverse over the digits of
            // the current element
            for (let j = 0; j < strEle.length; j++) {

                // Checks if parity of check and
                // current digit is same or not
                if (strEle[j].charCodeAt() % 2 == check) {

                    // Rotates the string by j + 1 times
                    // in anticlockwise
                    arr[i] = parseInt(strEle.substr(j + 1)
                                + strEle.substr(0, j + 1));

                    // Marks the flag
                    // as true and break
                    flag = true;
                    break;
                }
            }

            // If flag is false
            if (flag == false) {
                // Update exists
                exists = false;
                break;
            }

            // Changes the
            // parity of check
            check = !(check);
        }

        // Checks if arr[] cannot be
        // modified, then returns false
        if (!exists) {
            arr = cpy;
            return false;
        }

        // Otherwise, return true
        else
            return true;
    }

    // Function to rotate the digits of array
    // elements such that array elements are
    // in the form of even-odd or odd-even form
    function convert_arr(arr)
    {

        // If array elements can be arranged
        // in even-odd manner alternately
        if (is_possible(arr, 0)) {
            for (let i = 0; i < arr.length; i++)
                document.write(arr[i] + " ");
        }

        // If array elements can be arranged
        // in odd-even manner alternately
        else if (is_possible(arr, 1)) {
            for (let i = 0; i < arr.length; i++)
                document.write(arr[i] + " ");
        }

        // Otherwise, prints -1
        else
          document.write("-1");
    }

    // Driver Code

    let arr = [ 143, 251, 534, 232, 854 ];
    convert_arr(arr);

</script>
```

**Output:** 

```
314 251 534 223 854
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)