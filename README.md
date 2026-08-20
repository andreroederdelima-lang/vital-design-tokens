# vital-design-tokens

Fonte única de verdade dos tokens de marca da Vital: cor primária (`#00645F`), fonte (Ubuntu),
raio de borda e paleta de gráfico. Consumido pelos frontends `plataforma.comissao.vital`,
`vital-credenciados` e `rescuedeck-producao`.

## Por que este repo existe

Os três sistemas usam a mesma stack (Tailwind v4 CSS-first + shadcn "new-york") sem terem sido
combinados, e cada um foi divergindo: o token declarado dizia uma cor, a tela usava outra (hex
copiado à mão, cada cópia se afastando um pouco mais). Este pacote existe para ser a única cópia
— trocar cor/fonte da marca é editar `tokens.css`, taggear uma versão nova; cada repo faz bump
quando quiser.

## Como consumir

```json
// package.json
"dependencies": {
  "vital-design-tokens": "github:andreroederdelima-lang/vital-design-tokens#v1.0.0"
}
```

```css
/* client/src/index.css — logo após @import "tailwindcss" */
@import "vital-design-tokens/tokens.css";
```

Depois do `@import`, remova do `:root`/`.dark` locais os tokens que passam a vir daqui:
`--font-sans`, `--primary`, `--primary-foreground`, `--primary-hover`, `--sidebar-primary`,
`--sidebar-primary-foreground`, `--chart-1..5`, `--radius`, e a escala `--color-teal-*`/
`--color-ocre-400`. Tokens neutros (`--background`, `--foreground`, `--border`, `--muted`,
`--sidebar`) e o wiring `@theme inline` continuam locais a cada repo.

## Fonte (Ubuntu) — snippet de `index.html`

Cole dentro de `<head>`, com o mesmo padrão não-bloqueante já provado em produção no RescueDeck:

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  rel="preload"
  as="style"
  href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500;700&display=swap"
/>
<link
  rel="stylesheet"
  href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500;700&display=swap"
  media="print"
  onload="this.media='all'"
/>
<noscript>
  <link
    rel="stylesheet"
    href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500;700&display=swap"
  />
</noscript>
```

Um check de CI em cada repo consumidor deve grepar por `family=Ubuntu` em `index.html` — é assim
que o bug original aconteceu no comissao.vital: o bloco de fonte ficou comentado e ninguém notou.

## Bump de versão

Tag nova (`vX.Y.Z`) no `main` deste repo. Cada consumidor decide quando atualizar sua própria
dependência — nada propaga sozinho. Registre a mudança em `CHANGELOG.md`.

## O que NÃO está aqui, de propósito

- Segunda cor de marca (bege/ocre "oficial") — cada sistema hoje usa um hex diferente
  (`#B5AE94` RescueDeck, `#D4C5A0` comissao.vital, `#C6BCA4` só em doc arquivada no
  credenciados) e não há decisão fechada de qual é a certa. Fica como token local nomeado
  (`--color-accent-warm`) em cada repo até essa escolha ser feita.
- Escala de sombra/elevação — nenhum drift foi encontrado; os três usam as utilities padrão do
  Tailwind.
- Componentes React — este pacote é só tokens CSS, não uma biblioteca de componentes.
