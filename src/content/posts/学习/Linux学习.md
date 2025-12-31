---
title: Linux学习
published: 2025-12-31
description: Linux的学习心得，包括常见的命令，一些注意事项等等
image: ./image/cover.jpg
tags: ["Linux", "学习"]
category: 学习
draft: false


---

## Linux常见的命令

一般都是可以执行，如果缺乏权限的话，可以在命令前面加个sudo，代表以

#### 1. ls：列出当前目录下的文件和子目录

```Linux
输入：ls
输出：test.py      background.jpg      image   
```

#### 2. cd：切换工作目录

```Linux
输入：cd..
效果：返回到上一级目录；

输入：cd code
效果：切换到code目录
```

#### 3. pwd：显示当前工作目录

```Linux
输入：pwd
输出：当前工作目录位置；比如/home/hui/code
```

#### 4. mkdir：创建一个新目录

```Linux
输入：mkdir paltform
效果：在当前工作目录下创建了一个名位“platform”的目录
```

### rm家族

> ### ==切记Linux里面rm删除指令不会扔到回收站里面，是彻底删除的，所以在执行rm相关指令的话，请仔细检查==
>
> #### 5. rm：删除文件或者目录
>
> ```Linux
> 基本语法格式：rm [options] name...
> options是各种命令选项，效果是指定命令的行为，比如删除空目录，删除文件等等，后续会补充
> 输入：rm file.txt
> 效果：删除file.txt
> 
> 输入：rm file.txt picture.jpg video.mp4
> 效果：删除 file.txt, picture.jpg和video.mp4
> ```
>
> #### 6. rmdir或者rm -d ：删除一个空目录
>
> ```Linux
> 输入：rmdir platform或者rm -d platform
> 效果：把当前目录下名为“platform”的空目录给删除掉，必须保证该目录里面没有文件，是个空目录
> ```
>
> #### 7. rm -r：递归删除目录及其所有子目录和文件
>
> ```Linux
> 输入；rm -r platform
> 效果：会把platform里面的目录和文件递归删除，也会把platform这个目录也删除掉
> ```
>
> #### 8. rm -f：强制删除指定的文件，不能删除目录
>
> ```
> 输入：rm -f platform.txt
> 效果：强制删除该文件，即使该文件不存在或者是只读文件，也会被删除。
> ```
>
> #### 9. rm -rf：强制递归删除目录和文件（很危险）
>
> ```
> 输入：rm -rf platform
> 效果：强制把platform里面的目录和文件递归删除，也会把platform这个目录也删除掉
> ```
>
> #### 10. rm -i：交互式删除，删除每个文件前都进行询问
>
> ```Linux
> 输入：rm -i *.txt
> 输出：
> rm：是否删除普通空文件 'file1.txt'？ y
> rm：是否删除普通空文件 'file2.txt'？ n （不删除）
> rm：是否删除普通空文件 'file3.txt'？ y
> ```
>
> #### 11.  rm- I：交互式删除，但是批量式确认，删除超过三个以上的文件时只确认一次
>
> ```
> 输入：rm -I *.txt
> 输出：
> rm：是否删除5个参数？ y   # 只问一次
> 如果只有2个文件，不会询问
> ```
>
> #### 12. rm *：（通配符，任意个字符）
>
> ```Linux
> 输入：rm *.txt             
> 效果：删除所有.txt文件
> 
> 输入：rm *  
> 效果：删除所有文件
> 
> 输入：rm a*                
> 效果：删除以a开头的文件
> ```
>
> #### 13. rm ?：（通配符，单个字符）
>
> ```Linux
> 输入：rm ?.txt
> 效果：删除单个字符的.txt文件，比如a.txt，b.txt
> 
> 输入：rm a?.txt
> 效果：删除以a开头，后面只跟一个字符的.txt文件，比如ab.txt，a1.txt，a2.txt
> ```
>
> #### 14. rmdir -p：删除空目录链，如果父目录也空了，也一并删除
>
> ```Linux
> 创建目录链（所有目录都空）
> mkdir -p parent/child/grandchild
> 
> 输入：rmdir -p parent/child/grandchild
> 效果：三个目录都被删除
> 
> 如果目录里面有文件的话，删除会失败
> ```
>
> #### 15. rmdir -v：显示删除目录的详细信息
>
> ```Linux
> 输入：rmdir -v dir1 dir2 dir3
> 输出：
> rmdir: 正在删除目录 'dir1'
> rmdir: 正在删除目录 'dir2'
> rmdir: 正在删除目录 'dir3'
> ```

#### 15. cp：复制文件

```Linux
输入：cp file.txt /path/to/destination/
详情；将file.txt复制到/path/to/destination/文件夹内
```

> `-r` 或 `-R`：递归复制目录及其内容（用于复制目录）。
>
> `-i`：交互模式，覆盖前提示用户确认。
>
> `-f`：强制复制，覆盖目标文件而不提示。
>
> `-v`：显示详细的复制过程（verbose）。
>
> `-p`：保留文件的原始属性（如权限、时间戳等）。
>
> `-a`：归档模式，等同于 `-dpR`，保留所有文件属性和递归复制目录。
>
> `-u`：仅当源文件比目标文件新时才复制（更新模式）。
>
> `-l`：创建硬链接而不是复制文件。
>
> `-s`：创建符号链接（软链接）而不是复制文件。

```Linux
输入：cp file1.txt file2.txt /path/to/destination/
详情：复制多个文件到目标目录，复制file1.txt和file2.txt到destination目录
```

```Linux
输入：cp file.txt /path/to/destination/newfile.txt
详情：将file.txt复制到/path/to/destination/并重命名为newfile.txt
```

```
输入：cp -r /path/to/source_dir /path/to/destination/
详情：将source_dir目录及其内容递归复制到 destination 目录。
```

```Linux
输入：cp -i file.txt /path/to/destination/
详情：交互式复制，如果目标位置已存在同名文件，会提示用户确认是否覆盖。
```

```Linux
输入：cp -u file.txt /path/to/destination/
详情：仅当file.txt比目标文件新时才会复制
```

```Linux
输入：cp -p file.txt /path/to/destination/
详情：复制文件并保留其原始属性（如权限、时间戳等）。
```

```
输入：cp -v file.txt /path/to/destination/
详情：显示复制过程的详细信息
```

```Linux
输入：cp -l file.txt /path/to/destination/
详情：复制一份文件的硬链接，本质上是同一个文件起了不同名字
```

```Linux
输入：cp -s file.txt /path/to/destination/
详情：复制一份文件的符号链接，有点像快捷方式
```

#### 16. mv：移动文件位置或重命名文件

```linux
输入：mv file.txt dest_dirtory
详情：将file.txt移动到dest_dirtory目录当中
```

```Linux
输入：mv source.txt dest_file.txt
详情：将source.txt重命名为dest_file.txt
```

```Linux
输入：mv source_directory dest_directory
详情：目录名 dest_directory 已存在，将 source_directory 移动到目录名 dest_directory 中；
目录名 dest_directory 不存在则 source_directory 改名为目录名 dest_directory
```

> - `-b`: 当目标文件或目录存在时，在执行覆盖前，会为其创建一个备份。
> - `-i`: 如果指定移动的源目录或文件与目标的目录或文件同名，则会先询问是否覆盖旧文件，输入 y 表示直接覆盖，输入 n 表示取消该操作。
> - `-f`: 如果指定移动的源目录或文件与目标的目录或文件同名，不会询问，直接覆盖旧文件。
> - `-n`: 不要覆盖任何已存在的文件或目录。
> - `-u`：当源文件比目标文件新或者目标文件不存在时，才执行移动操作。

#### 17. touch：创建空文件或者更新文件的时间戳

```Linux
输入：touch file.txt
详情：如果file.txt在当前目录不存在，那么就会创建一个空的file.txt
如果file.txt已经存在，它会更新该文件的访问和修改时间戳为当前时间
```

