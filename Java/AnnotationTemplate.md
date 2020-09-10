1.常用的注解：

@author 作者名

@date 日期

@version 版本标识

@parameter 参数及其意义

@return 返回值

@throws 异常类及抛出条件

@deprecated 引起不推荐使用的警告

@override 重写

@see 链接跳转，可以指向包，类，方法，属性

2.设置注释模板的步骤：Window++>Preferences++>Java++>CodeStyle++>CodeTemplates++>Comments(生成Java时自动生成注释)/Code(手动插入注释)

3.具体的Comment如何设置：

1.点击Comments下的Files可对整个Java文件进行注释：包括公司名称，版权所属，作者信息，日期等。

```java
/**  
 * <p>Title: ${file_name}</p>  
 * <p>Description: ${todo}(用一句话描述该文件做什么)</p>  
 * <p>Copyright: Copyright (c) 2017</p>  
 * <p>Company: www.ychs.com</p>  
 * @author lipeng 
 * @date ${date}  
 * @version v1.0  
 */  
```

2.点击Types对类进行注释：

```java
/**  
 * <p>Title: ${type_name}</p>  
 * <p>Description: ${todo}(用一句话描述该文件做什么)</p>  
 * @author shenlan  
 * @date ${date}  
 */  
```

3.点击Fields对字段进行注释：  

```java
/** 
* @Fields ${field} : ${todo}(用一句话描述这个变量表示什么) 
*/
```

4.点击Constructors对构造方法进行注释：

```java
/**  
 * <p>Title: </p>  
 * <p>Description: </p>  
 * ${tags}  
 */  
```

5.点击Methods对方法进行注释：

```java
/**  
 * <p>Title: ${enclosing_method}</p>  
 * <p>Description: ${todo}(用一句话描述这个方法的作用)</p> 
 * ${tags}  
 */  
```

6.点击Overriding Methods对重写方法进行注释：

```java
/* (non-Javadoc)  
 * <p>Title: ${enclosing_method}</p>  
 * <p>Description: ${todo}(用一句话描述这个方法的作用)</p>  
 * ${tags}  
 * ${see_to_overridden}  
 */
```

7.Delegate methods对代表方法进行注释：

```java
/**  
 * ${tags}  
 * ${see_to_target}  
 */
```

8.Getters对get方法进行注释：

```java
/**
 * @return the ${bare_field_name}  
 */
```

9.Setters对set方法进行注释：

```java
/**
 * @param ${param} the ${bare_field_name} to set  
 */
```

