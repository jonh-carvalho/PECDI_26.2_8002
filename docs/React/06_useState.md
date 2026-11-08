---
id: 06_useState
title: 06 - Estado com useState
---

# 06 - **Estado com useState**

## Introdução

**Estado** é uma das características mais importantes do React. Ele permite que componentes "lembrem" de informações e reajam a mudanças, tornando a interface dinâmica e interativa.

### O que é Estado?

- **Definição**: Dados que podem mudar ao longo do tempo em um componente
- **Reatividade**: Quando o estado muda, o componente re-renderiza automaticamente
- **Local**: Cada componente gerencia seu próprio estado
- **useState**: Hook que permite adicionar estado a componentes funcionais

### Por que usar Estado?

- **Interatividade**: Responder a ações do usuário (cliques, digitação)
- **Dinamismo**: Conteúdo que muda baseado em condições
- **Experiência**: Interfaces mais ricas e responsivas
- **Dados temporários**: Armazenar informações que não vem de props

### Sintaxe do useState

```jsx
import { useState } from 'react';

function MeuComponente() {
  // useState retorna o valor atual e a função que o atualiza
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Contador: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Incrementar
      </button>
    </div>
  );
}
```

### Regras Importantes

1. **Importe useState**: `import { useState } from 'react'`
2. **Use no topo**: Sempre no início da função do componente
3. **Não em loops/condições**: useState deve ser sempre executado
4. **Estado é imutável**: Use sempre a função set para atualizar

## Primeiro exemplo: contador

O contador mostra o ciclo básico do estado: o componente começa com um valor, uma ação chama a função `setCount` e o React renderiza novamente a tela com o valor atualizado.

```jsx
import { useState } from 'react';

function Contador() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Contagem: {count}</p>
      <button onClick={() => setCount(count + 1)}>Adicionar</button>
      <button onClick={() => setCount(0)}>Zerar</button>
    </div>
  );
}

export default Contador;
```

### Pratique

1. Adicione um botão para diminuir o contador.
2. Mostre uma mensagem diferente quando o contador chegar a zero.
3. Crie um botão que alterne entre “Olá!” e “Até logo!”.

## Resumo

- `useState` guarda um valor que pode mudar durante o uso do componente.
- A função setter atualiza o estado; não altere a variável diretamente.
- Quando o estado muda, o React renderiza novamente o componente.

Quando estiver confortável com esses exemplos, continue para [06b - Estado com useState: aplicação](./06b_useState_Aplicado.md).
