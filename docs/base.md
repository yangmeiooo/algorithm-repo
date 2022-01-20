## Kmp

kmp 算法

解决了一个什么样的问题？

其实就是高效的解决了，2个字符串部分匹配的时候。

当出现失配的时候，待匹配字符串需要移动到哪里。

原先暴力匹配， 主串移动一格，辅串回到0.

但是极端情况出现很多无效匹配。



其实就是利用了  部分匹配的信息。

当前j 失配， 需要利用[0,,,j-1] 的部分匹配信息，于是需要 PMT

移动位数 = 已匹配的字符数 - 对应的部分匹配值（x = j - cal[Jj-1]）

为了处理j-1 在数组的边界情况。 产生了next 数组。

统一右移1位，cal[0] = -1;



```java
package com.test.lambda;

public class StrTest {

    public static void test(int[] cal, String s){

       int i = 0;
       int k = -1;
       cal[0] = -1;

       while(i < cal.length - 1) {

           if (k == -1 || s.charAt(i) == s.charAt(k))  {
               i++;
               k++;
               cal[i] = k;
           } else {
               k = cal[k];
           }
       }

    }


//    public void test1(){
//
//        int i = 0, j = -1;
//        while(i < s.size()) {
//            if( j==-1 || s[i] == s[j]) {
//                i++;
//                j++;
//                next.push_back(j);
//            }
//            else {
//                j = next[j]; // 如果s[i]!=s[j]说明匹配失败, 回到上一级公共前后缀处
//            }
//        }
//
//    }

    public static int find(String p,String s, int[] cal) {

        int i = 0;
        int j = 0;

        while(i < p.length() && j < s.length()) {
            if (j == -1 || p.charAt(i) == s.charAt(j)) {
                i++;
                j++;
            } else {
                j = cal[j];
            }

            if (j == s.length()) {
                return i - (s.length());
            }
        }
        return -1;
    }


    public static void main(String[] args) {

        String p = "ABACABABHI";
        String s = "ABAB";
        int[] cal = new int[s.length()];

        test(cal, s);
        for(int a: cal) {
            System.out.print(a);
        }

        int index = find(p, s, cal);
        System.out.println(index);
    }

}
```

## 快速排序

快速排序其实是 分治思想的运用，将一个 大的问题分解成2个或者多个子问题，

子问题再继续分，最好将答案合并。

快速排序步骤：

- 选择一个基准值。
- 将大于这个基准值放右边，小于等于这个基准值放到左边，这叫一次划分。
- 再以基准值左边 继续递归， 右边继续递归上述过程。



具体步骤： 准备 左右指针

​						选取基准。

​						左指针右移动找一个比基准大的停止，右指针左移动找一个小于（等于）基准的停止。

​						交换，左右指针的元素，继续。直到左指针超过右指针。

​					重复上面基准值左边部分和右边部分。





方法一：

​	中间位数交换。

其实就是 从右边开始找，如果找到小于中值的，就换到前面，但是pivt先存着。

如果左边开始找，大于的，就换到右边，最后中间位置，再存值。

```java
public class Test {

    public static void quick(int l,int r, int[] arr) {
        if (l >= r) return;
        int patition = partitions(l , r , arr);
        quick(l, patition- 1, arr);
        quick(patition + 1, r, arr);
    }

    private static int partitions(int l, int r, int[] arr) {

        int pitv = arr[l];
        while(l < r) {
            while(l < r && arr[r] >= pitv) {r--;}
            arr[l] = arr[r];

            while(l < r && arr[l] <= pitv) {l++;}
            arr[r] = arr[l];
        }

        arr[l] = pitv;
        return l;
    }

    public static void main(String[] args) {

        int[] arr = {2,5,1,4, 1, 9};
        //int[] arr = {1,1,2,7,11,1,1};
        quick(0, arr.length-1 , arr);
        //sortss(arr, 0, arr.length -1);
        for(int a : arr) {
            System.out.print(a);
        }

    }
}
```





方法二：

其实就是，从左边开始找大于的，从右边开始找下于的。

再交换。

```java
   public static void main(String[] args) {
       int num[] = {1,1,2,7,11,1,1};
       // int num[] = {2,5,1,4,1,9};
        new QuickSort().sort(num, 0, num.length-1);
        for (int n : num) {
            System.out.print(n + " ");
        }
    }

    void sort(int num[], int left, int right) {
        if (left <right) {
            int index = partition(num, left, right);
            System.out.println(index);
            sort(num, left, index-1);
            sort(num, index, right);
        }

    }

    public int partition(int[] num, int left, int right) {
        if(num==null || num.length<=0 || left<0 || right>=num.length){
            return 0;
        }
        int prio = num[left];
        while(left<right){
            while (num[left] < prio)
                left++;
            while (num[right] > prio)
                right--;
            if (left<=right) {
                swap(num, left, right);
                left++;
                right--;
            }
        }
        return left;
    }

    public void swap(int[] num, int left, int right) {
        int temp = num[left];
        num[left] = num[right];
        num[right] = temp;
    }

```







总结： 方法一和方法二的区别，最本质上的东西是，最后返回的index索引位置不同。

方法一索引位置l，r 最终相等。  而方法二 index 不等。

## 归并排序

归并排序也是用到了分治的思想，  不同于快排的partition每次让一个数字找到一个合理的位置。

而是递归到底，再合并的想法。



```java
public class GuiTest {

    public static void gui(int l,int r , int[] arr){

        if (l >= r) return;
        int mid = (l + r) >> 1;
        gui(l, mid, arr);
        gui(mid + 1, r , arr);
        merge(arr,l, mid ,r);
    }

    public static void merge(int[] arr,int l,int mid,int r) {
        int[] temp = new int[r -l + 1];

        int index = 0;
        int low = l;
        int high = mid + 1;

        while(low <= mid && high <= r){
            if (arr[low] <= arr[high]) {
                temp[index++] = arr[low++];
            } else {
                temp[index++] = arr[high++];
            }
        }

        while(low <= mid) {
            temp[index++] = arr[low++];
        }
        while(high <= r) {
            temp[index++] = arr[high++];
        }
        int j = 0;
        int len = (r-l+1);
        while(j < len) {
            arr[j + l] = temp[j++];
        }
    }

    public static void main(String[] args) {

        int[] arr = {2,5,1,4,1,9};

        gui(0, arr.length -1 , arr);
        for(int a: arr) {
            System.out.println(a);
        }

    }
}

```



