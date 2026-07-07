# Three.js / WebGL — decidir antes de usar

Leia este arquivo ANTES de decidir usar 3D. Ele existe principalmente para te ajudar a decidir CONTRA.

## O teste do protagonista

3D só entra se for **protagonista da experiência** — o elemento assinatura em si. Um blob 3D decorativo no canto é custo (peso, bateria, complexidade) sem retorno, e é tell de IA. Perguntas de corte:

1. O sujeito tem uma dimensão física/espacial real? (produto físico, arquitetura, dados espaciais → sim; SaaS de planilha → provavelmente não)
2. A experiência 3D substituiria o hero inteiro, não decoraria ele?
3. Você aceita gastar TODA a economia de ousadia aqui? (3D + outras assinaturas = árvore de Natal)

Três "sim" → prossiga. Qualquer "não" → considere alternativas: SVG animado, vídeo, CSS 3D transforms (perspective + rotateX/Y são suficientes para 80% dos efeitos "3D" premiados).

## Budget de performance (inegociável)

- 60fps em mobile médio ou corta a feature
- Carregamento lazy: Three.js só baixa após LCP, via dynamic import quando a seção se aproxima do viewport
- `renderer.setPixelRatio(Math.min(devicePixelRatio, 2))` — nunca acima de 2
- Pausar o render loop quando o canvas sai do viewport (`IntersectionObserver`)
- Fallback estático elegante (imagem/SVG da mesma cena) para WebGL indisponível e reduced-motion

## Padrões que funcionam em sites premiados

| Efeito | Abordagem |
|---|---|
| Objeto hero rotacionando com scroll | Modelo glTF comprimido (Draco) + rotação mapeada ao progresso do ScrollTrigger |
| Distorção de imagem no hover | Plane + shader com uv displacement (fragment shader simples) |
| Partículas reagindo ao cursor | `Points` + `BufferGeometry`, máx ~10k partículas mobile / 50k desktop |
| Texto 3D | Evite `TextGeometry` (pesado); prefira texto HTML sobreposto ao canvas |
| Material com aparência premium | `MeshPhysicalMaterial` + environment map (HDRI pequeno) > luzes múltiplas |

## Shaders — dose mínima

Um fragment shader de 20 linhas (noise + distorção de uv + mix de cores da paleta) produz mais "wow" que uma cena complexa. Use as cores do plano de tokens como uniforms — o shader pertence à direção de arte, não flutua fora dela.

## Integração com GSAP

- GSAP anima uniforms e propriedades de objetos 3D normalmente: `gsap.to(mesh.rotation, {...})`
- Um único `requestAnimationFrame` loop: o do Three.js. GSAP tem seu próprio ticker — sincronize com `gsap.ticker.add(render)` em vez de dois loops
