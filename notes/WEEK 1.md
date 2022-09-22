# WEEK 1
## 1、
## 2、Java8新特性
1. Lambda 表达式：Lambda 允许把函数作为一个方法的参数（函数作为参数传递到方法中）。
语法表达式：
   `(parameters) -> expression
或
(parameters) ->{ statements; }`
   ```
   //遍历输出：e为参数，类型由编译器推理得到
   Arrays.asList( "a", "b", "d" ).forEach( e -> System.out.println( e ) );
   //排序：list作为参数并接收返回值，返回值类型由编译器推理得到
   Collections.sort(list,(i1,i2)-> i2.compareTo(i1));
	
2. 方法引用：方法引用使得开发者可以直接引用现存的方法、Java类的构造方法或者实例对象。
      
       //示例类
       public static class Car {
           public static Car create( final Supplier< Car > supplier ) {
               return supplier.get();
           }
           public static void collide( final Car car ) {
               System.out.println( "Collided " + car.toString() );
           }
           public void follow( final Car another ) {
               System.out.println( "Following the " + another.toString() );
           }
           public void repair() {
               System.out.println( "Repaired " + this.toString() );
           }
       }
- 构造函数引用： </br>
		`List< Car > cars = Arrays.asList( Car :: new ); `
- 静态方法引用：  </br>
		`cars.forEach( Car::collide );     `
- 成员方法引用：
     ```
		//不接收参数
		cars.forEach( Car::repair );
- 实例对象的方法引用： 
     ```
		final Car car = Car.create( Car::new );
		//接收一个Car类型的参数
		cars.forEach( car::follow );