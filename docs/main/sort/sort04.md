# 希尔排序

 一句话：**希尔排序是一种插入排序的高效改进版本** , 是不是懂得插入排序的小伙伴，瞬间懂了一半了；  
什么？不懂插入排序？就地给你开一个[传送门](/main/sort/sort03.md)，*走你，不送*     
接下来我们唠唠：怎么就高效了？

**一：先看他的理论：**   
通过将数组拆分为多个较小的子数组，对这些子数组执行插入排序，逐渐减小子数组的间隔，直到整个数组变得有序

**二：在看分解动作：**
1. 将数组拆分为多个较小的子数组
2. 对这些子数组执行插入排序
3. 逐渐减小子数组的间隔
4. 重复以上动作

三： 明白了？提取关键词，记入脑子！！！
拆分、、、、排序、、、、缩小间隔、、、、再来一次、、拆分、、排序、、...

四：最后看整体思想：   
先将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序，待整个序列中的记录“基本有序”时，再对全体记录进行依次直接插入排序


### 一张图，带你看清细节
![归并排序](../../image/sort04-01.png)


### 一起动手，丰衣足食
拆分、、、、排序、、、、缩小间隔、、、、再来一次、、


```js
// 撸
```