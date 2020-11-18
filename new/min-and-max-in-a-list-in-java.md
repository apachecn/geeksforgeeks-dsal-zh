# Java列表中的最小值和最大值

给定一个未排序的整数列表，请在其中找到最大值和最小值。

```
Input : list = [10, 4, 3, 2, 1, 20]
Output : max = 20, min = 1

Input : list = [10, 400, 3, 2, 1, -1]
Output : max = 400, min = -1

```

**排序**

这是效率最低的方法，但可以完成工作。 想法是按自然顺序对列表进行排序，然后第一个或最后一个元素分别是最小和最大元素。 下面的Java实现。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// This java program find minimum and maximum value``// of an unsorted list of Integer by using Collection``import` `java.util.ArrayList;``import` `java.util.Collections;``import` `java.util.List;``public` `class` `GFG {` `// function to find minimum value in an unsorted` `// list in Java using Collection` `public` `static` `Integer findMin(List<Integer> list)` `{` `// check list is empty or not` `if` `(list ==` `null` `&#124;&#124; list.size() ==` `0` `) {` `return` `Integer.MAX_VALUE;` `}` `// create a new list to avoid modification ` `// in the original list` `List<Integer> sortedlist =` `new` `ArrayList<>(list);` `// sort list in natural order` `Collections.sort(sortedlist);`[ `// first element in the sorted list` `// would be minimum` `return` `sortedlist.get(` `0` `);` `}` `// function return maximum value in an unsorted` `// list in Java using Collection` ] `public` `static` `Integer findMax(List<Integer> list)` `{` `// check list is empty or not` `if` `(list ==` `null` `&#124;&#124; list.size() ==` `0` `) {` `return` `Integer.MIN_VALUE;` `}` `// create a new list to avoid modification` `// in the original list` `List<Integer> sortedlist =` `new` `ArrayList<>(list);` `// sort list in natural order` `Collections.sort(sortedlist);` `// last element in the sorted list would be maximum` [HT G258] `return` `sortedlist.get(sortedlist.size() -` `1` `);` `}` `public` `static` `void` `main(String[] args)` `{`​​ `// create an ArrayList Object list` `List<Integer> list =` `new` `ArrayList<>();` `// add element in ArrayList object list` `list.add(` `44` `);` `list.add(` `11` `);` `list.add(` `22` `);` `list.add(` `33` `);` `// print min amd max value of ArrayList` `System.out.println(` `"Min: "` `+ findMin(list));` `System.out.println(` `"Max: "` `+ findMax(list));` `}``}` |

*chevron_right**filter_none*

**输出：**

```
Min: 11
Max: 44
```

 **Collections.max（）

Collections.min（）方法根据指定元素的自然顺序返回指定集合中的最小元素，而Collections.max（）返回指定集合中的最大元素。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// This java program find minimum and maximum value``// of an unsorted list of Integer by using Collection``import` `java.util.ArrayList;``import` `java.util.Collections;``import` `java.util.List;``public` `class` `GFG {` `// function to find minimum value in an unsorted` `// list in Java using Collection` `public` `static` `Integer findMin(List<Integer> list)` `{` `// check list is empty or not` `if` `(list ==` `null` `&#124;&#124; list.size() ==` `0` `) {` `return` `Integer.MAX_VALUE;` `}` `// return minimum value of the ArrayList` `return` `Collections.min(list);` `}` `// function return maximum value in an unsorted` `//  list in Java using Collection` `public` `static` `Integer findMax(List<Integer> list)` `{` `// check list is empty or not` `if` `(list ==` `null` `&#124;&#124; list.size() ==` `0` `) {` `return` `Integer.MIN_VALUE;` `}` [ `// return maximum value of the ArrayList` `return` `Collections.max(list);` `}`[ `public` `static` `void` `main(String[] args)` `// create an ArrayList Object list` `List<Integer> list =` `new` `ArrayList<>();` `// add element in ArrayList object list` `list.add(` `44` `);` `list.add(` `11` `);` `list.add(` `22` `);`[H TG221]  `list.add(` `33` `);` `// print min amd max value of ArrayList` `System.out.println(` `"Min: "` `+ findMin(list));` `System.out.println(` `"Max: "` `+ findMax(list));` `}``}` |

*chevron_right**filter_none*

**输出：**

```
Min: 11
Max: 44
```

**天真**

这是在未排序列表中查找最小值和最大值的幼稚方法，其中我们对照列表中存在的所有值进行检查，并保持到目前为止找到的最小值和最大值。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码***