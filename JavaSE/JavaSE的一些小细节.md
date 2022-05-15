# java细节
## 科学记数法形式
314e2      314E2 (E的大小写没有区分)    314E-2
```java
double  f = 314e2;  //314*10^2-->31400.0
double  f2 = 314e-2; //314*10^(-2)-->3.14
```
## 尾缀注意点
1. 添加尾缀说明
　　我们知道Java在变量赋值的时候，其中float、double、long数据类型变量，需要在赋值直接量后面分别添加f或F、d或D、l或L尾缀来说明。
　　其中，long类型最好以大写L来添加尾缀，因为小写l容易和数字1混淆。
　　例如：
`long lNum  = 1234L;`
`float fNum = 1.23f;`
`double dNum = 1.23d;`
>这是Java语法规定，不添加尾缀很容易引起编译器报错，并且程序可读性也会变差。

2. 不添加尾缀也不会报错的情况
　　Java语言中，整数直接量（例如：1、2、10等），JVM虚拟机是默认为int类型数据的。所以，当整数直接量赋给long、float或者double，而不添加尾缀，虚拟机也会直接将int类型数据自动转换为对应类型然后赋值。因为数据长度短的转换为长的并不会造成数据丢失，所以默认可以自动转换。　
　　例如：
`long  lNum  = 5;   //不报错，因为int自动转换为long类型，不会报错`
`float fNum  = 7;   //不报错，因为int自动转换为float类型，不会报错`
`double dNum = 10;  //同上`
　　但是，当浮点直接量（例如：1.2等），JVM虚拟机默认为double类型，如果直接赋值给float就会引起编译器报错。
`float fNum  = 1.2; //报错，因为1.2虚拟机是默认为double类型，不能直接赋值给float类型变量`
`float fNew  = 1.3f;//正确，因为尾缀添加了f，即告诉了虚拟机1.3属于float类型变量`
3. 总结
　　所以，当Java中遇到这三种类型变量需要赋直接量时候，最好都添加上相应的尾缀。这样不仅会防止编译器报错，也会增加程序的可读性。
　　但是下面这种情况就算添加尾缀也是错的，因为尾缀仅是为了告诉虚拟机该直接数属于什么数据类型，而不能实现数据类型强制转换。
`long lNum = 1.2L;      //错误，double类型数据不能直接赋值给long类型`
`long lNew = (long)1.2; //正确，double类型数据强制转换为long类型`

4. 浮点数注意点
```java
//注意：浮点型默认是double类型的，要想将一个double类型的数赋给float类型，必须后面加上F或者f
float f1 = 3.14234567898623F;
System.out.println(f1);
//注意：double类型后面可以加D或者d，但是一般我们都省略不写
double d1 = 3.14234567898623D;
System.out.println(d1);
//注意：我们最好不要进行浮点类型的比较：
float f2 = 0.3F;
double d2 = 0.3;
System.out.println(f2==d2);
```
## boolean类型
`boolean`类型有两个常量值，`true`和`false`，在内存中占一位（不是一个字节），不可以使用 `0` 或非 `0` 的整数替代 `true` 和 `false` ，这点和C语言不同。 `boolean` 类型用来判断逻辑条件，一般用于程序流程控制 。
## 类型转换
```java
public class TestVar{
    public static void main(String[] args){
        //类型转换的两种形式：
        double d = 6;//int-->double  自动类型转换
        System.out.println(d);
        int i = (int)6.5;//double--->int  强制类型转换 （强转）
        System.out.println(i);
        
        //在同一个表达式中，有多个数据类型的时候，应该如何处理：
        //多种数据类型参与运算的时候，整数类型，浮点类型，字符类型都可以参与运算，唯独布尔类型不可以参与运算。
        //double d2 = 12+1294L+8.5F+3.81+'a'+true;
        double d2 = 12+1294L+8.5F+3.81+'a';
        System.out.println(d2);
        /*
        类型级别：(从低到高的)
        byte,short,char-->int--->long--->float--->double
        级别用来做什么？当一个表达式中有多种数据类型的时候，要找出当前表达式中级别最高的那个类型，然后
        其余的类型都转换为当前表达式中级别最高的类型进行计算。
        double d2 = 12+1294L+8.5F+3.81+'a';
                  = 12.0+1294.0+8.5+3.81+97.0
        */
        int i2 = (int)(12+1294L+8.5F+3.81+'a');
        System.out.println(i2);
        /*
        在进行运算的时候：
        左=右  : 直接赋值
        左<右  ：强转
        左>右  ：直接自动转换
        */
        
        //以下情况属于特殊情形：对于byte，short，char类型来说，只要在他们的表示范围中，赋值的时候就不需要进行
        //强转了直接赋值即可。
        byte b = 12;
        System.out.println(b);
        byte b2 = (byte)270;
        System.out.println(b2);
    }
}
```
## final常量
一个变量被final修饰，这个变量就变成了一个常量，这个常量的值就不可变了。这个常量就是我们所说的字符常量。
### 字面常量
包括整形常量，字符型常量，字符串常量。注意：不存在数组常量，结构体常量等结构型的字面常量。但是存在结构型的符号常量
### 符号常量
（可以定义结构型常量）用#define和const定义的常量！
这两种常量之间的区别：#define定义的常量，除了字符串字面常量外都不占内存，所以无法取常量的地址，仅仅是宏替换而已
### eg：
1. `#define NAME “pang dong”；`
本质是字符串字面常量，会占用“静态存储区”；
2. `#define MAX 256；`
本质是整形的字面常量，不会分配内存。
>约定俗成的规定：字符常量的名字全部大写.

## Scanner的使用(`import java.util.Scanner;`)
```java
//拿来一个扫描器：
Scanner sc = new Scanner(System.in);
//给一个友好性的提示：
System.out.print("请录入一个半径：");
//让扫描器扫描键盘录入的int类型的数据：
int r = sc.nextInt();
```
## 逻辑运算符与位运算符
* 逻辑运算符：
逻辑与 ：`&` 规律：只要有一个操作数是`false`，那么结果一定是`false`
短路与：`&&` 规律：效率高一些，只要第一个表达式是`false`，那么第二个表达式就不用计算了，结果一定是`false`
逻辑或：`|` 规律：只要有一个操作数是`true`，那么结果一定是`true`
短路或：`||` 规律：效率高一些，只要第一个表达式是`true`，那么第二个表达式就不用计算了，结果一定是`true`
逻辑非：   `!`  规律：相反结果
逻辑异或： `^`  规律：两个操作数相同，结果为false，不相同，结果为`true`
* 位运算符：
`<<`   左移
`>>` 有符号右移
`>>>` 无符号右移
`&` 与
`|` 或
`^`异或
`~`反
> 1. 4乘以8最快的方式：  4<<3 
> 2. -6>>2 = -2
> 6:`000000000 00000000 00000000 00000110`
> 取反:`11111111 11111111 11111111 11111001`
> 加1:`11111111 11111111 11111111 11111010`--> `-6`
> `>>`:`11111111 11111111 11111111 11111110`~~`10`~~
> 减1:`11111111 11111111 11111111 11111101`
> 取反:`00000000 00000000 00000000 00000010`
> 加负号:`-2`

## `switch`

* 语法结构：
```java
switch(){
        case * :
        case * :
        .......
}
```
* `switch`后面是一个()，()中表达式返回的结果是一个等值，这个等值的类型可以为：
**`int`,`byte`,`short`,`char`,`String`,枚举类型**
* 这个()中的等值会依次跟`case`后面的值进行比较，如果匹配成功，就执行:后面的代码
* 为了防止代码的“穿透”效果：在每个分支后面加上一个关键词`break`，遇到`break`这个分支就结束了
* 类似`else`的“兜底”“备胎”的分支：`default`分支
* `default`分支可以写在任意的位置上，但是如果没有在最后一行，后面必须加上`break`关键字，
如果在最后一行的话，`break`可以省略
* 相邻分支逻辑是一样的，那么就可以只保留最后一个分支，上面的都可以省去不写了
* `switch`分支和`if`分支区别：
表达式是等值判断的话--》`if` ，`switch`都可以
如果表达式是区间判断的情况---》`if`最好
* `switch`应用场合：就是等值判断，等值的情况比较少的情况下

## 构成方法重载的条件：
* 不同的含义：形参类型、形参个数、形参顺序不同
* **只有返回值不同不构成方法的重载**
如：`int a(String str){}`与 `void a(String str){}`不构成方法重载
* **只有形参的名称不同不构成方法的重载**
如：`int a(String str){}`与`int a(String s){}`不构成方法重载

## main方法

* main方法：程序的入口，在同一个类中，如果有多个方法，那么虚拟机就会识别main方法，从这个方法作为程序的入口
* main方法格式严格要求：`public static void main(String[] args){}`

>`public static` --->修饰符 ，暂时用这个 -->面向对象一章
`void` --->代表方法没有返回值 对应的类型void
`main `--->见名知意名字
`String[] args`  --->形参  --->不确定因素

### 问题：程序中是否可以有其他的方法也叫main方法？
可以，构成了方法的重载。
```java
public class TestArray{
    public static void main(String[] args){
                
    }
    public static void main(String str){
            
    }
}
```

### 形参为String[] 那么实参到底是什么？
```java
public class TestArray{
    public static void main(String[] args){
        //从侧面验证：
        //int[] arr1; //如果对数组只声明，没有后续操作，那么相当于 白定义了。
        //int[] arr2 = null; 
        //System.out.println(arr2.length);//Exception in thread "main" java.lang.NullPointerException
        //int[] arr3 = new int[0];
        //System.out.println(arr3.length);//0
        //int[] arr4 = new int[4];
        //System.out.println(arr4.length);//4
        
        //System.out.println(args.length);//0
        //从这个结果证明，参数是String[],实参是  new String[0] 
        //默认情况下，虚拟机在调用main方法的时候就是传入了一个长度为0的数组
        
        System.out.println(args.length);
        for(String str:args){
                System.out.println(str);
        }
    }
}
```
手动传入实参：
有特殊符号的时候可以加上`""`
```
D:java_code>java TestArray aa bb cc dd "e e"
5
aa
bb
cc
dd
e e
```

没有特殊符号用空格隔开即可：
```
D:java_code>java TestArray aa bb cc dd ee
5
aa
bb
cc
dd
ee
```

## 可变参数(了解，不使用)
```java
public class TestArray12{
    /*
    1.可变参数：作用提供了一个方法，参数的个数是可变的 ,解决了部分方法的重载问题
    int...num
    double...num
    boolean...num
    2.可变参数在JDK1.5之后加入的新特性
    3.方法的内部对可变参数的处理跟数组是一样
    4.可变参数和其他数据一起作为形参的时候，可变参数一定要放在最后
    5.我们自己在写代码的时候，建议不要使用可变参数。
    */
    public static void main(String[] args){
            //method01(10);
            //method01();
            //method01(20,30,40);
            method01(30,40,50,60,70);
            //method01(new int[]{11,22,33,44});
    }
    public static void method01(int num2,int...num){
        System.out.println("-----1");
        for(int i:num){
                System.out.print(i+"\t");
        }
        System.out.println();
        
        System.out.println(num2);
    }
}
```
