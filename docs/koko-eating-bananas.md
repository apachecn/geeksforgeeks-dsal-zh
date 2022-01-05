# 科科吃香蕉

> 原文:[https://www.geeksforgeeks.org/koko-eating-bananas/](https://www.geeksforgeeks.org/koko-eating-bananas/)

考虑到第 N 堆香蕉，第 I 堆有一堆香蕉和 **H** 小时，直到守卫回来(第 N < H)。找到每小时能吃的最少( **S** )香蕉，这样 Koko 就能在 **H** 小时内吃完所有香蕉。每一个小时，科科都会选择一堆香蕉，然后从那堆香蕉中吃下 **S** 香蕉。如果堆里的香蕉少于 **S** ，那么她就全部吃光，那一个小时内不会再吃香蕉了。

**示例:**

> **输入:**成堆=【3，6，7，11】，H = 8
> **输出:** 4
> **说明:** Koko 每小时会吃 4 根香蕉，把香蕉全部吃完
> 
> **输入:**成堆=【30，11，23，4，20】，H = 6
> **输出:** 23
> **说明:** Koko 每小时会吃 23 根香蕉才能吃完所有的香蕉

**天真的做法:**科科每小时至少要吃一根香蕉。让下界成为**开始**。Koko 一个小时能吃的最大香蕉数是所有堆中香蕉的最大数量。这是 **S** 的最大可能值。让上限结束。具有从**开始**到**结束**的搜索间隔，并且使用线性搜索，对于 **S** 的每个值，可以检查这个吃香蕉的速度是否有效。 **S** 的第一个有效值将是最慢的速度和想要的答案。

**时间复杂度:** O(N * W)，其中 **W** 是所有香蕉堆中最大的香蕉

**方法:**在答题技巧上使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以高效地解决给定的问题:

*   创建一个布尔函数，检查选择的速度(香蕉/小时)是否足以在给定的 **H** 小时内吃掉所有香蕉
*   **S** 的下限是 1 个香蕉/小时，因为 Koko 每小时必须吃一个香蕉，上限是所有堆的最大香蕉数
*   将二分搜索法应用于可能的答案范围，以获得 S 的最小值
    *   如果布尔函数满足中间值，则将较高值减少到中间值
    *   否则将下限更新为中间+ 1

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

bool check(vector<int>& bananas, int mid_val, int H)
{
    int time = 0;
    for (int i = 0; i < bananas.size(); i++) {

        // to get the ceil value
        if (bananas[i] % mid_val != 0) {

            // in case of odd number
            time += ((bananas[i] / mid_val) + 1);
        }
        else {

            // in case of even number
            time += (bananas[i] / mid_val);
        }
    }

    // check if time is less than
    // or equals to given hour
    if (time <= H) {
        return true;
    }
    else {
        return false;
    }
}

int minEatingSpeed(vector<int>& piles, int H)
{

    // as minimum speed of eating must be 1
    int start = 1;

    // Maximum speed of eating
    // is the maximum bananas in given piles
    int end = *max_element(piles.begin(), piles.end());

    while (start < end) {
        int mid = start + (end - start) / 2;

        // Check if the mid(hours) is valid
        if ((check(piles, mid, H)) == true) {

            // If valid continue to search
            // lower speed
            end = mid;
        }
        else {
            // If cant finish bananas in given
            // hours, then increase the speed
            start = mid + 1;
        }
    }
    return end;
}

// Driver code
int main()
{
    vector<int> piles = { 30, 11, 23, 4, 20 };
    int H = 6;
    cout << minEatingSpeed(piles, H);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.util.*;

class GFG{

static boolean check(int[] bananas, int mid_val, int H)
{
    int time = 0;
    for (int i = 0; i < bananas.length; i++) {

        // to get the ceil value
        if (bananas[i] % mid_val != 0) {

            // in case of odd number
            time += ((bananas[i] / mid_val) + 1);
        }
        else {

            // in case of even number
            time += (bananas[i] / mid_val);
        }
    }

    // check if time is less than
    // or equals to given hour
    if (time <= H) {
        return true;
    }
    else {
        return false;
    }
}

static int minEatingSpeed(int []piles, int H)
{

    // as minimum speed of eating must be 1
    int start = 1;

    // Maximum speed of eating
    // is the maximum bananas in given piles
    int end = Arrays.stream(piles).max().getAsInt();

    while (start < end) {
        int mid = start + (end - start) / 2;

        // Check if the mid(hours) is valid
        if ((check(piles, mid, H)) == true) {

            // If valid continue to search
            // lower speed
            end = mid;
        }
        else {
            // If cant finish bananas in given
            // hours, then increase the speed
            start = mid + 1;
        }
    }
    return end;
}

// Driver code
public static void main(String[] args)
{
    int []piles = { 30, 11, 23, 4, 20 };
    int H = 6;
    System.out.print(minEatingSpeed(piles, H));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation for the above approach
def check(bananas, mid_val, H):
  time = 0;
  for i in range(len(bananas)):

    # to get the ceil value
    if (bananas[i] % mid_val != 0):

      # in case of odd number
      time += bananas[i] // mid_val + 1;
    else:

      # in case of even number
      time += bananas[i] // mid_val

  # check if time is less than
  # or equals to given hour
  if (time <= H):
    return True;
  else:
    return False;

def minEatingSpeed(piles, H):
  # as minimum speed of eating must be 1
  start = 1;

  # Maximum speed of eating
  # is the maximum bananas in given piles
  end = sorted(piles.copy(), reverse=True)[0]

  while (start < end):
    mid = start + (end - start) // 2;

    # Check if the mid(hours) is valid
    if (check(piles, mid, H) == True):

      # If valid continue to search
      # lower speed
      end = mid;
    else:

      # If cant finish bananas in given
      # hours, then increase the speed
      start = mid + 1;
  return end;

# Driver code
piles = [30, 11, 23, 4, 20];
H = 6;
print(minEatingSpeed(piles, H));

# This code is contributed by gfgking.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Linq;
public class GFG{

static bool check(int[] bananas, int mid_val, int H)
{
    int time = 0;
    for (int i = 0; i < bananas.Length; i++) {

        // to get the ceil value
        if (bananas[i] % mid_val != 0) {

            // in case of odd number
            time += ((bananas[i] / mid_val) + 1);
        }
        else {

            // in case of even number
            time += (bananas[i] / mid_val);
        }
    }

    // check if time is less than
    // or equals to given hour
    if (time <= H) {
        return true;
    }
    else {
        return false;
    }
}

static int minEatingSpeed(int []piles, int H)
{

    // as minimum speed of eating must be 1
    int start = 1;

    // Maximum speed of eating
    // is the maximum bananas in given piles
    int end = piles.Max();

    while (start < end) {
        int mid = start + (end - start) / 2;

        // Check if the mid(hours) is valid
        if ((check(piles, mid, H)) == true) {

            // If valid continue to search
            // lower speed
            end = mid;
        }
        else {
            // If cant finish bananas in given
            // hours, then increase the speed
            start = mid + 1;
        }
    }
    return end;
}

// Driver code
public static void Main(String[] args)
{
    int []piles = { 30, 11, 23, 4, 20 };
    int H = 6;
    Console.Write(minEatingSpeed(piles, H));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

function check(bananas, mid_val, H) {
  let time = 0;
  for (let i = 0; i < bananas.length; i++) {
    // to get the ceil value
    if (bananas[i] % mid_val != 0) {
      // in case of odd number
      time += Math.floor(bananas[i] / mid_val) + 1;
    } else {
      // in case of even number
      time += Math.floor(bananas[i] / mid_val);
    }
  }

  // check if time is less than
  // or equals to given hour
  if (time <= H) {
    return true;
  } else {
    return false;
  }
}

function minEatingSpeed(piles, H) {
  // as minimum speed of eating must be 1
  let start = 1;

  // Maximum speed of eating
  // is the maximum bananas in given piles
  let end = [...piles].sort((a, b) => b - a)[0];

  while (start < end) {
    let mid = start + Math.floor((end - start) / 2);

    // Check if the mid(hours) is valid
    if (check(piles, mid, H) == true) {
      // If valid continue to search
      // lower speed
      end = mid;
    } else {
      // If cant finish bananas in given
      // hours, then increase the speed
      start = mid + 1;
    }
  }
  return end;
}

// Driver code

let piles = [30, 11, 23, 4, 20];
let H = 6;
document.write(minEatingSpeed(piles, H));

</script>
```

**Output**

```
23
```

**时间复杂度:** O(N log W) (W 是所有堆中香蕉的最大值)
T3】辅助空间: O(1)