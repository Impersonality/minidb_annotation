1.为什么要抽象成三层（entry,db_file,db），两层可以么，读写一条数据为读写一个entry
答：db_file和entry是接近存储层的概念，entry类似一条（行）数据，db_file是一个文件。
db是对db_file的抽象，接近db的概念， db通过对文件的管理，来实现数据库。所以minidb合并db_file和db是可以的，因为它很小。
