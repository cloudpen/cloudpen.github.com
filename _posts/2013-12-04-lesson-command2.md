---
title: ASP.net课程--Command操作数据库(2)
layout: post
category: Lesson
---

该例主要用来说明如何使用Command的对象来验证登录信息。并且介绍如何将数据库的连接移至Web.config文件中。

使用Web.config连接数据库的方法是，
在configuration之间加入以下内容：

{% highlight c# %}
  	<connectionStrings>
		<add name="ConString" connectionString="Data Source=localhost;Initial Catalog=t1;Integrated Security=True;Pooling=False" providerName="System.Data.SqlClient"/>
	</connectionStrings>
{% endhighlight %} 

验证登录的方法是，从表单中接收用户名和密码信息，通过SQL语句中的Select语句，将接受到的信息放入数据库中查询，如果有反馈结果，则通过验证通过，反之登录失败，具体验证代码如下：

{% highlight c# %}
	string username = Request.Form["username"];
        string passwd=Request.Form["password"];
        string ConString = ConfigurationManager.ConnectionStrings["ConString"].ConnectionString;
        SqlConnection con = new SqlConnection(ConString);
        con.Open();
        SqlCommand comm = new SqlCommand("select count(*) from s1 where username='"+username+"' and passwd='"+passwd+"'",con);
        if ((int)comm.ExecuteScalar() > 0)
            Response.Write("登录成功");
        else
            Response.Write("登录失败");
{% endhighlight %} 

通过上述操作，可制作完成一个简单的登录验证系统。