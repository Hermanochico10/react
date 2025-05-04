# Aula 2 — React: Estado, Eventos, Estilização com styled-components e Estrutura com Vite

---

## 🎯 Objetivos da Aula

- Compreender o que é e por que usar o hook `useState`
- Entender como o estado torna componentes reativos
- Manipular eventos como `onClick`, `onChange` e `onSubmit`
- Criar um formulário controlado com estado
- Estilizar componentes com `styled-components` ao invés de `className`
- Criar tema claro/escuro com `ThemeProvider`
- Criar e organizar a estrutura de um projeto com Vite

---

## ⚙️ Configuração do Projeto com Vite

### Pré-requisitos

- Node.js instalado → https://nodejs.org/

### Criar o Projeto

```bash
npm create vite@latest aula-react -- --template react
cd aula-react
npm install
npm install styled-components
```

### Estrutura Sugerida

```
src/
├── components/
│   ├── FormularioContato/
│   │   └── index.jsx
│   ├── CardGrid/
│   │   └── index.jsx
│   └── Tema/
│       └── index.jsx
├── styles/
│   ├── GlobalStyle.js
│   └── theme.js
├── App.jsx
└── main.jsx
```

---

## 🧠 Explicações Fundamentais

### 🔹 O que é estado?

Estado é qualquer informação que **muda com o tempo** e que precisa ser **refletida na interface**. Exemplo: input digitado, botão clicado, tema ativo etc.

### 🔹 Por que usamos `useState`?

Antes dos Hooks, só componentes de classe tinham estado. Com `useState`, **componentes funcionais modernos** se tornam dinâmicos.

```js
const [valor, setValor] = useState(inicial)
```

- `valor` → o dado armazenado
- `setValor` → função para atualizar o valor e renderizar o componente novamente

### 🔹 Por que Hooks e componentização?

- Cada componente cuida do seu próprio estado
- Lógica e estrutura ficam organizadas e reutilizáveis
- Escalabilidade em projetos React reais

### 🔹 Por que usamos `styled-components`?

- Estilo encapsulado dentro do componente
- Sem conflitos de CSS
- Temas dinâmicos
- Maior legibilidade e coesão
- Abandona o `className` e separação forçada entre HTML e CSS

---

## 🧪 Exercício 1 — Formulário Controlado

### `src/components/FormularioContato/index.jsx`

```jsx
import { useState } from 'react'
import styled from 'styled-components'

const Form = styled.form`
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 300px;
  margin: 0 auto;
`

const Input = styled.input`
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
`

const Button = styled.button`
  padding: 8px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
`

export function FormularioContato() {
  const [nome, setNome] = useState('')
  const [idade, setIdade] = useState('')
  const [profissao, setProfissao] = useState('')

  function handleSubmit(e) {
    e.preventDefault()
    alert(`Nome: ${nome}\nIdade: ${idade}\nProfissão: ${profissao}`)
  }

  return (
    <Form onSubmit={handleSubmit}>
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
      <Button type="submit">Enviar</Button>
    </Form>
  )
}
```

---

## 🧪 Exercício 2 — Grid de Cards Responsivos

### `src/components/CardGrid/index.jsx`

```jsx
import styled from 'styled-components'

const Grid = styled.div`
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  padding: 20px;
`

const Card = styled.div`
  background: white;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 0 6px rgba(0,0,0,0.1);
  text-align: center;
`

const Button = styled.button`
  margin-top: 10px;
  padding: 6px 12px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
`

const cards = [
  { nome: 'Ana', profissao: 'Designer' },
  { nome: 'Bruno', profissao: 'Dev Front-end' },
  { nome: 'Carlos', profissao: 'Dev Back-end' },
  { nome: 'Diana', profissao: 'Product Owner' },
  { nome: 'Eduardo', profissao: 'QA' },
  { nome: 'Fernanda', profissao: 'UX Researcher' }
]

export function CardGrid() {
  return (
    <Grid>
      {cards.map((card, index) => (
        <Card key={index}>
          <h3>{card.nome}</h3>
          <p>{card.profissao}</p>
          <Button>Curtir</Button>
        </Card>
      ))}
    </Grid>
  )
}
```

---

## 🧪 Exercício 3 — Tema Dinâmico com styled-components

### `src/components/Tema/index.jsx`

```jsx
import { useState } from 'react'
import styled, { ThemeProvider } from 'styled-components'
import { lightTheme, darkTheme } from '../../styles/theme'

const Container = styled.div`
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  background-color: ${({ theme }) => theme.background};
  color: ${({ theme }) => theme.text};
`

const Button = styled.button`
  margin-top: 10px;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background-color: ${({ theme }) => theme.buttonBackground};
  color: ${({ theme }) => theme.buttonText};
`

export function Tema() {
  const [modoEscuro, setModoEscuro] = useState(false)

  return (
    <ThemeProvider theme={modoEscuro ? darkTheme : lightTheme}>
      <Container>
        <p>Tema atual: {modoEscuro ? 'Escuro' : 'Claro'}</p>
        <Button onClick={() => setModoEscuro(!modoEscuro)}>
          Alternar Tema
        </Button>
      </Container>
    </ThemeProvider>
  )
}
```

### `src/styles/theme.js`

```js
export const lightTheme = {
  background: '#f9f9f9',
  text: '#222',
  buttonBackground: '#007bff',
  buttonText: '#fff'
}

export const darkTheme = {
  background: '#222',
  text: '#f9f9f9',
  buttonBackground: '#0056b3',
  buttonText: '#fff'
}
```

---

## ✅ App principal

### `src/App.jsx`

```jsx
import { FormularioContato } from './components/FormularioContato'
import { CardGrid } from './components/CardGrid'
import { Tema } from './components/Tema'

function App() {
  return (
    <>
      <FormularioContato />
      <CardGrid />
      <Tema />
    </>
  )
}

export default App
```

---

## ✅ Conclusão

- O `useState` permite criar componentes dinâmicos e reativos.
- Hooks como `useState` tornam o código funcional mais limpo e moderno.
- styled-components encapsula o estilo com o componente.
- O projeto React deve ser estruturado de forma modular, clara e escalável.
