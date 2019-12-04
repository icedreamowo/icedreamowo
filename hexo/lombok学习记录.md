---
title: lombok学习记录
date: 2019-09-22 20:30:00
tags:
	-IT TECH
---
<h1>lombok目前存在一些已知问题 暂停深入学习 19/10/12</h1>  

**lombok**可用于减少代码量,优化代码,使代码风格更美观  
**lombok**提供了多种注释,每种注释可以自动生成一些类中的常见类似代码,如Getter/Setter代码块,构造器代码块,Equals函数等  
lombok包在IDE环境下使用时会产生编译错误,需要运行lombok.jar并选择编译器的路径,在自动更改编译器的配置文件之后可以成功编译  

-----
例:Person类

*@AllArgsConstructor*
为类生成一个全参的函数构造器
即
```java
Person(arg1, arg2, arg3...){
	this.arg1 = arg1;
	//...
}
```

*@NoArgsConstructor*
为类生成一个无参的函数构造器
即
```java
Person(){ }		//default value
```
注意当成员变量中有**被final修饰的未定义成员变量时**使用此注释会报错
~~警告:The blank final field (...) may not have been initialized~~

*@RequiredArgsConstructor*
为类生成一个**必要参数**的函数构造器
**必要参数**与@NonNull和~~final~~注释有关
当成员变量被@NonNull或者~~final~~修饰时,它是一个**必要参数**
```java
@RequiredArgsConstructor
public class Person {
	private String arg1;
	@NonNull private String arg2;
}

	Person(String arg2){
		this.arg1 = arg2;
	}
```

*@EqualsAndHashCode*
*@ToString*

*@Getter*
*@Setter*

*@Data*
根据API文档解释@Data注释相当于@Getter,@Setter,@RequiredArgsConstructor,@ToString和@EqualsAndHashCode
但是经过实际测试,@Data在有@AllArgsConstructor或@NoArgsConstructor注释的情况下将**不会实现**@RequiredArgsConstructor注释
**例子如下:**
```java
@Data
public class Person {
	private String arg1;
	@NonNull private String arg2;
}
/*	此时生成的构造函数
	Person(String arg2);
*/

@Data
@AllArgsConstructor
public class Person {
	private String arg1;
	@NonNull private String arg2;
}
/*	此时可用的构造函数
	Person(String arg1,String arg2);
*/

@Data
@NoArgsConstructor
public class Person {
	private String arg1;
	@NonNull private String arg2;
}
/*	此时可用的构造函数
	Person();
*/

@Data
@AllArgsConstructor
@NoArgsConstructor
@RequiredArgsConstructor
public class Person {
	private String arg1;
	@NonNull private String arg2;
}
/*	此时可用的构造函数
	Person();
	Person(String arg2);
	Person(String arg1,String arg2);
*/
```
必要参数函数构造器在*@RequiredArgsConstructor*重复注释后再次可用,这可能是一个bug


*@Cleanup*

*@Helper*
用于修饰在**方法内部**定义的辅助类

*@ExtensionMethod*

*@NonFinal*

*@NonNull*

*@SneakyThrows*

*@Synchronized*

*@val*
*@var*

*@Value*

-----

*@Accessors*

*@Builder*
*@Builder.ObtainVia*
*@Singular*
*@SuperBuilder*

*@FieldDefaults*

*@PackagePrivate*

*@FieldNameConstants*

*@Tolerate*

*@UtilityClass*

*@With*

-----

***日志类注释***
*@Log4j*
*@Log4j2*

*@CustomLog*

*@CommonsLog*

*@Flogger*

*@JBossLog*

*@Log*

*@Slf4j*

*@XSlf4j*

-----
hombok API文档			:https://projectlombok.org/api/overview-tree.html
随便找的博客教程		:https://www.cnblogs.com/heyonggang/p/8638374.html

