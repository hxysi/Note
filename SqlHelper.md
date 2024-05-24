把这一串代码复制到SqlHelper类中，将第二行的`database=`后面改为自己的数据库名，以及`uid`和`pwd`也是改为自己数据库的登录名和密码
```C#
  int recordRows = 0;
  string strCon = "server=.;database=Hotel Management System;uid=WFSQL;pwd=123456";
  public int execSql(string strSql)
  {
      SqlConnection sCon = new SqlConnection(strCon);
      SqlCommand Cmd = new SqlCommand(strSql, sCon);
      sCon.Open();
      int i = Cmd.ExecuteNonQuery();
      sCon.Close();
      return i;
  }
  
  public bool Reader(string strSql, bool isQuery)
  {
      recordRows = 0;
      bool f = false;
      SqlConnection sCon = new SqlConnection(strCon);
      SqlCommand Cmd = new SqlCommand(strSql, sCon);
      sCon.Open();
      SqlDataReader sReader = Cmd.ExecuteReader();
      if (sReader.HasRows)
      {
          f = true;
      }
      else
      {
          f = false;
      }
      if (isQuery)
      {
          while (sReader.Read())
          {
              recordRows++;
          }
      }
      sCon.Close();
      sReader.Close();
      return f;
  }
  
  public int getRecord()
  {
  
      int record = recordRows;
      return record;
  }
  
  public DataSet getDs(string strSql)
  {
      SqlConnection sCon = new SqlConnection(strCon);
      SqlDataAdapter Dap = new SqlDataAdapter(strSql, sCon);
      DataSet Ds = new DataSet();
      sCon.Open();
      Dap.Fill(Ds);
      sCon.Close();
      return Ds;
  }
```

