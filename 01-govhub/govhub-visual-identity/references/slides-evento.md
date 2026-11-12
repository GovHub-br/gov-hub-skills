# Slides Gov Hub, variante EVENTO (padrão Abrelatam)

Variante de apresentação com **narrativa visual**: título com peso misto,
abertura de seção com pílula roxa e numeral gigante, formas e cartões
também nos slides de conteúdo, balões, diagramas de hub e fluxo, fotos e
QR code. Nasceu no deck da **Abrelatam/ConDatos 2026** ("Interoperabilidade
na prática") e foi reaplicada com sucesso na palestra do Gov Hub (antiga
Agile Trends) e na Oficina MIR, em 2026-11.

O CSS completo está em [`slides-evento.css`](slides-evento.css): **copie
o arquivo inteiro** para dentro do `<style>` do deck e use os blocos HTML
abaixo trocando só texto, imagem e posição.

## Qual variante usar

| Pedido | Variante |
|---|---|
| Palestra, evento, congresso, oficina, apresentação para público externo, "igual à da Abrelatam", "com mais cara de palestra" | **evento** (este arquivo) |
| Apresentação institucional, prestação de contas, aula com muito texto ou tabela, "no padrão do relatório", "sóbria" | **sóbria** ([`slides-sober.md`](slides-sober.md)) |
| Na dúvida | pergunte, mostrando as duas em uma frase cada |

As duas compartilham: canvas 1920×1080, fundo claro, Reddit Sans, navy +
roxo + `#F2F1F6`, rodapé só com número + símbolo, parceiros na capa e no
encerramento na ordem de [`partners.md`](partners.md). Não misture
componentes das duas no mesmo deck.

## Arquitetura e exportação

- Uma `section.gh-slide` de 1920×1080 por slide; `@page { size: 1920px
  1080px; margin: 0 }` (já no CSS). Variante de fundo: `gh-slide--soft`
  (`#F2F1F6`), usada **só** na abertura de seção.
- Logos: copie `references/logo/` para a pasta do deck (ou aponte para
  uma pasta `logo/` compartilhada, ex.: `../logo/`). Ícones de produto
  `-sober` do CDN ([`icons-catalog.md`](icons-catalog.md)), salvos
  localmente em `logo/icons/` se o deck precisar funcionar offline.
- Imagens do deck (fotos, prints, QR) em `img/` ao lado do HTML.
- **Exportação com Chrome headless** (não WeasyPrint: este CSS usa
  flex, `calc()`, `object-fit` e SVG inline que o WeasyPrint quebra):

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --disable-gpu --no-pdf-header-footer --virtual-time-budget=8000 --print-to-pdf="$PWD/deck.pdf" "file://$PWD/deck.html"
```

  O PDF sai com páginas de 1440×810 pt: é o mesmo 1920×1080 px, está certo.
- **Conferência visual obrigatória de todas as páginas.** Um jeito rápido
  de olhar o deck inteiro numa imagem só:

```bash
pdftoppm -r 24 -png deck.pdf /tmp/p && ffmpeg -loglevel error -y -pattern_type glob -i '/tmp/p-*.png' -vf "scale=640:360,pad=644:364:2:2:gray,tile=3x7" -frames:v 1 /tmp/sheet.png
```

  Depois amplie (`-r 48`) só os slides suspeitos.

## Ordem canônica

`capa` → `agenda` (opcional, decks com 3+ seções) → (`seção` →
`conteúdo` × N → `frase de impacto` opcional) × seções → `para levar`
(opcional) → `encerramento`.

Número de página é texto fixo no rodapé, capa = 1; a abertura de seção
conta mas não mostra rodapé. Renumere tudo ao inserir ou tirar slide.

## Regras que não mudam

- **Título** (`.gh-h`): navy, peso **400 com destaque em 800** (`<b>`),
  `letter-spacing: -0.025em`, caixa alta e baixa. O destaque é a parte
  que carrega a mensagem, nunca a frase toda. Título de conteúdo 64–76px
  (`.gh-head` usa 68px); frase de impacto 104–136px; capa 100–112px.
- **Eyebrow** (`.gh-eyebrow`) acima de todo título: 22px, caixa alta,
  `letter-spacing: 4px`, `--purple-700`. É o nome da seção ou o assunto.
- **Corpo** (`.gh-lead`) 32px `--text-body`, destaques em `<b>` navy.
- **Margens** de 120px nas laterais; cabeçalho a partir de `top: 96px`;
  conteúdo entre `y 300` e `y 960`.
- **Rodapé** igual ao sóbrio: número 30px navy bold à esquerda,
  `icone-none-navy.svg` 52px à direita. Em slide com imagem ocupando a
  direita, o rodapé fica só com o número (`style="right:auto; width:…"`).
- **Formas**: pílulas (cápsula inteira ou sangrando por uma borda),
  meia-lua `#F2F1F6` saindo do topo, círculo roxo grande sangrando pela
  borda. No máximo **uma forma decorativa por slide de conteúdo**, sempre
  sangrando pela borda e longe do texto.
- **Cor por elemento**: cartão neutro `#F2F1F6` com texto navy; cartão de
  destaque roxo `#613EFF` ou navy `#0A005A` com texto branco. Numa fileira
  de 3 cartões, a sequência claro → roxo → navy funciona bem.
- **Acento `#BE006E`** é permitido nesta variante, como em
  [`palette.md`](palette.md): só em detalhe (balão de resposta, círculo
  numerado, numerais da segunda coluna da agenda, alguns pontos da grade).
  Nunca em título, nunca em área grande, no máximo um uso por slide.
- **Lilás `#C9BDFF`** só como cor de apoio em grade de pontos e numeral
  sobre navy.
- **Imagens** (prints, fotos) com cantos de 28–36px; prints ganham
  contorno `--border-soft` (`.gh-shot`), fotos não (`.gh-photo`).
- **Texto do deck** segue Linguagem Simples e a convenção sem travessão
  de [`editorial-report.md`](editorial-report.md).

## Blocos HTML (copie e troque só o texto)

### Capa

```html
<section class="gh-slide">
  <div class="gh-pill-right" style="top:410px; width:560px; height:220px;"></div>
  <svg class="gh-shape" viewBox="0 0 266 100" aria-hidden="true" style="left:-150px; top:230px; width:430px; height:162px;">
    <rect width="266" height="100" rx="50" fill="#F2F1F6"/>
  </svg>
  <img class="gh-cover__logo" src="logo/logomarca-horizontal-navy.svg" alt="Gov Hub">
  <div class="gh-cover__content">
    <h1 class="gh-h gh-cover__title">Interoperabilidade<br><b>na prática</b></h1>
    <p class="gh-cover__subtitle">Conectando sistemas de compras públicas fragmentados</p>
    <!-- opcional: <p class="gh-cover__meta"><b>Nome do evento</b> · Cidade, data</p> -->
  </div>
  <div class="gh-cover__footer">
    <img src="logo/parceiros/lab-livre-black.svg" alt="Lab Livre">
    <img src="logo/parceiros/unb-dark-outlined.svg" alt="UnB">
    <!-- Ipea / ministério do projeto, na ordem de partners.md -->
    <!-- ministério: <img class="gh-logo-mgi" src="logo/parceiros/mgi_positivo-defeso.svg" alt="MGI"> -->
    <!-- logo do evento (PNG): <img class="gh-logo-abre" src="logo/evento/....png" alt="..."> -->
  </div>
</section>
```

Classes de altura para logos fora do padrão de 64px: `.gh-logo-mgi`
(104px, ministérios com bandeira), `.gh-logo-ipea` (54px),
`.gh-logo-abre` (100px, PNG de evento com o texto embaixo). Para outro
logo de evento, crie uma classe igual ajustando a altura no olho.
Pergunte antes de colocar nome de pessoa ou logo de evento na capa.

### Agenda

```html
<section class="gh-slide">
  <div class="gh-head">
    <p class="gh-eyebrow">Agenda</p>
    <h2 class="gh-h">O que vamos <b>ver hoje</b></h2>
  </div>
  <div class="gh-agenda">
    <div class="gh-num__i"><div class="gh-num__n">01</div><p class="gh-num__t">O problema</p></div>
    <div class="gh-num__i gh-num__i--b"><div class="gh-num__n">03</div><p class="gh-num__t">Como aplicar</p></div>
    <div class="gh-num__i"><div class="gh-num__n">02</div><p class="gh-num__t">A solução</p></div>
    <div class="gh-num__i gh-num__i--b"><div class="gh-num__n">04</div><p class="gh-num__t">Como está hoje</p></div>
  </div>
  <div class="gh-footer"><span class="gh-footer__page">2</span><img class="gh-footer__logo" alt="" src="logo/icone-none-navy.svg"></div>
</section>
```

A grade tem 2 colunas e lê em coluna: 01, 02 à esquerda; 03, 04 à
direita (`--b` deixa o numeral em `#BE006E`).

### Abertura de seção

```html
<section class="gh-slide gh-slide--soft">
  <div class="gh-sec__pill"></div>
  <div class="gh-sec__num">01</div>
  <svg class="gh-shape" viewBox="0 0 266 100" aria-hidden="true" style="left:-150px; bottom:120px; width:400px; height:150px;">
    <rect width="266" height="100" rx="50" fill="#0A005A"/>
  </svg>
  <div class="gh-sec__text">
    <p class="gh-eyebrow">O problema</p>
    <h1 class="gh-h">Uma política,<br><b>vários sistemas.</b></h1>
  </div>
</section>
```

Sem rodapé. Título em até 2 linhas curtas (cabe ~20 caracteres por linha
a 104px).

### Conteúdo: cabeçalho padrão

Todo slide de conteúdo começa com o cabeçalho e termina com o rodapé:

```html
<section class="gh-slide">
  <div class="gh-head">
    <p class="gh-eyebrow">A tentativa</p>
    <h2 class="gh-h">Em 2021, a lei criou um <b>portal nacional</b></h2>
  </div>
  <!-- corpo: um dos blocos abaixo, a partir de top ≈ 330px -->
  <div class="gh-footer"><span class="gh-footer__page">4</span><img class="gh-footer__logo" alt="" src="logo/icone-none-navy.svg"></div>
</section>
```

Se o corpo for uma figura grande, use `gh-head gh-head--compact` (título
56px, sobe para `top: 64px`) e `.gh-fig`.

### Corpo: texto + par de cartões (contraste)

```html
<div class="abs" style="left:120px; top:330px; width:760px;">
  <p class="gh-lead">A lei criou o <b>Portal Nacional de Contratações Públicas</b> para reunir os dados em um lugar só.</p>
</div>
<div class="gh-stack" style="left:1000px; right:120px; top:300px;">
  <div class="gh-duo__card" style="background:#613EFF; color:#fff;">
    <p class="gh-duo__k" style="color:#fff; opacity:.85;">Nasceu para</p>
    <p class="gh-duo__t"><b>publicizar</b> as compras</p>
  </div>
  <div class="gh-duo__card" style="background:#F2F1F6; color:#0A005A;">
    <p class="gh-duo__k" style="color:#3F28A6;">Não para</p>
    <p class="gh-duo__t"><b>monitorá-las</b></p>
  </div>
</div>
```

### Corpo: números em cartões (2 ou 3)

```html
<div class="gh-grid3" style="top:430px;">
  <div><p class="gh-stat__n">87%</p><p class="gh-stat__t">dos itens <b>não têm código NCM</b>.</p></div>
  <div><p class="gh-stat__n">98%</p><p class="gh-stat__t">das linhas são <b>duplicadas</b>.</p></div>
  <div><p class="gh-stat__n">1 → 2</p><p class="gh-stat__t">o <b>mesmo órgão</b> com dois códigos.</p></div>
</div>
<p class="gh-note" style="left:120px; top:880px; width:1400px;">Fonte: …</p>
```

Com 2 cartões, encurte a grade (`style="top:400px; right:600px;"`) e use
a direita para um `.gh-bigcircle` com frase (ver "círculo com frase").
Sempre cite a fonte do número em `.gh-note`.

### Corpo: número-chave gigante + grade de pontos

```html
<div class="abs" style="left:120px; top:150px; width:900px;">
  <p class="gh-eyebrow">Um país continental: 27 UFs e mais de 5.500 municípios</p>
  <p class="gh-kpi">+200</p>
  <h2 class="gh-h" style="font-size:56px; margin-top:40px;">sistemas, cada um com <b>critérios próprios.</b></h2>
</div>
<div class="gh-dots"><!-- SVG gerado pelo script abaixo --><p class="gh-dots__cap">Cada forma, um sistema diferente.</p></div>
```

A grade de pontos é um SVG 760×380 com 20×10 formas da marca (círculo,
anel, meia-lua, quarto, pílula) sorteadas nas cores navy, roxo,
`#3F28A6`, `#C9BDFF` e um pouco de `#BE006E`. Gere com:

```python
import random; random.seed(7)
C=['#613EFF']*6+['#0A005A']*5+['#3F28A6']*3+['#C9BDFF']*2+['#BE006E']
out=[]
for r in range(10):
  for c in range(20):
    x,y=19+38*c,19+38*r; f=random.choice(C); k=random.randrange(5)
    out.append([f'<circle cx="{x}" cy="{y}" r="13" fill="{f}"/>',
      f'<circle cx="{x}" cy="{y}" r="10" fill="none" stroke="{f}" stroke-width="6"/>',
      f'<path d="M{x-13} {y-6}h26a13 13 0 0 1-26 0z" fill="{f}"/>',
      f'<path d="M{x-12} {y-12}h24a24 24 0 0 1-24 24z" fill="{f}"/>',
      f'<rect x="{x-15}" y="{y-7}" width="30" height="14" rx="7" fill="{f}"/>'][k])
print('<svg width="760" height="380" viewBox="0 0 760 380" aria-hidden="true">'+''.join(out)+'</svg>')
```

### Corpo: três cartões numerados (problemas, tensões)

```html
<div class="gh-bn">
  <div style="background:#F2F1F6; color:#0A005A;">
    <p class="gh-bn__n" style="color:#613EFF;">01</p>
    <p class="gh-bn__t">Sem interoperabilidade</p>
    <p class="gh-bn__d">Os sistemas não conversam entre si.</p>
  </div>
  <div style="background:#613EFF; color:#fff;">
    <p class="gh-bn__n">02</p><p class="gh-bn__t">…</p><p class="gh-bn__d">…</p>
  </div>
  <div style="background:#0A005A; color:#fff;">
    <p class="gh-bn__n" style="color:#C9BDFF;">03</p><p class="gh-bn__t">…</p><p class="gh-bn__d">…</p>
  </div>
</div>
```

### Corpo: cartões com ícone e detalhe (benefícios)

```html
<div class="gh-tcards">
  <div class="gh-split">
    <div class="gh-split__top">
      <div class="gh-tcard__icon"><img src="logo/icons/database-sober.svg" alt=""></div>
      <p class="gh-bcard__t">Fonte única dos dados</p>
      <p class="gh-x__from">Cada órgão <b>mantém seu sistema</b></p>
    </div>
    <div class="gh-split__bottom"><p class="gh-tcard__q">A padronização acontece na camada.</p></div>
  </div>
  <!-- repita .gh-split até 3 -->
</div>
```

### Corpo: lista curta numerada (pilares, impactos)

```html
<div class="gh-pillars" style="top:380px;">
  <div class="gh-pillar"><span class="gh-pillar__n">1</span><span class="gh-pillar__t">Software livre</span></div>
  <!-- até 6 itens em 3 colunas -->
</div>
```

Para 7–8 itens use `gh-pillar gh-pillar--4` (4 colunas, número em cima)
e destaque o último em roxo (`style="background:#613EFF;"`, número branco
com texto roxo, título branco). Itens de 2–4 palavras; texto maior vai
para `.gh-bn` ou `.gh-tcards`.

### Corpo: hub (fontes → Gov Hub → usos)

```html
<svg class="gh-shape" style="left:0; top:0; width:1920px; height:1080px;" viewBox="0 0 1920 1080" aria-hidden="true">
  <g fill="none" stroke="#613EFF" stroke-width="5" stroke-linecap="round">
    <path d="M580 416 C 680 416, 660 550, 760 550"/>
    <path d="M580 550 L 750 550"/>
    <path d="M580 684 C 680 684, 660 550, 760 550"/>
    <path d="M1160 550 C 1260 550, 1240 416, 1340 416"/>
    <path d="M1170 550 L 1340 550"/>
    <path d="M1160 550 C 1260 550, 1240 684, 1340 684"/>
  </g>
</svg>
<span class="gh-hub__k" style="left:120px;">Fontes</span>
<span class="gh-hub__k" style="left:1340px;">Uso</span>
<div class="gh-node gh-node--in"  style="top:360px;">Sistemas federais</div>
<div class="gh-node gh-node--in"  style="top:494px;">Execução orçamentária</div>
<div class="gh-node gh-node--in"  style="top:628px;">Sistemas estaduais</div>
<div class="gh-hub">
  <img src="logo/logomarca-horizontal-white.svg" alt="Gov Hub">
  <p class="gh-hub__layers">Bronze · Prata · Ouro</p>
</div>
<div class="gh-node gh-node--out" style="top:360px;">Painéis</div>
<div class="gh-node gh-node--out" style="top:494px;">Dados abertos</div>
<div class="gh-node gh-node--out" style="top:628px;">Ciência de dados e IA</div>
<div class="gh-rail">Código aberto e documentado.</div>
```

Nós a 134px de distância (`top` 360/494/628). Com 2 saídas, use `top`
427 e 561 e troque as curvas da direita por
`M1160 550 C 1260 550, 1240 483, 1340 483` e `… 617, 1340 617`.

### Corpo: fluxo em 3 passos com retorno

```html
<div class="gh-flow" style="top:440px;">
  <div class="gh-flow__step" style="background:#F2F1F6; color:#0A005A;"><span class="gh-flow__k">Primeiro</span>As perguntas</div>
  <div class="gh-flow__arrow">→</div>
  <div class="gh-flow__step" style="background:#613EFF; color:#fff;"><span class="gh-flow__k">Depois</span>Uma camada que traduz</div>
  <div class="gh-flow__arrow">→</div>
  <div class="gh-flow__step" style="background:#0A005A; color:#fff;"><span class="gh-flow__k">Resultado</span>Dado utilizável</div>
</div>
<svg class="gh-shape" style="left:0; top:0; width:1920px; height:1080px;" viewBox="0 0 1920 1080" aria-hidden="true">
  <path d="M1552 612 V 676" fill="none" stroke="#3F28A6" stroke-width="5" stroke-dasharray="12 10" stroke-linecap="round"/>
  <path d="M1538 668 L1552 694 L1566 668 Z" fill="#3F28A6"/>
</svg>
<div class="gh-back">
  <span class="gh-back__k">Retorno</span>
  <div class="gh-flow__step gh-flow__step--back">Melhoria na fonte</div>
  <div class="gh-flow__step gh-flow__step--back">Melhores decisões</div>
</div>
```

### Corpo: pipeline em 3 colunas (extração → camadas → uso)

```html
<div class="gh-pipe">
  <div class="gh-pipe__col" style="flex:0 0 360px; background:#F2F1F6; color:#0A005A;">
    <p class="gh-pipe__k" style="color:#3F28A6;">1 · Extração</p>
    <div class="gh-src"><i></i>Sistemas governamentais</div>
    <p class="gh-pipe__tool">com <b>Apache Airflow</b></p>
  </div>
  <div class="gh-pipe__col" style="flex:1; background:#613EFF; color:#fff;">
    <p class="gh-pipe__k">2 · Datawarehouse</p>
    <div class="gh-layers">
      <div class="gh-layer" style="background:rgba(255,255,255,.18);">Raw</div>
      <div class="gh-layer" style="background:#9C5A2E;">Bronze</div>
      <div class="gh-layer" style="background:#8C93A8;">Silver</div>
      <div class="gh-layer" style="background:#C79A1C;">Gold</div>
    </div>
    <div class="gh-steps"><span>Tratamento</span><span>Integração</span><span>Qualificação</span></div>
    <p class="gh-pipe__tool" style="padding-top:30px;">com <b>dbt</b></p>
  </div>
  <div class="gh-pipe__col" style="flex:0 0 520px; background:#0A005A; color:#fff;">
    <p class="gh-pipe__k" style="color:#C9BDFF;">3 · Uso</p>
    <div class="gh-use">Business Intelligence <small>Superset</small></div>
  </div>
</div>
```

Se já existir um diagrama de arquitetura pronto (ex.: o `fig4-arquitetura`
da skill de diagramas/fluxos), prefira-o com `.gh-head--compact` +
`.gh-fig`:

```html
<div class="gh-fig"><img src="diagramas/fig4-arquitetura.png" alt="Arquitetura do Gov Hub"></div>
```

### Corpo: caso real com linha do tempo vertical

```html
<div class="abs" style="left:0; top:640px; width:760px; height:220px; border-radius:0 999px 999px 0; background:#613EFF;"></div>
<div class="gh-card" style="left:1060px; right:120px; top:110px; bottom:130px;">
  <p class="gh-card__k">Em construção agora</p>
  <p class="gh-card__t">Observatório de Contratações Públicas</p>
  <span class="gh-tag">Infraestrutura de dados</span>
  <div class="gh-vtl">
    <div class="gh-vtl__i">Planejamento anual</div>
    <div class="gh-vtl__i" style="margin-bottom:0">Pagamento</div>
  </div>
</div>
```

### Corpo: prints e fotos

```html
<!-- texto à esquerda (left:120, width ~520–560), imagens à direita -->
<div class="gh-shot"  style="left:760px; top:96px;  width:1040px; height:420px;"><img src="img/print-1.jpg" alt="…"></div>
<div class="gh-shot"  style="left:760px; top:546px; width:500px;  height:400px;"><img src="img/print-2.jpg" alt="…"></div>
<div class="gh-photo" style="left:1290px; top:546px; width:510px; height:400px;"><img src="img/foto.jpg" alt="…"></div>
<div class="gh-footer" style="right:auto; width:560px;"><span class="gh-footer__page">5</span></div>
```

Espaço de 30px entre imagens. `.gh-shot` recorta pelo canto superior
esquerdo (prints de planilha e painel leem dali); `.gh-photo` centraliza.

Para reaproveitar imagens de um PDF antigo: rasterize a página a 144 dpi
(`pdftoppm -r 144 -png -f N -l N in.pdf p`) e recorte com
`ffmpeg -i p-N.png -vf "crop=W:H:X:Y" out.jpg`, usando as coordenadas da
página a 1920×1080 multiplicadas por 2.

### Corpo: conversa (pergunta e resposta)

```html
<div class="gh-bubbles" style="left:900px; top:290px; width:900px;">
  <div class="gh-bubble gh-bubble--in">Quais foram os principais motivos de afastamento?</div><br>
  <div class="gh-bubble gh-bubble--out" style="margin-left:80px;">Licença para tratamento de saúde, com <b>80 afastamentos</b>.</div>
</div>
```

`--out` é `#BE006E` por padrão; troque para roxo
(`style="background:#613EFF;"`) quando o slide já tiver outro rosa ou
quando a resposta for de um sistema (IA, assistente).

### Corpo: círculo com frase

```html
<div class="gh-bigcircle" style="right:-160px; top:300px; width:640px; height:640px;"></div>
<div class="gh-incircle" style="right:60px; top:500px; width:380px;">
  <p>Cada pergunta,<br><b>um trabalho manual.</b></p>
</div>
```

O texto precisa ficar **dentro da parte visível** do círculo: com o
círculo em `right:-160px` e 640px, a parte visível vai de x 1440 a 1920,
então o texto fica com `right:60px` e no máximo 380px de largura.

### Frase de impacto / "Para levar"

```html
<section class="gh-slide">
  <svg class="gh-shape" viewBox="0 0 100 50" aria-hidden="true" style="right:160px; top:-1px; width:380px; height:190px;">
    <path fill="#F2F1F6" d="M0 0h100a50 50 0 0 1-100 0z"/>
  </svg>
  <div class="abs" style="left:120px; top:300px; width:1500px;">
    <p class="gh-eyebrow">O problema</p>
    <h2 class="gh-h" style="font-size:128px;">Transparência não é<br>só <b>publicar</b>.</h2>
    <p class="gh-h" style="font-size:52px; margin-top:48px;">Dado publicado <b>não é, necessariamente,</b> dado utilizável.</p>
  </div>
  <div class="gh-pill-bleed" style="top:830px; width:780px;">
    <span class="gh-pill-bleed__ico"><svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="#FFFFFF" stroke-width="2.6" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="M13 6l6 6-6 6"/></svg></span>
    O Gov Hub é software livre
  </div>
  <div class="gh-footer"><span class="gh-footer__page">6</span><img class="gh-footer__logo" alt="" src="logo/icone-none-navy.svg"></div>
</section>
```

No máximo uma por seção. A pílula que sangra pela direita
(`.gh-pill-bleed`) também serve em slide de conteúdo como conclusão; o
ícone pode ser seta para a direita (conclusão) ou diagonal
`<path d="M7 7l10 10"/><path d="M17 8v9H8"/>` (consequência).

### Citação

```html
<div class="gh-block" style="left:120px; right:120px; top:150px; bottom:170px; padding:90px 120px;">
  <div class="gh-block__q">“</div>
  <h2 class="gh-h">O Gov Hub existe para <b>fortalecer a capacidade do Estado</b> de …</h2>
  <!-- opcional: <p class="gh-block__cite">Autor, fonte</p> -->
</div>
```

### Sistemas por parceiro (etiquetas)

```html
<div class="gh-sys" style="top:290px;">
  <p class="gh-sys__k">Sistemas estruturantes do Governo Federal</p>
  <p class="gh-chips"><span class="gh-chip" style="background:#613EFF; color:#fff;">SIAFI</span><!-- … --></p>
</div>
<div class="gh-partners" style="top:560px;">
  <div class="gh-partner"><span class="gh-partner__n">MinC</span><p class="gh-chips"><span class="gh-chip">CultBR</span></p></div>
  <!-- até 5 parceiros -->
</div>
```

### Encerramento

Padrão: título + contato à esquerda, um QR dentro de pílula roxa à
direita, parceiros embaixo.

```html
<section class="gh-slide">
  <svg class="gh-shape" viewBox="0 0 100 50" aria-hidden="true" style="right:160px; top:-1px; width:380px; height:190px;">
    <path fill="#F2F1F6" d="M0 0h100a50 50 0 0 1-100 0z"/>
  </svg>
  <div class="abs" style="left:120px; top:300px; width:1000px;">
    <p class="gh-eyebrow">Saiba mais</p>
    <h2 class="gh-h" style="font-size:96px;">Vamos <b>conversar?</b></h2>
    <p class="gh-lead" style="margin-top:36px; width:820px;">Conheça o Gov Hub e fale com a equipe do Lab Livre: <b>lablivre@unb.br</b></p>
  </div>
  <div class="abs" style="right:0; top:250px; width:700px; height:520px; border-radius:999px 0 0 999px; background:#613EFF;"></div>
  <div class="gh-qr" style="left:1380px; top:330px; width:360px;">
    <div class="gh-qr__box" style="width:360px; height:360px; border:none; background:#fff;"><img src="img/qr.png" alt="QR code"></div>
    <p class="gh-qr__cap" style="color:#fff;">Aponte a câmera</p>
  </div>
  <div class="gh-cover__footer" style="bottom:56px;">
    <img src="logo/logomarca-horizontal-black.svg" alt="Gov Hub">
    <img src="logo/parceiros/lab-livre-black.svg" alt="Lab Livre">
    <img src="logo/parceiros/unb-dark-outlined.svg" alt="UnB">
  </div>
</section>
```

O mesmo bloco de pílula + QR serve para divulgar uma publicação no meio
do deck. Variante com diálogo: `.gh-bubbles` (uma pergunta `--in`, uma
resposta `--out`) no lugar do texto, `.gh-contact` no canto inferior
esquerdo e `.gh-qr` pequeno à direita. Variante com até 3 colunas
(contato, saiba mais, feedback): `.gh-ends` / `.gh-end`, só quando o
usuário pedir; por padrão, **um QR só e sem foto ou nome de pessoa**. Se
o QR ainda não existir, deixe o `.gh-qr__box` tracejado com o texto
"QR code" e avise.

## Armadilhas já cometidas

1. **CSS incompleto quebra slides em silêncio.** Copiar só parte do
   `slides-evento.css` deixou cartões e etiquetas sem estilo (texto
   minúsculo no canto). Copie o arquivo inteiro.
2. **Texto de círculo fora da área visível** quando o círculo sangra pela
   borda: calcule a parte visível (ver "círculo com frase").
3. **Pílula sangrando com texto longo** estoura a largura: até ~45
   caracteres numa pílula de 820px; ajuste `width` ou encurte.
4. **Numeração** fixa no rodapé: ao inserir slide (ex.: agenda), renumere
   tudo.
5. **Diagrama reaproveitado de outro projeto** pode trazer detalhes
   específicos daquele parceiro (ex.: "SIAFI via Tesouro Gerencial" do
   MIR). Avise o usuário.
6. Nome de pessoa, foto e logo de evento na capa ou no encerramento:
   pergunte; o usuário já pediu para tirar quando o deck seria reusado.

## Checklist de conferência visual

(1) número de páginas do PDF = número de `.gh-slide`; (2) títulos com
peso misto e destaque na parte certa; (3) nenhum texto fora de cartão,
círculo ou pílula; (4) no máximo uma forma decorativa e um rosa por slide
de conteúdo; (5) imagens nítidas e sem distorção; (6) numeração contínua;
(7) parceiros na ordem de `partners.md` e versão `-defeso` dos
ministérios quando valer o defeso.

## Histórico

- **2026-10 (Abrelatam/ConDatos 2026):** deck "Interoperabilidade na
  prática" em PT e ES; origem dos componentes, adaptados dos templates de
  post (`social-posts.md`).
- **2026-10 (Oficina MIR):** agenda em 2 colunas e figura grande com
  cabeçalho compacto.
- **2026-11-10:** palestra do Gov Hub (antiga Agile Trends) refeita nesta
  variante; entraram prints/fotos, pipeline em 3 colunas, pilares,
  parceiros em etiquetas e encerramento com um QR só. O usuário pediu
  para tirar nome, foto, QR de feedback, Ipea e o nome do evento.
- **2026-11-12:** registrada como variante na skill, ao lado da sóbria.
