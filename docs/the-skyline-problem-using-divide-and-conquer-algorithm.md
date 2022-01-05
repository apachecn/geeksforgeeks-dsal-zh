# 使用分治算法的天际线问题

> 原文:[https://www . geesforgeks . org/the-skyline-问题-使用分治算法/](https://www.geeksforgeeks.org/the-skyline-problem-using-divide-and-conquer-algorithm/)

给定二维城市中的 n 个矩形建筑，计算这些建筑的天际线，消除隐藏线。主要任务是从侧面查看建筑物，并移除所有不可见的部分。

所有建筑共用一个底部，每个**建筑**用三个一组(左、中、右)表示

*   ' left ':x 是否与左侧(或墙壁)协调。
*   ' right ':是右侧的 x 坐标
*   “ht”:是建筑物的高度。

A **天际线**是矩形条的集合。矩形**条**表示为一对(左，ht)，其中左是条左侧的 x 坐标，ht 是条的高度。
 **例:**

```
Input: Array of buildings
       { (1, 11, 5), (2, 6, 7), (3, 13, 9), (12, 7, 16), (14, 3, 25),
         (19, 18, 22), (23, 13, 29), (24, 4, 28) }
Output: Skyline (an array of rectangular strips)
        A strip has x coordinate of left side and height 
        (1, 11), (3, 13), (9, 0), (12, 7), (16, 3), (19, 18),  
        (22, 3), (25, 0)
Below image is for input 1 :

Consider following as another example when there is only one
building
Input:  {(1, 11, 5)}
Output: (1, 11), (5, 0)

```

一个**简单的解决方法**就是初始化天际线或者结果为空，然后一个一个的给天际线添加建筑。通过首先找到重叠的条带来添加建筑物。如果没有重叠条带，新建筑将添加新条带。如果发现重叠条带，则现有条带的高度可能会增加。该解决方案的时间复杂度为 0(n<sup>2</sup>

我们可以使用 **[【分治】](https://www.geeksforgeeks.org/divide-and-conquer-set-1-find-closest-pair-of-points/)** 在θ(nLogn)时间内找到 Skyline。这个想法类似于[合并排序](http://geeksquiz.com/merge-sort/)，把给定的一组建筑分成两个子集。递归地为两半构建天际线，最后合并两条天际线。

**如何合并两条天际线？**
这个想法类似于合并排序的合并，先从两个天际线的条带开始，比较 x 坐标。拾取 x 坐标较小的条带，并将其添加到结果中。添加条带的高度被认为是从 skyline1 和 skyline2 的当前高度的最大值。

**显示合并工作的示例:**

```
  Height of new Strip is always obtained by takin maximum of following
     (a) Current height from skyline1, say 'h1'.  
     (b) Current height from skyline2, say 'h2'
  h1 and h2 are initialized as 0\. h1 is updated when a strip from
  SkyLine1 is added to result and h2 is updated when a strip from 
  SkyLine2 is added.

  Skyline1 = {(1, 11),  (3, 13),  (9, 0),  (12, 7),  (16, 0)}
  Skyline2 = {(14, 3),  (19, 18), (22, 3), (23, 13),  (29, 0)}
  Result = {}
  h1 = 0, h2 = 0

  Compare (1, 11) and (14, 3).  Since first strip has smaller left x,
  add it to result and increment index for Skyline1\. 
  h1 = 11, New Height  = max(11, 0)   
  Result =   {(1, 11)}

  Compare (3, 13) and (14, 3). Since first strip has smaller left x,
  add it to result and increment index for Skyline1
  h1 = 13, New Height =  max(13, 0)
  Result =  {(1, 11), (3, 13)}   

  Similarly (9, 0) and (12, 7) are added.
  h1 = 7, New Height =  max(7, 0) = 7
  Result =   {(1, 11), (3, 13), (9, 0), (12, 7)}

  Compare (16, 0) and (14, 3). Since second strip has smaller left x, 
  it is added to result.
  h2 = 3, New Height =  max(7, 3) = 7
  Result =   {(1, 11), (3, 13), (9, 0), (12, 7), (14, 7)}

  Compare (16, 0) and (19, 18). Since first strip has smaller left x, 
  it is added to result.
  h1 = 0, New Height =  max(0, 3) = 3
  Result =   {(1, 11), (3, 13), (9, 0), (12, 7), (14, 7), (16, 3)}

Since Skyline1 has no more items, all remaining items of Skyline2 
are added 
  Result =   {(1, 11), (3, 13), (9, 0), (12, 7), (14, 7), (16, 3), 
              (19, 18), (22, 3), (23, 13), (29, 0)}

One observation about above output is, the strip (14, 7) is redundant
(There is already an strip of same height). We remove all redundant 
strips. 
  Result =   {(1, 11), (3, 13), (9, 0), (12, 7), (16, 3), (19, 18), 
              (22, 3), (23, 13), (29, 0)}

In below code, redundancy is handled by not appending a strip if the 
previous strip in result has same height.
```

下面是上述思想的 C++实现。

```
// A divide and conquer based C++
// program to find skyline of given buildings
#include <iostream>
using namespace std;

// A structure for building
struct Building {
    // x coordinate of left side
    int left;

    // height
    int ht;

    // x coordinate of right side
    int right;
};

// A strip in skyline
class Strip {
    // x coordinate of left side
    int left;

    // height
    int ht;

public:
    Strip(int l = 0, int h = 0)
    {
        left = l;
        ht = h;
    }
    friend class SkyLine;
};

// Skyline: To represent Output(An array of strips)
class SkyLine {
    // Array of strips
    Strip* arr;

    // Capacity of strip array
    int capacity;

    // Actual number of strips in array
    int n;

public:
    ~SkyLine() { delete[] arr; }
    int count() { return n; }

    // A function to merge another skyline
    // to this skyline
    SkyLine* Merge(SkyLine* other);

    // Constructor
    SkyLine(int cap)
    {
        capacity = cap;
        arr = new Strip[cap];
        n = 0;
    }

    // Function to add a strip 'st' to array
    void append(Strip* st)
    {
        // Check for redundant strip, a strip is
        // redundant if it has same height or left as previous
        if (n > 0 && arr[n - 1].ht == st->ht)
            return;
        if (n > 0 && arr[n - 1].left == st->left) {
            arr[n - 1].ht = max(arr[n - 1].ht, st->ht);
            return;
        }

        arr[n] = *st;
        n++;
    }

    // A utility function to print all strips of
    // skyline
    void print()
    {
        for (int i = 0; i < n; i++) {
            cout << " (" << arr[i].left << ", "
                 << arr[i].ht << "), ";
        }
    }
};

// This function returns skyline for a
// given array of buildings arr[l..h].
// This function is similar to mergeSort().
SkyLine* findSkyline(Building arr[], int l, int h)
{
    if (l == h) {
        SkyLine* res = new SkyLine(2);
        res->append(
            new Strip(
                arr[l].left, arr[l].ht));
        res->append(
            new Strip(
                arr[l].right, 0));
        return res;
    }

    int mid = (l + h) / 2;

    // Recur for left and right halves
    // and merge the two results
    SkyLine* sl = findSkyline(
        arr, l, mid);
    SkyLine* sr = findSkyline(
        arr, mid + 1, h);
    SkyLine* res = sl->Merge(sr);

    // To avoid memory leak
    delete sl;
    delete sr;

    // Return merged skyline
    return res;
}

// Similar to merge() in MergeSort
// This function merges another skyline
// 'other' to the skyline for which it is called.
// The function returns pointer to the
// resultant skyline
SkyLine* SkyLine::Merge(SkyLine* other)
{
    // Create a resultant skyline with
    // capacity as sum of two skylines
    SkyLine* res = new SkyLine(
        this->n + other->n);

    // To store current heights of two skylines
    int h1 = 0, h2 = 0;

    // Indexes of strips in two skylines
    int i = 0, j = 0;
    while (i < this->n && j < other->n) {
        // Compare x coordinates of left sides of two
        // skylines and put the smaller one in result
        if (this->arr[i].left < other->arr[j].left) {
            int x1 = this->arr[i].left;
            h1 = this->arr[i].ht;

            // Choose height as max of two heights
            int maxh = max(h1, h2);

            res->append(new Strip(x1, maxh));
            i++;
        }
        else {
            int x2 = other->arr[j].left;
            h2 = other->arr[j].ht;
            int maxh = max(h1, h2);
            res->append(new Strip(x2, maxh));
            j++;
        }
    }

    // If there are strips left in this
    // skyline or other skyline
    while (i < this->n) {
        res->append(&arr[i]);
        i++;
    }
    while (j < other->n) {
        res->append(&other->arr[j]);
        j++;
    }
    return res;
}

// Driver Function
int main()
{
    Building arr[] = {
        { 1, 11, 5 }, { 2, 6, 7 }, { 3, 13, 9 }, { 12, 7, 16 }, { 14, 3, 25 }, { 19, 18, 22 }, { 23, 13, 29 }, { 24, 4, 28 }
    };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Find skyline for given buildings
    // and print the skyline
    SkyLine* ptr = findSkyline(arr, 0, n - 1);
    cout << " Skyline for given buildings is \n";
    ptr->print();
    return 0;
}
```

**输出:**

```
 Skyline for given buildings is
 (1, 11),  (3, 13),  (9, 0),  (12, 7),  (16, 3),  (19, 18), 
 (22, 3),  (23, 13),  (29, 0),

```

上述递归实现的时间复杂度与合并排序相同。

t(n)= t(n/2)+θ(n)

上述递推的解是θ(nLogn)

 **参考文献:**

*   [http://facility . kfupm . edu . sa/ics/Dar wish/stuff/ics 353 讲义/Ch4Ch5.pdf](http://faculty.kfupm.edu.sa/ics/darwish/stuff/ics353handouts/Ch4Ch5.pdf)
*   [www . cs . ucf . edu/~ sarahb/COP 3503/讲座/DivideAndConquer.ppt](http://www.cs.ucf.edu/~sarahb/COP3503/Lectures/DivideAndConquer.ppt)

本文由 **Abhay Rathi** 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论