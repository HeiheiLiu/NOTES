# `+`
---
java中`+`的有关细节

---

## `+`运算符
### `+`运算符的作用：
（1）表示正数
（2）表示相加操作
（3）进行字符串的拼接
```java
public class TestOpe03{
    public static void main(String[] args){
        //表示正数：
        System.out.println(+5);//5
        //相加操作：
        System.out.println(5+6);//11
        System.out.println(5+'6');//59
        //字符串的拼接：
        //规则：+左右两侧的任意一侧有字符串，那么这个加号就是字符串拼接的作用，结果一定是字符串
        int num = 56;
        System.out.println("num="+num);//"num=56" ---> num=56
        System.out.println(5+6+"7");//11+"7"--->"117"  --->117
        System.out.println(5+'6'+"7");//59 +"7"--->"597" --->597
        System.out.println("5"+6+"7");//"56"+"7"  --->"567"--->567
        System.out.println("5"+'6'+"7");//"56"+"7"--->"567"--->567
        System.out.println("5"+'6'+'7');//"56"+'7'--->"567"---567
    }
}
```

## `++`优先级>`+`
```java
int a = 5;
System.out.println(a++ + a++);//5+6=11
System.out.println(a++ + ++a);//7+9=16
System.out.println(++a + a++);//10+10=20
System.out.println(++a + ++a);//12+13=25 
```

## `a+=b`  和  `a=a+b`  区别：
1. `a+=b`    可读性稍差 编译效率高   底层自动进行类型转换
2. `a=a+b`     可读性好  编译效率低   手动进行类型转换
3. a+=b相当于a=a+b,那么也相当于  a=b+a吗？ 基本类型相同，String类型不同
4. 下面的代码哪一句出错：  4
```java
byte a = 10;    //--->1
int b = 20;     //--->2
a+=b;   //---->3
a = a+b;   //---->4
```
更正：  `a = (byte)(a+b);`