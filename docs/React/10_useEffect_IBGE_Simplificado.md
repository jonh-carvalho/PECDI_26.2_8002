---
id: 10_useEffect_IBGE_Simplificado
title: 10 - Carregamento automático com useEffect e IBGE
---

# 10 - Carregamento automático com useEffect e IBGE

No roteiro anterior, a busca à API do IBGE começou após um clique. Agora, vamos carregar os países automaticamente quando o componente `App` aparecer na tela.

## Pré-requisitos

- O fluxo `fetch` → JSON → estado apresentado em [09 - Consumo simplificado da API do IBGE](./09_HTTP_APIs_IBGE_Simplificado.md)
- `useState`, componentes e renderização de listas

## 1. Execute a busca ao abrir a tela

No `src/App.jsx`, importe `useEffect` e coloque a busca dentro de um efeito com uma lista de dependências vazia:

```jsx
import { useEffect, useState } from 'react';

const API_URL = 'https://servicodados.ibge.gov.br/api/v1/paises';

function App() {
  const [countries, setCountries] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState('');

  useEffect(() => {
    const loadCountries = async () => {
      try {
        const response = await fetch(API_URL);

        if (!response.ok) {
          throw new Error('Não foi possível carregar os países.');
        }

        const data = await response.json();
        const mappedCountries = data.map((country) => ({
          id: country.id['ISO-3166-1-ALPHA-3'],
          name: country.nome.abreviado,
          capital: country.governo?.capital?.nome ?? 'Não informada',
          region: country.localizacao?.regiao?.nome ?? 'Não informada'
        }));

        setCountries(mappedCountries);
      } catch (requestError) {
        setError(requestError.message || 'Ocorreu um erro ao buscar os países.');
      } finally {
        setIsLoading(false);
      }
    };

    loadCountries();
  }, []);

  if (isLoading) {
    return <p>Carregando países...</p>;
  }

  if (error) {
    return <p role="alert">Erro: {error}</p>;
  }

  return (
    <main>
      <h1>Países do IBGE</h1>
      <p>Total de países: {countries.length}</p>
      <ul>
        {countries.map((country) => (
          <li key={country.id}>
            <strong>{country.name}</strong> — Capital: {country.capital} —
            Região: {country.region}
          </li>
        ))}
      </ul>
    </main>
  );
}

export default App;
```

## 2. O que mudou?

- `useEffect` executa a busca após a primeira renderização.
- O array vazio `[]` indica que o efeito não depende de valores que mudam.
- `isLoading` começa como `true`, porque os dados são buscados assim que a tela abre.
- Os estados de carregamento, erro e sucesso controlam o que a interface mostra.

O callback passado a `useEffect` não deve ser declarado como `async`. Em vez disso, criamos a função assíncrona `loadCountries` dentro do efeito e a chamamos ali.

Se o projeto usar `<React.StrictMode>`, é possível observar mais de uma execução do efeito durante o desenvolvimento. Isso é intencional no modo de desenvolvimento e ajuda a identificar efeitos que não lidam corretamente com montagens repetidas.

## Exercício

Mostre uma mensagem de sucesso junto ao total de países carregados. Confira também a tela com a conexão desligada para observar a mensagem de erro.

## Próximo passo

Com os países carregados automaticamente, você pode continuar para os roteiros de filtros e aplicar critérios à lista recebida.
