# Coerção de Tipos em JavaScript

Neste repositório, exploramos o conceito de coerção de tipos em JavaScript. A coerção de tipos é o processo de converter um valor de um tipo para outro (como de string para número, objeto para booleano, etc.). Isso é aplicável tanto a tipos primitivos quanto a objetos, e entender como funciona é fundamental para escrever código seguro e prever o comportamento de expressões.

## Tipos Primitivos

### Coerção para String

A conversão explícita para string pode ser feita usando a função String(valor), e a coerção implícita ocorre ao usar o operador + com pelo menos um operando sendo uma string.

```javascript
String(123); // explicita
123 + ""; // implicita
```

Todos os tipos primitivos podem ser convertidos para strings:

```javascript
String(123); // '123'
String(-12.3); // '-12.3'
String(null); // 'null'
String(undefined); // 'undefined'
String(true); // 'true'
String(false); // 'false'
```

### Coerção para Boolean

A conversão explícita para boolean pode ser feita usando a função Boolean(valor), e a coerção implícita ocorre em contextos lógicos e com operadores lógicos.

```javascript
Boolean(2);         // explicita
if (2) { ... }      // implicita
!!2;                // implicita
```

Valores vazios, nulos e undefined são considerados falsos, enquanto outros valores são considerados verdadeiros:

```javascript
Boolean(""); // false
Boolean(0); // false
Boolean(-0); // false
Boolean(NaN); // false
Boolean(null); // false
Boolean(undefined); // false
Boolean(false); // false

Boolean({}); // true
Boolean([]); // true
Boolean(Symbol()); // true
```

### Coerção para Número

A conversão explícita para número pode ser feita usando a função Number(valor), e a coerção implícita ocorre em operações matemáticas, comparações e operadores aritméticos.

```javascript
Number(null); // 0
Number(undefined); // NaN
Number(true); // 1
Number(false); // 0
Number(" 12 "); // 12
Number("-12.34"); // -12.34
```

## Objetos e o Método [[ToPrimitive]]

A coerção de objetos para tipos primitivos ocorre por meio do método interno [[ToPrimitive]], que utiliza os métodos valueOf e toString do objeto. A conversão para número ou string é determinada pelo contexto da operação.

```javascript
// Exemplo hipotético de implementação do [[ToPrimitive]]
[[ToPrimitive]](valor, tipoPreferencial) {
if (tipoPreferencial === 'number') {
if (valor.valueOf é primitivo) {
return valor.valueOf();
}
if (valor.toString é primitivo) {
return valor.toString();
}
} else if (tipoPreferencial === 'string') {
if (valor.toString é primitivo) {
return valor.toString();
}
if (valor.valueOf é primitivo) {
return valor.valueOf();
}
}
throw TypeError("Não foi possível converter para primitivo");
}
```

## Symbol.toPrimitive em ES6

A partir do ES6, é possível controlar a coerção de objetos para tipos primitivos implementando o método Symbol.toPrimitive no objeto.

```javascript
const meuObjeto = {
  valor: 42,
  [Symbol.toPrimitive](tipo) {
    if (tipo === "number") {
      return this.valor;
    }
    if (tipo === "string") {
      return `Valor: ${this.valor}`;
    }
  },
};
```

## Objects Lifecycle: toString, valueOf e Symbol.toPrimitive

Em JavaScript, objetos podem ser convertidos para tipos primitivos usando os métodos toString, valueOf e Symbol.toPrimitive. Esses métodos controlam como um objeto se comporta em operações de coerção.
toString

O método toString converte um objeto em uma representação de string. Esse método é invocado automaticamente quando um objeto é usado em contextos que esperam uma string.

```javascript
const objetoExemplo = {
  valor: 42,
  toString() {
    return `Valor: ${this.valor}`;
  },
};

console.log(objetoExemplo + " é um número"); // Saída: "Valor: 42 é um número"
```

## valueOf

O método valueOf retorna o valor primitivo associado a um objeto. Esse método é chamado automaticamente quando um objeto é usado em contextos que esperam um valor primitivo, como em operações matemáticas.

```javascript
const objetoExemplo = {
  valor: 42,
  valueOf() {
    return this.valor;
  },
};

console.log(objetoExemplo + 10); // Saída: 52
```

## Symbol.toPrimitive (ES6)

O método Symbol.toPrimitive é uma maneira mais avançada de controlar a coerção de um objeto para um tipo primitivo. Ele permite definir como um objeto deve se comportar em relação a diferentes tipos de coerção: para número, para string e padrão.

```javascript
const meuObjeto = {
  valor: 42,
  [Symbol.toPrimitive](tipo) {
    if (tipo === "number") {
      return this.valor;
    }
    if (tipo === "string") {
      return `Valor: ${this.valor}`;
    }
    return this.valor; // Comportamento padrão
  },
};

console.log(meuObjeto + 10); // Saída: 52
console.log(String(meuObjeto)); // Saída: "Valor: 42"
```

## Conclusão

Compreender a coerção de tipos e o ciclo de vida de objetos no JavaScript é essencial para evitar erros sutis e escrever código mais confiável. Através do uso correto dos métodos toString, valueOf e Symbol.toPrimitive, você pode controlar como seus objetos são convertidos em tipos primitivos, garantindo que o comportamento seja previsível e adequado às suas necessidades.

Este repositório explora em detalhes esses conceitos, fornecendo exemplos práticos e explicações para ajudá-lo a dominar a coerção de tipos e entender como os objetos são tratados em diferentes contextos no JavaScript.

Referências:

[freecodecamp](https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839)
