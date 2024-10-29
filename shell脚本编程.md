# helloworld

~~~shell
#!/bin/bash
# This is ower first shell
# by author rivers 2021.09
echo "hello world"
~~~

# 变量

变量分为三种(所有的变量全是字符串,算数运算需要通过命令)

系统变量

~~~shell
# Shell常见的变量之一系统变量，主要是用于对参数判断和命令返回值判断时使用，系统变量详解如下：

$0 		当前脚本的名称；
$n 		当前脚本的第n个参数,n=1,2,…9；
$* 		当前脚本的所有参数(不包括程序本身)；
$# 		当前脚本的参数个数(不包括程序本身)；
$? 		令或程序执行完后的状态，返回0表示执行成功；
$$ 		程序本身的PID号。
~~~

环境变量

~~~shell
#Shell常见的变量之二环境变量，主要是在程序运行时需要设置，环境变量详解如下：

PATH  		命令所示路径，以冒号为分割；
HOME  		打印用户家目录；
SHELL 		显示当前Shell类型；
USER  		打印当前用户名；
ID    		打印当前用户id信息；
PWD   		显示当前所在路径；
TERM  		打印当前终端类型；
HOSTNAME    显示当前主机名；
PS1         定义主机命令提示符的；
HISTSIZE    历史命令大小，可通过 HISTTIMEFORMAT 变量设置命令执行时间;
RANDOM      随机生成一个 0 至 32767 的整数;
HOSTNAME    主机名
~~~

用户变量

~~~shell
# 常见的变量之三用户变量，用户变量又称为局部变量，主要用在Shell脚本内部或者临时局部使用，系统变量详解如下：
a=rivers 				       自定义变量A；
Httpd_sort=httpd-2.4.6-97.tar  自定义变量N_SOFT；
BACK_DIR=/data/backup/         自定义变量BACK_DIR；
IPaddress=10.0.0.1			   自定义变量IP1；

~~~

# echo -e扩展

~~~shell
#!/bin/bash
# This is echo color shell
# by author rivers 2021.09-23
# 字体颜色
for i in {31..37}; do
echo -e "\033[$i;40mHello world!\033[0m"
done
# 背景颜色
for i in {41..47}; do
echo -e "\033[47;${i}mHello world!\033[0m"
done
# 显示方式
for i in {1..8}; do
echo -e "\033[$i;31;40mHello world!\033[0m"
done
~~~

# if

~~~shell
# If条件判断语句，通常以if开头，fi结尾。也可加入else或者elif进行多条件的判断

# 单分支语句 ---比较大小
	if (条件表达式);then
		语句1
	fi

# 双分支if 语句
	if (表达式)
		语句1
	else
		语句2
	fi

# 多支条件语句 ---判断成绩
	if (表达式)
		语句1
	elif
		语句2
	elif
		语句2
	fi  
~~~

逻辑判断标识符

~~~shell
-f	 	判断文件是否存在 eg: if [ -f filename ]；
-d	 	判断目录是否存在 eg: if [ -d dir     ]；
-eq		等于，应用于整型比较 equal；
-ne		不等于，应用于整型比较 not equal；
-lt		小于，应用于整型比较 letter；
-gt		大于，应用于整型比较 greater；
-le		小于或等于，应用于整型比较；
-ge 	大于或等于，应用于整型比较；
-a		双方都成立（and） 逻辑表达式 –a 逻辑表达式；
-o		单方成立（or） 逻辑表达式 –o 逻辑表达式；
-z		空字符串；
-x      是否具有可执行权限
||      单方成立；
&&      双方都成立表达式。
~~~

判断crond服务是否运行

~~~shell
#!/bin/bash
# this is check crond
# by author rivers on 2021-9.23

# 定义一个变量名
name=crond
# -v 反转查找 -c 计算符合条件的列数
num=$(ps -ef|grep $name|grep -vc grep)
if [ $num -eq 1 ];then
    echo "$num running!"
else
    echo "$num is not running!"
fi
~~~

判断系统目录是否存在

~~~shell
#!/bin/bash
# this is check directory 
# by author rivers on 2021-9.27 
# -d 判断一个目录是否存在 -a 关系 ! 取反
if  [  !  -d  tmp  -a  !  -d  tmp  ];then
         mkdir  -p  tmp  
fi
~~~

~~~shell
# if 语句可以直接对命令状态进行判断，就省去了获取$?这一步！
# 如果第一个条件符合就不再向下匹配
#!/bin/bash
# this check grade shell
# by author rivers on 2021-09-27

grade=$1
if [ $grade -gt 90 ];then
  echo "Is's very good!"
elif [ $grade -gt 70 ];then
  echo "Is's is good!"

elif [ $grade -ge 60 ];then
  echo "pass"

else
  echo "no pass"
fi
~~~

# for

~~~shell
#格式：for name [ [ in [ word ... ] ] ; ] do list ; done
  for 变量名 in 取值列表; do
    语句 1
  done
~~~

检查同一局域网 多台主机是否存活

~~~shell
#!/bin/bash
# check hosts is on/Off
# by rivers on 20219-23

Network=$1
for Host in $(seq 1 10); do
    ping -c 1 $Network.$Host >/dev/null && result=0 || result=1

    if [ "$result" == 0 ]; then
        echo -e "\033[32;1m$Network.$Host is up \033[0m"
        echo "$Network.$Host" >>/tmp/up.txt

    else
        echo -e "\033[;31m$Network.$Host is down \033[0m"
        echo "$Network.$Host" >>/tmp/down.txt
    fi
done
~~~

# while

~~~shell
# While循环语句与for循环功能类似，主要用于对某个数据域进行循环读取、对文件进行遍历，通常用于需要循环某个文件或者列表，满足循环条件会一直循环，不满足则退出循环，其语法格式以while…do开头，done结尾与 
#while 关联的还有一个 until 语句，它与 while 不同之处在于，是当条件表达式为 false 时才循环，实际使用中比较少，这里不再讲解。

while  (表达式)
do
  语句1
done
~~~

break 和 continue 语句
break 是终止循环。
continue 是跳出当前循环。

~~~shell
#!/bin/bash
#示例 1：在死循环中，满足条件终止循环
while true; do
    # let修饰的变量可以进行算数运算
    let N++
    if [ $N -eq 5 ]; then
        break
    fi
    echo $N
done
~~~

~~~shell
N=0
while [ $N -lt 5 ]; do
    let N++
    if [ $N -eq 3 ]; then
        continue
    fi
    echo $N
done
~~~

~~~shell
# 打印 1-100 数字
i=0
while ((i <= 100)); do
    echo $i
    i=$(expr $i + 1)
done
~~~

求1-100的总和

~~~shell
#!/bin/bash
# by author rivers on 2021-9-27
j=0
i=1
while ((i<=100))
do
     j=`expr $i + $j`
     ((i++))
done
echo $j
~~~

每十秒循环判断用户登陆

~~~shell
#!/bin/bash
#Check File to change. 
#By author rivers 2021-9-27
USERS="root"
while true
do
        echo "The Time is `date +%F-%T`"
        sleep 10
        NUM=`who|grep "$USERS"|wc -l`
        if [[ $NUM -ge 1 ]];then
                echo "The $USERS is login in system."
        fi
done
~~~

# case

~~~shell
#Case选择语句，主要用于对多个选择条件进行匹配输出，与if elif语句结构类似，通常用于脚本传递输入参数，打印出输出结果及内容，其语法格式以Case…in开头，esac结尾。语法格式如下：
case 模式名  in
  模式 1)
    命令
    ;;
  模式 2)
    命令
    ;;
*)
不符合以上模式执行的命令
esac
# 每个模式必须以右括号结束，命令结尾以双分号结束。
~~~

httpd服务启动脚本

~~~shell
#!/bin/bash

while true; do
    echo -e "
    \033[31m start \033[0m
    \033[32m stop \033[0m 
    \033[33m status \033[0m
    \033[34m quit \033[0m 
    "
    read -p "请输入你的选择 start|stop|quit|status：" char
    case $char in
    'start')
        systemctl start httpd && echo "httpd服务已经开启" || echo "开启失败"
        ;;
    'stop')
        systemctl stop httpd && echo "httpd服务已经关闭" || echo "关闭失败"
        ;;
    'restart')
        systemctl restart httpd && echo "httpd服务已经重启" || echo "重启失败"
        ;;
    'status')
        systemctl status httpd
        ;;
    'quit')
        break
        ;;
    *)
        echo "没有这个选项"
        ;;
    esac
done
~~~

~~~shell
#!/bin/bash

while true; do
    echo -e "
    \033[31m start \033[0m
    \033[32m stop \033[0m 
    \033[33m status \033[0m
    \033[34m quit \033[0m 
    "
    read -p "请输入你的选择 start|stop|quit|status：" char
    case $char in
    start)
        systemctl start httpd && echo "httpd服务已经开启" || echo "开启失败"
        ;;
    stop)
        systemctl stop httpd && echo "httpd服务已经关闭" || echo "关闭失败"
        ;;
    restart)
        systemctl restart httpd && echo "httpd服务已经重启" || echo "重启失败"
        ;;
    status)
        systemctl status httpd
        ;;
    quit)
        break
        ;;
    *)
        echo "没有这个选项"
        ;;
    esac
done
~~~

# select

~~~shell
#select 是一个类似于 for 循环的语句
#Select语句一般用于选择，常用于选择菜单的创建，可以配合PS3来做打印菜单的输出信息，其语法格式以select…in do开头，done结尾：

select i in （表达式） 
do
语句
done
~~~

~~~shell
# 选择mysql 版本
#!/bin/bash
# by author rivers on 2021-9-27
PS3="Select a number: "
while true; do
    select mysql_version in 5.1 5.6 quit; do
        case $mysql_version in
        5.1)
            echo "mysql 5.1"
            break
            ;;
        5.6)
            echo "mysql 5.6"
            break
            ;;
        quit)
            exit
            ;;
        *)
            echo "Input error, Please enter again!"
            break
            ;;
        esac
    done
done
~~~

~~~shell
#!/bin/bash
#by author rivers on 2021-9-27
PS3="Please enter you select install menu:"
select i in http php mysql quit; do
    case $i in
    http)
        echo -e "\033[31m Test Httpd \033[0m"
        ;;
    php)
        echo -e "\033[32m Test PHP\033[0m"
        ;;
    mysql)
        echo -e "\033[33m Test MySQL.\033[0m"
        ;;
    quit)
        echo -e "\033[32m The System exit.\033[0m"
        exit
        ;;
    esac
done
~~~

注意:输入的是1,2,3,4



# 案例



## 遍历当前目录下文件

~~~shell
#!/bin/bash

# 声明一个数组来存储文件列表
files=(*)

# 遍历数组并打印每个文件的名称
for file in "${files[@]}"; do
    # 检查文件是否是普通文件（可选，但有助于过滤目录和其他特殊文件）
    if [ -f "$file" ]; then
        echo "$file"
    fi
done

~~~



