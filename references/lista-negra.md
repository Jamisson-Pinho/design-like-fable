# Lista Negra — Defaults que denunciam design de IA

Estes padrões são legítimos para ALGUNS briefs, mas aparecem independente do sujeito — são defaults, não escolhas. Se o brief pedir explicitamente um deles, as palavras do brief sempre vencem. Se o brief deixa o eixo livre, NÃO gaste essa liberdade num item desta lista.

## Os três looks clássicos de IA

1. **Creme editorial**: fundo creme quente (~#F4F1EA), serif display de alto contraste, accent terracota/argila (~#D97757 — que é o accent da própria Anthropic, então num brief de cliente lê-se como assinatura de IA)
2. **Dark + ácido**: fundo quase-preto com UM accent verde-ácido ou vermelhão
3. **Broadsheet**: layout tipo jornal, hairline rules, border-radius zero, colunas densas

## Tells de layout

- Hero centralizado: badge/eyebrow em cima + headline + subheadline + dois botões (primário sólido + secundário ghost) lado a lado
- Número grande com label pequeno + 3 estatísticas de apoio + gradiente de accent — só use se for genuinamente a melhor opção
- Grid de 3 cards com ícone, título e parágrafo — o layout mais gerado do planeta
- Seção "logos de clientes" em cinza dessaturado logo abaixo do hero
- Footer de 4 colunas idêntico em qualquer site

## Tells de cor e efeito

- Gradiente roxo→azul (ou roxo→rosa) em botões, textos ou blobs
- Glassmorphism (blur + borda translúcida) espalhado sem motivo
- Sombras `box-shadow: 0 4px 6px rgba(0,0,0,0.1)` em tudo
- Blobs orgânicos animados flutuando no fundo do hero
- Grid de pontos ou linhas tech no background "porque é tech"

## Tells de tipografia

- Inter para tudo (ou Inter + Inter). Inter é excelente — como utility, não como personalidade
- Poppins como "toque amigável" default
- Space Grotesk como "toque tech" default
- Headline com UMA palavra em cor de accent ou itálico ("Build something *amazing*")

## Tells de motion

- Tudo com fade-up ao entrar no viewport, mesmo delay, mesmo easing
- `ease-in-out` genérico em tudo
- Parallax sutil no hero "porque sim"
- Contadores numéricos animados em estatísticas
- Typewriter effect no headline

## Tells de copy

- "Transforme seu negócio", "Leve sua empresa ao próximo nível", "Soluções inovadoras"
- Headline que descreve a categoria do produto em vez de criar tensão ou promessa
- CTA "Saiba mais" / "Get Started" sem contexto
- Três adjetivos vazios em sequência ("rápido, seguro e confiável")

## Tells internos desta skill (defaults fabricados em casa)

Padrões que ESTA skill tende a repetir entre projetos — o mesmo teste da inércia se aplica:
- Fio SVG serpenteando entre seções, em qualquer projeto, com qualquer verbo — o fio só é legítimo se o verbo de motion for da família do traço E houver jornada sequencial real de 3+ etapas
- Coordenadas/labels em fonte mono como eyebrow — poderoso quando codifica dado real, tique quando vira decoração
- Repetir a família de assinatura do projeto anterior — rotação é obrigatória
- Ao notar um novo padrão repetindo entre gerações desta skill, adicione-o aqui

## Como usar esta lista

No portão anti-genérico, passe cada item do seu plano de tokens por esta lista. Para cada coincidência, pergunte: "escolhi isso PARA este sujeito ou cheguei aqui por inércia?" Se a resposta honesta for inércia, revise e registre o que mudou.

Esta lista deve crescer: ao notar um novo padrão repetitivo nas próprias gerações, adicione-o aqui.
