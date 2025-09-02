---
theme: seriph
background: https://cover.sli.dev
title: Pokenode-ts
info: |
  ## Pokenode-ts
  Uma apresentação sobre desenvolvimento de um wrapper TypeScript para a PokéAPI
  e os aprendizados técnicos durante o processo.

  Por: Gabriel da Cunha
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
seoMeta:
  ogImage: auto
---

# Pokenode-ts

Wrapper TypeScript para a PokéAPI

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/Gabb-c" target="_blank" class="slidev-icon-btn" title="GitHub Profile">
    <carbon:logo-github />
  </a>
  <a href="https://pokenode-ts.vercel.app/" target="_blank" class="slidev-icon-btn" title="Documentação">
    <carbon:document />
  </a>
</div>

<!--
Apresentação sobre o desenvolvimento do Pokenode-ts, focando na problemática, solução e desafios técnicos
-->

---
transition: fade-out
---

# Agenda

<div class="flex items-center justify-center h-full">

<div class="grid grid-cols-3 gap-16 text-center">

<div
  v-motion
  :initial="{ x: -300, opacity: 0 }"
  :enter="{ x: 0, opacity: 1, transition: { delay: 300, duration: 800 } }"
>
  <div class="text-6xl mb-4">🤔</div>
  <h3 class="text-xl font-bold">Problemática</h3>
</div>

<div
  v-motion
  :initial="{ y: -300, opacity: 0 }"
  :enter="{ y: 0, opacity: 1, transition: { delay: 600, duration: 800 } }"
>
  <div class="text-6xl mb-4">🎮</div>
  <h3 class="text-xl font-bold">Solução</h3>
</div>

<div
  v-motion
  :initial="{ x: 300, opacity: 0 }"
  :enter="{ x: 0, opacity: 1, transition: { delay: 900, duration: 800 } }"
>
  <div class="text-6xl mb-4">🚀</div>
  <h3 class="text-xl font-bold">Desafios</h3>
</div>

</div>

</div>

---
layout: center
class: text-center
---

<img src="https://media.giphy.com/media/6uGhT1O4sxpi8/giphy.gif" alt="John Travolta Confused" class="w-96 mx-auto" />

---

# O que é a PokéAPI?

<div class="text-center space-y-8">

<div class="text-8xl mb-6">🐾</div>

<div class="space-y-6">
  <h2 class="text-3xl font-bold">RESTful API sobre Pokémon</h2>
  <div class="text-xl opacity-80">Dados completos de mais de 1000 Pokémon</div>
</div>

<div class="grid grid-cols-2 gap-8 mt-12">
  <div class="text-center">
    <div class="text-4xl mb-2">📊</div>
    <div class="font-bold">Estatísticas</div>
    <div class="text-sm opacity-60">HP, Attack, Defense...</div>
  </div>
  
  <div class="text-center">
    <div class="text-4xl mb-2">🎯</div>
    <div class="font-bold">Habilidades</div>
    <div class="text-sm opacity-60">Moves, Types, Abilities...</div>
  </div>
</div>

<div class="mt-8 text-lg">
  <code class="bg-gray-800 px-4 py-2 rounded">https://pokeapi.co/api/v2/pokemon/pikachu</code>
</div>

</div>

---
transition: slide-up
level: 2
---

# Problemática

<div class="text-center mb-8">
  <div class="text-8xl mb-4">😰</div>
  <h2 class="text-2xl">Integrando com a PokéAPI</h2>
</div>

````md magic-move
```ts
// Tentando buscar um Pokemon sem tipagem
async function getPokemon(name: string) {
  const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${name}`);
  const data = await response.json(); // any 😱
  
  // Sem autocompletion, sem validação
  console.log(data.name);      // Pode quebrar?
  console.log(data.abilities); // Existe essa propriedade?
  
  return data; // tipo: any
}
```

```ts
// Tentando adicionar tipagem manual
interface Pokemon {
  name: string;
  // ... dezenas de outras propriedades? 🤯
  abilities?: Array<{ ability: { name: string } }>;
  types?: Array<{ type: { name: string } }>;
}

async function getPokemon(name: string): Promise<Pokemon> {
  // Ainda sem garantias de que a tipagem está correta
  return response.json() as Pokemon; // 🤞
}
```

```ts
// Outros problemas
❌ Requests repetitivas (sem cache)
❌ Tratamento de erro inconsistente  
❌ Documentação espalhada

✅ Solução: Uma biblioteca dedicada!
🎯 Objetivo: Tipagem + Cache + DX
```
````

---
layout: image-right
image: https://repository-images.githubusercontent.com/361033992/6ad7e080-ca27-11eb-933e-a5d251bd8096
---

# Pokenode-ts

<div class="space-y-8">

<div
  v-motion
  :initial="{ x: -100, opacity: 0 }"
  :enter="{ x: 0, opacity: 1, transition: { delay: 200, duration: 600 } }"
  class="text-xl font-bold"
>
  🎮 Wrapper TypeScript da PokéAPI
</div>

<div
  v-motion
  :initial="{ x: -100, opacity: 0 }"
  :enter="{ x: 0, opacity: 1, transition: { delay: 400, duration: 600 } }"
  class="space-y-3"
>
  <div class="flex items-center gap-3">
    <span class="text-2xl">✨</span>
    <span>Tipagem completa automática</span>
  </div>
  
  <div class="flex items-center gap-3">
    <span class="text-2xl">⚡</span>
    <span>Cache inteligente configurável</span>
  </div>
  
  <div class="flex items-center gap-3">
    <span class="text-2xl">🏗️</span>
    <span>13 clients especializados</span>
  </div>
  
  <div class="flex items-center gap-3">
    <span class="text-2xl">📦</span>
    <span>Zero dependências externas</span>
  </div>
</div>

<div
  v-motion
  :initial="{ y: 50, opacity: 0 }"
  :enter="{ y: 0, opacity: 1, transition: { delay: 800, duration: 600 } }"
  class="text-center"
>
  <div class="bg-gray-800 px-4 py-2 rounded-lg inline-block">
    <code class="text-green-400">npm install pokenode-ts</code>
  </div>
</div>

</div>

---

# Pokenode-ts

````md magic-move
```ts
// ❌ Antes: Sem tipagem, sem cache
const response = await fetch('https://pokeapi.co/api/v2/pokemon/pikachu');
const pokemon = await response.json(); // any 😱

console.log(pokemon.name); // Pode quebrar?
```

```ts
// ✅ Depois: Com Pokenode-ts
import { PokemonClient } from 'pokenode-ts';

const api = new PokemonClient({ cacheOptions: { ttl: 300000 } });
const pokemon = await api.getPokemonByName('pikachu');

console.log(pokemon.name);     // string ✨
console.log(pokemon.types);    // PokemonType[] ✨
console.log(pokemon.abilities); // PokemonAbility[] ✨
```

```tsx
// 🚀 Exemplo: App React com Pokenode-ts
import { PokemonClient } from 'pokenode-ts';
import { useState, useEffect } from 'react';

function PokemonCard({ name }: { name: string }) {
  const [pokemon, setPokemon] = useState<Pokemon | null>(null);
  
  useEffect(() => {
    const api = new PokemonClient();
    api.getPokemonByName(name).then(setPokemon);
  }, [name]);

  return (
    <div>
      <h3>{pokemon?.name}</h3>
      <p>Type: {pokemon?.types[0].type.name}</p>
    </div>
  ); // TypeScript garante segurança! ✨
}
```
````

---

# Desafios e Aprendizados

````md magic-move
```ts
// 🎯 Desafio 1: Aprender TypeScript para mapear responses
interface Pokemon {
  id: number;
  name: string;
  types: Array<{
    type: {
      name: string;
      url: string;
    };
  }>;
  abilities: Array<{
    ability: {
      name: string;
      url: string;
    };
    is_hidden: boolean;
  }>;
}
```

```
// 📁 Desafio 2: Organização do código
src/
├── clients/           # 13 clients especializados
│   ├── pokemon.client.ts
│   ├── base.ts
│   └── ...
├── models/            # +200 interfaces TypeScript
│   ├── Pokemon/
│   ├── Common/
│   └── ...
├── constants/         # Endpoints e configurações
└── config/           # Sistema de logging
```

```json
// 🔧 Desafio 3: Ferramentas de qualidade
{
  "scripts": {
    "lint": "biome ci src",
    "format": "biome format ./src", 
    "test": "vitest",
    "test:coverage": "vitest run --coverage"
  },
  "devDependencies": {
    "@biomejs/biome": "^2.2.0",
    "vitest": "^3.2.4",
    "@vitest/coverage-v8": "^3.2.4"
  }
}
```

```yml
// 🚀 Desafio 4: CI/CD com deploy NPM
name: Release
on:
  push:
    branches: [master]
jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pnpm install
      - run: pnpm test
      - run: pnpm build
      - run: semantic-release
    env:
      NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

```ts
// 📚 Desafio 5: Documentação com VitePress
export default defineConfig({
  title: 'Pokenode-ts',
  description: 'Type-Safe PokéAPI wrapper',
  themeConfig: {
    nav: [
      { text: 'Guide', link: '/guides/getting-started' },
      { text: 'Clients', link: '/clients/pokemon-client' }
    ]
  }
})
// Deploy automático na Vercel
```
````

---
layout: center
class: text-center
---

# Obrigado!

<div class="text-center space-y-8">

<div class="text-6xl">🙏</div>

<h2 class="text-3xl font-bold">Perguntas?</h2>

<div class="space-y-6">
  <div class="space-y-2">
    <p class="text-xl font-bold">Gabriel da Cunha</p>
    <p class="text-base opacity-70">IFRS • 2025</p>
  </div>
</div>

<PoweredBySlidev />

</div>
