[toc]
GDB 命令行参数
=
启动 GDB：
-
l  gdb executable

l  gdb -e executable -c core-file

l  gdb executable -pid process-id 

（使用命令 'ps -auxw' 可以查看进程的 pid）

###选项
 含义
 
–help
-h
 列出命令行参数。
 
–exec=file
-e file
 指定可执行文件。
 
–core=core-file
-c core-file
 指明 core 文件。
 
–command=file
-x file
 从指定文件中读取 gdb 命令。
 
–directory=directory
-d directory
 把指定目录加入到源文件搜索路径中。
 
–cd=directory
 以指定目录作为当前路径来运行 gdb 。
 
–nx
-n
 不要执行 .gdbinit 文件中的命令。默认情况下，这个文件中的命令会在所有命令行参数处理完后被执行。
 
–batch
 在非交互模式下运行 gdb 。从文件中读取命令，所以需要 -x 选项。
 
–symbols=file
-s file
 从指定文件中读取符号表。
 
-write
 允许对可执行文件和 core 文件进行写操作。
 
–quiet
-q
 不要打印介绍和版权信息。
 
–tty=device
 指定 device 为运行程序的标准输入输出。
 
–pid=process-id
-p process-id
 指定要附属的进程 ID 。
 

 

GDB命令
-
GDB 中使用的命令：

命令
 描述
 
help
 列出 gdb 帮助信息。
 
help topic
 列出相关话题中的 gdb 命令。
 
help command
 列出命令描述信息。
 
apropos search-word
 搜索相关的话题。
 
###info args

i args
 列出运行程序的命令行参数。
 
info breakpoints
 列出断点。
 
info break
 列出断点号。
 
info break breakpoint-number
 列出指定断点的信息。
 
info watchpoints
 列出观察点。
 
info registers
 列出使用的寄存器。
 
info threads
 列出当前的线程。
 
info set
 列出可以设置的选项。
 
###Break and Watch
   
break funtion
break line-number
 在指定的函数，或者行号处设置断点。
 
break +offset
break -offset
 在当前停留的地方前面或后面的几行处设置断点。
 
break file:func
 在指定的file文件中的func处设置断点。
 
break file:nth
 在指定的file文件中的第nth行设置断点。
 
break *address
 在指定的地址处设置断点。一般在没有源代码时使用。
 
break line-number ifcondition
 如果条件满足，在指定位置设置断点。
 
break line threadthread-number
 在指定的线程中中断。使用info threads可以显示线程号。
 
tbreak
 设置临时的断点。中断一次后断点会被删除。
 
watch condition
 当条件满足时设置观察点。
 
clear
clear func
clear nth
 清除函数func处的断点。
清除第nth行处的断点。
 
delete
d
 删除所有的断点或观察点。
 
delete breakpoint-number
delete range
 删除指定的断点，观察点。
 
disable breakpoint-number-or-range
enable breakpoint-number-or-range
 不删除断点，仅仅把它设置为无效，或有效。
例子：
显示断点： info break
设置无效： disable 2-9
 
enable oncebreakpoint-number
 设置指定断点有效，当到达断点时置为无效。
 
enable del breakpoint-number
 设置指定断点有效，当到达断点时删除它。
 
finish
 继续执行到函数结束。
 
###Line Execution
   
step
s
step number-of-steps-to-perform
 进入下一行代码的执行，会进入函数内部。
 
next
n
next number
 执行下一行代码。但不会进入函数内部。
 
until
until line-number

until line-number ifcondition
 继续运行直到到达指定行号，或者函数，地址等。
 
return
return expression
 弹出选中的栈帧（stack frame）。如果后面指定参数，则返回表达式的值。
 
stepi
si
nexti
ni
 执行下一条汇编/CPU指令。
 
###info signals
info handle
handle SIGNAL-NAMEoption
 当收到信号时执行下列动作：nostop（不要停止程序），stop（停止程序执行），print（显示信号），noprint（不显示），pass/noignore（允许程序处理信号），nopass/ignore（不让程序接受信号）
 
where
 显示当前的行号和所处的函数。
 
Program Stack
   
backtrace
bt
bt inner-function-nesting-depth
bt -outer-function-nesting-depth
 显示当前堆栈的追踪，当前所在的函数。
 
backtrace full
 打印所有局部变量的值。
 
frame number
f number
 选择指定的栈帧。
 
up number
down number
 向上或向下移动指定个数的栈帧。
 
info frame addr
 描述选中的栈帧。
 
info args
info all-reg
info locals
info catch
 显示选中栈帧的参数，局部变量，异常处理函数。all-reg也会列出浮点寄存器。
 
###Source Code
   
list
l
list line-number
list function
list -
list start#,end#
list filename:function
 列出相应的源代码。
 
set listsize count
show listsize
 设置list命令打印源代码时的行数。
 
directory directory-name
dir directory-name
show directories
 在源代码路径前添加指定的目录。
 
directory
 当后面没有参数时，清除源代码目录。
 
###Examine Variables
   
print variable
p variable
p file::variable
p 'file'::variable
 打印指定变量的值。
 
p *array-var@length
 打印arrary-var中的前length项。
 
p/x var
 以十六进制打印整数变量var。
 
p/d var
 把变量var当作有符号整数打印。
 
p/u var
 把变量var作为无符号整数打印。
 
p/o var
 把变量var作为八进制数打印。
 
p/t var
x/b address
x/b &variable
 以整数二进制的形式打印var变量的值。
 
p/c variable
 当字符打印。
 
p/f variable
 以浮点数格式打印变量var。
 
p/a variable
 打印十六进制形式的地址。
 
x/w address
x/4b &variable
 打印指定的地址，以四字节一组的方式。
 
call expression
 类似于print，但不打印 void 。
 
disassem addr
 对指定地址中的指令进行反汇编。
 
###Controlling GDB
   
set gdb-option value
 设置 GDB 的选项。
 
set print array on
set print array off
show print array
 以可读形式打印数组。默认是 off 。
 
set print array-indexes on
set print array-indexes off
show print array-indexes
 打印数组元素的下标。默认是 off 。
 
set print pretty on
set print pretty off
show print pretty
 格式化打印 C 结构体的输出。
 
set print union on
set print union off
show print union
 打印 C 中的联合体。默认是 on 。
 
set print demangle on
set print demangle off
show print demangle
 控制 C++ 中名字的打印。默认是 on 。
 
###Working Files
   
info files
info share
 列出当前的文件，共享库。
 
file file
 把file当作调试的程序。如果没指定参数，丢弃。
 
core file
 把file当作 core 文件。如果没指定参数，则丢弃。
 
exec file
 把file当作执行程序。如果没指定参数，则丢弃。
 
symbol file
 从file中读取符号表。如果没指定参数，则丢弃。
 
load file
 动态链入file文件，并读取它的符号表。
 
path directory
 把目录directory加入到搜索可执行文件和符号文件的路径中。
 
###Start and Stop
   
run
r
run command-line-arguments
run < infile > outfile
 从头开始执行程序，也允许进行重定向。
 
continue
c
 继续执行直到下一个断点或观察点。
 
continue number
 继续执行，但会忽略当前的断点number次。当断点在循环中时非常有用。
 
kill
 停止程序执行。
 
quit
q
 退出 GDB 调试器。
 

GDB 操作提示
-
l  在编译可执行文件时需要给 gcc 加上 "-g" 选项，这样它才会为生成的可执行文件加入额外的调试信息。

l  不要使用编译器的优化选项，比如： "-O"，"-O2"。因为编译器会为了优化而改变程序流程，那样不利于调试。

l  在 GDB 中执行 shell 命令可以使用：shell command

l  GDB 命令可以使用 TAB 键来补全。按两次 TAB 键可以看到所有可能的匹配。

l  GDB 命令缩写：例如 info bre 中的 bre 相当于 breakpoints。

GDB 在 Emacs 中的操作：

emacs 按键
 动作
 
M-x gdb
 切换到 gdb 模式。
 
C-h m
 显示 gdb 模式介绍信息。
 
M-s
 等同于gdb 中的 step 命令。
 
M-n
 等同于gdb 中的 next 命令。
 
M-i
 等同于gdb 中的 stepi 命令。
 
C-c C-f
 等同于gdb 中的 finish 命令。
 
M-c
 等同于gdb 中的 continue 命令。
 
M-u
 等同于gdb 中的 up 命令。
 
M-d
 等同于gdb 中的 down 命令。
 

Copyed From 程序人生 
Home Page:http://www.programlife.net 
Source URL:http://www.programlife.net/gdb-manual.html 
