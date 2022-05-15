# 数组
## 数组的初始化
数组的初始化方式总共有三种：静态初始化、动态初始化、默认初始化。
### 静态初始化
  除了用new关键字来产生数组以外，还可以直接在定义数组的同时就为数组元素分配空间并赋值。

eg:
* 一维数组
```java
int[] arr = {12,23,45};
int[] arr = new int[]{12,23,45};
```
* 二维数组
```java
int[][] arr = {{1,2},{4,5,6},{4,5,6,7,8,9,9}};
int[][] arr =new int[][] {{1,2},{4,5,6},{4,5,6,7,8,9,9}};
```
>注意：
1.`new int[3]{12,23,45};`-->错误 更正`new int[]{12,23,45};`
2.`int[] arr ;arr = {12,23,45};`  --->错误`int[] arr ;arr = new int[]{12,23,45};`

### 动态初始化
数组定义与为数组元素分配空间并赋值的操作分开进行。

eg:
* 一维数组
```java
int[] arr ;
arr = new int[3]
arr[0] = 12;
arr[1] = 23;
arr[2] = 45;
```
* 二维数组
```java
int[][] arr = new int[3][]; //本质上定义了一维数组长度为3，每个“格子”中放入的是一个数组
arr[0] = new int[]{1,2};
arr[1] = new int[]{3,4,5,6};
arr[2] = new int[]{34,45,56};
```
  * 二维数组的遍历
    ```java
    int[][] arr = new int[3][2];
    public class TestArray16{
        public static void main(String[] args){
            int[][] arr = new int[3][2];
            //本质上：定义一维数组，长度为3，每个数组“格子”中，有一个默认的长度为2的数组：
            arr[1] = new int[]{1,2,3,4};
            //数组遍历：
            for(int[] a:arr){
                for(int num:a){
                    System.out.print(num+"\t");
                }
                System.out.println();
            }
        }
    }
    ```

### 默认初始化
数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。

eg:
`int[] arr = new int[3];`   ---> 数组有默认的初始化值

## Array工具类
```java
import java.util.Arrays;
public class TestArray13{
    public static void main(String[] args){
        //给定一个数组：
        int[] arr = {1,3,7,2,4,8};
        //toString:对数组进行遍历查看的，返回的是一个字符串，这个字符串比较好看
        System.out.println(Arrays.toString(arr));
        
        //binarySearch:二分法查找：找出指定数组中的指定元素对应的索引：
        //这个方法的使用前提：一定要查看的是一个有序的数组：
        //sort：排序 -->升序
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));
        System.out.println(Arrays.binarySearch(arr,4));
        
        int[] arr2 = {1,3,7,2,4,8};
        //copyOf:完成数组的复制：
        int[] newArr = Arrays.copyOf(arr2,4);
        System.out.println(Arrays.toString(newArr));
        
        //copyOfRange:区间复制：
        int[] newArr2 = Arrays.copyOfRange(arr2,1,4);//[1,4)-->1,2,3位置
        System.out.println(Arrays.toString(newArr2));
        
        //equals:比较两个数组的值是否一样：
        int[] arr3 = {1,3,7,2,4,8};
        int[] arr4 = {1,3,7,2,4,8};
        System.out.println(Arrays.equals(arr3,arr4));//true
        System.out.println(arr3==arr4);//false ==比较左右两侧的值是否相等，比较的是左右的地址值，返回结果一定是false
        
        //fill：数组的填充：
        int[] arr5 = {1,3,7,2,4,8};
        Arrays.fill(arr5,10);
        System.out.println(Arrays.toString(arr5));
    }
}
```
##  数组的复制操作
`static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length)`
>src->源数组
srcPos->源数组中的起始位置
dest->目标数组
destPos->目标数组中的起始位置
length->要复制的数组元素个数