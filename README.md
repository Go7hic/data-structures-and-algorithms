# data-structures-and-algorithms
javascript data structures and algorithms

## 数据结构


## 排序算法
1.冒泡排序：比较任何两个相邻的项，如果第一个比第二个大，则交换它们

```js
function swap(arr, index1, index2) {
  var aux = arr[index1]
  arr[index1] = arr[index2]
  arr[index2] = aux
}
function bubbleSort(arr) {
  var len = arr.length;
  for (var i = 0; i < len; i++) {
    for (var j = 0; j < len - i - 1 ; j++) {
      if (arr[j] > arr[j+1]) {
        swap(arr , j ,j+1)
      }
    }
  }
  return arr
}
// 测试
var a = bubbleSort([5,4,3,2,7,1]); // a = [1,2,3,4,5,7]
```

2.选择排序：找到数据结构中最小值并将其放在第一位，接着找到第二小的值并将其放在第二位，以此类推

```js
function swap(arr, index1, index2) {
  var aux = arr[index1]
  arr[index1] = arr[index2]
  arr[index2] = aux
}
function selectorSort(arr) {
  var len = arr.length,indexMin;
  for (var i = 0; i < len -1 ; i++) {
    indexMin = i;
    for (var j = i ; j < len; j++) {
      if (arr[indexMin] > arr[j]) {
        indexMin = j
      }
    }
    if (i !== indexMin) {
      swap(arr ,i, indexMin)
    }
  }
  return arr
}
// 测试
var a = selectorSort([5,4,3,2,7,1]); // a = [1,2,3,4,5,7]
```

3.插入排序：假设第一个数已经是排序好了的，然后拿他和第二个进行比较，确定第二个是插到第一个之前还是留在原位，排好后再和第三个比较，以此类推

```js
function insertSort(arr) {
  var len = arr.length,j ,temp;
  for (var i = 1; i < len; i++) {
    j = i;
    temp = arr[i];
    while (j > 0 && arr[j-1] > temp) {
      arr[j] = arr[j-1]
      j--;
    }
    arr[j] = temp
  }
  return arr
}
```

4.归并排序：将原始数组切分成较小的数组，直到每个小数组只有一个位置，接着将小数组归并成较大数组，直到最后只有一个排序完成的大数组。归并排序是一种分治思想， firefox 浏览器对于 js 数组原生的 sort 方法实现就是用的归并算法

```js
function merge(left, right) {
  var result = [], il = 0, ir = 0;
  while(il < left.length && ir < right.length) {
    if(left[il] < right[ir]) {
      result.push(left[il++]);
    } else {
      result.push(right[ir++]);
    }
  }
  while (il < left.length) {
    result.push(left[il++])
  }
  while(ir < right.length) {
    result.push(right[ir++])
  }
  return result;
}
function mergeSort(arr) {
  var len = arr.length;
  if (len === 1) {
    return arr
  }
  var mid = Math.floor(len/2),
    left = arr.slice(0, mid),
    right = arr.slice(mid, len);
  return merge(mergeSort(left), mergeSort(right));
}
// 测试
var a = selectorSort([5,4,3,2,7,1]); // a = [1,2,3,4,5,7]
```

5.快速排序：和前面的归并算法一样，采用分治思想，谷歌 chrome 对js 原生 sort 的实现就是类似的快排算法。

```js
function quickSort(arr) {
  quick(arr, 0, arr.length - 1)
  return arr;
}
function quick(arr, left, right) {
  var index;
  if (arr.length > 1) {
    index = partition(arr, left, right);
    if (left < index - 1) {
      quick(arr, left ,index - 1)
    }
    if (index < right) {
      quick(arr, index, right)
    }
  }
}
function swap(arr, index1, index2) {
  var aux = arr[index1]
  arr[index1] = arr[index2]
  arr[index2] = aux
}
function partition(arr, left, right) {
  var pivot = arr[Math.floor((right + left) / 2)], i = left, j = right;
  while(i <= j) {
    while(arr[i] < pivot) {
      i++
    }
    while(arr[j] > pivot) {
      j--
    }
    if (i <= j) {
      swap(arr, i ,j)
      i++;
      j--;
    }
  }
  return i
}

// 测试
var a = selectorSort([5,4,3,2,7,1]); // a = [1,2,3,4,5,7]
```

## 搜索算法



## 了解大 O 表示法
大 O 表示法通常来描述算法的性能和复杂程度。一般讨论的是 CPU 占用时间

- O(1) 常数的
- O(log(n)) 对数的
- O(log(n)c) 对数多项式的
- O(n) 线性的
- O(n^2) 二次的
- O(n^c) 多项式的
- O(c^n) 指数的

O(1)
```
function add(n) {
  return ++n
}
```

O(n)
```
function search(arr, item) {
  for (var i = 0; i < arr.length; i++) {
    if (item === arr[i]) {
      return i
    }
  }
  return -1
}
```
 如果数组arr 的长度为 n，那么这个函数的时间复杂度就是 O(n)
 
 O(n^2)
```
 function swap(arr, index1, index2) {
   var aux = arr[index1]
   arr[index1] = arr[index2]
   arr[index2] = aux
 }
 function bubbleSort(arr) {
   var length = arr.length;
   for (var i = 0; i < length; i++) {
     for (var j = 0; j < length -1; j++) {
       if (arr[j] > arr[j+1]) {
         swap(arr, j, j+1)
       }
     }
   }
 }
```
 上面这个类似冒泡排序的函数，有两层循环，如果数组的长度为 n；那么时间复杂度应该为 O(n^2)
 
 ## 常见的复杂度速查表

![Imgur](http://i.imgur.com/PzFruXj.jpg)
![Imgur](http://i.imgur.com/IHTiz4v.jpg)

参考：http://bigocheatsheet.com/
