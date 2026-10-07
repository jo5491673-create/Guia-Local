# Registro de decisões — layout + ligação



| Ajuste | Intrínseca ou deliberada? | Por quê | Onde falhava |
|---|---|---|---|
| Base do CSS = celular; `@media (min-width: 48em)` acrescenta o resto | Deliberada | Os antigos `max-width: 520px` corrigiam o desktop "de cima para baixo" e deixavam 521–767px quebrados. Agora a base já funciona no pequeno. | Sidebar de 220px + conteúdo espremia tudo abaixo de ~700px  |
| Sidebar: empilhada (lista em linha) na base → coluna lateral em ≥ 48em | Deliberada (o desenho muda: barra vira coluna) | Não é questão de quantidade de trilhas, é outra organização. | ~768px  (coluna útil < ~550px) |
| `.cards`: `repeat(auto-fit, minmax(min(100%, 260px), 1fr))` | Intrínseca | Nº de cards por linha depende só do espaço; sem media query. `min(100%, …)` impede estouro em telas < 260px. | Flex com `flex: 1 1 280px` estourava abaixo de ~312px ⚠ |
| Cabeçalho: coluna na base → linha em ≥ 48em (com `flex-wrap`) | Deliberada + wrap intrínseco | Título e menu empilham no celular; lado a lado só quando cabem. | Menu espremido ao lado do título abaixo de ~600px |
| Tabela: fonte/padding menores na base, `overflow-wrap: anywhere` | Intrínseca | Texto quebra dentro da célula em vez de empurrar a página. | ~360px (coluna "Detalhe" com a data longa)  |
| `.wrap { width: 100% }` | Intrínseca | Em `body` flex/grid, `margin: auto` fazia o wrap encolher ao conteúdo. | Qualquer largura |
| `grid-template-columns: … minmax(0, 1fr)` | Intrínseca | Sem o `0`, conteúdo largo alarga a coluna e gera rolagem horizontal. | Celular |
| Padding de `.wrap`, `section.card`, `.hero` reduzido na base | Deliberada | Em 320px, 24+36px de padding comem quase metade da largura. | ≤ 400px  |
| Card da home = `<a class="card-body">` envolvendo o conteúdo | — (ligação) | Card inteiro clicável; "Ver detalhes" virou `<span>` para não aninhar links. CCXP fica sem link (`div`, mesmo espaçamento). | — |
| Detalhe: menu → `index.html`, `index.html#cards`; barra interna com "← Voltar aos locais" + âncoras | — (ligação) | Âncora `#eventos` não existia na detalhe (link quebrado): trocada por `index.html#cards`. Rótulo "Comodidades" → "Atrações" para bater com o `<h2>`. | — |

## Ficou de fora
- **Tipografia** (tamanhos de fonte, famílias, `clamp()`): segunda parte da aula. Só mexi em `font-size` da tabela e dos títulos onde isso decidia se cabia na tela.
- **Mídia** (imagens reais, `srcset`, `<picture>`): idem. As imagens já têm `width: 100%`, então não estouram.
- **Conteúdo**: a nota "4,1 de 10" e a seção "Próximos eventos" (que não existe na detalhe) não foram tocadas.
