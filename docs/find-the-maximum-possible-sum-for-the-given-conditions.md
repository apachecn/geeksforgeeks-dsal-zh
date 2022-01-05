# 求给定条件下的最大可能和

> 原文:[https://www . geesforgeks . org/find-给定条件下的最大可能总和/](https://www.geeksforgeeks.org/find-the-maximum-possible-sum-for-the-given-conditions/)

给定一个大小为 N 的数组 **arr[]** ，任务是通过以下给定条件找到数组的最大可能和:

*   在每一步，只有一个元素可以用来增加总和。
*   如果从数组中选择了某个元素 K，数组中剩余的数字将减少 1。
*   数组中的元素不能减少到超过 0。

**示例:**

> **输入:** arr = {6，6，6}
> **输出:** 15
> **说明:**
> 最初，总和为 0。因为所有元素都是相等的，所以选择任何一个元素。
> 选择前六后求和= 6。剩余元素= {5，5}。
> 选五后求和= 11。剩余元素= {4}。
> 最后，选择 4，使最大和为 15。
> 
> **输入:** arr = {0，1，0}
> **输出:** 1
> **说明:**
> 最初，总和为 0。数组中只能选择一个数字，因为其余元素都是 0。
> 因此，最大和= 1。

**方法:**由于所有其他元素的值都减少 1，很明显，如果我们在每次迭代中选择最大元素，我们就会得到最大和。因此，为了做到这一点，使用了[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。

*   其思想是按降序对数组的元素进行排序。
*   现在，由于我们可以在每次迭代中选择最大值，因此我们将元素 K 在某个索引‘I’处的值计算为**(K–I)**。
*   如果在任何索引处，元素的值变为 0，那么所有超过该索引的元素都将为 0。

下面是上述方法的实现:

## C++

```
// C++ program to find the maximum
// possible Sum for the given conditions
#include<bits/stdc++.h>
using namespace std;

// Function to find the maximum
// possible sum for the
// given conditions
int maxProfit(int arr[], int n)
{

    // Sorting the array
    sort(arr, arr + n, greater<int>());

    // Variable to store the answer
    int ans = 0;

    // Iterating through the array
    for(int i = 0; i < n; i++)
    {

       // If the value is greater than 0
       if ((arr[i] - (1 * i)) > 0)
           ans += (arr[i] - (1 * i));

       // If the value becomes 0
       // then break the loop because
       // all the weights after this
       // index will be 0
       if ((arr[i] - (1 * i)) == 0)
           break;
    }

    // Print profit
    return ans;
}

// Driver code
int main()
{
    int arr[] = {6, 6, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxProfit(arr, n);
    return 0;
}

// This code is contributed by ankitkumar34
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// possible Sum for the given conditions
import java.util.Arrays;
import java.util.Collections;

public class GFG{

    // Function to find the maximum
    // possible sum for the
    // given conditions
    static int maxProfit(Integer [] arr)
    {

        // Sorting the array
        Arrays.sort(arr, Collections.reverseOrder());

        // Variable to store the answer
        int ans = 0;

        // Iterating through the array
        for(int i = 0; i < arr.length; i++)
        {

           // If the value is greater than 0
           if ((arr[i] - (1 * i)) > 0)
               ans += (arr[i] - (1 * i));

           // If the value becomes 0
           // then break the loop because
           // all the weights after this
           // index will be 0
           if ((arr[i] - (1 * i)) == 0)
               break;
        }

        // Print profit
        return ans;
    }

// Driver code
public static void main(String[] args)
{
    Integer arr[] = { 6, 6, 6 };
    System.out.println(maxProfit(arr));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# possible Sum for the given conditions

# Function to find the maximum
# possible sum for the
# given conditions
def maxProfit(arr):

    # Sorting the array
    arr.sort(reverse = True)

    # Variable to store the answer
    ans = 0

    # Iterating through the array
    for i in range(len(arr)):

        # If the value is greater than 0
        if (arr[i]-(1 * i))>0:
            ans+=(arr[i]-(1 * i))

        # If the value becomes 0
        # then break the loop because
        # all the weights after this
        # index will be 0
        if (arr[i]-(1 * i))== 0:
            break

    # print profit
    return ans   

# Driver code
if __name__ == "__main__":

    arr = [6, 6, 6]

    print(maxProfit(arr))

```

## C#

```
// C# program to find the maximum
// possible Sum for the given conditions
using System;

class GFG{

// Function to find the maximum
// possible sum for the
// given conditions
static int maxProfit(int[] arr)
{

    // Sorting the array
    Array.Sort(arr);
    Array.Reverse(arr);

    // Variable to store the answer
    int ans = 0;

    // Iterating through the array
    for(int i = 0; i < arr.Length; i++)
    {

       // If the value is greater than 0
       if ((arr[i] - (1 * i)) > 0)
           ans += (arr[i] - (1 * i));

       // If the value becomes 0
       // then break the loop because
       // all the weights after this
       // index will be 0
       if ((arr[i] - (1 * i)) == 0)
           break;
    }

    // Print profit
    return ans;
}

// Driver code
static public void Main ()
{
    int[] arr = { 6, 6, 6 };

    Console.Write(maxProfit(arr));
}
}

// This code is contributed by Shubhamsingh10
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// possible Sum for the given conditions

// Function to find the maximum
// possible sum for the
// given conditions
function maxProfit(arr)
{

    // Sorting the array
    arr.sort();
    arr.reverse();

    // Variable to store the answer
    let ans = 0;

    // Iterating through the array
    for(let i = 0; i < arr.length; i++)
    {

        // If the value is greater than 0
        if ((arr[i] - (1 * i)) > 0)
            ans += (arr[i] - (1 * i));

        // If the value becomes 0
        // then break the loop because
        // all the weights after this
        // index will be 0
        if ((arr[i] - (1 * i)) == 0)
            break;
    }

    // Print profit
    return ans;
}

// Driver code
let arr = [ 6, 6, 6 ];

document.write(maxProfit(arr));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
15
```