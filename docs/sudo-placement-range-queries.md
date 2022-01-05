# Sudo 放置|范围查询

> 原文:[https://www.geeksforgeeks.org/sudo-placement-range-queries/](https://www.geeksforgeeks.org/sudo-placement-range-queries/)

给定 Q 个查询，每个查询由两个整数 L 和 R 组成，任务是找到 L 和 R 之间的总数(两者都包括在内)，它们的二进制表示中几乎有三个集合位。
**例** :

```
Input : Q = 2
        L = 3, R = 7
        L = 10, R = 16
Output : 5
         6
For the first query, valid numbers are 3, 4, 5, 6, and 7.
For the second query, valid numbers are 10, 11, 12, 13, 14 and 16.
```

**先决条件** : [比特操纵](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)T6

**方法 1(简单)**:一种简单的方法是遍历 L 和 R 之间的所有数字，并找到这些数字中每个数字的设置位数。如果一个数字的设置位不超过 3 位，则递增计数器变量。作为计数器返回答案。**注**:这种方法效率很低，因为数字 L 和 R 可能有很大的值(高达 10 <sup>18</sup> )。
**方法 2(高效)**:这里需要的高效方法是预计算。由于 L 和 R 的值在[0，10 <sup>18</sup> ]的范围内(包括这两个值)，因此它们的二进制表示最多可以有 60 位。现在，由于有效数字是具有几乎 3 个设置位的数字，所以通过生成所有 60 位的位序列来找到它们，这些位序列具有小于或等于 3 个设置位。这可以通过固定 i <sup>第</sup>位、j <sup>第</sup>位和 k <sup>第</sup>位(0，60)来实现。一旦所有有效数字都按排序顺序生成，应用二分搜索法来查找给定范围内的数字的计数。
以下是上述办法的实施情况。

## C++

```
// CPP program to find the numbers
// having atmost 3 set bits within
// a given range
#include <bits/stdc++.h>

using namespace std;

#define LL long long int

// This function prints the required answer for each query
void answerQueries(LL Q, vector<pair<LL, LL> > query)
{
    // Set of Numbers having at most 3 set bits
    // arranged in non-descending order
    set<LL> s;

    // 0 set bits
    s.insert(0);

    // Iterate over all possible combinations of
    // i, j and k for 60 bits
    for (int i = 0; i <= 60; i++) {
        for (int j = i; j <= 60; j++) {
            for (int k = j; k <= 60; k++) {
                // 1 set bit
                if (j == i && i == k)
                    s.insert(1LL << i);

                // 2 set bits
                else if (j == k && i != j) {
                    LL x = (1LL << i) + (1LL << j);
                    s.insert(x);
                }
                else if (i == j && i != k) {
                    LL x = (1LL << i) + (1LL << k);
                    s.insert(x);
                }
                else if (i == k && i != j) {
                    LL x = (1LL << k) + (1LL << j);
                    s.insert(x);
                }

                // 3 set bits
                else {
                    LL x = (1LL << i) + (1LL << j) + (1LL << k);
                    s.insert(x);
                }
            }
        }
    }
    vector<LL> validNumbers;
    for (auto val : s)
        validNumbers.push_back(val);

    // Answer Queries by applying binary search
    for (int i = 0; i < Q; i++) {
        LL L = query[i].first;
        LL R = query[i].second;

        // Swap both the numbers if L is greater than R
        if (R < L)
            swap(L, R);
        if (L == 0)
            cout << (upper_bound(validNumbers.begin(), validNumbers.end(),
                    R) - validNumbers.begin()) << endl;
        else
            cout << (upper_bound(validNumbers.begin(), validNumbers.end(),
                   R) - upper_bound(validNumbers.begin(), validNumbers.end(),
                   L - 1)) << endl;
    }
}

// Driver Code
int main()
{
    // Number of Queries
    int Q = 2;
    vector<pair<LL, LL> > query(Q);
    query[0].first = 3;
    query[0].second = 7;
    query[1].first = 10;
    query[1].second = 16;

    answerQueries(Q, query);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the numbers
// having atmost 3 set bits within
// a given range
import java.util.*;
import java.io.*;

public class RangeQueries {

    //Class to store the L and R range of a query
    static class Query {
        long L;
        long R;
    }

    //It returns index of first element which is greater than searched value
     //If searched element is bigger than any array element function
     // returns first index after last element.
    public static int upperBound(ArrayList<Long> validNumbers,
                                    Long value)
    {
        int low = 0;
        int high = validNumbers.size()-1;

        while(low < high){
            int mid = (low + high)/2;
            if(value >= validNumbers.get(mid)){
                low = mid+1;
            } else {
                high = mid;
            }
        }
        return low;
    }

    public static void answerQueries(ArrayList<Query> queries){
        // Set of Numbers having at most 3 set bits
        // arranged in non-descending order
        Set<Long> allNum = new HashSet<>();

        //0 Set bits
        allNum.add(0L);

        //Iterate over all possible combinations of i, j, k for
        // 60 bits. And add all the numbers with 0, 1 or 2 set bits into
        // the set allNum.
        for(int i=0; i<=60; i++){
            for(int j=0; j<=60; j++){
                for(int k=0; k<=60; k++){

                    //For one set bit, check if i, j, k are equal
                    //if yes, then set that bit and add it to the set
                    if(i==j && j==k){
                        allNum.add(1L << i);
                    }

                    //For two set bits, two of the three variable i,j,k
                    //will be equal and the third will not be. Set both
                    //the bits where two variabls are equal and the bit
                    //which is not equal, and add it to the set
                    else if(i==j && j != k){
                        long toAdd = (1L << i) + (1L << k);
                        allNum.add(toAdd);
                    }
                    else if(i==k && k != j){
                        long toAdd = (1L << i) + (1L << j);
                        allNum.add(toAdd);
                    }
                    else if(j==k && k != i){
                        long toAdd = (1L << j) + (1L << i);
                        allNum.add(toAdd);
                    }

                    //Setting all the 3 bits
                    else {
                        long toAdd = (1L << i) + (1L << j) + (1L << k);
                        allNum.add(toAdd);
                    }

                }
            }
        }

        //Adding all the numbers to an array list so that it can be sorted
        ArrayList<Long> validNumbers = new ArrayList<>();
        for(Long num: allNum){
            validNumbers.add(num);
        }

        Collections.sort(validNumbers);

        //Answer queries by applying binary search
        for(int i=0; i<queries.size(); i++){
            long L = queries.get(i).L;
            long R = queries.get(i).R;

            //Swap L and R if R is smaller than L
            if(R < L){
                long temp = L;
                L = R;
                R = temp;
            }

            if(L == 0){
                int indxOfLastNum = upperBound(validNumbers, R);
                System.out.println(indxOfLastNum+1);
            }
            else {
                int indxOfFirstNum = upperBound(validNumbers, L);
                int indxOfLastNum = upperBound(validNumbers, R);
                System.out.println((indxOfLastNum - indxOfFirstNum +1));
            }

        }

    }

    public static void main(String[] args){
        int Q = 2;
        ArrayList<Query> queries = new ArrayList<>();

        Query q1 = new Query();
        q1.L = 3;
        q1.R = 7;

        Query q2 = new Query();
        q2.L = 10;
        q2.R = 16;

        queries.add(q1);
        queries.add(q2);

        answerQueries(queries);
    }

}
```

**时间复杂度** : O((最大位数) <sup>3</sup> + Q * logN，其中 Q 为查询数，N 为包含所有有效数的集合的大小。l 有效数字。