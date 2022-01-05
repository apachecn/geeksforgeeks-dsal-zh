# 从数组中移除一个数字，使其成为几何级数

> 原文:[https://www . geesforgeks . org/remove-number-array-make-geometric-progression/](https://www.geeksforgeeks.org/remove-number-array-make-geometric-progression/)

给定一个由 N 个正元素组成的数组 arr[]，任务是通过最多移除一个元素来确定是否有可能将该数组转换为几何图形 T2。如果是，则找到将数组转换为几何级数的移除数的索引。
特例:
1)如果整个数组已经在 GP 中，那么返回任意索引。
2)如果无法将数组转换为 GP，则打印“不可能”。

**示例:**

```
Input  : arr[] = [2, 4, 8, 24, 16, 32]
Output : 3
Number to remove is arr[3], i.e., 24
After removing 24 array will be [2, 4, 8, 16, 32] which 
is a GP with starting value 2 and common ratio 2.

Input  : arr[] = [2, 8, 30, 60]
Output : Not Possible

```

我们可以通过处理一些特殊情况，然后找到枢轴元素来解决这个问题，去掉枢轴元素使数组成为一个 GP。首先，我们将检查我们的枢轴元素是第一个还是第二个元素，如果不是，那么它们之间的乘数将是我们的 GP 的公共比率，如果是，那么我们找到了我们的解决方案。
一旦我们得到 GP 的公比，我们就可以用这个比值来检查数组元素，如果这个比值在某个索引处违反，那么我们就跳过这个元素，从下一个索引开始检查它是否是上一个 GP 的延续。
在下面的代码中，实现了一个 isGP 方法，该方法在删除索引' index '处的元素后，检查数组是否为 GP。这个方法是为第一个、第二个和最后一个元素的特殊情况处理而编写的。

请参见下面的代码，以便更好地理解。

## C++

```
// C++ program to find the element removing which
// complete array becomes a GP
#include <bits/stdc++.h>
using namespace std;
#define EPS 1e-6

//  Utitilty method to compare two double values
bool fEqual(double a, double b)
{
    return (abs(a - b) < EPS);
}

//  Utility method to check, after deleting arr[ignore],
//  remaining array is GP or not
bool isGP(double arr[], int N, int ignore)
{
    double last = -1;
    double ratio = -1;

    for (int i = 0; i < N; i++)
    {
        //  check ratio only if i is not ignore
        if (i != ignore)
        {
            //  last will be -1 first time
            if (last != -1)
            {
                //  ratio will be -1 at first time
                if (ratio == -1)
                    ratio = (double)arr[i] / last;

                //  if ratio is not constant return false
                else if (!fEqual(ratio, (double)arr[i] / last))
                    return false;
            }
            last = arr[i];
        }
    }
    return true;
}

//  method return value removing which array becomes GP
int makeGPbyRemovingOneElement(double arr[], int N)
{
    /*  solving special cases separately */
    //  Try removing first element
    if (isGP(arr, N, 0))
        return 0;

    //  Try removing second element
    if (isGP(arr, N, 1))
        return 1;

    //  Try removing last element
    if (isGP(arr, N, N-1))
        return (N-1);

    /*  now we know that first and second element will be
        part of our GP so getting constant ratio of our GP */
    double ratio = (double)arr[1]/arr[0];
    for (int i = 2; i < N; i++)
    {
        if (!fEqual(ratio, (double)arr[i]/arr[i-1]))
        {
             /* At this point, we know that elements from arr[0]
               to arr[i-1] are in GP. So arr[i] is the element
               removing which may make GP.  We check if removing
               arr[i] actually makes it GP or not. */
            return (isGP(arr+i-2, N-i+2, 2))? i : -1;
         }
    }

    return -1;
}

//  Driver code to test above method
int main()
{
    double arr[] = {2, 4, 8, 30, 16};
    int N = sizeof(arr) / sizeof(arr[0]);

    int index = makeGPbyRemovingOneElement(arr, N);
    if (index == -1)
        cout << "Not possible\n";
    else
        cout << "Remove " << arr[index]
             << " to get geometric progression\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element removing which
// complete array becomes a GP
import java.util.*;

class GFG {

    final static double EPS = (double) 1e-6;

    // Utitilty method to compare two double values
    static boolean fEqual(double a, double b) {
        return (Math.abs(a - b) < EPS);
    }

    // Utility method to check, after deleting arr[ignore],
    // remaining array is GP or not
    static boolean isGP(double[] arr, int N, int ignore) {
        double last = -1;
        double ratio = -1;

        for (int i = 0; i < N; i++) {

            // check ratio only if i is not ignore
            if (i != ignore) {

                // last will be -1 first time
                if (last != -1) {

                    // ratio will be -1 at first time
                    if (ratio == -1)
                        ratio = (double) arr[i] / last;

                    // if ratio is not constant return false
                    else if (!fEqual(ratio, (double) arr[i] / last))
                        return false;
                }
                last = arr[i];
            }
        }
        return true;
    }

    // method return value removing which array becomes GP
    static int makeGPbyRemovingOneElement(double[] arr, int N) {

        /* solving special cases separately */
        // Try removing first element
        if (isGP(arr, N, 0))
            return 0;

        // Try removing second element
        if (isGP(arr, N, 1))
            return 1;

        // Try removing last element
        if (isGP(arr, N, N - 1))
            return (N - 1);

        /*
        * now we know that first and second element will be
        * part of our GP so getting constant ratio of our GP
        */
        double ratio = (double) arr[1] / arr[0];
        for (int i = 2; i < N; i++) {
            if (!fEqual(ratio, (double) arr[i] / arr[i - 1])) {
                /*
                * At this podouble, we know that elements from arr[0]
                * to arr[i-1] are in GP. Soarr[i] is the element
                * removing which may make GP. We check if removing
                * arr[i] actually makes it GP or not.
                */
                double[] temp = new double[N - i + 2];
                int k = 0;
                for (int j = i - 2; j < N; j++) {
                    temp[k++] = arr[j];
                }
                return (isGP(temp, N - i + 2, 2)) ? i : -1;
            }
        }

        return -1;
    }

    // Driver Code
    public static void main(String[] args) {

        double arr[] = { 2, 4, 8, 30, 16 };
        int N = arr.length;

        int index = makeGPbyRemovingOneElement(arr, N);
        if (index == -1)
            System.out.println("Not possible");
        else
            System.out.println("Remove " + arr[index] +
                        " to get geometric progression");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python program to find the element removing which
# complete array becomes a GP

EPS = 1e-7

# Utitilty method to compare two double values
def fEqual(a, b):
    return abs(a - b) < EPS

# Utility method to check, after deleting arr[ignore],
# remaining array is GP or not
def isGP(arr, N, ignore):
    last = -1
    ratio = -1

    for i in range(N):

        # check ratio only if i is not ignore
        if i != ignore:

            # last will be -1 first time
            if last != -1:

                # ratio will be -1 at first time
                if ratio == -1:
                    ratio = arr[i] / last

                    # if ratio is not constant return false
                elif not fEqual(ratio, arr[i] / last):
                    return False
            last = arr[i]

    return True

# Method return value removing which array becomes GP
def makeGPbyRemovingOneElement(arr, N):

    # Solving special cases separately
    # Try removing first element
    if isGP(arr, N, 0):
        return 0

    # Try removing second element
    if isGP(arr, N, 1):
        return 1

    # Try removing last element
    if isGP(arr, N, N - 1):
        return N - 1

    # now we know that first and second element will be
    # part of our GP so getting constant ratio of our GP
    ratio = arr[1] / arr[0]

    for i in range(2, N):
        if not fEqual(ratio, arr[i] / arr[i - 1]):

            # At this point, we know that elements from arr[0]
            # to arr[i-1] are in GP. So arr[i] is the element
            # removing which may make GP. We check if removing
            # arr[i] actually makes it GP or not.
            return i if isGP(arr[i - 2:], N - i + 2, 2) else -1

    return -1

# Driver Code
if __name__ == "__main__":
    arr = [2, 4, 8, 30, 16]
    N = len(arr)

    index = makeGPbyRemovingOneElement(arr, N)

    if index == -1:
        print("Not Possible")
    else:
        print("Remove %d to get geometric progression" % arr[index])

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find the element
// removing which complete array
// becomes a GP
using System;

class GFG{

static double EPS = (double)1e-6;

// Utitilty method to compare two
// double values
static bool fEqual(double a, double b)
{
    return (Math.Abs(a - b) < EPS);
}

// Utility method to check, after
// deleting arr[ignore], remaining
// array is GP or not
static bool isGP(double[] arr, int N,
                               int ignore)
{
    double last = -1;
    double ratio = -1;

    for(int i = 0; i < N; i++)
    {

        // Check ratio only if i is not ignore
        if (i != ignore)
        {

            // last will be -1 first time
            if (last != -1)
            {

                // ratio will be -1 at first time
                if (ratio == -1)
                    ratio = (double)arr[i] / last;

                // If ratio is not constant return false
                else if (!fEqual(ratio,
                        (double) arr[i] / last))
                    return false;
            }
            last = arr[i];
        }
    }
    return true;
}

// Method return value removing
// which array becomes GP
static int makeGPbyRemovingOneElement(double[] arr,
                                      int N)
{

    // Solving special cases separately
    // Try removing first element
    if (isGP(arr, N, 0))
        return 0;

    // Try removing second element
    if (isGP(arr, N, 1))
        return 1;

    // Try removing last element
    if (isGP(arr, N, N - 1))
        return (N - 1);

    // Now we know that first and second
    // element will be part of our GP so
    // getting constant ratio of our GP
    double ratio = (double) arr[1] / arr[0];

    for(int i = 2; i < N; i++)
    {
        if (!fEqual(ratio, (double)arr[i] /
                                   arr[i - 1]))
        {

            // At this podouble, we know that
            // elements from arr[0] to arr[i-1]
            // are in GP. Soarr[i] is the element
            // removing which may make GP. We check
            // if removing arr[i] actually makes
            // it GP or not.
            double[] temp = new double[N - i + 2];
            int k = 0;
            for(int j = i - 2; j < N; j++)
            {
                temp[k++] = arr[j];
            }
            return (isGP(temp, N - i + 2, 2)) ? i : -1;
        }
    }
    return -1;
}

// Driver Code
public static void Main(string[] args)
{

    double []arr = { 2, 4, 8, 30, 16 };
    int N = arr.Length;

    int index = makeGPbyRemovingOneElement(arr, N);
    if (index == -1)
        Console.Write("Not possible");
    else
        Console.Write("Remove " + arr[index] +
                      " to get geometric progression");
}
}

// This code is contributed by rutvik_56
```

**输出:**

```
Remove 30 to get geometric progression

```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。