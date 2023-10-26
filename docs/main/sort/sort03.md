# 插入排序



老实说，第一次听到的时候，有点懵，怎么插？往哪里插？怎么排？按什么规则排？

先看解释：
> 插入排序，一般也被称为直接插入排序;

> 插入排序是一种<b style="color:#FF3399">最简单</b>的排序方法

> 基础思想：**通过逐个将元素插入到已排序部分的正确位置来排序一个数组**

看完还是有点懵？往下看

### 一张图，带你看清细节
![归并排序](../../image/sort03-01.gif)

```
假如 3 是一个有序序列；从第二位 44 开始，从后往前依次对比，如果比3大，则放在3的后面位置
再从后一位 38 开始；从后往前依次对比，比44小，则继续向前对比，比3大，则插入在3的后面位置；
再从后一位 5 开始；从后往前依次对比，比44小，则继续向前对比，比38小，则继续向前对比，比3大，则插入在3的后面位置；
...
依次类推，直到最后一位插入到正确的位置；插入排序完成；

```

看到这里是不是有点清晰了？ 

还不清晰？ 那就刷新页面，从头看，我当你没来过


### 一起动手，丰衣足食
依次？ 递增？ 再依次？ 那就双循环嘛，开撸 


```js
// 闷头就是一波骚操作，撸出来的代码是这样的

// 结果... 还对了，真佩服我这缜密的心思

/** 插入排序 */
function sortInsert(arr) {
  let tempArray = JSON.parse(JSON.stringify(arr));
  let i = 1;
  // 从第一个开始
  for(i = 1; i < tempArray.length; i++) {
    // 从后向前，一个一个对比；
    for(j = i; j > 0; j--) {
      if(tempArray[j] < tempArray[j-1]) {
        console.log(i + "-" + j + ":" + tempArray[j] + "-" + tempArray[j-1] + "换");
        // 后面小于前面， 换位置
        let temp = tempArray[j];
        tempArray[j] = tempArray[j-1];
        tempArray[j-1] = temp;
      } else {
        // 跳过里面循环
        console.log(i + "-" + j + ":" + tempArray[j] + "-" + tempArray[j-1]);
        break;
      }
    }
  }

  return tempArray;
}

let arr = [0, 4, 1, 3, 2, 5]
let result = sortInsert(arr);
console.log(result);

//log
// 1-1:4-0
// 2-2:1-4换
// 2-1:1-0
// 3-3:3-4换
// 3-2:3-1
// 4-4:2-4换
// 4-3:2-3换
// 4-2:2-1
// 5-5:5-4
// [ 0, 1, 2, 3, 4, 5 ]
```
### 成品区
撸完，当让是要瞎得瑟一圈，看看广大网民的技术是不是真的没我强，

看了两篇，虚头巴脑的都不是干货；果断 chatGPT 一下，

还真别说，真有比咱强的，向高手学习，来一波优化，你再看，你细细的品，果然味道不一样了

```js

// 你品，你细细的品

/** 插入排序 */
function sortInsert(arr) {
  let tempArray = JSON.parse(JSON.stringify(arr));

  for (let i = 1; i < tempArray.length; i++) {
    let current = tempArray[i];
    let j = i - 1;

    while (j >= 0 && current < tempArray[j]) {
      // 后面小于前面，交换位置
      tempArray[j + 1] = tempArray[j];
      j--;
    }

    // 插入当前元素到正确位置
    tempArray[j + 1] = current;
  }

  return tempArray;
}

let arr = [0, 4, 1, 3, 2, 5];
let result = sortInsert(arr);
console.log(result);

```
