# Aula 2 — React: Estado, Eventos e Estilização com styled-components

---

## 🎯 Objetivos da Aula

- Compreender o uso do `useState` para gerenciamento de estado em componentes funcionais.
- Manipular eventos como `onClick`, `onChange` e `onSubmit`.
- Criar formulários controlados em React com validação.
- Estilizar componentes utilizando `styled-components`, incluindo temas e responsividade.
- Configurar e estruturar um projeto React com Vite, utilizando `GlobalStyle`.

---

## ⚙️ Configuração do Projeto com Vite

### 1. Pré-requisitos

- Node.js instalado: https://nodejs.org/

### 2. Criar o Projeto

```bash
npm create vite@latest nome-do-projeto -- --template react
cd nome-do-projeto
npm install
```

### 3. Instalar styled-components

```bash
npm install styled-components
```

---

## 🗂️ Estrutura de Pastas e Arquivos

```
src/
├── assets/
│   └── images/
├── components/
│   ├── Button/
│   │   ├── index.jsx
│   │   └── styles.js
│   ├── Card/
│   │   └── index.jsx
│   └── Form/
│       ├── index.jsx
│       └── styles.js
├── pages/
│   ├── Home/
│   │   ├── index.jsx
│   │   └── styles.js
│   └── About/
│       ├── index.jsx
│       └── styles.js
├── styles/
│   ├── GlobalStyle.js
│   └── theme.js
├── App.jsx
└── main.jsx
```

---

## 🧠 Conceitos Fundamentais

### 🔹 O que é estado em React?

Estado é qualquer informação que pode mudar ao longo do tempo e que afeta o que é exibido na interface. Em React, utilizamos o hook `useState` para adicionar estado a componentes funcionais.

### 🔹 Por que usar `useState`?

Antes dos Hooks, apenas componentes de classe podiam ter estado. Com `useState`, podemos adicionar estado a componentes funcionais, tornando-os mais simples e fáceis de entender.

### 🔹 Por que usar styled-components?

- Permite escrever CSS dentro do JavaScript, promovendo maior coesão entre estilo e lógica.
- Evita conflitos de nomes de classes, pois os estilos são escopados ao componente.
- Facilita a criação de temas dinâmicos e reutilização de estilos.

---

## 💡 Exemplo 1 — Contador Simples

**Arquivo:** `src/components/Contador/index.jsx`

```jsx
import { useState } from 'react'
import { Botao } from './styles'

export function Contador() {
  const [contador, setContador] = useState(0)

  const incrementar = () => {
    setContador(contador + 1)
  }

  return (
    <div>
      <p>Valor atual: {contador}</p>
      <Botao onClick={incrementar}>Incrementar</Botao>
    </div>
  )
}
```

**Arquivo:** `src/components/Contador/styles.js`

```jsx
import styled from 'styled-components'

export const Botao = styled.button`
  padding: 10px 20px;
  margin-top: 20px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
`
```

---

## 💡 Exemplo 2 — Formulário Controlado com Validação

**Arquivo:** `src/components/FormularioContato/index.jsx`

```jsx
import { useState } from 'react'
import { Formulario, Input, Botao, Erro } from './styles'

export function FormularioContato() {
  const [nome, setNome] = useState('')
  const [email, setEmail] = useState('')
  const [erro, setErro] = useState('')

  const handleSubmit = (e) => {
    e.preventDefault()

    if (nome.trim() === '' || email.trim() === '') {
      setErro('Por favor, preencha todos os campos.')
      return
    }

    setErro('')
    alert(`Nome: ${nome}\nEmail: ${email}`)
  }

  return (
    <Formulario onSubmit={handleSubmit}>
      <Input
        type="text"
        placeholder="Digite seu nome"
        value={nome}
        onChange={(e) => setNome(e.target.value)}
      />
      <Input
        type="email"
        placeholder="Digite seu email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      {erro && <Erro>{erro}</Erro>}
      <Botao type="submit">Enviar</Botao>
    </Formulario>
  )
}
```

**Arquivo:** `src/components/FormularioContato/styles.js`

```jsx
import styled from 'styled-components'

export const Formulario = styled.form`
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 300px;
  margin: 0 auto;
`

export const Input = styled.input`
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
`

export const Botao = styled.button`
  padding: 8px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
`

export const Erro = styled.span`
  color: red;
  font-size: 12px;
`
```

---

## 💡 Exemplo 3 — Tema Claro e Escuro com GlobalStyle

**Arquivo:** `src/components/AlternarTema/index.jsx`

```jsx
import { useState } from 'react'
import { ThemeProvider } from 'styled-components'
import { GlobalStyle } from '../../styles/GlobalStyle'
import { temaClaro, temaEscuro } from '../../styles/theme'
import { Container, Botao } from './styles'

export function AlternarTema() {
  const [modoEscuro, setModoEscuro] = useState(false)

  const alternarTema = () => {
    setModoEscuro(!modoEscuro)
  }

  return (
    <ThemeProvider theme={modoEscuro ? temaEscuro : temaClaro}>
      <GlobalStyle />
      <Container>
        <p>Tema atual: {modoEscuro ? 'Escuro' : 'Claro'}</p>
        <Botao onClick={alternarTema}>Alternar Tema</Botao>
      </Container>
    </ThemeProvider>
  )
}
```

**Arquivo:** `src/components/AlternarTema/styles.js`

```jsx
import styled from 'styled-components'

export const Container = styled.div`
  padding: 20px;
  border-radius: 8px;
  text-align: center;
`

export const Botao = styled.button`
  margin-top: 10px;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background-color: ${({ theme }) => theme.botaoFundo};
  color: ${({ theme }) => theme.botaoTexto};
`
```

**Arquivo:** `src/styles/GlobalStyle.js`

```jsx
import { createGlobalStyle } from 'styled-components'

export const GlobalStyle = createGlobalStyle`
  body {
    margin: 0;
    padding: 0;
    background-color: ${({ theme }) => theme.fundo};
    color: ${({ theme }) => theme.texto};
    font-family: Arial, sans-serif;
  }
`
```

**Arquivo:** `src/styles/theme.js`

```jsx
export const temaClaro = {
  fundo: '#f9f9f9',
  texto: '#222',
  botaoFundo: '#007bff',
  botaoTexto: '#fff'
}

export const temaEscuro = {
  fundo: '#222',
  texto: '#f9f9f9',
  botaoFundo: '#0056b3',
  botaoTexto: '#fff'
}
```

---

## 💡 Exemplo 4 — Card com CSS-in-JS embutido

**Arquivo:** `src/components/Card/index.jsx`

```jsx
import styled from 'styled-components'

// Estilos definidos diretamente no mesmo arquivo
const CardContainer = styled.div`
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 16px;
  text-align: center;
`

const Titulo = styled.h3`
  margin: 0 0 8px 0;
`

const Descricao = styled.p`
  margin: 0;
`

export function Card({ titulo, descricao }) {
  return (
    <CardContainer>
      <Titulo>{titulo}</Titulo>
      <Descricao>{descricao}</Descricao>
    </CardContainer>
  )
}
```

---

### 📌 Observação Didática

> Neste componente, usamos `styled-components` diretamente no mesmo arquivo do componente.  
> Essa abordagem é válida especialmente quando os estilos são simples e exclusivos.  
> Para estilos mais reutilizáveis, manter um `styles.js` é mais organizado.

---

## 🧪 Exercícios Propostos

### Exercício 1 — Formulário Completo

- Criar um componente `FormularioContato`.
- Campos: nome, idade, profissão.
- Todos os inputs devem ser controlados com `useState`.
- Ao submeter, mostrar um `alert` com os dados formatados.
- Implementar validação para garantir que todos os campos estejam preenchidos.

### Exercício 2 — Grid de Cards Responsivos

- Criar um array com objetos representando pessoas (nome e profissão).
- Criar componente `Card` estilizado com styled-components.
- Exibir os cards em grid usando `display: grid`.
- Responsivo para 1 coluna (mobile), 2 colunas (tablet), 4 colunas (desktop).
