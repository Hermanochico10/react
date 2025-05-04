# 🧪 Gabarito Completo — Projeto React com Vite e styled-components

---

## ⚙️ Criação do Projeto

### Pré-requisitos

- Node.js instalado

### Criar projeto com Vite

```bash
npm create vite@latest meu-projeto -- --template react
cd meu-projeto
npm install
```

### Instalar styled-components

```bash
npm install styled-components
```

---

## 🗂️ Estrutura do Projeto

```
src/
├── components/
│   ├── Card/
│   │   ├── index.jsx
│   │   └── styles.js
│   ├── CardGrid/
│   │   ├── index.jsx
│   │   └── styles.js
│   └── FormularioContato/
│       ├── index.jsx
│       └── styles.js
├── styles/
│   ├── GlobalStyle.js
│   └── theme.js       (se desejar implementar tema depois)
├── App.jsx
└── main.jsx
```

---

## 📄 Arquivo: `src/main.jsx`

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

---

## 📄 Arquivo: `src/App.jsx`

```jsx
import { FormularioContato } from './components/FormularioContato';
import { CardGrid } from './components/CardGrid';
import { GlobalStyle } from './styles/GlobalStyle';

function App() {
  return (
    <>
      <GlobalStyle />
      <h1 style={{ textAlign: 'center' }}>Exercícios da Aula 2</h1>
      <FormularioContato />
      <CardGrid />
    </>
  );
}

export default App;
```

---

## 📄 Arquivo: `src/styles/GlobalStyle.js`

```jsx
import { createGlobalStyle } from 'styled-components';

export const GlobalStyle = createGlobalStyle`
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'Arial', sans-serif;
    background-color: #f4f4f4;
    color: #333;
  }

  h1 {
    margin: 40px 0 20px;
  }
`;
```

---

## ✅ Exercício 1 — Formulário Controlado

### 📄 `src/components/FormularioContato/index.jsx`

```jsx
import { useState } from 'react';
import { Formulario, Input, Botao, Erro } from './styles';

export function FormularioContato() {
  const [nome, setNome] = useState('');
  const [idade, setIdade] = useState('');
  const [profissao, setProfissao] = useState('');
  const [erro, setErro] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();

    if (!nome || !idade || !profissao) {
      setErro('Por favor, preencha todos os campos.');
      return;
    }

    setErro('');
    alert(`Nome: ${nome}\nIdade: ${idade}\nProfissão: ${profissao}`);
  };

  return (
    <Formulario onSubmit={handleSubmit}>
      <Input
        type="text"
        placeholder="Nome"
        value={nome}
        onChange={(e) => setNome(e.target.value)}
      />
      <Input
        type="number"
        placeholder="Idade"
        value={idade}
        onChange={(e) => setIdade(e.target.value)}
      />
      <Input
        type="text"
        placeholder="Profissão"
        value={profissao}
        onChange={(e) => setProfissao(e.target.value)}
      />
      {erro && <Erro>{erro}</Erro>}
      <Botao type="submit">Enviar</Botao>
    </Formulario>
  );
}
```

### 📄 `src/components/FormularioContato/styles.js`

```jsx
import styled from 'styled-components';

export const Formulario = styled.form`
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 300px;
  margin: 0 auto 40px;
`;

export const Input = styled.input`
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
`;

export const Botao = styled.button`
  padding: 8px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
`;

export const Erro = styled.span`
  color: red;
  font-size: 12px;
`;
```

---

## ✅ Exercício 2 — Grid de Cards Responsivos

### 📄 `src/components/Card/index.jsx`

```jsx
import { CardContainer, Titulo, Descricao, Botao } from './styles';

export function Card({ nome, profissao }) {
  return (
    <CardContainer>
      <Titulo>{nome}</Titulo>
      <Descricao>{profissao}</Descricao>
      <Botao>Curtir</Botao>
    </CardContainer>
  );
}
```

### 📄 `src/components/Card/styles.js`

```jsx
import styled from 'styled-components';

export const CardContainer = styled.div`
  background: white;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 0 6px rgba(0,0,0,0.1);
  text-align: center;
`;

export const Titulo = styled.h3`
  margin: 0 0 8px 0;
`;

export const Descricao = styled.p`
  margin: 0;
`;

export const Botao = styled.button`
  margin-top: 10px;
  padding: 6px 12px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    background-color: #218838;
  }
`;
```

---

### 📄 `src/components/CardGrid/index.jsx`

```jsx
import { Grid } from './styles';
import { Card } from '../Card';

const pessoas = [
  { nome: 'Ana', profissao: 'Designer' },
  { nome: 'Bruno', profissao: 'Dev Front-end' },
  { nome: 'Carlos', profissao: 'Dev Back-end' },
  { nome: 'Diana', profissao: 'Product Owner' },
  { nome: 'Eduardo', profissao: 'QA' },
  { nome: 'Fernanda', profissao: 'UX Researcher' }
];

export function CardGrid() {
  return (
    <Grid>
      {pessoas.map((pessoa, index) => (
        <Card key={index} nome={pessoa.nome} profissao={pessoa.profissao} />
      ))}
    </Grid>
  );
}
```

### 📄 `src/components/CardGrid/styles.js`

```jsx
import styled from 'styled-components';

export const Grid = styled.div`
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  padding: 20px;
`;
```

---

## ✅ Resultado Esperado

- Um formulário funcional com validação local e feedback.
- Um grid de cards estilizados, totalmente responsivo.
- Projeto React moderno usando Vite e styled-components.
- Arquitetura de pastas organizada para escalar.
