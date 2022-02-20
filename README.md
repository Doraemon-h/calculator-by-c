# 思路：
将.txt文件中的字符一个一个读，然后将其划分成不同的token后并分类：1表示float、int，2表示变量名，3表示浮点数，4表示整数，5表示运算符，6表示分号，7表示write函数。然后开始读取token，分三种情况，一种遇到float、int，然后接着向下读取直到读取到分号；一种是遇到变量开头，然后接着读取到“=”，调用计算等号后面的函数after_eauql，将后面的tokens直到;之前的合并成一个字符串，然后调用逆波兰函数，将中缀表达式转化成后缀表达式并计算，然后返回到符号表中的值;第三种是遇到write函数，打印符号表中的数值。（相当于一行一行的读取）。对于负数的处理，遇到“-”左边无符号的，把这个数值前面加个0，相当于把所有的负数看成零减去一个数。


# 使用方法：
只能输入一个参数，第一个参数为读取的文件，结果直接打印出来。（时间原因，没有做把答案存进文档之中）

# 文法：
<无符号整数>::=<数字>{<数字>}
<变量说明部分>::=float|int <标识符>;
<标识符>::=<字母>{<字母>|<数字>};
<赋值语句>::=<标识符>:=<表达式>;
<输出语句>::=write(<标识符>);
……

# 测试用例：
输入：
int a;
float b;
a = -3*3;
b=a*2-a/2;
write(b);
write(a).
输出：
-13.5
-9
