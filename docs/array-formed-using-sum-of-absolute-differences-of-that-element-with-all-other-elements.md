# 使用该元素与所有其他元素的绝对差之和形成的数组

> 原文:[https://www . geesforgeks . org/array-formed-使用该元素与所有其他元素的绝对差之和/](https://www.geeksforgeeks.org/array-formed-using-sum-of-absolute-differences-of-that-element-with-all-other-elements/)

给定排序后的 **N** 个不同正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是生成一个数组，使得新数组中每个索引处的元素是对应元素与给定数组中所有其他元素的绝对差之和。

> **输入:**arr[]=【2，3，5】
> **输出:**【4，3，5】
> **解释:**
> 距离(2)= | 2–3 |+| 2–5 | = 4
> 距离(3)= | 3–2 |+| 3–5 | = 3
> 距离(5)= | 5–2 |+| 5–3 | = 5
> 因此，我们将返回【4，3，5】
> 
> **输入:**arr[]=【2，3，5，6】
> **输出:**【8，6，6，8】
> **解释:**
> 距离(2)= | 2–3 |+| 2–5 |+| 2–6 | = 8
> 距离(3)= | 3–2 |+| 3–5 |+| 3–6 | = 6
> 距离(5)= | 5–2 |+| 5–3 |+| 5–6

**天真方法:**想法是[为数组中的每个元素生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)**arr【】**并将新数组中每个元素的对的绝对差之和相加。在上述步骤之后，打印所有元素的数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the new array
vector<int> calculate(int* arr, int n)
{

    // Initialize the Arraylist
    vector<int> ans;

    // Sum of absolute differences
    // of element with all elements
    for(int i = 0; i < n; i++)
    {

        // Initialize int sum to 0
        int sum = 0;

        for(int j = 0; j < n; j++)
        {
            sum += abs(arr[i] - arr[j]);
        }

        // Add the value of sum to ans
        ans.push_back(sum);
    }

    // Return the final ans
    return ans;
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 2, 3, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    vector<int> ans = calculate(arr, n);

    cout << "[";
    for(auto itr : ans)
        cout << itr << ", ";

    cout << "]";

    return 0;
}
// This code is contributed by jrishabh99
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to return the new array
    private static List<Integer>
    calculate(int[] arr)
    {
        // Length of the arraylist
        int n = arr.length;

        // Initialize the Arraylist
        List<Integer> ans
            = new ArrayList<Integer>();

        // Sum of absolute differences
        // of element with all elements
        for (int i = 0;
            i < arr.length; i++) {

            // Initialize int sum to 0
            int sum = 0;

            for (int j = 0;
                j < arr.length; j++) {

                sum += Math.abs(arr[i] - arr[j]);
            }

            // Add the value of sum to ans
            ans.add(sum);
        }

        // Return the final ans
        return ans;
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given array arr[]
        int[] arr = { 2, 3, 5, 6 };

        // Function Call
        System.out.println(calculate(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the new array
# private static List<Integer>
def calculate(arr):

    # Length of the arraylist
    n = len(arr)

    # Initialize the Arraylist
    ans = []

    # Sum of absolute differences
    # of element with all elements
    for i in range(n):

        # Initialize sum to 0
        sum = 0

        for j in range(len(arr)):
            sum += abs(arr[i] - arr[j])

        # Add the value of sum to ans
        ans.append(sum)

    # Return the final ans
    return ans

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 2, 3, 5, 6 ]

    # Function call
    print(calculate(arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to return the new array
private static List<int> calculate(int[] arr)
{

    // Length of the arraylist
    int n = arr.Length;

    // Initialize the Arraylist
    List<int> ans = new List<int>();

    // Sum of absolute differences
    // of element with all elements
    for(int i = 0; i < arr.Length; i++)
    {

        // Initialize int sum to 0
        int sum = 0;

        for(int j = 0; j < arr.Length; j++)
        {
            sum += Math.Abs(arr[i] - arr[j]);
        }

        // Add the value of sum to ans
        ans.Add(sum);
    }

    // Return the final ans
    return ans;
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int[] arr = { 2, 3, 5, 6 };

    List<int> tmp = calculate(arr);
    Console.Write("[");
    for(int i = 0; i < tmp.Count; i++)
    {
        if(i != tmp.Count - 1)
        {
            Console.Write(tmp[i] + ", ");
        }
        else
        {
            Console.Write(tmp[i]);
        }
    }
    Console.Write("]");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

   // Function to return the new array
   function
    calculate(arr)
    {
        // Length of the arraylist
        let n = arr.length;

        // Initialize the Arraylist
        let ans
            = [];

        // Sum of absolute differences
        // of element with all elements
        for (let i = 0;
            i < arr.length; i++) {

            // Initialize let sum to 0
            let sum = 0;

            for (let j = 0;
                j < arr.length; j++) {

                sum += Math.abs(arr[i] - arr[j]);
            }

            // Add the value of sum to ans
            ans.push(sum);
        }

        // Return the final ans
        return ans;
    }

// Driver Code

    // Given array arr[]
       let arr = [ 2, 3, 5, 6 ];

        // Function Call
        document.write(calculate(arr));

</script>
```

**Output:** 

```
[8, 6, 6, 8]
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(N)

**有效方法:**为了优化上述方法，其思想是跟踪左边值的累积减法和右边值的总和。每个元素的所有对之差的总和由下式给出:

> 元素数量到左*当前值-元素数量到右*当前值

*   求给定数组中所有元素的[和(比如**和**)。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   将**子**初始化为 0。
*   遍历给定的数组，对每个元素执行以下操作:
    *   从总和中减去当前值**arr【I】**。
    *   使用公式将每个元素的所有对的差值加到结果数组中:

```
sub + (i * arr[i]) - ((n - i - 1) * arr[i]) + sum
```

*   从总和中减去当前值**arr【I】**。
*   完成上述步骤后，打印结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return list of
// total Distance of each element
// from other elements in array
vector<int> calculate(int arr[],
                      int n)
{
  int sub = 0;
  int sum = 0;

  // Initialize the arraylist
  vector<int> ans;

  // Keep track of the
  // accumulated of the
  // sum of values to right
  for (int i = n - 1;
           i >= 0; i--)
    sum += arr[i];

  // Keep track of the
  // accumulated subtraction
  // of the values to the left
  for (int i = 0; i < n; i++)
  {
    sum -= arr[i];

    // Add the value to the
    // resultant array ans[]
    ans.push_back(sub + (i * arr[i]) -
                 ((n - i - 1) *
                   arr[i]) + sum);

    sub -= arr[i];
  }

  // Return the final
  // answer
  return ans;
}

// Driver Code
int main()
{
  // Initialize the array
  int arr[] = {2, 3, 5, 6};
  int n = sizeof(arr) /
          sizeof(arr[0]);
  vector<int> ans = (calculate(arr, n));

  for (int i = 0; i < n; i++)
    cout << ans[i] << " ";
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to return list of
    // total Distance of each element
    // from other elements in array
    private static List<Integer>
    calculate(int[] arr)
    {
        // Length of the array
        int n = arr.length;
        int sub = 0;
        int sum = 0;

        // Initialize the arraylist
        List<Integer> ans
            = new ArrayList<Integer>();

        // Keep track of the accumulated
        // of the sum of values to right
        for (int i = n - 1; i >= 0; i--)
            sum += arr[i];

        // Keep track of the accumulated
        // subtraction of the values to the left
        for (int i = 0; i < arr.length; i++) {

            sum -= arr[i];

            // Add the value to the resultant
            // array ans[]
            ans.add(sub
                    + (i * arr[i])
                    - ((n - i - 1)
                    * arr[i])
                    + sum);

            sub -= arr[i];
        }
        // return the final answer
        return ans;
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Initialize the array
        int[] arr = { 2, 3, 5, 6 };

        // Function Call
        System.out.println(calculate(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return list of
# total Distance of each element
# from other elements in array
def calculate (arr):

    # Length of the array
    n = len(arr)
    sub = 0
    Sum = 0

    # Initialize the ArrayList
    ans = []

    # Keep track of the accumulated
    # of the sum of values to right
    for i in range(n - 1, -1, -1):
        Sum += arr[i]

    # Keep track of the accumulated
    # subtraction of values to left
    for i in range(len(arr)):
        Sum -= arr[i]

        # Add the value to the resultant
        # array ans[]
        ans.append(sub + (i * arr[i]) -
               ((n - i - 1) * arr[i]) + Sum)

        sub -= arr[i]

    # Return the final answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Initialize the array
    arr = [ 2, 3, 5, 6 ]

    # Function call
    print(calculate(arr))

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return list of
// total Distance of each element
// from other elements in array
private static List<int> calculate(int[] arr)
{

    // Length of the array
    int n = arr.Length;
    int sub = 0;
    int sum = 0;

    // Initialize the arraylist
    List<int> ans = new List<int>();

    // Keep track of the accumulated
    // of the sum of values to right
    for(int i = n - 1; i >= 0; i--)
        sum += arr[i];

    // Keep track of the accumulated
    // subtraction of the values to the left
    for(int i = 0; i < arr.Length; i++)
    {
        sum -= arr[i];

        // Add the value to the resultant
        // array ans[]
        ans.Add(sub + (i * arr[i]) -
                 ((n - i - 1) *
                 arr[i]) + sum);

        sub -= arr[i];
    }

    // return the readonly answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Initialize the array
    int[] arr = { 2, 3, 5, 6 };

    // Function Call
    Console.Write("[ ");
    foreach(int i in calculate(arr))
        Console.Write(i + ", ");

    Console.Write("]");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript program for the
// above approach

// Function to return list of
// total Distance of each element
// from other elements in array
function calculate(arr, n)
{
  var sub = 0;
  var sum = 0;

  // Initialize the arraylist
  var ans = [];

  // Keep track of the
  // accumulated of the
  // sum of values to right
  for (var i = n - 1;
           i >= 0; i--)
    sum += arr[i];

  // Keep track of the
  // accumulated subtraction
  // of the values to the left
  for (var i = 0; i < n; i++)
  {
    sum -= arr[i];

    // Add the value to the
    // resultant array ans[]
    ans.push(sub + (i * arr[i]) -
                 ((n - i - 1) *
                   arr[i]) + sum);

    sub -= arr[i];
  }

  // Return the final
  // answer
  return ans;
}

// Driver Code
// Initialize the array
var arr = [2, 3, 5, 6]
var n = arr.length;
var ans = (calculate(arr, n));

for (var i = 0; i < n; i++)
  document.write( ans[i] + " ");

// This code is contributed by famously.
</script>
```

**Output:** 

```
[8, 6, 6, 8]
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(N)*