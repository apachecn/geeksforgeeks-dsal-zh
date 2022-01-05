# A 和 B 之间有和的子集

> 原文:[https://www.geeksforgeeks.org/subsets-sum-b/](https://www.geeksforgeeks.org/subsets-sum-b/)

给定一组 N 个整数。找出给定数组中有多少子集的和在 A 和 B 之间(包括 A 和 B)。

> **约束:**
> 1 ≤ N ≤ 34、
> -2 * 10<sup>7</sup>≤arr<sub>I</sub>≤2 * 10<sup>7</sup>
> -5 * 10<sup>8</sup>≤A、B ≤ 5 * 10 <sup>8</sup>

示例:

```
Input : S[] = { 1, -2, 3 }, A = -1, B = 2
Output : 5

Explanation:
1) 0 = 0 (the empty subset)
2) {1} = 1
3) {1, -2} = 1 + (-2) = -1
4) {-2, 3} = (-2) + 3 = 1
5) {1, -2, 3} = 1 + (-2) + 3 = 2
```

**方法 1(蛮力)**:我们可以生成给定数字的所有子集，即[幂集](https://www.geeksforgeeks.org/power-set/)，并找到给定 A 和 b 之和的子集数量，但这将有 2 个 <sup>34 个</sup>运算，效率不是很高。因此，下面是解决这个问题的有效方法。
**方法 2 (** [**在中间相遇**](https://www.geeksforgeeks.org/meet-in-the-middle/) **)** :这基本上把时间复杂度从 O(2 <sup>N</sup> )降低到 O(2 <sup>N/2</sup> )
我们把集合分成两个集合【0…N/2】和【(N/2+1)……(N-1)】,分别为这两个集合生成所有子集和，这两个集合的和为 2 * 2 【T20 现在，我们能做的就是找到这些集合的组合，给出期望的和。这也可以用一种有效的方法来完成，对一个集合求和，并对另一个集合的特定值进行求和。对第二个集合进行排序，对于第一个集合中的每个元素，搜索 A–S2[I](假设为“低”)的下界和 B–S2[I]
(假设为“高”)的上界。减去(高–低)得到想要的答案。

> **例如** S = { 1，2，-1，0 }，A = 1，B = -1。
> 将 S 分为两组后，S1 = { 1，2 }，S2 = { -1，0 }。
> S1 的幂集= { {0}、{1}、{2}、{1，2} }和 S2 的幂集= { {0}、{-1}、{0}、{-1，0} }
> S1 的子集和= { 0，1，2，3 }和 S2 的子集和= { 0，-1，0，-1 }
> 现在对 S2 进行排序{-1，-1，0，0 }对于 S1 的每个值，我们二分搜索法值将产生期望的和。对于 0，我们在 S2 搜索(-1)–0 =-1 作为下限，1–0 = 1 作为上限，对于 1，我们在 S2 搜索(-1)–1 =-2 和 1–1 = 0，以此类推。

## C++

```
// C++ program to find the Number of Subsets that
// have sum between A and B
#include <bits/stdc++.h>
using namespace std;

/* Function to Generate all subsets of a set
   start --> Starting Index of the Set for the
             first/second half Set
   setSize --> Number of element in half Set
   S --> Original Complete Set
   res --> Store the subsets sums */
void generateSubsets(int start, int setSize, int S[],
                                    vector<int>& res)
{
    // setSize of power set of a set with setSize
    // N is (2^n - 1)
    unsigned int pow_setSize = pow(2, setSize);

    // Store the sum of particular subset of set
    int sum;

    // Run from counter 000..0 to 111..1
    for (int counter = 0; counter < pow_setSize; counter++) {

        // set the sum initially to zero
        sum = 0;

        for (int j = 0; j < setSize; j++) {

            // Check if jth bit in the counter is set
            // If set then print jth element from set
            if (counter & (1 << j))
                sum += S[j + start];
        }

        // Store the sum in a vector
        res.push_back(sum);
    }
}

int numberOfSubsets(int S[], int N, int A, int B)
{
    // Vectors to store the subsets sums
    // of two half sets individually
    vector<int> S1, S2;

    // Generate subset sums for the first half set
    generateSubsets(0, N / 2, S, S1);

    // Generate subset sums for the second half set
    if (N % 2 != 0)
        generateSubsets(N / 2, N / 2 + 1, S, S2);
    else
        generateSubsets(N / 2, N / 2, S, S2);

    // Sort the second half set
    sort(S2.begin(), S2.end());

    // Vector Iterator for S1 and S2;
    vector<int>::iterator low, high;

    // number of required subsets with desired Sum
    int ans = 0;

    for (int i = 0; i < S1.size(); i++) {

        // search for lower bound
        low = lower_bound(S2.begin(), S2.end(), A - S1[i]);

        // search for upper bound
        high = upper_bound(S2.begin(), S2.end(), B - S1[i]);

        // Add up to get the desired answer
        ans += (high - low);
    }
    return ans;
}

// Driver Program to test above functions
int main()
{
    int S[] = { 1, -2, 3 };
    int N = sizeof(S) / sizeof(S[0]);

    int A = -1, B = 2;

    // Find the number of subsets with desired Sum
    cout << numberOfSubsets(S, N, A, B) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;
import java.util.function.BiPredicate;

// Java program to find the Number of Subsets that
// have sum between A and B
public class Main
{

    /* Function to Generate all subsets of a set
    start --> Starting Index of the Set for the
             first/second half Set
    setSize --> Number of element in half Set
    S --> Original Complete Set
    res --> Store the subsets sums */
    private static void generateSubsetSumsRecur(int[] arr, int st, int end, int index, int runningSum, List<Integer> sums) {
        if (index == end+1) {
            sums.add(runningSum);
            return;
        }
        generateSubsetSumsRecur(arr, st, end, index+1, runningSum+arr[index], sums);
        generateSubsetSumsRecur(arr, st, end, index+1, runningSum, sums);
    }
    private static long numberOfSubsets(int arr[],int n, int a, int b) {
        // Generate subset sums for the first half set
        List<Integer> sums = new ArrayList<>();
        generateSubsetSumsRecur(arr, 0, n/2, 0, 0, sums);
        Integer[] firstSubsetSums= sums.toArray(new Integer[0]);

        // Generate subset sums for the second half set
        List<Integer> sums2 = new ArrayList<>();
        generateSubsetSumsRecur(arr, n/2+1, n-1, n/2+1, 0, sums2);
        Integer[] secondSubsetSums= sums2.toArray(new Integer[0]);

        // Sort the second half set
        Arrays.sort(secondSubsetSums);

        long count = 0;
        for(int i=0; i<firstSubsetSums.length; i++) {
            int p = findLastIdxWithFalsePredicate(secondSubsetSums,
                                                  a-firstSubsetSums[i],
                                                  (sum, mark)->sum>=mark);
            int q = findLastIdxWithFalsePredicate(secondSubsetSums,
                                                  b-firstSubsetSums[i],
                                                  (sum, mark)->sum>mark);
            count += (q-p);
        }
        return count;
    }
    private static int findLastIdxWithFalsePredicate(Integer[] sums,
                                                     int val,
                                                     BiPredicate<Integer, Integer> pred) {
        int min = 0;
        int max = sums.length-1;
        while (min<max) {
            int mid = min + (max-min+1)/2;
            if (pred.test(sums[mid], val)) {
                max = mid-1;
            } else {
                min = mid;
            }
        }
        if (pred.test(sums[min], val))
            return -1;
        return min;
    }

  // Driver code
    public static void main(String args[])
    {
        int N = 3;
        int A = -1;
        int B = 2;

        int arr[] = { 1, -2, 3 };
        System.out.println(numberOfSubsets(arr, N, A, B));
    }
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program to find the number of
# subsets that have sum between A and B

# Module for Bisection algorithms
import bisect

'''
Function to Generate all subsets of a set
    start --> Starting Index of the Set for the
        first/second half Set
    setSize --> Number of element in half Set
    S --> Original Complete Set
    res --> Store the subsets sums
'''
def generateSubsets(start, setSize, S, res):

    # setSize of power set of a set with setSize
    # N is (2^n - 1)
    pow_setSize = pow(2, setSize)

    # Store the sum of particular subset of set
    add = 0

    # Run from counter 000..0 to 111..1
    for counter in range(pow_setSize):

        # set the sum initially to zero
        add = 0

        for j in range(setSize):

            # Check if jth bit in the counter is set
            # If set then print jth element from set
            if counter & (1 << j):
                add += S[j + start]

        # Store the sum in a vector
        res.append(add)

def numberOfSubsets(S, N, A, B):

    # Vectors to store the subsets sums
    # of two half sets individually
    S1 = []
    S2 = []

    # Generate subset sums for the first half set
    generateSubsets(0, N // 2, S, S1)

    # Generate subset sums for the second half set
    if (N % 2 != 0):
        generateSubsets(N // 2,
                        N // 2 + 1, S, S2)
    else:
        generateSubsets(N // 2,
                        N // 2, S, S2)

    # Sort the second half set
    S2.sort()

    # Number of required subsets
    # with desired Sum
    ans = 0

    for i in range(len(S1)):

        # Search for lower bound
        low = bisect.bisect_left(S2, A - S1[i])

        # Search for upper bound
        high = bisect.bisect_right(S2, B - S1[i])

        # Add up to get the desired answer
        ans += (high - low)

    return ans

# Driver code
if __name__=="__main__":

    S = [ 1, -2, 3 ]
    N = len(S)

    A = -1
    B = 2

    # Find the number of subsets
    # with desired Sum
    print(numberOfSubsets(S, N, A, B))

# This code is contributed by vinaylingam
```

**Output:** 

```
5
```

**时间复杂度:** O(2 * 2 <sup>N/2</sup> ，其中 N 为集合的大小。