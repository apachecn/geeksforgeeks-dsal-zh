# 检查(I，j)是否存在，使得 arr[i]！= arr[j]，arr[arr[i]]等于 arr[arr[j]]

> 原文:[https://www . geeksforgeeks . org/check-if-ij-exists-so-arri-arrj-and-arr RRI-等于-arr rrj/](https://www.geeksforgeeks.org/check-whether-ij-exists-such-that-arri-arrj-and-arrarri-is-equal-to-arrarrj/)

给定数组 A[]。任务是确定是否有可能选择两个指数**‘I’**和**‘j’**，从而满足以下条件:-

> 1.  **A [I]** is not equal to **A [J]** .
> 2.  **A[A[i]]** 等于 **A[A[j]]** 。

**注意:**数组中元素的值小于 N 的值，即每 I，arr[i] < N.
**示例:**

```
Input: N = 4, A[] = {1, 1, 2, 3}
Output: Yes
As A[3] != to A[1] but A[A[3]] == A[A[1]]

Input: N = 4, A[] = {2, 1, 3, 3}
Output: No
As A[A[3]] == A[A[4]] but A[3] == A[4]
```

**进场:**

1.  通过运行两个循环开始遍历 arr[]数组。
2.  变量 **i** 指向指数 0，变量 **j** 指向下一个 I
3.  如果 Arr[i]不等于 Arr[j]，则检查 Arr[Arr[I]–1]是否等于 Arr[Arr[j]–1]。如果是，则返回真。
    否则也检查其他索引的 Arr[Arr[i]- 1]和 Arr[Arr[j]–1]。
4.  重复以上步骤，直到遍历完所有元素/索引。
5.  如果没有发现这样的指数，返回假。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that will tell whether
// such Indices present or Not.
bool checkIndices(int Arr[], int N)
{

    for (int i = 0; i < N - 1; i++) {
        for (int j = i + 1; j < N; j++) {

            // Checking 1st condition i.e whether
            // Arr[i] equal to Arr[j] or not
            if (Arr[i] != Arr[j]) {

                // Checking 2nd condition i.e whether
                // Arr[Arr[i]] equal to Arr[Arr[j]] or not.
                if (Arr[Arr[i] - 1] == Arr[Arr[j] - 1])
                    return true;
            }
        }
    }

    return false;
}

// Driver Code
int main()
{
    int Arr[] = { 3, 2, 1, 1, 4 };
    int N = sizeof(Arr) / sizeof(Arr[0]);

    // Calling function.
    checkIndices(Arr, N) ? cout << "Yes"
                         : cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

// Function that calculates marks.
class GFG
{
    static boolean checkIndices(int Arr[], int N)
    {

        for (int i = 0; i < N - 1; i++) {
            for (int j = i + 1; j < N; j++) {

                // Checking 1st condition i.e whether
                // Arr[i] equal to Arr[j] or not
                if (Arr[i] != Arr[j]) {

                    // Checking 2nd condition i.e whether
                    // Arr[Arr[i]] equal to Arr[Arr[j]] or not.
                    if (Arr[Arr[i] - 1] == Arr[Arr[j] - 1])
                        return true;
                }
            }
        }
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        int Arr[] = { 3, 2, 1, 1, 4 };
        int N = Arr.length;

        if(checkIndices(Arr, N))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is Contributed by
// Naman_Garg
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Function that will tell whether
# such Indices present or Not.
def checkIndices(Arr, N):

    for i in range(N - 1):
        for j in range(i + 1, N):

            # Checking 1st condition i.e whether
            # Arr[i] equal to Arr[j] or not
            if (Arr[i] != Arr[j]):

                # Checking 2nd condition i.e whether
                # Arr[Arr[i]] equal to Arr[Arr[j]] or not.
                if (Arr[Arr[i] - 1] == Arr[Arr[j] - 1]):
                    return True

    return False

# Driver Code
if __name__ == "__main__":

    Arr = [ 3, 2, 1, 1, 4 ]
    N =len(Arr)

    # Calling function.
    if checkIndices(Arr, N):
        print("Yes") 
    else:
        print("No")

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function that calculates marks.
static bool checkIndices(int []Arr, int N)
{
    for (int i = 0; i < N - 1; i++)
    {
        for (int j = i + 1; j < N; j++)
        {

            // Checking 1st condition i.e whether
            // Arr[i] equal to Arr[j] or not
            if (Arr[i] != Arr[j])
            {

                // Checking 2nd condition i.e
                // whether Arr[Arr[i]] equal
                // to Arr[Arr[j]] or not.
                if (Arr[Arr[i] - 1] == Arr[Arr[j] - 1])
                    return true;
            }
        }
    }
    return false;
}

// Driver code
static public void Main ()
{
    int []Arr = { 3, 2, 1, 1, 4 };
    int N = Arr.Length;

    if(checkIndices(Arr, N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is Contributed by Sachin
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function that will tell whether
// such Indices present or Not.
function checkIndices($Arr, $N)
{
    for ($i = 0; $i < $N - 1; $i++)
    {
        for ($j = $i + 1;
                  $j < $N; $j++)
        {

            // Checking 1st condition i.e
            // whether Arr[i] equal to
            // Arr[j] or not
            if ($Arr[$i] != $Arr[$j])
            {

                // Checking 2nd condition i.e
                // whether Arr[Arr[i]] equal to
                // Arr[Arr[j]] or not.
                if ($Arr[$Arr[$i] - 1] == $Arr[$Arr[$j] - 1])
                    return true;
            }
        }
    }

    return false;
}

// Driver Code
$Arr = array(3, 2, 1, 1, 4);
$N = sizeof($Arr);

// Calling function.
if(checkIndices($Arr, $N))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function that will tell whether
// such Indices present or Not.
function checkIndices(Arr, N)
{

    for (var i = 0; i < N - 1; i++) {
        for (var j = i + 1; j < N; j++) {

            // Checking 1st condition i.e whether
            // Arr[i] equal to Arr[j] or not
            if (Arr[i] != Arr[j]) {

                // Checking 2nd condition i.e whether
                // Arr[Arr[i]] equal to Arr[Arr[j]] or not.
                if (Arr[Arr[i] - 1] == Arr[Arr[j] - 1])
                    return true;
            }
        }
    }

    return false;
}

// Driver Code
var Arr = [ 3, 2, 1, 1, 4 ];
var N = Arr.length;

// Calling function.
checkIndices(Arr, N) ? document.write( "Yes")
                    : document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(1)