# 🧪 Exercícios da Aula 2 — React: Estado, Eventos e Estilização com styled-components

---

## ✅ Exercício 1 — Formulário Controlado com Validação

### Objetivo

Criar um componente `FormularioContato` com os campos: nome, idade e profissão.  
Todos os inputs devem ser controlados com `useState`.  
Ao submeter, mostrar um `alert` com os dados formatados.  
Implementar validação para garantir que todos os campos estejam preenchidos.

---

### 📁 Estrutura de Arquivos

```
src/
└── components/
    └── FormularioContato/
        ├── index.jsx
        └── styles.js
```

---

### 📄 Arquivo: `src/components/FormularioContato/index.jsx`

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

---

### 📄 Arquivo: `src/components/FormularioContato/styles.js`

```jsx
import styled from 'styled-components';

export const Formulario = styled.form`
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 300px;
  margin: 0 auto;
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

### Objetivo

Criar um array com objetos representando pessoas (nome e profissão).  
Criar componente `Card` estilizado com `styled-components`.  
Exibir os cards em grid usando `display: grid`.  
Responsivo para:
- 1 coluna (mobile)
- 2 colunas (tablet)
- 4 colunas (desktop)

---

### 📁 Estrutura de Arquivos

```
src/
└── components/
    ├── Card/
    │   ├── index.jsx
    │   └── styles.js
    └── CardGrid/
        ├── index.jsx
        └── styles.js
```

---

### 📄 Arquivo: `src/components/Card/index.jsx`

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

---

### 📄 Arquivo: `src/components/Card/styles.js`

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

### 📄 Arquivo: `src/components/CardGrid/index.jsx`

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

---

### 📄 Arquivo: `src/components/CardGrid/styles.js`

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

## 📦 Dependência necessária

```bash
npm install styled-components
```
