# Changelog

## 1.0.1 — 2026-08-20

Fix antes do primeiro consumo real: `--font-sans` estava solto dentro de `:root`, fora de
qualquer bloco `@theme`. No Tailwind v4 isso NÃO gera a utility `font-sans` — a fonte cairia
em silêncio pro fallback do sistema, exatamente o bug que este pacote existe pra evitar. Movido
para `@theme { --font-sans: ...; }`.

## 1.0.0 — 2026-08-20

Primeira versão. Tokens extraídos 1:1 do RescueDeck (`rescuedeck-producao`), único dos três
sistemas onde a cor declarada no token batia com a cor realmente usada na tela.

- Cor primária: teal `#00645F` (`oklch(0.42 0.08 175)`), com `--primary-hover` para os dois
  modos claro/escuro.
- Fonte: Ubuntu (300/400/500/700).
- Raio: `0.75rem`.
- Paleta de gráfico (`--chart-1..5`) derivada da matiz 175, não de azul genérico.
- Escala `--color-teal-50..950` e `--color-ocre-400` (accent secundário do RescueDeck).
