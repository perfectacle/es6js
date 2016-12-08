# CH 8. Number and Math - `by 권성`
## 목차
* Numeric Literals  
  * Binary Literal
  * Octal Literal
  * Hexadecimal
* Number
* Math

## Numeric Literals
### Binary Literal
수학식: 11<sub>(2)</sub>  
프로그래밍 언어: 0b11

**in ES5**
```javascript
console.log(parseInt('11', 2)); // 3
```

**in ES6**
```javascript
console.log(0b11); // 3
```

### Octal Literal
수학식: 71<sub>(8)</sub>  
프로그래밍 언어: 071

**in ES5**
```javascript
console.log(071); // 57
```

**in strict mode**
```javascript
'use strict';
console.log(071); // Uncaught SyntaxError: Octal literals are not allowed in strict mode.
```
ES5의 strict mode에서는 8진수 리터럴이 적용되지 않습니다.  
왜냐하면 ES5에는 8진수 문법이 존재하지 않기 때문입니다.  
그럼에도 불구하고 브라우저 사들은 비표준 요소인 8진수 리터럴을 지원하게끔 구현하였습니다.  
따라서 strict mode에 따라서 8진수 리터럴의 사용 가능 여부가 달려있습니다.

[MDN Strict mode](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Strict_mode#엄격한_모드_변경)  
`strict mode in ECMAScript 5 forbids octal syntax.
Octal syntax isn't part of ECMAScript 5,
but it's supported in all browsers by prefixing the octal number with a zero:
0644 === 420 and "\045" === "%".`

**in ES6**
```javascript
console.log(0o71); // 57
```

### Hexadecimal
수학식: FF<sub>(16)</sub>  
프로그래밍 언어: 0xFF, xFF, hFF, etc.

**in ES5**
```javascript
console.log(0xff); // 255
console.log(0xA); // 10
```

### Caution
```javascript
console.log(0b11.1); // Uncaught SyntaxError: missing ) after argument list
```

실수가 되는 게 아니라 Number.prototype.1로 접근을 하게 됩니다.  
10진수의 경우에는 실수 취급합니다.

```javascript
Number.prototype.Aa = 'Aa';
console.log(0b11.Aa); // 'Aa'
1.Aa; // Uncaught SyntaxError: Invalid or unexpected token
```

## Number
### Number <-> String
```javascript
const num1 = '10';
const num2 = '10';
const sum = num1 + num2; // '1010'
const sub = num1 - num2; // 0
const mul = num1 * num2; // 100
const div = num1 / num2; // 1
```
#### String to Number
* parseInt(string[, radix])
* parseFloat(string)
* Number()
* +object, 1*object

##### parseInt(str[, radix])
```javascript
console.log(parseInt('11')); // 11
console.log(parseInt('11.11')); // 11
console.log(parseInt('11A')); // 11
console.log(parseInt('A11')); // NaN
console.log(parseInt('11A1')); // 11
console.log(parseInt('11.A')); // 11
console.log(parseInt('011')); // 11
console.log(parseInt('11 0')); // 11
```

##### parseFloat(str)
```javascript
console.log(parseFloat('11')); // 11
console.log(parseFloat('11.11')); // 11.11
console.log(parseFloat('11A')); // 11
console.log(parseFloat('A11')); // NaN
console.log(parseFloat('11A1')); // 11
console.log(parseFloat('11.A')); // 11
console.log(parseFloat('011')); // 11
console.log(parseFloat('11 0')); // 11
```

##### Number(object)
```javascript
console.log(Number('11')); // 11
console.log(Number('11.11')); // 11.11
console.log(Number('11A')); // NaN
console.log(Number('A11')); // NaN
console.log(Number('11A1')); // NaN
console.log(Number('11.A')); // NaN
console.log(Number('011')); // 11
console.log(Number(true)); // 1
console.log(Number(new Date())); // 1481186433309
```

##### +str, 1*str
```javascript
console.log(+'11'); // 11
console.log(+'11.11'); // 11.11
console.log(+'11A'); // NaN
console.log(+'A11'); // NaN
console.log(+'11A1'); // NaN
console.log(+'11.A'); // NaN
console.log(+'011'); // 11
console.log(+true); // 1
console.log(+new Date()); // 1481186433309
```

##### Performance
```javascript
const iterations = 10000000;
console.time('parseInt()');
for(let i=0; i<iterations; i++){
    parseInt('1.1'); // parseInt(): 561.062ms
};
console.timeEnd('parseInt()');
console.time('parseFloat()');
for(let i=0; i<iterations; i++){
    parseFloat('1.1'); // parseFloat(): 737.437ms
};
console.timeEnd('parseFloat()');
console.time('Number()');
for(let i=0; i<iterations; i++){
    Number('1.1'); // Number(): 844.648ms
};
console.timeEnd('Number()');
console.time('+string');
for(let i=0; i<iterations; i++){
    +'1.1'; // +string: 20.724ms
};
console.timeEnd('+string');
console.time('1*string');
for(let i=0; i<iterations; i++){
    1*'1.1'; // 1*string: 21.459ms
};
console.timeEnd('1*string');
```