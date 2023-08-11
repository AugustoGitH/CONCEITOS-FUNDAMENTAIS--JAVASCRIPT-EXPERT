# Call Stack e Memory Heap em JavaScript

Neste repositório, vamos explorar os conceitos de Call Stack e Memory Heap em JavaScript. Esses dois componentes desempenham papéis importantes na execução de código JavaScript e na alocação de memória.

## Call Stack (Pilha de Chamadas)

A Call Stack é uma estrutura de dados que rastreia as chamadas de função em um programa. Quando uma função é chamada, ela é empilhada no topo da pilha, e quando a função retorna, ela é desempilhada.

### Funcionamento da Call Stack

- Funções são empilhadas quando são chamadas.
- A função no topo da pilha é a que está sendo executada.
- Quando a função retorna, ela é removida da pilha.

## Memory Heap (Monte de Memória)

A Memory Heap é onde objetos e dados complexos são armazenados em JavaScript. Ao contrário da Call Stack, que lida com a execução de funções, a Memory Heap armazena dados persistentes, como objetos e arrays.

### Funcionamento da Memory Heap

- Objetos e dados complexos são armazenados na Memory Heap.
- A Heap pode armazenar dados não ordenados que crescem dinamicamente.

A Memory Heap lida com a alocação de memória para objetos que não são primitivos. Primitivos, como strings e números, são armazenados na Call Stack. No entanto, objetos maiores, como arrays e objetos personalizados, são armazenados na Memory Heap.

Exemplo de alocação na Memory Heap:

```javascript
const pessoa = {
  nome: "Maria",
  idade: 25,
};
const numeros = [1, 2, 3, 4, 5];
```

## Interação entre Call Stack e Memory Heap

A Call Stack lida com a sequência de execução de funções, enquanto a Memory Heap armazena dados complexos que persistem além das chamadas de função.
Conclusão

O entendimento da Call Stack e da Memory Heap é crucial para escrever código JavaScript eficiente e compreender como o gerenciamento de memória ocorre. Esses conceitos nos ajudam a evitar problemas de desempenho e vazamentos de memória.
