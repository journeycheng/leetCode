## 归并排序

归并排序是将多个有序列表合并成一个新的有序列表。即将待排序序列分成若干个字序列，每个字序列是有序的，再把有序字序列合并为整体有序序列。

2-路归并

归并排序算法稳定，数组需要O(n)的额外空间，时间复杂度为O(nlogn)，算法不是自适应的，不需要对数据的随机读取。

工作原理：
- 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列
- 设定两个指针，最初位置分别为两个已经排序序列的起始位置
```java
public class MergeSort{
    public static void mergeSort(int[] array){
        mergesort(array, 0, array.length-1);
    }
    
    private static void mergesort(int[] array, int begin, int end){
        if (begin >= end){
            return;
        }
        int mid = (begin + end) / 2;
        mergesort(array, begin, mid);
        mergesort(array, mid+1, end);
        merge(array, begin, mid, end);
    }
    
    private static void merge(int[] array, int begin, int mid, int end){
        int[] tmp = new int[array.length];
        int tmp_index = begin;
        int left_start = begin;
        int right_start = mid + 1;
        
        while(left_start <= mid && right_start <= end){
            if(array[left_start] <= array[right_start]){
                tmp[tmp_index ++] = array[left_start ++];
            }else{
                tmp[tmp_index ++] = array[right_start ++];
            }
            
            while(left_start < mid+1){
                tmp[tmp_index ++] = array[left_start ++];
            }
            while(right_start < end){
                tmp[tmp_index ++] = array[right_start ++];
            }
            
        }
        while(start <= end){
            array[start] = tmp[start++];
        }
    }
}

```
