# 特殊符号

1. # 注释

2. ; 命令分隔符

```
echo hello; echo there


if [ -x "$filename" ]; then    # 注意: "if"和"then"需要分隔.
	echo "File $filename exists."; cp $filename $filename.bak
else
	 echo "File $filename not found."; touch $filename
fi;echo "File test complete."
```

3. ;; 终止case选项

4. .点命令
   - 等价source命令
   - 字符匹配

5. 双引号，阻止字符串中的大部分特殊字符

6. 单引号，阻止字符串中所有的的特殊字符

7. 逗号，连接一系列算术操作

8. \\ 转移字符 

9. / 文件路径分割线

10. ` 命令替换

11. 冒号

    1)  空命令,等价于"NOP"也可以被认为与shell的内建命令true作用相同. ":"命令是一个bash的内建命令, 它的退出码(exit status)是"true"(0).

	2) if/then 中的占位符

	```
	if condition
	then
	    :
	else
        take some action
	fi

	```
    3) 二元命令中的占位符

	```
	: ${username=`whoami`}
	```
    
	4) 在参数替换中评估字符串变量

	```
	: ${HOSTNAME?} ${USER?} ${MAIL?}
	```
    5) 清空文件

	```
	: > data.xxx
	```

	6) path变量分隔符

12. 感叹号，取反操作符

13. 星号，通配符

14. 问号
    - 测试操作符
    - 通配符

15. $ 
    - 引用变量的内容
	- 行结束符

16. ${}  参数替换

17. $* $@ 位置参数

18. $? 退出码状态

19. $$ 保存它所在脚本的进程ID

20. ()
    - 命令组,在括号中的命令列表, 将会作为一个子shell来运行.
    - 初始化数组
	
	```
	Array=(element1 element2 element3)
	```

21. 大括号

   - 大括号扩展
   
   ```
    cat {file1,file2,file3} > combined_file
    把file1, file2, file3连接在一起, 并且重定向到combined_file中
   
    cp file22.{txt,backup}
	拷贝"file22.txt"到"file22.backup"中
   ```

22. \[\] 
    
	- 条件测试
    - 数组元素
	- 字符范围

23. \[\[\]\] 测试

24. (())  整数扩展

25. 重定向

```
 cmd > file        重定向标准输出  
 cmd &> file       重定向stdout和stderr
 cmd >&2           重定向stdout到stderr
 cmd > file 2>&1   stdout和stderr重定向到文件
 cmd >> file       追加
 [i]<> file        打开file用来读写,并且分配文件描述符给i
 cmd >|file        强制重定向

 cmd < file    输入重定向

command << delimiter    here document
    document
	delimiter
```

26. | 管道

27. || 或逻辑

28. & 后台运行命令

29. && 与操作

30. - 用于重定向stdin或stdout

```
(cd /src/dir && tar cf - .)|(cd /dst/dir && tar xpvf -)

实现从一个目录移动整个目录树到另外一个目录
这里的 “-” 做为stdout 和 stdin
```

```
 echo "whatevet" | cat -
```

```
grep Linux file1 | diff file2 -
```

31. ~+ 当前工作目录.相当$PWD内部变量.

32. ~- 先前的工作目录. 相当于$OLDPWD内部变量.

# 变量和参数

## 变量替换

1. 变量使用等号复制，使用$对变量进行引用

2. 等号的前后不能存在空格

```
VARIABLE =value   //解释器认为VALIABLE为一个命令，带有参数=value
VARIABLE= value   //解释器认为value为一个命令，并且带有环境变量VARIABLE=“”
```

3. $variable是${variable}的简写
