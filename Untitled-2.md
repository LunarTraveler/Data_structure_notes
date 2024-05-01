//单调栈的用法（用于求出目标index左右最近的最小值和最大值都是可以求的）

```java
public static int[][] Monotonous_Stack(int[] height){
    int len = height.length;
    int[] stack = new int[len];
    int size = 0;
    int[] left = new int[len];
    int[] right = new int[len];
    for(int i = 0;i < len;i++){
        当栈顶元素大于等于当前的元素是，及发现了距离自己左边最近的大于自己的值
        while(size > 0 && height[i] <= stack[size - 1]){
            size--;
        } 
        left[i] = size == 0 ? -1 : stack[size - 1];
        stack[size++] = i;
    }
    size = 0;
    for(int i = len - 1;i >= 0;i--){
        当栈顶元素大于等于当前的元素是，及发现了距离自己右边最近的大于自己的值
        while(size > 0 && height[i] <= stack[size - 1){
            size--;
        }
        right[i] = size == 0 ? len : stzck[size - 1];
        stack[size++] = i;
    }
    这个找到了index的两边最近的比自己大值的下标，有下标可知道具体的值进而求解问题
    如最大矩阵的问题等
}

这个是发现距离自己最近的最小值
public static int[][] Monotonous_Stack(int[] height){
    int len = height.length;
    int[] stack = new int[len];
    int size = 0;
    int[] left = new int[len];
    int[] right = new int[len];
    for(int i = 0;i < len;i++){
        while(size > 0 && height[i] >= stack[size - 1]){
            size--;
        } 
        left[i] = size == 0 ? -1 : stack[size - 1];
        stack[size++] = i;
    }
    size = 0;
    for(int i = len - 1;i >= 0;i--){
        while(size > 0 && height[i >= stack[size - 1){
            size--;
        }
        right[i] = size == 0 ? len : stzck[size - 1];
        stack[size++] = i;
    }
    这个找到了index的两边最近的比自己小的值
}
```

堆（优先队列）

在Java中可以使用Priority queue类就行实现堆的用法了

它主要是用于维护在一个集合中的前K个最大或最小的用法

在数据储存中是一个动态数组来保留数据元素[1, 2, 3, 4, 5, 6, 7, 8, 9]

                                            1

                                    2               3

                             4          5       6        7

                        8       9

其实是以一个完全二叉树为数学模型的（分为大根堆    小根堆）就是看这个对维护的是最大的几个值还是维护几个比较小的值

```java
//这个是大根堆的描述
// 还需要写出出堆和入堆动态调整的过程
class Heap{

    int[] heap = new int[10];

    int size = 0;

    public void swap(int[] arr, int i, int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public void heapInsert(int[] arr, int i){
        如果新加入的比自己的父亲节点还大，那么就交换他们两个的值
        新加入的节点来到父亲节点的位置，继续往上看，在进行判断
        while(arr[i] > arr[(i - 1) / 2]){
            swap(arr, i, (i - 1) / 2);
            i = (i - 1) / 2;
        }
    }

    public void heapify(int[] arr, int i, int size){
        int left = i * 2 + 1;
        //求出来i位置的左孩子的下标
        while(left < size){
            //这里进入代表左孩子下标没有超出size的范围
            //右孩子的下标就是left + 1
            int best = left + 1 < size && arr[left + 1] > arr[left] ? left + 1 : left;
            //在拿这个比较大的与父亲节点进行比较即可
            best = arr[best] > arr[i] ? best : i;
            //代表来到了更节点，已经是最大的了
            if(best == i){
                break;
            }
            swap(arr, best, i);
            i = best;
            left = i * 2 + 1;
        }
    }


}
```

进而可以实现一个堆排序

```java
/**
 * 堆排序演示
 *
 * @author Lvan
 */
public class HeapSort {
    public static void main(String[] args) {
//        int[] arr = {5, 1, 7, 3, 1, 6, 9, 4};
        int[] arr = {16, 7, 3, 20, 17, 8};

        heapSort(arr);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }


    /**
     * 创建堆，
     * @param arr 待排序列
     */
    private static void heapSort(int[] arr) {
        //创建堆
        for (int i = (arr.length - 1) / 2; i >= 0; i--) {
            //从第一个非叶子结点从下至上，从右至左调整结构
            adjustHeap(arr, i, arr.length);
        }

        //调整堆结构+交换堆顶元素与末尾元素
        for (int i = arr.length - 1; i > 0; i--) {
            //将堆顶元素与末尾元素进行交换
            int temp = arr[i];
            arr[i] = arr[0];
            arr[0] = temp;

            //重新对堆进行调整
            adjustHeap(arr, 0, i);
        }
    }

    /**
     * 调整堆
     * @param arr 待排序列
     * @param parent 父节点
     * @param length 待排序列尾元素索引
     */
    private static void adjustHeap(int[] arr, int parent, int length) {
        //将temp作为父节点
        int temp = arr[parent];
        //左孩子
        int lChild = 2 * parent + 1;

        while (lChild < length) {
            //右孩子
            int rChild = lChild + 1;
            // 如果有右孩子结点，并且右孩子结点的值大于左孩子结点，则选取右孩子结点
            if (rChild < length && arr[lChild] < arr[rChild]) {
                lChild++;
            }

            // 如果父结点的值已经大于孩子结点的值，则直接结束
            if (temp >= arr[lChild]) {
                break;
            }

            // 把孩子结点的值赋给父结点
            arr[parent] = arr[lChild];

            //选取孩子结点的左孩子结点,继续向下筛选
            parent = lChild;
            lChild = 2 * lChild + 1;
        }
        arr[parent] = temp;
    }
}
```

```java

```
