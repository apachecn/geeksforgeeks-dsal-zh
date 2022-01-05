# 使用 JavaScript 的插入排序可视化

> 原文:[https://www . geesforgeks . org/insert-sort-visualization-use-JavaScript/](https://www.geeksforgeeks.org/insertion-sort-visualization-using-javascript/)

插入排序是一种简单的排序算法，其中来自未排序部分的值被拾取并放置在排序部分的正确位置。

为了了解更多。请参考[插入排序](https://www.geeksforgeeks.org/insertion-sort/)。

像**插入排序**这样的算法可以通过可视化而不是长代码来轻松理解。在本文中，**插入排序可视化工具**是使用 **HTML，CSS & JavaScript 实现的。**

**先决条件:**

*   [插入输出](https://www.geeksforgeeks.org/insertion-sort/)。
*   基础 [HTML](https://www.geeksforgeeks.org/html-tutorials/) 、[CSS](https://www.geeksforgeeks.org/css-tutorials/)&[JavaScript](https://www.geeksforgeeks.org/javascript-tutorial/)。
*   JavaScript 中的承诺。
*   JavaScript 中的异步/等待函数。

**进场:**

*   按钮**生成新数组**使用**数学.随机()**函数和一个对应于高度值的条生成随机值数组。
*   不同的颜色用于指示哪些元素是未排序的(天蓝色)、已比较的(深蓝色)和已排序的(浅绿色)。
*   按钮**插入排序**使用选择排序算法对元素进行排序。
*   最后，对元素进行排序。

**示例:**

*   点击**生成新数组**按钮，生成新的随机数组。
*   点击**选择排序**按钮进行可视化。

## 超文本标记语言

```
<!DOCTYPE html>
<html lang="en">

  <!-- head -->
  <head>

    <!-- linking style.css -->
    <link href="style.css" rel="stylesheet" />
  </head>

  <!-- body -->
  <body>
    <section class="head">Insertion Sort</section>
    <section class="data-container"></section>
    <section id="ele"></section>
    <div style="margin: auto; width: fit-content;">

     <!-- "Generate New Array" button -->
   <button  class="btn1" 
           onclick="generate()" id="Button1" >
     Generate New Array</button>   

   <!-- "Insertion Sort" button -->
   <button class="btn2" 
           onclick="InsertionSort(),disable()" 
           id="Button2" >
     Insertion Sort</button>
    </div>     
  </body>

  <!-- linking index.js -->
  <script src="index.js"></script>
</html>
```

## 半铸钢ˌ钢性铸铁(Cast Semi-Steel)

```
.mySlides {
  display: none;
}

body {
  background-color: rgb(255, 235, 211);
  font-family: Verdana, sans-serif;
}

.head {
  margin-top: 20px;
  margin-right: 20vw;
  margin-left: 20vw;
  text-align: center;
  font-size: 30px;
  background-color: #6f459e;
  color: white;
  border-radius:19px;
  font-weight: bolder;
}

.data-container {
  width: 600px;
  height: 364px;
  position: relative;
  margin: 0 auto;
}

.bar {
  width: 28px;
  position: absolute;
  left: 0;
  bottom: 0;
  background-color: rgb(0, 183, 255);
  transition: 0.2s all ease;
}

.bar__id {
  position: absolute;
  top: -24px;
  width: 100%;
  text-align: center;
}
.btn1
{
padding: 12px;
font-weight: bolder; 
background-color: #6f459e; 
border-radius: 10px; 
color: white; 
font-size: 16px; 
border: white; 
margin-top: 1vw;
margin-right: 1vw;
}
.btn2
{
padding: 12px; 
font-weight: bolder; 
background-color: #6f459e; 
border-radius: 10px; 
color: white; 
font-size: 16px; 
border: white
}
#ele{
  text-align: center;
  height: 35px;
}
```

## java 描述语言

```
const container = 
document.querySelector(".data-container");

// Function to generate bars
function generatebars(num = 20) {

   //For loop to generate 20 bars
  for (let i = 0; i < num; i += 1) {

    // To generate random values from 1 to 100
    const value = Math.floor(Math.random() * 100) + 1;

     // To create element "div"
    const bar = document.createElement("div");

    // To add class "bar" to "div"
    bar.classList.add("bar");

     // Provide height to the bar
    bar.style.height = `${value * 3}px`;
    // Translate the bar towards positive X axis 
    bar.style.transform = `translateX(${i * 30}px)`;

    // To create element "label"
    const barLabel = document.createElement("label");

    // To add class "bar_id" to "label"
    barLabel.classList.add("bar__id");

    // Assign value to "label"
    barLabel.innerHTML = value;

    // Append "Label" to "div"
    bar.appendChild(barLabel);

    // Append "div" to "data-container div"
    container.appendChild(bar);
  }
}

// Asynchronous function to perform "Insertion Sort"
  async function InsertionSort(delay = 600) {
  let bars = document.querySelectorAll(".bar");

  // Provide lightgreen colour to 0th bar
  bars[0].style.backgroundColor = " rgb(49, 226, 13)";
  for (var i = 1; i < bars.length; i += 1) {

    // Assign i-1 to j
    var j = i - 1;

    // To store the integer value of ith bar to key 
    var key = 
    parseInt(bars[i].childNodes[0].innerHTML);

    // To store the ith bar height to height
    var height = bars[i].style.height;

    // For selecting section having id "ele"
    var barval=document.getElementById("ele")

    // For dynamically Updating the selected element
      barval.innerHTML=
      `<h3>Element Selected is :${key}</h3>`;

    //Provide darkblue color to the ith bar 
    bars[i].style.backgroundColor = "darkblue";

    // To pause the execution of code for 600 milliseconds
    await new Promise((resolve) =>
    setTimeout(() => {
      resolve();
    }, 600)
  );

    // For placing selected element at its correct position 
    while (j >= 0 && parseInt(bars[j].childNodes[0].innerHTML) > key) {

      // Provide darkblue color to the jth bar
      bars[j].style.backgroundColor = "darkblue";

      // For placing jth element over (j+1)th element
      bars[j + 1].style.height = bars[j].style.height;
      bars[j + 1].childNodes[0].innerText = 
      bars[j].childNodes[0].innerText;

      // Assign j-1 to j
      j = j - 1;

      // To pause the execution of code for 600 milliseconds
      await new Promise((resolve) =>
        setTimeout(() => {
          resolve();
        }, 600)
      );

      // Provide lightgreen color to the sorted part
      for(var k=i;k>=0;k--){
        bars[k].style.backgroundColor = " rgb(49, 226, 13)";
      }
    }

    // Placing the selected element to its correct position
    bars[j + 1].style.height = height;
    bars[j + 1].childNodes[0].innerHTML = key;

    // To pause the execution of code for 600 milliseconds
    await new Promise((resolve) =>
      setTimeout(() => {
        resolve();
      }, 600)
    );

    // Provide light green color to the ith bar
    bars[i].style.backgroundColor = " rgb(49, 226, 13)";
  }

  barval.innerHTML="<h3>Sorted!!!</h3>";

  // To enable the button 
  // "Generate New Array" after final(sorted)
  document.getElementById("Button1")
  .disabled = false;
  document.getElementById("Button1")
  .style.backgroundColor = "#6f459e";

  // To enable the button 
  // "Insertion Sort" after final(sorted)
  document.getElementById("Button2")
  .disabled = false;
  document.getElementById("Button2")
  .style.backgroundColor = "#6f459e";
}

// Call "generatebars()" function 
generatebars();

// Function to generate new random array 
function generate()
{
  window.location.reload();
}

// Function to disable the button
function disable()
{
  // To disable the button "Generate New Array"
  document.getElementById("Button1")
  .disabled = true;
  document.getElementById("Button1")
  .style.backgroundColor = "#d8b6ff";

  // To disable the button "Insertion Sort"
  document.getElementById("Button2")
  .disabled = true;
  document.getElementById("Button2")
  .style.backgroundColor = "#d8b6ff";  
}
```

**输出:**

<video class="wp-video-shortcode" id="video-556088-1" width="640" height="360" preload="metadata" controls=""><source type="video/mp4" src="https://media.geeksforgeeks.org/wp-content/uploads/20210203144011/Insertion-Sort-Visualizer--video.mp4?_=1">[https://media.geeksforgeeks.org/wp-content/uploads/20210203144011/Insertion-Sort-Visualizer--video.mp4](https://media.geeksforgeeks.org/wp-content/uploads/20210203144011/Insertion-Sort-Visualizer--video.mp4)</video>