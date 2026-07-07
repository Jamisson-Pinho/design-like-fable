# Armadilhas — cicatrizes de bugs reais

Erros observados em produção. Leia antes de escrever código com GSAP, Three.js ou CSS complexo. Adicione novas cicatrizes conforme surgirem.

## GSAP

- **ScrollTrigger sem cleanup em React/Next:** todo `ScrollTrigger.create()` ou tween com scrollTrigger dentro de componente PRECISA de `gsap.context()` + `ctx.revert()` no cleanup do `useEffect` (ou o hook `useGSAP` do @gsap/react). Sem isso: triggers duplicados a cada re-render, posições quebradas em navegação SPA
- **`ScrollTrigger.refresh()` após conteúdo assíncrono:** imagens/fonts que carregam depois mudam alturas e desalinham todos os triggers. Chame refresh no `window.load` e após fetches que alteram layout
- **SplitText quebra acessibilidade:** texto fatiado em spans vira ruído para leitor de tela. Adicione `aria-label` com o texto original no elemento pai e `aria-hidden="true"` nos fragmentos
- **Pin dentro de container com `overflow: hidden` ou `transform`:** pin quebra silenciosamente. Pins vivem em ancestrais "limpos"
- **FOUC de elementos animados:** elementos que entram animados devem começar invisíveis via CSS (`visibility: hidden` + `autoAlpha` no GSAP), não via JS — senão piscam antes do JS carregar
- **Tween novo a cada mousemove:** cria centenas de tweens concorrentes. Use `gsap.quickTo()` para tracking de cursor

## SVG path animation

- **`getTotalLength()` em SVG oculto ou não renderizado retorna 0** e a animação morre em silêncio. Meça só depois do SVG estar no DOM e visível (não dentro de `display:none`)
- **`dasharray` de desenho vs `dasharray` de estilo tracejado conflitam:** para desenhar um traço que TERMINA tracejado, anime com `dasharray = comprimento total` e troque para o padrão tracejado ao completar (via callback/ScrollTrigger), nunca os dois ao mesmo tempo
- **`preserveAspectRatio` esquecido:** path desenhado para desktop desalinha das seções em telas estreitas. Defina explicitamente (`xMidYMin meet`) e teste a 360px; em mobile, prefira reposicionar o fio para uma margem lateral
- **Path com `vector-effect` ausente:** stroke escala junto com o viewBox e fica grosso demais em telas pequenas — use `vector-effect="non-scaling-stroke"` quando o traço deve ter espessura constante

## Three.js

- **Canvas sem `dispose()`:** ao desmontar, chame `geometry.dispose()`, `material.dispose()`, `texture.dispose()` e `renderer.dispose()` — senão vaza memória GPU a cada navegação
- **Dois RAF loops (GSAP + Three):** causa jitter. Um loop só: `gsap.ticker.add(render)`
- **`setPixelRatio(window.devicePixelRatio)` sem cap:** em telas 3x renderiza 9x mais pixels. Cap em 2
- **Render loop rodando fora do viewport:** drena bateria. Pause com `IntersectionObserver`
- **Modelos glTF sem compressão Draco:** 15MB de modelo mata o LCP. Comprima sempre

## CSS

- **Especificidades que se cancelam:** `.section { padding: 4rem }` vs `section.cta { padding: 0 }` — o resultado depende de ordem de declaração e vira loteria. Uma convenção só (classes, especificidade plana) e custom properties para variações
- **Espaçamento entre seções duplicado:** padding-bottom da seção A + padding-top da B = buraco de 8rem inexplicável. Decida: espaçamento é responsabilidade de UM lado (ou use `gap` no container pai)
- **`clamp()` com unidade errada no meio:** `clamp(3rem, 8vw, 9rem)` — o valor central em `vw` é o que escala; esquecer isso trava o tamanho
- **`100vh` em mobile:** barra do navegador causa jump. Use `100dvh` com fallback
- **Animar `filter: blur()` ou `box-shadow`:** repaint caro, jank garantido. Glow animado = pseudo-elemento com `opacity` animada
- **Z-index arms race:** valores 9999 empilhados denunciam falta de stacking context planejado. Defina camadas nomeadas em custom properties

## Next.js / React específicos

- **`window`/`document` em SSR:** Three.js e plugins GSAP que tocam DOM só importam client-side (`dynamic import` com `ssr: false` ou dentro de `useEffect`)
- **Registrar plugin GSAP uma vez:** `gsap.registerPlugin(ScrollTrigger)` no módulo, não dentro do componente
- **Fonts com `next/font`:** carregamento manual de webfonts causa FOUT que desloca triggers do ScrollTrigger
