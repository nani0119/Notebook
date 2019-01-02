# bash support hot key

## 注释

注释使用的热键以引导字符“\\”+c(comment)开始

| 按键  | 作用                | 备注           |
|-------|---------------------|----------------|
| \\cl  | end-of-line comment | 在行尾添加注释 |
| \\cc  | code->comment       | 注释掉一行     |
| \\co  | uncomment code      | 反注释一行     |
| \\cfr | frame comment       | 增加注释块     |
| \\cfu | function comment    |                |
| \\csh | shebang             |                |
| \\ch  | file header         | 文件头         |
| \\cd  | date                |                |
| \\ct  | time                |                |
| \\css | sections comment    |                |
| \\ckc | keyword comments    |                |
| \\cma | plug-in macros      |                |
| \\ce  | echo ""             |                |
| \\cr  | remove echo ""      |                |

---

## 语句

语句使用的热键以引导字符“\\”+s(statements)开始

| 按键  | 作用                       |
|-------|----------------------------|
| \\sc  | case in ...esac            |
| \\sei | elif then                  |
| \\sfo | for((...))do done          |
| \\sf  | for in do done             |
| \\si  | if then fi                 |
| \\sie | if then else fi            |
| \\ss  | select in do done          |
| \\su  | until do done              |
| \\sw  | while do done              |
| \\sfu | function                   |
| \\se  | echo -e ""                 |
| \\sp  | printf "%s"                |
| \\sae | array element ${.[.]}      |
| \\saa | arr.elem.s(all)${.[@]}     |
| \\sas | arr.elem.s(1word) ${.[*] } |
| \\ssa | subarray ${.[@]::}         |
| \\san | no. of arr. elem.s ${.[@]} |
| \\sai | list of indices ${.[*]}    |

## 测试条件

测试条件使用热键以引导字符“\\”+t(test)开始

| 按键  | 用途                            | 备注         |
|-------|---------------------------------|--------------|
| \\ta  | arithmetic tests                | 算术测试     |
| \\tfp | file permissions                |              |
| \\tft | file type                       |              |
| \\tfc | file characteristics            | 文件特性测试 |
| \\ts  | string comparisons              |              |
| \\toe | option is enabled               |              |
| \\tvs | variables has been set          |              |
| \\tfd | file descr.refers to a terminal |              |
| \\tm  | string matches regexp           |              |

## 模式匹配

模式匹配使用的热键以引导字符“\\”+p(pattern)开始

| 按键  | 用途                     | 备注            |
|-------|--------------------------|-----------------|
| \\pzo | ?(\|)                    | zero or one     |
| \\pzm | *(\|)                    | zero or more    |
| \\pom | +(\|)                    | one or more     |
| \\peo | @(\|)                    | exactly one     |
| \\pae | !(\|)                    | anything except |
| \\pbr | ${BASH_REMATCH[0: : :3]} |                 |
| \\ppc | POSIX classes            |                 |

## IO重定向

| 按键  | 作用                   |
|-------|------------------------|
| \\ior | IO-redirections (list) |
| \\ioh | here-dicyment          |


## Snippets

| 按键  | 用途                     |
|-------|--------------------------|
| \\nr  | read code snippet        |
| \\nv  | view code snippet        |
| \\nw  | write code snippet       |
| \\ne  | edit code snippet        |
| \\ntl | edit local templates     |
| \\ntc | edit custom templates    |
| \\ntp | edit persional templates |
| \\ntr | reread the templates     |
| \\ntw | template setup wizard    |
| \\nts | choose style             |

## 运行

| 按键  | 作用                            |
|-------|---------------------------------|
| \\rr  | run script                      |
| \\ra  | set script cmd. line arguments  |
| \\rba | set interp.cmd. line arguments  |
| \\rc  | check syntax                    |
| \\rco | syntax check options            |
| \\ro  | change output destination       |
| \\rd  | set "direct run"                |
| \\rse | set shell executable            |
| \\rx  | set xterm size                  |
| \\re  | make script excutabnle/not exec |
| \\rh  | hardcopy buffer                 |
| \\rs  | plug-in settings                |

## help

| 按键 | 作用                    |
|------|-------------------------|
| \\he | english dictionary      |
| \\hb | display the bash manual |
| \\hh | help (bash builtins)    |
| \\hm | show manual             |
| \\hp | help(plug-in)           |
