---
id: 06b_useState_Aplicado
title: 06b - Estado com useState: aplicação
---

# 06b - **Estado com useState: aplicação**

Nesta segunda parte, vamos aplicar o estado em um exemplo maior. Antes de continuar, pratique o contador e a alternância apresentados em [06_useState.md](./06_useState.md).

## Evoluindo o Projeto: Adicionando Interatividade

Vamos adicionar funcionalidades interativas ao nosso projeto "Lista de Países" usando useState.

### Funcionalidades a Implementar:

1. **Favoritar países**: Marcar/desmarcar países como favoritos
2. **Contador de favoritos**: Mostrar quantos países foram favoritados
3. **Filtro de favoritos**: Mostrar apenas países favoritos

### 1. Componente com Estado - Favoritos

```jsx
// src/components/CountryCard.jsx
function CountryCard({ id, flag, name, capital, population, language, isFavorite = false, onToggleFavorite }) {
  // Função para lidar com o clique no card
  const handleCardClick = () => {
    // Alterna o estado de favorito ao clicar no card
    onToggleFavorite?.(id);
  };

  return (
    <div 
      className={`country-card ${isFavorite ? 'favorite' : ''}`}
      onClick={handleCardClick}
    >
      <div className="country-header">
        <span className="flag">{flag}</span>
        <h3>{name}</h3>
        <button 
          className="favorite-btn"
          // Evita que o clique no botão propague para o card
          onClick={(e) => { e.stopPropagation(); onToggleFavorite?.(id); }}
          // Exibe uma mensagem de tooltip ao passar o mouse sobre o botão
          title={isFavorite ? 'Remover dos favoritos' : 'Adicionar aos favoritos'}
        >
          // Exibe um coração preenchido ou vazio dependendo do estado de favorito
          {isFavorite ? '❤️' : '🤍'}
        </button>
      </div>
      <div className="country-info">
        <p><strong>Capital:</strong> {capital}</p>
        <p><strong>População:</strong> {population}</p>
        <p><strong>Idioma:</strong> {language}</p>
        // Exibe um badge de favorito se o país estiver marcado como favorito
        {isFavorite && <p className="favorite-badge">⭐ Favorito</p>}
      </div>
    </div>
  );
}

export default CountryCard;
```

### 2. Contador de Favoritos no Header

```jsx
// src/components/Header.jsx
function Header({ title, subtitle, favoriteCount  }) {
  return (
    <header className="app-header">
      <h1>{title}</h1>
      {subtitle && <p>{subtitle}</p>}

      <div className="favorite-counter">
        <span>❤️ {favoriteCount} países favoritos</span>
      </div>

    </header>
  );
}
export default Header;
```

### 3. App com Estado Global

```jsx
// src/App.jsx
import { useState } from 'react';
import './App.css';
import CountryGrid from './components/CountryGrid';
import Header from './components/Header';

function App() {
  // Estado inicial com lista de países
  const [countries, setCountries] = useState([
    { id: 1, flag: "🇧🇷", name: "Brasil", capital: "Brasília", population: "215 milhões", language: "Português" },
    { id: 2, flag: "🇦🇷", name: "Argentina", capital: "Buenos Aires", population: "45 milhões", language: "Espanhol" },
    { id: 3, flag: "🇨🇱", name: "Chile", capital: "Santiago", population: "19 milhões", language: "Espanhol" },
    { id: 4, flag: "🇺🇾", name: "Uruguai", capital: "Montevidéu", population: "3.5 milhões", language: "Espanhol" },
    { id: 5, flag: "🇵🇪", name: "Peru", capital: "Lima", population: "33 milhões", language: "Espanhol" },
    { id: 6, flag: "🇨🇴", name: "Colômbia", capital: "Bogotá", population: "51 milhões", language: "Espanhol" }
  ]);
  // Armazena os IDs dos países favoritos
  const [favorites, setFavorites] = useState([]);
  // Estado para controlar se apenas favoritos devem ser mostrados
  const [showOnlyFavorites, setShowOnlyFavorites] = useState(false);

  // Função para alternar o estado de favorito de um país
  const toggleFavorite = (id) => {
    setFavorites((prev) =>
      prev.includes(id) ? prev.filter((fid) => fid !== id) : [...prev, id]
    );
  };

  const favoriteCount = favorites.length;
  // Filtra os países a serem exibidos com base no estado de filtro
  const visibleCountries = showOnlyFavorites
    ? countries.filter((c) => favorites.includes(c.id))
    : countries;

  return (
    <div className="app">
      <Header 
        title="🌍 Lista de Países da América do Sul"
        subtitle="Explore países sul-americanos e suas informações"
        favoriteCount={favoriteCount}
      />
      
      <div className="controls">
        <button 
          className={`filter-btn ${showOnlyFavorites ? 'active' : ''}`}
          // Alterna o estado de filtro ao clicar no botão
          onClick={() => setShowOnlyFavorites(!showOnlyFavorites)}
        >
          // Exibe o texto do botão com base no estado de filtro
          {showOnlyFavorites ? 'Mostrar Todos' : 'Mostrar Favoritos'}
        </button>
      </div>
      
      <CountryGrid 
        countries={visibleCountries}
        favorites={favorites}
        onToggleFavorite={toggleFavorite}
      />
    </div>
  );
}

export default App;
```

### 4. CountryGrid para "impressão" de países usando map

```jsx
// src/components/CountryGrid.jsx
import CountryCard from './CountryCard';

function CountryGrid({ countries, favorites = [], onToggleFavorite }) {
  return (
    <div className="country-grid">
      {countries.map((country) => (
        <CountryCard 
          key={country.id}
          id={country.id}
          flag={country.flag}
          name={country.name}
          capital={country.capital}
          population={country.population}
          language={country.language}
          isFavorite={favorites.includes(country.id)}
          onToggleFavorite={onToggleFavorite}
        />
      ))}
    </div>
  );
}

export default CountryGrid;
```
### 5. CSS Atualizado para Interatividade

```css
/* App.css */
.app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Arial, sans-serif;
}

.app-header {
  text-align: center;
  margin-bottom: 40px;
  padding: 30px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
}

.favorite-counter {
  margin-top: 15px;
  background: rgba(255,255,255,0.2);
  padding: 10px 20px;
  border-radius: 25px;
  display: inline-block;
  font-weight: bold;
}

.controls {
  text-align: center;
  margin-bottom: 30px;
}

.filter-btn {
  background: #3498db;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 25px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  background: #2980b9;
  transform: translateY(-2px);
}

.filter-btn.active {
  background: #e74c3c;
}

.country-card {
  border: 1px solid #e1e8ed;
  border-radius: 15px;
  padding: 25px;
  background: white;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
  transition: all 0.3s ease;
}

.country-card.favorite {
  border-color: #e74c3c;
  box-shadow: 0 3px 15px rgba(231, 76, 60, 0.2);
}

.country-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 15px;
}

.favorite-btn {
  background: none;
  border: none;
  font-size: 1.5em;
  cursor: pointer;
  padding: 5px;
  border-radius: 50%;
  transition: transform 0.2s ease;
}

.favorite-btn:hover {
  transform: scale(1.2);
}

.favorite-badge {
  color: #e74c3c;
  font-weight: bold;
  margin-top: 10px;
}
```

## Conceitos Importantes do useState

### 1. **O valor do estado nesta renderização**
```jsx
function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
    console.log(count); // Ainda mostra o valor desta renderização
  };

  // Na próxima renderização, count terá o valor atualizado.
}
```

Chamar a função setter agenda uma nova renderização; não altera a variável `count` que pertence à renderização atual.

### 2. **Atualizações por Função**
```jsx
// Problemático em múltiplas atualizações
setCount(count + 1);
setCount(count + 1); // Só incrementa 1

// Correto para múltiplas atualizações
setCount(prevCount => prevCount + 1);
setCount(prevCount => prevCount + 1); // Incrementa 2
```

### 3. **Estado com Objetos**
```jsx
const [user, setUser] = useState({ name: '', age: 0 });

// Não modifique diretamente
user.name = 'João'; // Não funciona

// Crie novo objeto
setUser({ ...user, name: 'João' });
```

### 4. **Estado com Arrays**
```jsx
const [items, setItems] = useState([]);

// Adicionar item
setItems([...items, novoItem]);

// Remover item
setItems(items.filter(item => item.id !== idToRemove));

// Atualizar item
setItems(items.map(item => 
  item.id === id ? { ...item, updated: true } : item
));
```

### Exercícios Práticos

**1. Contador Avançado:**
- Criar botões para incrementar, decrementar e resetar
- Adicionar limite mínimo e máximo
- Mostrar mensagens baseadas no valor

**2. Lista de Tarefas:**
- Adicionar novas tarefas
- Marcar como concluída
- Remover tarefas
- Contar tarefas pendentes

**3. Expandir o projeto de países:**
- Adicionar formulário para novos países
- Implementar busca por nome
- Adicionar modo escuro/claro

### Próximos Passos

Agora que você já conhece estado e eventos de clique, pode avançar para uma trilha prática com dados reais:

1. Em [09 - Consumo simplificado da API do IBGE](./09_HTTP_APIs_IBGE_Simplificado.md), carregue países ao clicar em um botão.
2. Em [10 - Carregamento automático com useEffect e IBGE](./10_useEffect_IBGE_Simplificado.md), faça a mesma requisição ao abrir a tela.

Essa trilha introduz a API passo a passo. Os roteiros completos [09_HTTP_APIs.md](./09_HTTP_APIs.md) e [10_useEffect.md](./10_useEffect.md) continuam disponíveis para aprofundamento.

### Resumo

- **useState**: Hook para adicionar estado a componentes
- **Reatividade**: Mudanças no estado re-renderizam o componente
- **Imutabilidade**: Sempre criar novos valores, não modificar existentes
- **Atualização de estado**: A função setter agenda uma nova renderização
- **Função setter**: Use funções para atualizações baseadas no valor anterior
- **Projeto prático**: Lista de países com funcionalidades interativas
- **Próximo passo**: Buscar dados reais de países na API do IBGE
