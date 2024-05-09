

<span style='color:rgb(238, 5, 43);font-size:18px'>红色重点样式：</span><span style='color:rgb(238, 5, 43);font-size:18px'></span>

## 常见用法

**防止高DPI导致窗体模糊**

1. **在解决方案中创建新的应用程序清单**

![image-20240427161635419](C:\Users\LHX\AppData\Roaming\Typora\typora-user-images\image-20240427161635419.png)

2. **将标签对**`<application>`**取消注释**

![image-20240427161719547](C:\Users\LHX\AppData\Roaming\Typora\typora-user-images\image-20240427161719547.png)

**禁止缩放**

```C#
this.FormBorderStyle = FormBorderStyle.FixedDialog;
this.MaximizeBox = false;
this.MinimizeBox = false;
```



## 数组

### 一维数组

数组存储的是n个相同的数据类型的元素。

声明语法：`int[] a = new int[10]`，定义时必须指定长度。

可以有不规则的二维数组，行列可以不等

类型：

* 整型
* 浮点数
* 字符
* 字符串

初始化方法1：

```C#
int[ ] a = new int[3];
a[0] = 1;
a[1] = 2;
```

方式2：（长度必须和赋值长度相同）

```C#
int[ ] c = new int[3]{1,2,3};
```

方式3：

```C#
int [ ] c = {1,2,3};
```

### 二维数组

语法：

`int [m,n] 数组名`，或`int[,] a = {{},{},{}}`这是规则的二维数组

`int[m][n] 数组名`，这是不规则的。

使用方法：`Console.Write(a[])`

初始化：

```C#
int[][] a = new int[2][2];
```

或

```C#
int [][] a = new int[2][];
a[0] = new int[3];
a[1] = new int[4];
```

不规则初始化：

```C#
```



# C#面向对象程序设计

## 构造函数

**定义：对象最初进行实例化的时期的初始化过程。**

* 创建对象时将调用构造函数，每个类都有构造函数，即使没有声明它，编译器也会自动提供一个默认的构造函数。
* **主要作用：为对象分配内存空间，完成初始化操作。**

**在C#中，类的构造函数遵循以下规定：**

* 构造函数名称与类名相同
* 一个类可以有多个构造函数
* 如果类中没有显示的定义构造函数，编译器会自动生成一个默认的构造函数，并用默认值初始化对象的字段
* 如果类中只有带参数的构造函数，则没有默认构造函数
* 构造函数没有返回值，也不能使用void关键字
* 一般情况下，构造函数总是public，但也可是其他
* 构造函数也可以通过关键字this调用另一个构造函数。
* 构造函数可以通过初始值设定项来调用基类的构造函数

> [!note]
>
> ```C#
> class Program{
>   public static void Main(String [ ] args){
>     Vechile v = new Vehicle( 20 );  //因为在Vechile中定义了构造函数，所以这里可以直接传参。
>   }
> }
> 
> class Vechile
> {
>     public int Weight;
>     public int Height;
>     public Vehicle()
>     {
>         Weight = 10;
>     }
> 
>     public Vehicle(int _Height)
>     {
>         Height = _Height;
>     }
> 
> }
> ```
>
> 在上面的代码中，第一个构造函数就是我们定义的没有带参数的构造函数，它给字段Weight设置了初始值为10，第二个构造函数是带参数的，需要我们手动传入参数。

## 类的属性

> [!tip]
>
> ***类还有一种特殊的成员称为属性。它既可以被视为一种成员变量，也可以看作一种成员方法，实际上是对成员变量的一种拓展。对用户而言，属性是一种 “ 成员变量 ” ，但这种 “ 成员变量 ” 不是真正存在的，而是关联到一个或若干个成员变量；对程序员而言，属性是一种能够读写成员变量的特殊方法。***

**定义语法：**

```C#
数据类型  属性名
{
  get { return 表达式1; }
  set { 表达式2; }
}
```

在上面的代码中，表达式2通常包含特殊变量value。

> [!note]
>
> 1. **get语句和set语句称为属性访问器，get的返回值类型与属性类型相同 或 隐式转换为属性类型。set访问器等价于一个具有隐含参数的value方法。**
> 2. **给属性赋值时使用set访问器，使用value设置属性值。获取属性值时使用get访问器，get通过return返回属性值。**
> 3. **在属性定义中，如果既有get，又有set，表示 可读 / 写 属性；如果只有get访问器，表示只读属性；如果只有set访问器，表示只写属性。**

**范例：**

```C#
public class A
{
    public int a = 10;
    public int age;
    public int Age
    {
        get { return age; }
        set { age = value; }
    }
    public void Write()
    {
        Console.WriteLine(age);
    }
}
```

在上面的代码中，演示了如何创建类的属性，有一个类 A ，属性中设置了 `set`与`get`，代表可读也可写，`set`中有一个特殊的变量`value`，可以接收用户录入的值。

**范例：（使用类的属性）**

```C#
public static void Main(string[] args)
{
    int age = 3;
    A a = new A();
    a.Age = age;
    int k = a.Age;
    Console.WriteLine(k);
    a.Write();
}
```

在`Main`方法中，定义了一个变量`age`，同时实例化了类`A`，在使用`对象.属性 = 变量`的方法，就可以对类中的属性进行赋值操作。同时因为类`A`中设置了`get`，所以我们可以使用另一个变量`k`来接收类`A`属性中返回的值。

****

## 封装、继承、重载和多态

### 封装

**封装的概念：就是用一个框架把数据和代码组合在一起，形成一个对象。外部不能直接访问对象内部的数据，能见到的知识提供给外面访问的公共操作（称为接口）**

> [!tip]
>
> ***在C#中，类是支持对象封装的 ==工具==，而对象则是封装的 ==基本单元==。封装的对象之间进行通信叫做 ==消息传递==。消息是面向对象发出的服务请求，是面向对象系统中对象之间交互的途径。***

### 继承

**继承的概念：继承是面向对象编程技术的一块基石，通过它可以创建分等级层次的类。继承也是父类和子类之间共享数据的方法和机制，通过把父类称为基类，子类称为派生类。一个类可以有任意数目的派生类，从基类派生出的类还可以再派生，通过继承相互练习的类就构成了类的树。**

> [!tip]
>
> ***派生类会从其基类中继承得到所有的操作、属性、特征、事件，而基类中的实例构造函数、析构函数则不会被继承。也就是说，继承是指一个派生类或子类能够直接获得基类或父类已有的属性和方法，不需要重复定义。继承具有传递性，但 C# 只支持单继承，也就是说一个类最多允许从一个父类中派生，即只能有一个父类，但一个父类可以派生出多个子类。***

**语法：**

```C#
class 基类名{
  成员;
}
class 派生类名 : 基类名{
  成员;
}
```

> [!note]
>
> 派生类可以继承基类中的<span style='color:rgb(238, 5, 43);font-size:18px'> 保护成员 </span>和 <span style='color:rgb(238, 5, 43);font-size:18px'>公有成员</span>，但不能继承 <span style='color:rgb(238, 5, 43);font-size:18px'>私有成员</span>。被继承后，成员的性质没有发生改变。

如果在派生类中定义了与基类成员同名的新成员，<span style='color:rgb(238, 5, 43);font-size:18px'>则需要使用关键字base才能实现对基类中同名成员的访问。</span>

**范例：**

```C#
internal class Program
{
    public static void Main(string[] args)
    {
        B b = new B();
        b.test();
    }

    public class A
    {
        public int a = 10;
    }

    public class B : A
    {
        private int a = 4;
        public void test()
        {
            Console.WriteLine("基类中的a={0},派生类类中的a={1}",base.a,a);
        }
    }
}
```

![image-20240226234501493](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240226234501493.png)

> [!note]
>
> ***如果基类中定义了带参的一个或多个构造函数，则派生类中也必须定义至少一个构造函数，且派生类中的构造函数必须通过 base( ) 函数调用基类中的某一个构造函数。***

### 重载

**定义：重载是指成员方法的重新加载，具体来说，就是定义具有相同函数名，但函数参数个数或参数类型不同的多个函数实现版本。**

> [!tip]
>
> ***<span style='color:rgb(238, 5, 43);font-size:18px'>重载</span> 简单理解就是：函数名相同，形参有差别，个数不同或类型不同。方法的重载（Overloading）与方法的返回值没有直接关系。方法重载是基于方法名和参数列表（参数的数量、类型或顺序）的，而不是基于方法的返回类型。即使两个重载方法具有相同的返回类型，只要它们的参数列表不同，它们就可以共存于同一个类中。***

==方法的重载和方法的返回值无关，只要函数名相同，形参不同就可以构成重载关系。==

**范例：**

```C#
public class Calculator
{
    // 第一个Add方法，没有参数，返回值为void
    public void Add()
    {
        Console.WriteLine("No parameters provided.");
    }

    // 第二个Add方法，有两个int类型的参数，返回值为int
    public int Add(int a, int b)
    {
        return a + b;
    }

    // 第三个Add方法，有两个参数，第一个参数为int类型，第二个为double类型，返回值为double
    public double Add(int a, double b)
    {
        return a + b;
    }
}
```

**满足重载的三个条件：**

* 在同一个类中
* 方法名相同
* 形参列表不同

### 多态

**概念：多态是指同一个消息或操作作用于不同的对象，可以有不同的解释，产生不同的执行结果。**

**多态有两种：**

* 静态多态
* 动态多态

**范例：**

> [!important]
>
> ```C#
> public class ClassExtension  //Extension意为 拓展，延伸。
>     //类的封装、继承、重载、多态。
> {
>     public static void Main(string[] args)
>     {
>         Animal animal = new Animal();
>         Animal cat = new Cat();
>         Animal dog = new Dog();
>         animal.MakeSound();
>         cat.MakeSound();
>         dog.MakeSound();
>     }
>     class Animal
>     {
>         public virtual void MakeSound()
>         {
>             Console.WriteLine("Animal Parent");
>         }
>     }
>     class Cat : Animal
>     {
>         public override void MakeSound()
>         {
>             Console.WriteLine("Cat Sound");
>         }
>     }class Dog : Animal
>     {
>         public override void MakeSound()
>         {
>             Console.WriteLine("Dog Sound");
>         }
>     }
> }
> ```
>
> > [!note]
> >
> > 在上面代码中，有一个基类`Animal`，在这个类中定义了一个虚方法`MakeSound`，虚方法允许子类对这个方法进行方法重写以实现多态。子类`Cat`和`Dog`中都加上了`override`关键字，表示对子类中的虚方法进行重写。在`Main`方法实例化对象的时候，`new Cat()`和`new Dog()`分别创建了两个实例，但这两个实例都是`Animal`类型的，从这里就体现出了多态性。

****

## 接口及其实现

> [!tip]
>
> ***接口要先声明，然后通过继承来实现***

**接口声明格式：**

```C#
修饰符 interface 接口名称 : 继承的接口列表{
  接口内容;
}
```

**范例：**

```C#
public interface Interface
//定义一个接口
{
    void payIn(decimal amount);
    bool Withdraw(decimal amonut);

    decimal Balance
    {
        get;
    }
}
```

在上面的代码中，定义了一个接口，有一个`payIn`方法和一个`Withdraw`方法，和一个`Balance`属性。

> [!note]
>
> **接口定义通常遵循以下规则：**
>
> * **接口名是任意合法标识符，建议以**`I`**开头**。
> * **声明的接口可以继承一个基类和多个其他接口**
> * 接口修饰符可以使用`new`、`public`、`protected`、`internal`、`private`
> * **接口成员前不允许有修饰符，默认都为**`public`
> * **接口成员可以分为四类：方法、属性、事件和所引起，而不能包含成员变量**
> * **不能在声明接口的同时编写接口成员的实现代码**

**定义接口的语法如下：**

```C#
interface 接口名{
  接口成员;
}
```

这里的接口成员包括：

* 属性
* 方法
* 事件

> [!note]
>
> ***并且使用***`interface`***关键字定义接口时，只能声明接口的成员，不能对接口的成员的具体操作进行实现。***

**如果要对接口成员的具体操作进行实现，需要用到类的继承：**

我们先定义一个接口，这个接口中包含一个`CreateShape`方法：

```C#
interface IShape{
  void CreateShape( );
}
```

然后我们创建一个类继承这个接口：

```C#
public class Re : IShape{
  public void CreateShape( ){
    Console.WriteLine( " I create a Re shape " );
  }
}
```

这样就完成了对接口中方法的实现。

> [!tip]
>
> ***当我们要使用接口的时候，需要进行实例化操作***

**使用接口方法如下：**

```C#
class Program{
  public static void Main( string [ ] args){
    IShape s = new Re( );
    s.CreateShape( );
  }
  interface IShape{
  	void CreateShape( );
	}
  public class Re : IShape{
    public void CreateShape( ){
      Console.WriteLine( " I create a Re shape " );
    }
  }
}
```

上面的代码演示了如何使用接口。当我们要使用接口的时候，<span style='color:rgb(238, 5, 43);font-size:18px'>我们需要创建实现接口成员方法的类的实例，保存到接口类型的变量中</span>，上面的代码中，实现了接口成员的类是 `Re` ，接口是 `IShape` ，所以定创建实例的语法如下： `IShape s = new Re();`。`new Re()`创建了类的实例，`IShape s`则创建了一个`IShape`类型的变量，这就是接口的使用方法。

> [!note]
>
> ***如果有两个接口，每个接口中都各有一个方法，并且一个接口继承自另一个接口，这种情况下派生接口就继承了父接口的所有成员，所以我们要定义一个类，继承自子接口，然后在其中实现成员的操作。***

**范例：**

```C#
public class Interface
{
    public static void Main(string[] args)
    {
        ISp2 s = new Iss2();
        s.AnotherCreateShape();
        s.CreateShape();
    }

    interface ISp1
    {
        void CreateShape();
    }

    interface ISp2 : ISp1
    {
        void AnotherCreateShape();
    }

    public class Iss2 : ISp2
    {
        public void CreateShape()
        {
            Console.WriteLine("I create one Shape");
        }

        public void AnotherCreateShape()
        {
            Console.WriteLine("I create another shape");
        }
    }
}
```

上面的代码中，`ISp1`是一个父接口，`ISp2`是一个子接口，==当我们使用到了接口继承的操作时，我们要将父接口与子接口所有的成员都进行具体操作的实现==。<span style='color:rgb(238, 5, 43);font-size:18px'>由于继承的关系，子接口中继承了父接口所有的成员，所以我们需要定义一个类继承自子接口</span>，在这个类中实现所有成员的操作。

***

## 委托

### 定义委托

> [!tip]
>
> ***C# 中的委托（Delegate）类似于 C 或 C++ 中函数的指针。委托（Delegate） 是存有对某个方法的引用的一种引用类型变量。引用可在运行时被改变。***
>
> ***委托（Delegate）特别用于实现事件和回调方法。所有的委托（Delegate）都派生自 System.Delegate 类。***

**定义委托的语法：**`属性 修饰符 delegate 返回类型 委托类型名 (参数列表)`

**范例：**

```C#
public delegate int MyDelegate( string s );
```

上面的委托可被用于引用任何一个带有一个单一的 *string* 参数的方法，并返回一个 *int* 类型变量。

> [!note]
>
> ***参数列表和返回类型共同决定了委托类型能够关联的一组方法。委托没有具体的实现体，它能够带包什么样的方法由它的返回值类型和参数列表决定。***

### 实例化

> [!tip]
>
> ***委托类型名和类名一样，都用于创建对象。用委托类型名实例化的对象就是委托对象。***

**范例：**

```C#
public delegate void MyDelegate( );  //声明了一个委托，可以委托一个没有返回值，没有参数的方法。

class A
{
    public static void test( )
    {
        Console.WriteLine("Test the Delegate");
    }
}
class Program{
  public static void Main( string [ ] args ){
    Mydelegate m = new MyDelegate( A.test );  //委托实例化，选择了要委托的方法。
    m( ); //Test the Delegat
  }
}
```

上面代码中，第1行声明了一个委托，可以委托一个没有返回值，没有参数的方法。在`Main`方法中，实例化了创建的委托，由于类`A`中，`test`方法是静态的，==所以我们在委托的时候可以直接使用类名来访问==。最后使用实例化的对象`m`来委托`A.test()`方法。

> [!caution]
>
> ***能被委托的方法必须是在运行时为内存中已经能确定的方法，如静态方法，对象的方法，而类的非静态方法（还没有实例化）是不能委托的。***

### 委托的多播

> [!tip]
>
> ***委托的多播直白一点说就是将几个委托组合在一起。***

* 委托对象可使用 "+" 运算符进行合并。一个合并委托调用它所合并的两个委托。只有相同类型的委托可被合并。"-" 运算符可用于从合并的委托中移除组件委托。

* 使用委托的这个有用的特点，您可以创建一个委托被调用时要调用的方法的调用列表。这被称为委托的 多播（multicasting），也叫组播。

**范例：**

首先定义了一个类`A`，类中有两个方法

```C#
public class A
{
    public static void test1()
    {
        Console.WriteLine("Test1");
    }

    public static void test2()
    {
        Console.WriteLine("Test2");
    }
}
```

然后我们声明一个委托：

```C#
public delegate void MyDelegate();
```

接着在`Main`方法中使用多播：

```C#
public static void Main(string[] args)
{
    int s = new int();
    MyDelegate m;
    MyDelegate m1 = new MyDelegate(A.test1);
    MyDelegate m2 = new MyDelegate(A.test2);
    m = m1 + m2;
    m();
}
```

上面代码中，我们先创建了一个`MyDelegate`类型的变量`m`但是它没有任何指向。接着我们实例化了两个委托，`A.test1`和`A.test2`分别赋值给了`m1`和`m2`，然后使用`+`运算符==将两个委托合并为一个委托==，==这就是多播。==

## 事件

> [!note]
>
> ***事件是基于委托的。***
>
> ***事件是操作发生时允许执行特定应用程序的代码机制。***
>
> ***基本上说是一个用户操作，如按键、点击、鼠标移动等等，或者是一些提示信息，如系统生成的通知。应用程序需要在事件发生时响应事件。例如，中断。***
>
> ***C# 中使用事件机制实现线程间的通信。***

事件分类：

* 事前事件
* 事后事件

==类或对象可以通过事件向其他类或对象通知发生的相关事件。==

***发送（或引发）事件的类称为 “ 发布器 ” ，接收（或处理）事件的类称为 “ 订阅器 ” 。***

<span style='color:rgb(238, 5, 43);font-size:18px'>**发布器（publisher）** </span>是一个包含事件和委托定义的对象。事件和委托之间的联系也定义在这个对象中。发布器（publisher）类的对象调用这个事件，并通知其他的对象。

<span style='color:rgb(238, 5, 43);font-size:18px'>**订阅器（subscriber）**</span> 是一个接受事件并提供事件处理程序的对象。在发布器（publisher）类中的委托调用订阅器（subscriber）类中的方法（事件处理程序）。

定义事件语法：

```C#
访问修饰符  event  委托名  事件名;
```

在类的内部声明事件，首先必须声明该事件的委托类型：

```C#
public delegate void Mydelegate( );
```

然后使用上声明委托类型的事件：

```C#
public event MyDelegate MyEvent;
```

---

# 访问数据库

## 创建连接

**导入命名空间**

```C#
Using System.data
Using System.Data.SqlClient
```

**创建字符串**

```C#
string strCon = "server= . ; database=BMS; uid = jjww ; pwd = jjww "
```

**实例化**

```C#
SqlConnection mCon = new SqlConnection(strCon)
```

**打开实例**

```C#
mCon.Open();
```

**关闭实例**

```C#
mCon.Close();
```

**状态检查**

```C#
mCon.State.ToString();
if(mCon.State.ToString().ToUpper() == 'OPEN') //判断是否为打开状态
{
    mCon.Close();
}
```

## **SqlCommnad对象**

> [!tip]
>
> **SqlCommand对象主要是用来执行Sql语句**

**返回有效记录值**

```C#
SqlCommand mCmd = new SqlCommand( strSql , mCon ); //实例化对象
int i =  ExcuteNonQuery( );                           //返回有效记录行数
```

## **DataReader对象**

> [!tip]
>
> **概述：DataReader是一个简单的数据集，主要从数据源中读取数据集。必须一致保持与数据库的连接。**

| 属性            | 说明                                    |
| --------------- | --------------------------------------- |
| HasRows         | 判断数据库中是否有数据                  |
| FieldCount      | 获取当前行数                            |
| RecordsAffected | 获取执行SQL语句所更改、添加或删除的行数 |

| 方法  | 说明                               |
| ----- | ---------------------------------- |
| Read  | 使DataReader对象前进到下一条记录   |
| Close | 关闭对象                           |
| Get   | 用来读取数据集的当前行的某一列数据 |

### DataReader使用方法

> [!note]
>
> **使用DataReader有两个步骤：**
>
> **1. 首先是先实现DataReader的查找数据逻辑，写在处理sql的文件中**
>
> **2. 在窗体文件中使用DataReader**

1. ***在SqlHelper文件中***

**创建连接**

```C#
SqlConnection mCon = new SqlConnection(strCon);
```

**创建Command对象**

```C#
SqlCommand Cmd = new SqlCommand(strSql, mCon);
```

**连接数据库：**`mCon.Open();`

**创建DataReader对象：**`SqlDataReader mRead = Cmd.ExcuteReader();`

> [!caution]
>
> ***这里要注意：***
>
> ***初始化DataReader对象的时候使用的是SqlCommand这个类的对象中的ExcuteReader( )方法***

**判断是否有数据**

`````C#
if( mRead.HasRows){
    //Code...
}
`````

**完整逻辑**

```C#
public bool reader(string strSql)//创建一个返回bool值的方法
{
    SqlConnection mCon = new SqlConnection(strCon);
    SqlCommand Cmd = new SqlCommand(strSql, mCon);
    mCon.Open();
    bool f = false;
    SqlDataReader mRead = Cmd.ExecuteReader();
    if (mRead.HasRows)
    {
        f = true;
    }
    else
    {
        f = false;
    }
    mCon.Close();
    mRead.Close();
    return f;
}
```

2. ***在窗体文件中***

**实例化SqlHelper类**

```C#
sqlHelper sh = new sqlHelper();
```

**获取需要判断的数据**

`````C#
string uName = this.tbUname.Text.Trim();
string upwd = this.tbPwd.Text.Trim();
`````

**写SQL**

```C#
string strSql = "Select * from table_1 where uName = '" + uName + "' and uPwd = '" + upwd + "'";
```

**使用DataReader**

```C#
if (sh.reader(strSql))
{
    MessageBox.Show("登录成功");
}
else
{
    MessageBox.Show("登录失败");
}
```

## DataSet和DataAdapter对象

> [!tip]
>
> - **DataSet实质上相当于在内存中的一个小型关系数据库。一个DataSet对象包含一组DataTable对象和DataRelation对象，其中每个DataTable对象都由DataColumn、DataRow、Constraint集合对象组成。他主要是通过DataAdapter检索数据，并填充到DataSet中。**
> - **DataAdapter对象是DataSet和数据库之间的桥梁，负责在DataSet和数据库之间传递数据。他使用Sql命令检索数据，并填充到DataSet和DataTable中。DataAdapter支持参数化查询。**

***简单来说，DataSet是一个数据容器，用于存储和操作数据，而DataAdapter是一个数据传输工具，用于在数据库和DataSet之间移动数据。***

### 使用方法

> [!note]
>
> **两个步骤：**
>
> - **在sqlHelper中：需要创建一个返回值为DataSet的方法。这个方法中不需要使用SqlCommand对象，要使用SqlDataAdapter对象和DataSet对象。**
> - **在窗体中，实例化一个DataSet对象，并且使用这个对象，接着给DataGripView控件填充数据。**

1. ***在SqlHelper中***

**实例化SqlConnection对象和SqlDataAdapter对象**

```C#
SqlConnection mCon = new SqlConnection(strCon);
SqlDataAdapter mDp = new SqlDataAdapter(strSql, mCon);
```

> [!note]
>
> **实例化SqlDataAdapter对象时，需要两个参数：**
>
> 1. **Sql字符串**
> 2. **连接字符串**

**实例化DataSet对象**

```C#
 DataSet mDs = new DataSet();
```

**连接数据库：**`mCon.Open()`

**填充DataSet对象：**`mDp.Fill(mDs)`

**关闭连接：**`mCon.Close()`

**完整逻辑：**

```C#
 public DataSet getDs(string strSql)
 {
     SqlConnection mCon = new SqlConnection(strCon);
     SqlDataAdapter mDp = new SqlDataAdapter(strSql, mCon);
     DataSet mDs = new DataSet();
     mCon.Open();
     mDp.Fill(mDs);
     mCon.Close() ;
     return mDs;
 }
```

> [!note]
>
> **在SqlHelper中，需要先创建一个返回值为DataSet的方法，然后在这个方法中实现具体的操作逻辑。**

2. ***在窗体文件中***

**实例化sqlHelper类**

```C#
sqlHelper sh = new sqlHelper( );
```

**创建DataSet对象**

~~~C#
DataSet mDs = new DataSet( );
~~~

**调用sh中的getDs方法**

```C#
mDs = sh.getDs( strSql );
```

**给DataGripView添加数据源**

```C#
this.dvgData.Datasource = mDs.Table[0];
```

> [!note]
>
> `this.dvgData.Datasource = mDs.Table[0];`
>
> ***这里的dvgData是我们创建的控件DataGripView，Datasource是数据源，Table[x]表示操作的是第x个DataTable***

**完整逻辑**

```C#
string strSql = /*Sql语句*/
DataSet Ds = new DataSet( );
Ds = sqls.getDs( strSql );		//这里的getDs是我们在sql类中自己定义的方法
this.dvgData1.DataSource = Ds.Table[0];   //dvgData1是DataGripView控件
```

## 总结

> [!note]
>
> <p style="color:red;font-size:20px">创建连接</p>
>
> **想要操作数据库，都要先定义连接：**
>
> 1. *定义连接的字符串：*`string strCon = ""server=.;database=BMS;uid=WFSQL;pwd=123456";"`
> 2. *创建*`SqlConnection`*对象*，*需要传入上面创建的*`strCon`*字符串*：
>
> ```C#
> SqlConnect sCon = new SqlConnect( strCon );
> ```

---

> [!note]
>
> <p style="font-size:20px;color:red">SqlCommand与SqlAdapter</p>
>
> `SqlCommand`和`SqlAdapter`都属于需要sql的操作，所以实例化对象的时候需要传入两个参数：
>
> 1. `strSql`：一个*<u>sql字符串</u>*
> 2. `sCon`：一个`SqlConnection`类型的对象
>
> **使用语法：**
>
> `SqlCommand Cmd = new SqlCommand(strSql,sCon);`
>
> `SqlDataAdapter Dap = new SqlDataAdapter(strSql,sCon);`

---

> [!note]
>
> <p style="font-size:20px;color:red">SqlDataReader</p>
>
> `SqlDataReader`，实例化这个对象的时候需要使用到`SqlCommand`类型的对象中的方法，所以必须先创建一个`SqlCommand`类型的对象，再调用这个对象中的`ExcuteReader`方法：
>
> ```C#
> SqlCommand Cmd = new SqlCommand( strSql,sCon );
> SqlDataReader sReader = new Cmd.ExcuteReader( );
> ```

















