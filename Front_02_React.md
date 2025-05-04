# Aula 2 — Estado, Eventos e Estilização Responsiva no React

## 🎯 Objetivos da Aula

### Parte 1 — Gerenciamento de Estado e Eventos

- Compreender o que é o “estado” em React.
- Entender o que são e como funcionam os hooks.
- Aprender a usar o useState para controlar o estado.
- Lidar com eventos como onClick, onChange e onSubmit.
- Criar um formulário controlado, onde os dados digitados são sincronizados com o estado.

### Parte 2 — Estilização e Responsividade

- Aplicar CSS moderno em componentes React.
- Criar interfaces responsivas usando Flexbox e Grid.
- Entender as diferenças entre CSS Puro, Styled Components e TailwindCSS.
- Implementar um botão para alternar tema claro/escuro com base no estado.

---

## 1️⃣ O que é “estado” em React?

🧠 Conceito:

Estado é qualquer informação que muda com o tempo e que impacta o que é renderizado na tela.

No React, usamos o estado para armazenar dados dentro do componente e reagir a mudanças. Quando o estado muda, o componente é re-renderizado automaticamente.

---

## 2️⃣ O que é um Hook?

📌 Definição:

Um hook é uma função especial do React que permite acessar recursos internos da biblioteca em componentes funcionais.

Antes dos hooks (em React 15), era necessário usar classes para ter estado e ciclo de vida. Com os hooks (desde o React 16.8), podemos usar tudo isso em componentes funcionais.

🔧 Principais hooks (introdução):

- useState: para armazenar valores que mudam.
- useEffect: para executar efeitos colaterais (como chamadas de API).
- useContext, useReducer, etc. (avançados, mais tarde).

---

## 3️⃣ useState: Primeiro Hook

### 📥 Importação

```js
import { useState } from 'react';
```

### 📚 Exemplo com explicação

```jsx
function Contador() {
  const [contador, setContador] = useState(0);
}
```

Explicação:

- contador: valor atual do estado.
- setContador: função que atualiza esse valor.
- useState(0): define o valor inicial como 0.

---

### 🖥 Exemplo completo

```jsx
function Contador() {
  const [contador, setContador] = useState(0);

  function incrementar() {
    setContador(contador + 1);
  }

  return (
    <div>
      <p>Você clicou {contador} vezes</p>
      <button onClick={incrementar}>Clique aqui</button>
    </div>
  );
}
```

---

## 4️⃣ Manipulação de Eventos no React

🎯 Eventos são funções que reagem a interações do usuário.

Exemplos:

- onClick
- onChange
- onSubmit

### 📚 Exemplo

```jsx
<button onClick={() => alert('Você clicou!')}>Clique</button>
```

---

## 5️⃣ Formulários Controlados

🧠 Conceito:

Em React, formulários devem ser controlados: os inputs não armazenam seus próprios valores, eles só refletem o estado.

💡 Por que fazer isso?

- Validação fácil.
- Envio com dados seguros.
- Comportamento previsível.

### 🖥 Exemplo

```jsx
function Formulario() {
  const [nome, setNome] = useState('');

  function handleSubmit(e) {
    e.preventDefault();
    alert(`Nome: ${nome}`);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input 
        type="text" 
        value={nome} 
        onChange={(e) => setNome(e.target.value)} 
        placeholder="Digite seu nome" 
      />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## 6️⃣ Estilização Responsiva com CSS Moderno

### 🔧 Flexbox (1D)

```css
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

### 🔧 Grid (2D)

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
}
```

---

## 7️⃣ Tema Claro e Escuro

### 🖥 Exemplo

```jsx
function Tema() {
  const [modoEscuro, setModoEscuro] = useState(false);

  const estilo = {
    backgroundColor: modoEscuro ? '#121212' : '#fff',
    color: modoEscuro ? '#fff' : '#000',
    padding: '20px',
    borderRadius: '8px'
  };

  return (
    <div style={estilo}>
      <p>Tema atual: {modoEscuro ? 'Escuro' : 'Claro'}</p>
      <button onClick={() => setModoEscuro(!modoEscuro)}>
        Alternar Tema
      </button>
    </div>
  );
}
```

---

## 🧪 Atividades Práticas

### Atividade Prática 1: Formulário Controlado

- Criar um componente com campos: nome, idade e profissão.
- Armazenar os valores no estado.
- Exibir um alerta com os dados ao submeter.

### Atividade Prática 2: Layout Responsivo com Cards

- Criar um componente com vários “cards” usando Grid.

Responsividade:

- Mobile: 1 coluna  
- Tablet: 2 colunas  
- Desktop: 4 colunas

### Atividade Prática 3: Tema Dinâmico

- Botão que alterna o modo claro/escuro.
- Aplicar os estilos dinamicamente via style ou classes CSS.

---

## 📦 Desafio Extra

- Refatorar um dos componentes usando styled-components.
- Mostrar como aplicar o modo escuro usando props e styled.

---

## 🧠 Conclusão

- O useState é a base do comportamento dinâmico no React.
- Eventos devem ser tratados com funções claras e organizadas.
- Inputs devem ser controlados para garantir previsibilidade.
- CSS moderno (Flexbox e Grid) é essencial para criar interfaces adaptáveis.
- Conceitos como tema escuro são simples de implementar com estado.
