#### 事务
> 一个逻辑单元一组操作,要么全部执行,要么全部不执行

#### 流程控制
- begin transaction
- commit
- rollback

#### 事务四个特性
- 原子性(Atomicity): 一个事务中的所有操作要么全部执行,要么全部不执行
- 一致性(Consistency): 事务前后的数据完整性必须保持一致性
- 隔离性(Isolation): 多个事务独立,不相互影响
- 持久性(Durability): 事务提交将保存到数据库

#### 事务并发问题:
- 脏读: a事务读取到了b事务未提交的数据
- 不可重复读: a事务同一条sql语句两次查询结果不一致
- 欢读: a事务中,两次读取的数据量不一致

#### 事务隔离级别:
mysql默认隔离为可重复读
- 未提交读(read uncommitted),出现脏读
- 提交读(read committed),出现不可重复读
- 可重复读(repeatable read),出现幻读
- 串行化(serializable)

安全性: ru < rc < rr < s  
性能: ru > rc > rr > s

#### 代码:
```php
$dsn = 'mysql:dbname=met;host=localhost';
$pdo = new PDO($dsn, 'root', '');
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

try {
    $pdo->beginTransaction();
    $sql2 = "insert into swoole(`name`,`age`) values('roob',23)";
    echo $pdo->exec($sql2) ? 'yes' : 'no';
    echo "\n";
    $pdo->commit();
} catch (Exception $e) {
    echo $e->getMessage() . "\n";
    $pdo->rollBack();
}
```
