# Java 列表中的最小值和最大值

> 原文：[https://www.geeksforgeeks.org/min-and-max-in-a-list-in-java/](https://www.geeksforgeeks.org/min-and-max-in-a-list-in-java/)

给定一个未排序的整数列表，请在其中找到最大值和最小值。

```
Input : list = [10, 4, 3, 2, 1, 20]
Output : max = 20, min = 1

Input : list = [10, 400, 3, 2, 1, -1]
Output : max = 400, min = -1

```

**排序**

这是效率最低的方法，但可以完成工作。 想法是按自然顺序对列表进行排序，然后第一个或最后一个元素分别是最小和最大元素。 下面的 Java 实现。

```

// This java program find minimum and maximum value 
// of an unsorted list of Integer by using Collection 
import java.util.ArrayList; 
import java.util.Collections; 
import java.util.List; 

public class GFG { 

    // function to find minimum value in an unsorted 
    // list in Java using Collection 
    public static Integer findMin(List<Integer> list) 
    { 

        // check list is empty or not 
        if (list == null || list.size() == 0) { 
            return Integer.MAX_VALUE; 
        } 

        // create a new list to avoid modification  
        // in the original list 
        List<Integer> sortedlist = new ArrayList<>(list); 

        // sort list in natural order 
        Collections.sort(sortedlist); 

        // first element in the sorted list 
        // would be minimum 
        return sortedlist.get(0); 
    } 

    // function return maximum value in an unsorted 
    // list in Java using Collection 
    public static Integer findMax(List<Integer> list) 
    { 

        // check list is empty or not 
        if (list == null || list.size() == 0) { 
            return Integer.MIN_VALUE; 
        } 

        // create a new list to avoid modification 
        // in the original list 
        List<Integer> sortedlist = new ArrayList<>(list); 

        // sort list in natural order 
        Collections.sort(sortedlist); 

        // last element in the sorted list would be maximum 
        return sortedlist.get(sortedlist.size() - 1); 
    } 

    public static void main(String[] args) 
    { 

        // create an ArrayList Object list 
        List<Integer> list = new ArrayList<>(); 

        // add element in ArrayList object list 
        list.add(44); 
        list.add(11); 
        list.add(22); 
        list.add(33); 

        // print min amd max value of ArrayList 
        System.out.println("Min: " + findMin(list)); 
        System.out.println("Max: " + findMax(list)); 
    } 
} 

```

**输出**：

```
Min: 11
Max: 44
```

`Collections.max()`

`Collections.min()`方法返回指定集合中的最小元素，而`Collections.max()`返回指定集合中的最大元素（根据其元素的自然顺序）。

```

// This java program find minimum and maximum value 
// of an unsorted list of Integer by using Collection 
import java.util.ArrayList; 
import java.util.Collections; 
import java.util.List; 

public class GFG { 

    // function to find minimum value in an unsorted 
    // list in Java using Collection 
    public static Integer findMin(List<Integer> list) 
    { 

        // check list is empty or not 
        if (list == null || list.size() == 0) { 
            return Integer.MAX_VALUE; 
        } 

        // return minimum value of the ArrayList 
        return Collections.min(list); 
    } 

    // function return maximum value in an unsorted 
    //  list in Java using Collection 
    public static Integer findMax(List<Integer> list) 
    { 

        // check list is empty or not 
        if (list == null || list.size() == 0) { 
            return Integer.MIN_VALUE; 
        } 

        // return maximum value of the ArrayList 
        return Collections.max(list); 
    } 

    public static void main(String[] args) 
    { 

        // create an ArrayList Object list 
        List<Integer> list = new ArrayList<>(); 

        // add element in ArrayList object list 
        list.add(44); 
        list.add(11); 
        list.add(22); 
        list.add(33); 

        // print min amd max value of ArrayList 
        System.out.println("Min: " + findMin(list)); 
        System.out.println("Max: " + findMax(list)); 
    } 
} 

```

**输出**：

```
Min: 11
Max: 44
```

**朴素**

这是在未排序列表中查找最小值和最大值的幼稚方法，其中我们对照列表中存在的所有值进行检查，并保持到目前为止找到的最小值和最大值。

```

// This java program find minimum and maximum value 
// of an unsorted list of Integer 
import java.util.ArrayList; 
import java.util.List; 

public class GFG { 

    // Naive function to find minimum value in an 
    // unsorted list in Java 
    public static Integer findMin(List<Integer> list) 
    { 
        // initialize min to some maximum value 
        Integer min = Integer.MAX_VALUE; 

        // loop through every element in the list and 
        // compare min found so far with current value 
        for (Integer i : list) { 

            // update min if found to be more than  
            // the current element 
            if (min > i) { 
                min = i; 
            } 
        } 

        return min; 
    } 

    // This function return maximum value in an 
    // unsorted list in Java 
    public static Integer findMax(List<Integer> list) 
    { 
        // initialize max variable to minimum value 
        Integer max = Integer.MIN_VALUE; 

        // loop for compare to current max value 
        // with all list element and find maximum value 
        for (Integer i : list) { 

            // update max if found to be less than  
            // the current element 
            if (max < i) { 
                max = i; 
            } 
        } 

        return max; 
    } 

    public static void main(String[] args) 
    { 
        // create an ArrayList Object list 
        List<Integer> list = new ArrayList<>(); 
        // add element in ArrayList object list 
        list.add(44); 
        list.add(11); 
        list.add(22); 
        list.add(33); 

        // print min amd max value of ArrayList 
        System.out.println("Min: " + findMin(list)); 
        System.out.println("Max: " + findMax(list)); 
    } 
} 

```

**输出**：

```
Min: 11
Max: 44
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。