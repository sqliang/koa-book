{% raw %}

# xtemplate的基础语法

xtemplate所有的语法索引请看[文档](https://github.com/kissyteam/xtemplate/blob/master/docs/syntax.md)，这里只抽取核心语法进行讲解。

## 行内命令 与 块状命令

行内命令 简单地理解就是可以一行写完的命令...比如{{name}}。

块状命令 就是需要多行结合才算完整的命令，比如{{#if}....{{else}}zzzz{{/if}}。

所有的块状命令起始都要加上 # ，比如{{#if}}。需要有结束标记 / ，比如{{/if}}。

## 简单的变量

格式：{{变量}}，比如{{name}}，数据是{"name":"xtemplate"}，{{name}}会被替换成xtemplate。

如果数据中带有html标签呢？比如{"name":"&lt;p&gt;xtemplate&lt;&#x2F;p&gt;"}。

xtemplate会自动转译，输出的内容是 &lt;p&gt;xtemplate&lt;&#x2F;p&gt;。

如果希望不转译呢？可以使用{{{name}}}，这样就可以渲染数据中的html格式。

如果name字段不存在，{{name}} 渲染成空字符。

## 变量支持使用运算符

比如：{{x+y}}，数据是{"x":1,"y":2}，渲染的结果会是3。

xtemplate还会自动转换变量类型为数值型，比如数据为 {"x":1,"y":"2"}，渲染的结果依旧是3，不会是12。

xtemplate 支持最常用的 + - * / % 运算符。

当然直接 {{x+1}}也是可以的，但不支持{{x--}}或{{x++}}的形式。

## 注释

有时模板会很复杂，维护的需要我们需要加些注释，但我们不希望注释打印到页面中，如何处理呢？

使用 {{! 我是神奇的注释}}

## if 条件判断
 
if 块状命令由 {{#if()}}、{{elseif()}}（不是必须，else与if中间不要加空格）、{{else}}（不是必须，不要加 #）、{{/if}}组成。
 
运算符支持：===、!==、>、>=、<、<= 。

特别特别留意，判断相等使用===，不能使用==，这个细节不知道坑过多少人...

举例：数据 {"x":2}

    {{#if( x===1 )}}
        1
    {{elseif (x===2)}}
        2
    {{else}}
        3
    {{/if}}
    
留意，{{#if( x===1 )}} 中的()是不可省略的，这与旧的xtemplate不同。
    
渲染结果为2。

## ||、&&、!的使用

有时判断条件比较复杂，比如同时判断x等于1，y等于2。

    {{#if(x===1 && y===2)}}
    x等于1，y等于2
    {{/if}}
    
使用&&符号，当然“或”的判断可以使用||，“非”的判断使用!，比如{{#if(!x)}}。
    
有没有发现xtemplate语法跟js很相似！！！

     
使用if命令相当繁琐，有时还会写错，其实简单的字段存在性判断可以使用||、&&，比如：

    {{name||"明河"}}
    
当name字段数据不存在时，默认输出“明河”。

{% endraw %}


