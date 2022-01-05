# 通过交换其中一个数组的对来检查两个数组是否相等

> 原文:[https://www . geeksforgeeks . org/check-if-two-arrays-可以通过交换阵列中的一对来使其相等/](https://www.geeksforgeeks.org/check-if-two-arrays-can-be-made-equal-by-swapping-pairs-of-one-of-the-arrays/)

给定两个大小相同的二进制[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr1[]** 和 **arr2[]** ，任务是仅当 **arr1[i] = 0** 和**arr 1[j]= 1**(*0≤I<j<N)*)时，通过交换成对的 **arr1[ ]** 来使两个数组相等。如果可以使两个阵列相等，打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr1[] = {0，0，1，1}，arr2[] = {1，1，0，0}
> **输出:**是
> **解释:**
> 交换 arr1[1]和 arr1[3]，变成 arr1[] = {0，1，1，0}。
> 交换 arr1[0]和 arr1[2]，变成 arr1[] = {1，1，0，0}。
> 
> **输入:** arr1[] = {1，0，1，0，1}，arr2[] = {0，1，0，0，1}
> **输出:**否

**方法:**按照以下步骤解决问题:

*   初始化两个变量，说**计数**和**标志** (= *真*)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并对每个数组元素执行以下操作:
    *   **如果 arr1[i]！= arr2[i]:**
        *   如果 **arr1[i] == 0** ，将**计数**增加 **1** 。
        *   否则，用 **1** 递减**计数**，如果**计数< 0** ，则更新**标志=假**。
*   如果**标志**等于**真**，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if two arrays
// can be made equal or not by swapping
// pairs of only one of the arrays
void checkArrays(int arr1[], int arr2[], int N)
{
    // Stores elements required
    // to be replaced
    int count = 0;

    // To check if the arrays
    // can be made equal or not
    bool flag = true;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If array elements are not equal
        if (arr1[i] != arr2[i]) {

            if (arr1[i] == 0)

                // Increment count by 1
                count++;
            else {

                // Decrement count by 1
                count--;
                if (count < 0) {
                    flag = 0;
                    break;
                }
            }
        }
    }

    // If flag is true and count is 0,
    // print "Yes". Otherwise "No"
    if (flag && count == 0)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// Driver Code
int main()
{
    // Given arrays
    int arr1[] = { 0, 0, 1, 1 };
    int arr2[] = { 1, 1, 0, 0 };

    // Size of the array
    int N = sizeof(arr1) / sizeof(arr1[0]);
    checkArrays(arr1, arr2, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
public class GFG
{

  // Function to check if two arrays
  // can be made equal or not by swapping
  // pairs of only one of the arrays
  static void checkArrays(int arr1[], int arr2[], int N)
  {

    // Stores elements required
    // to be replaced
    int count = 0;

    // To check if the arrays
    // can be made equal or not
    boolean flag = true;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // If array elements are not equal
      if (arr1[i] != arr2[i])
      {
        if (arr1[i] == 0)

          // Increment count by 1
          count++;
        else
        {

          // Decrement count by 1
          count--;
          if (count < 0)
          {
            flag = false;
            break;
          }
        }
      }
    }

    // If flag is true and count is 0,
    // print "Yes". Otherwise "No"
    if ((flag && (count == 0)) == true)
      System.out.println("Yes");
    else
      System.out.println("No");
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given arrays
    int arr1[] = { 0, 0, 1, 1 };
    int arr2[] = { 1, 1, 0, 0 };

    // Size of the array
    int N = arr1.length;  
    checkArrays(arr1, arr2, N);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to check if two arrays
# can be made equal or not by swapping
# pairs of only one of the arrays
def checkArrays(arr1, arr2, N):

    # Stores elements required
    # to be replaced
    count = 0

    # To check if the arrays
    # can be made equal or not
    flag = True

    # Traverse the array
    for i in range(N):

        # If array elements are not equal
        if (arr1[i] != arr2[i]):

            if (arr1[i] == 0):

                # Increment count by 1
                count += 1
            else:

                # Decrement count by 1
                count -= 1
                if (count < 0):
                    flag = 0
                    break

    # If flag is true and count is 0,
    # pr"Yes". Otherwise "No"
    if (flag and count == 0):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    # Given arrays
    arr1 = [0, 0, 1, 1]
    arr2 = [1, 1, 0, 0]

    # Size of the array
    N = len(arr1)

    checkArrays(arr1, arr2, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if two arrays
  // can be made equal or not by swapping
  // pairs of only one of the arrays
  static void checkArrays(int[] arr1, int[] arr2, int N)
  {

    // Stores elements required
    // to be replaced
    int count = 0;

    // To check if the arrays
    // can be made equal or not
    bool flag = true;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // If array elements are not equal
      if (arr1[i] != arr2[i])
      {
        if (arr1[i] == 0)

          // Increment count by 1
          count++;
        else
        {

          // Decrement count by 1
          count--;
          if (count < 0)
          {
            flag = false;
            break;
          }
        }
      }
    }

    // If flag is true and count is 0,
    // print "Yes". Otherwise "No"
    if ((flag && (count == 0)) == true)
      Console.WriteLine("Yes");
    else
      Console.WriteLine("No");
  }

// Driver Code
static public void Main()
{
    // Given arrays
    int[] arr1 = { 0, 0, 1, 1 };
    int[] arr2 = { 1, 1, 0, 0 };

    // Size of the array
    int N = arr1.Length;  
    checkArrays(arr1, arr2, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
// Java script program for above approach

// Function to check if two arrays
// can be made equal or not by swapping
// pairs of only one of the arrays
function checkArrays(arr1,arr2,N)
{

    // Stores elements required
    // to be replaced
    let count = 0;

    // To check if the arrays
    // can be made equal or not
    let flag = true;

    // Traverse the array
    for (let i = 0; i < N; i++) {

    // If array elements are not equal
    if (arr1[i] != arr2[i])
    {
        if (arr1[i] == 0)

        // Increment count by 1
        count++;
        else
        {

        // Decrement count by 1
        count--;
        if (count < 0)
        {
            flag = false;
            break;
        }
        }
    }
    }

    // If flag is true and count is 0,
    // print "Yes". Otherwise "No"
    if ((flag && (count == 0)) == true)
    document.write("Yes");
    else
    document.write("No");
}

// Driver Code

    // Given arrays
    let arr1 = [ 0, 0, 1, 1 ];
    let arr2 = [ 1, 1, 0, 0 ];

    // Size of the array
    let N = arr1.length;
    checkArrays(arr1, arr2, N);

// This code is contributed by Gottumukkala Sravan Kumar (171fa07058)
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)