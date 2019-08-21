---
# shell Command Learning
---
## Linux 资源
- [Linux 工具快速教程](http://linuxtools-rst.readthedocs.io/zh_CN/latest/)
- 采用[Sphinx](http://www.pythondoc.com/sphinx/index.html)结合[reStructuredText](http://docutils.sourceforge.net/rst.html)语言作为笔记记录。

<!--more-->

目前存在的问题就是shell中数据进制的解释问题，保证指定位数。

## 常用命令
### 命令参数
$0    脚本名称
$1-9　脚本执行时的参数1到参数9
$?	  脚本的返回值　　　　
$#	  脚本执行时，输入的参数的个数
$@	  输入的参数的具体内容（将输入的参数作为一个多个对象，即是所有参数的一个列表）
$*	  输入的参数的具体内容（将输入的参数作为一个单词）

### 查看文件数量
```bash
ls -l *.zip |grep "^-"|wc -l
```
### 批量解压
```bash
find . -name '*.zip' -exec unzip {} \;  
```
### cut
适合处理“以单个字符间隔”的文本内容，不利于多个空格的文本文件处理，学会综合使用 `awk` 及 `sed` 结合正则表达式实现文本文件的处理分析。

`paste` 可实现相同行数文件内容的左右合并，`cat` 一般实现文件内容的上下合并。
``` bash
-b ：以字节为单位进行分割。
    这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。
    支持形如3-5的写法，而且多个定位之间用逗号隔开。  
-c ：以字符为单位进行分割。
-d ：自定义分隔符，默认为制表符。
    利用 sed -n l [input] 判断识别空格和制表符。制表符显示为\t符号，空格原样显示。  
-f ：与-d一起使用，指定显示哪个区域。
-n ：取消分割多字节字符。
    仅和 -b 标志一起使用。若字符最后一个字节落在由 -b 标志的 List 参数指示的<br />范围之内，该字符将被写出；否则，该字符将被排除。
    cut命令若使用了-b选项，cut会先把-b后面所有的定位进行从小到大排序，然后再提取。可不能颠倒定位的顺序。
```

### gcc
GCC(GNU C Compiler or GNU Complier Collection)是GNU项目的编译器套件。能够编译C、C++和Objective C语言编写的程序。

GCC能够支持多种不同的C语言变体，比如ANSI C和传统(Kernighan和Ritchie，K&R)C。此外，GCC在g77的帮助下也能够编译Fortran程序，而用于支持Pascal，Modula 3，Ada 9X以及其他语言的编译器前端也在开发中。

使用GCC，程序员能够对编译过程有更多的控制。编译过程分为4个阶段：预处理，适当编译，汇编，连接。而程序员可以在编译的任何阶段结束后停止整个编译过程以检查或使用编译器在该阶段的输出信息。

#### 文件扩展名
`.c :` C语言源代码； 预处理、编译、汇编 
`.C/.cc/.cxx :` C++语言源代码； 预处理、编译、汇编 
`.m :` Objective C语言源代码； 预处理、编译、汇编 
`.i :` 预处理后的C语言源代码； 编译、汇编 
`.ii :` 预处理后的C++语言源代码； 编译、汇编 
`.s/.S :` 汇编语言源代码； 汇编 
`.h :` 预处理文件(标头文件)； (不常出现在指令行) 
其他扩展名的文件是由连接程序来处理，通常有： 
`.o  :` 编译后的目标代码(Object file) 
`.a/.so :` 编译后的库代码(Archive file) 

#### 命令行选项 
GCC可以接受的命令行选项长达数页，下列只列出了最常用的部分。 
`-o FILE:` 指定输出文件名，在编译为目标代码时，这一选项不是必须的。如果FILE没有指定，默认文件名是a.out 
`-c :` 只编译不连接 
`-D :` FOO=BAR 在命令行定义预处理宏FOO，其值为BAR 
`-I :` DIRNAME 将DIRNAME加入到包含文件的搜索目录列表中 
`-L :` DIRNAME 将DIRNAME加入到库文件的搜索目录列表中 
`-static :` 链接静态库，即执行静态链接默认情况下GCC只链接共享库 
`-l FOO :` 链接名为libFOO的函数库 
`-g :` 在可执行程序中包含标准调试信息 
`-ggdb :` 在可执行程序中包含只有GNU debugger(gdb)才能识别的大量调试信息 
`-O :` 优化编译过的代码 
`-ON :` 指定代码优化的级别为N，0~3，默认N=1 
`-ansi :` 支持ANSI/ISO C的标准语法，取消GNU的语法扩展中与该标准有冲突部分（但这一选项并不能保证生成ANSI兼容的代码） 
`-pedantic :` 允许发出ANSI/ISO C标准所列出的所有警告 
`-pedantic-errors :` 允许发出ANSI/ISO C标准所列出的所有错误 
`-traditional :` 支持K&R C 语法 
`-w :` 关闭所有警告，建议不要使用此项 
`-Wall :` 允许发出GCC能提供的所有有用的警告 
`-Werror :` 把所有警告转换为错误，以在警告发生时终止编译 
`-MM :` 输出一个make兼容的相关列表 
`-v :` 显示在编译过程的每一步中用到的命令 

### git
```bash
# -n：加上这个参数，执行命令时，是不会删除任何文件，而是展示此命令要删除的文件列表预览。
git rm -r -n --cached foldername
git rm -r --cached  foldername  # 最终执行命令
git commit -m 'remove folder all file out of control.'  # 提交
git push origin master  # 提交到远程服务器

eg： 每日自动推送到github（sync_to_github.sh）
#!/bin/bash
cd /home/aqf/tongqingqing/run_job/github
tim2=$(date +%Y%m%d)12
#tim2=$(date -d "1 day ago" +"%Y%m%d")12
fig=/home/aqf/tongqingqing/run_job/wrf_project/figure

rm -rf display/
git init
git clone https://github.com/Geek-007/display.git
cd display/
#mkdir WRF CMAQ CMAX WRFchem
cp -r ${fig}/${tim2} ./WRF/.
cat > README.md << EOF

# *NEC Weather Forecasting Experiment*
<br><br><br>
$(date) All Update
-------------------------------------------------------------
<br>
<table><tr>
<td><img src=https://github.com/Geek-007/display/blob/master/WRF/${tim2}/${tim2}_t2m.gif border=0></td>
<td><img src=https://github.com/Geek-007/display/blob/master/WRF/${tim2}/${tim2}_uv10m.gif border=0></td>
<td><img src=https://github.com/Geek-007/display/blob/master/WRF/${tim2}/${tim2}_rh2m.gif border=0></td>
</tr></table>
<table><tr>
<td><img src=https://github.com/Geek-007/display/blob/master/WRF/${tim2}/${tim2}_precip.gif border=0></td>
<td><img src=https://github.com/Geek-007/display/blob/master/WRF/${tim2}/${tim2}_snowfall.gif border=0></td>
<td><img src=https://github.com/Geek-007/display/blob/master/WRF/${tim2}/${tim2}_snowcover.gif border=0></td>
</tr></table>
<br>


EOF

mv README.md ./WRF/.

#git rm -r --cached 2019051312
#rm -rf  2019051312
git add -A
git commit -m ${tim2}
#git config --global user.email "1069093304@qq.com"
# git config --global user.name "geek-007"
git remote rm origin
git remote add origin git@github.com:Geek-007/display.git  #https://github.com/Geek-007/display.git
git push -u origin master
```

### iconv
文件编码修改，包括文件名及文件内容编码的转换
``` bash
# 文件内容编码变换
find *.TSM -exec sh -c "iconv -f GBK -t UTF8 {} -o UTF8/{}" \;
```

### mv
文件重命名
利用 `cut` 实现文件名的分隔及文件名指定字符截取
``` bash
for  i in `ls | grep HTTP`; do
    mv -f $i `echo $i | cut -d '&' -f 3 | cut -d '=' -f 2`
    # newName=`echo $i | cut -d '&' -f 3 | cut -d '=' -f 2`
    # mv $i $newName
done
```
``` bash
# 文件名前添加相应的字符串SDQD1
for i in `ls`;
    do mv -f $i `echo "GXWZ1_"$i`;
done
#
# 修改文件名前面四个字母为JSLY1
for i in `ls`;
    do mv -f $i `echo $i | sed 's/^..../FJXM/'`;
done
# 
# 修改文件名后面五个字母为JSLY1
for i in `ls`;
    do mv -f $i `echo $i | sed 's/.....$/P.TSM/'`;
done
```
``` bash
# 以下部分还有待于进一步测试。批量修改文件名，删除文件名中的某些字符。
for file in `ls *.jpg`;do mv $file `echo $file|sed 's/_finished//g'`;done;
ls *.jpg |awk -F "_finished" '{print "mv "$0" "$1$2""}'|bash
ls *.jpg |awk -F "_finished" '{print "mv "$0" "$1$2""}'
rename "_finished" "" *.jpg
for file in `ls *.jpg`;do mv $file `echo ${file%_finished*}.jpg`;done;
for file in `ls *.jpg`;do mv $file ${file%_finished*}.jpg;done;
```

### rename
文件重命名，空格去除
``` bash
find . -type f -name "* *" |
while read name; do
na=$(echo $name | tr ' ' '_')
mv "$name" "$na" 
done
```
sed 版本实现
``` bash
for f in *;do mv "$f" `echo "$f" | sed 's/[ ]\+/_/g' `; done
sed 's/[[:space:]]\+/_/g'
# sed里的出现一次或多次的加号是需要添加反斜杠的。即：\+
```
rename 版本实现
``` bash
rename 's/[ ]+/_/g' *
```

### sed
注意单引号和双引号的引用区别。
单引号：shell处理命令时，对其中的内容不做任何处理。即此时是引号内的内容是sed命令所定义的格式。
双引号：shell处理命令时，要对其中的内容进行算术扩展。如果想让shell扩展后得到sed命令所要的格式。
``` bash
# -i表示直接修改文件内容，不输出到终端
sed -i "s/GXWZ1/FJXM1/g" `ls`   # 目录下文件内容的全局修改
sed -i "s/GXWZ1/FJXM1/gi" $(ls) # 大小写不敏感
```
正则表达式认可的特殊字符有：
`. * [ ] ^ $ { } \ + ? | ( )`
这些特殊字符中的一个作为文本字符，需要在特殊字符前添加反斜杠字符\ 来转义它。
``` bash
sed -i s/gPhone\\AHHB1\\2014/Pressure/g `ls`
```

### tar
文件打包压缩及文件解压。
#### 参数说明
- 独立参数
`-c` : 建立压缩档案
`-x` : 解压
`-t` : 查看内容
`-r` : 向压缩归档文件末尾追加文件
`-u` : 更新原压缩包中的文件
这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。

- 可选参数
`-z` : 有gzip属性的
`-j` : 有bz2属性的
`-Z` : 有compress属性的
`-v` : 显示所有过程
`-O` : 将文件解开到标准输出
根据需要在压缩或解压档案时可选

- 必选参数-f
`-f` : 使用档案名字，切记，这个参数是**最后一个参数**，后面只能接档案名。

#### 压缩打包
``` bash
tar -zcvf name.tar.gz name
tar -jcvf name.tar.bz2 name
zip -ry name.zip name
# zip命令要加两个选项:
#   -r 表示递归目录，不然只压出来一个空目录
#   -y 表示保持符号链接，而不用把符号链接指向的文件也压进来
```
对比发现[压缩率](http://blog.csdn.net/kimsoft/article/details/8059578) `bzip2 > gzip > zip` 。zip的通用性较好，而现在windows下软件winrar,7zip等对tar.gz的支持也非常好。推荐用tar.gz，bzip2要耗费更多的CPU。

``` bash
# 批量解压
for tar in *.tar.gz; do
    tar xvf $tar;
done
```

#### [常用总结](http://www.cnblogs.com/qq78292959/archive/2011/07/06/2099427.html)
1. *.tar 用 tar -xvf 解压
2. *.gz 用 gzip -d或者gunzip 解压
3. *.tar.gz和*.tgz 用 tar -xzf 解压
4. *.bz2 用 bzip2 -d或者用bunzip2 解压
5. *.tar.bz2用tar -xjf 解压
6. *.Z 用 uncompress 解压
7. *.tar.Z 用tar -xZf 解压
8. *.rar 用 unrar e/x 解压，下载编译后[rar](http://www.rarsoft.com/download.htm)。
9. *.zip 用 unzip 解压

### [wget](https://java-er.com/blog/wget-useage-x/)
文件的断点续传(主要用于下载时间受限的文件资料)，结合 `curl` 使用。如果网址中包含特殊字符，则用双引号包含网址。
#### 下载文件
``` bash
# 针对性下载指定的文件
wget -k [web]
cat index.html | grep /raw | cut -d '"' -f 8 > wget.txt # 筛选指定位置的网址
wget --user=username --password=passwd -k [source_wget.txt] 
# 下载指定目录的文件
wget -m -c -np -nd -P prefix URL    # -m: 最大递归深度且不移走 .listing 文件,不要重新下载文件除非比本地文件新
# wget -m -c -np -nd -P data ftp://ftp.cgps.ac.cn/products/position/gamit/ 
# 下载网站附件
wget -r -erobots=off -l2 -np  http://soostrc.comet.ucar.edu/data/grib/gfs/20171203/grib.t12z/
```
#### 主要参数
`- P`: 表示下载的目标目录
`- r`: 表示递归下载
`-np`: 表示不下载旁站连接
`- k`: 表示将下载的网页里的链接修改为本地链接
`- p`: 获得所有显示网页所需的元素
`- c`: 断点续传
`-nd`: 递归下载时不创建一层一层的目录，把所有的文件下载到当前目录
`- L`: 递归时不进入其它主机，如wget -c -r [web]
`- A`: 指定要下载的文件样式列表，多个样式用逗号分隔
`- i`: 后面跟一个文件，文件内指明要下载的URL

#### 启动参数
`-V`: –version 显示wget的版本后退出
`-h`: –help 打印语法帮助
`-b`: –background 启动后转入后台执行
`-e`: –execute=COMMAND 执行’.wgetrc’格式的命令，wgetrc格式参见/etc/wgetrc或~/.wgetrc

#### 文件参数
`- o`: –output-file=FILE 把记录写到FILE文件中
`- a`: –append-output=FILE 把记录追加到FILE文件中
`- d`: –debug 打印调试输出
`- q`: –quiet 安静模式(没有输出)
`- v`: –verbose 冗长模式(这是缺省设置)
`-nv`: –non-verbose 关掉冗长模式，但不是安静模式
`- i`: –input-file=FILE 下载在FILE文件中出现的URLs
`- F`: –force-html 把输入文件当作HTML格式文件对待
`- B`: –base=URL 将URL作为在-F -i参数指定的文件中出现的相对链接的前缀
`–sslcertfile=FILE`: 可选客户端证书 –sslcertkey=KEYFILE 可选客户端证书的KEYFILE –egd-file=FILE 指定EGD socket的文件名

#### 下载参数
`-bind-address=ADDRESS`: 指定本地使用地址(主机名或IP，当本地有多个IP或名字时使用)
`- t`: –tries=NUMBER 设定最大尝试链接次数(0 表示无限制).
`- O`: –output-document=FILE 把文档写到FILE文件中
`-nc`: –no-clobber 不要覆盖存在的文件或使用.#前缀
`- c`: –continue 接着下载没下载完的文件
`-progress=TYPE`: 设定进程条标记
`-N`: –timestamping 不要重新下载文件除非比本地文件新
`-S`: –server-response 打印服务器的回应
`-T`: –timeout=SECONDS 设定响应超时的秒数
`-w`: –wait=SECONDS 两次尝试之间间隔SECONDS秒
`-waitretry=SECONDS`: 在重新链接之间等待1…SECONDS秒
`-random-wait`: 在下载之间等待0…2*WAIT秒
`-Y`: -proxy=on/off 打开或关闭代理
`-Q`: -quota=NUMBER 设置下载的容量限制
`-limit-rate=RATE`: 限定下载输率

#### 目录参数
`-nd`: –no-directories 不创建目录
`- x`: –force-directories 强制创建目录
`-nH`: –no-host-directories 不创建主机目录
`- P`: –directory-prefix=PREFIX 将文件保存到目录 PREFIX/…
`-cut-dirs=NUMBER`: 忽略 NUMBER层远程目录

#### HTTP 选项参数
`-http-user=USER`: 设定HTTP用户名为 USER.
`-http-passwd=PASS`: 设定http密码为 PASS
`-C`: –cache=on/off 允许/不允许服务器端的数据缓存 (一般情况下允许)
`-E`: –html-extension 将所有text/html文档以.html扩展名保存
`-ignore-length`: 忽略 ‘Content-Length’头域
`-header=STRING`: 在headers中插入字符串 STRING
`-proxy-user=USER`: 设定代理的用户名为 USER
`proxy-passwd=PASS`: 设定代理的密码为 PASS
`referer=URL`: 在HTTP请求中包含 ‘Referer: URL’头
`-s`: –save-headers 保存HTTP头到文件
`-U`: –user-agent=AGENT 设定代理的名称为 AGENT而不是 Wget/VERSION
`no-http-keep-alive`: 关闭 HTTP活动链接 (永远链接)
`cookies=off`: 不使用 cookies
`load-cookies=FILE`: 在开始会话前从文件 FILE中加载cookie
`save-cookies=FILE`: 在会话结束后将 cookies保存到 FILE文件中

#### FTP 选项参数
`-nr`: –dont-remove-listing 不移走 `.listing` 文件
`- g`: –glob=on/off 打开或关闭文件名的 globbing机制
`passive-ftp`: 使用被动传输模式 (缺省值).
`active-ftp`: 使用主动传输模式
`retr-symlinks`: 在递归的时候，将链接指向文件(而不是目录)

#### 递归下载参数
`-r`: –recursive 递归下载－－慎用!
`-l`: –level=NUMBER 最大递归深度 (inf 或 0 代表无穷)
`-delete-after`: 在现在完毕后局部删除文件
`-k`: –convert-links 转换非相对链接为相对链接
`-K`: –backup-converted 在转换文件X之前，将之备份为 X.orig
`-m`: –mirror 等价于 -r -N -l inf -nr
`-p`: –page-requisites 下载显示HTML文件的所有图片
递归下载中的包含和不包含(accept/reject)：
`-A`: –accept=LIST 分号分隔的被接受扩展名的列表
`-R`: –reject=LIST 分号分隔的不被接受的扩展名的列表
`-D`: –domains=LIST 分号分隔的被接受域的列表
`-exclude-domains=LIST`: 分号分隔的不被接受的域的列表
`-follow-ftp`: 跟踪HTML文档中的FTP链接
`-follow-tags=LIST`: 分号分隔的被跟踪的HTML标签的列表
`-G`: –ignore-tags=LIST 分号分隔的被忽略的HTML标签的列表
`-H`: –span-hosts 当递归时转到外部主机
`-L`: –relative 仅仅跟踪相对链接
`-I`: –include-directories=LIST 允许目录的列表
`-X`: –exclude-directories=LIST 不被包含目录的列表
`-np`: –no-parent 不要追溯到父目录
``` bash
wget -S –spider URL # 不下载只显示过程
```

#### 使用技巧
对于本地电脑的内存问题，打不开很大的网页，可以通过使用 `wget -k web` 拉取该网页，通过文本的分析的方式打开。
``` bash
# 下面的账户密码需要一定程度的修改处理。该网页大小达7Mb左右，当前 ()2017年12月18日10:25:26 链接30103行。
wget -k --ftp-user=CRYOSAT722(small) --ftp-password=UIJMmwpa_修改 ftp://science-pds.cryosat.esa.int/SIR_GDR/ALL/
cat index.html | grep /CS | cut -d '"' -f 2 > cryosat.txt
```

#### 格式转换
wget 仅实现拉取远程文件，无法解析源码文件。对于HTML格式的文件可以采用正则表达式替换源码以及采用 `html2text` 实现格式转化，两种方法转换均不太完全。
``` bash
sed -e 's/<[^>]*>//g' > downloaded_file.txt
```

#### 使用示例
文件批量下载并且重命名文件
``` bash
#!/bin/bash
while read URL name
do
    wget -i -c "$URL" -O $name
done < uwyo.txt
```
`uwyo.txt` 文件如下：
``` bash
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=01&FROM=0100&TO=3112&STNM=51777 20170101003112.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=02&FROM=0100&TO=2812&STNM=51777 20170201002812.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=03&FROM=0100&TO=3112&STNM=51777 20170301003112.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=04&FROM=0100&TO=3012&STNM=51777 20170401003012.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=05&FROM=0100&TO=3112&STNM=51777 20170501003112.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=06&FROM=0100&TO=3012&STNM=51777 20170601003012.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=07&FROM=0100&TO=3112&STNM=51777 20170701003112.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=08&FROM=0100&TO=3112&STNM=51777 20170801003112.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=09&FROM=0100&TO=3012&STNM=51777 20170901003012.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=10&FROM=0100&TO=3112&STNM=51777 20171001003112.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=11&FROM=0100&TO=3012&STNM=51777 20171101003012.txt
http://weather.uwyo.edu/cgi-bin/sounding?region=seasia&TYPE=TEXT%3ALIST&YEAR=2017&MONTH=12&FROM=0100&TO=3112&STNM=51777 20171201003112.txt
```

参考文献：[美]Kurt Wall等著 张辉译.《GNU/Linux编程指南》第二版 26-45. 
参考网站：[GNU文档](http://gcc.gnu.org/onlinedocs/)

## 修订历史
- 2017-10-15: 初稿
- 2017-12-18: 增加 `gcc` 说明
- 2018-02-02: 增加文本内容的处理命令
- 2018-04-01: 增加 `wget` 的使用示例
