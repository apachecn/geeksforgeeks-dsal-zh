# 第一句最小字符的出现频率小于第二句

> 原文:[https://www . geesforgeks . org/第一句中最小字符的出现频率小于第二句中最小字符的出现频率/](https://www.geeksforgeeks.org/frequency-of-smallest-character-in-first-sentence-less-than-that-of-second-sentence/)

给定两个[字符串数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)、**arr 1【】**和**arr 2【】**，任务是计算**arr 2【】**中最小字符频率小于**arr 1【】**中每个字符串最小字符频率的字符串数量。

**示例:**

> **输入:**arr 1[]= {“cbd”}，arr 2[]= {“zaaaz”}
> **输出:** 1
> **说明:**
> 最小字符在“CBD”中出现的频率为 1，小于最小字符在“zaaaz”中出现的频率为 2。
> 因此，字符串“cbd”的总计数为 1。
> 
> **输入:**arr 1[]= {“yyy”、“ZZ”}，arr 2[]= {“x”、“xx”、“xxx”、“xxxx”}
> T3】输出:1 2
> T6】解释:T8】1。“yyy”中最小字符的出现频率为 3，小于“xxxx”中最小字符的出现频率 4。
> 因此，字符串“yyy”的总计数为 1。
> 2。“zz”中最小字符的出现频率为 2，小于“xxx”和“xxxx”中最小字符的出现频率，分别为 3 和 4。
> 因此，字符串“zz”的总计数为 2。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  对于数组中的每个字符串， **arr2[]** [计算最小字符的频率](https://www.geeksforgeeks.org/basic/frequency-counting/)并将其存储在数组中(比如说 **freq[]** )。
2.  排序频率数组 **freq[]** 。
3.  现在，对于数组 **arr1[]** 中的每个字符串，计算字符串中[最小字符的出现频率(比如说 **X** )。](https://www.geeksforgeeks.org/program-to-find-the-largest-and-smallest-ascii-valued-characters-in-a-string/)
4.  对于每个 **X** ，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)通过本文[讨论的方法](https://www.geeksforgeeks.org/find-the-number-of-elements-greater-than-k-in-a-sorted-array/)找到**freq【】**中大于 X 的元素数量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the frequency of
// minimum character
int countMinFreq(string s)
{

    // Sort the string s
    sort(s.begin(), s.end());

    // Return the count with smallest
    // character
    return count(s.begin(), s.end(), s[0]);
}

// Function to count number of frequency
// of smallest character of string arr1[]
// is less than the string in arr2[]
void countLessThan(vector<string>& arr1,
                   vector<string>& arr2)
{
    // To store the frequency of smallest
    // character in each string of arr2
    vector<int> freq;

    // Traverse the arr2[]
    for (string s : arr2) {

        // Count the frequency of smallest
        // character in string s
        int f = countMinFreq(s);

        // Append the frequency to freq[]
        freq.push_back(f);
    }

    // Sort the frequency array
    sort(freq.begin(), freq.end());

    // Traverse the array arr1[]
    for (string s : arr1) {

        // Count the frequency of smallest
        // character in string s
        int f = countMinFreq(s);

        // find the element greater than f
        auto it = upper_bound(freq.begin(),
                              freq.end(), f);

        // Find the count such that
        // arr1[i] < arr2[j]
        int cnt = freq.size()
                  - (it - freq.begin());

        // Print the count
        cout << cnt << ' ';
    }
}

// Driver Code
int main()
{

    vector<string> arr1, arr2;
    arr1 = { "yyy", "zz" };
    arr2 = { "x", "xx", "xxx", "xxxx" };

    // Function Call
    countLessThan(arr1, arr2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to count the frequency of
  // minimum character
  static int countMinFreq(String s)
  {

    // Sort the string s
    char[] tempArray = s.toCharArray();
    Arrays.sort(tempArray);
    s = new String(tempArray);

    // Return the count with smallest
    // character
    int x = 0;
    for (int i = 0; i < s.length(); i++)
      if (s.charAt(i) == s.charAt(0))
        x++;
    return x;
  }

  // Function to count number of frequency
  // of smallest character of string arr1[]
  // is less than the string in arr2[]
  static void countLessThan(List<String> arr1,
                            List<String> arr2)
  {

    // To store the frequency of smallest
    // character in each string of arr2
    List<Integer> freq = new ArrayList<Integer>();

    // Traverse the arr2[]
    for (String s : arr2)
    {

      // Count the frequency of smallest
      // character in string s
      int f = countMinFreq(s);

      // Append the frequency to freq[]
      freq.add(f);
    }

    // Sort the frequency array
    Collections.sort(freq);

    // Traverse the array arr1[]
    for (String s : arr1) {

      // Count the frequency of smallest
      // character in string s
      int f = countMinFreq(s);

      // find the element greater than f
      int it = upper_bound(freq, f);

      // Find the count such that
      // arr1[i] < arr2[j]
      int cnt = freq.size() - it;

      // Print the count
      System.out.print(cnt + " ");
    }
  }

  static int upper_bound(List<Integer> freq, int f)
  {
    int low = 0, high = freq.size() - 1;

    while (low < high) {
      int mid = (low + high) / 2;
      if (freq.get(mid) > f)
        high = mid;
      else
        low = mid + 1;
    }

    return (freq.get(low) < f) ? low++ : low;
  }

  // Driver Code
  public static void main(String[] args)
  {
    List<String> arr1, arr2;
    arr1 = Arrays.asList(new String[] { "yyy", "zz" });
    arr2 = Arrays.asList(
      new String[] { "x", "xx", "xxx", "xxxx" });

    // Function Call
    countLessThan(arr1, arr2);
  }
}

// This code is contributed by jithin.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_right as upper_bound

# Function to count the frequency
# of minimum character
def countMinFreq(s):

    # Sort the string s
    s = sorted(s)

    # Return the count with smallest
    # character
    x = 0
    for i in s:
        if i == s[0]:
            x += 1
    return x

# Function to count number of frequency
# of smallest character of string arr1[]
# is less than the string in arr2[]
def countLessThan(arr1, arr2):

    # To store the frequency of smallest
    # character in each string of arr2
    freq = []

    # Traverse the arr2[]
    for s in arr2:

        # Count the frequency of smallest
        # character in string s
        f = countMinFreq(s)

        # Append the frequency to freq[]
        freq.append(f)

    # Sort the frequency array
    feq = sorted(freq)

    # Traverse the array arr1[]
    for s in arr1:

        # Count the frequency of smallest
        # character in string s
        f = countMinFreq(s);

        # find the element greater than f
        it = upper_bound(freq,f)

        # Find the count such that
        # arr1[i] < arr2[j]
        cnt = len(freq)-it

        # Print the count
        print(cnt, end = " ")

# Driver Code
if __name__ == '__main__':

    arr1 = ["yyy", "zz"]
    arr2 = [ "x", "xx", "xxx", "xxxx"]

    # Function Call
    countLessThan(arr1, arr2);

# This code is contributed by Mohit Kumar
```

## java 描述语言

```
<script>

// JS program for the above approach
function upper_bound(freq, f)
{
    let low = 0, high = freq.length - 1;

    while (low < high) {
        let mid = Math.floor((low + high) / 2);
        if (freq[mid] > f)
            high = mid;
          else
            low = mid + 1;
    }

    return (freq[low] < f) ? low++ : low;
}
// Function to count the frequency of
// minimum character
function countMinFreq(s)
{

    // Sort the string s
    s = s.split('').sort().join('');
    // Return the count with smallest
    // character
    let x = 0;
    for(let i=0;i<s.length;i++){
        if(s[i] == s[0])
            x += 1;
    }
    return x;
}

// Function to count number of frequency
// of smallest character of string arr1[]
// is less than the string in arr2[]
function countLessThan(arr1,arr2)
{
    // To store the frequency of smallest
    // character in each string of arr2
    let freq = [];

    // Traverse the arr2[]
    for (let i = 0;i< arr2.length;i++) {

        // Count the frequency of smallest
        // character in string s
        let f = countMinFreq(arr2[i]);

        // Append the frequency to freq[]
        freq.push(f);
    }

    // Sort the frequency array
    freq= freq.sort(function(a,b){return a-b});
    // Traverse the array arr1[]
    for (let i = 0;i< arr1.length;i++) {

        // Count the frequency of smallest
        // character in string s
        let f = countMinFreq(arr1[i]);

        // find the element greater than f
        let it = upper_bound(freq, f);

        // Find the count such that
        // arr1[i] < arr2[j]
        let cnt = freq.length
                  - (it);

        // Print the count
        document.write(cnt,' ');
    }
}

// Driver Code
let arr1, arr2;
arr1 = [ "yyy", "zz" ];
arr2 = [ "x", "xx", "xxx", "xxxx" ];

// Function Call
countLessThan(arr1, arr2);

</script>
```

**Output:** 

```
1 2
```

***时间复杂度:** O(N + M*log M)* ，其中 N 和 M 分别是给定数组的长度。

***辅助空间:**O(M)*T4】