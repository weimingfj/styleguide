#Java代码规范  v0.3#
##源文件基础##
1. 文件名  
源文件以其最顶层的类名来命名，大小写敏感，文件扩展名为.java。
2. 文件编码：UTF-8  
源文件编码格式为 UTF-8。
3. 源文件结构  
	源文件包含(按顺序地)：
  - 许可证或版权信息(如有需要)
  - package语句
  - import语句
  - 一个顶级类(只有一个)  

	以上每个部分之间用一个空行隔开。
## 命名约定 ##
遵循驼峰式命名法，标识符只能使用ASCII字母和数字，因此每个有效的标识符名称都能匹配正则表达式\w+。

1. 包名  
使用小写字母如 com.xxx.settlment，不要 com.xxx.Settlement；单词间不要用字符隔开，比如 com.xxx.settlment.jsfutil，而不要com.xxx.settlement.jsf_util。
2. 类名  
类名要首字母大写，比如 SupplierService, PaymentOrderAction。
3. 方法名  
方法名都要符合首字母小写的风格。  
方法名通常是动词或动词短语，一般情况下动词在前，如addOrder()。  
4. 常量名  
全部字母大写，用下划线分隔单词。一般情况下用static final修饰的变量就是常量。
5. 变量名
变量名（包括方法的参数名）首字母小写，名字通常是名词或名词短语，应该避免用单个字符命名或类似text1、test2之类的命名方式。
6. 枚举  
全部字母大写，用下划线分隔单词，换行可选。

		private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }

		public enum Events {
			ORDER_PAID,
			ORDER_CREATED
		}

## 代码格式 ##
1. 使用大括号  
大括号与if, else, for, do, while语句一起使用，即使只有一条语句(或是空)，也应该把大括号写上。  
	**1.1.** 对于非空块和块状结构，大括号遵循Kernighan和Ritchie风格 (Egyptian brackets):
	- 左大括号前不换行
	- 左大括号后换行
	- 右大括号前换行
	- 如果右大括号是一个语句、函数体或类的终止，则右大括号后换行; 否则不换行。例如，如果右大括号后面是else或逗号，则不换行。  
  示例:

            public void method() {
	        	if (condition()) {
					try {
	    				something();
	    			} catch (ProblemException e) {
	    				recover();
					}
				}
	    	}

	**1.2.** 一个空的块状结构里什么也不包含，大括号可以简洁地写成{}，不需要换行。例外：如果它是一个多块语句的一部分(if/else 或 try/catch/finally) ，即使大括号内没内容，右大括号也要换行。  
  示例：

            void doNothing() {}
        
2. 块缩进：4个空格  
每当开始一个新的块，缩进增加4个空格，当块结束时，缩进返回先前的缩进级别。缩进级别适用于代码和注释。  
这里使用空格代替tab的原因主要是统一代码显示的格式，对于习惯使用tab的同学，请调整IDE对tab的配置修改为4个空格，切勿tab与空格混用。
3. 一行一个语句  
每个语句后要换行。
4. 行宽  
不做硬性要求，由于我们现在用的都是宽屏，建议120-150个字符，已美观及易读性为主
5. 自动换行  
定义：一般情况下，一行长代码为了避免超出列限制(120或150个字符)而被分为多行。  
自动换行时，第一行后的每一行至少比第一行多缩进4个空格。  
当存在连续自动换行时，同一级语法元素的缩进是相同的，如果不同级则再多缩进4个空格。
6. 空行  
空行可以表达代码在语义上的分割，注释的作用范围等等。将类似操作，或一组操作放在一起不用空行隔开，而用空行隔开不同组的代码。  
以下情况需要使用一个空行：
  - 类内连续的成员之间：字段，构造函数，方法，嵌套类，静态初始化块，实例初始化块。
	> 例外： 两个连续字段之间的空行是可选的，用于字段的空行主要用来对字段进行逻辑分组。
  - 在函数体内，语句的逻辑分组间使用空行。
  - 多个连续的空行是允许的，但没有必要这样做(我们也不鼓励这样做)。  
  例子：

			order = orderDao.findOrderById(id);

			//update properties
			order.setUserName(userName);
			order.setPrice(456);
			order.setStatus(PAID);

			orderService.updateTotalAmount(order);

			session.saveOrUpdate(order);
上例中的空行，使注释的作用域很明显。
7. 用小括号来限定组  
除非作者和reviewer都认为去掉小括号也不会使代码被误解，或是去掉小括号能让代码更易于阅读，否则我们不应该去掉小括号。 
8. 变量声明  
不要使用组合声明，比如int a, b;。
9. 注解(Annotations)  
注解紧跟在文档块后面，应用于类、方法和构造函数，一个注解独占一行。缩进级别不变。参数上的注解允许出现在同一行。例如：

		@Result
		private String name;

		@Override
		@Nullable
		public String getNameIfPresent(@Value String str) { ... }
10. 注释  
注释与其周围的代码在同一缩进级别。它们可以是/\* \.\.\. \*/风格，也可以是//\.\.\.风格。对于多行的/\* \.\.\. \*/注释，后续行必须从\*开始， 并且与前一行的\*对齐。以下示例注释都是OK的。

			/*
			 * This is          // And so           /* Or you can
 			 * okay.            // is this.          * even do this. */
 			 */
## Javadoc ##
表明类和方法等的意义和用法等的注释，要以javadoc的方式来写。Java Doc是个类的使用者来看的，主要介绍 是什么，怎么用等信息。凡是类的使用者需要知道，都要用Java Doc 来写。非Java Doc的注释，往往是个代码的维护者看的，着重告述读者为什么这样写，如何修改，注意什么问题等。

1. 格式  
多行形式：

		/**
 		 * Multiple lines of Javadoc text are written here,
 		 * wrapped normally...
 		 */
		public int method(String p1) { ... }
单行形式：

		/** An especially short bit of Javadoc. */
2. Javadoc标记  
标准的Javadoc标记按以下顺序出现：@param, @return, @throws, @deprecated, 前面这4种标记如果出现，描述都不能为空。 当描述无法在一行中容纳，连续行需要至少再缩进4个空格。