# 如何将 N 个物体均匀的放入 N 个相邻移动的地方

> 原文:[https://www . geeksforgeeks . org/如何通过相邻移动将 n 个对象平均放置到 n 个位置/](https://www.geeksforgeeks.org/how-to-evenly-put-n-objects-into-n-places-with-adjacent-moves/)

假设有 N 个对象不均匀地分布在 N 个容器中。您可以将一个对象从一个容器移动到相邻的容器，这被认为是一次移动。什么策略可以最大限度地减少移动次数，从而保持时间复杂度为 0(N)？
示例:

> 例 1。假设您有 5 个容器，填充为:
> 1，2，1，1，0
> 您将需要三次移动来将一个对象从第二个容器传递到最后一个- >，从第二个移动到第三个，然后移动到第四个，最后移动到第五个:
> 1，1，2，1，0
> 1，1，1，2，0
> 1，1，1，1
> 示例 2。现在更复杂一点。
> 假设你有 5 个容器，所有对象都在最后一个容器中:
> 0，0，0，0，5
> 显然，你会从右向左移动:
> 0，0，0，1，4
> 0，0，1，0，4
> 0，1，0，0，4
> 1，0，0，0，4
> 1，0，0，1，3
> 1，0，1，0，3
> 所有物体都在中间:
> 0，0，5，0，0
> 看起来没错:
> 0，1，4，0，0
> 1，0，4，0，0
> 1，1，3，0，0
> 1，1，2，1，0
> 1，1，2，0，1
> 1，1，1，1，1
> 需要 6 次移动

这个问题弱弱地提醒了一个所谓的[鸽巢或狄利克雷原理](https://en.wikipedia.org/wiki/Pigeonhole_principle)–n 个物品放入 m 个容器中，用 n > m，那么至少一个容器必须包含一个以上的物品。因此它出现在标题中。
**进场**听起来相当琐碎:沿着集装箱排从头到尾移动，如果你遇到一个空集装箱，把它装满，如果你遇到一个有几个物体(不止一个)的集装箱，尽量把量减少到只有一个。
更准确地说，一个人必须保持一个有太多对象的容器队列和另一个空位置队列，并使用它们来传递对象。显然，由于我们试图一有可能就传递对象，所以在我们做了所有可能的运动后，每一步都会有一个队列变空。
再详细一点:
每次遇到空的地方，我们都会检查有多个物体的容器队列中是否有东西，如果有，就拿一个物体把空的地方填满。如果没有，将这个空位置添加到队列中。
每次遇到人满为患的集装箱，都要检查空位的队列是否有东西，如果有，尽量把当前集装箱的物品尽可能多的放入这些空集装箱，从它们的队列中取出。如果没有空的，将过度拥挤的集装箱推到满集装箱的队列中。
过度拥挤集装箱的队列中有成对的数字:多余物品的位置和数量。空容器的队列只保留位置的数字，因为它们是空的。
如果输入是以对象 A 的坐标数组的形式提供的，首先将其重组为每个位置的数量数组。
这个问题可以不止一个维度，就像启发了这篇文章的[编码挑战 Selenium 2016](https://app.codility.com/programmers/task/sprinklers_arrangement/) 一样。但是因为维度是独立的，所以每个维度的结果只是被总结以得到最终的答案。
余数问题的完整实现包括最终答案取模 10^9+7.
示例:

```
Input : 
Coordinates of objects are
X = [1, 2, 2, 3, 4] and array Y = [1, 1, 4, 5, 4] 
Output :
5
Input :
X = [1, 1, 1, 1] and array Y = [1, 2, 3, 4] 
Output :
6
Input :
 X = [1, 1, 2] and array Y = [1, 2, 1]
Output :
4
```

注:还有另一种方法，可能会在另一篇文章中介绍，灵感来自于《余度[未来移动性](https://app.codility.com/programmers/challenges/future_mobility2018/)挑战》中一个更难的问题。包括以下步骤:

*   从每个位置减去 1，现在我们争夺所有 0，而不是所有 1
*   将数组切割成片段，例如在每个片段中，对象的移动都是在一个方向上，每个片段的开头和结尾都可以去掉零。样品:1，0，-1，0，-2，2 切成 1，0，-1 和-2，2。切割点由前缀和的零发现
*   计算每个碎片的第二个积分。那是前缀从左到右的前缀。最正确的值是移动量。样本序列:1，0，-1。前缀是 1，1，0。第二个前缀是 1，2，2。这个片段的答案是 2(从 0 到 2 的两次移动)
*   结果是所有片段结果的总和

最后执行第一种方式:

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <queue>
#include <vector>
using namespace std;
#define MODULO 1000000007

/* Utility function for one dimension
unsigned long long solution(vector<int>& A)
Parameters: vector<int>& A - an array of numbers
of objects per container
Return value: How many moves to make all containers
              have one object */
unsigned long long solution(vector<int>& A)
{
    // the final result cannot be less than
    // zero, so we initiate it as 0
    unsigned long long res = 0;

    // just to keep the amount of objects for future usage
    const unsigned int len = (unsigned int)A.size();

     // The queue of objects that are ready for move,
     // as explained in the introduction. The queue is
     // of pairs, where the first value is the index
     // in the row of containers, the second is the
     // number of objects there currently.
    queue<pair<unsigned int, unsigned int> > depot;

     // The queue of vacant containers that are ready
     // to be filled, as explained in the introduction,
     // just the index on the row, since they are
    // empty - no amount, zero is meant.
    queue<unsigned int> depotOfEmpties;

    // how many objects have coordinate i
    vector<unsigned int> places(len, 0);

    // initiates the data into a more convenient way,
    // not coordinates of objects but how many objects
    // are per place
    for (unsigned int i = 0; i < len; i++) {
        places.at(A.at(i) - 1)++;
    }

    // main loop, movement along containers as
    // explained in the introduction
    for (unsigned int i = 0; i < len; i++) {

        // if we meet the empty container at place i
        if (0 == places.at(i)) {

            // we check that not objects awaiting
            // to movement, the queue of objects
            // is possible empty
            if (depot.empty()) {

                 // if true, no object to move, we
                 // insert the empty container into
                 // a queue of empties 
                depotOfEmpties.push(i);
            }

            // there are some object to move, take
            // the first from the queue  
            else {

                // and find how distant it is
                unsigned int distance = (i - depot.front().first);

                // we move one object and making
                // "distance" moves by it
                res += distance;

                // since the result is expected MODULO
                res = res % MODULO;

                // now one object left the queue
                // for movement, so we discount it
                depot.front().second--;

                 // if some elements in the objects
                 // queue may loose all objects, 
                while (!depot.empty() && depot.front().second < 1) {
                    depot.pop(); // remove all them from the queue
                }
            }
        }

        // places.at(i) > 0, so we found the current
        // container not empty
        else {

            // if it has only one object, nothing must
            // be done
            if (1 == places.at(i)) {

                // so the object remains in its place,
                // go further
                continue;            
            }

            // there are more than one there, need
            // to remove some
            else {

                // how many to remove? To leave one
                unsigned int pieces = places.at(i) - 1;

                // how many empty places are awaiting to fill
                // currently? Are they enough to remove "pieces"?
                unsigned int lenEmptySequence = depotOfEmpties.size();

                // Yes, we have places for all objects
                // to remove from te current 
                if (pieces <= lenEmptySequence) {

                    // move all objects except one
                    for (unsigned int j = 0; j < pieces; j++) {

                        // add to the answer and apply MODULOto
                        // prevent overflow
                        res = (res + i - depotOfEmpties.front()) % MODULO;

                        // remove former empty from the queue of empties
                        depotOfEmpties.pop();
                    }
                }

                // empty vacancies are not enough or absent at all
                else {
                    for (unsigned int j = 0; j < lenEmptySequence; j++) {

                        // fill what we can
                        res = (res + i - depotOfEmpties.front()) % MODULO;

                        // and remove filled from the vacancies queue 
                        depotOfEmpties.pop();
                    }

                    // since we still have too many objects in
                    // this container, push it into the queue for
                    // overcrowded containers
                    depot.push(pair<unsigned int, unsigned int>(i,
                                        pieces - lenEmptySequence));
                }
            }
        }
    }

    // the main loop end
    return res; // return the result
}

/* Main function for two dimensions as in
   Codility problem
int solution(vector<int>& A, vector<int>& B)
Parameters:
 vector<int>& A - coordinates x of the objects
 vector<int>& B - coordinates y of the objects
Return value:
 No. of moves to make all verticals and horizontals
 have one object
*/
int solution(vector<int>& A, vector<int>& B)
{
    unsigned long long res = solution(B);
    res += solution(A);
    res = res % MODULO;
    return (int)res;
}

// test utility for the driver below
#include <iostream>
void test(vector<int>& A, vector<int>& B, int expected,
         bool printAll = false, bool doNotPrint = true)
{
    int res = solution(A, B);
    if ((expected != res && !doNotPrint) || printAll) {
        for (size_t i = 0; i < A.size(); i++) {
            cout << A.at(i) << " ";
        }
        cout << endl;
        for (size_t i = 0; i < B.size(); i++) {
            cout << B.at(i) << " ";
        }
        cout << endl;
        if (expected != res)
            cout << "Error! Expected: " << expected << "  ";
        else
            cout << "Expected: " << expected << "  ";
    }
    cout << " Result: " << res << endl;
}

// Driver (main)
int main()
{
    int A4[] = { 1, 2, 2, 3, 4 };
    int B4[] = { 1, 1, 4, 5, 4 };
    vector<int> VA(A4, A4 + 5);
    vector<int> VB(B4, B4 + 5);
    test(VA, VB, 5);

    int A0[] = { 1, 1, 1, 1 };
    int B0[] = { 1, 2, 3, 4 };
    VA = vector<int>(A0, A0 + 4);
    VB = vector<int>(B0, B0 + 4);
    test(VA, VB, 6);

    int A2[] = { 1, 1, 2 };
    int B2[] = { 1, 2, 1 };
    VA = vector<int>(A2, A2 + 3);
    VB = vector<int>(B2, B2 + 3);
    test(VA, VB, 4);

    // square case
    int A3[] = { 1, 2, 3, 1, 2, 3, 1, 2, 3 };
    int B3[] = { 1, 1, 1, 2, 2, 2, 3, 3, 3 };
    VA = vector<int>(A3, A3 + 9);
    VB = vector<int>(B3, B3 + 9);
    test(VA, VB, 54);
    // also
    int A5[] = { 7, 8, 9, 7, 8, 9, 7, 8, 9 };
    int B5[] = { 7, 7, 7, 8, 8, 8, 9, 9, 9 };
    VA = vector<int>(A5, A5 + 9);
    VB = vector<int>(B5, B5 + 9);
    test(VA, VB, 54);

    int A6[] = { 1, 1, 2, 3 };
    int B6[] = { 1, 2, 3, 4 };
    VA = vector<int>(A6, A6 + 4);
    VB = vector<int>(B6, B6 + 4);
    test(VA, VB, 3);
    test(VB, VA, 3);

    int A7[] = { 1, 1, 3, 5, 5 };
    int B7[] = { 1, 5, 3, 1, 5 };
    VA = vector<int>(A7, A7 + 5);
    VB = vector<int>(B7, B7 + 5);
    test(VA, VB, 4);
    test(VB, VA, 4);

    // smaller square case
    int A8[] = { 1, 2, 1, 2 };
    int B8[] = { 1, 1, 2, 2 };
    VA = vector<int>(A8, A8 + 4);
    VB = vector<int>(B8, B8 + 4);
    test(VA, VB, 8);

    int A9[] = { 3, 4, 3, 4 };
    int B9[] = { 3, 3, 4, 4 };
    VA = vector<int>(A9, A9 + 4);
    VB = vector<int>(B9, B9 + 4);
    test(VA, VB, 8);

    int A10[] = { 1, 2, 3, 4, 1, 2, 3, 4, 1,
                     2, 3, 4, 1, 2, 3, 4 };
    int B10[] = { 1, 1, 1, 1, 2, 2, 2, 2, 3,
                      3, 3, 3, 4, 4, 4, 4 };
    VA = vector<int>(A10, A10 + 16);
    VB = vector<int>(B10, B10 + 16);
    test(VA, VB, 192);

    int A11[] = { 13, 14, 15, 16, 13, 14, 15,
         16, 13, 14, 15, 16, 13, 14, 15, 16 };
    int B11[] = { 13, 13, 13, 13, 14, 14, 14,
         14, 15, 15, 15, 15, 16, 16, 16, 16 };
    VA = vector<int>(A11, A11 + 16);
    VB = vector<int>(B11, B11 + 16);
    test(VA, VB, 192);
    return 0;
}
```

**Output:** 

```
Result: 5
 Result: 6
 Result: 4
 Result: 54
 Result: 54
 Result: 3
 Result: 3
 Result: 4
 Result: 4
 Result: 8
 Result: 8
 Result: 192
 Result: 192
```