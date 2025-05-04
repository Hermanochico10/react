# Aula 1 — Introdução ao React: JSX, Componentes e Props

## 🎯 Objetivos da Aula

- Entender o que é React.
- Compreender a diferença entre JavaScript e JSX.
- Criar um projeto React moderno usando Vite.
- Limpar e organizar o projeto inicial.
- Resetar o CSS global do navegador.
- Criar componentes funcionais no React.
- Entender e aplicar props em componentes.
- Praticar criando o componente ProfileCard.

---

## 1️⃣ O que é o React?

React é uma biblioteca JavaScript criada pelo Facebook para facilitar o desenvolvimento de interfaces de usuário.

### 🚀 Vantagens

- Componentização: dividir a UI em partes menores.
- Atualização eficiente via Virtual DOM.
- Fluxo de dados unidirecional.
- Grande ecossistema.

---

## 2️⃣ Diferença entre JavaScript e JSX

| JavaScript | JSX |
| :--- | :--- |
| Código tradicional JavaScript | Extensão que mistura HTML dentro do JavaScript |
| DOM manual | Interface declarativa |
| Mais verboso | Mais legível |

### Exemplo JavaScript puro:

```javascript
const element = document.createElement('h1');
element.textContent = 'Olá, Mundo!';
document.body.appendChild(element);
```

### Exemplo JSX:

```jsx
function App() {
  return <h1>Olá, Mundo!</h1>;
}
```

---

## 3️⃣ O que é o Vite?

Vite é uma ferramenta de build moderna para desenvolvimento front-end.

### 📦 Benefícios:

- Inicialização instantânea.
- HMR (Hot Module Replacement) rápido.
- Build otimizado para produção.

---

## 4️⃣ Criando o Projeto React com Vite

```bash
npm create vite@latest meu-projeto
# Escolha React -> JavaScript
cd meu-projeto
npm install
npm run dev
```

---

## 5️⃣ Limpando o Projeto Inicial

- Delete os arquivos:
  - `src/index.css`
  - `src/App.css`
- Remova suas importações de:
  - `src/main.jsx`
  - `src/App.jsx`

---

## 6️⃣ Resetando o CSS Global

Crie o arquivo:

```
src/styles/global.css
```

Conteúdo:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #f5f5f5;
  min-height: 100vh;
}
```

Importe no `App.jsx`:

```jsx
import './styles/global.css';
```

---

## 7️⃣ Estrutura de Pastas

```
src/
  components/
    Header/
      Header.jsx
      Header.css
  styles/
    global.css
  App.jsx
  main.jsx
```

---

## 8️⃣ Criando o Componente Header Fixo

### src/components/Header/Header.jsx

```jsx
import React from 'react';
import './Header.css';

/**
 * Componente Header fixo
 */
function Header() {
  return (
    <header className="header">
      <div className="logo">
        <h1>MeuLogo</h1>
      </div>
      <nav className="navigation">
        <ul>
          <li><a href="#">Início</a></li>
          <li><a href="#">Sobre</a></li>
          <li><a href="#">Contato</a></li>
        </ul>
      </nav>
      <div className="search">
        <input type="text" placeholder="Buscar..." />
      </div>
    </header>
  );
}

export default Header;
```

### src/components/Header/Header.css

```css
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #fff;
  padding: 10px 20px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.logo h1 {
  font-size: 24px;
  color: #333;
}

.navigation ul {
  display: flex;
  list-style: none;
  gap: 20px;
}

.navigation a {
  text-decoration: none;
  color: #333;
  font-weight: bold;
}

.search input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
```

---

## 9️⃣ Entendendo Importação e Exportação

- Importar componente:

```jsx
import Header from './components/Header/Header';
```

- Exportar componente:

```jsx
export default Header;
```

---

## 🔟 Introdução às Props

Props (propriedades) são dados passados de um componente pai para um filho.

### Exemplo básico:

```jsx
function Button({ text }) {
  return <button>{text}</button>;
}
```

Uso:

```jsx
<Button text="Clique aqui" />
```

---

## 1️⃣1️⃣ Atualizando o Header para Usar Props

### src/components/Header/Header.jsx (Atualizado)

```jsx
import React from 'react';
import './Header.css';

/**
 * Componente Header com prop de logotipo
 */
function Header({ logotipo }) {
  return (
    <header className="header">
      <div className="logo">
        <h1>{logotipo}</h1>
      </div>
      <nav className="navigation">
        <ul>
          <li><a href="#">Início</a></li>
          <li><a href="#">Sobre</a></li>
          <li><a href="#">Contato</a></li>
        </ul>
      </nav>
      <div className="search">
        <input type="text" placeholder="Buscar..." />
      </div>
    </header>
  );
}

export default Header;
```

No `App.jsx`:

```jsx
import React from 'react';
import Header from './components/Header/Header';
import './styles/global.css';

function App() {
  return (
    <>
      <Header logotipo="MeuSite" />
      <main>
        <h2>Bem-vindo ao Site!</h2>
        <p>Conteúdo principal aqui!</p>
      </main>
    </>
  );
}

export default App;
```

---

## 1️⃣2️⃣ Exercício: Criar o ProfileCard

### Instruções

- Criar `ProfileCard` como novo componente.
- Receber props: `nome`, `idade`, `profissao`.
- Exibir as informações.
- Botão que alerta `Olá, [nome]!`.

---

## 1️⃣3️⃣ Solução do Exercício

### src/components/ProfileCard/ProfileCard.jsx

```jsx
import React from 'react';
import './ProfileCard.css';

/**
 * Componente ProfileCard
 */
function ProfileCard({ nome, idade, profissao }) {
  function saudacao() {
    alert(`Olá, ${nome}!`);
  }

  return (
    <div className="profile-card">
      <h2>{nome}</h2>
      <p>Idade: {idade}</p>
      <p>Profissão: {profissao}</p>
      <button onClick={saudacao}>Dizer Olá</button>
    </div>
  );
}

export default ProfileCard;
```

### src/components/ProfileCard/ProfileCard.css

```css
.profile-card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.profile-card h2 {
  margin-bottom: 10px;
  color: #333;
}

.profile-card p {
  margin-bottom: 5px;
  color: #555;
}

.profile-card button {
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.profile-card button:hover {
  background-color: #0056b3;
}
```

---

Adicionando no `App.jsx`:

```jsx
import ProfileCard from './components/ProfileCard/ProfileCard';

function App() {
  return (
    <>
      <Header logotipo="MeuSite" />
      <main>
        <h2>Bem-vindo ao Site!</h2>
        <p>Conteúdo principal aqui!</p>

        <ProfileCard nome="João Silva" idade={30} profissao="Desenvolvedor" />
      </main>
    </>
  );
}

export default App;
```

---

# 🏁 Conclusão

Nesta aula você aprendeu:

- O que é React e JSX.
- Como iniciar projetos React com Vite.
- Como estruturar projetos organizadamente.
- Como criar e usar componentes.
- Como passar dados com props.

