# 常用命令记录
## Mac命令
---
更多命令参考[awesome-macos-command-line](https://github.com/herrbischoff/awesome-macos-command-line)
1. 查看文件路径，并拷贝到剪切板
``` zsh
realpath test | tee pbcopy # 查看当前目录的test文件的绝对路径 并拷贝到剪切板
```
2. 重启dock
```mac
killall dock
```
3. 删除迅雷无用组件
```shell
cd /Applications/Thunder.app/Contents/PlugIns

rm -rf featuredpage.* advertising.* xlbrowser.*
rm -rf activitycenter.* xlplayer.* xiazaibao.* iOSThunder.* searchtask.* lixianspace.* softmanager.*
```

## 常用工具命令
1. 删除maven所有更新失败的文件：
``` zsh
find /Users/shuqin/.m2/repository -name "*lastUpdated" | xargs rm -fr 
```
2. 安装homebrew:
```zsh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
3. ssh免密码登陆：
```zsh
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.2.100
```
## 查看日志相关命令
1. tail: -n:显示行号，相当于nl命令
```zsh
tail -100f test.log #实时监控100行日志
tail -n 10 test.log #查询日志尾部最后十行日志
tail -n +10 test.log #查询10行之后的所有日志
```
2. head:查看头尾多少行日志
```zsh
head -n 10 test.log #查看头十行日志
head -n -10 test.log #查看尾十行日志
```
3. cat，tac是倒序查看
```zsh
cat test.log #查看整个日志文件
cat -n test.log #查看整个日志文件并从1开始对日志编号
cat -b test.log #同-n，但不对空行编号
cat -s test.log #遇到两行以上的空白行，就代换为一行空白行,不输出多行空行
cat -E test.log #在每行结尾处加上$
```
4. more:类似于cat，但more能逐页阅读
```zsh
more [-dlfpcsu ] [-num ] [+/ pattern] [+ linenum] [file ... ]  #命令格式
more +n test.log #从第n行开始显示
more -n 
```
5. 组合命令
```zsh
cat -n test.log |grep "debug" #得到debug日志的行号
cat -n test.log |tail -n +92|head -n 20 #选择关键字所在的中间一行. 然后查看这个关键字前10行和后10行的日志
```

