# Shell Tutorial
## 变量
1. 变量命名规则同java
2. 变量引用采用 ```$name``` 或 ```${name}```的形式，第二次赋值时不能用此方式，直接用变量名即可
3. 变量用```readonly```修饰同java中```final```修饰效果
4. ```unset```可以删除变量
## 字符串
1. 字符串可以用单引号，双引号，无引号表示；双引号中可以包含变量，单引号中所有符号都会原样输出
2. 字符串拼接建议用```${name}```的方式
3. 字符串操作常用方法
    ```bash
    str="test"
    echo ${#str} #字符串长度
    echo ${str:1:3} #截取字符串，从第二个开始截取长度4
    ```
## 数组
1. 只有1维数组，数组元素用空格隔开
2. 数组定义
    ```bash
    array=(0 1 2 3) #数组的一般形式
    array=(
        0
        1
        2
    ) #也可以这样定义
    array[0]=1
    array[n]=100 #单独定义数组元素
    ```
3. 数组读取
    ```bash
    value=${array_name[n]} #读取数组元素
    ${array_name[@]} #读取数组所有元素
    lenth=${#array_name[@]} #数组元素个数
    lenth=${#array_name[*]} #同上
    ```
## 传递参数
1. 执行shell脚本时可传递参数
```bash
./test.sh 1 2 3 #执行脚本时传递三个参数
```
2. ```$#```表示参数个数
3. ```$*```以一个字符串表示所有参数，空格隔开
4. ```$@```以一个字符串表示一个参数，数组形式返回所有参数
5. ```$?```表示上一条命令的退出状态，为0表示没有错误，否则表示运行出错
6. ```$$```脚本运行当前进程id号
7. ```$!```后台运行的最后一个进程id号
## 运算符
1. 算术运算符同java，但是在使用*时需要\来转义，expr只提供整形数字进行运算
```bash
var=`expr 1 \* 10` #反引号表示先执行引号中内容
var=$(expr 1 \* 10) #此处要用()而不能使用{}
var=$((1 * 10)) #此处*无需转义

echo $var
```
2. 关系运算符，注意在使用关系表达式时，表达式需要放入``` [ ] ```中，左右均需要空格，因为```[```相当于test命令，```]```表示命令结束。关系运算符只支持数字不支持字符串，除非字符串为数字。关系运算符有```-eq```,```-ne```(not equal),```-gt```,```-lt```,```-ge```,```-le```。
```bash
a=10
b=1
if [ $a -eq $b ]
then 
    echo "a=b"
else 
    echo "a!=b"
fi
```
3. 布尔运算与逻辑运算符，布尔运算符有```!```、```-a```、```-o```。逻辑运算符同java ```||```、```&&```。需要注意：在使用逻辑运算符时需要使用``` [[ ]] ```表达式,而使用布尔运算时则可以直接用``` [ ] ```。 在使用双中括号时内部可以使用```>```、```<```，但是不能使用大于等于，小于等于。 
```bash
[[ 99+1 -eq 100 ]] && echo true || echo false #true
[ 99+1 -eq 100 ] && echo true || echo false #会报错，integer expression expected，但是仍然会返回false
[ $((99+1)) -eq 100 ] && echo true || echo false #true 算术扩展
```
4. 字符串运算符
```bash
[ $a = $b ] # 
```