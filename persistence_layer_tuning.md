#Persistence Layer Tuning

##数据库设计

###范式化与反范式化

OLTP vs OLAP

`@Embedded`可以用来定义反范式化列

###数据库分区

####水平分区

将大数据表拆分为多个小的数据表，每个表的列定义都一样。比如按照数据创建的年份。

相对于扫描大数据表，某些查询只需要扫描小的数据表，性能更好。

####垂直分区

将数据表中的列拆分到多个数据表中。特定的dataset只包含部分列的数据，但是包含所有行。使用JPA/Hibernate可以用lay one-to-many映射。

###数据库索引

索引可以有效提高读数据操作的性能。索引项按照一定顺序存储，索引也有助于出来group by和order by。

delete/update操作需要需要修改索引，会带来额外开销。

**创建索引的guidelines**

####在适当的列上索引

选择在where，group by和order by中出现的列建立索引。

####尽量使小索引

索引越小，处理越快，包括IO和比较。

####索引选择度高的列

distinct值越多越好

####使用合适的组合(multicolumn)索引

选择度高的列排在前面

##JDBC

* connection pool
* fetch size, batch size
* prepared statements, prepared statments pool on application server level

##JPA/Hibernate

