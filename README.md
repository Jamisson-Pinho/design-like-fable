# design-like-fable

> Skill de agente (Claude Skills) para criar sites e landing pages com nível de direção de arte premiada — identidade opinativa, motion design com GSAP, SVG narrativo com critério e copy integrada ao layout.

Criada por [Jamisson Pinho Lima (DevPinho)](https://github.com/Jamisson-Pinho).

## O que ela faz

Transforma o comportamento do modelo em um **protocolo de direção de arte**, não numa base de conhecimento:

- **Ordem inegociável** — sujeito → direção de arte → técnica. A estética nasce do mundo do assunto, nunca de um template
- **Portão anti-genérico** — antes de codar, o plano de tokens é verificado contra uma lista negra empírica de "defaults de IA" (os três looks clássicos, tells de layout, cor, tipo, motion e copy — incluindo os tells internos que a própria skill fabrica)
- **Economia de ousadia** — um único elemento assinatura, escolhido pelo verbo de motion num menu de 7 famílias, com rotação obrigatória entre projetos
- **Checklist binário de pré-entrega** — 12 verificações marcadas por escrito antes de entregar, derivadas de violações reais observadas em testes com modelos de capacidades variadas
- **Cicatrizes reais** — armadilhas de produção (cleanup de ScrollTrigger em React, `dispose()` no Three.js, waypoints flutuantes, conflitos de `dasharray`, `alert()` como validação)
- **Piso de qualidade silencioso** — responsivo a 360px, `prefers-reduced-motion`, foco visível, 60fps, só `transform`/`opacity`

## Estrutura

```
SKILL.md                     → filosofia, processo em 2 passadas, checklist de pré-entrega
references/
├── lista-negra.md           → defaults de IA + tells internos da própria skill
├── motion.md                → menu de famílias de assinatura, decisões GSAP, SVG narrativo
├── threejs.md               → teste do protagonista + budget de performance
├── copy.md                  → persuasão + copy como UX
└── armadilhas.md            → bugs reais de GSAP, Three.js, CSS, forms e Next.js
```

## Instalação

**Claude.ai / Claude Desktop:** empacote a pasta como `.skill` e faça upload em Settings → Skills.

**Claude Code:**

```bash
mkdir -p .claude/skills
git clone https://github.com/Jamisson-Pinho/awwwards-frontend .claude/skills/design-like-fable
```

## Pipeline recomendado

Esta skill executa melhor alimentada por um **Dossiê de Narrativa** (skill `narrativa-de-produto`: entrevista o cliente e extrai a metáfora central via procedimento mecânico) e pode herdar a assinatura pessoal da skill `estilo-devpinho`:

```
narrativa-de-produto  →  design-like-fable | estilo-devpinho  →  página final
     (pensa)                     (constrói)
```

## Filosofia

A página não fala sobre o produto — **ela se torna um objeto do mundo do produto.** Todo o resto deriva daí. E para modelos de diferentes capacidades: **princípio para os fortes, formulário para os fracos** — a skill carrega os dois.

## Licença

MIT
