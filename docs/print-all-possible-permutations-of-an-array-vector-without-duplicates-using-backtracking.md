# 使用回溯打印一个没有重复的数组/向量的所有可能排列

> 原文:[https://www . geesforgeks . org/print-所有可能的数组排列-无重复向量-使用回溯/](https://www.geeksforgeeks.org/print-all-possible-permutations-of-an-array-vector-without-duplicates-using-backtracking/)

给定[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **nums** ，任务是使用[回溯](https://www.geeksforgeeks.org/backtracking-introduction/)打印给定向量的所有可能排列

**示例**:

> **输入** : nums[] = {1，2，3}
> **输出** : {1，2，3}、{1，3，2}、{2，1，3}、{2，3，1}、{3，2，1}、{3，1，2}
> **解释**:有 6 种可能的排列
> 
> **输入** : nums[] = {1，3}
> **输出** : {1，3}、{3，1}
> **解释**:有 2 种可能的排列

**接近**:可以借助**回溯**解决任务。为了更好的理解，类似的文章如下:[打印给定字符串的所有排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)

![](img/ee04aef6d34ae9cebf843c1cb837c7bf.png)

下面是上述代码的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function for swapping two numbers
void swap(int& x, int& y)
{
    int temp = x;
    x = y;
    y = temp;
}

// Function to find the possible
// permutations
void permutations(vector<vector<int> >& res,
                  vector<int> nums, int l, int h)
{
    // Base case
    // Add the vector to result and return
    if (l == h) {
        res.push_back(nums);
        return;
    }

    // Permutations made
    for (int i = l; i <= h; i++) {

        // Swapping
        swap(nums[l], nums[i]);

        // Calling permutations for
        // next greater value of l
        permutations(res, nums, l + 1, h);

        // Backtracking
        swap(nums[l], nums[i]);
    }
}

// Function to get the permutations
vector<vector<int> > permute(vector<int>& nums)
{
    // Declaring result variable
    vector<vector<int> > res;
    int x = nums.size() - 1;

    // Calling permutations for the first
    // time by passing l
    // as 0 and h = nums.size()-1
    permutations(res, nums, 0, x);
    return res;
}

// Driver Code
int main()
{
    vector<int> nums = { 1, 2, 3 };
    vector<vector<int> > res = permute(nums);

    // printing result
    for (auto x : res) {
        for (auto y : x) {
            cout << y << " ";
        }
        cout << endl;
    }

    return 0;
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the possible
# permutations
def permutations(res, nums, l, h) :

    # Base case
    # Add the vector to result and return
    if (l == h) :
        res.append(nums);
        for i in range(len(nums)):
            print(nums[i], end=' ');

        print('')
        return;

    # Permutations made
    for i in range(l, h + 1):

        # Swapping
        temp = nums[l];
        nums[l] = nums[i];
        nums[i] = temp;

        # Calling permutations for
        # next greater value of l
        permutations(res, nums, l + 1, h);

        # Backtracking
        temp = nums[l];
        nums[l] = nums[i];
        nums[i] = temp;

# Function to get the permutations
def permute(nums):

    # Declaring result variable
    x = len(nums) - 1;
    res = [];

    # Calling permutations for the first
    # time by passing l
    # as 0 and h = nums.size()-1
    permutations(res, nums, 0, x);
    return res;

# Driver Code
nums = [ 1, 2, 3 ];
res = permute(nums);

# This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the possible
// permutations
function permutations(res, nums, l, h)
{

    // Base case
    // Add the vector to result and return
    if (l == h)
    {
        res.push(nums);
        for(let i = 0; i < nums.length; i++)
            document.write(nums[i] + ' ');

        document.write('<br>')
        return;
    }

    // Permutations made
    for(let i = l; i <= h; i++)
    {

        // Swapping
        let temp = nums[l];
        nums[l] = nums[i];
        nums[i] = temp;

        // Calling permutations for
        // next greater value of l
        permutations(res, nums, l + 1, h);

        // Backtracking
        temp = nums[l];
        nums[l] = nums[i];
        nums[i] = temp;
    }
}

// Function to get the permutations
function permute(nums)
{

    // Declaring result variable
    let x = nums.length - 1;
    let res = [];

    // Calling permutations for the first
    // time by passing l
    // as 0 and h = nums.size()-1
    permutations(res, nums, 0, x);
    return res;
}

// Driver Code
let nums = [ 1, 2, 3 ];
let res = permute(nums);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
1 2 3 
1 3 2 
2 1 3 
2 3 1 
3 2 1 
3 1 2 
```

***时间复杂度*** **:** O(N*N！)注意有 N 个！排列，打印排列需要 O(N)个时间。
***辅助空间*****:**O(r–l)