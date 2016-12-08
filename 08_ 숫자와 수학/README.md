# CH 8. Number and Math - `by 권성`
## 목차
* [Binary Literal & Octal Literal](#Binary-Literal-Octal-Literal)
* [Number](#Number)
* [Math](#Math)

## Binary Literal & Octal Literal
### Binary Literal
**in ES5**
```javascript
parseInt('11', 2); // 3
```

**in ES6**
```javascript
0b11; // 3
```

## Octal Literal
**in ES5**
```javascript
071; // 57
```

**in strict mode**
```javascript
'use strict';
071; // Uncaught SyntaxError: Octal literals are not allowed in strict mode.
```
ES5의 strict mode에서는 8진수 리터럴이 적용되지 않습니다.  
왜냐하면 ES5에는 8진수 문법이 존재하지 않기 때문입니다.  
그럼에도 불구하고 브라우저 사들은 비표준 요소인 8진수 리터럴을 지원하게끔 구현하였습니다.  
따라서 strict mode에 따라서 8진수 리터럴의 사용 가능 여부가 달려있습니다.  
`strict mode in ECMAScript 5 forbids octal syntax.  
Octal syntax isn't part of ECMAScript 5,  
but it's supported in all browsers by prefixing the octal number with a zero:  
0644 === 420 and "\045" === "%".`