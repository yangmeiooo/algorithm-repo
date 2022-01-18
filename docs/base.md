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





