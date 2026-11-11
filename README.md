# anmhelp — branch `analise-interface`

> ⚠️ **MATERIAL DE ANÁLISE TÉCNICA. NÃO É UMA CAMPANHA DE ARRECADAÇÃO E NÃO REPRESENTA NENHUMA ORGANIZAÇÃO.**
> Não faça doações a partir de nada neste repositório. Todos os formulários, botões de doação,
> links e integrações de pagamento foram desativados ou removidos.

## O que é

Cópia estática de uma página de "doação de ração via Pix" (capturada com saveweb2zip), preparada
exclusivamente para **auditoria técnica de interface e de comportamento**. A identidade da página
de origem (nome, CNPJ, e-mail, domínio, endereço) foi removida e substituída por marcadores como
`[ORGANIZAÇÃO REMOVIDA]`.

Esta branch **não deve ser publicada** (GitHub Pages, Netlify, Vercel etc.). A página tem
`noindex, nofollow` e uma faixa fixa de aviso, mas a intenção é apenas leitura/inspeção local.

## Estrutura

```
interface/                      Página neutralizada, sem nenhum JavaScript
  index.html                    HTML estático: scripts, iframes, rastreadores e metadados removidos;
                                botões/links de doação desativados (texto original em data-texto-original)
  css/                          Folhas de estilo originais (sem referências externas)
  images/                       Fotos usadas pela página (favicon e og-image excluídos)
evidencias/
  index-original-redigido.html.txt   HTML original completo, com identidade e tokens redigidos
  js-original/*.js.txt               JavaScript original redigido, salvo como .txt (não executa)
RELATORIO-AUDITORIA.md          Achados técnicos e sinais de alerta
```

## Como inspecionar

Abra `interface/index.html` localmente no navegador. Nenhum código é executado, nenhuma requisição
de pagamento é feita. Para analisar a lógica original, leia os arquivos em `evidencias/`.

## O que foi removido / desativado

- Todo `<script>` (inclusive o runtime do app, o Google Ads/gtag e o desafio do Cloudflare)
- `<iframe>` (mapa e iframe oculto de 1×1 px), `<video>`, `<form>`
- Metadados Open Graph/Twitter, JSON-LD de "Organization", favicon e imagem de compartilhamento
- `href` de todos os links (incluindo `mailto:`); botões com `disabled`
- Identificador de conversão do Google Ads (`AW-…`), token do Cloudflare, nome, CNPJ, e-mail,
  domínio e endereço — redigidos em todos os arquivos, inclusive nas evidências

A branch `main` não foi alterada.
