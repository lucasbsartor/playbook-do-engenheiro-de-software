# ⚡ Performance Frontend: Um Guia Prático para Engenheiros

> **Eperiências web rápidas e responsivas**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

## 📚 Índice

- [⚡ 1. Princípios Fundamentais](#-1-princípios-fundamentais)
- [🚀 2. Otimizações de Alta Prioridade (Essenciais)](#-2-otimizações-de-alta-prioridade-essenciais)
- [⏫ 3. Otimizações de Média Prioridade (Recomendadas)](#-3-otimizações-de-média-prioridade-recomendadas)
- [🔧 4. Otimizações de Baixa Prioridade (Ajustes Finos)](#-4-otimizações-de-baixa-prioridade-ajustes-finos)
- [🛠️ 5. Ferramentas e Análises de Performance](#-5-ferramentas-e-análises-de-performance)
- [📚 6. Diretrizes Específicas de Framework](#-6-diretrizes-específicas-de-framework)
- [📖 7. Leituras e Recursos Adicionais](#-7-leituras-e-recursos-adicionais)

---

## ⚡ 1. Princípios Fundamentais

- **Métricas Centrais para o Usuário:** Foque no que importa para o usuário: Largest Contentful Paint (LCP), First Input Delay (FID), Cumulative Layout Shift (CLS).
- **Aprimoramento Progressivo:** Entregue uma experiência funcional rapidamente e adicione recursos avançados depois.
- **Otimize o Caminho Crítico de Renderização:** Priorize assets/códigos necessários para o primeiro carregamento.
- **Reduza Requisições de Rede:** Menos e menores requisições = carregamento mais rápido.
- **Evite Layout Thrashing:** Agrupe mudanças no DOM e recálculos de estilo para evitar "jank".

**🔑 Principais Lições:**

- Foque em métricas centradas no usuário (LCP, FID, CLS) para impacto real.
- Otimize o caminho crítico de renderização e reduza requisições de rede.
- Agrupe mudanças no DOM para evitar layout thrashing.

---

## 🚀 2. Otimizações de Alta Prioridade (Essenciais)

**Estas mudanças trazem os maiores ganhos, rapidamente.**

### 🧑‍💻 Otimização de CSS

- **Incorpore CSS Crítico Inline:** Coloque o CSS acima da dobra diretamente no `<head>` para renderização instantânea.
- **Minifique CSS:** Use ferramentas como CSSNano ou PostCSS.
- **Remova CSS Não Utilizado:** Ferramentas como PurgeCSS ajudam a manter o CSS enxuto.
- **CSS Não Bloqueante:** Use atributos `media` ou carregue CSS não crítico de forma assíncrona.

**Exemplo: CSS Crítico Inline**

```html
<head>
  <style>
    /* Estilos críticos aqui */
    body {
      margin: 0;
      font-family: system-ui, sans-serif;
      background: #fff;
      color: #222;
    }
    header {
      min-height: 60px;
      background: #f5f5f5;
      display: flex;
      align-items: center;
      padding: 0 1rem;
    }
  </style>
  <link rel="stylesheet" href="main.css" />
</head>
```

### 🧑‍💻 Otimização de Imagens

- **Comprimir Imagens:** Use Squoosh, TinyPNG ou ImageOptim.
- **Formatos Modernos:** Prefira WebP ou AVIF para melhor compressão.
- **Imagens Responsivas:** Use `<picture>` e `srcset` para imagens adequadas ao dispositivo.
- **Lazy Load em Imagens Fora da Tela:**

**Exemplo: Imagem Responsiva**

```html
<picture>
  <source srcset="image.avif" type="image/avif" />
  <source srcset="image.webp" type="image/webp" />
  <img src="image.jpg" alt="..." loading="lazy" width="600" height="400" />
</picture>
```

### 🧑‍💻 Otimização de JavaScript

- **Minifique JS:** Use Terser ou UglifyJS.
- **Scripts Deferidos/Assíncronos:**
  - `async` para scripts independentes.
  - `defer` para scripts que rodam após o parsing.
- **Bundle e Tree Shaking:** Use Webpack, Rollup ou Parcel para remover código morto.

**Exemplo: Script Não Bloqueante**

```html
<script src="main.js" defer></script>
```

### 🧑‍💻 Rede e Carregamento de Recursos

- **Sempre Use HTTPS:** Habilita HTTP/2 e recursos de segurança.
- **Habilite Compressão:** GZIP ou Brotli para todos os assets de texto.
- **Defina Cabeçalhos de Cache:** Use `Cache-Control`, `Expires` e `ETag` para assets estáticos.
- **Minimize Requisições HTTP:** Combine arquivos ou use multiplexação HTTP/2.
- **Evite 404s:** Garanta que todos os recursos existam e estejam acessíveis.

### 🧑‍💻 Metas de Core Web Vitals

- **Peso da Página < 1500 KB (idealmente < 500 KB)**
- **Carregamento da Página < 3 segundos**
- **TTFB < 1,3 segundos**
- **Minimize iframes e CSS inline (exceto caminho crítico)**

**⚡ Ganhos Rápidos:**

- Incluir e minificar CSS crítico para pintura inicial mais rápida.
- Comprimir e servir imagens responsivas em formatos modernos.
- Minificar e deferir JavaScript; use atributos async/defer.
- Sempre use HTTPS e habilite compressão para todos os assets.
- Defina cabeçalhos de cache e evite requisições HTTP desnecessárias.

---

## ⏫ 3. Otimizações de Média Prioridade (Recomendadas)

- **Minifique HTML:** Remova espaços/comentários antes de servir.
- **Use um CDN:** Sirva assets estáticos a partir de edge locations.
- **Prefira SVG para Ícones/Logos:** Menor, escalável e estilizável.
- **Defina `width`/`height` em Imagens:** Previne layout shifts (CLS).
- **Lazy Load em Imagens:** Use `loading="lazy"` ou Intersection Observer.
- **Sirva Imagens no Tamanho Adequado:** Combine o tamanho da imagem ao tamanho de exibição.
- **Mantenha Dependências Atualizadas:** Ganhe melhorias de performance e segurança.
- **Service Workers:** Para cache avançado e suporte offline.
- **Mantenha Cookies Pequenos e Poucos:** <4096 bytes e <20 cookies por domínio.

**Exemplo: Lazy Loading de Imagem**

```html
<img src="photo.jpg" loading="lazy" width="400" height="300" alt="..." />
```

**🔑 Principais Lições:**

- Use CDN para assets estáticos e prefira SVG para ícones/logos.
- Defina width/height em imagens para evitar layout shifts.
- Mantenha dependências atualizadas e use service workers para cache avançado.

---

## 🔧 4. Otimizações de Baixa Prioridade (Ajustes Finos)

- **Otimização de Fontes:**
  - Use formato WOFF2.
  - Preconnect para domínios de fontes.
  - Subset de fontes para apenas caracteres necessários.
  - Use `font-display: swap;` para evitar texto invisível.
- **Preload/Prefetch de Recursos:**
  - `rel="preload"` para assets críticos descobertos tardiamente.
  - `rel="prefetch"` para navegações futuras prováveis.
- **Remova JS/CSS Não Utilizado:** PurgeCSS, tree shaking.
- **Concatene CSS (se HTTP/1.1):** Para sites pequenos, combinar arquivos pode ajudar.

**Exemplo: Preload de Fonte**

```html
<link
  rel="preload"
  href="/fonts/myfont.woff2"
  as="font"
  type="font/woff2"
  crossorigin
/>
```

**⚡ Ganhos Rápidos:**

- Use fontes WOFF2 e faça preload de recursos críticos.
- Remova JS/CSS não utilizado e concatene arquivos se usar HTTP/1.1.
- Subset de fontes e use font-display: swap para evitar texto invisível.

---

## 🛠️ 5. Ferramentas e Análises de Performance

- **DevTools do Navegador:** Chrome DevTools, Firefox, Safari para rede, performance e auditorias.
- **Lighthouse:** Auditorias automáticas de performance, acessibilidade, SEO.
- **PageSpeed Insights:** Dados de campo e laboratório para performance real.
- **WebPageTest:** Gráficos detalhados e testes multi-localização.
- **Análise de Bundles:** Webpack Bundle Analyzer, Rollup Visualizer, Bundlephobia.
- **Ferramentas de Imagem:** Squoosh.app para compressão e conversão de formatos.
- **RUM e Monitoramento Sintético:** Datadog, New Relic, Google Analytics, Pingdom.

**🔑 Principais Lições:**

- Use DevTools e Lighthouse para auditorias e profiling.
- Analise bundles e imagens para encontrar oportunidades de otimização.
- Monitore métricas reais de usuários e testes sintéticos para melhoria contínua.

---

## 📚 6. Diretrizes Específicas de Framework

- **Angular:** Lazy loading, compilação AOT, detecção de mudanças OnPush, tree shaking, web workers.
  - [Angular Performance Checklist](https://github.com/mgechev/angular-performance-checklist)
- **React:** Memoização (`React.memo`, `useMemo`), lazy loading, code splitting, SSR/SSG, listas virtualizadas.
  - [Otimizando Performance no React](https://react.dev/learn/optimization)
- **Vue.js:** Lazy loading, keep-alive, memoização, SSR, otimize `v-for` com `key`.
  - [Padrões de Performance Vue](https://learn-vuejs.github.io/vue-patterns/useful-links/)

**⚡ Ganhos Rápidos:**

- Use lazy loading, code splitting e memoização no framework de sua escolha.
- Siga os checklists e docs oficiais de performance para Angular, React e Vue.

---

## 📖 7. Leituras e Recursos Adicionais

- Google Web Vitals
- MDN Web Docs sobre Performance

---

> **Dica:** Performance de frontend é uma jornada—meça, otimize e repita. Dados reais de usuários são seu melhor guia.

---

**Este guia é um documento vivo. Contribua com melhorias e exemplos à medida que encontrar novos desafios!**

[Voltar ao Índice de Boas Práticas](./index.md)  
[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._
