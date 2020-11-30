# 前言

**排序算法是《数据结构与算法》中最基本的算法之一。**

## 原地算法（In-place）

> 不依赖额外的资源或者依赖少数的额外资源，仅依靠输出来覆盖输入，空间复杂度为 𝑂(1) 。

![](https://upload-images.jianshu.io/upload_images/10390288-f5548d9568dd9903.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/10390288-1b556e7f761a99af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

时间复杂度：

1. 平方阶 (O(n2)) 排序 各类简单排序：直接插入、直接选择和冒泡排序。

2. 线性对数阶 (O(nlog2n)) 排序 快速排序、堆排序和归并排序；

3. O(n1+§)) 排序，§ 是介于 0 和 1 之间的常数。 希尔排序

4. 线性阶 (O(n)) 排序 基数排序，此外还有桶、箱排序。

稳定性：

1. 稳定的排序算法：冒泡排序、插入排序、归并排序和基数排序。

2. 不是稳定的排序算法：选择排序、快速排序、希尔排序、堆排序。

# 排序算法

**本文所有输出的都是从小到大排序**

测试数据如下：

``` bash 
const data = [];
let len = 20;
while (len > 0) {
  data.push(Math.floor(Math.random() * 100));
  len--;
}
```

## 1. 冒泡排序

### 1.1 算法步骤
- 1. 比较相邻的元素，如果第一个比第二个大，就交换它们两个；
- 2. 依次比较相邻的元素，直到数组元素比较完成，那么这时，最大的元素就应该在数组的最后面；
- 3. 不断重复 1 和 2 的操作

### 1.2 动画演示

![](https://upload-images.jianshu.io/upload_images/10390288-606eef440c2cd6d9.gif?imageMogr2/auto-orient/strip)

### 1.3 代码实现

``` bash 
const bubbleSort = (list) => {
  const len = list.length;
  let k = len - 1;
  let last_index = 0; // 最后一次交换的位置
  for (let i = 0; i < len - 1; i++) {
    let is_change = false;// 是否有交换
    for (let j = 0; j < k; j++) {
      if (list[j] > list[j + 1]) {
        is_change = true;
        // 交换值
        [list[j], list[j + 1]] = [list[j + 1], list[j]];
        last_index = j;
      }
    }
    k = last_index;
    // 已经排好序了
    if (!is_change) break;
  }
  return list;
}
```

优化点：

- 1. 如果一轮外循环后，没有发生比较，说明已经排好序了，可以直接中止退出
- 2. 记录下最后一次比较值的位置，下一次比较到这里就 OK 了

## 2 选择排序

### 2.1 算法步骤

- 1. 首先在未排序序列中找到最小元素，存放到排序序列的起始位置
- 2. 再从剩余未排序元素中继续寻找最小元素，然后放到已排序序列的末尾
- 3. 重复第二步，直到所有元素均排序完毕

### 2.2 动画演示

![](https://upload-images.jianshu.io/upload_images/10390288-7c6b7a7af46ea9f1.gif?imageMogr2/auto-orient/strip)

### 2.3 代码实现

``` bash 
const selectSort = (list) => {
  let len = list.length;
  let min = 0;
  for (let i = 0; i < len - 1; i++) {
    min = i;
    for (let j = i + 1; j < len; j++) {
      if (list[min] > list[j]) {
        min = j;
      }
    }
    // 每一轮比较完，交换 i 和 min 位置
    [list[i], list[min]] = [list[min], list[i]];
  }
  return list;
}
```

## 3. 插入排序

### 3.1 算法步骤
- 1. 将第一个元素看成一个有序序列，其他元素看成一个无序序列
- 2. 取出无序序列耳朵第一个元素，与有序序列从尾向前依次比较，若 
- 3. 重复步骤2，直至无序序列全部比较完

### 3.2 动画演示

![](https://upload-images.jianshu.io/upload_images/10390288-1d786d1fa686da2d.gif?imageMogr2/auto-orient/strip)

### 3.3 代码实现

``` bash 
const insertSort = (list) => {
  let len = list.length
  for (let i = 1; i < len; i++) {
    const temp = list[i];
    let j = i - 1;
    while (j >= 0 && list[j] > temp) {
      list[j + 1] = list[j];
      j--;
    }
    list[j + 1] = temp;
  }
  return list;
}
```

# 参考

图片均来源于该文章

[十大经典排序算法动画与解析，看我就够了！（配代码完全版）](https://mp.weixin.qq.com/s/vn3KiV-ez79FmbZ36SX9lg)

# 源码

[源码](https://github.com/zhongzihao1996/my-blog/tree/master/35_JS%20%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)

---

END
