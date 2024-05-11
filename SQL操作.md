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

## **SqlCommand对象**

>[!tip]
>**SqlCommand对象主要是用来执行Sql语句**

**返回有效记录值**

```C#
SqlCommand mCmd = new SqlCommand( strSql , mCon ); //实例化对象
int i =  ExcuteNonQuery( );                           //返回有效记录行数
```

## **DataReader对象**

 [!tip]

 **概述：DataReader是一个简单的数据集，主要从数据源中读取数据集。必须一致保持与数据库的连接。**

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

>[!note]
>**使用DataReader有两个步骤：**
>
>**1. 首先是先实现DataReader的查找数据逻辑，写在处理sql的文件中**
>
>**2. 在窗体文件中使用DataReader**

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

>[!caution]
>
>***这里要注意：***
>
>***初始化DataReader对象的时候使用的是SqlCommand这个类的对象中的ExcuteReader( )方法***

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

>[!tip]
>
> - **DataSet实质上相当于在内存中的一个小型关系数据库。一个DataSet对象包含一组DataTable对象和DataRelation对象，其中每个DataTable对象都由DataColumn、DataRow、Constraint集合对象组成。他主要是通过DataAdapter检索数据，并填充到DataSet中。**
> - **DataAdapter对象是DataSet和数据库之间的桥梁，负责在DataSet和数据库之间传递数据。他使用Sql命令检索数据，并填充到DataSet和DataTable中。DataAdapter支持参数化查询。**
>
>***简单来说，DataSet是一个数据容器，用于存储和操作数据，而DataAdapter是一个数据传输工具，用于在数据库和DataSet之间移动数据。***

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
>    
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
> <p style="color:red;font-size:20px"创建连接</p
>
> **想要操作数据库，都要先定义连接：**
>
> 1. *定义连接的字符串：*`string strCon = ""server=.;database=BMS;uid=WFSQL;pwd=123456";"`
> 2. *创建*`SqlConnection`*对象*，*需要传入上面创建的*`strCon`*字符串*：

 ```C#
 SqlConnect sCon = new SqlConnect( strCon );
 ```

---

> [!note]
>
> <p style="font-size:20px;color:red"SqlCommand与SqlAdapter</p
>
> `SqlCommand`和`SqlAdapter`都属于需要sql的操作，所以实例化对象的时候需要传入两个参数：
>
> 1. `strSql`：一个*<usql字符串</u*
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
> <p style="font-size:20px;color:red"SqlDataReader</p
>
> `SqlDataReader`，实例化这个对象的时候需要使用到`SqlCommand`类型的对象中的方法，所以必须先创建一个`SqlCommand`类型的对象，再调用这个对象中的`ExcuteReader`方法：
>
> ```C#
> SqlCommand Cmd = new SqlCommand( strSql,sCon );
> SqlDataReader sReader = new Cmd.ExcuteReader( );
> ```
