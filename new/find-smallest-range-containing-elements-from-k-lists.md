# 从 k 个列表中查找包含元素的最小范围

> 原文：[https://www.geeksforgeeks.org/find-smallest-range-containing-elements-from-k-lists/](https://www.geeksforgeeks.org/find-smallest-range-containing-elements-from-k-lists/)

给定 k 个大小为 n 的整数排序列表，从 k 个列表中的每一个中查找至少包含元素的最小范围。 如果找到多个最小范围，请打印其中任何一个。

**示例**：

```
Input: K = 3
arr1[] : [4, 7, 9, 12, 15]
arr2[] : [0, 8, 10, 14, 20]
arr3[] : [6, 12, 16, 30, 50]
Output:
The smallest range is [6 8]

Explanation: Smallest range is formed by 
number 7 from the first list, 8 from second
list and 6 from the third list.

Input: k = 3
arr1[] : [4, 7]
arr2[] : [1, 2]
arr3[] : [20, 40]
Output:
The smallest range is [2 20]

Explanation:The range [2, 20] contains 2, 4, 7, 20
which contains element from all the three arrays.

```

**<u>朴素的方法：</u>** 给定 K 个排序列表，找到一个范围，其中每个列表中至少有一个元素。 解决问题的想法非常简单，通过将 k 个元素的最小值和最大值取为范围，可以将 k 个指针保持在范围内。 最初，所有指针将指向所有 k 个数组的开头。 存储范围从最大到最小。 如果必须将范围最小化，则必须增加最小值或必须减少最大值。 数组排序时不能减小最大值，但可以增大最小值。 要继续增加最小值，请增加包含最小值的列表的指针，并更新范围，直到其中一个列表用完。

*   **算法**：

    1.  创建一个长度为 k 的额外空间 *ptr* ，以存储指针和一个初始化为最大值的变量 *minrange* 。

    2.  最初，每个列表的索引为 0，因此将 *ptr [0..k]* 的每个元素初始化为 0，数组 ptr 将在范围内存储元素的索引。

    3.  重复以下步骤，直到至少列出一个列表：

        1.  现在，在由 ptr [0…k]数组指向的所有列表的当前元素中找到最小值和最大值。

        2.  现在，如果电流（最大-最小值）小于最小范围，则更新最小范围。

        3.  递增指向当前最小元素的指针。

*   **Implementation:**

    ## C++

    ```cpp

    // C++ program to finds out smallest range that includes 
    // elements from each of the given sorted lists. 
    #include <bits/stdc++.h> 

    using namespace std; 

    #define N 5 

    // array for storing the current index of list i 
    int ptr[501]; 

    // This function takes an k sorted lists in the form of 
    // 2D array as an argument. It finds out smallest range 
    // that includes elements from each of the k lists. 
    void findSmallestRange(int arr[][N], int n, int k) 
    { 
        int i, minval, maxval, minrange, minel, maxel, flag, minind; 

        // initializing to 0 index; 
        for (i = 0; i <= k; i++) 
            ptr[i] = 0; 

        minrange = INT_MAX; 

        while (1) { 
            // for mainting the index of list containing the minimum element 
            minind = -1; 
            minval = INT_MAX; 
            maxval = INT_MIN; 
            flag = 0; 

            // iterating over all the list 
            for (i = 0; i < k; i++) { 
                // if every element of list[i] is traversed then break the loop 
                if (ptr[i] == n) { 
                    flag = 1; 
                    break; 
                } 
                // find minimum value among all the list elements pointing by the ptr[] array 
                if (ptr[i] < n && arr[i][ptr[i]] < minval) { 
                    minind = i; // update the index of the list 
                    minval = arr[i][ptr[i]]; 
                } 
                // find maximum value among all the list elements pointing by the ptr[] array 
                if (ptr[i] < n && arr[i][ptr[i]] > maxval) { 
                    maxval = arr[i][ptr[i]]; 
                } 
            } 

            // if any list exhaust we will not get any better answer, so break the while loop 
            if (flag) 
                break; 

            ptr[minind]++; 

            // updating the minrange 
            if ((maxval - minval) < minrange) { 
                minel = minval; 
                maxel = maxval; 
                minrange = maxel - minel; 
            } 
        } 

        printf("The smallest range is [%d, %d]\n", minel, maxel); 
    } 

    // Driver program to test above function 
    int main() 
    { 
        int arr[][N] = { 
            { 4, 7, 9, 12, 15 }, 
            { 0, 8, 10, 14, 20 }, 
            { 6, 12, 16, 30, 50 } 
        }; 

        int k = sizeof(arr) / sizeof(arr[0]); 

        findSmallestRange(arr, N, k); 

        return 0; 
    } 
    // This code is contributed by Aditya Krishna Namdeo 

    ```

    ## Java

    ```java

    // Java program to finds out smallest range that includes 
    // elements from each of the given sorted lists. 
    class GFG { 

        static final int N = 5; 

        // array for storing the current index of list i 
        static int ptr[] = new int[501]; 

        // This function takes an k sorted lists in the form of 
        // 2D array as an argument. It finds out smallest range 
        // that includes elements from each of the k lists. 
        static void findSmallestRange(int arr[][], int n, int k) 
        { 
            int i, minval, maxval, minrange, minel = 0, maxel = 0, flag, minind; 

            // initializing to 0 index; 
            for (i = 0; i <= k; i++) { 
                ptr[i] = 0; 
            } 

            minrange = Integer.MAX_VALUE; 

            while (true) { 
                // for mainting the index of list containing the minimum element 
                minind = -1; 
                minval = Integer.MAX_VALUE; 
                maxval = Integer.MIN_VALUE; 
                flag = 0; 

                // iterating over all the list 
                for (i = 0; i < k; i++) { 
                    // if every element of list[i] is traversed then break the loop 
                    if (ptr[i] == n) { 
                        flag = 1; 
                        break; 
                    } 
                    // find minimum value among all the list elements pointing by the ptr[] array 
                    if (ptr[i] < n && arr[i][ptr[i]] < minval) { 
                        minind = i; // update the index of the list 
                        minval = arr[i][ptr[i]]; 
                    } 
                    // find maximum value among all the list elements pointing by the ptr[] array 
                    if (ptr[i] < n && arr[i][ptr[i]] > maxval) { 
                        maxval = arr[i][ptr[i]]; 
                    } 
                } 

                // if any list exhaust we will not get any better answer, so break the while loop 
                if (flag == 1) { 
                    break; 
                } 

                ptr[minind]++; 

                // updating the minrange 
                if ((maxval - minval) < minrange) { 
                    minel = minval; 
                    maxel = maxval; 
                    minrange = maxel - minel; 
                } 
            } 
            System.out.printf("The smallest range is [%d, %d]\n", minel, maxel); 
        } 

        // Driver program to test above function 
        public static void main(String[] args) 
        { 

            int arr[][] = { 
                { 4, 7, 9, 12, 15 }, 
                { 0, 8, 10, 14, 20 }, 
                { 6, 12, 16, 30, 50 } 
            }; 

            int k = arr.length; 

            findSmallestRange(arr, N, k); 
        } 
    } 
    // this code contributed by Rajput-Ji 

    ```

    ## 蟒蛇

    ```

    # Python3 program to finds out  
    # smallest range that includes 
    # elements from each of the  
    # given sorted lists. 

    N = 5

    # array for storing the  
    # current index of list i 
    ptr = [0 for i in range(501)] 

    # This function takes an k sorted  
    # lists in the form of 2D array as  
    # an argument. It finds out smallest 
    # range that includes elements from  
    # each of the k lists. 
    def findSmallestRange(arr, n, k): 

        i, minval, maxval, minrange, minel, maxel, flag, minind = 0, 0, 0, 0, 0, 0, 0, 0

        # initializing to 0 index 
        for i in range(k + 1): 
            ptr[i] = 0

        minrange = 10**9

        while(1):     

                # for mainting the index of list  
                # containing the minimum element 
            minind = -1
            minval = 10**9
            maxval = -10**9
            flag = 0

            # iterating over all the list 
            for i in range(k): 

                    # if every element of list[i] is  
                    # traversed then break the loop 
                if(ptr[i] == n): 
                    flag = 1    
                    break

                # find minimum value among all the list  
                # elements pointing by the ptr[] array  
                if(ptr[i] < n and arr[i][ptr[i]] < minval): 
                    minind = i # update the index of the list 
                    minval = arr[i][ptr[i]] 

                # find maximum value among all the  
                # list elements pointing by the ptr[] array 
                if(ptr[i] < n and arr[i][ptr[i]] > maxval): 
                    maxval = arr[i][ptr[i]] 

            # if any list exhaust we will  
            # not get any better answer, 
            # so break the while loop 
            if(flag): 
                break

            ptr[minind] += 1

            # updating the minrange 
            if((maxval-minval) < minrange): 
                minel = minval 
                maxel = maxval 
                minrange = maxel - minel 

        print("The smallest range is [", minel, maxel, "]") 

    # Driver code 
    arr = [ 
        [4, 7, 9, 12, 15], 
        [0, 8, 10, 14, 20], 
        [6, 12, 16, 30, 50] 
        ] 

    k = len(arr) 

    findSmallestRange(arr, N, k) 

    # This code is contributed by mohit kumar 

    ```

    ## C#

    ```cs

    // C# program to finds out smallest 
    // range that includes elements from 
    // each of the given sorted lists. 
    using System; 

    class GFG { 

        static int N = 5; 

        // array for storing the current index of list i 
        static int[] ptr = new int[501]; 

        // This function takes an k sorted 
        // lists in the form of 2D array as 
        // an argument. It finds out smallest range 
        // that includes elements from each of the k lists. 
        static void findSmallestRange(int[, ] arr, 
                                      int n, int k) 
        { 
            int i, minval, maxval, minrange, 
                minel = 0, maxel = 0, flag, minind; 

            // initializing to 0 index; 
            for (i = 0; i <= k; i++) { 
                ptr[i] = 0; 
            } 

            minrange = int.MaxValue; 

            while (true) { 
                // for mainting the index of 
                // list containing the minimum element 
                minind = -1; 
                minval = int.MaxValue; 
                maxval = int.MinValue; 
                flag = 0; 

                // iterating over all the list 
                for (i = 0; i < k; i++) { 
                    // if every element of list[i] 
                    // is traversed then break the loop 
                    if (ptr[i] == n) { 
                        flag = 1; 
                        break; 
                    } 

                    // find minimum value among all the 
                    // list elements pointing by the ptr[] array 
                    if (ptr[i] < n && arr[i, ptr[i]] < minval) { 
                        minind = i; // update the index of the list 
                        minval = arr[i, ptr[i]]; 
                    } 

                    // find maximum value among all the 
                    // list elements pointing by the ptr[] array 
                    if (ptr[i] < n && arr[i, ptr[i]] > maxval) { 
                        maxval = arr[i, ptr[i]]; 
                    } 
                } 

                // if any list exhaust we will 
                // not get any better answer, 
                // so break the while loop 
                if (flag == 1) { 
                    break; 
                } 

                ptr[minind]++; 

                // updating the minrange 
                if ((maxval - minval) < minrange) { 
                    minel = minval; 
                    maxel = maxval; 
                    minrange = maxel - minel; 
                } 
            } 
            Console.WriteLine("The smallest range is"
                                  + "[{0}, {1}]\n", 
                              minel, maxel); 
        } 

        // Driver code 
        public static void Main(String[] args) 
        { 

            int[, ] arr = { 
                { 4, 7, 9, 12, 15 }, 
                { 0, 8, 10, 14, 20 }, 
                { 6, 12, 16, 30, 50 } 
            }; 

            int k = arr.GetLength(0); 

            findSmallestRange(arr, N, k); 
        } 
    } 

    // This code has been contributed by 29AjayKumar 

    ```

*   **输出**：

    ```
    The smallest range is [6 8]
    ```

*   **Complexity Analysis:**

    *   **时间复杂度**：O（n * k <sup>2</sup> ），要找到长度为 k 的数组中的最大值和最小值，所需时间为 O（k），并遍历所有 k 长度为 n 的数组（在最坏的情况下），时间复杂度为 O（n * k），则总时间复杂度为 O（n * k <sup>2</sup> ）。

    *   **空间复杂度**：O（k），需要一个长度为 k 的额外数组，因此空间复杂度为 O（k）

**<u>高效方法</u>**：该方法保持不变，但是可以通过使用最小堆或*优先级队列*来降低时间复杂度。 最小堆可用于以对数时间或 log k 时间而不是线性时间来查找最大值和最小值。 其余方法保持不变。

*   **算法**：

    1.  创建一个 Min 堆来存储 k 个元素，每个数组一个，并将初始化为最大值的变量 *minrange* 初始化为最大值，还保留一个变量 *max* 以存储最大整数。

    2.  最初，将每个列表中每个元素的第一个元素放置在 *max* 中。

    3.  重复以下步骤，直到至少列出一个列表：

        1.  要查找最小值或 *min* ，请使用 Min 堆的顶部或根，它是最小元素。

        2.  现在，如果电流（最大-最小值）小于最小范围，则更新最小范围。

        3.  从优先级队列中删除 top 或 root 元素，然后从列表中插入包含 min 元素的下一个元素，并使用插入的新元素更新 max。

*   **实现**：

    ## C++

    ```cpp

    // C++ program to finds out smallest range that includes 
    // elements from each of the given sorted lists. 
    #include <bits/stdc++.h> 
    using namespace std; 

    #define N 5 

    // A min heap node 
    struct MinHeapNode { 
        // The element to be stored 
        int element; 

        // index of the list from which the element is taken 
        int i; 

        // index of the next element to be picked from list 
        int j; 
    }; 

    // Prototype of a utility function to swap two min heap nodes 
    void swap(MinHeapNode* x, MinHeapNode* y); 

    // A class for Min Heap 
    class MinHeap { 

        // pointer to array of elements in heap 
        MinHeapNode* harr; 

        // size of min heap 
        int heap_size; 

    public: 
        // Constructor: creates a min heap of given size 
        MinHeap(MinHeapNode a[], int size); 

        // to heapify a subtree with root at given index 
        void MinHeapify(int); 

        // to get index of left child of node at index i 
        int left(int i) { return (2 * i + 1); } 

        // to get index of right child of node at index i 
        int right(int i) { return (2 * i + 2); } 

        // to get the root 
        MinHeapNode getMin() { return harr[0]; } 

        // to replace root with new node x and heapify() new root 
        void replaceMin(MinHeapNode x) 
        { 
            harr[0] = x; 
            MinHeapify(0); 
        } 
    }; 

    // Constructor: Builds a heap from a 
    // given array a[] of given size 
    MinHeap::MinHeap(MinHeapNode a[], int size) 
    { 
        heap_size = size; 
        harr = a; // store address of array 
        int i = (heap_size - 1) / 2; 
        while (i >= 0) { 
            MinHeapify(i); 
            i--; 
        } 
    } 

    // A recursive method to heapify a subtree with root at 
    // given index. This method assumes that the subtrees 
    // are already heapified 
    void MinHeap::MinHeapify(int i) 
    { 
        int l = left(i); 
        int r = right(i); 
        int smallest = i; 
        if (l < heap_size && harr[l].element < harr[i].element) 
            smallest = l; 
        if (r < heap_size && harr[r].element < harr[smallest].element) 
            smallest = r; 
        if (smallest != i) { 
            swap(harr[i], harr[smallest]); 
            MinHeapify(smallest); 
        } 
    } 

    // This function takes an k sorted lists in the form of 
    // 2D array as an argument. It finds out smallest range 
    // that includes elements from each of the k lists. 
    void findSmallestRange(int arr[][N], int k) 
    { 
        // Create a min heap with k heap nodes. Every heap node 
        // has first element of an list 
        int range = INT_MAX; 
        int min = INT_MAX, max = INT_MIN; 
        int start, end; 

        MinHeapNode* harr = new MinHeapNode[k]; 
        for (int i = 0; i < k; i++) { 
            // Store the first element 
            harr[i].element = arr[i][0]; 

            // index of list 
            harr[i].i = i; 

            // Index of next element to be stored 
            // from list 
            harr[i].j = 1; 

            // store max element 
            if (harr[i].element > max) 
                max = harr[i].element; 
        } 

        // Create the heap 
        MinHeap hp(harr, k); 

        // Now one by one get the minimum element from min 
        // heap and replace it with next element of its list 
        while (1) { 
            // Get the minimum element and store it in output 
            MinHeapNode root = hp.getMin(); 

            // update min 
            min = hp.getMin().element; 

            // update range 
            if (range > max - min + 1) { 
                range = max - min + 1; 
                start = min; 
                end = max; 
            } 

            // Find the next element that will replace current 
            // root of heap. The next element belongs to same 
            // list as the current root. 
            if (root.j < N) { 
                root.element = arr[root.i][root.j]; 
                root.j += 1; 

                // update max element 
                if (root.element > max) 
                    max = root.element; 
            } 

            // break if we have reached end of any list 
            else
                break; 

            // Replace root with next element of list 
            hp.replaceMin(root); 
        } 

        cout << "The smallest range is "
             << "["
             << start << " " << end << "]" << endl; 
        ; 
    } 

    // Driver program to test above functions 
    int main() 
    { 
        int arr[][N] = { 
            { 4, 7, 9, 12, 15 }, 
            { 0, 8, 10, 14, 20 }, 
            { 6, 12, 16, 30, 50 } 
        }; 
        int k = sizeof(arr) / sizeof(arr[0]); 

        findSmallestRange(arr, k); 

        return 0; 
    } 

    ```

    ## Java

    ```java

    // Java program to find out smallest 
    // range that includes elements from 
    // each of the given sorted lists. 
    class GFG { 

        // A min heap node 
        static class Node { 
            // The element to be stored 
            int ele; 

            // index of the list from which 
            // the element is taken 
            int i; 

            // index of the next element 
            // to be picked from list 
            int j; 

            Node(int a, int b, int c) 
            { 
                this.ele = a; 
                this.i = b; 
                this.j = c; 
            } 
        } 

        // A class for Min Heap 
        static class MinHeap { 
            Node[] harr; // array of elements in heap 
            int size; // size of min heap 

            // Constructor: creates a min heap 
            // of given size 
            MinHeap(Node[] arr, int size) 
            { 
                this.harr = arr; 
                this.size = size; 
                int i = (size - 1) / 2; 
                while (i >= 0) { 
                    MinHeapify(i); 
                    i--; 
                } 
            } 

            // to get index of left child 
            // of node at index i 
            int left(int i) 
            { 
                return 2 * i + 1; 
            } 

            // to get index of right child 
            // of node at index i 
            int right(int i) 
            { 
                return 2 * i + 2; 
            } 

            // to heapify a subtree with 
            // root at given index 
            void MinHeapify(int i) 
            { 
                int l = left(i); 
                int r = right(i); 
                int small = i; 
                if (l < size && harr[l].ele < harr[i].ele) 
                    small = l; 
                if (r < size && harr[r].ele < harr[small].ele) 
                    small = r; 
                if (small != i) { 
                    swap(small, i); 
                    MinHeapify(small); 
                } 
            } 

            void swap(int i, int j) 
            { 
                Node temp = harr[i]; 
                harr[i] = harr[j]; 
                harr[j] = temp; 
            } 

            // to get the root 
            Node getMin() 
            { 
                return harr[0]; 
            } 

            // to replace root with new node x 
            // and heapify() new root 
            void replaceMin(Node x) 
            { 
                harr[0] = x; 
                MinHeapify(0); 
            } 
        } 

        // This function takes an k sorted lists 
        // in the form of 2D array as an argument. 
        // It finds out smallest range that includes 
        // elements from each of the k lists. 
        static void findSmallestRange(int[][] arr, int k) 
        { 
            int range = Integer.MAX_VALUE; 
            int min = Integer.MAX_VALUE; 
            int max = Integer.MIN_VALUE; 
            int start = -1, end = -1; 

            int n = arr[0].length; 

            // Create a min heap with k heap nodes. 
            // Every heap node has first element of an list 
            Node[] arr1 = new Node[k]; 
            for (int i = 0; i < k; i++) { 
                Node node = new Node(arr[i][0], i, 1); 
                arr1[i] = node; 

                // store max element 
                max = Math.max(max, node.ele); 
            } 

            // Create the heap 
            MinHeap mh = new MinHeap(arr1, k); 

            // Now one by one get the minimum element 
            // from min heap and replace it with 
            // next element of its list 
            while (true) { 
                // Get the minimum element and 
                // store it in output 
                Node root = mh.getMin(); 

                // update min 
                min = root.ele; 

                // update range 
                if (range > max - min + 1) { 
                    range = max - min + 1; 
                    start = min; 
                    end = max; 
                } 

                // Find the next element that will 
                // replace current root of heap. 
                // The next element belongs to same 
                // list as the current root. 
                if (root.j < n) { 
                    root.ele = arr[root.i][root.j]; 
                    root.j++; 

                    // update max element 
                    if (root.ele > max) 
                        max = root.ele; 
                } 
                // break if we have reached 
                // end of any list 
                else
                    break; 

                // Replace root with next element of list 
                mh.replaceMin(root); 
            } 
            System.out.print("The smallest range is [" + start + " " + end + "]"); 
        } 

        // Driver Code 
        public static void main(String[] args) 
        { 
            int arr[][] = { { 4, 7, 9, 12, 15 }, 
                            { 0, 8, 10, 14, 20 }, 
                            { 6, 12, 16, 30, 50 } }; 

            int k = arr.length; 

            findSmallestRange(arr, k); 
        } 
    } 

    // This code is contributed by nobody_cares 

    ```

    ## C#

    ```cs

    // C# program to find out smallest 
    // range that includes elements from 
    // each of the given sorted lists. 
    using System; 
    using System.Collections.Generic; 

    class GFG { 

        // A min heap node 
        public class Node { 
            // The element to be stored 
            public int ele; 

            // index of the list from which 
            // the element is taken 
            public int i; 

            // index of the next element 
            // to be picked from list 
            public int j; 

            public Node(int a, int b, int c) 
            { 
                this.ele = a; 
                this.i = b; 
                this.j = c; 
            } 
        } 

        // A class for Min Heap 
        public class MinHeap { 
            // array of elements in heap 
            public Node[] harr; 

            // size of min heap 
            public int size; 

            // Constructor: creates a min heap 
            // of given size 
            public MinHeap(Node[] arr, int size) 
            { 
                this.harr = arr; 
                this.size = size; 
                int i = (size - 1) / 2; 
                while (i >= 0) { 
                    MinHeapify(i); 
                    i--; 
                } 
            } 

            // to get index of left child 
            // of node at index i 
            int left(int i) 
            { 
                return 2 * i + 1; 
            } 

            // to get index of right child 
            // of node at index i 
            int right(int i) 
            { 
                return 2 * i + 2; 
            } 

            // to heapify a subtree with 
            // root at given index 
            void MinHeapify(int i) 
            { 
                int l = left(i); 
                int r = right(i); 
                int small = i; 
                if (l < size && harr[l].ele < harr[i].ele) 
                    small = l; 
                if (r < size && harr[r].ele < harr[small].ele) 
                    small = r; 
                if (small != i) { 
                    swap(small, i); 
                    MinHeapify(small); 
                } 
            } 

            void swap(int i, int j) 
            { 
                Node temp = harr[i]; 
                harr[i] = harr[j]; 
                harr[j] = temp; 
            } 

            // to get the root 
            public Node getMin() 
            { 
                return harr[0]; 
            } 

            // to replace root with new node x 
            // and heapify() new root 
            public void replaceMin(Node x) 
            { 
                harr[0] = x; 
                MinHeapify(0); 
            } 
        } 

        // This function takes an k sorted lists 
        // in the form of 2D array as an argument. 
        // It finds out smallest range that includes 
        // elements from each of the k lists. 
        static void findSmallestRange(int[, ] arr, int k) 
        { 
            int range = int.MaxValue; 
            int min = int.MaxValue; 
            int max = int.MinValue; 
            int start = -1, end = -1; 

            int n = arr.GetLength(0); 

            // Create a min heap with k heap nodes. 
            // Every heap node has first element of an list 
            Node[] arr1 = new Node[k]; 
            for (int i = 0; i < k; i++) { 
                Node node = new Node(arr[i, 0], i, 1); 
                arr1[i] = node; 

                // store max element 
                max = Math.Max(max, node.ele); 
            } 

            // Create the heap 
            MinHeap mh = new MinHeap(arr1, k); 

            // Now one by one get the minimum element 
            // from min heap and replace it with 
            // next element of its list 
            while (true) { 
                // Get the minimum element and 
                // store it in output 
                Node root = mh.getMin(); 

                // update min 
                min = root.ele; 

                // update range 
                if (range > max - min + 1) { 
                    range = max - min + 1; 
                    start = min; 
                    end = max; 
                } 

                // Find the next element that will 
                // replace current root of heap. 
                // The next element belongs to same 
                // list as the current root. 
                if (root.j < n) { 
                    root.ele = arr[root.i, root.j]; 
                    root.j++; 

                    // update max element 
                    if (root.ele > max) 
                        max = root.ele; 
                } 
                else
                    break; // break if we have reached 
                // end of any list 

                // Replace root with next element of list 
                mh.replaceMin(root); 
            } 
            Console.Write("The smallest range is [" + start + " " + end + "]"); 
        } 

        // Driver Code 
        public static void Main(String[] args) 
        { 
            int[, ] arr = { { 4, 7, 9, 12, 15 }, 
                            { 0, 8, 10, 14, 20 }, 
                            { 6, 12, 16, 30, 50 } }; 

            int k = arr.GetLength(0); 

            findSmallestRange(arr, k); 
        } 
    } 

    // This code is contributed by Rajput-Ji 

    ```

*   **输出**：

    ```
    The smallest range is [6 8]
    ```

*   **Complexity Analysis:**

    *   **时间复杂度**：O（n * k * log k）。

        为了找到长度为 k 的最小堆中的最大值和最小值，所需时间为 O（log k），并遍历所有长度为 n 的 k 个数组（在最坏的情况下），时间复杂度为 O（n * k），则总时间复杂度为 O（n * k * log k）。

    *   **空间复杂度**：O（k）。

        优先级队列将存储 k 个元素，因此空间复杂度 os O（k）

本文由 **Aditya Goel** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以写一篇文章，并将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

