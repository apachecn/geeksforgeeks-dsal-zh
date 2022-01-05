# 在给定的 N 个范围内找到从 1 到 M 的缺失元素| Set-2

> 原文:[https://www . geesforgeks . org/find-the-missing-elements-从-1 到-m-in-给定-n-ranges-set-2/](https://www.geeksforgeeks.org/find-the-missing-elements-from-1-to-m-in-given-n-ranges-set-2/)

给定一个相交和重叠的整数 *m* 和 *n* 范围(例如【a，b】)。任务是找出范围内不属于任何给定范围的所有数字。

**示例:**

> **输入:** m = 6，范围= {{1，2}，{4，5}}
> **输出:** 3 6
> 因为给定的范围中只缺少 3 和 6。
> 
> **输入:** m = 5，范围= {{2，4}}
> **输出:** 1 5

**方法 1:** 由于我们有 *n* 个范围，如果范围不重叠且不相交，则遵循此处[描述的方法](https://www.geeksforgeeks.org/find-the-missing-elements-from-1-to-m-in-given-n-ranges/)。
但是这里有重叠和交叉的范围，所以首先合并所有的范围，这样就没有重叠或交叉的范围了。
合并完成后，从每个范围迭代，找出缺失的数字。

下面是上述方法的实现:

**时间复杂度:O(nlogn)**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// function to find the missing
// numbers from the given ranges
void findNumbers(vector<pair<int, int> > ranges, int m)
{
    vector<int> ans;

    // prev is use to store end of last range
    int prev = 0;

    // j is used as counter for range
    for (int j = 0; j < ranges.size(); j++) {
        int start = ranges[j].first;
        int end = ranges[j].second;
        for (int i = prev + 1; i < start; i++)
            ans.push_back(i);
        prev = end;
    }

    // for last range
    for (int i = prev + 1; i <= m; i++)
        ans.push_back(i);

    // finally print all answer
    for (int i = 0; i < ans.size(); i++)
        if (ans[i] <= m)
            cout << ans[i] << " ";
}

// function to return the ranges after merging
vector<pair<int, int> > mergeRanges(
    vector<pair<int, int> > ranges, int m)
{
    // sort all the ranges
    sort(ranges.begin(), ranges.end());
    vector<pair<int, int> > ans;

    ll prevFirst = ranges[0].first,
       prevLast = ranges[0].second;

    // merging of overlapping ranges
    for (int i = 0; i < m; i++) {
        ll start = ranges[i].first;
        ll last = ranges[i].second;

        // ranges do not overlap
        if (start > prevLast) {
            ans.push_back({ prevFirst, prevLast });
            prevFirst = ranges[i].first;
            prevLast = ranges[i].second;
        }
        else
            prevLast = last;

        if (i == m - 1)
            ans.push_back({ prevFirst, prevLast });
    }
    return ans;
}

// Driver code
int main()
{
    // vector of pair to store the ranges
    vector<pair<int, int> > ranges;
    ranges.push_back({ 1, 2 });
    ranges.push_back({ 4, 5 });

    int n = ranges.size();
    int m = 6;

    // this function returns merged ranges
    vector<pair<int, int> > mergedRanges
        = mergeRanges(ranges, n);

    // this function is use to find
    // missing numbers upto m
    findNumbers(mergedRanges, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class GFG{

static class Pair
{
    int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find the missing
// numbers from the given ranges
static void findNumbers(ArrayList<Pair> ranges,
                        int m)
{
    ArrayList<Integer> ans = new ArrayList<>();

    // prev is use to store end of last range
    int prev = 0;

    // j is used as counter for range
    for(int j = 0; j < ranges.size(); j++)
    {
        int start = ranges.get(j).first;
        int end = ranges.get(j).second;

        for(int i = prev + 1; i < start; i++)
            ans.add(i);

        prev = end;
    }

    // For last range
    for(int i = prev + 1; i <= m; i++)
        ans.add(i);

    // Finally print all answer
    for(int i = 0; i < ans.size(); i++)
        if (ans.get(i) <= m)
            System.out.print(ans.get(i) + " ");
}

// Function to return the ranges after merging
static ArrayList<Pair> mergeRanges(ArrayList<Pair> ranges,
                                   int m)
{

    // Sort all the ranges
    Collections.sort(ranges, new Comparator<Pair>()
    {
        public int compare(Pair first, Pair second)
        {
            if (first.first == second.first)
            {
                return first.second - second.second;
            }
            return first.first - second.first;
        }
    });

    ArrayList<Pair> ans = new ArrayList<>();

    int prevFirst = ranges.get(0).first,
         prevLast = ranges.get(0).second;

    // Merging of overlapping ranges
    for(int i = 0; i < m; i++)
    {
        int start = ranges.get(i).first;
        int last = ranges.get(i).second;

        // Ranges do not overlap
        if (start > prevLast)
        {
            ans.add(new Pair(prevFirst, prevLast));
            prevFirst = ranges.get(i).first;
            prevLast = ranges.get(i).second;
        }
        else
            prevLast = last;

        if (i == m - 1)
            ans.add(new Pair(prevFirst, prevLast));
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Vector of pair to store the ranges
    ArrayList<Pair> ranges = new ArrayList<>();
    ranges.add(new Pair(1, 2));
    ranges.add(new Pair(4, 5));

    int n = ranges.size();
    int m = 6;

    // This function returns merged ranges
    ArrayList<Pair> mergedRanges = mergeRanges(ranges, n);

    // This function is use to find
    // missing numbers upto m
    findNumbers(mergedRanges, m);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# function to find the missing
# numbers from the given ranges
def findNumbers(ranges, m):

    ans = []

    # prev is use to store
    # end of last range
    prev = 0

    # j is used as counter for range
    for j in range(len(ranges)):
        start = ranges[j][0]
        end = ranges[j][1]

        for i in range(prev + 1, start):
            ans.append(i)

        prev = end

    # For last range
    for i in range(prev + 1, m + 1):
            ans.append(i)

    # Finally print all answer
    for i in range(len(ans)):
        if (ans[i] <= m):
            print(ans[i], end = ' ')

# Function to return the ranges
# after merging
def mergeRanges(ranges, m):

    # sort all the ranges
    ranges.sort()
    ans = []

    prevFirst = ranges[0][0]
    prevLast = ranges[0][1]

    # Merging of overlapping ranges
    for i in range(m):
        start = ranges[i][0]
        last = ranges[i][1]

        # Ranges do not overlap
        if (start > prevLast):
            ans.append([prevFirst, prevLast])
            prevFirst = ranges[i][0]
            prevLast = ranges[i][1]
        else:
            prevLast = last;

        if (i == m - 1):
            ans.append([prevFirst, prevLast])

    return ans

# Driver code
if __name__=="__main__":

    # Vector of pair to store the ranges
    ranges = []
    ranges.append([ 1, 2 ]);
    ranges.append([ 4, 5 ]);

    n = len(ranges)
    m = 6

    # This function returns merged ranges
    mergedRanges = mergeRanges(ranges, n);

    # This function is use to find
    # missing numbers upto m
    findNumbers(mergedRanges, m);

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to check
// if the year is a leap year
// using macros
using System;
using System.Collections.Generic;
class GFG {

    // function to find the missing
    // numbers from the given ranges
    static void findNumbers(List<Tuple<int, int>> ranges, int m)
    {
        List<int> ans = new List<int>();

        // prev is use to store end of last range
        int prev = 0;

        // j is used as counter for range
        for (int j = 0; j < ranges.Count; j++) {
            int start = ranges[j].Item1;
            int end = ranges[j].Item2;
            for (int i = prev + 1; i < start; i++)
                ans.Add(i);
            prev = end;
        }

        // for last range
        for (int i = prev + 1; i <= m; i++)
            ans.Add(i);

        // finally print all answer
        for (int i = 0; i < ans.Count; i++)
            if (ans[i] <= m)
                Console.Write(ans[i] + " ");
    }

    // function to return the ranges after merging
    static List<Tuple<int, int>> mergeRanges(
        List<Tuple<int, int>> ranges, int m)
    {
        // sort all the ranges
        ranges.Sort();
        List<Tuple<int, int>> ans =
          new List<Tuple<int, int>>();    
        int prevFirst = ranges[0].Item1,
      prevLast = ranges[0].Item2;

        // merging of overlapping ranges
        for (int i = 0; i < m; i++)
        {
            int start = ranges[i].Item1;
            int last = ranges[i].Item2;

            // ranges do not overlap
            if (start > prevLast)
            {
                ans.Add(new Tuple<int,int>(prevFirst, prevLast ));
                prevFirst = ranges[i].Item1;
                prevLast = ranges[i].Item2;
            }
            else
                prevLast = last;

            if (i == m - 1)
                ans.Add(new Tuple<int,int>(prevFirst, prevLast ));
        }
        return ans;
    }

  // Driver code
  static void Main()
  {

    // vector of pair to store the ranges
    List<Tuple<int, int>> ranges = new List<Tuple<int, int>>();
    ranges.Add(new Tuple<int,int>(1, 2));
    ranges.Add(new Tuple<int,int>(4, 5));
    int n = ranges.Count;
    int m = 6;

    // this function returns merged ranges
    List<Tuple<int, int>> mergedRanges = mergeRanges(ranges, n);

    // this function is use to find
    // missing numbers upto m
    findNumbers(mergedRanges, m);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

class Pair
{
    constructor(first,second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find the missing
// numbers from the given ranges
function findNumbers( ranges,m)
{
    let ans = [];

    // prev is use to store end of last range
    let prev = 0;

    // j is used as counter for range
    for(let j = 0; j < ranges.length; j++)
    {
        let start = ranges[j].first;
        let end = ranges[j].second;

        for(let i = prev + 1; i < start; i++)
            ans.push(i);

        prev = end;
    }

    // For last range
    for(let i = prev + 1; i <= m; i++)
        ans.push(i);

    // Finally print all answer
    for(let i = 0; i < ans.length; i++)
        if (ans[i] <= m)
            document.write(ans[i] + " ");
}

// Function to return the ranges after merging
function mergeRanges(ranges,m)
{
    // Sort all the ranges
    ranges.sort(function(a,b){
            if (a.first == b.first)
            {
                return a.second - b.second;
            }
            return a.first - b.first;});

    let ans = [];

    let prevFirst = ranges[0].first,
         prevLast = ranges[0].second;

    // Merging of overlapping ranges
    for(let i = 0; i < m; i++)
    {
        let start = ranges[i].first;
        let last = ranges[i].second;

        // Ranges do not overlap
        if (start > prevLast)
        {
            ans.push(new Pair(prevFirst, prevLast));
            prevFirst = ranges[i].first;
            prevLast = ranges[i].second;
        }
        else
            prevLast = last;

        if (i == m - 1)
            ans.push(new Pair(prevFirst, prevLast));
    }
    return ans;
}

// Driver code
 // Vector of pair to store the ranges
let ranges = [];
ranges.push(new Pair(1, 2));
ranges.push(new Pair(4, 5));

let n = ranges.length;
let m = 6;

// This function returns merged ranges
let mergedRanges = mergeRanges(ranges, n);

// This function is use to find
// missing numbers upto m
findNumbers(mergedRanges, m);

// This code is contributed by ab2127

</script>
```

**Output:** 

```
3 6
```

**方法 2:**

制作一个 m 大小的数组，并用零初始化它。对于每个范围{L，R}做数组[L]++和数组[R+1]–。现在，在取 sum 的同时迭代数组，如果 sum = x 在索引 I 处，这表示数字 I 在 sum 范围内，例如，如果索引 2 的 sum = 3 的值表示数字 2 在 3 范围内。因此，当总和为 0 时，表示给定的数字不在任何给定的范围内，打印这些数字

下面给出了上述方法 2 的实现。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// function to find the missing
// numbers from the given ranges
void findNumbers(vector<pair<int, int> > ranges, int m)
{

    //Initialized the array of size m+1 with zero
    int r[m+1];
    memset(r,0,sizeof(int)*(m+1));

    //for each range [L,R] do array[L]++ and array[R+1]--
    for(int i=0;i<ranges.size();i++)
    {
        if(ranges[i].first<=m)
            r[ranges[i].first]++;//array[L]++

        if(ranges[i].second+1<=m)
            r[ranges[i].second+1]--;//array[R+1]--
    }

    // Now iterate array and take the sum
    // if sum = x i.e, that particular number
    // comes under x ranges
    // thats means if sum = 0 so that number does not
    // include in any of ranges(print these numbers)
    int sum=0;
    for(int i=1;i<=m;i++)
    {
        sum+=r[i];
        if(sum==0){
            cout<<i<<" ";
        }
    }
}
// Driver Code
int main() {

    // vector of pair to store the ranges
    vector<pair<int, int> > ranges;
    ranges.push_back({ 1, 2 });
    ranges.push_back({ 4, 5 });

    int n = ranges.size();
    int m = 6;

    // this function is use to find
    // missing numbers upto m
    findNumbers(ranges, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class GFG
{
    static class Point
    {
        int x;
        int y;
    }

    // function to find the missing
    // numbers from the given ranges
    static void findNumbers(Point ranges[], int m)
    {

        // Initialized the array of size m+1 with zero
        int r[] = new int[m + 1];
        Arrays.fill(r, 0);

        // for each range [L,R] do array[L]++ and array[R+1]--
        for(int i = 0; i < 2; i++)
        {
            if(ranges[i].x <= m)
                r[ranges[i].x]++;// array[L]++

            if(ranges[i].y + 1 <= m)
                r[ranges[i].y + 1]--;// array[R+1]--
        }

        // Now iterate array and take the sum
        // if sum = x i.e, that particular number
        // comes under x ranges
        // thats means if sum = 0 so that number does not
        // include in any of ranges(print these numbers)
        int sum = 0;
        for(int i = 1; i <= m; i++)
        {
            sum += r[i];
            if(sum == 0)
            {
                System.out.print(i + " ");
            }
        }
    }

  // Driver code
    public static void main(String[] args)
    {

        // vector of pair to store the ranges
        Point ranges[] = new Point[2];       
        ranges[0] = new Point();
        ranges[0].x = 1;
        ranges[0].y = 2;
        ranges[1] = new Point();
        ranges[1].x = 4;
        ranges[1].y = 5;      
        int n = 2;
        int m = 6;

        // this function is use to find
        // missing numbers upto m
        findNumbers(ranges, m);
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to find the missing
# numbers from the given ranges
def findNumbers(ranges, m):

    # Initialized the array
    # of size m+1 with zero
    r = [0] * (m + 1)

    # For each range [L,R] do
    # array[L]++ and array[R+1]--
    for i in range (len(ranges)):

        if(ranges[i][0] <= m):

            # array[L]++
            r[ranges[i][0]] += 1

        if(ranges[i][1] + 1 <= m):

             # array[R+1]--
            r[ranges[i][1] + 1] -= 1

    # Now iterate array and
    # take the sum if sum = x
    # i.e, that particular number
    # comes under x ranges
    # thats means if sum = 0 so
    # that number does not include
    # in any of ranges(print these numbers)
    sum = 0

    for i in range(1, m + 1):  
        sum += r[i]
        if(sum == 0):
            print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    # Vector of pair to
    # store the ranges
    ranges = []
    ranges.append([1, 2])
    ranges.append([4, 5])

    n = len(ranges)
    m = 6

    # This function is use
    # to find missing numbers
    # upto m
    findNumbers(ranges, m)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// function to find the missing
// numbers from the given ranges
static void findNumbers(ArrayList ranges, int m)
{

    // Initialized the array of size m+1 with zero
    int []r = new int[m + 1];
    Array.Fill(r, 0);

    // for each range [L,R] do array[L]++ and array[R+1]--
    for(int i = 0; i < ranges.Count; i++)
    {
        if(((KeyValuePair<int, int>)ranges[i]).Key <= m)
            r[((KeyValuePair<int, int>)ranges[i]).Key]++;// array[L]++

        if(((KeyValuePair<int, int>)ranges[i]).Value + 1 <= m)
            r[((KeyValuePair<int, int>)ranges[i]).Value + 1]--;// array[R+1]--
    }

    // Now iterate array and take the sum
    // if sum = x i.e, that particular number
    // comes under x ranges
    // thats means if sum = 0 so that number does not
    // include in any of ranges(print these numbers)
    int sum = 0;
    for(int i = 1; i <= m; i++)
    {
        sum += r[i];
        if(sum == 0)
        {
            Console.Write(i + " ");
        }
    }
}

// Driver Code
static void Main(string []arg)
{

    // vector of pair to store the ranges
    ArrayList ranges = new ArrayList();

    ranges.Add(new KeyValuePair<int,int>(1, 2));
    ranges.Add(new KeyValuePair<int,int>(4, 5));

    int n = ranges.Count;
    int m = 6;

    // this function is use to find
    // missing numbers upto m
    findNumbers(ranges, m);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // function to find the missing
    // numbers from the given ranges
    function findNumbers(ranges,m)
    {
        let r=new Array(m+1);
        for(let i=0;i<r.length;i++)
        {
            r[i]=0;
        }

        // for each range [L,R] do
        // array[L]++ and array[R+1]--
        for(let i = 0; i < 2; i++)
        {
            if(ranges[i][0] <= m)
                r[ranges[i][0]]++;// array[L]++

            if(ranges[i][1] + 1 <= m)
                r[ranges[i][1] + 1]--;// array[R+1]--
        }

        // Now iterate array and take the sum
        // if sum = x i.e, that particular number
        // comes under x ranges
        // thats means if sum = 0 so that number does not
        // include in any of ranges(print these numbers)
        let sum = 0;
        for(let i = 1; i <= m; i++)
        {
            sum += r[i];
            if(sum == 0)
            {
                document.write(i + " ");
            }
        }
    }

    // Driver code

    // vector of pair to store the ranges
    let ranges = [];
    ranges.push([1, 2])
    ranges.push([4, 5])
    let n = 2;
    let m = 6;
    // this function is use to find
    // missing numbers upto m
    findNumbers(ranges, m);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3 6
```

**时间复杂度:O(n)**