# Landing Page — Venak Tecidos

Página única (HTML + CSS + JS puro, sem dependências) pensada para **converter visita do Instagram em conversa no WhatsApp**.

```
LP-Venak-Tecidos/
├── index.html              ← a landing page inteira (é só abrir no navegador)
├── assets/
│   ├── logo.png            ← logo com fundo removido (760px, 22 KB)
│   ├── logo-branca.png     ← versão branca, usada no rodapé escuro
│   ├── logo-original.png   ← arquivo original em alta (2169px), guardado
│   └── favicon.png         ← ícone da aba: "V" branco sobre navy
└── README.md
```

## Estrutura da página (ordem de persuasão)

| # | Bloco | Função na conversão |
|---|-------|---------------------|
| 1 | Header fixo com CTA | O botão de WhatsApp nunca sai da tela |
| 2 | Hero escuro + contadores | Promessa clara em 5 segundos + números que geram confiança |
| 3 | Marquee de tecidos | Mostra variedade sem ocupar espaço e dá ritmo à rolagem |
| 4 | Benefícios (4 cards) | Quebra as objeções principais (frete, metragem, preço, insegurança) |
| 5 | Coleções (6 cards) | Cada card abre o WhatsApp **com a mensagem já escrita** daquela categoria |
| 6 | Como comprar (3 passos) | Tira o medo de comprar tecido sem tocar |
| 7 | Instagram | Reforça os +4 mil seguidores e leva ao perfil |
| 8 | Lojas (VTA/VTM/VTP) | Converte quem prefere ir presencialmente |
| 9 | FAQ | Últimas objeções antes do clique |
| 10 | CTA final + rodapé | Fechamento |
| + | WhatsApp flutuante (desktop) e barra fixa (mobile) | CTA sempre a um toque |

### Efeitos aplicados

Barra de progresso de leitura · header que vira vidro ao rolar (e troca a logo branca pela
navy) · auroras animadas e textura de grão no hero · título que sobe linha por linha na
abertura · amostras de tecido com parallax do mouse · contadores que sobem quando entram na
tela · marquee infinito que pausa no hover · halo dourado seguindo o cursor nos benefícios ·
tilt 3D + zoom da estampa + brilho nos cards de coleção · trilho dourado que preenche com o
scroll no "como comprar" · botões magnéticos com brilho atravessando · FAQ animado ·
reveal em cascata em tudo. **Tudo desligado automaticamente** para quem usa
`prefers-reduced-motion`.

Cada botão de WhatsApp abre a conversa com uma **mensagem diferente e pré-preenchida**, então
você já sabe de onde a pessoa veio. As UTMs da campanha (`?utm_source=instagram&utm_campaign=bio`)
são repassadas junto na mensagem.

## ⚠️ O que precisa ser trocado antes de publicar

1. **Endereços e horários das lojas** — hoje estão como `Endereço da loja — Alfenas/MG` e
   `Seg a sex: 9h–18h · Sáb: 9h–12h`. Confirme os dados reais das 3 unidades e ajuste também os
   links do Google Maps (procure pelo link curto de cada loja no Google Meu Negócio).
2. **Fotos reais** — todos os retângulos estampados são padrões em SVG gerados por código
   (placeholders bonitos, mas placeholders). Troque os elementos com `data-pattern` por `<img>`
   com fotos dos tecidos: 3 no hero, 6 nos cards de coleção, 6 na grade do Instagram.
3. **Logo** — ✅ resolvido. A PNG original (2169×725, RGB sem canal alfa) foi recortada do fundo
   branco e virou `logo.png` (transparente, 760px, 22 KB), `logo-branca.png` (rodapé escuro) e
   `favicon.png` (V branco sobre navy). O arquivo original ficou em `logo-original.png`.
   Se um dia aparecer a versão vetorial (SVG/AI), vale trocar — fica perfeita em qualquer tamanho.
4. **Domínio** — troque `https://www.venaktecidos.com.br/` no `<link rel="canonical">`,
   nas tags `og:` e no JSON-LD pelo domínio real.
5. **`assets/og-cover.jpg`** (1200×630) — a imagem que aparece quando o link é compartilhado no
   WhatsApp/Instagram. Sem ela o link fica sem miniatura. (O favicon já está pronto.)
6. **FAQ** — confira as respostas de pagamento, prazo e retirada com a operação real da loja.

## Configuração rápida

Tudo o que muda com frequência está no topo do `<script>`, no fim do `index.html`:

```js
const VENAK = {
  telefone: '5535999492502',
  mensagemPadrao: 'Ola! Vim pelo site da Venak Tecidos.'
};
```

## Rastreamento

A função `track()` já dispara eventos para **GA4 (`gtag`)**, **Meta Pixel (`fbq`)** e
**GTM (`dataLayer`)** — basta colar a tag de cada ferramenta no `<head>` que os eventos
(`cta_header`, `cat_tecidos`, `cta_como`, `cta_final`, etc.) começam a chegar sozinhos.
Recomendo marcar todos os `cta_*` e `cat_*` como conversão no GA4 e no Gerenciador de Anúncios.

## Como publicar

É um site estático: sobe em **Netlify, Vercel, Cloudflare Pages ou GitHub Pages** arrastando a
pasta — leva 2 minutos e é grátis. Depois é só apontar o domínio e trocar o link da bio do
Instagram (hoje aponta direto para o `wa.me`) para a landing page com UTM:

```
https://seudominio.com.br/?utm_source=instagram&utm_medium=bio&utm_campaign=perfil
```

## Checklist de performance/SEO já resolvido

- Arquivo único, sem framework e sem biblioteca externa (só as fontes do Google)
- Responsivo de 320px ao desktop, com barra de CTA dedicada no mobile
- `prefers-reduced-motion` respeitado
- JSON-LD `Store` com as 3 cidades e telefone, para aparecer melhor na busca local
- Títulos e meta description escritos para "tecidos Alfenas / Machado / Paraguaçu"
