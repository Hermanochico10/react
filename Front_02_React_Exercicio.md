# 🧪 Exercícios da Aula 2 — React: Estado, Eventos e Estilização Responsiva

---

## ✅ Exercício 1 — Formulário Controlado

### Objetivo

Criar um componente que use `useState` para controlar três campos: nome, idade e profissão. Ao submeter, deve exibir os dados via `alert`.

### 📁 Arquivo: `src/components/FormularioContato/FormularioContato.jsx`

```jsx
import React, { useState } from 'react';
import './FormularioContato.css';

function FormularioContato() {
  const [nome, setNome] = useState('');
  const [idade, setIdade] = useState('');
  const [profissao, setProfissao] = useState('');

  function handleSubmit(e) {
    e.preventDefault();
    alert(`Nome: ${nome}\nIdade: ${idade}\nProfissão: ${profissao}`);
  }

  return (
    <form className="formulario" onSubmit={handleSubmit}>
      <input 
        type="text" 
        placeholder="Nome" 
        value={nome} 
        onChange={(e) => setNome(e.target.value)} 
        required
      />
      <input 
        type="number" 
        placeholder="Idade" 
        value={idade} 
        onChange={(e) => setIdade(e.target.value)} 
        required
      />
      <input 
        type="text" 
        placeholder="Profissão" 
        value={profissao} 
        onChange={(e) => setProfissao(e.target.value)} 
        required
      />
      <button type="submit">Enviar</button>
    </form>
  );
}

export default FormularioContato;
```

### 📁 Arquivo: `src/components/FormularioContato/FormularioContato.css`

```css
.formulario {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 300px;
  margin: 0 auto;
}

.formulario input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.formulario button {
  padding: 8px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.formulario button:hover {
  background-color: #0056b3;
}
```

---

## ✅ Exercício 2 — Grid de Cards Responsivos

### Objetivo

Exibir uma lista de cards em uma grade (`Grid`), com responsividade para mobile, tablet e desktop.

### 📁 Arquivo: `src/components/CardGrid/CardGrid.jsx`

```jsx
import React from 'react';
import './CardGrid.css';

const cards = [
  { nome: 'Ana', profissao: 'Designer' },
  { nome: 'Bruno', profissao: 'Dev Front-end' },
  { nome: 'Carlos', profissao: 'Dev Back-end' },
  { nome: 'Diana', profissao: 'Product Owner' },
  { nome: 'Eduardo', profissao: 'QA' },
  { nome: 'Fernanda', profissao: 'UX Researcher' }
];

function CardGrid() {
  return (
    <div className="grid">
      {cards.map((card, index) => (
        <div key={index} className="card">
          <h3>{card.nome}</h3>
          <p>{card.profissao}</p>
          <button>Curtir</button>
        </div>
      ))}
    </div>
  );
}

export default CardGrid;
```

### 📁 Arquivo: `src/components/CardGrid/CardGrid.css`

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  padding: 20px;
}

.card {
  background: white;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 0 6px rgba(0,0,0,0.1);
  text-align: center;
}

.card button {
  margin-top: 10px;
  padding: 6px 12px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.card button:hover {
  background-color: #218838;
}
```

---

## ✅ Exercício 3 — Tema Dinâmico com useState

### Objetivo

Alternar entre tema claro e escuro com um botão, aplicando classes CSS dinamicamente com base no estado.

### 📁 Arquivo: `src/components/Tema/Tema.jsx`

```jsx
import React, { useState } from 'react';
import './Tema.css';

function Tema() {
  const [modoEscuro, setModoEscuro] = useState(false);

  return (
    <div className={modoEscuro ? 'tema escuro' : 'tema claro'}>
      <p>Tema atual: {modoEscuro ? 'Escuro' : 'Claro'}</p>
      <button onClick={() => setModoEscuro(!modoEscuro)}>
        Alternar Tema
      </button>
    </div>
  );
}

export default Tema;
```

### 📁 Arquivo: `src/components/Tema/Tema.css`

```css
.tema {
  padding: 20px;
  border-radius: 8px;
  text-align: center;
}

.tema.claro {
  background-color: #f9f9f9;
  color: #222;
}

.tema.escuro {
  background-color: #222;
  color: #f9f9f9;
}

.tema button {
  margin-top: 10px;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background-color: #007bff;
  color: white;
}

.tema button:hover {
  background-color: #0056b3;
}
```
