# Motion — linguagem, GSAP e assinatura do autor

Motion não é enfeite: é a voz da página. Antes de animar qualquer coisa, escreva a linguagem de movimento em uma frase, derivada da direção de arte. Ex: "movimentos confiantes e rápidos com overshoot sutil" ou "lentidão cerimonial, nada abaixo de 800ms".

## Princípios

- **Nada anima sozinho.** Toda animação tem relação com outra: coreografia, não efeitos soltos. Um momento orquestrado > dez efeitos espalhados
- **Scroll é a timeline da narrativa.** Se o conteúdo é sequencial, o scroll conta a história (pin + scrub). Se é revelação, batch com stagger
- **Easing é assinatura.** O easing escolhido deve ser reconhecível e consistente no site inteiro. Nunca `ease-in-out` genérico
- **Performance é restrição criativa:** apenas `transform` e `opacity`; `will-change` cirúrgico (aplicar antes, remover depois); jamais animar `width`, `height`, `top`, `left`, `box-shadow`

## Decisões GSAP (condição → técnica)

| Situação | Técnica |
|---|---|
| Narrativa sequencial por scroll | `ScrollTrigger` com `pin: true` + `scrub: 1` |
| Revelação de conteúdo em lista/grid | `ScrollTrigger.batch()` com stagger `0.06–0.1s` |
| Headline com impacto | `SplitText` por palavra ou linha (não por caractere, vira ruído), `y: 100%` + clip |
| Transição de estado/layout | `Flip` plugin |
| Sequência de entrada da página | UMA timeline mestre, não tweens soltos |
| Fio narrativo conectando seções | SVG path que se desenha com scroll (ver "SVG narrativo" abaixo) |
| Ícone/check/selo com vida | SVG stroke animado (`stroke-dashoffset`), nunca GIF/Lottie pesado |
| Elemento seguindo cursor | `quickTo()` (não tween novo por mousemove) |
| Hover micro-interação | CSS puro se simples; GSAP só se precisar de interrupção suave (`overwrite: 'auto'`) |

Regra dura: nunca anime mais de 2 propriedades além de `transform`/`opacity` no mesmo elemento.

## Vocabulário de easing

- `power4.out` — entradas confiantes, padrão para reveals
- `expo.out` — dramaticidade, elementos hero
- `back.out(1.7)` — overshoot com personalidade (ver assinatura abaixo)
- `elastic.out(1, 0.5)` — brincalhão, usar no máximo 1x por página
- Custom bezier — quando a direção pede uma voz própria, crie e use SÓ ela

## Menu de famílias de assinatura

O elemento assinatura NASCE do verbo de motion — nunca de preferência por técnica. Procedimento mecânico: (1) pegue o verbo do projeto; (2) encontre a família cujo movimento MIMETIZA esse verbo; (3) se a família escolhida foi usada no projeto anterior, pegue a segunda melhor. Uma família por projeto.

| Família | Verbo que a justifica | Exemplo |
|---|---|---|
| **Fio que se desenha** | traçar, costurar, percorrer, escoar | rota, costura, curva, assinatura manuscrita |
| **Elemento que bate** | carimbar, cravar, martelar, selar | carimbos, selos, etiquetas que chegam com impacto |
| **Elemento vivo** | observar, acompanhar, reagir | mascote/ícone com proximity awareness |
| **Tipografia cinética** | pesar, crescer, gritar, respirar | variable font animada, display reagindo ao scroll |
| **Revelação material** | descobrir, revelar, abrir, descascar | máscaras/clip-path descobrindo conteúdo por camadas |
| **Mudança de estado global** | atravessar, amanhecer, mergulhar, virar | fundo/tema da página inteira transiciona com o scroll |
| **Objeto protagonista** | girar, montar, examinar | objeto central (3D ou sprite) manipulado pelo scroll — só se passar no teste do protagonista |

Sinal de alerta: se você escolheu a família ANTES de definir o verbo, está escolhendo por hábito. Verbos sóbrios (acolher, organizar, esclarecer) frequentemente apontam para "revelação material" ou "mudança de estado" em dose mínima — ou para assinatura tipográfica estática, sem motion nenhum. Nem todo projeto premiado tem um efeito; alguns têm só uma decisão.

## SVG narrativo — o desenho que conta a história

Técnica de alto impacto e custo quase zero: um `<path>` SVG que se desenha conforme o usuário rola, funcionando como fio condutor entre seções (uma rota, um traço de caneta, um circuito, uma linha do tempo, uma raiz crescendo — a metáfora vem do MUNDO DO SUJEITO). É frequentemente a melhor resposta quando 3D é tentador mas reprovaria no teste do protagonista: conta a mesma história pesando nada.

**Receita canônica (stroke-dashoffset + scrub):**
```js
const path = document.querySelector('#fio');
const len = path.getTotalLength();
gsap.set(path, { strokeDasharray: len, strokeDashoffset: len });
gsap.to(path, {
  strokeDashoffset: 0,
  ease: 'none', // scrub dita o ritmo, não o easing
  scrollTrigger: { trigger: '.secao', start: 'top 70%', end: 'bottom 55%', scrub: 1 }
});
```

**Regras de uso:**
- O path é desenhado à mão no viewBox (curvas `C`/`S` serpenteando entre as colunas de conteúdo), posicionado absoluto atrás do conteúdo (`pointer-events: none`), com âncoras visuais (pontos/marcadores) onde ele "para" em cada seção
- Se o traço final deve ser tracejado (rota, costura), anime com `dasharray = comprimento total` e restaure o padrão tracejado ao completar — os dois efeitos usam a mesma propriedade e conflitam se aplicados juntos
- Variações da mesma família: assinatura manuscrita se escrevendo, sublinhado desenhado sob a palavra-chave do headline, contorno de ilustração se revelando, check de confirmação (`stroke` curto + `back.out`)
- Mobile: reposicione o path para uma margem lateral (viewBox estreito) em vez de escondê-lo — o fio narrativo é conteúdo, não decoração
- Quando considerar usar: o verbo de motion é da família do traço (traçar, costurar, percorrer) E a página tem 3+ seções que formam jornada sequencial real E o projeto anterior não usou fio. Quando NÃO usar: verbo de outra família, seções paralelas sem sequência, ou como reflexo — **esta técnica é o default interno mais tentador desta skill; trate-a como candidata entre iguais no menu de famílias, e desconfie sempre que ela for sua primeira ideia**

## ★ Assinatura de motion do autor

Preferências pessoais consolidadas de projetos anteriores. Quando o brief não impõe outra linguagem, esta é a voz default — mas sujeita à economia de ousadia: escolha 1–2 destes elementos por projeto, não todos.

**1. Overshoot como personalidade.**
Easing assinatura: `cubic-bezier(0.34, 1.56, 0.64, 1)` (equivalente GSAP: `back.out(1.7)`). Entradas de elementos "vivos" — mascotes, chips, cards interativos — passam do ponto e voltam. Transmite energia e simpatia sem infantilizar.

**2. Elementos que reagem ao usuário (proximity awareness).**
Componentes com "consciência" do cursor: rotação direcional apontando para o mouse quando ele entra num raio (~150px), cálculo via `Math.atan2`, com transição suave na entrada e `quickTo()` no tracking. Herança dos mascotes estilo Octocat: rotação com eixo correto + blink animation em intervalos aleatórios (3–7s). Usar em mascotes, ícones hero ou no elemento assinatura — nunca em tudo.

**3. Stagger conversacional.**
Conteúdo que entra como conversa: bolhas/cards aparecendo em sequência com delay entre 300–600ms, cada um com scale de 0.95→1 + fade + leve y. Indicador de "digitando" (três pontos pulsando) antes de conteúdo importante. Ideal para forms interativos, depoimentos, fluxos de onboarding.

**4. Celebração em conversão.**
O momento de conversão (form enviado, acordo aceito, meta atingida) merece recompensa visual: confetti direcional, check com stroke animado (SVG `stroke-dashoffset`), ou pulso de glow. Curto (<2s), uma vez só, nunca em loop.

**5. Glow ambiente em dark themes.**
Em direções dark-tech: radial-gradients de accent com opacidade baixa (0.12–0.22) posicionados atrás de elementos-chave, respirando lentamente (scale 1→1.08, 6–8s, `ease: sine.inOut`, yoyo). Atmosfera, não protagonismo.

**6. SVG narrativo como fio condutor.**
Preferência forte do autor: quando a página tem uma jornada sequencial, o elemento assinatura default é um path SVG que se desenha com o scroll conectando as etapas (técnica na seção "SVG narrativo" acima). A metáfora do traço sempre deriva do sujeito — rota náutica para logística, traço de caneta para editorial, circuito para tech, linha de costura para moda.

**Aplicação da assinatura:** se a direção de arte é dark-tech/produto digital → itens 2, 3 ou 5 são candidatos a assinatura. Se é institucional sóbrio → apenas o item 1 em dose homeopática, ou nada. A assinatura serve à direção, nunca o contrário.

## Acessibilidade de motion

```css
@media (prefers-reduced-motion: reduce) {
  /* motion decorativo: OFF. Transições funcionais: fade 150ms */
}
```
Em GSAP: `gsap.matchMedia()` com a query de reduced-motion definindo o set alternativo. Isso faz parte do piso de qualidade, não é opcional.
