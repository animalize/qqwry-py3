用于在qqwry.dat里查找IP地址归属地，另提供一个从纯真网络更新qqwry.dat的小工具。

已上传到PyPI，执行此命令即可安装：``pip install qqwry-py3``

﻿﻿特点 Break
======

1. for Python 3.0+。

2. 提供两套实现供选择。有一个查找速度更快，但加载慢、占用内存多。

3. 在i3 3.6GHz，Python 3.6上查询速度达18.0万次/秒。

4. 提供一个从纯真网络(cz88.net)更新qqwry.dat的小工具，用法见本文最后一部分。

用法
======

  >>> from qqwry import QQwry
  >>> q = QQwry()
  >>> q.load_file('qqwry.dat')
  >>> q.lookup('8.8.8.8')
  ('美国', '加利福尼亚州圣克拉拉县山景市谷歌公司DNS服务器')

解释q.load_file(filename, loadindex=False)函数
----------------------------------------------

| 
| 加载qqwry.dat文件。成功返回True，失败返回False。
| 参数filename可以是qqwry.dat的文件名（str类型），也可以是bytes类型的文件内容。
| 
| 当参数loadindex=False时（默认参数）：
| 程序行为：把整个文件读入内存，从中搜索
| 加载速度：很快，0.004 秒
| 进程内存：较少，16.9 MB
| 查询速度：较慢，5.3 万次/秒
| 使用建议：适合桌面程序、大中小型网站
| 
| 当参数loadindex=True时：
| 程序行为：把整个文件读入内存。额外加载索引，把索引读入更快的数据结构
| 加载速度：★★★非常慢，因为要额外加载索引，0.78 秒★★★
| 进程内存：较多，22.0 MB
| 查询速度：较快，18.0 万次/秒
| 使用建议：仅适合高负载服务器
| 
| （以上是在i3 3.6GHz, Win10, Python 3.6.2 64bit，qqwry.dat 8.86MB时的数据）

解释q.lookup('8.8.8.8')函数
---------------------------

| 
| 找到则返回一个含有两个字符串的元组，如：('国家', '省份')
| 没有找到结果，则返回一个None

解释q.clear()函数
-----------------

| 
| 清空已加载的qqwry.dat
| 再次调用load_file时不必执行q.clear()

解释q.is_loaded()函数
---------------------

q对象是否已加载数据，返回True或False

解释q.get_lastone()函数
-----------------------

| 
| 返回最后一条数据，最后一条通常为数据的版本号
| 没有数据则返回一个None

  >>> q.get_lastone()
  ('纯真网络', '2020年9月30日IP数据')

从纯真网络(cz88.net)更新qqwry.dat的小工具
=========================================

  >>> from qqwry import updateQQwry
  >>> ret = updateQQwry(filename)

| 
| 当参数filename是str类型时，表示要保存的文件名。
| 成功后返回一个正整数，是文件的字节数；失败则返回一个负整数。
| 
| 当参数filename是None时，函数直接返回qqwry.dat的文件内容（一个bytes对象）。
| 成功后返回一个bytes对象；失败则返回一个负整数。这里要判断一下返回值的类型是bytes还是int。


| 
| 负整数表示的错误：
| -1：下载copywrite.rar时出错
| -2：解析copywrite.rar时出错
| -3：下载qqwry.rar时出错
| -4：qqwry.rar文件大小不符合copywrite.rar的数据
| -5：解压缩qqwry.rar时出错
| -6：保存到最终文件时出错


Features
========

1. for Python 3.0+.

2. Provide two sets of implementations for selection. One finds faster, but loads slowly and takes up more memory.

3. The query speed on i3 3.6GHz and Python 3.6 is 180,000 times per second.

4. Provide a small tool to update qqwry.dat from Chunzhen Network (cz88.net), see the last part of this article for usage.

usage
======

  >>> from qqwry import QQwry
  >>> q = QQwry()
  >>> q.load_file('qqwry.dat')
  >>> q.lookup('8.8.8.8')
  ('United States','Google DNS server in Mountain View, Santa Clara County, California')

Explain the q.load_file(filename, loadindex=False) function
-----------------------------------------------------------

|
| Load the qqwry.dat file. Return True on success, False on failure.
| The parameter filename can be the file name of qqwry.dat (str type), or the file content of bytes type.
|
| When the parameter loadindex=False (default parameter):
| Program behavior: read the entire file into memory, search from it
| Loading speed: very fast, 0.004 seconds
| Process memory: less, 16.9 MB
| Query speed: slower, 53,000 times per second
| Suggestions for use: suitable for desktop programs, large, medium and small websites
|
| When the parameter loadindex=True:
| Program behavior: Read the entire file into memory. Load an additional index, read the index into a faster data structure
| Loading speed: ★★★Very slow, because of the additional loading index, 0.78 seconds★★★
| Process memory: more, 22.0 MB
| Query speed: faster, 180,000 times per second
| Recommendations for use: only suitable for high-load servers
|
| (The above is the data when i3 3.6GHz, Win10, Python 3.6.2 64bit, qqwry.dat 8.86MB)

Explain the q.lookup('8.8.8.8') function
----------------------------------------

|
| If found, return a tuple containing two strings, such as: ('country','province')
| If no result is found, a None is returned

Explain the q.clear() function
------------------------------

|
| Clear the loaded qqwry.dat
| It is not necessary to execute q.clear() when calling load_file again

Explain the q.is_loaded() function
----------------------------------

Whether the q object has loaded data, return True or False

Explain the q.get_lastone() function
------------------------------------

|
| Return the last piece of data, the last piece is usually the version number of the data
| Return None if there is no data

  >>> q.get_lastone()
  ('纯真网络', '2020年9月30日IP数据')

Update the widget of qqwry.dat from Chunzhen Network (cz88.net)
===============================================================

  >>> from qqwry import updateQQwry
  >>> ret = updateQQwry(filename)

|
| When the parameter filename is of type str, it indicates the name of the file to be saved.
| Upon success, it returns a positive integer, which is the number of bytes in the file;
| Upon failure, it returns a negative integer.
|
| When the parameter filename is None, the function directly returns the content of the qqwry.dat file (a bytes object).
| Return a bytes object on success; return a negative integer on failure. Here to determine whether the type of the return value is bytes or int.


|
| Errors represented by negative integers:
| -1: An error occurred while downloading copywrite.rar
| -2: Error when parsing copywrite.rar
| -3: An error occurred when downloading qqwry.rar
| -4: qqwry.rarfile size does not match the data of copywrite.rar
| -5: Error when decompressing qqwry.rar
| -6: An error occurred while saving to the final file
