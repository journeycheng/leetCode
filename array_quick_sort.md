```java
public class QuickSort{
  
    public static void quicksort(int[] array){
        if (array != null){
            quickSort(array, 0, array.length-1);
        }
    }
    
    
    private static void quickSort(int[] array, int begin, int end){
        if(begin >= end || array == null){
            return;
        }
        int p = partition(array, begin, end);
        quickSort(array, begin, p-1);
        quickSort(array, p+1, end);
        
    }
    
    private static int partition(int[] array, begin, end){
        int key = array[begin];
        int low = begin;
        int high = end;
        
        while(low < high){
            while(array[high] >= key && high > low){
                high --;
            }
            swap(array, low, high);
            
            while(array[low] <= key && low < high){
                low ++;
            }
            swap(array,low, hight);
        }
        return low; 
    }
    
    private static void swap(int[] array, int index1, int index2){
        int tmp = array[index1];
        array[index1] = array[index2];
        array[index2] = tmp;
    }
}
