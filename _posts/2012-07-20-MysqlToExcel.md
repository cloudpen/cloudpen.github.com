---
title: Mysql导出Excel无乱码代码
category: IT
layout: post
---

这两天做系统做得很High，一个星期做了两个系统，PHP+Mysql+Ajax。其中用了不少技术，准备整理出来和大家一起分享，今天先分享一个php导出mysql为excel文件，并保证中文无乱码的程序。

    <?php
    $DB_Server = “localhost”;
    $DB_Username = “root”;
    $DB_Password = “”;
    $DB_DBName = “”;  //数据库名
    $DB_TBLName = “”; //表名
    session_start();
    $banji=$_SESSION['banji'];//接收导出条件
    $savename = date(“YmjHis”);
    $Connect = @mysql_connect($DB_Server, $DB_Username, $DB_Password) or die(“Couldn’t connect.”);
    mysql_query(“Set Names ‘utf8′”);
    $file_type = “vnd.ms-excel”;
    $file_ending = “xls”;
    header(“Content-Type: application/$file_type;charset=gb2312″); //关键，决定文件编码，excel中文一般为gb2312
    header(“Content-Disposition: attachment; filename=”.$savename.”.$file_ending”);
    //header(“Pragma: no-cache”);
    
    $now_date = date(“Y-m-j H:i:s”);
    $title = “数据库名:$DB_DBName,数据表:$DB_TBLName,备份日期:$now_date”;
    
    $sql = “Select * from $DB_TBLName where banji=’$banji’”;
    $ALT_Db = @mysql_select_db($DB_DBName, $Connect) or die(“Couldn’t select database”);
    $result = @mysql_query($sql,$Connect) or die(mysql_error());
    $title=iconv(“UTF-8″, “gb2312″, “$title” );
    echo(“$titlen”);
    $sep = “t”;
    for ($i = 0; $i < mysql_num_fields($result); $i++) {
        echo mysql_field_name($result,$i) . “t”;
    }
    print(“n”);
    $i = 0;
    while($row = mysql_fetch_row($result)) {
        $schema_insert = “”;
            for($j=0; $j<mysql_num_fields($result);$j++) {
              if(!isset($row[$j]))
                  $schema_insert .= “NULL”.$sep;
              elseif ($row[$j] != “”)
                  $schema_insert .= iconv(“UTF-8″, “gb2312″, “$row[$j]” ).$sep;  //关键，iconv转编码，数据库中为utf8,转为gb2312
              else
                  $schema_insert .= “”.$sep;
                    }
             $schema_insert = str_replace($sep.”$”, “”, $schema_insert);
             $schema_insert .= “t”;
            print(trim($schema_insert));
            print “n”;
            $i++;
    }
    
    return (true);
    ?>