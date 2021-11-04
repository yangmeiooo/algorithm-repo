#### [剑指 Offer 41. 数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/) hard

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。

```java
class MedianFinder {

    // 设计一个数据结构
    // 能够添加和找到当前加入元素的中位数
    // 难点：1. 可以被添加 无限个数，数被怎么存储下来呢？ 其实需要存吗？根本不需要
    //      
    //      2. addNum 进去的数，其实后续除了求中位数的时候会用到。其他多余的数
    //          其他时候，多余的数 不会被用到了。
    //      3. 每次添加一个元素，其实都要有序，其实这个时候就用到了堆。 堆这个数据结构能维持顺序。
    //      4. 不管后续数据怎么加，保证数据顺序往前流动？ 怎么做呢？
    //      5. 单个数字，leftmax， rightmin 其实是不合适的。 就得使用数据容器。
    //      6. int 都得先转double

    // 维护当前数据结构中的数字数量
    private int size = 0;

    // 左边 最大
    private int leftmax = 0;
    // 右边 最小
    private int rightmin = 0;

    /** initialize your data structure here. */
    public MedianFinder() {

    }
    
    public void addNum(int num) {
        ++this.size;
        if(this.size == 1) {
            leftmax = num;
        } else if (this.size == 2) {
            if (num >= leftmax) {
                rightmin = num;
            } else {
                int temp = leftmax;
                leftmax = num;
                rightmin = temp;
            }
           
        } else if (num > rightmin) {
            leftmax = rightmin;
            rightmin = num;
        } else {
            leftmax = leftmax >= num ? leftmax: num;
        }
    }
    
    public double findMedian() {
        if (size % 2 == 0) {
            return (double)(((double)leftmax + (double)rightmin) / 2);
        } else {
            return (double)(leftmax);
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```



以上是错误的。



正确的题解：

```
```







#### [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

```java
class Solution {

    // 滑动窗口解法，应该是
    // 最小的时候，会扩大，大于的时候会缩小
    // 怎么才能很好的写出这个算法呢？？
    public int[] maxSlidingWindow(int[] nums, int k) {
        int max = Integer.MIN_VALUE:

        int l = -1;
        int r = 0;
        int len = nums.length;

        while(r < len && r - l <= k) { // 小于 继续while

                    // 看左边边界 l 先到合适范围。

                    // 再看右边范围

                    // 选出当前窗口的最大值

                    // 再移动右边一位

                    // 再缩小左边一位
        }
    }
}
```

