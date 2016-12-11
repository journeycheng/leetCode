## 数组二分查找

```java
public class BinarySearch{
    public static int binarysearch(int[] array, int key){
        low = 0;
        high = array.length - 1;
        
        while(low <= high){
            mid = (low + high) / 2;
            if(array[mid] == key){
                return mid;
            }else if(array[mid] > key){
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
        return -1;
    }
}
```

递归的方法
```java
 public class BinarySearch{   
    public static int binarySearch(int[] array, int key, int begin_index, int end_index){
        int mid_index = (begin_index + end_index) / 2;
        if(key < array[begin_index] || key > array[end_index] || begin_index > end_index){
            return -1;
        }
        if(array[mid_index] < key){
            binarySearch(array, key, mid_index + 1, end_index);
        }else if(array[mid_index] > key){
            binarySearch(array, key, begin_index, mid_index + 1);
        }else{
            return mid_index;
        }
    }
}
```
