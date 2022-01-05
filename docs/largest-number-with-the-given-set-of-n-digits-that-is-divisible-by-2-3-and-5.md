# 给定 N 位数集合中可被 2、3 和 5 整除的最大数字

> 原文:[https://www . geeksforgeeks . org/给定 n 位数可被 2-3-5 整除的最大数/](https://www.geeksforgeeks.org/largest-number-with-the-given-set-of-n-digits-that-is-divisible-by-2-3-and-5/)

给定一组**‘N’**数字。任务是从这些数字中找出我们能得到的最大整数。结果数必须能被 2、3 和 5 整除。
**注:**不需要使用集合中的所有数字。此外，前导零是不允许的。
**例:**

> **输入:** N = 11，setOfDigits = {3，4，5，4，5，3，5，3，4，4，0}
> **输出:** 5554443330
> 将所有元素按非递增顺序排列为 5，5，5，4，4，4，4，3，3，3，0 后。所有数字的总和是 40。因此，当我们发现 40 的余数被 3 除时，就是 1。然后我们将开始从头到尾遍历，如果我们遇到任何具有相同余数的数字，我们在位置 7 得到 4，它将被删除。现在总和是 36，可被 3 整除，新的最大数字将是 5554443330，可被 2、3 和 5 整除。
> **输入:** N = 1，setOfDigits = {0}
> **输出:** 0

**方法:**下面是解决这个问题的分步算法:

1.  初始化向量中的一组数字。
2.  任何一个数都可以被 2、3 和 5 整除，前提是数字的总和可以被 3 整除，并且最后一个数字是 0。
3.  如果向量中不存在 0，那么就不可能创建一个数，因为它不能被 5 整除。
4.  如果其后的第一个元素为 0，则以非递增方式对向量进行排序，然后打印 0。
5.  用 3 求所有数字和的模，如果是 1，则删除第一个具有相同余数的元素，同时从末尾遍历。
6.  如果没有余数相同的元素，则删除余数为*3–y*的两个元素。
7.  将向量的所有剩余数字打印为一个整数。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Function to find the largest
// integer with the given set
int findLargest(int n, vector<int>& v)
{

    int flag = 0;
    ll sum = 0;

    // find sum of all the digits
    // look if any 0 is present or not
    for (int i = 0; i < n; i++) {
        if (v[i] == 0)
            flag = 1;
        sum += v[i];
    }

    // if 0 is not present, the resultant number
    // won't be divisible by 5
    if (!flag)
        cout << "Not possible" << endl;

    else {
        // sort all the elements in a non-decreasing manner
        sort(v.begin(), v.end(), greater<int>());

        // if there is just one element 0
        if (v[0] == 0) {
            cout << "0" << endl;
            return 0;
        }
        else {
            int flag = 0;

            // find the remainder of the sum
            // of digits when divided by 3
            int y = sum % 3;

            // there can a remainder as 1 or 2
            if (y != 0) {

                // traverse from the end of the digits
                for (int i = n - 1; i >= 0; i--) {

                    // first element which has the same remainder
                    // remove it
                    if (v[i] % 3 == y) {
                        v.erase(v.begin() + i);
                        flag = 1;
                        break;
                    }
                }
                // if there is no element which
                // has a same remainder as y
                if (flag == 0) {

                    // subtract it by 3 ( could be one or two)
                    y = 3 - y;

                    int cnt = 0;
                    for (int i = n - 1; i >= 0; i--) {

                        // delete two minimal digits
                        // which has a remainder as y
                        if (v[i] % 3 == y) {
                            v.erase(v.begin() + i);
                            cnt++;

                            if (cnt >= 2)
                                break;
                        }
                    }
                }
            }
            if (*v.begin() == 0)
                cout << "0" << endl;

            // print all the digits as a single integer
            else
                for (int i : v) {
                    cout << i;
                }
        }
    }
}

// Driver code
int main()
{
    // initialize the number of set of digits
    int n = 11;

    // initialize all the set of digits in a vector
    vector<int> v{ 3, 9, 9, 6, 4, 3, 6, 4, 9, 6, 0 };

    findLargest(n, v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG {

    // Function to find the largest
    // integer with the given set
    static int findLargest(int n, Vector<Integer> v)
    {

        int flag = 0;
        long sum = 0;

        // find sum of all the digits
        // look if any 0 is present or not
        for (int i = 0; i < n; i++) {
            if (v.get(i) == 0)
                flag = 1;
            sum += v.get(i);
        }

        // if 0 is not present, the resultant number
        // won't be divisible by 5
        if (flag != 1)
            System.out.println("Not possible");

        else {
            // sort all the elements in a non-decreasing manner
            Collections.sort(v, Collections.reverseOrder());

            // if there is just one element 0
            if (v.get(0) == 0) {
                System.out.println("0");
                return 0;
            }
            else {
                int flags = 0;

                // find the remainder of the sum
                // of digits when divided by 3
                int y = (int)(sum % 3);

                // there can a remainder as 1 or 2
                if (y != 0) {

                    // traverse from the end of the digits
                    for (int i = n - 1; i >= 0; i--) {

                        // first element which has the same remainder
                        // remove it
                        if (v.get(i) % 3 == y) {
                            v.remove(i);
                            flags = 1;
                            break;
                        }
                    }

                    // if there is no element which
                    // has a same remainder as y
                    if (flags == 0) {

                        // subtract it by 3 ( could be one or two)
                        y = 3 - y;

                        int cnt = 0;
                        for (int i = n - 1; i >= 0; i--) {

                            // delete two minimal digits
                            // which has a remainder as y
                            if (v.get(i) % 3 == y) {
                                v.remove(i);
                                cnt++;

                                if (cnt >= 2)
                                    break;
                            }
                        }
                    }
                }
                if (v.get(0) == 0)
                    System.out.println("0");

                // print all the digits as a single integer
                else
                    for (Integer i : v) {
                        System.out.print(i);
                    }
            }
        }
        return Integer.MIN_VALUE;
    }

    // Driver code
    public static void main(String[] args)
    {
        // initialize the number of set of digits
        int arr[] = { 3, 9, 9, 6, 4, 3, 6, 4, 9, 6, 0 };
        int n = 11;

        Vector<Integer> v = new Vector<Integer>();

        // initialize all the set of digits in a vector
        for (int i = 0; i < n; i++)
            v.add(i, arr[i]);

        findLargest(n, v);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to find the largest
# integer with the given set
def findLargest(n, v):
    flag = 0
    sum = 0

    # find sum of all the digits
    # look if any 0 is present or not
    for i in range(n):
        if (v[i] == 0):
            flag = 1
        sum += v[i]

    # if 0 is not present, the resultant number
    # won't be divisible by 5
    if (flag == 0):
        print("Not possible")

    else:

        # sort all the elements in a
        # non-decreasing manner
        v.sort(reverse = True)

        # if there is just one element 0
        if (v[0] == 0):
            print("0")
            return 0

        else:
            flag = 0

            # find the remainder of the sum
            # of digits when divided by 3
            y = sum % 3

            # there can a remainder as 1 or 2
            if (y != 0):

                # traverse from the end of the digits
                i = n - 1
                while(i >= 0):

                    # first element which has the same
                    # remainder, remove it
                    if (v[i] % 3 == y):
                        v.remove(v[i])
                        flag = 1
                        break
                    i -= 1

                # if there is no element which
                # has a same remainder as y
                if (flag == 0):

                    # subtract it by 3 ( could be one or two)
                    y = 3 - y

                    cnt = 0
                    i = n - 1
                    while(i >= 0):

                        # delete two minimal digits
                        # which has a remainder as y
                        if (v[i] % 3 == y):
                            v.remove(v[i])
                            cnt += 1

                            if (cnt >= 2):
                                break

                        i -= 1

            # print all the digits as a single integer
            for i in (v):
               print(i, end = "")

# Driver code
if __name__ == '__main__':

    # initialize the number of set of digits
    n = 11

    # initialize all the set of
    # digits in a vector
    v = [3, 9, 9, 6, 4, 3,
            6, 4, 9, 6, 0]

    findLargest(n, v)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG {

    // Function to find the largest
    // integer with the given set
    static int findLargest(int n, ArrayList v)
    {

        int flag = 0;
        long sum = 0;

        // find sum of all the digits
        // look if any 0 is present or not
        for (int i = 0; i < n; i++) {
            if ((int)v[i] == 0)
                flag = 1;
            sum += (int)v[i];
        }

        // if 0 is not present, the resultant number
        // won't be divisible by 5
        if (flag != 1)
            Console.WriteLine("Not possible");

        else {
            // sort all the elements in a non-decreasing manner
            v.Sort();
            v.Reverse();

            // if there is just one element 0
            if ((int)v[0] == 0) {
                Console.WriteLine("0");
                return 0;
            }
            else {
                int flags = 0;

                // find the remainder of the sum
                // of digits when divided by 3
                int y = (int)(sum % 3);

                // there can a remainder as 1 or 2
                if (y != 0) {

                    // traverse from the end of the digits
                    for (int i = n - 1; i >= 0; i--) {

                        // first element which has the same remainder
                        // remove it
                        if ((int)v[i] % 3 == y) {
                            v.RemoveAt(i);
                            flags = 1;
                            break;
                        }
                    }

                    // if there is no element which
                    // has a same remainder as y
                    if (flags == 0) {

                        // subtract it by 3 ( could be one or two)
                        y = 3 - y;

                        int cnt = 0;
                        for (int i = n - 1; i >= 0; i--) {

                            // delete two minimal digits
                            // which has a remainder as y
                            if ((int)v[i] % 3 == y) {
                                v.RemoveAt(i);
                                cnt++;

                                if (cnt >= 2)
                                    break;
                            }
                        }
                    }
                }
                if ((int)v[0] == 0)
                    Console.WriteLine("0");

                // print all the digits as a single integer
                else
                    for (int i = 0; i < v.Count; i++) {
                        Console.Write(v[i]);
                    }
            }
        }
        return int.MinValue;
    }

    // Driver code
    static void Main()
    {
        // initialize the number of set of digits
        int[] arr = { 3, 9, 9, 6, 4, 3, 6, 4, 9, 6, 0 };
        int n = 11;

        ArrayList v = new ArrayList();

        // initialize all the set of digits in a vector
        for (int i = 0; i < n; i++)
            v.Add(arr[i]);

        findLargest(n, v);
    }
}

// This code contributed by mits
```

**Output:** 

```
999666330
```

**替代解决方案:**
下面是华盛顿州西雅图市基冈·费希尔的一个实现

## C++

```
#include <bits/stdc++.h>
using namespace std;

// return a String representing the largest value that is
// both a combination of the values from the parameter array
// "vals" and divisible by 2, 3, and 5.
string findLargest(int vals[], int N)
{

    // sort the array in ascending order
    sort(vals, vals + N);
    string sb;

    // index of the lowest value divisible by 3 in "vals"
    // if not present, no possible value
    int index_div_3 = -1;

    // if a zero is not found, no possible value
    bool zero = false;

    // find minimum multiple of 3 and check for 0
    for (int i = 0; i < N; i++)
    {

        // break when finding the first multiple of 3
        // which is minimal due to sort in asc order
        if (vals[i] % 3 == 0 && vals[i] != 0)
        {
            index_div_3 = i;
            break;
        }
        if (vals[i] == 0)
        {
            zero = true;
        }
    }

    // if no multiple of 3 or no zero, then no value
    if (index_div_3 == -1 || !zero)
    {
        return sb;
    }

    // construct the output StringBuilder
    // adding the values to the string from highest
    // to lowest, not adding the val[index_div_3]
    // until reaching the 0s in the array, at which
    // point add the multiple of 3 followed by
    // any 0s in the array
    for (int i = N - 1; i >= 0; i--)
    {
        if (i != index_div_3)
        {
            if (vals[i] == 0 && index_div_3 != -1)
            {
                sb = sb + to_string(vals[index_div_3]);
                sb = sb + to_string(vals[i]);
                index_div_3 = -1;
            }
            else
            {
                sb = sb + to_string(vals[i]);
            }
        }
    }
    return sb;
}

int main()
{
    int vals[] = { 0, 0, 0, 2, 3, 4, 2, 7, 6, 9 };
    int N = sizeof(vals) / sizeof(vals[0]);
    cout << "Output = " << findLargest(vals, N) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

class GFG {
    // Driver
    public static void main()
    {
        int[] vals = { 0, 0, 0, 2, 3, 4, 2, 7, 6, 9 };
        System.out.println("Output = " + findLargest(vals));
    }

    // return a String representing the largest value that is
    // both a combination of the values from the parameter array
    // "vals" and divisible by 2, 3, and 5.
    public static String findLargest(int[] vals)
    {
        // sort the array in ascending order
        Arrays.sort(vals);
        StringBuilder sb = new StringBuilder();

        // index of the lowest value divisible by 3 in "vals"
        // if not present, no possible value
        int index_div_3 = -1;

        // if a zero is not found, no possible value
        boolean zero = false;

        // find minimum multiple of 3 and check for 0
        for (int i = 0; i < vals.length; i++) {

            // break when finding the first multiple of 3
            // which is minimal due to sort in asc order
            if (vals[i] % 3 == 0 && vals[i] != 0) {
                index_div_3 = i;
                break;
            }
            if (vals[i] == 0) {
                zero = true;
            }
        }

        // if no multiple of 3 or no zero, then no value
        if (index_div_3 == -1 || !zero) {
            return sb.toString();
        }

        // construct the output StringBuilder
        // adding the values to the string from highest
        // to lowest, not adding the val[index_div_3]
        // until reaching the 0s in the array, at which
        // point add the multiple of 3 followed by
        // any 0s in the array
        for (int i = vals.length - 1; i >= 0; i--) {
            if (i != index_div_3) {
                if (vals[i] == 0 && index_div_3 != -1) {
                    sb.append(vals[index_div_3]);
                    sb.append(vals[i]);
                    index_div_3 = -1;
                }
                else {
                    sb.append(vals[i]);
                }
            }
        }
        return sb.toString();
    }
}
```

## 蟒蛇 3

```
# Return a String representing the largest
# value that is both a combination of the
# values from the parameter array
# "vals" and divisible by 2, 3, and 5.
def findLargest (vals):

    # Sort the array in ascending order
    vals.sort()
    sb = ""

    # Index of the lowest value divisible
    # by 3 in "vals" if not present, no
    # possible value
    index_div_3 = -1

    # If a zero is not found, no possible value
    zero = False

    # Find minimum multiple of 3 and check for 0
    for i in range(len(vals)):

        # Break when finding the first
        # multiple of 3 which is minimal
        # due to sort in asc order
        if (vals[i] % 3 == 0 and vals[i] != 0):
            index_div_3 = i
            break

        if (vals[i] == 0):
            zero = True

    # If no multiple of 3 or no zero, then no value
    if (index_div_3 == -1 or zero == False):
        return str(sb)

    # Construct the output String by
    # adding the values to the string from highest
    # to lowest, not adding the val[index_div_3]
    # until reaching the 0s in the array, at which
    # point add the multiple of 3 followed by
    # any 0s in the array
    for i in range(len(vals) - 1, -1, -1):
        if (i != index_div_3):

            if (vals[i] == 0 and index_div_3 != -1):
                sb += str(vals[index_div_3])
                sb += str(vals[i])
                index_div_3 = -1
            else:
                sb += str(vals[i])

    return str(sb)

# Driver code
if __name__ == '__main__':

    vals = [ 0, 0, 0, 2, 3, 4, 2, 7, 6, 9 ]

    print("Output =", findLargest(vals))

# This code is contributed by himanshu77
```

## C#

```
using System;
using System.Text;
class GFG
{
    // Driver
    public static void Main()
    {
        int[] vals = { 0, 0, 0, 2, 3, 4, 2, 7, 6, 9 };
        Console.WriteLine("Output = " + findLargest(vals));
    }

    // return a String representing the largest value that is
    // both a combination of the values from the parameter array
    // "vals" and divisible by 2, 3, and 5.
    public static string findLargest(int[] vals)
    {
        // sort the array in ascending order
        Array.Sort(vals);
        StringBuilder sb = new StringBuilder();

        // index of the lowest value divisible by 3 in "vals"
        // if not present, no possible value
        int index_div_3 = -1;

        // if a zero is not found, no possible value
        bool zero = false;

        // find minimum multiple of 3 and check for 0
        for (int i = 0; i < vals.Length; i++) {

            // break when finding the first multiple of 3
            // which is minimal due to sort in asc order
            if (vals[i] % 3 == 0 && vals[i] != 0) {
                index_div_3 = i;
                break;
            }
            if (vals[i] == 0) {
                zero = true;
            }
        }

        // if no multiple of 3 or no zero, then no value
        if (index_div_3 == -1 || !zero) {
            return sb.ToString();
        }

        // construct the output StringBuilder
        // adding the values to the string from highest
        // to lowest, not adding the val[index_div_3]
        // until reaching the 0s in the array, at which
        // point add the multiple of 3 followed by
        // any 0s in the array
        for (int i = vals.Length - 1; i >= 0; i--) {
            if (i != index_div_3) {
                if (vals[i] == 0 && index_div_3 != -1) {
                    sb.Append(vals[index_div_3]);
                    sb.Append(vals[i]);
                    index_div_3 = -1;
                }
                else {
                    sb.Append(vals[i]);
                }
            }
        }
        return sb.ToString();
    }
}

// This code is contributed by SoumikMondal
```

**Output:** 

```
Output = 9764223000
```