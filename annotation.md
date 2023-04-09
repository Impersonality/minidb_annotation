1.核心结构体(entry/db_file/db)的结构分析
entry是bit_cask的数据单元，类似mysql的一行数据，db_file的struct是一个文件，存储db的所有entries， 
entry和db_file是存储层的结构，db就是db层的结构，db的struct有一个db_file，indexes，lock。
它的功能之一是将db操作 转换为对db_file和entry的操作，类似于业务系统中的service，将Put/Get/Delete转换成Read/Write；
indexes索引自然是加速查询，lock负责数据安全性。

2.minidb和bustdb存储方式比较
minidb打开一个file作为db，数据单元entry连续的存放于file中，数据修改只有append entry。
bustdb使用b+ tree作为存储结构，不过b+ tree是在程序中的拓扑结构，tree的每个节点对应一个page，page在磁盘上是连续存储的页。
页的大小有固定限制，数据单元没有，数据修改可能会引起树的结构变化，但磁盘上的页不会移动。
