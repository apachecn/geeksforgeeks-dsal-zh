# 0/1 背包问题打印所有可能的解决方案

> 原文:[https://www . geesforgeks . org/0-1-背包问题打印所有可能的解决方案/](https://www.geeksforgeeks.org/0-1-knapsack-problem-to-print-all-possible-solutions/)

给定 **N** 物品的重量和利润，将这些物品放入一个容量为 **W** 的背包中。任务是打印该问题的所有可能解决方案，使得没有剩余重量小于背包剩余容量的物品。另外，计算最大利润。
**例:**

> **输入:**利润[] = {60，100，120，50}
> 权重[] = {10，20，30，40}，W = 40
> **输出:**
> 10: 60，20: 100，
> 10: 60，30: 120，
> 最大利润= 180
> **解释:**
> 从所有可能的解决方案中获得的最大利润是 10
> 10: 60，30: 120，
> 20: 100，30: 120，
> 最大利润= 220
> **解释:**
> 所有可能的解决方案的最大利润为 220

**方法:**想法是[对物品的重量和利润进行配对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)，然后尝试数组的所有[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，并包括重量，直到没有重量小于背包剩余容量的物品。同时，在包含一个项目后，用该项目的利润增加该解决方案的利润。
以下是上述方法的实现:

## C++

```
// C++ implementation to print all
// the possible solutions of the
// 0/1 Knapsack problem

#include <bits/stdc++.h>

using namespace std;

// Utility function to find the
// maximum of the two elements
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to find the all the
// possible solutions of the
// 0/1 knapSack problem
int knapSack(int W, vector<int> wt,
            vector<int> val, int n)
{
    // Mapping weights with Profits
    map<int, int> umap;

    set<vector<pair<int, int>>> set_sol;
    // Making Pairs and inserting
    // into the map
    for (int i = 0; i < n; i++) {
        umap.insert({ wt[i], val[i] });
    }

    int result = INT_MIN;
    int remaining_weight;
    int sum = 0;

    // Loop to iterate over all the
    // possible permutations of array
    do {
        sum = 0;

        // Initially bag will be empty
        remaining_weight = W;
        vector<pair<int, int>> possible;

        // Loop to fill up the bag
        // untill there is no weight
        // such which is less than
        // remaining weight of the
        // 0-1 knapSack
        for (int i = 0; i < n; i++) {
            if (wt[i] <= remaining_weight) {

                remaining_weight -= wt[i];
                auto itr = umap.find(wt[i]);
                sum += (itr->second);
                possible.push_back({itr->first,
                     itr->second
                });
            }
        }
        sort(possible.begin(), possible.end());
        if (sum > result) {
            result = sum;
        }
        if (set_sol.find(possible) ==
                        set_sol.end()){
            for (auto sol: possible){
                cout << sol.first << ": "
                     << sol.second << ", ";
            }
            cout << endl;
            set_sol.insert(possible);
        }

    } while (
        next_permutation(wt.begin(),
                           wt.end()));
    return result;
}

// Driver Code
int main()
{
    vector<int> val{ 60, 100, 120 };
    vector<int> wt{ 10, 20, 30 };
    int W = 50;
    int n = val.size();
    int maximum = knapSack(W, wt, val, n);
    cout << "Maximum Profit = ";
    cout << maximum;
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation to prall
# the possible solutions of the
# 0/1 Knapsack problem

INT_MIN=-2147483648
def nextPermutation(nums: list) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        if sorted(nums,reverse=True)==nums:
            return None
        n=len(nums)
        brk_point=-1
        for pos in range(n-1,0,-1):
            if nums[pos]>nums[pos-1]:
                brk_point=pos
                break
        else:
            nums.sort()
            return
        replace_with=-1
        for j in range(brk_point,n):
            if nums[j]>nums[brk_point-1]:
                replace_with=j
            else:
                break
        nums[replace_with],nums[brk_point-1]=nums[brk_point-1],nums[replace_with]
        nums[brk_point:]=sorted(nums[brk_point:])
        return nums

# Function to find the all the
# possible solutions of the
# 0/1 knapSack problem
def knapSack(W, wt, val, n):
    # Mapping weights with Profits
    umap=dict()

    set_sol=set()
    # Making Pairs and inserting
    # o the map
    for i in range(n) :
        umap[wt[i]]=val[i]

    result = INT_MIN
    remaining_weight=0
    sum = 0

    # Loop to iterate over all the
    # possible permutations of array
    while True:
        sum = 0

        # Initially bag will be empty
        remaining_weight = W
        possible=[]

        # Loop to fill up the bag
        # untill there is no weight
        # such which is less than
        # remaining weight of the
        # 0-1 knapSack
        for i in range(n) :
            if (wt[i] <= remaining_weight) :

                remaining_weight -= wt[i]
                sum += (umap[wt[i]])
                possible.append((wt[i],
                     umap[wt[i]])
                )

        possible.sort()
        if (sum > result) :
            result = sum

        if (tuple(possible) not in set_sol):
            for sol in possible:
                print(sol[0], ": ", sol[1], ", ",end='')

            print()
            set_sol.add(tuple(possible))

        if not nextPermutation(wt):
            break
    return result

# Driver Code
if __name__ == '__main__':
    val=[60, 100, 120]
    wt=[10, 20, 30]
    W = 50
    n = len(val)
    maximum = knapSack(W, wt, val, n)
    print("Maximum Profit =",maximum)

#This code was contributed by Amartya Ghosh
```

**Output:** 

```
10: 60, 20: 100, 
10: 60, 30: 120, 
20: 100, 30: 120, 
Maximum Profit = 220
```