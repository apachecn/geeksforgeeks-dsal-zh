# 最小互换，以便应用二分搜索法

> 原文:[https://www . geesforgeks . org/minimum-swaps-so-binary-search-可应用/](https://www.geeksforgeeks.org/minimum-swaps-so-that-binary-search-can-be-applied/)

给定一个长度为 n 和一个整数 k 的未排序数组，在使用二分搜索法之前，找到最小交换以获得 k 的位置。在这里，我们可以任意多次交换任意两个数字。如果我们不能通过交换元素得到位置，打印“-1”。
**例:**

```
Input : arr = {3, 10, 6, 7, 2, 5, 4}
        k = 4
Output : 2
Explanation :
Here, after swapping 3 with 7 and 2 with 5, the 
final array will look like {7, 10, 6, 3, 5, 2, 4}.
Now, if we provide this array to binary search we
can get the position of 4.

Input : arr = {3, 10, 6, 7, 2, 5, 4}
        k = 10
Output : -1
Explanation :
Here, we can not get the position of 10 if we 
provide this array to the binary search even 
not with swapping some pairs.
```

**进场:**在讨论进场之前，我们必须假设这里我们不应该对换。我们只需要计算互换的最小数量，这样如果我们将新创建的数组提供给二分搜索法，我们就可以得到 k 的位置。为了做到这一点，我们需要将给定的数组传递给二分搜索法，并专注于以下事情:-

*   在去二分搜索法之前，我们需要计算最小元素的数量，即 k 的 **num_min** 和最大元素的数量，即 k 的 **num_max** 这里，num_min 表示 k 的较小可用元素的数量，num_max 表示我们可以用于交换的较大可用元素的数量
*   给定数组中 k 的**实际位置。**

下面是在实现二分搜索法期间将发生的测试用例:-
**用例 1:** 如果 arr[mid]大于 k，但是 k 的位置大于 mid。二分搜索法会带我们去(从[0]到[1 中])。但实际上我们的元素介于两者之间(arr[mid+1]到 arr[最后一个元素])。所以，为了走正确的方向，我们需要比 k 小的东西，这样我们就可以用 arr[mid]交换它，我们可以在 arr[mid+1]到 arr[last_element]之间切换。因此，这里我们需要一个交换，即**需要最少的**。
**情况 2:** 如果 arr[mid]小于 k 但 k 的位置小于 mid。二分搜索法会带我们去(arr[mid+1]到 arr[last_element])。但实际上我们的元素介于两者之间(arr[0]到 arr[mid-1])。所以，为了走正确的方向，我们需要大于 k 的东西，这样我们就可以用 arr[mid]交换它，我们可以在 arr[0]到 arr[mid-1]之间切换。因此，这里我们需要一次交换，即**需要最大值**。
**情况 3:**
如果 arr[mid]大于 k，k 的位置小于 mid。现在，在这种情况下，二分搜索法可以正常工作。但是等等，这是我们必须努力解决的重要问题。正如我们所知，在这种情况下，二分搜索法可以正常工作，arr[mid]在正确的位置，因此不会在任何交换中使用，因此这里我们必须减少它的一个更大的可用元素，即从 num_max。当 arr[mid]小于 k 且 k 的位置大于 mid 时，情况也是如此。在这里，我们必须减少它的一个较小的可用元素，即从 num_min。
**案例 4:** 如果 arr[mid] == k 或 pos == mid，那么我们很容易从二分搜索法出来。
所以，到目前为止，我们已经计算了 **need_minimum** 即交换所需的最小元素数， **need_maximum** 即交换所需的最大元素数， **num_max** 即 k 中仍可用于交换的较大元素总数， **num_min** 即 k 中可用于交换的最小元素总数。
现在这里我们要考虑两种情况:
**情况 1:** 如果需要 _ 最小值大于需要 _ 最大值。在这种情况下，我们必须用 k 的较小值交换所有这些需要的最大值元素，所以我们必须使用 num_min 中较小的元素。现在所有的需求最大值交换都完成了。这里最主要的是，当我们用更小的元素交换所有这些需要的最大元素时，这些更小的元素得到了它们正确的位置。因此，我们已经间接完成了一些所需的较小元素交换，这将被计算为**需要 _ 最小–需要 _ 最大**，并且可用的 num_min 将是**num _ min–需要 _ 最大**。现在，我们必须计算剩余需求最小互换。如果我们有足够的 num_min，即 num_min >需要 _ 最小值，我们可以计算这些互换。对于这种情况，互换将是**需要 _ 最大+需要 _ 最小**否则将是-1。当我们的需求最小值小于需求最大值时，同样的概念也适用。
以下是上述方法的基本实现:-

## C++

```
// CPP program to find Minimum number
// of swaps to get the position of
// the element if we provide an
// unsorted array to binary search.
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum swaps.
int findMinimumSwaps(int* arr, int n,
                     int k)
{
    int pos, num_min, num_max,
    need_minimum, need_maximum, swaps;
    num_min = num_max = need_minimum = 0;
    need_maximum = swaps = 0;

    // Here we are getting number of
    // smaller and greater elements of k.
    for (int i = 0; i < n; i++) {
        if (arr[i] < k)
            num_min++;

        else if (arr[i] > k)
            num_max++;
    }

    // Here we are calculating the actual
    // position of k in the array.
    for (int i = 0; i < n; i++) {
        if (arr[i] == k) {
            pos = i;
            break;
        }
    }

    int left, right, mid;
    left = 0;
    right = n - 1;

    // Implementing binary search as
    // per the above-discussed cases.
    while (left <= right) {
        mid = (left + right) / 2;

        // If we find the k.
        if (arr[mid] == k) {
            break;
        }

        else if (arr[mid] > k) {

            // If we need minimum
            // element swap.
            if (pos > mid)
                need_minimum++;

            else

                // Else the element is
                // at the right position.
                num_min--;

            left = mid + 1;
        }

        else {
            if (pos < mid)

                // If we need maximum
                // element swap.
                need_maximum++;

            else

                // Else element is at
                // the right position
                num_max--;

            right = mid - 1;
        }
    }

    // Calculating the required swaps.
    if (need_minimum > need_maximum) {
        swaps = swaps + need_maximum;
        num_min = num_min - need_maximum;
        need_minimum = need_minimum - need_maximum;
        need_maximum = 0;
    }

    else {
        swaps = swaps + need_minimum;
        num_max = num_max - need_minimum;
        need_maximum = need_maximum - need_minimum;
        need_minimum = 0;
    }

    // If it is impossible.
    if (need_maximum > num_max || need_minimum > num_min)
        return -1;

    else
        return (swaps + need_maximum + need_minimum);
}

// Driver function
int main()
{
    int arr[] = { 3, 10, 6, 7, 2, 5, 4 }, k = 4;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findMinimumSwaps(arr, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find Minimum number
// of swaps to get the position of
// the element if we provide an
// unsorted array to binary search.
public class GFG {

// Function to find minimum swaps.
    static int findMinimumSwaps(int[] arr, int n,
            int k) {
        int pos = 0, num_min, num_max,
                need_minimum, need_maximum, swaps;
        num_min = num_max = need_minimum = 0;
        need_maximum = swaps = 0;

        // Here we are getting number of
        // smaller and greater elements of k.
        for (int i = 0; i < n; i++) {
            if (arr[i] < k) {
                num_min++;
            } else if (arr[i] > k) {
                num_max++;
            }
        }

        // Here we are calculating the actual
        // position of k in the array.
        for (int i = 0; i < n; i++) {
            if (arr[i] == k) {
                pos = i;
                break;
            }
        }

        int left, right, mid;
        left = 0;
        right = n - 1;

        // Implementing binary search as
        // per the above-discussed cases.
        while (left <= right) {
            mid = (left + right) / 2;

            // If we find the k.
            if (arr[mid] == k) {
                break;
            } else if (arr[mid] > k) {

                // If we need minimum
                // element swap.
                if (pos > mid) {
                    need_minimum++;
                } else // Else the element is
                // at the right position.
                {
                    num_min--;
                }

                left = mid + 1;
            } else {
                if (pos < mid) // If we need maximum
                // element swap.
                {
                    need_maximum++;
                } else // Else element is at
                // the right position
                {
                    num_max--;
                }

                right = mid - 1;
            }
        }

        // Calculating the required swaps.
        if (need_minimum > need_maximum) {
            swaps = swaps + need_maximum;
            num_min = num_min - need_maximum;
            need_minimum = need_minimum - need_maximum;
            need_maximum = 0;
        } else {
            swaps = swaps + need_minimum;
            num_max = num_max - need_minimum;
            need_maximum = need_maximum - need_minimum;
            need_minimum = 0;
        }

        // If it is impossible.
        if (need_maximum > num_max || need_minimum > num_min) {
            return -1;
        } else {
            return (swaps + need_maximum + need_minimum);
        }
    }

// Driver function
    public static void main(String[] args) {

        int arr[] = {3, 10, 6, 7, 2, 5, 4}, k = 4;
        int n = arr.length;
        System.out.println(findMinimumSwaps(arr, n, k));
    }

}

/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 program to find Minimum number
# of swaps to get the position of
# the element if we provide an
# unsorted array to binary search.

# Function to find minimum swaps.
def findMinimumSwaps(arr,
                     n, k):

    num_min = num_max = need_minimum = 0
    need_maximum = swaps = 0

    # Here we are getting number of
    # smaller and greater elements of k.
    for i in range(n):
        if (arr[i] < k):
            num_min += 1

        elif (arr[i] > k):
            num_max += 1

    # Here we are calculating the actual
    # position of k in the array.
    for i in range(n):
        if (arr[i] == k):
            pos = i
            break

    left = 0
    right = n - 1

    # Implementing binary search as
    # per the above-discussed cases.
    while (left <= right):
        mid = (left + right) // 2

        # If we find the k.
        if (arr[mid] == k):
            break

        elif (arr[mid] > k):
            # If we need minimum
            # element swap.
            if (pos > mid):
                need_minimum += 1

            else:

                # Else the element is
                # at the right position.
                num_min -= 1

            left = mid + 1

        else:
            if (pos < mid):

                # If we need maximum
                # element swap.
                need_maximum += 1

            else:

                # Else element is at
                # the right position
                num_max -= 1

            right = mid - 1

    # Calculating the required swaps.
    if (need_minimum > need_maximum):
        swaps = swaps + need_maximum
        num_min = num_min - need_maximum
        need_minimum = (need_minimum -
                        need_maximum)
        need_maximum = 0

    else:
        swaps = swaps + need_minimum
        num_max = num_max - need_minimum
        need_maximum = (need_maximum -
                        need_minimum)
        need_minimum = 0

    # If it is impossible.
    if (need_maximum > num_max or
        need_minimum > num_min):
        return -1

    else:
        return (swaps + need_maximum +
                need_minimum)

# Driver function
if __name__ == "__main__":

    arr = [3, 10, 6, 7, 2, 5, 4]
    k = 4
    n = len(arr)
    print(findMinimumSwaps(arr, n, k))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find Minimum number
// of swaps to get the position of
// the element if we provide an
// unsorted array to binary search.

using System;
public class GFG{

// Function to find minimum swaps.
    static int findMinimumSwaps(int[] arr, int n,
            int k) {
        int pos = 0, num_min, num_max,
                need_minimum, need_maximum, swaps;
        num_min = num_max = need_minimum = 0;
        need_maximum = swaps = 0;

        // Here we are getting number of
        // smaller and greater elements of k.
        for (int i = 0; i < n; i++) {
            if (arr[i] < k) {
                num_min++;
            } else if (arr[i] > k) {
                num_max++;
            }
        }

        // Here we are calculating the actual
        // position of k in the array.
        for (int i = 0; i < n; i++) {
            if (arr[i] == k) {
                pos = i;
                break;
            }
        }

        int left, right, mid;
        left = 0;
        right = n - 1;

        // Implementing binary search as
        // per the above-discussed cases.
        while (left <= right) {
            mid = (left + right) / 2;

            // If we find the k.
            if (arr[mid] == k) {
                break;
            } else if (arr[mid] > k) {

                // If we need minimum
                // element swap.
                if (pos > mid) {
                    need_minimum++;
                } else // Else the element is
                // at the right position.
                {
                    num_min--;
                }

                left = mid + 1;
            } else {
                if (pos < mid) // If we need maximum
                // element swap.
                {
                    need_maximum++;
                } else // Else element is at
                // the right position
                {
                    num_max--;
                }

                right = mid - 1;
            }
        }

        // Calculating the required swaps.
        if (need_minimum > need_maximum) {
            swaps = swaps + need_maximum;
            num_min = num_min - need_maximum;
            need_minimum = need_minimum - need_maximum;
            need_maximum = 0;
        } else {
            swaps = swaps + need_minimum;
            num_max = num_max - need_minimum;
            need_maximum = need_maximum - need_minimum;
            need_minimum = 0;
        }

        // If it is impossible.
        if (need_maximum > num_max || need_minimum > num_min) {
            return -1;
        } else {
            return (swaps + need_maximum + need_minimum);
        }
    }

// Driver function
    public static void Main() {

        int []arr = {3, 10, 6, 7, 2, 5, 4};
        int k = 4;
        int n = arr.Length;
        Console.WriteLine(findMinimumSwaps(arr, n, k));
    }

}

/*This code is contributed by PrinciRaj1992*/
```

## java 描述语言

```
<script>
    // Javascript program to find Minimum number
    // of swaps to get the position of
    // the element if we provide an
    // unsorted array to binary search.

    // Function to find minimum swaps.
    function findMinimumSwaps(arr, n, k)
    {
        let pos, num_min, num_max,
        need_minimum, need_maximum, swaps;
        num_min = num_max = need_minimum = 0;
        need_maximum = swaps = 0;

        // Here we are getting number of
        // smaller and greater elements of k.
        for (let i = 0; i < n; i++) {
            if (arr[i] < k)
                num_min++;

            else if (arr[i] > k)
                num_max++;
        }

        // Here we are calculating the actual
        // position of k in the array.
        for (let i = 0; i < n; i++) {
            if (arr[i] == k) {
                pos = i;
                break;
            }
        }

        let left, right, mid;
        left = 0;
        right = n - 1;

        // Implementing binary search as
        // per the above-discussed cases.
        while (left <= right) {
            mid = parseInt((left + right) / 2, 10);

            // If we find the k.
            if (arr[mid] == k) {
                break;
            }

            else if (arr[mid] > k) {

                // If we need minimum
                // element swap.
                if (pos > mid)
                    need_minimum++;

                else

                    // Else the element is
                    // at the right position.
                    num_min--;

                left = mid + 1;
            }

            else {
                if (pos < mid)

                    // If we need maximum
                    // element swap.
                    need_maximum++;

                else

                    // Else element is at
                    // the right position
                    num_max--;

                right = mid - 1;
            }
        }

        // Calculating the required swaps.
        if (need_minimum > need_maximum) {
            swaps = swaps + need_maximum;
            num_min = num_min - need_maximum;
            need_minimum = need_minimum - need_maximum;
            need_maximum = 0;
        }

        else {
            swaps = swaps + need_minimum;
            num_max = num_max - need_minimum;
            need_maximum = need_maximum - need_minimum;
            need_minimum = 0;
        }

        // If it is impossible.
        if (need_maximum > num_max || need_minimum > num_min)
            return -1;

        else
            return (swaps + need_maximum + need_minimum);
    }

    let arr = [ 3, 10, 6, 7, 2, 5, 4 ], k = 4;
    let n = arr.length;
    document.write(findMinimumSwaps(arr, n, k));

    // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
2
```