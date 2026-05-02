---
name: instagram-carousel
description: Cria carrosséis para Instagram com mockup visual interativo, exportação em PNG por slide, em português. Use esta skill SEMPRE que o usuário pedir para criar um carrossel, post em sequência, slides para Instagram, conteúdo em carrossel, ou qualquer variação como "faz um carrossel sobre X", "cria slides para o Instagram", "quero postar um carrossel", "transforma esse texto em carrossel". Também use quando o usuário quiser transformar um artigo, texto ou tema em formato de carrossel visual. A skill conduz uma entrevista rápida para garantir que o conteúdo e visual estejam certeiros antes de gerar qualquer imagem. Não use para Stories isolados, Reels ou posts simples de imagem única.
---

# Instagram Carousel Skill

Cria carrosséis para Instagram em português: entrevista o usuário, gera mockup interativo para aprovação, exporta PNGs individuais por slide. Legenda e hashtags são responsabilidade de outra skill (`instagram-caption`).

---

## Fluxo obrigatório

```
1. ENTREVISTA     → coletar conteúdo + direção visual
2. ESTRUTURA      → propor número de slides e roteiro
3. MOCKUP         → gerar preview interativo para aprovação
4. AJUSTES        → iterar até aprovação
5. EXPORTAÇÃO     → gerar PNGs individuais de cada slide
```

Nunca pule etapas. Nunca gere PNGs sem aprovação explícita do mockup.

---

## ETAPA 1 — Entrevista

Antes de qualquer coisa, faça as perguntas abaixo. Se o usuário já forneceu alguns dados na conversa, não repita — preencha o que falta.

### Perguntas obrigatórias (faça todas de uma vez, de forma conversacional):

**Sobre o conteúdo:**
1. Qual é o tema ou objetivo do carrossel? (ex: dicas, tutorial, lançamento, história, tendência)
2. Qual é a mensagem principal que o leitor deve levar?
3. Tem texto, artigo ou tópicos prontos para usar — ou quer que eu crie tudo do zero?

**Sobre o público e tom:**
4. Para quem é esse conteúdo? (ex: empreendedores, jovens, mães, profissionais de saúde)
5. Qual é o tom? (ex: educativo, inspiracional, divertido, autoridade, próximo/informal)

**Sobre o visual:**
6. Tem identidade visual definida (cores, fontes, logo)? Se sim, descreva ou mencione a skill de identidade visual.
7. Tem referências visuais ou estilos que admira? (ex: minimalista, colorido, tipográfico, fotográfico)
8. Vai usar fotos/imagens reais ou prefere ilustrações e formas geométricas?

**Sobre o formato:**
9. Qual proporção prefere para os slides?
   - **1:1** (1080×1080px) — quadrado, clássico
   - **4:5** (1080×1350px) — retrato, ocupa mais espaço no feed e gera mais atenção
10. Tem alguma preferência de quantos slides? (ou deixa flexível)
11. O slide de capa já tem um título definido — ou quer sugestões?

> Se o usuário estiver com pressa ou disser "vai lá", use defaults razoáveis e informe as escolhas feitas.

---

## ETAPA 2 — Estrutura do carrossel

Com base na entrevista, proponha a estrutura antes de gerar o mockup:

```
Slide 1 — CAPA         → título impactante + gancho visual
Slide 2 — INTRODUÇÃO   → contexto / problema
Slides 3-N — CONTEÚDO  → um ponto por slide, direto ao ponto
Slide final — CTA      → chamada para ação clara
```

Apresente o roteiro resumido (título de cada slide) e peça confirmação antes de avançar.

---

## ETAPA 3 — Mockup interativo

Gere um **artifact HTML interativo** que simula o carrossel como seria no Instagram.

### Especificações técnicas do mockup:

**Dimensões:** conforme o formato escolhido na entrevista:
- 1:1 → 1080×1080px (quadrado)
- 4:5 → 1080×1350px (retrato)

Escale o mockup para caber na tela mantendo a proporção correta.
**Navegação:** botões anterior/próximo, indicador de slide atual (ex: "2/6")
**Interface:** fundo escuro ao redor simulando o feed do Instagram

### Diretrizes visuais do mockup:

Siga os princípios da skill `frontend-design`:
- Escolha uma direção estética clara e execute com precisão
- Tipografia distintiva — nunca Inter, Roboto ou Arial
- Hierarquia visual forte: título dominante, subtítulo secundário, texto corpo pequeno
- Composição com intenção: assimetria, espaço em branco generoso, elementos âncora
- Paleta coesa com no máximo 3 cores principais + 1 cor de destaque
- Cada slide deve ter identidade visual consistente com os demais

### Estrutura de cada slide:

```
┌─────────────────────────────┐
│  [logo/marca — pequeno]     │
│                             │
│  TÍTULO GRANDE              │
│  subtítulo se necessário    │
│                             │
│  corpo de texto curto       │
│  (máx. 2-3 linhas)          │
│                             │
│  [elemento visual/ícone]    │
│                             │
│  @handle — número do slide  │
└─────────────────────────────┘
```

**Regras de copy por slide:**
- Capa: título de até 8 palavras, máximo impacto
- Slides de conteúdo: máximo 40 palavras por slide
- CTA final: 1 ação clara + @handle ou link

### Qualidade do mockup:

O mockup deve parecer profissional o suficiente para o usuário conseguir avaliar se aprovaria ou não para publicação. Não é um wireframe — é um preview real.

---

## ETAPA 4 — Iteração

Após mostrar o mockup, pergunte:

> "O que você quer ajustar? Posso mudar cores, tipografia, copy, layout, número de slides ou qualquer outra coisa antes de exportar."

Itere até o usuário aprovar explicitamente com algo como "aprovado", "pode exportar", "gostei", "tá bom".

---

## ETAPA 5 — Exportação em PNG

Após aprovação, gere cada slide como arquivo PNG individual usando Python + html2image ou Playwright.

### Script de exportação:

Use as dimensões corretas conforme o formato escolhido:
- 1:1 → `width=1080, height=1080`
- 4:5 → `width=1080, height=1350`

```python
# Instalar dependência
# pip install html2image --break-system-packages

from html2image import Html2Image

# Ajuste width/height conforme o formato escolhido (1:1 ou 4:5)
WIDTH, HEIGHT = 1080, 1080   # 1:1
# WIDTH, HEIGHT = 1080, 1350  # 4:5

hti = Html2Image(output_path='/mnt/user-data/outputs/', size=(WIDTH, HEIGHT))

slides_html = [
    # lista de HTML strings, uma por slide
]

for i, html in enumerate(slides_html, 1):
    hti.screenshot(
        html_str=html,
        save_as=f'slide_{i:02d}.png'
    )
    print(f'Slide {i} exportado.')
```

Se `html2image` não estiver disponível, use `Playwright`:

```python
# pip install playwright --break-system-packages
# python -m playwright install chromium

from playwright.sync_api import sync_playwright

# Ajuste conforme o formato escolhido (1:1 ou 4:5)
WIDTH, HEIGHT = 1080, 1080   # 1:1
# WIDTH, HEIGHT = 1080, 1350  # 4:5

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = browser.new_page(viewport={'width': WIDTH, 'height': HEIGHT})
    
    for i, html in enumerate(slides_html, 1):
        page.set_content(html)
        page.screenshot(path=f'/mnt/user-data/outputs/slide_{i:02d}.png')
        print(f'Slide {i} exportado.')
    
    browser.close()
```

### Nomenclatura dos arquivos:

```
slide_01.png  ← capa
slide_02.png
slide_03.png
...
slide_NN.png  ← CTA
```

Após exportar, use `present_files` para entregar todos os PNGs ao usuário.

---

## Integração com outras skills

### Identidade visual (`vanguardia-visual-identity` ou equivalente):
Quando a skill de identidade visual estiver disponível, leia-a **antes da etapa de mockup** para extrair:
- Paleta de cores (primária, secundária, destaque, fundo)
- Fontes (display, corpo)
- Elementos de marca (logo, padrões, ícones)
- Tom visual geral

Aplique essas definições no mockup. Se a skill não existir, pergunte ao usuário ou use um estilo limpo e neutro.

### Legenda e hashtags (`instagram-caption`):
Esta skill **não gera** legenda nem hashtags. Ao finalizar a exportação, informe:
> "Os slides estão prontos! Para gerar a legenda e as hashtags, use a skill `instagram-caption` com o tema e contexto desse carrossel."

---

## Integração com pasta local (extensão futura)

Para fluxos automatizados com acesso a arquivos locais, esta skill pode ser usada com:
- **Claude Code + MCP Filesystem**: leitura de briefings em `/carousel-inputs/` e salvamento de PNGs em `/carousel-outputs/`
- **Claude in Chrome**: upload de arquivos e download dos PNGs gerados

Documente o caminho de entrada e saída no projeto quando essa integração for configurada.

---

## Defaults quando o usuário não especifica

| Parâmetro | Default |
|---|---|
| Formato | 4:5 (1080×1350px) — melhor desempenho no feed |
| Número de slides | 6 a 8 |
| Tom | Educativo e próximo |
| Estilo visual | Tipográfico, minimalista |
| Cores | Neutro escuro + 1 cor de destaque vibrante |
| Handle | @handle (placeholder) |
| Fonte | Escolha distintiva conforme tema |

---

## O que nunca fazer

- Nunca gerar PNGs sem aprovação do mockup
- Nunca usar fontes genéricas (Inter, Roboto, Arial, system-ui)
- Nunca colocar mais de 40 palavras em um slide de conteúdo
- Nunca gerar legenda ou hashtags (responsabilidade da `instagram-caption`)
- Nunca assumir identidade visual sem perguntar ou ler a skill correspondente
