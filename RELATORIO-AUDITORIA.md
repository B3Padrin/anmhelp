# Relatório de auditoria técnica — página de "doação de ração via Pix"

Material de análise. Não é campanha e não representa nenhuma organização. Dados de identificação da
página de origem foram redigidos neste repositório; o arquivo .zip original permanece com quem o enviou.

## 1. Arquitetura

- App React com renderização no servidor (runtime "vinext", empacotado com Vite/rolldown), exportado
  como HTML estático + chunks em `_next/static/chunks/`.
- A cópia capturada está **incompleta**: 12 chunks carregados sob demanda não vieram no .zip, entre eles
  `PixModal`, `SalesDashboard`, `analytics-client`, `visible-tracking` e `google-browser`. Ou seja, o fluxo
  de pagamento em si (geração do Pix) não está presente — apenas as chamadas que o disparam.

## 2. Rotas de servidor referenciadas no código

| Rota | Observação |
|---|---|
| `/api/checkout` | Criação da cobrança |
| `/api/payments/status` | Polling do status do pagamento (`id`, `token`, `includePix`) |
| `/api/postback` | Retorno de gateway |
| `/api/webhooks/blackcat` | Webhook de gateway de pagamento |
| `/api/webhooks/activepayments` | Webhook de gateway de pagamento |
| `/api/webhooks/hodle` | Webhook de gateway de pagamento |
| `/api/attribution`, `/api/monitor/source` | Atribuição de tráfego/origem |
| `/api/admin/:action`, `/vendas` | Painel administrativo e "dashboard de vendas" |
| `/obrigado`, `/obrigado-caramelo` | Páginas pós-pagamento |

Três gateways diferentes integrados a uma "ONG", e uma rota chamada `/vendas` com `SalesDashboard`,
são incomuns para uma organização de doação.

## 3. Rastreamento e terceiros

- Google Ads com rótulo de conversão (`AW-…`, redigido) disparado em `PreferencesLoader`.
- Desafio/beacon do Cloudflare injetado por iframe oculto de 1×1 px (token redigido).
- Chaves em `localStorage`/`sessionStorage` com prefixo `sos_` para consentimento e estado do checkout.

## 4. Sinais de alerta no conteúdo

- **Endereço declarado é um posto de combustível** (Posto Ipiranga em Lauro de Freitas/BA), exibido em mapa.
- Domínio de topo `.shop` para uma "organização sem fins lucrativos".
- CNPJ exibido tem dígitos verificadores válidos, mas isso não comprova existência — conferir na Receita Federal.
- Linguagem de urgência repetida ("cada minuto conta", "Urgente", "as tigelas podem amanhecer vazias").
- Imagem com "Dívidas: R$ 73.635,19" sobre um documento ilegível, sem fonte.
- Métricas sem lastro: "500+ resgatados", "98% de aprovação dos doadores", "100% transparência".
- Valores "quebrados" por pacote (R$ 33,79 / 64,90 / 91,45 / 177,32 / 416,75 / 742,90), típicos de
  checkout de vendas, com aviso em letra miúda de que não há entrega de ração.
- Imagens de "sacos de ração premium" genéricas (mockups), e fotos de animais/pessoas sem crédito ou origem.
- Página "Transparência" anunciada, mas sem prestação de contas na página principal.

## 5. Conclusão

A página tem estrutura de funil de vendas com checkout Pix e múltiplos gateways, apresentada como ONG,
e vários sinais típicos de golpes de doação. Não foi possível verificar a existência da organização a
partir do material. Recomenda-se: consultar o CNPJ na Receita Federal; não realizar doações; e, se
confirmada a fraude, denunciar ao provedor do domínio, ao Google (anúncios) e às autoridades
(delegacia de crimes cibernéticos / SaferNet Brasil).

## 6. Neutralização aplicada nesta branch

Ver `README.md`, seção "O que foi removido / desativado".
