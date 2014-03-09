---
title: ASP.net课程--Command操作数据库(1)
layout: post
category: Lesson
---

ASP.net中可以采用Command对象执行SQL命令来对数据库进行操作。一般常用的方法有：

+ ExecuteReader() -- 执行一个查询，返回查询数据，数据只读不可写
+ ExecuteScalar() -- 执行一个查询，返回查询数据中第1行第1列处的值，可以用于各种数值统计
+ ExecuteNonQuery() -- 执行一个非查询命令，返回受影响的行数

以下是一个简单的用户注册页面的核心代码，用的正是上述ExecuteScalar方法和ExecuteNonQuery方法的组合。

从表单中接收username和userpasswd的值，并通过ExecuteScalar的方法来查询username是否已经在数据库中存在，如存在则返回不可注册提示，如不存在则可进行下一步注册，即通过ExecuteNonQuery来对数据库进行写操作。

代码1：
{% highlight c# %}
      protected void Page_Load(object sender, EventArgs e)
         {
            string username=Request.Form["username"];
            string passwd=Request.Form["userpasswd"];
            if (checkuser(username)){
            SqlConnection conn = new SqlConnection();
            SqlTransaction trans;
            conn.ConnectionString = "Data Source=localhost;Initial Catalog=T1;Integrated Security=True;Pooling=False";
            conn.Open();
            trans = conn.BeginTransaction();
            SqlCommand comm = new SqlCommand("insert into s1(username,password) values('"+username+"','"+passwd+"')",conn,trans);
            try
            {
               comm.ExecuteNonQuery();
               trans.Commit();
               Response.Write("注册成功");
             }
            catch {
              trans.Rollback();
              Response.Write("注册失败");
             }
            conn.Close();
            }else{
             Response.Write("您的用户名已注册");
             }
         }
{% endhighlight %}       
代码2：
{% highlight c# %}
      protected bool checkuser(string username) {
            SqlConnection conn = new SqlConnection();
            conn.ConnectionString = "Data Source=localhost;Initial Catalog=T1;Integrated Security=True;Pooling=False";
            conn.Open();
            SqlCommand comm = new SqlCommand("select count(*) from s1 where username='" + username+"'", conn);
            if ((int)comm.ExecuteScalar() > 0)
                  return false;
            else
                  return true;
      }
{% endhighlight %}   