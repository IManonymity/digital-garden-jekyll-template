---
---

flex (Fast LEXical analyzer generator)是用于快速生成词法扫描器的工具，用户只需要填写flex文件就可以生成想要的扫描器。

### flex工作流程

![](/assets/images/flex工作流程.png)

解释：
- 对`*.flex`文件使用***flex***进行处理，得到`lex.yy.c`文件
- 使用C编译器对`lex.yy.c`进行编译，得到可执行文件
- 执行上述生成的可执行文件，并将输入放进去，得到输出的tokens序列

例子：
- 给定一个写好的example.flex文件
- 使用flex进行处理：`flex example.flex`
- 使用gcc进行编译：`gcc -o target lex.yy.c`
- 运行扫描器：`./target < input_file` 或者`./target` + 手动输入字符

### flex文件格式

```flex
definitions  
%%  
rules  
%%  
user code
```

解释：
- flex文件的内容可以根据`%%`划分为三个区域
	- definitions：定义一些可用的格式，格式如`name  definition`
	- rules：书写正则表达式规则，格式如`pattern action`
	- user code：自定义处理逻辑
- definition：
	- /* content \*/：会原封不动地复制到`lex.yy.c`中
	- 未缩进的%{ content %}：%{ %}会被去掉，content被复制到`lex.yy.c`中
	- 缩进的内容：缩进的内容会原封不动地复制到`lex.yy.c`中
- rules：
	- action中可以使用return语句，作为yylex的返回值
	- action中如果没有return语句，yylex就不会返回，直到输入结束，才会返回0

例子：
```cpp
%%
[0-9]+  printf("?");
#       return 0;
.       ECHO;
%%

int main(int argc, char* argv[]) {
    yylex();
    return 0;
}

int yywrap() { 
    return 1;
}
```

注意事项：
- 只有rules是必须的，definitions和user  code可以不写
- flex工具会将rules的内容转换成一个`yylex`函数
- main 函数是程序的入口， flex 会将这些代码原样的复制到 **lex.yy.c** 文件的最后面
- 我们可以在文件最前面使用`%{ Declarations %}`添加头文件声明等
- flex 提供两个全局变量 **yytext** 和 **yyleng**，分别用来表示刚刚匹配到的字符串以及它的长度。



### flex资源介绍
- [FLEX Tutorial (ucr.edu)](http://alumni.cs.ucr.edu/~lgao/teaching/flex.html)
- [Lexical Analysis With Flex, for Flex 2.6.3: Top (virginia.edu)](https://www.cs.virginia.edu/~cr4bd/flex-manual/index.html#SEC_Contents)