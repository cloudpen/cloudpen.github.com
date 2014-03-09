---
title: ASP.net课程—Application对象的应用
layout: post
category: Lesson
---

同去年，依旧是以实现聊天室的功能来讲解Application的功能。

以下主要用到的是Application的变量存储功能，变量清除功能。注意点：使用Application之前需要lock，用完之后要unlock，清除用Remove或者RemoveAll。

将教材案例中混在一起的编码分解成三大部分：页面呈现基本元素，后台方法、函数，页面美化文件。最终实现效果如图所示：

<img src="http://cloudpen-image.u.qiniudn.com/lesson-application.png" width="640" height="480" />

相关文件代码如下：

1 主文件内容
{% highlight html %}
 <%@ Page Language=”C#” AutoEventWireup=”true” CodeFile=”Default.aspx.cs” Inherits=”_Default” %>
    
    <!DOCTYPE html PUBLIC “-//W3C//DTD XHTML 1.0 Transitional//EN” “http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd“>
    
    <html xmlns=”http://www.w3.org/1999/xhtml“>
    <head runat=”server”>
    <title></title>
    <link  rel=”Stylesheet” type=”text/css” id=”css” />
    <script type=”text/javascript”>
    function change(a){
    var css=document.getElementById(“css”);
    if ( a==1)
    css.setAttribute(“href”,”StyleSheet.css”);
    if (a==2)
    css.setAttribute(“href”,”StyleSheet2.css”);
    }
    </script>
    
    </head>
    <body onload=”change(1)”>
    <form id=”form1″ runat=”server”>
    <h1 id=”title”>聊天室</h1>
    <div id=”m1″><asp:Label ID=”message” runat=”server”></asp:Label></div>
    <br />
    <asp:Label ID=”count” runat=”server”></asp:Label>
    <br />
    <br />
    昵称：
    <asp:TextBox ID=”txtName” runat=”server”></asp:TextBox>
    说话：
    <asp:TextBox ID=”txtWord” runat=”server”></asp:TextBox>
    <asp:Button ID=”btn” runat=”server” Text=”发送” onclick=”btn_Click” />
    <asp:Button ID=”clean” runat=”server” Text=”清屏” onclick=”clean_Click” />
    <select onchange=change(this.value)>
    <option>请选择</option>
    <option value=1>样式一</option>
    <option value=2>样式二</option>
    </select>
    </form>
    </body>
    </html>
{% endhighlight %} 
2 aspx.cs内容
{% highlight c# %}
	protected void Page_Load(object sender, EventArgs e)
    {
    string strMessage=(string)Application["Message"];
    message.Text = strMessage;
    count.Text = “当前在线：” + Application["counts"] + “人”;
    Session.Timeout = 1;
    }
    protected void btn_Click(object sender, EventArgs e)
    {
    string strName = txtName.Text;
    string strWord = txtWord.Text;
    Application.Lock();
    Application["Message"]=”<span>”+strName+”说：”+strWord+”</span><br/>”+Application["Message"];
    message.Text=(string)Application["Message"];
    }
    protected void clean_Click(object sender, EventArgs e)
    {
    Application.Contents.RemoveAll();
    Response.Redirect(“”);
    } 
{% endhighlight %} 
3 Css样式表文件内容
{% highlight css %}
    h1
    {
    text-align:center;
    color:Blue;
    }
    
    #m1
    {
    background-color:#000;
    border:5px solid #eee;
    color:#fff;
    padding:10px;
    line-height:150%;
    font-size:18px;
    font-family:黑体;
    text-align:left;
    height:300px;
    margin:20px;
    overflow:auto;
       
    filter:alpha(Opacity=80);
       }
      
     body
     {
     text-align:center;
     background-image:url(“1.jpg”);
     background-repeat:no-repeat;
     }
{% endhighlight %} 