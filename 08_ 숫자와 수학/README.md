# CH 8. Number and Math - `by 권성`
## 목차
* [Numeric Literals](numeric-literals.md)  
  * Binary Literal
  * Octal Literal
  * Hexadecimal
* Number
* Math



## Number
* Number type(Primitive values)
* Number object(Wrapper object)



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
console.log(parseInt(true)); // NaN
console.log(parseInt(new Date())); // NaN
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
console.log(parseFloat(true)); // NaN
console.log(parseFloat(new Date())); // NaN
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
}
console.timeEnd('parseInt()');
console.time('parseFloat()');
for(let i=0; i<iterations; i++){
    parseFloat('1.1'); // parseFloat(): 737.437ms
}
console.timeEnd('parseFloat()');
console.time('Number()');
for(let i=0; i<iterations; i++){
    Number('1.1'); // Number(): 844.648ms
}
console.timeEnd('Number()');
console.time('+string');
for(let i=0; i<iterations; i++){
    +'1.1'; // +string: 20.724ms
}
console.timeEnd('+string');
console.time('1*string');
for(let i=0; i<iterations; i++){
    1*'1.1'; // 1*string: 21.459ms
}
console.timeEnd('1*string');
```

#### Number to String
* Number.prototype.toString()
* String(number)
* '' + number

##### Number.prototype.toString()
```javascript
console.log(1.1.toString()); // '1.1'
console.log(1.0.toString()); // '1'
console.log(0b11.toString()); // '3'
console.log(NaN.toString()); // 'NaN'
console.log(Infinity.toString()); // 'Infinity'
console.log(-Infinity.toString()); // -Infinity
console.log(0.0.toString()); // '0'
```

##### String(number)
```javascript
console.log(String(1.1)); // '1.1'
console.log(String(1)); // '1'
console.log(String(0b11)); // '3'
console.log(String(NaN)); // 'NaN'
console.log(String(Infinity)); // 'Infinity'
console.log(String(-Infinity)); // '-Infinity'
console.log(String(0)); // '0'
```

##### '' + number
```javascript
console.log('' + 1.1); // '1.1'
console.log('' + 1); // '1'
console.log('' + 0b11); // '3'
console.log('' + NaN); // 'NaN'
console.log('' + Infinity); // 'Infinity'
console.log('' + -Infinity); // '-Infinity'
console.log('' + 0); // '0'
```

##### Performance
```javascript
const iterations = 10000000;
console.time('Number.prototype.toString()');
for(let i=0; i<iterations; i++){
    1.1.toString(); // Number.prototype.toString(): 268.619ms
}
console.timeEnd('Number.prototype.toString()');
console.time('String(number)');
for(let i=0; i<iterations; i++){
    String(1.1); // String(): 159.045ms
}
console.timeEnd('String(number)');
console.time('\'\' + number');
for(let i=0; i<iterations; i++){
    '' + 1.1; // '' + number: 20.594ms
}
console.timeEnd('\'\' + number');
```