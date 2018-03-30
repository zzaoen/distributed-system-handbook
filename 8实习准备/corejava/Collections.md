Collections是一个包装类，其中包含有各种有关集合操作的静态多态方，比如可以作用在List和Set上，此类不能实例化。

## 排序

```
Integer[] array = new Integer[]{3, 10, 4, 0, 2};
List<Integer> integers = Arrays.asList(array);
Collections.sort(integers);
out.println(integers); //[0, 2, 3, 4, 10]
```
在这里借用了Arrays的asList方法，该方法可以将数组转成一个List。这里也只能对封装类型Integer数组调用asList方法，如果是int型的数组调用asList会出现其他问题。可以查考[Arrays用法总结](https://blog.csdn.net/zhzh402/article/details/79670509)。

## 混排

```
out.println(integers); //[0, 2, 3, 4, 10]
Collections.shuffle(integers);
out.println(integers); //[0, 3, 10, 2, 4]
```

## 反转

```
out.println(integers); //[0, 3, 10, 2, 4]
Collections.reverse(integers);
out.println(integers); //[3, 0, 4, 2, 10]
```

## 填充（覆盖）元素

```
array = new Integer[]{3, 10, 4, 0, 2};
integers = Arrays.asList(array);
Collections.fill(integers, -1);
out.println(integers); //[-1, -1, -1, -1, -1]
out.println(Arrays.toString(array)); //[-1, -1, -1, -1, -1]
```
通过输出可以发现原数组的值也跟着发生了变化，因为是封装类型，所以`Integer[]`中和`List<Integer>`中的元素指向的是用一个Integer对象的地址，所以两个会一起变化。

## 替换元素
```
array = new Integer[]{3, 10, 4, 4, 4};
integers = Arrays.asList(array);
Collections.replaceAll(integers, 4, -4);
out.println(integers); //[3, 10, -4, -4, -4]
```

## 拷贝List

```
out.println(integers); //[3, 10, -4, -4, -4]
List<Integer> integersCopy = new ArrayList<>();  integersCopy.add(1);
integersCopy.add(1);
integersCopy.add(1);
integersCopy.add(1);
integersCopy.add(1);
integersCopy.add(1); 
//如果不对List调用add方法，integerCopy还是空的，下面的copy方法会出错
Collections.copy(integersCopy, integers);
out.println(integersCopy); //[3, 10, -4, -4, -4, 1]
```

## 返回List中的最大值，最小值

```
array = new Integer[]{3, 10, 4, 0, 2};
integers = Arrays.asList(array);
out.println(integers);
out.println(Collections.min(integers)); //0
out.println(Collections.max(integers)); //10
```

## 源列表中第一次和最后一次出现指定列表的起始位置

```
Integer[] array1 = new Integer[]{3, 10, 4, 0, 2, 4, 0};
List integers1 = Arrays.asList(array1);
Integer[] array2 = new Integer[]{4, 0};
List integers2 = Arrays.asList(array2);
out.println(Collections.lastIndexOfSubList(integers1, integers2)); //5
out.println(Collections.indexOfSubList(integers1, integers2)); //2
```

## 循环移动

```
out.println(integers); [3, 10, 4, 0, 2]
Collections.rotate(integers, 1); //[2, 3, 10, 4, 0] 依次右移一位
out.println(integers);
Collections.rotate(integers, -2); //[10, 4, 0, 2, 3] 依次左移两位
out.println(integers);
```

## 二分查找，返回所在的下标。没有找到返回负的下标值。

```
array = new Integer[]{0, 2, 4, 10, 20};
integers = Arrays.asList(array);
out.println(Collections.binarySearch(integers, 4)); //2
out.println(Collections.binarySearch(integers, 9)); //-4
```

## 指定元素在集合中出现的次数

```
array = new Integer[]{0, 2, 4, 4, 20};
integers = Arrays.asList(array);
out.println(Collections.frequency(integers, 4)); //2
```

列表项