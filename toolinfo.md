#toolinfo
##linux 编译环境
### 基本命令
####重定向
```
./game -console | tee install.log
```

#### 解压文件


```
tar xzvf ntfs-3g-***.tar.gzgit
```
#### 源代码编译和安装软件
```
--下面指定了软件安装在 /usr/local中
tar -xvf xxxx.tgz
./configure --prefix=/opt/xxxx
or
./configure --prefix=/usr/local
然后
make
sudo make install
```
#### scp
```
scp nhmj_server_15/ wuhaifeng@192.168.10.201:~/gitDevlp/配置保存/dymj/self/
#### 
```


#### 杀死制定的端口的程序
kill -9 20009


#### vim 快捷键
```
1）单行复制
    在命令模式下，将光标移动到将要复制的行处，按“yy”进行复制；
2、粘贴
在命令模式下，将光标移动到将要粘贴的行处，按“p”进行粘贴
Ctrl + u 清除一行
Ctrl + y 恢复前面清除的那行
Ctrl-a 	移动光标到行首。
Ctrl-e 	移动光标到行尾。
Ctrl-f 	光标前移一个字符；和右箭头作用一样。
Ctrl-b 	光标后移一个字符；和左箭头作用一样。
Alt-f 	光标前移一个字。
Alt-b 	光标后移一个字。
Ctrl-l 	清空屏幕，移动光标到左上角。clear 命令完成同样的工作。
Ctrl+r 恢复上一步被撤销的操作
```


#### 上一个命令是否运行成功
```
$?
```


#### shell 脚本远程执行
```
ssh user@server bash < script.sh  远程执行 script.sh 的脚本

``` 


#### 给普通用户添加root权限
echo "wuhaifeng ALL=(ALL)ALL">> /etc/sudoers


#### yum 
```
yum install mysql-community-server
java 版本删除和替换
yum remove java
yum search openjdk
yum -y install java-1.8.0-openjdk

--yum 学习文档
https://www.cnblogs.com/vathe/p/6736094.html
```


#### gdb
```
gdb ./cxmj_hall core.1000 查看core文件
where 或者 bt 定位错误信息
```

### iptables
```
vim /etc/sysconfig/iptables
service iptables restart
systemctl restart iptables.service
```


### systemctl
```
systemctl: --CentOS 7 系统服务启动、重启、设置服务启动项命令以合并为,systemctl 
sudo systemctl enable sshd  --注册sshd 这样再/ect/init.d 就能看到启动item

启动对应的服务器
sudo systemctl start sshd

开机启动对应的服务：
chkconfig sshd on
```


###动态库查找方法



#### 设置方法
1. 方法1：
1.1：当前bash中临时修改
export LD_LIBRARY_PATH="/home/wuhaifeng/develop/curl-7.54.0/lib:$LD_LIBRARY_PATH"

1.2： 永久修改
在 ~/.bashrc 进行变量设置

2. 方法2:
/etc/ld.so.conf 
/sbin/ldconfig



#### 基本问题定位
启动软件失败，找不到动态库
1: 在/etc/ld.so.conf中加入/usr/local/lib这一行
2: 再运行：/sbin/ldconfig –v更新一下配置即可

### PATH 路径设置
1. 临时方法：
export PATH=$PATH:/usr/local/go/bin  
2. 永久方法：
vim ~/.bashrc ---用户级别进行设置
export PATH=$PATH:/usr/local/go/bin
source ~/.bashrc  --进行生效


### 安装字体
1. 将要的字体复制到/usr/share/fonts/chinese/TrueType目录下
2. 修改字体权限，使root以外的用户可以使用这些字体。 给字体使用666的权限
3. 建立字体缓存，命令：cd /usr/share/fonts/chinses/TrueType  # mkfontscale  # mkfontdir  # fc-cache  -fv  查看安装的字体  #fc-list :lang=zh


### 设备挂载
1. 查看下分区表的name
fdisk -l 
   设备 Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048  3907024895  1953511424    7  HPFS/NTFS/exFAT

2. 进行挂载
mount -t ntfs-3g /dev/sdc1 /mnt/Windows


### 远程连接pc
1. 方法1 rdesktop
rdesktop  -a 16 192.168.10.26:3389 -u zhongzhong -p 123456 -a 16 -g 1200x1560 -r sound:off -5


### screen

screen -S "xsmj" //creat screen
screen -ls:查看已经开启的(用screen开启的窗口）
screen -D -r 1000:进入开启的screen 窗口
进入screen 窗口后，
ctrl+a c:复制一个窗口
ctrl+a p:切换窗口（前一个窗口）
ctrl+a d:从screen 窗口退出
C-a [ 进入拷贝/回滚模式  然后输入esc就恢复正常

Ctrl-a <Esc> 进入选择模式
<PageUp> 或 Ctrl-u 光标上移一页
<PageDown> 或 Ctrl-d 光标下移一页
<Left> 或 h 光标左移一格
<Down> 或 j 光标下移一行
<Up> 或 k 光标上移一行
<Right> 或 l 光标右移一格
<Space> 选择开始，选择结束
<Esc> 退出选择模式
Ctrl-a ] 粘贴选择的内容


### tmux

```
鼠标滚屏
⌃b [ 快捷键进入 copy 模式，
然后使用翻页、字符定位来选择需要的字符

会话操作
tmux ls # 列出所有 tmux 会话
tmux a -t foo # 恢复名称为 foo 的会话，会话默认名称为数字
tmux kill-session -t foo # 删除名称为 foo 的会话

tmux new -s foo # 新建名称为 foo 的会话
tmux a # 恢复至上一次的会话
tmux kill-server # 删除所有的会话

copy:
ctrl+b [ copy
ctrl+b ] cppy to
shift
shift + insert
窗格操作
	% 左右平分出两个窗格

	" 上下平分出两个窗格

	x 关闭当前窗格

	{ 当前窗格前移

	} 当前窗格后移

	; 选择上次使用的窗格

	o 选择下一个窗格，也可以使用上下左右方向键来选择

	space 切换窗格布局，tmux 内置了五种窗格布局，也可以通过 ⌥1 至 ⌥5来切换

	z 最大化当前窗格，再次执行可恢复原来大小

	q 显示所有窗格的序号，在序号出现期间按下对应的数字，即可跳转至对应的窗格

```

## windows


###远程拷贝失效问题
关闭进程
在windows 服务器 -> 打开任务管理器 -> 查找 rdpclip.exe 进程 -> 结束此进程。

启动进程
开始 -> 运行 -> 输入 rdpclip.exe 并回车重新运行此程序。


### 添加静态路由
```
// 192.168.10.73是本机ip， 192.168.10.1是路由网关
route add 192.168.10.73 mask 255.255.255.255 192.168.10.1 metric 1

// 抓包完成后，删除该表项
route delete 192.168.10.73
```


### cmd 设置代理
```
set http_proxy=http://127.0.0.1:1080
set https_proxy=127.0.0.1:1080
```


### 查看端口是否被占用
```
netstat -ano | findstr "6002"
netstat   -anp | grep 
kill - 9 24233
```


## password


### sy
1. svn和禅道的账号密码
 ```
 用户名: wuhaifeng 
 密码：Sy20171009
 ```

2. gerrit
    ```
    你的用户名为：wuhaifeng 

    密码为：20000400

    http://192.168.1.130/r/#/, 
    
    ```
3. 多肉svn 
    http://192.168.20.79:18080/svn/duorou  
    
    http://192.168.20.79:18080/svn/duorou/trunk/策划文档/配置 
    http://192.168.20.79:18080/svn/duorou/trunk/serverpack/test 
    
4. wifi 密码
    20131109    


## 内网维护


### 192.168.20.35 --内网数据库
192.168.20.35
Zgxl777shoyoonet

### 192.168.10.252 --内网服务器
### whf-bj 
192.168.10.203

### 登入服务器重启
```
ssh root@192.168.20.248
yes
123456
redis-cli
auth 123456
pubsub channels
publish zsmj reload_table:t_config_app
exit
```

## 工具使用

### client hot update
#### literacy hot update
地址：
http://192.168.20.251:8080/jenkins/job/fn_dn_js_resource_gen/
para： literacy  dev

客户端热更：    
http://192.168.20.35:12398/BranchUpdate
密码： shoyoonet


####策划验收
```
客户端预览流程，针对不需要热更到客户端App的稳定版本：

打开Mac屏幕共享 --> 输入“vnc://192.168.1.62/” --> 点击连接 --> 用户名：“duanwei” 密码：“123” --> 点击连接 --> 操作“git checkout .”、“git pull”命令 --> creator重新打开 --> 通知策划验收，验收地址“http://192.168.1.62:7456”

本地开发版本地址不建议公开给策划做验收
```

### mysql
```
systemctl start mysqld  启动 MySQL：
systemctl stop mysqld  停止MySQL：
systemctl restart  mysqld
systemctl status mysqld  查看 MySQL 运行状态：
systemctl enable mysqld 设置开机:


exam:
更新指定ID的房卡：
use local_mj_publicdatabase;
select RoomCard, Name, UserId from t_account where UserId = 12153;
update t_account set RoomCard = 500 where UserId = 12153;

房间异常关闭客户端没有推出s
use local_mj_publicdatabase;
select * from t_account where UserId = 12153;
update t_account set RoomServerType = 0, RoomServerId = 0, RoomId = 0,  OnlineServer = 0 where UserId = 12153;

use local_xsmjdatabase;
select * from t_room where IsOver = 0 and RoomAllUser like "%12153%";
select * from t_room where IsOver = 0;
update t_room set IsOver = 1 where IsOver = 0 and RoomAllUser like "%12153%";


远程登入mysql服务器
mysql -h 192.168.20.248 -P 3306 -u root -p123456   
mysql -u root       //进入本地数据库

info:
执行SQL脚本
1： 在未连接SQL的情况下执行
mysql -h localhost -u root -p 123456  < d:\book.sql\\回车即可；
方式2：连接MYSQL的情况下执行
\. showTable.sql

获取列名
select COLUMN_NAME from information_schema.COLUMNS where table_name = 'your_table_name' and table_schema = 'your_db_name';

命令：
describe students;  //使用 describe 表名; 命令可查看已创建的表的详细信息
show create table students;  //显示创建表语句

SELECT DATEDIFF(NOW(), VisitTime), VisitTime, UserId FROM `t_visit_history` WHERE DATEDIFF(NOW(), VisitTime) > 7

select:
select * from students where name like "%t%";  ---通配符是%

SELECT COUNT(*), UserId FROM `t_collection_user` 
WHERE UserId IN(10043, 10047, 10055) 
GROUP BY UserId

SELECT Company, OrderNumber FROM Orders ORDER BY Company desc, OrderNumber limit 1----排序显示并只显示一个以Company排序后然后再以OrderNumber进行排序

更新：
update students set age = age + 2 where id = 2 or id = 1;

创建后表的修改：
语法：
 alter table 表名 add 列名 列数据类型 [after 插入位置];  ---添加列
示例：
 alter table students add address char(60);

表格更新：
 alter table 表名 change 列名称 列新名称 新数据类型;
将表 tel 列改名为 telphone: alter table students change tel telphone char(13) default "-";

insert:
insert into students (name, sex, age) values("孙丽华", "女", 21);

//插入的时候有重复的KEY的情况
insert into students (id, name,sex,age)values(3, "default", "man", "1") on duplicate key update age = age + 1, name = 'whf';


3: 返回值直接用unix_timestamp进行处理
select id, unix_timestamp(mdyTime) from students;

INNER JOIN://有时为了得到完整的结果，我们需要从两个或更多的表中获取结果。我们就需要执行 join
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName

SQL UNION
简单说明：
UNION 操作符用于合并两个或多个 SELECT 语句的结果集。
请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

示例：
SELECT E_Name FROM Employees_China  //另外，UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。
UNION   ////默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。
SELECT E_Name FROM Employees_USA

//FOREIGN KEY--一个表中的 FOREIGN KEY 指向另一个表中的 PRIMARY KEY。
CREATE TABLE Orders
(
Id_O int NOT NULL,
OrderNo int NOT NULL,
Id_P int,
PRIMARY KEY (Id_O),
FOREIGN KEY (Id_P) REFERENCES Persons(Id_P)
)

//CHECK--对具体列中值的限定
CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT chk_Person CHECK (Id_P>0 AND City='Sandnes')
)

索引//
创建一个简单的索引，名为 "PersonIndex"，在 Person 表的 LastName 列：
CREATE INDEX PersonIndex ON Person (LastName) 

//通过使用 DROP 语句，可以轻松地删除索引、表和数据库。

//GROUP BY 语句用于结合合计函数，根据一个或多个列对结果集进行分组
select name, sum(age) from students group by name;

//在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与合计函数一起使用。 this is error *** where name > sum
select name, sum(age) from students group by name having sum(age) > 32;

--tobo 数据库的备份和恢复
SELECT *
INTO Persons_backup
FROM Persons



4: 创建表
create table students
	（
		id int unsigned not null auto_increment primary key,
		name char(8) not null DEFAULT '',
		sex char(4) not null,
		age tinyint unsigned not null,
		tel char(13) null default "-"
	)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```


### node js


####基本命令
```
npm init
sudo npm install mysql
typings install dt~mocha --save
npm install --save lodash @types/lodash
```


### iterm2

```
command + t	新建标签
command + w	关闭标签
command + 数字 command + 左右方向键	切换标签
command + enter	切换全屏
command + f	查找
command + d	垂直分屏
command + shift + d	水平分屏
command + option + 方向键 command + [ 或 command + ]	切换屏幕
command + ;	查看历史命令
command + shift + h	查看剪贴板历史
ctrl + u	清除当前行
ctrl + l	清屏
ctrl + a	到行首
ctrl + e	到行尾
ctrl + f/b	前进后退
ctrl + p	上一条命令
ctrl + r	搜索命令历史
```


### zip
zip -q -r -e -m -o myfile.zip someThing


### curl


####基本使用
```
CHCP 65001 --中文不会乱码
curl -d "package="com.baida.duorou.wechatgame"&version="1.0.0"&gameid=22&playerid=10223&nickname="10223"&goodsid="com.baida.duorou.ios.6.240"&devicemodel=&devicename=&deviceid="d0819a05-dc86-17cf-77f7-c32bf4dd8fc0"&systemversion=&systemname=&sign="cafbb4148433e8e916e15b133dcb99b6"" http://192.168.10.26:63841/WeChatGameRecharge
```


### beycompare



#### linux 版本破解
```
rm -rf ~/.config/bcompare/registry.dat
```


###  lua


#### 快捷键
   Ctrl + P -----------菜单上的解释是gotoanythings，用"#"匹配，
	Ctrl+Shift +k -----------删除一行
	Ctrl + 回车 -----------添加一行空行jjjjjkkj
	Ctrl + Shift +V --------粘贴过程中保持缩进
	Alt + F3 ---------------选中选择的词
	Ctrl + H ---------------替换
	Ctrl + Shift + D ---------复制这行文本

### visual studio 


#### 快捷键
ctrl + pageup
ctrl + pagedown

mac 上 netbeans keymap 扩张

#### vim 快捷键

##### 1. 网站： 


<https://github.com/VSCodeVim/Vim/blob/master/ROADMAP.md/>


<https://linuxtoy.org/archives/efficient-editing-with-vim.html>


##### 2. usefull
* 光标移动
    w：光标往前移动一个词。
    b：光标往后移动一个词。
    0：移动光标到当前行首。
    ^：移动光标到当前行的第一个字母位置。
    $：移动光标到行尾。
    fx：移动光标到当前行的下一个 x 处。很明显，x 可以是任意一个
*  在整个文件里面有效移动光标
    H：移动光标到屏幕上面
    M：移动光标到屏幕中间
    L：移动光标到屏幕下面
    /text：从当前光标处开始搜索字符串 text，并且到达 text 出现的地方。必须使用回车来开始这个搜       索命令。如果想重复上次的搜索的话，按 n。
？text：和上面类似，但是是反方向。

有效的移动大段的文本
使用可视选择（visual selections）和合适的选择模式
不像最初的 VI，Vim 允许你高亮（选择）一些文本，并且进行操作。这里有三种可视选择模式：

v：按字符选择。经常使用的模式，所以亲自尝试一下它。
V：按行选择。这在你想拷贝或者移动很多行的文本的时候特别有用。
<C-V>：按块选择。非常强大，只在很少的编辑器中才有这样的功能。你可以选择一个矩形块，并且在这个矩形里面的文本会被高亮。
在选择模式的时候使用上面所述的方向键和命令（motion）。比如，vwww，会高亮光标前面的三个词。Vjj 将会高亮当前行以及下面两行。

在可视选择模式下剪切和拷贝
一旦你高亮了选区，你或许想进行一些操作：

d：剪贴选择的内容到剪贴板。
y：拷贝选择的内容到剪贴板。
c：剪贴选择的内容到剪贴板并且进入插入模式。

 select word: viw
 当前行放在视窗正中心: zz
 scrolling 行: ctrl+e, ctrl+y
 
### netbeans


#### 快捷键
```
自动对齐：Alt + Shift + F
Ctrl + Q 移动到上次编辑的地方
删除整行：Ctrl + E，删除的为光标所在的整行。
查找文档 ctrl + shift + space
ctrl + b:   转到声明
编辑：
alt + s 选择单词
shift + end / home 选择行或者行尾

书签
contrl+M enable mark or dis
contrl+shift+m  删除当前文档中的书签
contrl+ shift+,  --上一个书签历史记录 
contrl+shift+.  --下一个书签历史记录
f2 --next mark
shift f2---last mark

```


### subline 


#### 快捷键
```
ctrl+alt+a  自动对齐
ctrl+m      找到匹配的括号

maker:
f2
```

### svn


#### 基本命令
```
svn add test.php ＜－ 添加test.php 
svn commit -m “添加我的测试用test.php“ test.php
svn revert friend.proto  恢复指定的文件
```

### cocos

### git


#### 配置
```
git config --global user.name “wuhaifeng”
git config --global user.email wuhaifeng@shoyoo.com
git config --global color.ui true
git config --global alias.ci "commit“
git config --global alias.co "checkout“
git config --global alias.br "branch“
git config --global alias.st "status“
git config --global alias.cp "cherry-pick“
git config core.ignorecase false
```

#### 基本命令
```
版本库中删除指定文件但是本地还是存在
1： ignre文件中新增指定目录
2： git rm -r --cached

merge:
合并dev分支到当前分支-----no-ff参数，表示禁用“Fast forward”：
git merge --no-ff -m "merge with no-ff" dev

branch:
git co -b branchA:创建分支branchA并进行切换
git co -b nbmj_proto origin/nbmj_proto:拉远程分支到本地
git br --set-upstream brname origin/brname
git branch -a :查看所有分支
git checkout master   :---切换分支
git br -d brname:本地分支删除
git push origin lan_sync_xsmj:推本地分支到远程

cherry-pick:
git cherry-pick commitid
git clone ssh://yuanshuangli@192.168.1.130:29418/alachess_server:远程仓库到本地

add：
git add .  --包括了所有的文件
git add -u  --不包括新文件--提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)

stash:
git stash apply
git stash drop
git stash list

patch:
	//1:利用两个提交的不同来生产path
			 commitID1  comitID2
	git diff acb8cd15   4ff35d80  > patch

	2: 利用working 区域和 index 区域的不同来生成path
	git diff > patch
	git apply patch


log mdy: 
增补提交//把当前index 进行增补修改
git ci --amend

多个提交进行合并：
5: git rebase -i commit-ID 

gitdiff
1.4 比较工作区与指定commit-id的差异
git diff commit-id  [<path>...]

```


### markdown 快捷键
#### 快捷键
* 插入代码 `CMD + Shift + K`
* 插入图片 `Control + Shift + I`

 
## todo
### 1. mac git 不能自动补全




