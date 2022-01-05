# 超级丑数(素数因子在给定集合中的数)

> 原文:[https://www . geesforgeks . org/超丑数-数-谁的素因子-给定集/](https://www.geeksforgeeks.org/super-ugly-number-number-whose-prime-factors-given-set/)

超级难看的数字是正数，其所有质因数都在给定的质数列表中。给定一个数字 n，任务是找到第 n 个超级丑的数字。
可以假设给定的一组素数被排序。另外，按照惯例，第一个超级丑的数字是 1。

**示例:**

```
Input  : primes[] = [2, 5]
         n = 5
Output : 8
Super Ugly numbers with given prime factors 
are 1, 2, 4, 5, 8, ...
Fifth Super Ugly number is 8

Input  : primes[] = [2, 3, 5]
         n = 50
Output : 243

Input : primes[] = [3, 5, 7, 11, 13]
        n = 9
Output: 21 
```

在我们之前的帖子中，我们讨论了[丑号](https://www.geeksforgeeks.org/ugly-numbers/)。这个问题基本上是**丑陋数字**的延伸。
这个问题的一个**简单的解决方法**就是从 1 开始一个一个的挑选每个数字，发现都是质数因子，如果所有质数因子都在给定的质数集中，那就说明这个数字超级难看。重复这个过程，直到我们得到第 n 个超级丑陋的数字。

这个问题的一个**高效解决方案**类似于[丑号](https://www.geeksforgeeks.org/ugly-numbers/)的**方法-2** 。下面是算法:

1.  设 **k** 为给定素数数组的大小。
2.  宣布一组超级难看的数字。
3.  将第一个难看的数字(总是 1)插入集合中。
4.  用 0 初始化大小为 k 的[k] 的数组**倍数。这个数组的每个元素都是素数[k]数组中相应素数的迭代器。**
5.  用素数[k]初始化 **nextMultipe[k]** 数组。这个数组的行为类似于给定素数[k]数组中每个素数的下一个多个变量，即:nextMultiple[i] = primes[i] *难看[++multiple_of[i]]。
6.  现在循环，直到集合中有 n 个元素。
    a)。在 nextMultiple[]数组中找到当前素数倍数中的最小值，并将其插入丑陋的数字集合中。
    b)。然后求出这个电流最小值是哪个素数的倍数。
    c。将迭代器增加 1，即:++multiple_Of[i]，为当前选定质数的下一个倍数，并为其更新下一个倍数。

下面是上述步骤的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find n'th Super Ugly number
#include<bits/stdc++.h>
using namespace std;

// Function to get the nth super ugly number
// primes[]       --> given list of primes f size k
// ugly           --> set which holds all super ugly
//                    numbers from 1 to n
// k              --> Size of prime[]
int superUgly(int n, int primes[], int k)
{
    // nextMultiple holds multiples of given primes
    vector<int> nextMultiple(primes, primes+k);

    // To store iterators of all primes
    int multiple_Of[k];
    memset(multiple_Of, 0, sizeof(multiple_Of));

    // Create a set to store super ugly numbers and
    // store first Super ugly number
    set<int> ugly;
    ugly.insert(1);

    // loop until there are total n Super ugly numbers
    // in set
    while (ugly.size() != n)
    {
        // Find minimum element among all current
        // multiples of given prime
        int next_ugly_no = *min_element(nextMultiple.begin(),
                                    nextMultiple.end());

        // insert this super ugly number in set
        ugly.insert(next_ugly_no);

        // loop to find current minimum is multiple
        // of which prime
        for (int j=0; j<k; j++)
        {
            if (next_ugly_no == nextMultiple[j])
            {
                // increase iterator by one for next multiple
                // of current prime
                multiple_Of[j]++;

                // this loop is similar to find  dp[++index[j]]
                // it -->  dp[++index[j]]
                set<int>::iterator it = ugly.begin();
                for (int i=1; i<=multiple_Of[j]; i++)
                    it++;

                nextMultiple[j] = primes[j] * (*it);
                break;
            }
        }
    }

    // n'th super ugly number
    set<int>::iterator it = ugly.end();
    it--;
    return *it;
}

/* Driver program to test above functions */
int main()
{
    int primes[] = {2,  5};
    int k = sizeof(primes)/sizeof(primes[0]);
    int n = 5;
    cout << superUgly(n, primes, k);
    return 0;
}
```

**输出:**

```
8
```

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

**另一种方法(使用 priority_queue)**
这里我们使用 min 堆 priority_queue。
想法是将第一个难看的 1 号推入 priority_queue，并在每次迭代中获取 priority_queue 的顶部，并将该顶部的所有倍数推入 priority_queue。
假设[] = {2，3，5}，
那么在第一次迭代中 1 是顶部的，所以弹出 1，推 1 * 2，1 * 3，1 * 5。
第二次迭代 min 为 2，所以弹出，推 2 * 2，2 * 3，2 * 5 等等。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for super ugly number
#include<bits/stdc++.h>
using namespace std;
//function will return the nth super ugly number
int ugly(int a[], int size, int n){

    //n cannot be negative hence return -1 if n is 0 or -ve
    if(n <= 0)
        return -1;

    if(n == 1)
        return 1;

    // Declare a min heap priority queue
    priority_queue<int, vector<int>, greater<int>> pq;

    // Push all the array elements to priority queue
    for(int i = 0; i < size; i++){
        pq.push(a[i]);
    }

    // once count = n we return no
    int count = 1, no;

    while(count < n){
        // Get the minimum value from priority_queue
        no = pq.top();
        pq.pop();

        // If top of pq is no then don't increment count. This to avoid duplicate counting of same no.
        if(no != pq.top())
        {
            count++;

            //Push all the multiples of no. to priority_queue
            for(int i = 0; i < size; i++){
                pq.push(no * a[i]);
            //    cnt+=1;
        }
        }
    }
    // Return nth super ugly number
    return no;
}

/* Driver program to test above functions */
int main(){
    int a[3] = {2, 3,5};
    int size = sizeof(a) / sizeof(a[0]);
    cout << ugly(a, size, 10)<<endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for super ugly number

# function will return the nth super ugly number
def ugly(a, size, n):

    # n cannot be negative hence return -1 if n is 0 or -ve
    if(n <= 0):
        return -1
    if(n == 1):
        return 1

    # Declare a min heap priority queue
    pq = []

    # Push all the array elements to priority queue
    for i  in range(size):
        pq.append(a[i])

    # once count = n we return no
    count = 1
    no = 0
    pq = sorted(pq)

    while(count < n):
        # sorted(pq)
        # Get the minimum value from priority_queue
        no = pq[0]
        del pq[0]

        # If top of pq is no then don't increment count.
        # This to avoid duplicate counting of same no.
        if(no != pq[0]):
            count += 1

            # Push all the multiples of no. to priority_queue
            for i in range(size):
                pq.append(no * a[i])
            #   cnt+=1
        pq = sorted(pq)
    # Return nth super ugly number
    return no

# /* Driver program to test above functions */
if __name__ == '__main__':
    a = [2, 3,5]
    size = len(a)
    print(ugly(a, size, 1000))

    # This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>
// Javascript program for super ugly number

    //function will return the nth super ugly number
    function ugly(a,size,n)
    {
        //n cannot be negative hence return -1 if n is 0 or -ve
    if(n <= 0)
        return -1;

    if(n == 1)
        return 1;

    // Declare a min heap priority queue
    let pq=[];;

    // Push all the array elements to priority queue
    for(let i = 0; i < size; i++){
        pq.push(a[i]);
    }

    // once count = n we return no
    let count = 1, no;
    pq.sort(function(a,b){return a-b;}) ;

    while(count < n){
        // Get the minimum value from priority_queue
        no = pq.shift();

        // If top of pq is no then don't increment count. This to avoid duplicate counting of same no.
        if(no != pq[0])
        {
            count++;

            //Push all the multiples of no. to priority_queue
            for(let i = 0; i < size; i++){
                pq.push(no * a[i]);
            //    cnt+=1;
        }

        }
        pq.sort(function(a,b){return a-b;}) ;
    }
    // Return nth super ugly number
    return no;
    }

    /* Driver program to test above functions */
    let a=[2, 3,5];
    let size = a.length;
    document.write(ugly(a, size, 1000));

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
51200000
```

**时间复杂度:** O(n*size*logn)
**辅助空间:** O(n)
发现有不正确的地方请写评论，或者想分享以上讨论话题的更多信息。