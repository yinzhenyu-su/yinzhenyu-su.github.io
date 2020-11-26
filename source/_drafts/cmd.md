---
title: cmd
date: 2020-10-13 00:24:27
tags:
  - [cmd]
---

```cmd
for /F %1 in ('svn-observer config -g') do ( set commitid=%1)
```

[设置变量]
格式：set 变量名=变量值
详细：被设定的变量以%变量名%引用

[取消变量]
格式：set 变量名=
详细：取消后的变量若被引用%变量名%将为空

[展示变量]
格式：set 变量名
详细：展示以变量名开头的所有变量的值

[列出所有可用的变量]
格式：set

[计算器]
格式：set /a 表达式
示例：set /a 1+2*3
输出 7

预定义的变量

下面是些已经被底层定义好可以直接使用的变量：不会出现在 SET 显示的变量列表中
%CD% - 扩展到当前目录字符串。
%DATE% - 用跟 DATE 命令同样的格式扩展到当前日期。
%TIME% - 用跟 TIME 命令同样的格式扩展到当前时间。
%RANDOM% - 扩展到 0 和 32767 之间的任意十进制数字。
%ERRORLEVEL% - 扩展到当前 ERRORLEVEL 数值。
%CMDEXTVERSION% - 扩展到当前命令处理器扩展名版本号。
%CMDCMDLINE% - 扩展到调用命令处理器的原始命令行。
%0 bat的完整路径名如"C:\Windows\system32\xxx.bat"
%1 bat参数1依次类推%2参数2...
%path% - 当前的环境变量。以分号隔开的路径列表，路径可包含空格，可以以'\'结尾, 可以以双引号包围之。


扩展变量

@ 与%i相关的变量（bat参数或者for循环的%i)
假设文件为C:\Documents and Settings\jinsun\桌面\ParseSinglePkgs.bat
%0        C:\Documents and Settings\jinsun\桌面\ParseSinglePkgs.bat
%~dp0 C:\Documents and Settings\jinsun\桌面\
%cd%   C:\Documents and Settings\jinsun\桌面
%~nx0   ParseSinglePkgs.bat
%~n0     ParseSinglePkgs
%~x0     .bat

获取批处理文件所在路径
在开发时，经常需要使用批处理运行一些程序，java程序 犹其是这样，往往需要运行时根路径。Hardcode一个路径总是令自己觉得不自在，例如一个java程序从一台机copy到另外一台机，盘符往往发生变化，先修改一下bat里的路径再运行显然很麻烦。
在批处理开头加入cd /d %~dp0 一行代码就真真实实地做到“编写一次，到处运行”。%0是批处理文件本身的路径，%~dp进行扩展， d向前扩展到驱动器，p往后扩展到路径。例如，你的bat文件在e:/mybat/test.bat,则%0就是e:/mybat/test.bat, %~dp0是e:/mybat/。 /d选项支持CD到不同盘符。
另外，%i提取第i个命令选项，例如%1提取第1个option，i可以取值从1到9
%~0： 取文件名（名+扩展名）
%~f0：取全路径
%~d0：取驱动器名
%~p0：只取路径（不包驱动器）
%~n0：只取文件名
%~x0：只取文件扩展名
%~s0：取缩写全路径名
%~a0：取文件属性
%~t0：取文件创建时间
%~z0：取文件大小
以上选项可以组合起来使用。

获取命令行参数
%0，%1，%2，... %9，可以用来引用命令行参数，其中%0表示被执行的bat文件本身，%1~%9表示第1到第9个命令行参数。
如果参数个数超过10个，可以用shift命令左移，这个时候%1表示第二个参数，%9表示第10个参数，一次类推。
比如下面的程序段用来获取完整的命令行参数字符串。（完成此功能一个更好的办法是用%*）
set CMD_LINE_ARGS=
:setArgs
if ""%1""=="""" goto doneSetArgs
set CMD_LINE_ARGS=%CMD_LINE_ARGS% %1
shift
goto setArgs
:doneSetArgs


@ 与%VAR%相关的变量
%VAR:str1=str2%   会将VAR中的str1替换为str2(str2如果为空则可以达到删除的效果,str1前可以加*，变量%ABC:*B=%是C)
%VAR:~0,-2%          会提取VAR 变量的所有字符，除了最后两个
%VAR:~-2%             会提取VAR 变量的最后两个

系统变量:
他们的值由系统将其根据事先定义的条件自动赋值,我们只需要调用而已

%ALLUSERSPROFILE% （allusersprofile)本地 返回“所有用户”配置文件的位置。 C:Documents and SettingsAll Users

%APPDATA% (appdata)本地返回默认情况下应用程序存储数据的位置。 C:Documents and SettingsAdministratorApplication Data

%CD% (cd)本地返回当前目录字符串。 C:Documents and SettingsAdministrator桌面

%CMDCMDLINE% (cmdcmdline)本地返回用来启动当前的 Cmd.exe 的准确命令行。 cmd /c ""C:Documents and SettingsAdministrator桌面a.bat" "

%CMDEXTVERSION%(cmdextversion)系统返回当前的“命令处理程序扩展”的版本号。2

%COMPUTERNAME% (computername)系统返回计算机的名称。 xxxx

%COMSPEC% (comspec) 系统返回命令行解释器可执行程序的准确路径。 C:WINDOWSsystem32cmd.exe

%DATE% 系统返回当前日期。使用与 date /t 命令相同的格式。由 Cmd.exe 生成。有关 date 命令的详细信息，请参阅 Date。

%ERRORLEVEL% (errorlevel) 系统返回上一条命令的错误代码。通常用非零值表示错误。

%HOMEDRIVE% (homedrive)系统返回连接到用户主目录的本地工作站驱动器号。基于主目录值而设置。用户主目录是在“本地用户和组”中指定的。 C:

%HOMEPATH% (homepath) 系统返回用户主目录的完整路径。基于主目录值而设置。用户主目录是在“本地用户和组”中指定的。 Documents and SettingsAdministrator

%HOMESHARE% (homeshare) 系统返回用户的共享主目录的网络路径。基于主目录值而设置。用户主目录是在“本地用户和组”中指定的。

%LOGONSERVER% (logonserver) 本地返回验证当前登录会话的域控制器的名称 \ xxxx

%NUMBER_OF_PROCESSORS% (numeer_of_processors) 系统指定安装在计算机上的处理器的数目。

%OS% (os)系统返回操作系统名称。Windows 2000 显示其操作系统为 Windows_NT。

%PATH% (path)系统指定可执行文件的搜索路径。

%PATHEXT% (pathext)系统返回操作系统认为可执行的文件扩展名的列表。 .COM .EXE .BAT .CMD .VBS .VBE .JS .JSE .WSF .WSH

%PROCESSOR_ARCHITECTURE% (processor_architecture) 系统返回处理器的芯片体系结构。值：x86 或 IA64 基于Itanium x86

%PROCESSOR_IDENTFIER% (processor_identfier)系统返回处理器说明。

%PROCESSOR_LEVEL% (processor_level)系统返回计算机上安装的处理器的型号。 15

%PROCESSOR_REVISION% (processor_revision)系统返回处理器的版本号。 4f02

%PROMPT% (prompt)本地 返回当前解释程序的命令提示符设置。由 Cmd.exe 生成。$P$G

%RANDOM% (random)系统返回 0 到 32767 之间的任意十进制数字。由 Cmd.exe 生成。 30580

%SYSTEMDRIVE% (systemdrive)系统返回包含 Windows server operating system 根目录（即系统根目录）的驱动器。 C:

%SYSTEMROOT% (systemroot)系统返回 Windows server operating system 根目录的位置。C:WINDOWS

%TEMP%(temp) C:DOCUME~1ADMINI~1LOCALS~1Temp和 %TMP% (tmp）C:DOCUME~1ADMINI~1LOCALS~1Temp系统和用户返回对当前登录用户可用的应用程序所使用的默认临时目录。有些应用程序需要 TEMP，而其他应用程序则需要 TMP。

%TIME% 系统 返回当前时间。使用与 time /t 命令相同的格式。由 Cmd.exe 生成。有关 time 命令的详细信息，请参阅 Time。

%USERDOMAIN% （userdomain)本地返回包含用户帐户的域的名称。 xxxx

%USERNAME% (username)本地返回当前登录的用户的名称。 Administrator

%USERPROFILE% (userprofile)本地返回当前用户的配置文件的位置。 C:Documents and SettingsAdministrator

%WINDIR%(windir) 系统 返回操作系统目录的位置。 C:WINDOWS
