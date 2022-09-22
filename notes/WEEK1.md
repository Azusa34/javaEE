# WEEK 1
## 1、
## 2、Java8新特性
1. **Lambda 表达式**：Lambda 允许把函数作为一个方法的参数（函数作为参数传递到方法中）。
语法表达式：
```
(parameters) -> expression
或
(parameters) ->{ statements; }
```
主要特征：
- 可选类型声明：不需要声明参数类型，编译器可以统一识别参数值。
- 可选的参数圆括号：一个参数无需定义圆括号，但多个参数需要定义圆括号。
- 可选的大括号：如果主体包含了一个语句，就不需要使用大括号。
- 可选的返回关键字：如果主体只有一个表达式返回值则编译器会自动返回值，大括号需要指定表达式返回了一个数值。
	
2. **方法引用**：方法引用使得开发者可以直接引用现存的方法、Java类的构造方法或者实例对象。
- 构造器引用：它的语法是`Class::new`，或者更一般的`Class< T >::new`实例如下：
```
final Car car = Car.create( Car::new );
final List< Car > cars = Arrays.asList( car );
```
- 静态方法引用：它的语法是`Class::static_method`，实例如下：
```
cars.forEach( Car::collide );
```
- 特定类的任意对象的方法引用：它的语法是`Class::method`实例如下：
```
cars.forEach( Car::repair );
```
- 特定对象的方法引用：它的语法是`instance::method`实例如下：
```
final Car police = Car.create( Car::new );
cars.forEach( police::follow );
```
3. **新的函数式接口**

函数式接口可以规定函数的参数类型和返回值类型，让其更好地支持 lambda 表达式。

JDK 1.8 之前已有的函数式接口:

- java.lang.Runnable
- java.util.concurrent.Callable
- java.security.PrivilegedAction
- java.util.Comparator
- java.io.FileFilter
- java.nio.file.PathMatcher
- java.lang.reflect.InvocationHandler
- java.beans.PropertyChangeListener
- java.awt.event.ActionListener
- javax.swing.event.ChangeListener

JDK 1.8 新增加的函数接口：

- java.util.function

java.util.function 包含了很多类，用来支持 Java的函数式编程，例如 `BiConsumer<T,U>` 代表了一个接受两个输入参数的操作，并且不返回任何结果。

4. **接口的默认方法**

当需要修改接口时候，需要修改全部实现该接口的类，目前的 java 8 之前的集合框架没有 foreach 方法，通常能想到的解决办法是在JDK里给相关的接口添加新的方法及实现。然而对于已经发布的版本，没法在不影响已有的实现的同时给接口添加新方法。所以引进的默认方法可以为了解决接口的修改与现有的实现不兼容的问题。

默认方法语法格式如下：

```java
public interface Vehicle {
	default void print() {
		System.out.println("我是一辆车!");
	}
}
```

但有时候一个类实现了多个接口，且这些接口有相同的默认方法：

```java
public interface Vehicle {
  default void print() {
    System.out.println("我是一辆车!");
  }
}

public interface FourWheeler {
  default void print() {
    System.out.println("我是一辆四轮车!");
  }
}
```

第一个解决方案是创建自己的默认方法，来覆盖重写接口的默认方法：

```java
public class Car implements Vehicle, FourWheeler {
  default void print() {
    System.out.println("我是一辆四轮汽车!");
  }
}
```

第二种解决方案可以使用 super 来调用指定接口的默认方法：

```java
public class Car implements Vehicle, FourWheeler {
	public void print() {
    Vehicle.super.print();
  }
}
```