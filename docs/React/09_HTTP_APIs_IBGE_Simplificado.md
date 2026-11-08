---
id: 09_HTTP_APIs_IBGE_Simplificado
title: 09 - Consumo simplificado da API do IBGE
---

# 09 - Consumo simplificado da API do IBGE

Neste roteiro, vamos buscar países da API do IBGE quando a pessoa clicar em um botão. O objetivo é acompanhar o caminho dos dados: fazer a requisição com `fetch`, converter a resposta JSON e guardar os países no estado do React.

## Pré-requisitos

- Componentes, JSX e eventos de clique
- `useState` e atualização de estado
- Uma aplicação React criada com Vite

## 1. Conheça o endereço da API

A API de países do IBGE está disponível em:

```text
https://servicodados.ibge.gov.br/api/v1/paises
```

Abra o endereço no navegador para ver a resposta. Ela é uma lista de países em JSON. Cada item contém informações como o nome, a capital e a região.

## 2. Busque os países ao clicar

No `src/App.jsx`, crie um estado para a lista e uma função que busca os dados. O `fetch` faz a requisição; `response.json()` converte a resposta para valores que o JavaScript pode usar.

```jsx
import { useState } from 'react';

const API_URL = 'https://servicodados.ibge.gov.br/api/v1/paises';

function App() {
  const [countries, setCountries] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState('');

  const loadCountries = async () => {
    setIsLoading(true);
    setError('');

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

  return (
    <main>
      <h1>Países do IBGE</h1>

      <button onClick={loadCountries} disabled={isLoading}>
        {isLoading ? 'Carregando...' : 'Carregar países'}
      </button>

      {error && <p role="alert">Erro: {error}</p>}

      {countries.length > 0 && (
        <>
          <p>Total de países: {countries.length}</p>
          <ul>
            {countries.map((country) => (
              <li key={country.id}>
                <strong>{country.name}</strong> — Capital: {country.capital} —
                Região: {country.region}
              </li>
            ))}
          </ul>
        </>
      )}
    </main>
  );
}

export default App;
```

## 3. Entenda o fluxo

1. O clique no botão chama `loadCountries`.
2. `fetch` solicita os dados ao IBGE.
3. `response.ok` verifica se a resposta HTTP foi bem-sucedida.
4. `response.json()` lê a lista recebida.
5. `map` seleciona os campos que a tela precisa.
6. `setCountries` atualiza o estado e o React renderiza a lista.
7. `try`, `catch` e `finally` tratam erro e encerram o indicador de carregamento.

O formato da resposta do IBGE não é o mesmo formato que exibimos na tela. Por isso, criamos `mappedCountries` com apenas os campos usados pelo exemplo.

## Exercício

Adicione à lista o código ISO de duas letras de cada país. Consulte a resposta da API para encontrar o campo correspondente.

## Próximo passo

Neste exemplo, a busca acontece após um clique. Em [10 - Carregamento automático com useEffect e IBGE](./10_useEffect_IBGE_Simplificado.md), vamos iniciar a mesma busca quando a tela abrir.
