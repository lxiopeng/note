# 算法学习笔记

[toc] 



## 一、位运算

### 1.位运算基础

1.1&(与)，|(或)，~(非/取反)，^(异或)

- 与：都为1结果为1
- 或：有一个为1结果为1
- 异或：二者不同时结果为1（可以理解为不进位加法）

1.2>>(右移),<<(左移),>>>(无符号右移)

1.3异或运算：A^A=0,A^0=A

### 2.位运算的简单运用

2.1判断奇偶数

```java
x & 1 == 0;//偶数
x & 1 == 1;//奇数
```

2.2获取二进制位是0还是1（两种解决方案）

2.3交换两个变量的值

```java
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

2.4不用判断语句，求整数的绝对值

### 3.找出唯一成对的数

3.1问题：1-1000这1000个数放在含有1001个元素的数组中，只有唯一的一个元素值重复，其他均只出现一次。每个数组元素只能访问一次，设计一个元素，将他找出来；不用辅助空间，能否设计一个算法实现？

3.2思路

- 思路一：由异或的性质A^A=0,A^0=A入手，将1001个元素连续异或（消除重复），则唯一成对的数别消除，如何找出唯一成对的数？将1-1000不重复的连续异或，之后和之前的数组元素的连续异或就可以得到这个数
- 思路二：开辟辅助空间helper，初始化helper，helper的下标表示arr对应的值，helper的值相当于一个计数器，初始化之后再次遍历找出helper值为2的下标即为arr中出现两次的数

3.3解法

- 解法一：异或运算

```java
int x1 = 0;
//求出1~N-1的连续异或
for (int i = 1; i <= N - 1; i++) {
    x1 = x1^i;
}
for (int i = 0; i < arr.length; i++) {
    x1 = x1^arr[i];
}
System.out.println(x1);
```

- 解法二：开辟辅助空间

```java
int[] helper = new int[N];
for (int i = 0; i < N; i++) {
    helper[arr[i]]++;
}
for (int i = 0; i < helper.length; i++) {
    if(helper[i] == 2) {
        System.out.println(i);
        break;
    }
}
```

### 4.找出唯一落单的数

4.1问题：一个数组里除了某一个数字之外，其他数字都出现了两次。编写一个程序找出这个只出现的一次的数字

4.2思路

- 思路一：异或运算，去除重复

4.3解法

- 解法一：异或运算，去重

```java
int x1 = 0;
for (int i = 0; i < arr.length; i++) {
    x1 = x1 ^ arr[i];
}
System.out.println(x1);
```

### 5.二进制中一的个数

5.1问题：请实现一个函数，输入一个整数，输出该二进制表示中1的个数。例如：9的二进制表示为1001，有2位是1

5.2思路：

- 思路一：把1都数出来，怎么数？循环32次，每一次把1移动（左移运算）到相应的位上做与运算，根据运算结果判断当前位是否为1，是的话计数
- 思路二：把原数无符号右移，和1做与运算，1不变
- 思路三：每次消除一个1，怎么消除，减1，减1的效果就是第一个1之后的低位会全部变为1，前面的数不动，例如111000减1变为110111，之后原数和减1后的数做与运算后就会消除最低为的1

5.3解法：

- 解法一：每次把1左移一位和原数的对应位置做与运算，从而输出1的个数

```java
int count = 0;
for (int i = 0; i < 32; i++) {
    if((N & (1<<i)) == (1<<i)) {
        count++;
    }
}
System.out.println(count);
```

- 解法二：每次原数无符号右移1位，与1做与运算

```java
int count = 0;
for (int i = 0; i < 32; i++) {
    if(((N >>> i) & 1) == 1) {
        count++;
    }
}
System.out.println(count);
```

- 解法三：每次消除最底位的1，count++,直到原数为零退出循环

```java
int count = 0;
while(N != 0) {
    N = (N & (N - 1));
    count++;
}
System.out.println(count);
```

### 6.是不是2的整数次方

6.1问题：用一条语句判断一个整数是不是2的整数次方

6.2思路：

- 思路一：二进制的整数次方的特点，只有以为是1，其余位都是0

6.3解法：

- 解法一：消除一个1，如果原数变为0则是2的整数次方，否则不是

```java
if((N & (N - 1)) == 0) {
    System.out.println("yes");
} else {
    System.out.println("no");
}
```

7.将整数的奇偶位互换

7.1问题：将整数的奇偶位互换，比如9的二进制：1001变为0110

7.2思路：

- 思路一：十进制转为二进制，二进制转字符串，字符串转字符数组，交换相邻的两位
- 思路二：与运算，用0来做与运算叫做消除，用1来做与运算叫做保留，原数与01010101保留偶数位，原数与10101010做与运算保留奇数位，保留奇数位的右移一位，保留偶数位的左移一位，两者做异或即可

7.3解法：

-  解法二：与运算和异或运算同时运用

```java
int N = sc.nextInt();
//取出偶数位：10101010....
int ou = N & 0xaaaaaaaa;
//取出奇数位：01010101....
int ji = N & 0x55555555;
int res = (ou >> 1) ^ (1 << ji);
System.out.println(res);
```

8.0~1之间的浮点数的二进制表示

8.1问题：给定一个介于0和1之间的实数，如（0.625），类型位double,打印它的二进制表示（0.101，因为小数点后的二进制分别表示0.5，0.25，0.125.......）,如果该数字无法精确的用32位以内的二进制表示，则打印“ERROR”

8.2思路：

- 思路一：乘二挪整，乘二，如果大于一，结果追加1，原数去除1，否则结果追加0，原数不变，直到原数等于0，或超过34（32+2）位无法表示

8.3解法：

- 解法一：乘二挪整

```java
double num = 0.625;
StringBuilder sb = new StringBuilder("0.");
while(num != 0) {
    double n = num * 2;
    //如果num*2大于1，sb追加1，num*2-1
    if (n >= 1) {
        sb.append("1");
        num = n - 1;
    } else {
        //如果num*2小于一，num=num*2，sb追加0
        sb.append("0");
        num = n;
    }
    //长度超过32位，退出
    if (sb.length() > 34) {
        System.out.println("ERROR");
        break;
    }
}
System.out.println(sb);
```

9.出现k次与出现1次

9.1问题：数组中只有一个数出现了1次，其他的数都出现了k次，请输出只出现了1次的数

9.2思路：

- 思路一：不进位加法（异或），两个相同的二进制数做不进位加法结果为零，三个相同的三进制数做不进位加法结果为零，十个相同的十进制数做不进位加法结果为零，，，所有数转成k进制，然后做k进制的不进位加法，最后转成十进制

9.3解法：

- 解法一：不进位加法,先转为三进制，结果转为二位字符数组中，然后做不进位加法

```java
//构造原数组
int[] arr = {1,1,1,2,2,2,3,3,3,4,5,5,5,6,6,6};
int len = arr.length;
//构造二维数组存储每个数的三进制
char[][] kRadix = new char[len][];
//进制数位3进制
int k = 3;
//转成三进制之后最长的长度
int maxLen = 0;
//十进制转三进制
for (int i = 0; i < arr.length; i++) {
    kRadix[i] = new StringBuilder(Integer.toString(arr[i],3)).reverse().toString().toCharArray();
    if (kRadix[i].length > maxLen) {
        maxLen = kRadix[i].length;
    }
}
//不进位加法
int[] resArr = new int[maxLen];
for (int i = 0; i < len; i++) {
    for (int j = 0; j < maxLen; j++) {
        if(j >= kRadix[i].length) {
            resArr[j] += 0;
        } else {
            resArr[j] += kRadix[i][j] - '0';
        }
    }
}
//结果转成十进制
int res = 0;
for (int i = 0; i < maxLen; i++) {
    res += Math.pow(3, i);
}
System.out.println(res);
```
