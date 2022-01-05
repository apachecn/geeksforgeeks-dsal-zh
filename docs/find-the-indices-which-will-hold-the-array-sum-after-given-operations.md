# 找到给定运算后保持数组和的索引

> 原文:[https://www . geeksforgeeks . org/find-the-indexs-哪些将持有给定运算后的数组总和/](https://www.geeksforgeeks.org/find-the-indices-which-will-hold-the-array-sum-after-given-operations/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是在执行给定的操作后，打印最有可能保持数组的全部和的索引:

*   选择任意两个元素，如**arr【I】**和**arr【j】**，将它们的总和存储在变量 **K** 中
*   在**最大值(arr[i]，arr[j])** 的索引处分配 **K** ，在**最小值(arr[i]，arr[j])** 的索引处分配 **0**

这样，在选择所有元素后，剩下的最后一个元素将存储整个数组的总和。任务是按照保持数组和的最大可能性的顺序返回数组的索引。

**示例:**

> **输入:** arr[] = {2，1，4}
> **输出:** {2}
> **说明:**元素的选择可以通过以下方式完成:
> 
> 方式一:
> 
> *   选择索引{0，1}处的元素，因此 arr[] = {3，0，4}
> *   选择索引{0，2}处的元素，因此 arr[] = {0，0，7}
> 
> 方式二:
> 
> *   选择索引{0，2}处的元素，因此 arr[] = {0，1，6}
> *   选择索引{1，2}处的元素，因此 arr[] = {0，0，7}
> 
> 方式三:
> 
> *   选择索引{1，2}处的元素，因此 arr[] = {2，0，5}
> *   选择索引{0，2}处的元素，因此 arr[] = {0，0，7}
> 
> 在这种情况下，输出= {2}，索引 0 和索引 1 持有总和的可能性为零，因此排除了它。
> 
> **输入:** arr[] = {1，2，4，3}
> **输出:** {1，2，3}

**方法:**对给定的数组元素进行排序，检查直到**I-1**的和是否大于具有元素的直到**的和，如果是**大于**，则该索引有可能是有效索引。**

1.  取一对的[向量，表示 **v** ，将所有元素和各自的索引存储成对，还取一个变量，表示**和**，将存储整个数组的和。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
2.  将向量按升序排序，取一个计数器，比如说 **c，**用 **1** 初始化，因为一个索引总是有可能保存数组的和。
3.  迭代从**倒数第二个**元素开始的向量，检查**的和直到****倒数第二个元素**是否大于的和直到**的和直到最后**(即数组的和)，如果大于**则**递增**计数器，这意味着它有**保持和的可能性**，否则**中断**循环**
4.  取一个向量说 **ans** 存储有效的索引，通过从末尾到计数器的迭代来存储索引，然后**对 **ans** 向量进行排序**并打印出来。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to predict the indices which
// will hold the sum of the given array
void predictIndices(int arr[], int N)
{
    // Variable for sum of the array
    int sum = 0;

    // Vector to store the elements along
    // with the indices in pair
    vector<pair<int, int> > v;
    for (int i = 0; i < N; i++) {
        v.push_back({ arr[i], i });
        sum += arr[i];
    }

    // Sort the vector
    sort(v.begin(), v.end());

    // Take a counter c, initialize
    // it with 1
    int c = 1;

    // Iterate over the vector from the end
    // excluding the last element and each time
    // update sum by decrementing its value
    // by the element in the sorted vector
    for (int i = N - 2; i >= 0; i--) {
        sum -= v[i + 1].first;

        // If element is greater than the sum
        // break the loop
        if (sum < v[i + 1].first) {
            break;
        }
        // Else increment the counter c
        else {
            c++;
        }
    }

    // Vector to store all the indices
    // which can hold the sum
    vector<int> ans;

    // Iterate the ans vector in reverse order
    // till index is greater or equal to N - c
    // and store the indices in ans vector
    for (int i = N - 1; i >= N - c; i--) {
        ans.push_back(v[i].second);
    }

    // Sort the ans vector
    sort(ans.begin(), ans.end());

    // Print the desired indices
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    predictIndices(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class GFG {

  public static class Pair {
    int first = 0;
    int second = 0;

    public Pair(int first, int second) {
      this.first = first;
      this.second = second;
    }
  }

  // Function to predict the indices which
  // will hold the sum of the given array
  public static void predictIndices(int arr[], int N)
  {

    // Variable for sum of the array
    int sum = 0;

    // Vector to store the elements along
    // with the indices in pair
    ArrayList<Pair> v = new ArrayList<Pair>();
    for (int i = 0; i < N; i++) {
      v.add(new Pair(arr[i], i));
      sum += arr[i];
    }

    // Sort the vector
    Collections.sort(v, new Comparator<Pair>() {
      @Override
      public int compare(Pair p1, Pair p2){
        return p1.first - p2.first;
      }
    });

    // Take a counter c, initialize
    // it with 1
    int c = 1;

    // Iterate over the vector from the end
    // excluding the last element and each time
    // update sum by decrementing its value
    // by the element in the sorted vector
    for (int i = N - 2; i >= 0; i--) {
      sum -= v.get(i + 1).first;

      // If element is greater than the sum
      // break the loop
      if (sum < v.get(i + 1).first) {
        break;
      }
      // Else increment the counter c
      else {
        c++;
      }
    }

    // Vector to store all the indices
    // which can hold the sum
    ArrayList<Integer> ans = new ArrayList<Integer>();

    // Iterate the ans vector in reverse order
    // till index is greater or equal to N - c
    // and store the indices in ans vector
    for (int i = N - 1; i >= N - c; i--) {
      ans.add(v.get(i).second);
    }

    // Sort the ans vector
    Collections.sort(ans);

    // Print the desired indices
    for (int i = 0; i < ans.size(); i++) {
      System.out.print(ans.get(i) + " ");
    }
  }

  // Driver Code
  public static void main(String args[]) {
    int arr[] = { 1, 2, 4, 3 };
    int N = arr.length;

    predictIndices(arr, N);
  }

}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python3  implementation for the above approach

# Function to predict the indices which
# will hold the sum of the given array
def predictIndices(arr, N):

    # Variable for sum of the array
    sum = 0

    # Vector to store the elements along
    # with the indices in pair
    v = []
    for i in range(N):
        v.append([arr[i], i])
        sum += arr[i]

    # Sort the vector
    v.sort()

    # Take a counter c, initialize
    # it with 1
    c = 1

    # Iterate over the vector from the end
    # excluding the last element and each time
    # update sum by decrementing its value
    # by the element in the sorted vector
    for i in range(N - 2, -1, -1):
        sum -= v[i + 1][0]

        # If element is greater than the sum
        # break the loop
        if (sum < v[i + 1][0]):
            break

        # Else increment the counter c
        else:
            c += 1

    # Vector to store all the indices
    # which can hold the sum
    ans = []

    # Iterate the ans vector in reverse order
    # till index is greater or equal to N - c
    # and store the indices in ans vector
    for i in range(N - 1, N - c-1, -1):
        ans.append(v[i][1])

    # Sort the ans vector
    ans.sort()

    # Print the desired indices
    for i in range(len(ans)):
        print(ans[i], end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 4, 3]
    N = len(arr)

    predictIndices(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

    class Pair
    {
        public int first = 0;
        public int second = 0;

        public Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to predict the indices which
    // will hold the sum of the given array
    public static void predictIndices(int[] arr, int N)
    {

        // Variable for sum of the array
        int sum = 0;

        // Vector to store the elements along
        // with the indices in pair
        List<Pair> v = new List<Pair>();
        for (int i = 0; i < N; i++)
        {
            v.Add(new Pair(arr[i], i));
            sum += arr[i];
        }

        // Sort the vector
        v.Sort((Pair x, Pair y) => x.first.CompareTo(y.first));

        // Take a counter c, initialize
        // it with 1
        int c = 1;

        // Iterate over the vector from the end
        // excluding the last element and each time
        // update sum by decrementing its value
        // by the element in the sorted vector
        for (int i = N - 2; i >= 0; i--)
        {
            sum -= v[i + 1].first;

            // If element is greater than the sum
            // break the loop
            if (sum < v[i + 1].first)
            {
                break;
            }
            // Else increment the counter c
            else
            {
                c++;
            }
        }

        // Vector to store all the indices
        // which can hold the sum
        List<int> ans = new List<int>();

        // Iterate the ans vector in reverse order
        // till index is greater or equal to N - c
        // and store the indices in ans vector
        for (int i = N - 1; i >= N - c; i--)
        {
            ans.Add(v[i].second);
        }

        // Sort the ans vector
        ans.Sort();

        // Print the desired indices
        for (int i = 0; i < ans.Count; i++)
        {
            Console.Write(ans[i] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 4, 3 };
        int N = arr.Length;

        predictIndices(arr, N);
    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>

// Javascript implementation for the above approach

// Function to predict the indices which
// will hold the sum of the given array
function predictIndices(arr, N)
{
    // Variable for sum of the array
    var sum = 0;

    // Vector to store the elements along
    // with the indices in pair
    var v = [];
    for (var i = 0; i < N; i++) {
        v.push([arr[i], i ]);
        sum += arr[i];
    }

    // Sort the vector
    v.sort();

    // Take a counter c, initialize
    // it with 1
    var c = 1;

    // Iterate over the vector from the end
    // excluding the last element and each time
    // update sum by decrementing its value
    // by the element in the sorted vector
    for (var i = N - 2; i >= 0; i--) {
        sum -= v[i + 1][0];

        // If element is greater than the sum
        // break the loop
        if (sum < v[i + 1][0]) {
            break;
        }
        // Else increment the counter c
        else {
            c++;
        }
    }

    // Vector to store all the indices
    // which can hold the sum
    var ans = [];

    // Iterate the ans vector in reverse order
    // till index is greater or equal to N - c
    // and store the indices in ans vector
    for (var i = N - 1; i >= N - c; i--) {
        ans.push(v[i][1]);
    }

    // Sort the ans vector
    ans.sort();

    // Print the desired indices
    for (var i = 0; i < ans.length; i++) {
        document.write(ans[i]+ " ");
    }
}

// Driver Code
var arr = [1, 2, 4, 3];
var N = arr.length;
predictIndices(arr, N);

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
1 2 3 
```

***时间复杂度*****:**O(NlogN)
***辅助空间*** **:** O(N)