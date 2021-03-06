## 编写带括号的四则运算产生式

    // 0 ~ 9
    <Number> ::= "0" | "1" | "2" | "3" | "4" | ... | "9"
    // 0 | (1~9)(0~9)... eg: 0 | 10 | 200 ...
    <DecimalNumber> ::= "0" | (("1" | "2" | ... | "9") <Number>*)
    // 优先级 括号
    <BracketsExpression> ::= <DecimalNumber> |
        "(" <AdditiiveExpression> ")"
    // 乘除
    <MultiplyExpression> ::= <BracketsExpression> |
        <MultiplyExpression> "*" <BracketsExpression> |
        <MultiplyExpression> "/" <BracketsExpression>
    // 加减
    <AdditiiveExpression> ::= <MultiplyExpression> |
        <AdditiiveExpression> "+" <MultiplyExpression> |
        <AdditiiveExpression> "-" <MultiplyExpression>

## 尽可能寻找你知道的计算机语言，尝试把它们分类
    Java 强类型
    C# 强类型
    Python 强类型
    JavaScript 弱类型

## 写一个正则表达式 匹配所有 Number 直接量
    - 整数/浮点数/二进制/八进制/十六进制
    /^(-?[0-9]+)| ([-+]?[0-9]*\.?[0-9]+) | ([01]+) | ([0-7]+\) |(0x[a-f0-9]{1,2}$)|(^0X[A-F0-9]{1,2}$)|(^[A-F0-9]{1,2}$)|(^[a-f0-9]{1,2})$/g;

## 写一个 UTF-8 Encoding 的函数

    function UTF8_Encoding(string){
        //return new Buffer();
        const code = encodeURIComponent(string);
        const bytes = [];
        for (var i = 0; i < code.length; i++) {
            const c = code.charAt(i);
            if (c === '%') {
                const hex = code.charAt(i + 1) + code.charAt(i + 2);
                const hexVal = parseInt(hex, 16);
                bytes.push(hexVal);
                i += 2;
            } else bytes.push(c.charCodeAt(0));
        }
        return bytes;
    }

## 写一个正则表达式，匹配所有的字符串直接量，单引号和双引号

    /[\u0021-\u007E]{6,16}|[\x21-\x7E]{6,16}|(['"])(?:(?!\1).)*?\1/g;