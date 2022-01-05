# 通过将数字放在给定数组指定的位置来构造最小的 N 位数

> 原文:[https://www . geeksforgeeks . org/construct-最小 n 位数字-通过在给定数组指定的位置放置可能的数字/](https://www.geeksforgeeks.org/construct-smallest-n-digit-number-possible-by-placing-digits-at-positions-specified-by-given-array/)

给定两个整数 **N** 和 **M** 和一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**arr【】**，任务是构造 **N** 个数字(*没有前导零*)的最小可能整数，使得左边的**arr[I][0]**个数字为 **arr[i][1]** 。如果无法构造任何这样的整数，打印**“否”**。否则，打印该号码。

**示例:**

> **输入:** N = 3，arr[]={{0，7}，{2，2}}
> **输出:** 702
> **说明:**根据条件，1 <sup>st</sup> 和 3 <sup>rd</sup> 数字应等于 7 和 2。编号应为 7 **_** 2 的形式。因此，最小可能整数是 702。
> 
> **输入:** N = 3，arr[]={{1，1}，{1，3 } }
> T3】输出:否

**天真方法:**由于位数总是从 **0** 到 **9** 的，最简单的方法是根据给定的条件放置位数，检查超过 **0** 且小于 **10 <sup>N</sup>** 的每个整数的[组合](https://www.geeksforgeeks.org/permutation-and-combination/)。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if num satisfies the
// arrangement specified by the vector A
bool check(int num, int N, int M,
           vector<pair<int, char> >& A)
{
    // Convert num to equivalent string
    string temp = to_string(num);

    // If the number of digits
    // is not equal to N
    if (temp.size() != N) {
        return false;
    }

    // Iterate over the vector A
    for (int i = 0; i < M; i++) {

        // If the digit at A[i].first position
        // not the same as A[i].second
        if (temp[A[i].first] != A[i].second) {
            return false;
        }
    }

    return true;
}

// Function to find the smallest integer
// satisfying the given conditions
void find_num(int N, vector<pair<int, char> >& A)
{
    int ans = -1;

    // Check for every combination upto 10^N
    for (int i = 0; i < pow(10, N); i++) {

        // If condition satisfies
        if (check(i, N, A.size(), A)) {
            ans = i;
            break;
        }
    }

    if (ans == -1)
        cout << "No";
    else
        cout << ans;
}

// Driver Code
int main()
{

    int N = 3;
    vector<pair<int, char> > A
        = { { 0, '7' }, { 2, '2' }, { 0, '7' } };

    find_num(N, A);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first;
        char second;
        public pair(int first, char second) 
        {
            this.first = first;
            this.second = second;
        }   
    };

// Function to check if num satisfies the
// arrangement specified by the vector A
static boolean check(int num, int N, int M,
           Vector<pair> A)
{
    // Convert num to equivalent String
    String temp = String.valueOf(num);

    // If the number of digits
    // is not equal to N
    if (temp.length() != N) {
        return false;
    }

    // Iterate over the vector A
    for (int i = 0; i < M; i++) {

        // If the digit at A[i].first position
        // not the same as A[i].second
        if (temp.charAt(A.get(i).first) != A.get(i).second) {
            return false;
        }
    }

    return true;
}

// Function to find the smallest integer
// satisfying the given conditions
static void find_num(int N, Vector<pair> A)
{
    int ans = -1;

    // Check for every combination upto 10^N
    for (int i = 0; i < Math.pow(10, N); i++) {

        // If condition satisfies
        if (check(i, N, A.size(), A)) {
            ans = i;
            break;
        }
    }

    if (ans == -1)
        System.out.print("No");
    else
        System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{

    int N = 3;
    Vector<pair> A = new Vector<>();
    A.add(new pair(0, '7' ));
    A.add(new pair(2, '2'));
    A.add(new pair( 0, '7'));

    find_num(N, A);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if num satisfies the
# arrangement specified by the vector A
def check(num, N, M, A) :

    # Convert num to equivalent string
    temp = str(num)

    # If the number of digits
    # is not equal to N
    if (len(temp) != N) :
        return False

    # Iterate over the vector A
    for i in range(M) :

        # If the digit at A[i].first position
        # not the same as A[i].second
        if (temp[A[i][0]] != A[i][1]) :
            return False

    return True

# Function to find the smallest integer
# satisfying the given conditions
def find_num(N, A) :

    ans = -1

    # Check for every combination upto 10^N
    for i in range(pow(10, N)) :

        # If condition satisfies
        if (check(i, N, len(A), A)) :
            ans = i
            break

    if (ans == -1) :
        print("No")
    else :
        print(ans)

N = 3
A = [ [ 0, '7' ], [ 2, '2' ], [ 0, '7' ] ]

find_num(N, A)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{
    public class pair
    {
        public int first;
        public char second;
        public pair(int first, char second) 
        {
            this.first = first;
            this.second = second;
        }   
    };

// Function to check if num satisfies the
// arrangement specified by the vector A
static bool check(int num, int N, int M,
           List<pair> A)
{
    // Convert num to equivalent String
    String temp = String.Join("",num);

    // If the number of digits
    // is not equal to N
    if (temp.Length != N) {
        return false;
    }

    // Iterate over the vector A
    for (int i = 0; i < M; i++) {

        // If the digit at A[i].first position
        // not the same as A[i].second
        if (temp[A[i].first] != A[i].second) {
            return false;
        }
    }

    return true;
}

// Function to find the smallest integer
// satisfying the given conditions
static void find_num(int N, List<pair> A)
{
    int ans = -1;

    // Check for every combination upto 10^N
    for (int i = 0; i < Math.Pow(10, N); i++) {

        // If condition satisfies
        if (check(i, N, A.Count, A)) {
            ans = i;
            break;
        }
    }

    if (ans == -1)
        Console.Write("No");
    else
        Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{

    int N = 3;
    List<pair> A = new List<pair>();
    A.Add(new pair(0, '7' ));
    A.Add(new pair(2, '2'));
    A.Add(new pair( 0, '7'));

    find_num(N, A);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if num satisfies the
// arrangement specified by the vector A
function check(num, N, M, A)
{
    // Convert num to equivalent string
    var temp = (num.toString());

    // If the number of digits
    // is not equal to N
    if (temp.length != N) {
        return false;
    }

    // Iterate over the vector A
    for (var i = 0; i < M; i++) {

        // If the digit at A[i][0] position
        // not the same as A[i][1]
        if (temp[A[i][0]] != A[i][1]) {
            return false;
        }
    }

    return true;
}

// Function to find the smallest integer
// satisfying the given conditions
function find_num(N, A)
{
    var ans = -1;

    // Check for every combination upto 10^N
    for (var i = 0; i < Math.pow(10, N); i++) {

        // If condition satisfies
        if (check(i, N, A.length, A)) {
            ans = i;
            break;
        }
    }

    if (ans == -1)
        document.write( "No");
    else
        document.write( ans);
}

// Driver Code
var N = 3;
var A = [ [ 0, '7' ], [ 2, '2' ], [ 0, '7' ] ];
find_num(N, A);

</script>
```

**Output:** 

```
702
```

**时间复杂度:**O(10<sup>N</sup>* M)
T5】辅助空间: O(N)

**高效方法:**按照以下步骤解决问题:

*   初始化一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp** ，给相应的位置分配数字。
*   如果需要放置的第一个数字是 **0** ，则打印**“否”**，因为数字不能包含前导零。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) arr【】，并在**地图**中的相应索引处插入数字。
*   运行从 **1** 到 **N** 的循环，对于每个 **i** ，检查在**地图**中的**I**T8 位置是否分配了一个数字。如果出现在**地图**中，将其添加到答案中。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest integer
// satisfying the given conditions
void find_num(int N, vector<pair<int, int> >& A)
{
    // Stores the digits at their
    // respective positions
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < A.size(); i++) {

        // If first digit required
        // to be placed is 0
        if (N > 1 and A[i].first == 0
            and A[i].second == 0) {

            // Not possible
            cout << "No";
            return;
        }

        // If multiple numbers are assigned
        // to be placed in a single position
        if (mp.find(A[i].first) != mp.end()
            and mp[A[i].first] != A[i].second) {

            // Not possible
            cout << "No";
            return;
        }

        // Assign the digits to their
        // respective positions
        mp[A[i].first] = A[i].second;
    }

    // Stores the result
    string ans = "";

    // Traverse for all N digits
    for (int i = 0; i < N; i++) {

        // For the first position
        if (N > 1 and i == 0) {

            // If digit is assigned
            // to the position
            if (mp.find(0) != mp.end()) {
                ans += to_string(mp[0]);
            }

            // Otherwise
            else {
                ans += to_string(1);
            }
        }

        else {
            // Add it to answer
            ans += to_string(mp[i]);
        }
    }

    cout << ans << "\n";
}

// Driver Code
int main()
{

    int N = 3;
    vector<pair<int, int> > A
        = { { 0, 7 }, { 2, 2 }, { 0, 7 } };

    find_num(N, A);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to find the smallest integer
// satisfying the given conditions
static void find_num(int N, pair []A)
{

    // Stores the digits at their
    // respective positions
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Traverse the array
    for(int i = 0; i < A.length; i++)
    {

        // If first digit required
        // to be placed is 0
        if (N > 1 && A[i].first == 0 &&
            A[i].second == 0)
        {

            // Not possible
            System.out.print("No");
            return;
        }

        // If multiple numbers are assigned
        // to be placed in a single position
        if (mp.containsKey(A[i].first) &&
            mp.get(A[i].first) != A[i].second)
        {

            // Not possible
            System.out.print("No");
            return;
        }

        // Assign the digits to their
        // respective positions
        mp.put(A[i].first, A[i].second);
    }

    // Stores the result
    String ans = "";

    // Traverse for all N digits
    for(int i = 0; i < N; i++)
    {

        // For the first position
        if (N > 1 && i == 0)
        {

            // If digit is assigned
            // to the position
            if (mp.containsKey(0))
            {

                ans += String.valueOf(mp.get(0));
            }

            // Otherwise
            else
            {
                ans += String.valueOf(1);
            }
        }
        else
        {

            // Add it to answer
            if (mp.get(i) == null)
                ans += String.valueOf(0);
            else
                ans += String.valueOf(mp.get(i));
        }
    }
    System.out.print(ans + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    pair []A = { new pair(0, 7),
                 new pair(2, 2),
                 new pair(0, 7)};

    find_num(N, A);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the smallest integer
# satisfying the given conditions
def find_num(N, A) :

    # Stores the digits at their
    # respective positions
    mp = {}

    # Traverse the array
    for i in range(len(A)) :

        # If first digit required
        # to be placed is 0
        if ((N > 1) and (A[i][0] == 0) and (A[i][1] == 0)) :

            # Not possible
            print("No")
            return

        # If multiple numbers are assigned
        # to be placed in a single position
        if ((A[i][0] in mp) and (mp[A[i][0]] != A[i][1])) :

            # Not possible
            print("No")
            return

        # Assign the digits to their
        # respective positions
        mp[A[i][0]] = A[i][1]

    # Stores the result
    ans = ""

    # Traverse for all N digits
    for i in range(N) :

        # For the first position
        if (N > 1 and i == 0) :

            # If digit is assigned
            # to the position
            if (0 in mp) :
                ans = ans + str(mp[0])

            # Otherwise
            else :
                ans = ans + str(1)

        else :
            # Add it to answer
            if i in mp :
                ans = ans + str(mp[i])
            else :
                ans = ans + str(0)

    print(ans)

# Driver code
N = 3
A = [ [ 0, 7 ], [ 2, 2 ], [ 0, 7 ] ]

find_num(N, A)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

public
 class pair
{
    public
 int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to find the smallest integer
// satisfying the given conditions
static void find_num(int N, pair []A)
{

    // Stores the digits at their
    // respective positions
    Dictionary<int,
            int> mp = new Dictionary<int,
                                      int>();

    // Traverse the array
    for(int i = 0; i < A.Length; i++)
    {

        // If first digit required
        // to be placed is 0
        if (N > 1 && A[i].first == 0 &&
            A[i].second == 0)
        {

            // Not possible
            Console.Write("No");
            return;
        }

        // If multiple numbers are assigned
        // to be placed in a single position
        if (mp.ContainsKey(A[i].first) &&
            mp[A[i].first] != A[i].second)
        {

            // Not possible
            Console.Write("No");
            return;
        }

        // Assign the digits to their
        // respective positions
        if(mp.ContainsKey(A[i].first))
            mp[A[i].first] = A[i].second;
        else
        mp.Add(A[i].first, A[i].second);
    }

    // Stores the result
    String ans = "";

    // Traverse for all N digits
    for(int i = 0; i < N; i++)
    {

        // For the first position
        if (N > 1 && i == 0)
        {

            // If digit is assigned
            // to the position
            if (mp.ContainsKey(0))
            {

                ans += String.Join("", mp[0]);
            }

            // Otherwise
            else
            {
                ans += String.Join("", 1);
            }
        }
        else
        {

            // Add it to answer
            if ( ! mp.ContainsKey(i) )
                ans += String.Join("", 0);
            else
                ans += String.Join("", mp[i]);
        }
    }
    Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    pair []A = { new pair(0, 7),
                 new pair(2, 2),
                 new pair(0, 7)};

    find_num(N, A);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
702
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*