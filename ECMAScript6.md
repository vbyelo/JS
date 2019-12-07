ECMAScript jest standartem języka skryptowego, gdzie JavaScript to jedna z jego implementacji. Można powiedzieć, że jest to jeden z dialektów języka ECMAScript.

Nowsza wersja wprowadza wiele nowości, między innymi:
* moduły oraz klasy
* skrócone składanie do tworzenia zmiennych i funkcji
* zasięg zmiennych
* stałe
* symbole
* interpolacja ciągów znaków
* pętla *for..of*

# Rozkład struktury obiektów

Niech mamy obiekt 

```javascript
var myObj = {
    a: 1,
    b: 2,
    c: 3
}
```

Przypisanie wartości z obiektu do zmiennych

```javascript
var a = myObj.a;
var b = myObj.b;
var c = myObj.c;
```

Przypisanie wartości z obiektu do zmiennych według skróconej składni

```javascript
var {a, b, c} = myObj;
```

W przypadku obiektu ważne jest, żeby nazwy zmiennych po lewej stronie wyrażenia znalazły swoje odzwierciedlenie w nazwach właściwości obiektu, które znajdują się po jego prawej stronie.

```javascript
var {c,d} = myObj;
console.log(c,d); // <1>
>  wynik:3, undefined
```

Rozkład struktury tablicy:

```javascript
var [x, y, z] = [1, 2, 3];
```

Rozkład struktury tablicy z pominięciem elementu:

```javascript
var [x,, z] = [1, 2, 3];
```

Zamiana wartości zmiennych miejściami

```javascript
var A = "foo";
var B = "bar";
[A, B] = [B, A]
console.log(A,B); //<1>
<1> Wynik: bar, foo
```


# Zasięg zmiennych

Można tworzyć rodzaj zmiennej, której zasięg ograniczony do danego bloku.
Taki zmienny możemy ustawić za pomocą wyrażenia *let*.

Deklaracja zmiennych za pomocą wyrażenia *var*:


```javascript
"use strict";

var myVar = "foo";
if (true){
    var myVar = "bar";
    console.log(myVar); // <1>
}
console.log(myVar); // <2>
<1> Wynik: bar
<2> Wynik: bar
```

Deklaracja zmiennych za pomocą wyrażenia *let*:

```javascript
"use strict";

var myVar = "foo";
if (true){
    let myVar = "bar";
    console.log(myVar); // <1>
}
console.log(myVar); // <2>
<1> Wynik: bar
<2> Wynik: foo
```

Deklaracja zmiennej _i_ oraz bezproblemowe odwołanie się do niej poza blokiem pętli:

```javascript
"use strict";

var myVar = "foo";
for (var i=0; i<5; ++i){
    console.log("value of 'i':", i); 
}
console.log("final value of 'i':", i);  
```


Deklaracja zmiennej _i_ oraz bezproblemowe odwołanie się do niej poza blokiem pętli:

```javascript
"use strict";

var myVar = "foo";
for (let i=0; i<5; ++i){
    console.log("value of 'i':", i); 
}
console.log("final value of 'i':", i);  // <1>

<1> Odwołanie się w tym miejście do zmiennej i spowoduje poinformowanie  o wyjątku o braku deklaracji tej zmiennej.
```

# Funkcje strzałki

Iterowanie po tablicy

```javascript
var collection = [1, 2, 3];

collection.forEach(function(item){
    console.log(item)});
```

```javascript
var collection = [1, 2, 3];

collection.forEach(item => console.log(item));
```

Po lewej stronie wyrażenie funkcji w postaci strzałki znajduje się argument dostarczony przez metodę _forEach_, natomiast po prawej stronie wyrażenia mamy już ciało funkcji, bez zbędnych w tym przypadku nawiasów klamrowych. Całość można też opisać w poniższy sposób:

```
argument => function body
```

W przypadku więcej niż jednego argumentu należy użyć nawiasów okrąglych po lewej stronie wyrażenia:

```
(argument1, argument2) => function body
```

Na przykład

```javascript
var collection = [1, 2, 3];

collection.forEach((item,index) => console.log(item, index));
```

Gdybyśmy chcieli użyć większej ilości kodu w ciele funkcji o skróconej składni,, dany kod możemy opakować w nawiasy klamrowe:

```javascript

collection.forEach(item => {
       job1(item);
       job2(item);
}); 
```

Przykład funkcji strzałki przy deklaracji klasy

```javascript

funktion myClass(){
    this.foo = "Hello";
    setTimeout(bar => console.log(this.foo + bar), 200, " World!"); // <1> 
}; 

new myClass();
```

# Operator spread

Operator _..._ pozwola rozproszyć zawartość tablicy dostępnej pod zmienną w miejscu użycia operatora. Spójrzmy na poniższy przykład, w którym rozpraszamy zawartość tablicy _a_ w tablicy _b_:

```javascript
let a = [3, 4];
let b = [1, 2, ...a, 5];

console.log(b);
```

Wynik tej operacje:

```javascript
[1, 2, 3, 4, 5]
```

Operatora tego możemy także użyć jako argumentu funkcji:

```javascript
function sum(...numbers){
    let result = 0;
    for (num of numbers){
        result += num;
    }
    return result;
}
let a = [1, 2];
let b = [3, 4, 5];

console.log(sum(2, ...a, ...b));
```
Wynik:

```
17
```


