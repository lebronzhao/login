# login

function sql_operation($mysqli,$sql){
//2.判断是否连接成功
//$mysqli->connect_errno 获取错误信息
//如果无错误，返回0 有错误，返回错误码

    if ($mysqli->connect_errno){
        //终止程序，并且提示错误
        die($mysqli->connect_errno);
    }
//3.执行数据库操作
//表格里面所有的字段设置编码格式 utf8
    $mysqli->query("set names utf8");
//执行sql语句
    $result = $mysqli->query($sql);
    if ($result){
        return "成功";
    } else {
        return "失败";
    }
//4.执行成功，关闭数据库
    $mysqli->close();
}
//1.链接数据库
$mysqli = new mysqli("localhost","root","","PHP1217");
$sql = "INSERT INTO user(name,age,sex) VALUES ('傻丁',18,'女')";
$result = sql_operation($mysqli,$sql);

* 插入
* INSERT INTO 表名(字段一,字段二...) VALUES(值一,值二...)
   *
* INSERT INTO user1(name,age,sex) VALUES("homework","30","男")
* 插入多条数据
   *INSERT INTO user1(name,age,sex) VALUES("老鞠","18","男"),("老丁","16","女")
    *
* 删除表中所有数据,但是不删除表格
* DELETE FROM user1
   *
    *
    *DELETE FROM 表名  WHERE 条件
* 同时满足两个条件用AND连接条件
* DELETE FROM user WHERE id=1
   *
* 改
* UPDATE 表名 SET 字段1=值1,字段2=值2 WHERE 条件
* UPDATE user1 SET name="方姐",age=18 WHERE id=5
   *
    *查
* 查找所有数据
* SELECT * FROM 表名
   *
* SELECT * FROM user1 WHERE age!=18
* SELECT * FROM user1 WHERE age<>18
   *
    *
* 模糊查询
* %代表零个或多个字符
* 查找表中name的值  以老字开头
* SELECT * FROM `user1` WHERE name like "%老"
* 只要有老都查出来
* SELECT * FROM `user1` WHERE name like "%老%"
   *
* 按照年龄降序排列(不加DESC(降序)就是默认的升序(ASC))
* SELECT * FROM user1 ORDER BY AGE DESC
   *
* 按拼音升序排列
* SELECT * FROM user1 ORDER BY CONVERT(name using gbk)
   *
* 查找表中所有name age字段
* SELECT name,age FROM user1
   *
    *
* 从表的第2条开始查,查3条
* 从0开始数
* SELECT * FROM `user1` LIMIT 2,3
   *