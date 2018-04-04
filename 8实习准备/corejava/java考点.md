# 静态、实例、局部变量

## 静态变量

又称类变量，可以在类不初始化是直接用类名调用。随着类的加载而存在，随着类的消失而消失。存储在方法区中。因为静态变量被所有的对象共享，所以不是线程安全的。

## 实例变量

又称成员变量，在类中定义，在整个类中可以访问。随着对象的建立而存在，随着对象的消失而消失。存储在对象所在的堆内存中。实例变量可以不初始化，系统会自动给它赋值，比如数字为0，boolean为假，对象引用为null。实例变量虽然是对象私有的，但是如果**只存在一个此对象的实例**，在多线程环境下也是非安全的；如果**多个线程访问的是不同的对象实例**，那么多线程下就是线程安全的。

## 局部变量

定义在方法中或者方法的参数列表。存储在栈内存中，超出作用域自动释放空间。局部变量必须要初始化之后才可以使用。每个线程执行时会把局部变量放在自己工作内存的栈中，线程间互不影响，是线程安全的。

# 关键字

## static

static主要有四种用法：

1. 用来**修饰成员变量**，将其变为**类的成员**，从而实现所有对象对于该成员的共享；
2. 用来**修饰成员方法**，将其变为类方法，可以直接使用**类名.方法名**的方式调用，常用于工具类；
3. **静态语句块**，将多个类成员放在一起初始化，使得程序更加规整，其中理解对象的初始化过程非常关键；
4. **静态导包**，将类的方法直接导入到当前类中，从而直接使用**方法名**即可调用类方法，更加方便。


### 1 修饰成员变量

static最常用的功能就是修饰类的属性和方法，让他们成为类的[成员]()属性和方法，我们通常将用static修饰的成员称为类成员或者静态成员，意思是static修饰的变量就不是由对象管理了，而是那个类管理，多个对象对应同一个变量，一个对象修改了这个变量，其他对象都会受影响。

```java
public class Person{
    String name;
    int age;
    public String toString() {
        return "Name:" + name + ", Age:" + age;
    }
}
```

![52282119504](D:\a_my\OneDrive\1研究生同步\1学习记录\20180114-分布式学习计划\8实习准备\corejava\1522821195040.png)

p1和p2两个变量引用的对象分别存储在内存中堆区域的不同地址中，所以他们之间相互不会干扰。两个Person对象的方法实际上只是指向了同一个方法定义。这个方法定义是位于内存中的一块不变区域（由jvm划分），我们暂称它为静态存储区。这一块存储区不仅存放了方法的定义，实际上从更大的角度而言，它存放的是各种类的定义，当我们通过new来生成对象时，会根据这里定义的类的定义去创建对象。多个对象仅会对应同一个方法，这里有一个让我们充分信服的理由，那就是不管多少的对象，他们的方法总是相同的，尽管最后的输出会有所不同，但是方法总是会按照我们预想的结果去操作，即不同的对象去调用同一个方法，结果会不尽相同。

```java
public class Person{
    String name;
    static int age;
    public String toString() {
        return "Name:" + name + ", Age:" + age;
    }
}
```

![52282135274](D:\a_my\OneDrive\1研究生同步\1学习记录\20180114-分布式学习计划\8实习准备\corejava\1522821352745.png)

给age加上了static关键字之后，age交给了Person类管理，对象不再拥有age属性。

### 2 修饰成员方法

相比于修饰成员属性，修饰成员方法对于数据的存储上面并没有多大的变化，因为我们从上面可以看出，方法本来就是存放在类的定义当中的。static修饰成员方法最大的作用，就是可以使用"类名.方法名"的方式操作方法，避免了先要new出对象的繁琐和资源消耗。在一个static修饰的方法中不能使用非static修饰的成员变量和方法。

静态方法在类加载的时候就存在，它不依赖于任何实例，所以静态方法必须要实现，也就是说abstract方法不可以同时是静态方法。

### 3 静态块

```java
class Book{
    public Book(String msg) {
        System.out.println(msg);
    }
}

public class Person {

    Book book1 = new Book("book1成员变量初始化");
    static Book book2 = new Book("static成员book2成员变量初始化");
    
    public Person(String msg) {
        System.out.println(msg);
    }
    
    Book book3 = new Book("book3成员变量初始化");
    static Book book4 = new Book("static成员book4成员变量初始化");
    
    public static void funStatic() {
        System.out.println("static修饰的funStatic方法");
    }
    
    public static void main(String[] args) {
        Person.funStatic();
        System.out.println("****************");
        Person p1 = new Person("p1初始化");
    }
    /**Output
     * static成员book2成员变量初始化
     * static成员book4成员变量初始化
     * static修饰的funStatic方法
     * ***************
     * book1成员变量初始化
     * book3成员变量初始化
     * p1初始化
     */
}
```

#### 初始化顺序

在存在继承时，初始化的顺序为：

1. 父类（静态变量、静态语句块块）
2. 子类（静态变量、静态语句块）
3. 父类（实例变量、普通语句块）
4. 父类（构造函数）
5. 子类（实例变量、普通语句块）
6. 子类（构造函数）

```java
public class SuperClass {
    static int i = 1;
    static {
        System.out.println("superclass: " + i);
    }
    public SuperClass() {
        System.out.println("superclass constructor");
    }
}

public class SubClass extends SuperClass {
    static int i = 2;
    static{
        System.out.println("subclass: " + i);
    }

    public SubClass() {
        System.out.println("subclass constructor");
    }
    public static void main(String[] args){
        System.out.println("main");
        SubClass b = new SubClass();
    }
}
/*
 * output
superclass: 1 //父类的静态变量和静态语句块先初始化并执行
subclass: 2 //子类的静态变量和静态语句块先初始化并执行
main //main方法语句执行
superclass constructor //子类构造方法，先调用父类构造方法
subclass constructor //子类构造方法
 */
```







### 4 静态导包

```java
import static com.**.Helper.
```

static导包之后，Helper类下面所有的static方法都可以直接调用，而不需要用类名.方法名的方式调用。

## final

### 1 修饰类

用final修饰一个类时，表明这个类不能被继承。也就是说，如果一个类你永远不会让他被继承，就可以用final进行修饰。final类中的成员变量可以根据需要设为final，但是要注意final类中的所有**成员方法都会被隐式地指定为final**方法。

### 2 修饰方法

final修饰方法可以把方法锁定，以防任何继承类修改它的含义，想明确禁止该方法在子类中被覆盖的情况下才将方法设置为final。类的private方法会隐式被指定为final。

如果在子类中定义的方法和基类中的一个 private 方法签名相同，此时子类的方法不是覆盖基类方法，而是重载了。

### 3 修饰变量

对于一个final变量，如果是**基本数据类型**的变量，则其数值一旦在初始化之后便不能更改；如果是**引用类型**的变量，则在对其初始化之后便不能再让其指向另一个对象，但是该对象中的成员变量还是可以被修改的。

```java
final ArrayList<Integer> list = new ArrayList<>();
list = new ArrayList<>(); // Cannot assign a value to final variable 
list.add(1)
```

```java
final String str1 = "ja";
String str2 = "ja";
String str3 = str1 + "va";
String str4 = str2 + "va";
String str5 = "java";
System.out.println(str3 == str5);//true
System.out.println("ja" + "va" == str5);//true
System.out.println(str4 == str5);//false
```

当final变量是基本数据类型以及String类型时，如果在**编译期间能知道它的确切值**（这个是前提，如果final String str1 = getja()这种方式得到的，结果就不一样了），则编译器会把它当做**编译期常量使用**（和c中宏替换差不多一个意思），用到该final变量的地方，相当于直接访问的这个常量，不需要在运行时确定。而不是final修饰的修饰的str2，在访问的时候要通过链接来进行。

## volatile

synchronized除了互斥的作用，还具有可见性的作用。是指在一个线程中修改变量的值以后，在其他线程中能够看到这个值。synchronized保证了synchronized块中的变量的可见性，而volatile保证了所修饰变量的可见性。因为volatile只是保证同一个变量在多线程中的可见性，所以它更多是用于修饰作为开关状态的变量。

```java
int i; public int getI(){return i};
volatile int j; public int getJ(){return j};
int k; public synchronized int getK(){return k};
```

getI调用获取的是**当前线程中的副本**，这个值不一定是最新的值。j是volatile修饰的，对于JVM来说这个变量不会有线程的本地副本，只会放在主存中，所以得到的一定是最新的。getK是synchronized修饰的，保证线程的本地副本和主存的同步，所以也会得到最新的值。



# 包装类型

```java
Integer a = new Integer(2);
Integer b = 2; //将2自动装箱成Integer
int c = 2;
System.out.println(a == b); //false,两个对象地址不同
System.out.println(a == c); //true,a自动拆箱得到int型值

Integer d = 2; //自动装箱，调用的是Integer.valueOf()方法
Integer e = 150, f = 150;
System.out.println(b == d); // true
System.out.println(e == f); // false

Integer g = new Integer(2);
System.out.println(a == g); // false
Integer h = Integer.valueOf(2);
Integer i = Integer.valueOf(2);
System.out.println(h == i); // true
```

两个new Integer(2)对象判断不相等，但是两个Integer.valueOf(2)判断是相等的

```java
public static Integer valueOf(int i) {
    final int offset = 128;
    if (i >= -128 && i <= 127) {
        return IntegerCache.cache[i + offset];
    }
    return new Integer(i);
}
```

valueOf() 方法会先判断值是否在缓存池中，如果在的话就直接使用缓存池的内容。

基本类型中使用缓冲池的值有：

- boolean values true and false
- all byte values
- short values between -128 and 127
- int values between -128 and 127
- char in the range \u0000 to \u007F


# switch

switch(expr)中，expr只能是byte、short、char、int、enum、String。

 swicth 的设计初衷是为那些只需要对少数的几个值进行等值判断，如果值过于复杂，那么还是用 if 比较合适。所以switch不支持long、float等类型。



# 枚举类



# 存储区

栈的位置仅次于CPU中的寄存器，所以[存取]()速度很快。但是栈中的数据大小与生存周期必须是确定的，缺乏灵活性，此外栈的数据可以共享。java中所有的基本数据类型和引用类型都是在栈中。

堆可以动态的分配内存大小，所以存取较慢，垃圾回收器会自动收走不再使用的数据。

java中有两种数据类型，基本类型（8种：char、byte、short、int、long、float、double、boolean），比如定义int a = 3，a是一个指向int类型的引用，指向3这个字面值。这些字面值数据大小可知，生存期可知，所以都存放在栈中。当我们定义int a = 3, b = 3时，编译器首先在栈中查找是否有字面值为3的地址，如果有，将a指向这个地址，如果没有会在栈中开辟一个地址。同样b便会指向字面值为3的地址（这就是为什么说栈中数据共享）。但是我们执行a++之后，a会指向字面值为4的地址，具体过程和上面一样，先在栈中查找，如果没有找到会在栈中创建。

通过字面值的引用修改其值，不会导致另一个指向此字面值的引用的值改变（上面解释过）。但是如果两个类对象的引用同时指向同一个对象，一个对象引用变量修改了这个对象的内部状态，另一个对象会得到修改后的状态。

另一种是包装类数据，比如Integer、String、Double等将相应的基本数据类型包装起来的类，这些类数据都存在堆中。所以new语句创建的数据对象都存放在堆中。



# String

```java
String str = "abc";
```

上面这个语句执行的过程：

1.     定义一个名为str的String类对象的引用，引用是在栈上的；
2.     在栈中查找有没有值为"abc"的地址，如果没有，在栈中开辟一个存放值为"abc"的地址，接着创建了一个新的String类型的对象o，并将o的字符串值指向栈中"abc"的地址，在栈中这个地址旁边记下这个引用的对象o。如果已经有了值为"abc"的地址，则直接查找对象o，并返回o的地址；
3.     **将str指向对象o的地址**。（需要注意的是str没有指向栈中存放"abc"的地址，而是指向了一个对象o，而o是指向"abc"的）


```java
String str1 = "abc"
String str2 = "abc"
System.out.println(str1 == str2); //true

String str1 = "abc"
String str2 = new String("abc")
System.out.println(str1 == str2); //false,new会在堆中创建的对象，所以两个地址肯定不一样。

System.out.println(str1.intern() == str2.intern()) //true
```

我们在使用诸如`String str = "abc"；`的格式定义类时，总是想当然地认为，我们创建了String类的对象str。但是对象可能并没有被创建（String有一个string pool，如果string pool中存在的变量就不会再创建新的了），唯一可以肯定的是，指向 String类的引用被创建了。至于这个引用到底是否指向了一个新的对象，必须根据上下文来考虑，除非你通过new()方法来显要地创建一个新的对象。因此，更为准确的说法是，我们创建了一个指向String类的对象的引用变量str，这个对象引用变量指向了某个值为"abc"的String类。

使用`String str = "abc"；`的方式，可以在一定程度上提高程序的运行速度，因为JVM会自动根据栈中数据的实际情况来决定是否有必要创建新对象。而对于`String str = new String("abc")；`的代码，则一概在堆中创建新对象，而不管其字符串值是否相等，是否有必要创建新对象，从而加重了程序的负担。

str调用intern()方法后，JVM 就会在当前类的常量池中查找是否存在与str等值的String，若存在则直接返回常量池中相应String的引用；若不存在，则会在常量池中创建一个等值的String，然后返回这个String在常量池中的引用。因此，只要是等值的String对象，使用intern()方法返回的都是常量池中同一个String引用，所以，这些等值的String对象通过intern()后使用==是可以匹配的。