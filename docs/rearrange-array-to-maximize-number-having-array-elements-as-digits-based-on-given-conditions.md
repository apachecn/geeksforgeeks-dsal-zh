# 根据给定条件重新排列数组，使数组元素的个数最大化

> 原文:[https://www . geeksforgeeks . org/rearray-array-to-number-having-array-elements-as-digits-based-on-conditions/](https://www.geeksforgeeks.org/rearrange-array-to-maximize-number-having-array-elements-as-digits-based-on-given-conditions/)

给定整数数组 **arr[]** 和长度为 **N** 的二进制字符串 **str** ，任务是通过从字符串中具有相同字符的索引中交换数组元素来重新排列给定的数组，使得重新排列的数组的元素以数字形式形成的数字是最大可能的。

**示例:**

> **输入:** arr[]={1，3，4，2}，str="0101"
> **输出:** 4 3 1 2
> **解释:**
> 既然 arr[0]小于 arr[2]，那就交换吧。因此，数组中最大可能的数字是 4、3、1、2。
> 
> **输入:** arr[] = { 1，3，456，6，7，8}，str = "101101"
> **输出:** 8 7 6 456 3 1
> **解释:**
> 出现在 0-c 索引处的数组元素:{3，7}
> 由上述两个数字组成的最大数量是 73
> 出现在 1-c 索引处的数组元素:{ 1，456，6，8 }

**接近**:按照以下步骤解决问题:

1.  创建两个数组来存储数组中的 0 字符索引元素和 1 字符索引元素。
2.  [对数组进行排序，从这两个数组中形成最大可能的数字](https://www.geeksforgeeks.org/given-an-array-of-numbers-arrange-the-numbers-to-form-the-biggest-number/)。
3.  迭代**字符串**，根据字符，从排序的数组中放置数组元素。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Comparison Function to sort()
int myCompare(int a, int b)
{
    string X = to_string(a);
    string Y = to_string(b);

    // Append Y at the end of X
    string XY = X.append(Y);

    // Append X at the end of Y
    string YX = Y.append(X);

    // Compare and return greater
    return XY.compare(YX) < 0 ? 1 : 0;
}

// Function to return the rearranged
// array in the form of largest
// possible number that can be formed
void findMaxArray(vector<int>& arr, string& str)
{
    int N = arr.size();
    vector<int> Z, O, ans(N);

    for (int i = 0; i < N; i++) {
        if (str[i] == '0') {
            Z.push_back(arr[i]);
        }

        else {
            O.push_back(arr[i]);
        }
    }

    // Sort them in decreasing order
    sort(Z.rbegin(), Z.rend(), myCompare);
    sort(O.rbegin(), O.rend(), myCompare);

    int j = 0, k = 0;

    // Generate the sorted array
    for (int i = 0; i < N; i++) {
        if (str[i] == '0') {
            ans[i] = Z[j++];
        }
        else {
            ans[i] = O[k++];
        }
    }

    for (int i = 0; i < N; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 3, 456, 6, 7, 8 };
    string str = "101101";
    findMaxArray(arr, str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to return the rearranged
// array in the form of largest
// possible number that can be formed
static void findMaxArray(int[] arr, String str)
{
    int N = arr.length;
    ArrayList<Integer> Z = new ArrayList<>(),
                       O = new ArrayList<>();

    int[] ans = new int[N];

    for(int i = 0; i < N; i++)
    {
        if (str.charAt(i) == '0')
        {
            Z.add(arr[i]);
        }
        else
        {
            O.add(arr[i]);
        }
    }

    // Sort them in decreasing order
    Collections.sort(Z, new Comparator<Integer>()
    {
        public int compare(Integer a, Integer b)
        {
            String X = Integer.toString(a);
            String Y = Integer.toString(b);

            // Append Y at the end of X
            String XY = X + Y;

            // Append X at the end of Y
            String YX = Y + X;

            // Compare and return greater
            return XY.compareTo(YX) > 0 ? -1 : 1;
        }
    });

    Collections.sort(O, new Comparator<Integer>()
    {
        public int compare(Integer a, Integer b)
        {
            String X = Integer.toString(a);
            String Y = Integer.toString(b);

            // Append Y at the end of X
            String XY = X + Y;

            // Append X at the end of Y
            String YX = Y + X;

            // Compare and return greater
            return XY.compareTo(YX) > 0 ? -1 : 1;
        }
    });

    int j = 0, k = 0;

    // Generate the sorted array
    for(int i = 0; i < N; i++)
    {
        if (str.charAt(i) == '0')
        {
            ans[i] = Z.get(j++);
        }
        else
        {
            ans[i] = O.get(k++);
        }
    }

    for(int i = 0; i < N; i++)
    {
        System.out.print(ans[i] + " ");
    }
}

// Driver code
public static void main (String[] args)
{
    int[] arr = { 1, 3, 456, 6, 7, 8 };
    String str = "101101";

    findMaxArray(arr, str);
}
}

// This code is contributed by offbeat
```

**Output:** 

```
8 7 6 456 3 1

```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*