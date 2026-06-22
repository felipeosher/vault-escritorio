---
tipo: identidade-visual
escritorio: Chalub & Pascarelli Advogados Associados
atualizado: 2026-06-21
uso: PADRÃO para TODA peça/documento jurídico do escritório
---

# 🎨 Identidade Visual — Chalub & Pascarelli Advogados Associados

> ⚠️ **REGRA PERMANENTE:** todo documento jurídico do escritório (memoriais, petições, pareceres, contratos, relatórios) deve ser produzido **sobre este timbre**. É o padrão oficial.

## Escritório
- **Nome:** CHALUB & PASCARELLI — Advogados Associados
- **Sócios:**
  - **Thaís Cohen Chalub** — OAB/AM 14.501 — (92) 98137-9322
  - **Felipe Benchaya Marinho Pascarelli Lopes** — OAB/AM 19.500 — (92) 98450-5454
- **Local:** Manaus/AM (DDD 92)

## Paleta de cores
| Cor | Hex | Uso |
|---|---|---|
| Azul-marinho (principal) | `#16203C` | Logo, títulos, barras laterais, nomes |
| Azul-marinho alt | `#1A2338` | Variação de destaque |
| Cinza médio | `#6B7280` | Texto secundário, OAB, telefones |
| Dourado (acento) | `#E8B53A` | Detalhes, ícones — usar com moderação |
| Branco | `#FFFFFF` | Fundo |

## Tipografia
- **Títulos / nome do escritório:** sans-serif geométrica (Montserrat / Poppins), negrito, tracking aberto.
- **Corpo de peça jurídica:** serifada clássica (Times New Roman / equivalente) para o texto corrido — padrão forense.
- **Destaques visual law:** sans-serif (Montserrat) para boxes, tabelas e callouts.

## Layout do timbre (A4 — 2565×3626 px)
- Logo (monograma C+P+A em círculo) + "CHALUB & PASCARELLI / Advogados Associados" no **canto superior esquerdo**.
- **Barras verticais azul-marinho** nas duas bordas (moldura lateral).
- **Rodapé:** dois blocos com nome + OAB + WhatsApp (Thaís à esquerda, Felipe à direita).

### Zona segura de texto (não invadir timbre)
- **Topo:** começar abaixo de **9%** da altura
- **Base:** terminar acima de **91%** da altura (não bater no rodapé)
- **Esquerda:** ≥ **6%** da largura (depois da barra)
- **Direita:** ≤ **94%** da largura (antes da barra)

## Assets (nesta pasta `/assets`)
- `timbre-a4.jpeg` — timbre A4 completo (usar como **fundo de página** no HTML/CSS)
- `Timbre Chalub & Pascarelli (original).docx` — arquivo original do Word

## Como produzir documentos (fluxo Bench)
1. HTML/CSS com `@page` A4 + `background-image` = `timbre-a4.jpeg`.
2. Texto dentro da zona segura (margens acima).
3. Corpo serifado; visual law (boxes/tabelas/timeline) em Montserrat + paleta.
4. Exportar PDF via Chromium headless (`--print-to-pdf`, `--no-pdf-header-footer`).
5. Salvar o PDF + o HTML-fonte na pasta do caso.

## Conexões
- [[_Caso Paulo - HUB]] — primeiro caso usando o timbre (Memorial visual law)
