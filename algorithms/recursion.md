# 算法学习笔记

[toc] 

## 二、递归

### 1.递归基础知识

1.1递归设计经验

- 找重复（子问题）
- 找重复中的变化（参数）
- 找参数变化的趋势（出口）

### 2.求阶乘

2.1问题:求n的阶乘

2.2想法：

- 想法一：
  - 找重复：n的阶乘=n*(n-1的阶乘),f(n)是求n的阶乘，f(n - 1)就是求n - 1的阶乘
  - 找变化：n每次减少1，变化的量作为参数
  - 找出口：n = 1的时候，返回1

2.3解法：

- 解法一：递归解法

```java
public static int factorial(int n) {
    if (n == 1) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

### 3.打印i~j

3.1问题：打印i到j

3.2想法：

- 想法一：
  - 找重复：打印i-j = 打印i + 打印i+1到j
  - 找变化：i每次加1
  - 找出口：i大于j的时候退出

3.3思维：

- 老板思维：自己做一部分，剩下的交给别人去做

- 切蛋糕思维：自己切一块，剩下的交给别人去切

3.4：解法：

- 解法一：递归解法

```java
public static void printItJ(int i,int j) {
    if (i > j) {
        return;
    }
    System.out.println(i);
    printItJ(i + 1,j);
}
```

### 4.数组求和

4.1问题：给定一个数组，求这个数组各元素的和

4.2想法：

- 想法一：
  - 找重复：arr的和 = arr[0] + arr[1 ~arr.length -1]的和
  - 找变化：添加变量begin，begin从0开始，每次加1
  - 找出口：当begin = arr.length - 1的时候，退出

4.3解法：

- 解法一：递归解法

```java
public static int sumArr(int[] arr,int begin) {
    if (begin == arr.length - 1) {
        return arr[begin];
    }
    return arr[begin] + sumArr(arr,begin + 1);
}
```

### 5.反转字符串

5.1问题：给定一个字符串，反转输出

5.2想法：

- 想法一：
  - 找重复：字符串的反转 = 最后一个字符 + 前面字符的反转
  - 找变化：添加一个变量end，end的值每次减少1
  - 找出口：end指向第一个字符的时候返回

5.3解法：

- 解法一：递归解法

```java
public static String reverse(String str,int end) {
    if (end == 0) {
        return "" + str.charAt(0);
    }
    return str.charAt(end) + reverse(str,end - 1);
}
```

### 6.斐波那契

6.1问题：求斐波那契数列 1，1，2，3，4，5，8，13，，，

6.2想法：

- 想法一：多分支递归，f(n) = f(n - 1) + f(n - 2)

6.3解法：

- 解法一：多分支递归解法

```java
public static int fib(int n) {
    if (n == 1 || n == 2) {
        return 1;
    }
    return fib(n - 1) + fib(n - 2); 
}
```

### 7.最大公约数

7.1问题：求两个数的最大公约数

7.2思路：

- 思路一：辗转相除法，m%n = 0,则最大公约数为n，如果m%n = k,则把n赋值给m，把k赋值给n，再次m%n = ?递归的出口：因为每次把余数k赋给n，所以当n = 0也就是余数为零时返回m

7.3解法：

- 解法一：辗转相除法

```java
public static int gcd(int m, int n) {
    if (n == 0) {
        return m;
    }
    return gcd(n,m%n);
}
```

### 8.汉诺塔

8.1问题：汉诺塔：把A柱的盘子移动到B柱，辅助柱C，每次移动一个，并且只能时大盘子在下面，小盘子在上面

8.2想法：

- 想法一：递归解法，子问题是什么？把1~n个盘子从A挪到B = 把1~n-1个盘子从A挪到C（C为辅助柱），把n挪到B，之后变A为辅助柱子，把1~n-2个盘子挪到A，把n-1挪到B，之后变为C为辅助柱子

8.3解法：

- 解法一：递归解法

```java
public static void hanoi(int N,String from,String to,String help) {
    if (N == 1) {
        System.out.println("move" + N + "from" + from + "to" + to);
    } else {
        hanoi(N - 1, from, help, to);
        System.out.println("move" + N + "from" + from + "to" + to);
        hanoi(N - 1, help, to, from);
    }
}
```

9.小白上楼梯

9.1问题：小白正在上楼梯，楼梯有n阶台阶，小白一次可以上1阶，2阶或者3阶，实现一种方法，计算小白有多少种走完楼梯的方式

9.2思路：

- 思路一：三分支递归：f(n) = f(n - 1) + f(n - 2) + f(n - 3)

9.3解法：

- 解法一：三分支递归

```java
public static int stairs(int n) {
    if (n == 0 || n == 1) {
        return 1;
    }
    if (n == 2) {
        return 2;
    }
    return stairs(n - 1) + stairs(n - 2) + stairs(n - 3);
}
```

