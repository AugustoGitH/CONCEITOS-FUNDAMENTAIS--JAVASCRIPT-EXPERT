# Tipo de Valor vs Tipo de Referência em JavaScript

Este repositório explora o conceito de tipos de valor e tipos de referência em JavaScript. As informações abaixo são adaptadas do artigo "Explaining Value vs Reference in JavaScript".

## Primitivos

JavaScript possui 5 tipos de dados que são passados por valor: Boolean, null, undefined, String e Number. Esses são chamados de tipos primitivos.

Se um tipo primitivo é atribuído a uma variável, podemos considerar que a variável contém o valor primitivo.

```javascript
var x = 10;
var y = "abc";
var z = null;
```

Quando atribuímos essas variáveis a outras variáveis usando =, copiamos o valor para a nova variável. Eles são copiados por valor.

```javascript
var x = 10;
var y = "abc";
var a = x;
var b = y;
console.log(x, y, a, b); // -> 10, 'abc', 10, 'abc'
```

Mudar um não afeta o outro. As variáveis não têm relação entre si.

```javascript
var x = 10;
var y = "abc";
var a = x;
var b = y;
a = 5;
b = "def";
console.log(x, y, a, b); // -> 10, 'abc', 5, 'def'
```

## Objetos

Variáveis atribuídas a um valor não-primitivo recebem uma referência a esse valor. Essa referência aponta para a localização do objeto na memória. As variáveis não contêm diretamente o valor.

```javascript
var reference = [1];
var refCopy = reference;
```

Quando copiamos um valor de tipo de referência para outra variável usando =, na verdade, copiamos o endereço desse valor como se fosse um valor primitivo.

```javascript
reference.push(2);
console.log(reference, refCopy); // -> [1, 2], [1, 2]
```

## Atribuição por Referência

Quando um valor de tipo de referência, um objeto, é copiado para outra variável usando =, o endereço desse valor é o que é copiado como se fosse um valor primitivo. Objetos são copiados por referência em vez de por valor.

```javascript
var obj = { first: "reference" };
```

## == e ===

Quando os operadores de igualdade == e === são usados em variáveis de tipo de referência, eles verificam a referência. Se as variáveis contiverem uma referência para o mesmo item, a comparação resultará em verdadeiro.

```javascript
var arrRef = ["Oi!"];
var arrRef2 = arrRef;
console.log(arrRef === arrRef2); // -> true
```

Se forem objetos distintos, mesmo que contenham propriedades idênticas, a comparação resultará em falso.

```javascript
var arr1 = ["Oi!"];
var arr2 = ["Oi!"];
console.log(arr1 === arr2); // -> false
```

## Passagem de Parâmetros por Funções

Quando passamos valores primitivos para uma função, a função copia os valores para seus parâmetros. É essencialmente o mesmo que usar =.

```javascript
var hundred = 100;
var two = 2;
function multiply(x, y) {
  return x * y;
}
var twoHundred = multiply(hundred, two);
```

## Funções Puras

Funções que não afetam nada no escopo externo são chamadas de funções puras. Se uma função só recebe valores primitivos como parâmetros e não usa variáveis em seu escopo circundante, ela é automaticamente pura, pois não pode afetar nada no escopo externo. Todas as variáveis criadas dentro dela são coletadas pelo coletor de lixo assim que a função retorna.

## Teste-se

O conceito de valor vs referência é frequentemente testado em entrevistas de programação. Tente descobrir o que é registrado no seguinte exemplo:

```javascript
function changeAgeAndReference(person) {
  person.age = 25;
  person = {
    name: "John",
    age: 50,
  };

  return person;
}
var personObj1 = {
  name: "Alex",
  age: 30,
};
var personObj2 = changeAgeAndReference(personObj1);
console.log(personObj1); // -> { name: 'Alex', age: 25 }
console.log(personObj2); // -> { name: 'John', age: 50 }
```

## Conclusão

Este repositório oferece uma visão abrangente sobre os conceitos de tipos de valor e tipos de referência em JavaScript. Consulte as referências fornecidas para mais informações e exemplos interativos.

Referências:

[codeburst](https://codeburst.io/explaining-value-vs-reference-in-javascript-647a975e12a0)
