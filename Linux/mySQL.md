## Command
The command in mysql should end with ";"
- 进入 `mysql -u username -p`
  - `-p` password
- 创建数据库 `create database [database_name]`
- `show databases`
- `use [database_name]`
- `show tables`
- `desc [table_name]`
- 创建表
  > ```create table  MIFit_Image (name char(100), path char(100), count int(10), firstName char(100), firstMD5 char(100), secondName char(100), secondMD5 char(100), thirdName char(100), thirdMD5 char(100));```
- 修改表名 `rename table [MIFit_Image] to [MIFit_Image_New]`
- 删除表 `drop table [tableName]`
  

## Data type
|Data type | Sample| Python obj |
| --- | --- | --- |
| DATE | '2015-01-01' | datetime.date |
| TIME |  |
| YEAR | |
| DATETIME | '2015-01-01 14:36:59' | datetime.datetime | 
| TIMESTAMP | 2022-04-14 16:21:50.220732 | datetime.datetime |
