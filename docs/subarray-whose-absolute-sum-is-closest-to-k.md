# 绝对和最接近 K 的子阵

> 原文:[https://www . geesforgeks . org/subarray-其绝对总和最接近-k/](https://www.geeksforgeeks.org/subarray-whose-absolute-sum-is-closest-to-k/)

给定 n 个元素和一个整数 K 的数组，任务是找到最小值为 **||a[i] + a[i + 1] + ……的子数组。a[j]|–K |**。换句话说，找到元素之和与 K 的偏差最小的邻接子阵列或绝对和最接近 K 的子阵列

**例**

> **输入:** : a[] = {1，3，7，10}，K = 15
> **输出:**子阵列{7，10}
> 相邻子阵列[7，10]显示与 15 的最小偏差为 2。
> 
> **输入:** a[] = {1，2，3，4，5，6}，K = 6
> **输出:**子阵列{1，2，3}
> 相邻的子阵列[1，2，3]显示与 6 的最小偏差为 0。

一种简单的方法是检查每个相邻子阵列的和及其与 k 的差

下面是上述方法的实现:

## C++

```
// C++ code to find sub-array whose
// sum shows the minimum deviation
#include <bits/stdc++.h>
using namespace std;

int* getSubArray(int arr[], int n, int K)
{
    int i = -1;
    int j = -1;
    int currSum = 0;

    // Starting index, ending index,
    // Deviation
    int* result = new int[3]{ i, j,
                              abs(K -
                              abs(currSum)) };

    // Iterate i and j to get all subarrays
    for(i = 0; i < n; i++)
    {
        currSum = 0;

        for(j = i; j < n; j++)
        {
            currSum += arr[j];
            int currDev = abs(K - abs(currSum));

            // Found sub-array with less sum
            if (currDev < result[2])
            {
                result[0] = i;
                result[1] = j;
                result[2] = currDev;
            }

            // Exactly same sum
            if (currDev == 0)
                return result;
        }
    }
    return result;
}

// Driver code  
int main()
{
    int arr[8] = { 15, -3, 5, 2, 7, 6, 34, -6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int K = 50;

    // Array to store return values
    int* ans = getSubArray(arr, n, K);

    if (ans[0] == -1)
    {
        cout << "The empty array shows "
             << "minimum Deviation";
    }
    else
    {
        for(int i = ans[0]; i <= ans[1]; i++)
            cout << arr[i] << " ";
    }
    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find sub-array whose
// sum shows the minimum deviation
class GFG{

public static int[] getSubArray(int[] arr,
                                int n,int K)
{
    int i = -1;
    int j = -1;
    int currSum = 0;

    // Starting index, ending index, Deviation
    int [] result = { i, j,
                      Math.abs(K -
                      Math.abs(currSum)) };

    // Iterate i and j to get all subarrays
    for(i = 0; i < n; i++)
    {
        currSum = 0;

        for(j = i; j < n; j++)
        {
            currSum += arr[j];
            int currDev = Math.abs(K -
                          Math.abs(currSum));

            // Found sub-array with less sum
            if(currDev < result[2])
            {
                result[0] = i;
                result[1] = j;
                result[2] = currDev;
            }

            // Exactly same sum
            if(currDev == 0)
                return result;
        }
    }
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 15, -3, 5, 2, 7, 6, 34, -6 };
    int n = arr.length;
    int K = 50;

    // Array to store return values
    int[] ans = getSubArray(arr, n, K);

    if(ans[0] == -1)
    {
        System.out.println("The empty array " +
                           "shows minimum Deviation");
    }
    else
    {
        for(int i = ans[0]; i <= ans[1]; i++)
            System.out.print(arr[i] + " ");
    }
}
}

// This code is contributed by dadimadhav
```

## 计算机编程语言

```
# Python Code to find sub-array whose
# sum shows the minimum deviation

def getSubArray(arr, n, K):
    i = -1
    j = -1
    currSum = 0
    # starting index, ending index, Deviation
    result = [i, j, abs(K-abs(currSum))]

    # iterate i and j to get all subarrays
    for i in range(0, n):

        currSum = 0

        for j in range(i, n):
            currSum += arr[j]
            currDev = abs(K-abs(currSum))

            # found sub-array with less sum
            if (currDev < result[2]):
                result = [i, j, currDev]

            # exactly same sum
            if (currDev == 0):
                return result
    return result

# Driver Code
def main():
    arr = [15, -3, 5, 2, 7, 6, 34, -6]

    n = len(arr)

    K = 50

    [i, j, minDev] = getSubArray(arr, n, K)

    if(i ==-1):
        print("The empty array shows minimum Deviation")
        return 0

    for i in range(i, j + 1):
        print arr[i],

main()
```

## C#

```
// C# code to find sub-array whose
// sum shows the minimum deviation
using System;

class GFG{

public static int[] getSubArray(int[] arr,
                                int n, int K)
{
    int i = -1;
    int j = -1;
    int currSum = 0;

    // Starting index, ending index, Deviation
    int [] result = { i, j,
                      Math.Abs(K -
                      Math.Abs(currSum)) };

    // Iterate i and j to get all subarrays
    for(i = 0; i < n; i++)
    {
        currSum = 0;

        for(j = i; j < n; j++)
        {
            currSum += arr[j];
            int currDev = Math.Abs(K -
                          Math.Abs(currSum));

            // Found sub-array with less sum
            if (currDev < result[2])
            {
                result[0] = i;
                result[1] = j;
                result[2] = currDev;
            }

            // Exactly same sum
            if (currDev == 0)
                return result;
        }
    }
    return result;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 15, -3, 5, 2, 7, 6, 34, -6 };
    int n = arr.Length;
    int K = 50;

    // Array to store return values
    int[] ans = getSubArray(arr, n, K);

    if (ans[0] == -1)
    {
        Console.Write("The empty array " +
                      "shows minimum Deviation");
    }
    else
    {
        for(int i = ans[0]; i <= ans[1]; i++)
            Console.Write(arr[i] + " ");
    }
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript code to find sub-array whose
// sum shows the minimum deviation

function getSubArray(arr, n, K)
{
    let i = -1;
    let j = -1;
    let currSum = 0;

    // Starting index, ending index, Deviation
    let result = [ i, j,
                      Math.abs(K -
                      Math.abs(currSum)) ];

    // Iterate i and j to get all subarrays
    for(i = 0; i < n; i++)
    {
        currSum = 0;

        for(j = i; j < n; j++)
        {
            currSum += arr[j];
            let currDev = Math.abs(K -
                          Math.abs(currSum));

            // Found sub-array with less sum
            if(currDev < result[2])
            {
                result[0] = i;
                result[1] = j;
                result[2] = currDev;
            }

            // Exactly same sum
            if(currDev == 0)
                return result;
        }
    }
    return result;
}

// driver code

     let arr = [ 15, -3, 5, 2, 7, 6, 34, -6 ];
    let n = arr.length;
    let K = 50;

    // Array to store return values
    let ans = getSubArray(arr, n, K);

    if(ans[0] == -1)
    {
        document.write("The empty array " +
                           "shows minimum Deviation");
    }
    else
    {
        for(let i = ans[0]; i <= ans[1]; i++)
            document.write(arr[i] + " ");
    }

</script>
```

**Output:** 

```
-3 5 2 7 6 34
```

**时间复杂度:** O(N^2)

**有效方法:**如果数组仅由**非负整数**组成，则使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来提高每次迭代中求和的计算时间。滑动窗口技术通过使用先前的子阵列和计算新的子阵列和来降低复杂性。增加右边的指数，直到差值(K-sum)大于零。考虑第一个子阵列为负(K-sum)，下一个子阵列为左索引= i+1(其中 I 为当前右索引)。

下面是上述方法的实现:

## C++

```
// C++ code to find non-negative sub-array
// whose sum shows minimum deviation. This
// works only if all elements in array are
// non-negative
#include <bits/stdc++.h>
using namespace std;

struct Pair
{
    int f, s, t;

    Pair(int f, int s, int t)
    {
        this->f = f;
        this->s = s;
        this->t = t;
    }
};

// Function to return the index
Pair* getSubArray(int *arr, int n, int K)
{
    int currSum = 0;
    int prevDif = 0;
    int currDif = 0;

    Pair *result = new Pair(
        -1, -1, abs(K - abs(currSum)));
    Pair *resultTmp = result;
    int i = 0;
    int j = 0;

    while (i<= j && j<n)
    {

        // Add Last element tp currSum
        currSum += arr[j];

        // Save Difference of previous Iteration
        prevDif = currDif;

        // Calculate new Difference
        currDif = K - abs(currSum);

        // When the Sum exceeds K
        if (currDif <= 0)
        {
            if (abs(currDif) < abs(prevDif))
            {

                // Current Difference greater
                // in magnitude. Store Temporary
                // Result
                resultTmp = new Pair(i, j, currDif);
            }
            else
            {

                // Difference in Previous was lesser
                // In previous, Right index = j-1
                resultTmp = new Pair(i, j - 1, prevDif);

                // In next iteration, Left Index Increases
                // but Right Index remains the Same
                // Update currSum and i Accordingly
                currSum -= (arr[i] + arr[j]);

                i += 1;
            }
        }

        // Case to simply increase Right Index
        else
        {
            resultTmp = new Pair(i, j, currDif);
            j += 1;
        }

        if (abs(resultTmp->t) < abs(result->t))
        {

            // Check if lesser deviation found
            result = resultTmp;
        }
    }
    return result;
}

// Driver Code
int main()
{
    int arr[] = { 15, -3, 5, 2, 7, 6, 34, -6 };

    int n = sizeof(arr) / sizeof(arr[0]);

    int K = 50;

    Pair *tmp = getSubArray(arr, n, K);
    int i = tmp->f;
    int j = tmp->s;
    int minDev = tmp->t;

    if (i == -1)
    {
        cout << "The empty array shows minimum Deviation"
             << endl;
        return 0;
    }

    for(int k = i + 1; k < j + 1; k++)
    {
        cout << arr[k] << " ";
    }

    return 0;
}

// This code is contributed by pratham76
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find non-negative sub-array
// whose sum shows minimum deviation. This
// works only if all elements in array are
// non-negative
import java.util.*;

class GFG{

static class Pair
{
    int f, s, t;

    Pair(int f, int s, int t)
    {
        this.f = f;
        this.s = s;
        this.t = t;
    }
};

// Function to return the index
static Pair getSubArray(int []arr, int n, int K)
{
    int currSum = 0;
    int prevDif = 0;
    int currDif = 0;

    Pair result = new Pair(
        -1, -1, Math.abs(K - Math.abs(currSum)));
    Pair resultTmp = result;
    int i = 0;
    int j = 0;

    while (i<= j && j<n)
    {

        // Add Last element tp currSum
        currSum += arr[j];

        // Save Difference of previous Iteration
        prevDif = currDif;

        // Calculate new Difference
        currDif = K - Math.abs(currSum);

        // When the Sum exceeds K
        if (currDif <= 0)
        {
            if (Math.abs(currDif) < Math.abs(prevDif))
            {

                // Current Difference greater
                // in magnitude. Store Temporary
                // Result
                resultTmp = new Pair(i, j, currDif);
            }
            else
            {

                // Difference in Previous was lesser
                // In previous, Right index = j-1
                resultTmp = new Pair(i, j - 1, prevDif);

                // In next iteration, Left Index Increases
                // but Right Index remains the Same
                // Update currSum and i Accordingly
                currSum -= (arr[i] + arr[j]);

                i += 1;
            }
        }

        // Case to simply increase Right Index
        else
        {
            resultTmp = new Pair(i, j, currDif);
            j += 1;
        }

        if (Math.abs(resultTmp.t) < Math.abs(result.t))
        {

            // Check if lesser deviation found
            result = resultTmp;
        }
    }
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 15, -3, 5, 2, 7, 6, 34, -6 };

    int n = arr.length;

    int K = 50;

    Pair tmp = getSubArray(arr, n, K);
    int i = tmp.f;
    int j = tmp.s;
    int minDev = tmp.t;

    if (i == -1)
    {
        System.out.print("The empty array shows minimum Deviation"
             +"\n");
        return ;
    }

    for(int k = i + 1; k < j + 1; k++)
    {
        System.out.print(arr[k]+ " ");
    }

}
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python Code to find non-negative
# sub-array whose sum shows minimum deviation
# This works only if all elements
# in array are non-negative

# function to return the index
def getSubArray(arr, n, K):
    currSum = 0
    prevDif = 0
    currDif = 0
    result = [-1, -1, abs(K-abs(currSum))]
    resultTmp = result
    i = 0
    j = 0

    while(i<= j and j<n):

        # Add Last element tp currSum
        currSum += arr[j]

        # Save Difference of previous Iteration
        prevDif = currDif

        # Calculate new Difference
        currDif = K - abs(currSum)

        # When the Sum exceeds K
        if(currDif <= 0):
            if abs(currDif) < abs(prevDif):

            # Current Difference greater in magnitude
            # Store Temporary Result
                resultTmp = [i, j, currDif]
            else:

            # Difference in Previous was lesser
            # In previous, Right index = j-1
                resultTmp = [i, j-1, prevDif]

            # In next iteration, Left Index Increases
            # but Right Index remains the Same
            # Update currSum and i Accordingly
            currSum -= (arr[i]+arr[j])

            i += 1

        # Case to simply increase Right Index
        else:
            resultTmp = [i, j, currDif]
            j += 1

        if(abs(resultTmp[2]) < abs(result[2])):
        # Check if lesser deviation found
            result = resultTmp

    return result

# Driver Code
def main():
    arr = [15, -3, 5, 2, 7, 6, 34, -6]

    n = len(arr)

    K = 50

    [i, j, minDev] = getSubArray(arr, n, K)

    if(i ==-1):
        print("The empty array shows minimum Deviation")
        return 0

    for i in range(i, j+1):
        print arr[i],

main()
```

## C#

```
// C# code to find non-negative sub-array
// whose sum shows minimum deviation. This
// works only if all elements in array are
// non-negative
using System;

public class GFG{

  class Pair
  {
    public int f, s, t;

    public Pair(int f, int s, int t)
    {
      this.f = f;
      this.s = s;
      this.t = t;
    }
  };

  // Function to return the index
  static Pair getSubArray(int []arr, int n, int K)
  {
    int currSum = 0;
    int prevDif = 0;
    int currDif = 0;

    Pair result = new Pair(
      -1, -1, Math.Abs(K - Math.Abs(currSum)));
    Pair resultTmp = result;
    int i = 0;
    int j = 0;

    while (i <= j && j < n)
    {

      // Add Last element tp currSum
      currSum += arr[j];

      // Save Difference of previous Iteration
      prevDif = currDif;

      // Calculate new Difference
      currDif = K - Math.Abs(currSum);

      // When the Sum exceeds K
      if (currDif <= 0)
      {
        if (Math.Abs(currDif) < Math.Abs(prevDif))
        {

          // Current Difference greater
          // in magnitude. Store Temporary
          // Result
          resultTmp = new Pair(i, j, currDif);
        }
        else
        {

          // Difference in Previous was lesser
          // In previous, Right index = j-1
          resultTmp = new Pair(i, j - 1, prevDif);

          // In next iteration, Left Index Increases
          // but Right Index remains the Same
          // Update currSum and i Accordingly
          currSum -= (arr[i] + arr[j]);

          i += 1;
        }
      }

      // Case to simply increase Right Index
      else
      {
        resultTmp = new Pair(i, j, currDif);
        j += 1;
      }

      if (Math.Abs(resultTmp.t) < Math.Abs(result.t))
      {

        // Check if lesser deviation found
        result = resultTmp;
      }
    }
    return result;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 15, -3, 5, 2, 7, 6, 34, -6 };

    int n = arr.Length;

    int K = 50;

    Pair tmp = getSubArray(arr, n, K);
    int i = tmp.f;
    int j = tmp.s;
    int minDev = tmp.t;

    if (i == -1)
    {
      Console.Write("The empty array shows minimum Deviation"
                    +"\n");
      return ;
    }

    for(int k = i + 1; k < j + 1; k++)
    {
      Console.Write(arr[k]+ " ");
    }

  }
}

// This code is contributed by 29AjayKumar
```

**Output**

```
-3 5 2 7 6 34
```

**时间复杂度:** O(N)