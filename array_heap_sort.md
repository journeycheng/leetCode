## 数组堆排序
堆排序是一种树形选择排序方法。在排序的过程中将array[0,1,...,n-1]看成是一棵完全二叉树的顺序存储结构，利用完全二叉树中双亲节点和孩子节点之间的内在关系，在当前无序区域中选择最大（最小）的元素。

```       
          0
         /  \
        1    2
       / \  / \ 
      3   4 5  6
      ...   ...
```

父节点为i（0<=i<=(n-1-1)/2），左孩子为2\*i+1，右孩子为2\*i+2。也可以说，第i个节点的父节点为(i-1)/2。最后一个节点的父节点为(n-1-1)/2.


堆的定义，其中0<=i<=(n-2)/2:
- 小根堆：array[i] <= array[2\*i+1] && array[i] <= array[2\*i+2]
- 大根堆：array[i] >= array[2\*i+1] && array[i] >= array[2\*i+2]

建立大根堆：

- 最后一个节点n-1是第(n-1-1)/2节点的孩子，对以第(n-1-1)/2节点的子树进行调整，使其子树称为堆。对于大根堆，调整方法为**根节点的值小于左右子女中值较大者，则进行交换**。
- 之后，依次对各节点(n-2)/2-1 ~ 0为根的子树进行调整，看该节点值是否大于其左右子节点的值，若不是，将左右子节点中较大者与之交换，交换后，可能会破坏下一级堆，于是继续采用上述风发构建下一级的堆，直到以该节点为根的子树构成堆为止
- 反复利用上述调整堆的方法建堆，直到根节点

------

上述过程总结如下：
1. 将存放在array中的n个元素构成初始堆；
2. 将堆顶元素与堆底元素进行交换，则序列的最大值即已放到正确的位置；
3. 此时堆已被破坏，将堆顶元素向下调整使其保持大根堆的性质，再重复2-3步，直到堆中仅剩一个元素为止



空间复杂度：o(1)

时间复杂度：建堆o(n)，每次调整o(logn)，故最好、最坏、平均情况下o(nlogn)

稳定性：不稳定


建立大根堆
```java
private int[] buildMaxHeap(int[] array){
    for(int i = (array.length-2)/2; i >= 0; i --){
        adjustDownToUp(array, i, array.length);
    }
    return array;
}


// 将元素array[k]自下向上逐步调整树形结构

private void adjustDownToUp(int[] array, int k, int length){
    int temp = array[k];
    for(int i = 2*k+1; i < length-1; i = 2*i + 1){
        if(i<length && array[i]< array[i+1]){
            i++;
        }
        if(tmp>=array[i]){
            break;
        }else{
            array[k] = array[i];
            k = i;
        }
    }
    array[k] = tmp;
}
```

堆排序
```java
public int[] heapSort(int[] array){
    array = buildMaxHeap(array);
    for(int i=array.length-1; i>1; i--){ //初始建堆，array[0]为第一趟值最大的元素
        int temp = array[0];   //将堆顶元素和堆低元素交换，即得到当前最大元素正确的排序位置
        array[0] = array[i];
        array[i] = temp;
        adjustDownToUp(array, 0, i);  //整理，将剩余的元素整理成堆
    }
}
```
