[toc]

# SORT

## Insertion Sort

>  Insertion sort is shown in the figure below:

<img src='../../images/Algorithm/insert_sort.gif'/>

> The code is shown below:

```java
public static int[] insertSort(int[] nums) {
  for(int i = 1;i < nums.length;i++) {
    int temp = nums[i];
    for(int j = i;j >= 0;j--) {
      if(j > 0 && nums[j - 1] > temp) {
        nums[j] = nums[j - 1];
      }else {
        nums[j] = temp;
        break;
      }
    }
  }
  return nums;
}
```

## Bubble Sort

> bubble sort is shown in the figure below:

<img src='../../images/Algorithm/bubble_sort.gif'/>

> The code is shown below:

```java
public static int[] bubbleSort(int[] nums) {
  for(int i = nums.length - 1;i > 0;i--) {
    boolean flag = false;
    for(int j = 0;j < i;j++) {
      if(nums[j] > nums[j + 1]) {
        int temp = nums[j];
        nums[j] = nums[j + 1];
        nums[j + 1] = temp;
        flag = true;
      }
    }
    if(!flag) break;
  }
  return nums;
}
```

## Selection Sort

> Selection sort is shown in the figure below:

<img src='../../images/Algorithm/selection_sort.gif'/>

> The coding is shown below:

```java
public static int[] selectSort(int[] nums){
  for(int i = 0;i < nums.length - 1;i++) {
    int min = nums[i];
    int minIndex = i;
    for(int j = i;j < nums.length;j++) {
      if(nums[j] < min) {
        min = nums[j];
        minIndex = j;
      }
    }
    if(minIndex != i) {
      nums[minIndex] = nums[i];
      nums[i] = min;
    }
  }
  return nums;
}
```

## Shell Sort

> Shell sort is shown in the figure below:

<img src='../../images/Algorithm/shell_sort.gif'/>

希尔排序是一段一段进行排序，比如 数组`[4,6,7,5,3,2,9,8,1,0]`,总长度为10，那么把这个数组55分，第一个`4`与第6个`2`比较，因为`2 < 4`，所以交换`4`和`2`，第一遍交换完后变为：`2 6 7 1 0 4 9 8 5 3`；第二遍把这个数组分为`2 2 2 3`四个部分，依然每部分相同的位置的数字进行比较…… 最后排序成功。

> The code is shown below:

```java
public static int[] shellSort(int[] nums) {
  int j;
  for(int gap = nums.length / 2;gap > 0;gap /= 2) { // gap（分段）一半一半地少
    for(int i = gap;i < nums.length;i++) { // 从gap 一直循环到数组尾部
      int temp = nums[i]; // 记录第一个元素
      for(j = i;j >= gap && nums[j - gap] > temp;j -= gap) { // 一开始j == i 这里nums[j] 与 nums[j - gap]比较 如果nums[j - gap]比较小 那么就应该交换j - gap 和 j的数字，
        nums[j] = nums[j - gap];
      }
      nums[j] = temp; // 因为如果上面循环只要运行过一次 j -= gap 那么这里就是把最小的数赋值 达到了排序的功能
    }
  }
  return nums;
}
```

## Heap Sort

> Heap Sort is shown in the figure below：

<img src='../../images/Algorithm/heap_sort.gif'/>

> The code is shown below:

```java
/**构建大顶堆**/
public static void maxHeapDown(int[] nums,int start,int end) {
  int c = start;
  int l = c * 2 + 1;
  int tmp = nums[c];
  for(;l <= end;c = l,l = 2 * l + 1) {
    if(l < end && nums[l] < nums[l + 1]) l++;
    if(nums[c] < nums[l]) {
      nums[c] = nums[l];
      nums[l] = tmp;
    }
    else break;
  }
}
/**堆排序**/
public static int[] heapSort(int[] nums) {
  int len = nums.length; // 获取数组长度
  for (int i = len / 2 - 1; i >= 0; i--) //第一次先排序成一个大顶堆
    maxHeapDown(nums,i,len - 1);
  for (int i = len - 1;i > 0;i--) {
    int tmp = nums[0];
    nums[0] = nums[i];
    nums[i] = tmp;

    maxHeapDown(nums,0,i - 1);
  }
  return nums;
}
```

## Merge Sort

> Merge sort is shown in the figure below:

<img src='../../images/Algorithm/merge_sort.gif'/>

> The code is shown below:

```java
public static void mergeSort(int[] nums,int left,int right) {
  if(left  >= right) return;
  int mid = (left + right) / 2;
  mergeSort(nums,left,mid);
  mergeSort(nums,mid + 1,right);

  int[] temp = new int[right - left + 1];
  int l = left,r = mid + 1;
  int cur = 0;
  while(l <= mid && r <= right) {
    if(nums[l] > nums[r]) temp[cur++] = nums[r++];
    else temp[cur++] = nums[l++];
  }

  while(l <= mid) temp[cur++] = nums[l++];
  while(r <= right) temp[cur++] = nums[r++];

  for(int i = 0;i < temp.length;i++) {
    nums[left + i] = temp[i];
  }
}
```

## Quick Sort

> Quick sort is shown in the figure below:

<img src='../../images/Algorithm/quick_sort.gif'/>

> The code is shown below:

```java
public static void quickSort(int[] nums,int left,int right) {
  if(left >= right) return;
  int partitionIndex = partition(nums,left,right);
  quickSort(nums,left,partitionIndex - 1);
  quickSort(nums,partitionIndex + 1,right);
}

public static int partition(int[] nums,int left,int right) {
  int pivot = left; //设定基准
  int index = pivot + 1;
  for(int i = index;i <= right;i++) {
    if(nums[i] < nums[pivot]) {
      int tmp = nums[i];
      nums[i] = nums[index];
      nums[index++] = tmp;
    }
  }
  int tmp = nums[index - 1];
  nums[index - 1] = nums[pivot];
  nums[pivot] = tmp;
  return index - 1;
}
```



## Bucket Sort