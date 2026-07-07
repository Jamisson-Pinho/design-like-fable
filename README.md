# awwwards-frontend

> Skill de agente (Claude Skills) para criar sites e landing pages com nível de direção de arte Awwwards — identidade opinativa, motion design com GSAP, SVG narrativo, Three.js com critério e copy integrada ao layout.

Criada por [Jamisson Pinho Lima (DevPinho)](https://github.com/Jamisson-Pinho).

## O que ela faz

Transforma o comportamento do modelo em um **protocolo de direção de arte**, não numa base de conhecimento:

- **Ordem inegociável** — sujeito → direção de arte → técnica. A estética nasce do mundo do assunto, nunca de um template
- **Portão anti-genérico** — antes de codar, o plano de tokens é verificado contra uma lista negra empírica de "defaults de IA" (os três looks clássicos, tells de layout, cor, tipo, motion e copy)
- **Economia de ousadia** — um único elemento assinatura memorável; todo o resto quieto e disciplinado
- **SVG narrativo** — receita canônica do fio que se desenha com o scroll (`getTotalLength` + `strokeDashoffset` + scrub) como assinatura default para jornadas sequenciais
- **Motion com voz** — tabela de decisão GSAP, vocabulário de easing e assinatura pessoal de movimento com regra de dose
- **Cicatrizes reais** — armadilhas de produção (cleanup de ScrollTrigger em React, `dispose()` no Three.js, conflitos de `dasharray`, especificidade CSS)
- **Piso de qualidade silencioso** — responsivo a 360px, `prefers-reduced-motion`, foco visível, 60fps, só `transform`/`opacity`

## Estrutura

```
SKILL.md                     → filosofia, processo em 2 passadas, portões
references/
├── lista-negra.md           → defaults de IA catalogados (consulta obrigatória)
├── motion.md                → decisões GSAP, SVG narrativo, assinatura de motion
├── threejs.md               → teste do protagonista + budget de performance
├── copy.md                  → persuasão + copy como UX
└── armadilhas.md            → bugs reais de GSAP, Three.js, CSS e Next.js
```

## Instalação

**Claude.ai / Claude Desktop:** empacote a pasta como `.skill` e faça upload em Settings → Skills (ou use o [skill-creator](https://docs.claude.com) para empacotar).

**Claude Code:** copie a pasta para o diretório de skills do projeto:

```bash
mkdir -p .claude/skills
git clone https://github.com/Jamisson-Pinho/awwwards-frontend .claude/skills/awwwards-frontend
```

## Pipeline recomendado

Esta skill executa melhor quando alimentada por um **Dossiê de Narrativa** (skill `narrativa-de-produto`, que entrevista o cliente e extrai a metáfora central via procedimento mecânico) e pode herdar a assinatura pessoal da skill `estilo-devpinho`:

```
narrativa-de-produto  →  awwwards-frontend | estilo-devpinho  →  página final
     (pensa)                    (constrói)
```

## Filosofia

A página não fala sobre o produto — **ela se torna um objeto do mundo do produto.** Todo o resto deriva daí.

## Licença

MIT
