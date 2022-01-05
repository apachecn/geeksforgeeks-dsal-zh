# 使用计数器实现最近最少使用(LRU)页面替换算法

> 原文:[https://www . geesforgeks . org/最近最少使用的 lru 页面替换算法使用计数器的实现/](https://www.geeksforgeeks.org/implementation-of-least-recently-used-lru-page-replacement-algorithm-using-counters/)

先决条件–[最近最少使用的(LRU)页面替换算法](https://www.geeksforgeeks.org/program-for-least-recently-used-lru-page-replacement-algorithm/)
最近最少使用的页面替换算法替换最近未使用的页面。

**实现:**
在本文中，LRU 是使用计数器实现的，一个 ctime(即 counter)变量用来表示当前时间，它为引用数组的每一页递增。[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的向量用于表示页面帧，该对的第一个变量是页码，第二个变量是当前时间。当要插入新页面并且框架已满时，具有最小 ctime 的页面将被删除(因为它是最近使用最少的页面)。如果页面再次被访问，ctime 的值将被更新。

**注意:**
最小 ctime(计数器/当前时间)值代表最近使用最少的页面。

**示例:**

```
Reference array is : 0, 0, 0, 2, 3, 0, 5, 7, 1, 2, 0, 8
Output :
When the number of frames is : 3
The number of page faults are : 9

Reference array is : 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 0, 1, 2, 3, 0, 0
Output :
When the number of frames is : 3
The number of page faults are : 15 
```

**代码:**

```
#include <bits/stdc++.h>

using namespace std;

// To calculate the number of page faults
void pageFaults(int frame_size, int* ref, int len, int ctime)
{
    // Count variable to count the
    // number of page faults
    int cnt = 0;
    // Arr to simulate frames
    vector<pair<int, int> > arr;

    // To initialise the array
    for (int i = 0; i < frame_size; i++) {
        arr.push_back(make_pair(-1, ctime));
    }

    int page;

    for (int i = 0; i < len; i++) {
        page = ref[i];
        auto it = arr.begin();

        for (it = arr.begin(); it != arr.end(); it++) {
            if (it->first == page) {
                break;
            }
        }

        // If page is found
        if (it != arr.end()) {
            // update the value of
            // current time
            it->second = ctime;
        }

        // If page is not found
        else {
            // Find the page with min value of ctime,
            // as it will be the least recently used
            vector<pair<int, int> >::iterator pos;
            pos = arr.begin();
            int min = pos->second;
            for (auto itr = arr.begin(); itr != arr.end(); itr++) {
                if (itr->second < min) {
                    pos = itr;
                    min = pos->second;
                }
            }

            // Erase this page from the frame vector
            arr.erase(pos);

            // Insert the new page
            arr.push_back(make_pair(page, ctime));
            cnt++;
        }
        ctime++;
    }
    cout << "The number of page faults is : " << cnt << endl;
}

int main()
{
    // This is the reference array
    int ref[] = { 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5 };
    int len = sizeof(ref) / sizeof(ref[0]);
    int frame_size = 3;
    // Ctime represents current time,
    // it is incremented for every page
    int ctime = 0;
    pageFaults(frame_size, ref, len, ctime);
}
```

**Output:**

```
The number of page faults is : 10

```